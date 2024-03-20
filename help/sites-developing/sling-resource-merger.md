---
title: AEM での Sling Resource Merger の使用
description: Sling Resource Merger は、リソースにアクセスおよびマージするためのサービスを提供します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1eed754e-9a7d-4b65-a929-757fc962614d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 100%

---

# AEM での Sling Resource Merger の使用{#using-the-sling-resource-merger-in-aem}

## 目的 {#purpose}

Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します.次の両方に対して差分メカニズムを提供します。

* [設定済み検索パス](/help/sites-developing/overlays.md#configuring-the-search-paths)を使用するリソースの&#x200B;**[オーバーレイ](/help/sites-developing/overlays.md)**。

* リソースタイプ階層を（**プロパティを通じて）使用するタッチ操作対応 UI のコンポーネントダイアログ（**）の`cq:dialog`オーバーライド`sling:resourceSuperType`。

Sling Resource Merger を使用すると、リソースやプロパティのオーバーレイ／オーバーライドが元のリソース／プロパティにマージされます。

* カスタマイズされた定義のコンテンツの方が、元の定義のコンテンツよりも優先されます（つまり、前者が後者を&#x200B;*オーバーレイ*&#x200B;または&#x200B;*オーバーライド*&#x200B;します）。

* 必要な場合には、カスタマイズされた定義に含まれる[プロパティ](#properties)が、元の定義からマージされたコンテンツをどう使用するかを指定します。

>[!CAUTION]
>
>Sling Resource Merger および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) に対してのみ使用できます。これはつまり、標準のタッチ操作対応 UI でのみ使用できるという意味です。特に、この方法で定義された特定のオーバーライドは、コンポーネントのタッチ操作対応ダイアログに対してのみ適用できます。
>
>その他の領域（タッチ操作対応コンポーネントやクラシック UI の他の側面を含む）のオーバーレイ／オーバーライドでは、適切なノードと構造を元の場所からカスタマイズの定義先にコピーします。

### AEM の目的 {#goals-for-aem}

AEM で Sling Resource Merger を使用する目的は、次のとおりです。

* `/libs` にカスタマイズの変更が加えられないようにする。
* `/libs` からレプリケートされる構造を減らす。

  Sling Resource Merger を使用するときは、`/libs` の構造全体をコピーすることは推奨されません。そうすると、カスタマイズ（通常は `/apps`）で維持される情報が多くなりすぎるからです。情報を不必要に複製すると、システムのアップグレード時に問題が発生しやすくなります。

>[!NOTE]
>
>オーバーライドは、検索パスに依存せず、`sling:resourceSuperType` プロパティに基づいて接続を確立します。
>
>ただし、オーバーライドは `/apps` 以下に定義されるのが一般的です。AEM では、カスタマイズを `/apps` 以下に定義することがベストプラクティスとされています。なぜなら `/libs` 以下のコンテンツを変更してはならないからです。

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（`/libs` 内に存在）を、`/apps` の下で再作成します。
>
>1. `/apps` 内で必要な変更を加えます
>

### プロパティ {#properties}

リソースマージャーには次のプロパティがあります。

* `sling:hideProperties`（`String` または `String[]`）

  非表示にするプロパティまたはプロパティのリストを指定します。

  ワイルドカード `*` を指定した場合はすべて非表示になります。

* `sling:hideResource`（`Boolean`）

  リソースを子も含めて完全に非表示にするかを示します。

* `sling:hideChildren`（`String` または `String[]`）

  非表示にする子ノードまたは子ノードのリストが格納されます。ノードのプロパティは維持されます。

  ワイルドカード `*` を指定した場合はすべて非表示になります。

* `sling:orderBefore`（`String`）

  現在のノードの直後に配置する兄弟ノードの名前が格納されます。

これらのプロパティは、対応する（元の）リソースおよびプロパティ（`/libs` 内）がオーバーレイ／オーバーライド（`/apps` 内）によってどのように使用されるかに影響します。

### 構造の作成 {#creating-the-structure}

オーバーレイまたはオーバーライドを作成するには、元のノードを同じ構造で、目的の場所（通常は `/apps`）に再作成する必要があります。次に例を示します。

* オーバーレイ

   * サイトコンソールのナビゲーションエントリの定義（パネルに表示されるもの）は次の場所で定義されています。


     `/libs/cq/core/content/nav/sites/jcr:title`

   * これをオーバーレイするには、次のノードを作成します。

     `/apps/cq/core/content/nav/sites`

     次に、必要に応じて `jcr:title` プロパティを更新します。

* オーバーライド

   * テキストコンソールのタッチ操作対応ダイアログの定義は、次の場所に定義されます。

     `/libs/foundation/components/text/cq:dialog`

   * これをオーバーライドするには、例えば、次のノードを作成します。

     `/apps/the-project/components/text/cq:dialog`

これらのいずれを作成する場合も、必要な作業はスケルトン構造を再作成することだけです。構造を簡単に再作成できるように、すべての中間ノードは、タイプ `nt:unstructured` として作成できます（例えば、`/libs` の元のノードタイプを反映する必要はありません）。

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
>Sling Resource Merger を使用するとき（つまり標準のタッチ操作対応 UI を扱うとき）は、`/libs` の構造全体をコピーすることは推奨されません。そうすると、`/apps` 内で維持される情報が多くなりすぎるからです。その場合、システムが何らかの理由でアップグレードされたときに問題が発生する可能性があります。

### ユースケース {#use-cases}

これらを標準機能と組み合わせることで、次の操作が可能になります。

* **プロパティの追加**

  `/libs` 定義に存在しないプロパティが `/apps` オーバーレイ／オーバーライドで必要になった場合に、プロパティを追加できます。

   1. `/apps` 内に、対応するノードを作成します。
   1. このノード``で新しいプロパティを作成します。

* **プロパティの再定義（自動作成されたプロパティ以外）**

  `/libs` で定義されているプロパティについて、`/apps` オーバーレイ／オーバーライドで新しい値が必要になった場合に、プロパティを再定義できます。

   1. `/apps` 内に、対応するノードを作成します。
   1. このノード（`apps` 以下）で対応するプロパティを作成します。

      * このプロパティには、Sling Resource Resolver 設定に基づいた優先順位が付けられます。
      * プロパティタイプの変更がサポートされています。

        `/libs` で使用されているものとは異なるプロパティタイプを使用する場合、その定義したプロパティタイプが使用されます。

  >[!NOTE]
  >
  >プロパティタイプの変更がサポートされています。

* **自動作成されたプロパティの再定義**

  デフォルトでは、自動作成されたプロパティ（`jcr:primaryType` など）はオーバーレイ／オーバーライドの対象にならず、現在 `/libs` 以下にあるノードタイプが尊重されます。オーバーレイ／オーバーライドを適用するには、`/apps` でノードを再作成して、プロパティを明示的に非表示にし、再定義する必要があります。

   1. `/apps` 以下に、必要な `jcr:primaryType` を持つ、対応するノードを作成します。
   1. 自動作成されたプロパティに設定された値で、そのノードに `sling:hideProperties` プロパティを作成します。例：`jcr:primaryType`

      `/apps`で定義されるこのプロパティは、`/libs` 以下で定義されるプロパティより優先されるようになります。

* **ノードおよびその子の再定義**

  `/libs` 内に定義されているノードとその子について、`/apps` オーバーレイ／オーバーライドで新しい設定が必要な場合は、再定義を行います。

   1. 次のアクションを組み合わせます。

      1. ノードの子の非表示（そのノードのプロパティは維持）
      1. プロパティの再定義

* **プロパティの非表示**

  `/libs` 内に定義されているプロパティが、`/apps` オーバーレイ／オーバーライドでは不要な場合に、プロパティを非表示にできます。

   1. `/apps` 内に、対応するノードを作成します。
   1. `String` 型または `String[]` 型の `sling:hideProperties` プロパティを作成します。これを使用して、非表示／無視するプロパティを指定します。ワイルドカードも使用できます。次に例を示します。

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **ノードおよびその子の非表示**

  `/libs` 内に定義されているノードとその子が、`/apps` オーバーレイ／オーバーライドでは不要な場合に、不要なものを非表示にできます。

   1. /apps 以下に、対応するノードを作成します。
   1. `sling:hideResource` プロパティを作成します

      * 型：`Boolean`
      * 値：`true`

* **ノードの子の非表示（そのノードのプロパティは維持）**

  ノード、そのプロパティおよびその子が `/libs` に定義されていて、ノードとそのプロパティは `/apps` オーバーレイ／オーバーライドで必要であるものの、一部またはすべての子ノードは `/apps` オーバーレイ／オーバーライドでは不要です。

   1. `/apps` 以下に、対応するノードを作成します。
   1. `sling:hideChildren` プロパティを作成します。

      * 型：`String[]`
      * 値：非表示にする（無視する）子ノードのリスト（`/libs` 内に定義されているもの）

      ワイルドカード &amp;ast; を使用してすべての子ノードを非表示にする（無視する）ことができます。

* **ノードの並べ替え**

  ノードとその兄弟が `/libs` 内で定義されていて、ノードの位置を変更したい場合には、目的のノードを `/apps` 内のオーバーレイ／オーバーライドで再作成し、その中で、`/libs` 内の適切な兄弟ノードを参照して新しい位置を定義します。

   * `sling:orderBefore` プロパティを使用します。

      1. `/apps` 以下に、対応するノードを作成します。
      1. `sling:orderBefore` プロパティを作成します。

         これは、現在のノードを配置する前の（`/libs` 以下にある）ノードを指定します。

         * 型：`String`
         * 値：`<before-SiblingName>`

### コードからの Sling Resource Merger の呼び出し {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger には 2 つのカスタムリソースプロバイダーが含まれています。1 つはオーバーレイ用、もう 1 つはオーバーライド用です。それぞれ、マウントポイントを使用して、コード内で呼び出すことができます。

>[!NOTE]
>
>リソースにアクセスする場合は、適切なマウントポイントを使用することをお勧めします。
>
>適切なマウントポイントを使用すれば、Sling Resource Merger が確実に呼び出され、完全にマージされたリソースが確実に返されます（`/libs` からレプリケートする必要がある構造が低減します）。

* オーバーレイ：

   * 目的：検索パスに基づいてリソースをマージする。
   * マウントポイント：`/mnt/overlay`
   * 使用方法：`mount point + relative path`
   * 例：

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* オーバーライド：

   * 目的：スーパータイプに基づいてリソースをマージする。
   * マウントポイント：`/mnt/overide`
   * 使用方法：`mount point + absolute path`
   * 例：

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用例 {#example-of-usage}

以下のページで、一部の例が紹介されています。

* オーバーレイ：

   * [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
   * [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)

* オーバーライド：

   * [ページプロパティの設定](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
