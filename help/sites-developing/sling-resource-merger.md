---
title: AEM での Sling Resource Merger の使用
seo-title: AEM での Sling Resource Merger の使用
description: Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します
seo-description: Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# AEM での Sling Resource Merger の使用{#using-the-sling-resource-merger-in-aem}

## 目的 {#purpose}

Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します。Sling Resource Merger は、次の両方に対して差分メカニズムを提供します。

* [設定済みの検索パス](/help/sites-developing/overlays.md#configuring-the-search-paths)を使用するリソースの&#x200B;**[オーバーレイ](/help/sites-developing/overlays.md)**。

* リソースタイプ階層を（**プロパティを通じて）使用するタッチ操作対応 UI のコンポーネントダイアログ（**）の`cq:dialog`オーバーライド`sling:resourceSuperType`。

Sling Resource Merger を使用すると、リソースやプロパティのオーバーレイ／オーバーライドが元のリソース／プロパティにマージされます。

* カスタマイズされた定義のコンテンツの方が、元の定義のコンテンツよりも優先されます（つまり、前者が後者をオーバーレイまたはオーバーライドします）。****

* 必要な場合には、カスタマイズされた定義に含まれる[プロパティ](#properties)が、元の定義からマージされたコンテンツをどう使用するかを指定します。

>[!CAUTION]
>
>Sling Resource Merger および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) に対してのみ使用できます。これはつまり、標準のタッチ操作対応 UI でのみ使用できるという意味です。特に、この方法で定義された特定のオーバーライドは、コンポーネントのタッチ操作対応ダイアログに対してのみ適用できます。
>
>その他の領域（タッチ操作対応コンポーネントやクラシック UI の他の側面を含む）のオーバーレイ／オーバーライドでは、適切なノードと構造を元の場所からカスタマイズの定義先にコピーします。

### AEM の目的 {#goals-for-aem}

AEM で Sling Resource Merger を使用する目的は、次のとおりです。

* ensure that customization changes are not made in `/libs`.
* reduce the structure that is replicated from `/libs`.

   When using the Sling Resource Merger it is not recommended to copy the entire structure from `/libs` as this would result in too much information being held in the customization (usually `/apps`). 情報を不必要に複製すると、システムのアップグレード時に問題が発生しやすくなります。

>[!NOTE]
>
>オーバーライドは、検索パスに依存せず、`sling:resourceSuperType` プロパティに基づいて接続を確立します。
>
>However, overrides are often defined under `/apps`, as best practice in AEM is to define customizations under `/apps`; this is because you must not change anything under `/libs`.

>[!CAUTION]
>
>You ***must*** not change anything in the `/libs` path.
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
   >
   >
1. Make any changes within `/apps`
>



### プロパティ {#properties}

リソースマージャーには次のプロパティがあります。

* `sling:hideProperties` ( `String` または `String[]`)

   非表示にするプロパティ、またはプロパティのリストを指定します。

   The wildcard `*` hides all.

* `sling:hideResource` ( `Boolean`)

   リソースの子を含め、リソースを完全に非表示にするかどうかを示します。

* `sling:hideChildren` ( `String` または `String[]`)

   非表示にする子ノード、または子ノードのリストが含まれます。 ノードのプロパティは維持されます。

   The wildcard `*` hides all.

* `sling:orderBefore` ( `String`)

   現在のノードを前に配置する兄弟ノードの名前が含まれます。

These properties affect how the corresponding/original resources/properties (from `/libs`) are used by the overlay/override (often in `/apps`).

### 構造の作成 {#creating-the-structure}

To create an overlay or override you need to recreate the original node, with the equivalent structure, under the destination (usually `/apps`). 次に例を示します。

* オーバーレイ

   * パネルに表示される、サイトコンソールのナビゲーションエントリの定義は、次の場所で定義されます。

      `/libs/cq/core/content/nav/sites/jcr:title`

   * これをオーバーレイするには、次のノードを作成します。

      `/apps/cq/core/content/nav/sites`

      次に、必要に応じてプロパティ `jcr:title` を更新します。

* オーバーライド

   * テキストコンソール用のタッチ対応ダイアログの定義は、次の場所で定義されます。

      `/libs/foundation/components/text/cq:dialog`

   * これを上書きするには、例えば次のノードを作成します。

      `/apps/the-project/components/text/cq:dialog`

これらのいずれを作成する場合も、必要な作業はスケルトン構造を再作成することだけです。To simplify the recreation of the structure all intermediary nodes can be of type `nt:unstructured` (they do not have to reflect the original node type; for example, in `/libs`).

上述のオーバーレイの例では、次のノードが必要になります。

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>When using the Sling Resource Merger (i.e. when dealing with the standard, touch-enabled UI) it is not recommended to copy the entire structure from `/libs` as it would result in too much information being held in `/apps`. その場合、システムが何らかの理由でアップグレードされたときに問題が発生する可能性があります。

### ユースケース {#use-cases}

オーバーレイを標準の機能と合わせることで、次の操作が可能になります。

* **プロパティの追加**

   The property does not exist in the `/libs` definition, but is required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. このノード「

* **プロパティの再定義（自動作成されたプロパティ以外）**

   The property is defined in `/libs`, but a new value is required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. このノード（`apps` 以下）で対応するプロパティを作成します。

      * このプロパティには、Sling Resource Resolver 設定に基づいた優先順位が付けられます。
      * プロパティタイプの変更がサポートされています。

         If you use a property type different to the one used in `/libs`, then the property type you define will be used.
   >[!NOTE]
   >
   >プロパティタイプの変更がサポートされています。

* **自動作成されたプロパティの再定義**

   By default, auto-created properties (such as `jcr:primaryType`) are not subject to an overlay/override to ensure that the node type currently under `/libs` is respected. To impose an overlay/override you have to recreate the node in `/apps`, explicitly hide the property and redefine it:

   1. Create the corresponding node under `/apps` with the desired `jcr:primaryType`
   1. 自動作成され `sling:hideProperties` たプロパティの値に設定したプロパティを、そのノードに作成します。例えば、 `jcr:primaryType`

      このプロパティは、で定義さ `/apps`れ、現在は、 `/libs`

* **ノードおよびその子の再定義**

   The node and its children are defined in `/libs`, but a new configuration is required in the `/apps` overlay/override.

   1. 次のアクションを両方実行します。

      1. ノードの子を非表示にします（そのノードのプロパティは維持されます）。
      1. プロパティを再定義します。

* **プロパティの非表示**

   The property is defined in `/libs`, but not required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. またはのタイプのプ `sling:hideProperties` ロパティを作 `String` 成しま `String[]`す。 これを使用して、非表示にする（無視する）プロパティを指定します。ワイルドカードを使用することもできます。次に例を示します。

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **ノードおよびその子の非表示**

   The node and its children are defined in `/libs`, but not required in the `/apps` overlay/override.

   1. /apps 以下に、対応するノードを作成します。
   1. Create a property `sling:hideResource`

      * type: `Boolean`
      * 値: `true`

* **ノードの子の非表示（そのノードのプロパティは維持）**

   The node, its properties and its children are defined in `/libs`. The node and its properties are required in the `/apps` overlay/override, but some or all of the child nodes are not required in the `/apps` overlay/override.

   1. Create the corresponding node under `/apps`
   1. プロパティを作成しま `sling:hideChildren`す。

      * type: `String[]`
      * value: a list of the child nodes (as defined in `/libs`) to hide/ignore
      ワイルドカード(&amp;ast;)は、すべての子ノードを非表示/無視するために使用できます。


* **ノードの並べ替え**

   The node and its siblings are defined in `/libs`. A new position is required so the node is recreated in the `/apps` overlay/override, where the new position is defined in reference to the appropriate sibling node in `/libs`.

   * Use the `sling:orderBefore` property:

      1. Create the corresponding node under `/apps`
      1. プロパティを作成しま `sling:orderBefore`す。

         これは、現在のノードを配置する前のノ `/libs`ードを指定します（例：）。

         * type: `String`
         * 値: `<before-SiblingName>`

### コードからの Sling Resource Merger の呼び出し {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger には 2 つのカスタムリソースプロバイダーが含まれています。1 つはオーバーレイ用、もう 1 つはオーバーライド用です。それぞれはコード内でマウントポイントを使用して呼び出すことができます。

>[!NOTE]
>
>リソースにアクセスするときは、適切なマウントポイントを使用することが推奨されます。
>
>This ensures that the Sling Resource Merger is invoked and the fully merged resource returned (reducing the structure that needs to be replicated from `/libs`).

* オーバーレイ：

   * 目的：検索パスに基づいてリソースをマージする。
   * mount point: `/mnt/overlay`
   * usage: `mount point + relative path`
   * 例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* オーバーライド：

   * 目的：スーパータイプに基づいてリソースをマージする。
   * mount point: `/mnt/overide`
   * usage: `mount point + absolute path`
   * 例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用例 {#example-of-usage}

以下のページで、一部の例が紹介されています。

* オーバーレイ：

   * [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
   * [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)

* オーバーライド：

   * [ページプロパティの設定](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

