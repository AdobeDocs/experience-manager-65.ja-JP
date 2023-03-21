---
title: AEM コンポーネントの開発
seo-title: Developing AEM Components
description: AEM コンポーネントを使用して、web ページ上で使用できるコンテンツを保持、書式設定およびレンダリングします。
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '3456'
ht-degree: 50%

---

# AEM コンポーネントの開発{#developing-aem-components}

AEM コンポーネントを使用して、web ページ上で使用できるコンテンツを保持、書式設定およびレンダリングします。

* [ページをオーサリング](/help/sites-authoring/default-components.md)するとき、作成者はコンポーネントを使用してコンテンツを編集および設定できます。

   * [コマース](/help/commerce/cif-classic/administering/ecommerce.md)サイトを構築するときは、コンポーネントを使用して、例えばカタログの情報を収集してレンダリングできます。詳しくは、[e コマースの開発](/help/commerce/cif-classic/developing/ecommerce.md)を参照してください。

   * [コミュニティ](/help/communities/author-communities.md)サイトを構築するときは、コンポーネントを使用して、訪問者に情報を提供したり、訪問者から情報を収集したりできます。詳しくは、[コミュニティの開発](/help/communities/communities.md)を参照してください。

* パブリッシュインスタンスでは、コンポーネントはコンテンツをレンダリングし、Web サイト訪問者に対して必要に応じて表示します。

>[!NOTE]
>
>このページの内容は、[AEM コンポーネント - 基本](/help/sites-developing/components-basics.md)を踏まえたものです。

>[!CAUTION]
>
>`/libs/cq/gui/components/authoring/dialog` の下にあるコンポーネントは、エディター（オーサリングのコンポーネントダイアログ）で使用することのみが意図されています。他の場所（例えば、ウィザードのダイアログなど）で使用されている場合は、期待どおりに動作しない可能性があります。

## コードサンプル {#code-samples}

このページには、AEMの新しいコンポーネントの開発に必要なリファレンスドキュメント（またはリファレンスドキュメントへのリンク）が記載されています。 実践的な例については、[AEM コンポーネントの開発 - コードサンプル](/help/sites-developing/developing-components-samples.md)を参照してください。

## 構造 {#structure}

コンポーネントの基本構造については、[AEM コンポーネント - 基本](/help/sites-developing/components-basics.md#structure)のページで説明しています。このドキュメントでは、タッチ対応 UI とクラシック UI の両方を扱っています。新しいコンポーネントでクラシック設定を使用する必要がない場合でも、既存のコンポーネントから継承する際にクラシック設定について知っていると役立ちます。

## 既存のコンポーネントとダイアログの拡張 {#extending-existing-components-and-dialogs}

実装するコンポーネントに応じて、全体を定義して開発するのではなく、既存のインスタンスを拡張またはカスタマイズできる場合があります [構造](#structure) 最初から

既存のコンポーネントまたはダイアログを拡張またはカスタマイズする場合、変更を加える前に、構造全体またはダイアログに必要な構造をコピーまたは複製できます。

### 既存のコンポーネントの拡張 {#extending-an-existing-component}

既存のコンポーネントの拡張は、 [リソースタイプ階層](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 関連する継承メカニズム

>[!NOTE]
>
>コンポーネントは、検索パスロジックに基づいたオーバーレイを使用して再定義することもできます。ただし、この場合、 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) がトリガーされず、 `/apps` はオーバーレイ全体を定義する必要があります。

>[!NOTE]
>
>この [コンテンツフラグメントコンポーネント](/help/sites-developing/customizing-content-fragments.md) また、カスタマイズや拡張も可能ですが、Assets との完全な構造と関係を考慮する必要があります。

### 既存のコンポーネントダイアログのカスタマイズ {#customizing-a-existing-component-dialog}

[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) を使用し、`sling:resourceSuperType` プロパティを定義することで、*コンポーネントダイアログ*&#x200B;をオーバーライドすることもできます。

つまり、ダイアログ全体を（`sling:resourceSuperType` を使用して）再定義するのとは対照的に、再定義する必要があるのは相違点だけです。これは、推奨されるコンポーネントダイアログ拡張方法です。

詳しくは、[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) を参照してください。

## マークアップの定義 {#defining-the-markup}

コンポーネントは [HTML](https://www.w3schools.com/htmL/html_intro.asp) を使用してレンダリングされます。コンポーネントでは、必要なコンテンツを取得して、オーサリング環境とパブリッシュ環境の両方で必要に応じてレンダリングするために必要な HTML を定義しなければなりません。

### HTML テンプレート言語の使用 {#using-the-html-template-language}

この [HTMLテンプレート言語 (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja)AEM 6.0 で導入されたは、JSP(JavaServer Pages) の代わりに、HTML用の優先かつ推奨されるサーバー側テンプレートシステムとして使用されます。 堅牢なエンタープライズ Web サイトを構築する必要がある Web 開発者にとって、HTL は、セキュリティと開発の効率を高めるのに役立ちます。

>[!NOTE]
>
>HTL と JSP の両方をコンポーネントの開発に使用できますが、AEMの推奨スクリプティング言語は HTL なので、このページでは HTL を使用した開発について説明します。

## コンテンツロジックの開発 {#developing-the-content-logic}

このオプションのロジックでは、レンダリングするコンテンツを選択または計算します。 適切な Use-API パターンを使用して HTL 式から呼び出されます。

ロジックを外観と切り離すメカニズムは、特定のビューに対して何が呼び出されるかを明確にするのに役立ちます。 また、同じリソースのビューが異なると、異なるロジックを使用できます。

### Java の使用 {#using-java}

[HTL Java Use-API を使用すると、HTL ファイルからカスタム Java クラスのヘルパーメソッドへのアクセスが可能になります](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=ja?lang=en). これにより、Java コードを使用して、コンポーネントコンテンツの選択と設定のロジックを実装できます。

### JavaScript の使用 {#using-javascript}

[HTL JavaScript Use-API を使用すると、HTL ファイルから JavaScript で記述されたヘルパーコードへのアクセスが可能になります](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). そのため、JavaScript コードを使用して、コンポーネントのコンテンツを選択および設定するためのロジックを実装できます。

### クライアント側HTMLライブラリの使用 {#using-client-side-html-libraries}

最新の Web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。 このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題への対処に役立つように、AEM では、**クライアント側ライブラリフォルダー**&#x200B;が提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義することができます。その後、クライアント側ライブラリシステムにより、最終的な web ページで、正しいコードを読み込むための正しいリンクが作成されます。

読み取り [クライアント側HTMLライブラリの使用](/help/sites-developing/clientlibs.md) を参照してください。

## 編集動作の設定 {#configuring-the-edit-behavior}

コンポーネントの編集動作を設定できます。コンポーネントで使用できるアクションなどの属性、インプレースエディターの特性、コンポーネント上のイベントに関連するリスナーなどが含まれます。 この設定は、特定の違いはあるものの、タッチ操作対応 UI とクラシック UI の両方に共通です。

タイプ `cq:EditConfig` の `cq:editConfig` ノードをコンポーネントノード（タイプ `cq:Component`）の下に追加し、特定のプロパティと子ノードを追加することによって、[コンポーネントの編集動作が設定されます](/help/sites-developing/components-basics.md#edit-behavior)。

## プレビュー動作の設定 {#configuring-the-preview-behavior}

**プレビュー**&#x200B;モードに切り替えると、ページが更新されなくても [WCM モード](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie が設定されます。

レンダリングが WCM モードの影響を受けるコンポーネントの場合は、明確にそのコンポーネントを更新し、この Cookie の値を使用するように定義する必要があります。

>[!NOTE]
>
>値 `EDIT` と `PREVIEW` は、タッチ操作対応 UI でのみ [WCM モード](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie に使用されます。

## ダイアログの作成と設定 {#creating-and-configuring-a-dialog}

作成者はダイアログを使用してコンポーネントとやり取りできます。ダイアログを使用することで、作成者や管理者はコンテンツを編集したり、コンポーネントを設定したり、（[デザインダイアログ](#creating-and-configuring-a-design-dialog)を使用して）デザインパラメーターを定義したりできます。

### Coral UI と Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) および [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) AEMの最新のルックアンドフィールを定義する。

[Granite UI には、様々な基本コンポーネント（ウィジェット）が用意されています](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) オーサリング環境でダイアログを作成するために必要です。 必要に応じて、この選択を拡張し、 [独自のウィジェットを作成](#creatinganewwidget).

詳しくは、以下を参照してください。

* Coral UI

   * すべてのクラウドソリューションに一貫性ある UI を提供
   * [AEM タッチ操作対応 UI の概念 - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI ガイド](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite UI

   * UI コンソールおよびダイアログの構築用に Coral UI マークアップを Sling コンポーネントにラップして提供
   * [AEM タッチ対応 UI の概念 - Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>Granite UI コンポーネントの性質（および ExtJS ウィジェットとの違い）により、タッチ操作対応 UI と [クラシック UI](/help/sites-developing/developing-components-classic.md).

### 新しいダイアログの作成 {#creating-a-new-dialog}

タッチ操作対応 UI 用のダイアログ：

* `cq:dialog` という名前です。
* `sling:resourceType` プロパティが設定された `nt:unstructured` ノードとして定義されます。

* `cq:Component` ノードの下のコンポーネント定義の横にあります。
* コンテンツ構造と `sling:resourceType` プロパティに基づいて、サーバーサイドに（Sling コンポーネントとして）レンダリングされます。
* Granite UI フレームワークを使用します。
* には、ダイアログ内のフィールドを記述するノード構造が含まれます。

   * これらのノードは、必須の `sling:resourceType` プロパティを持つ `nt:unstructured` ノードです。

ノード構造の例は次のとおりです。

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

ダイアログのカスタマイズは、ダイアログ自体がコンポーネントなので、コンポーネントの開発に似ています（コンポーネントスクリプトでレンダリングするマークアップや、クライアントライブラリで提供する動作やスタイルなど）。

例については、以下を参照してください。

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>タッチ操作対応 UI 用のダイアログがコンポーネントに定義されていない場合、クラシック UI ダイアログが互換性レイヤー内のフォールバックとして使用されます。 そのようなダイアログをカスタマイズするには、クラシック UI ダイアログをカスタマイズする必要があります。詳しくは、[クラシック UI 用の AEM コンポーネント](/help/sites-developing/developing-components-classic.md)を参照してください。

### ダイアログフィールドのカスタマイズ {#customizing-dialog-fields}

>[!NOTE]
>
>次を参照してください。
>
>* [ダイアログフィールドのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en)に関する AEM Gems セッション。
>* 「[コードサンプル - ダイアログフィールドのカスタマイズ方法](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)」で説明されている関連サンプルコード。
>


#### 新しいフィールドの作成 {#creating-a-new-field}

タッチ操作対応 UI のウィジェットは、Granite UI コンポーネントとして実装されています。

タッチ操作対応 UI 用のコンポーネントダイアログで使用する新しいウィジェットを作成するには、次の手順を実行する必要があります。 [新しい Granite UI フィールドコンポーネントを作成します。](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Granite UI の詳細については、 [Granite UI ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

ダイアログをフォーム要素の単純なコンテナと見なす場合、ダイアログコンテンツの主なコンテンツをフォームフィールドとして表示することもできます。 新しいフォームフィールドを作成するには、リソースタイプを作成する必要があります。これは、新しいコンポーネントの作成と同じです。 この作業を容易にするために、Granite UI は、`sling:resourceSuperType` を使用して以下を継承する汎用フィールドコンポーネントを提供しています。

`/libs/granite/ui/components/coral/foundation/form/field`

Granite UI には、具体的に言えばダイアログ（一般的に言えば[フォーム](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)）での使用に適した、幅広いフィールドコンポーネントが用意されています。

>[!NOTE]
>
>この点はクラシック UI とは異なります。クラシック UI では、ウィジェットは `cq:Widgets` ノードによって表され、各ノードには対応する ExtJS ウィジェットとの関係を確立するための特定の `xtype` があります。実装の観点では、これらのウィジェットは ExtJS フレームワークによってクライアントサイドでレンダリングされていました。

リソースタイプを作成したら、`sling:resourceType` プロパティで参照して新しいノードをダイアログに追加することで、フィールドをインスタンス化できます。

#### スタイルおよび動作用のクライアントライブラリの作成 {#creating-a-client-library-for-style-and-behavior}

コンポーネントのスタイル設定と動作を定義する場合は、カスタム CSS/LESS および JS を定義する専用の[クライアントライブラリ](/help/sites-developing/clientlibs.md)を作成できます。

クライアントライブラリをコンポーネントダイアログ専用に読み込む（すなわち、別のコンポーネント用には読み込まれないようにする）には、ダイアログの `extraClientlibs`** ** プロパティを、作成したクライアントライブラリのカテゴリ名に設定する必要があります。この方法は、クライアントライブラリが非常に大きい場合や、フィールドがそのダイアログに固有で、他のダイアログで必要になることがない場合にお勧めです。

クライアントライブラリをすべてのダイアログ用に読み込むには、クライアントライブラリのカテゴリプロパティを `cq.authoring.dialog` に設定します。これは、すべてのダイアログをレンダリングする際にデフォルトで含まれるクライアントライブラリのカテゴリ名です。 クライアントライブラリが小さく、フィールドが汎用で、他のダイアログで再利用できる場合に、この方法を使用します。

例えば、次を参照してください。

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

#### フィールドの拡張（継承） {#extending-inheriting-from-a-field}

要件に応じて、次のいずれかを実行できます。

* 指定された Granite UI フィールドをコンポーネントの継承（`sling:resourceSuperType`）で拡張する
* ウィジェットライブラリ API（JS/CSS の継承）に従って、基になるウィジェットライブラリ（Granite UI の場合は Coral UI）から特定のウィジェットを拡張する

#### ダイアログフィールドへのアクセス {#access-to-dialog-fields}

レンダリング条件（`rendercondition`）を使用して、ダイアログ内の特定のタブやフィールドへのアクセス権を持つユーザーを制御することもできます。以下に例を示します。

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### フィールドイベントの処理 {#handling-field-events}

ダイアログフィールドのイベントの処理方法は、 [カスタムクライアントライブラリのリスナー](#listeners-in-a-custom-client-library). これは、以前の方法からの変更です。 [コンテンツ構造のリスナー](#listenersinthecontentstructureclassicui).

#### カスタムクライアントライブラリのリスナー {#listeners-in-a-custom-client-library}

フィールドにロジックを挿入するには、以下を実行する必要があります。

1. 対象となるフィールドを、指定された CSS クラス（*フック*）でマークします。
1. クライアントライブラリで、その CSS クラス名にフックされた JS リスナーを定義します（これにより、カスタムロジックがフィールドのみにスコープされ、同じタイプの他のフィールドには影響を与えません）。

これを実現するには、やり取りする、基になるウィジェットライブラリについて理解する必要があります。詳しくは、 [Coral UI ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) を使用して、反応するイベントを特定します。 これは、以前に ExtJS で実行する必要があったプロセスと非常に似ています。特定のウィジェットのドキュメントページを見つけ、そのイベント API の詳細を確認します。

例えば、次を参照してください。

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

#### コンテンツ構造のリスナー {#listeners-in-the-content-structure}

ExtJS を使用したクラシック UI では、コンテンツ構造内に特定のウィジェットのリスナーを持つのが通常でした。 タッチ操作対応 UI で同じことを実現する方法は、JS リスナーコード（またはコードなど）がコンテンツで定義されなくなったので、異なります。

コンテンツ構造は、セマンティック構造を記述します。基になるウィジェットの性質を暗示してはなりません（必ず）。 コンテンツ構造に JS コードを含めないことで、コンテンツ構造を変更しなくても実装の詳細を変更できます。 つまり、コンテンツ構造にタッチする必要なくウィジェットライブラリを変更できます。

#### ダイアログの可用性の検出 {#dialog-ready}

ダイアログが使用可能で準備が整ったときにのみ実行する必要があるカスタム JavaScript がある場合は、`dialog-ready` イベントをリッスンする必要があります。

このイベントは、ダイアログが読み込まれて（または再度読み込まれて）、使用の準備ができたときにトリガーされます。つまり、ダイアログの DOM に変更（作成／更新）がある場合に必ずトリガーされます。

`dialog-ready` は、ダイアログ内のフィールドや類似のタスクをカスタマイズする JavaScript カスタムコードをフックするために使用できます。

### フィールドの検証 {#field-validation}

#### 必須フィールド {#mandatory-field}

特定のフィールドを必須としてマークするには、フィールドのコンテンツノードで次のプロパティを設定します。

* 名前：`required`
* 型：`Boolean`

例えば、次を参照してください。

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### フィールドの検証 (Granite UI) {#field-validation-granite-ui}

Granite UI でのフィールド検証および Granite UI コンポーネント（ウィジェットと同等）のフィールド検証は、`foundation-validation` API を使用して実行します。[詳しくは、`foundation-valdiation`Granite のドキュメントを参照してください。](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

詳しくは、例えば、以下を参照してください。

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## デザインダイアログの作成と設定 {#creating-and-configuring-a-design-dialog}

コンポーネントに[デザインモード](/help/sites-authoring/default-components-designmode.md)で編集できるデザイン詳細がある場合は、デザインダイアログが表示されます。

デザインダイアログの定義は、[コンテンツの編集に使用されるダイアログ](#creating-a-new-dialog)の定義によく似ています。違いはノードとして定義される点です。

* ノード名：`cq:design_dialog`
* 型：`nt:unstructured`

## インプレースエディターの作成と設定 {#creating-and-configuring-an-inplace-editor}

インプレースエディターを使用すると、ダイアログを開かなくても、段落フロー内のコンテンツを直接編集できます。 例えば、標準のテキストコンポーネントとタイトルコンポーネントには、どちらもインプレースエディターが用意されています。

インプレースエディターは、すべてのコンポーネントタイプに対して必要ではなく、意味もありません。

詳しくは、 [ページオーサリングの拡張 — 新しいインプレースエディターの追加](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) を参照してください。

## コンポーネントツールバーのカスタマイズ {#customizing-the-component-toolbar}

この [コンポーネントツールバー](/help/sites-developing/touch-ui-structure.md#component-toolbar) を使用すると、編集、設定、コピー、削除など、コンポーネントに対する様々なアクションにユーザーがアクセスできます。

詳しくは、 [ページオーサリングの拡張 — コンポーネントツールバーに新しいアクションを追加](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) を参照してください。

## 参照レールのコンポーネントの設定（借りた/貸した） {#configuring-a-component-for-the-references-rail-borrowed-lent}

新しいコンポーネントが他のページのコンテンツを参照する場合は、 **借りたコンテンツ** および **貸したコンテンツ** セクション [**参照**](/help/sites-authoring/basic-handling.md#references) レール。

標準搭載のAEMは、参照コンポーネントのみをチェックします。 コンポーネントを追加するには、OSGi バンドル **WCM オーサリングコンテンツ参照設定**&#x200B;を設定する必要があります。

定義に新しいエントリを作成し、確認するプロパティと共にコンポーネントを指定します。次に例を示します。

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## 段落システムへのコンポーネントの有効化と追加 {#enabling-and-adding-your-component-to-the-paragraph-system}

コンポーネントを開発した後、適切な段落システムで使用できるように、必要なページで使用できるようにする必要があります。

これは、次のいずれかの方法で実行できます。

* using [デザインモード](/help/sites-authoring/default-components-designmode.md) （特定のページの編集時）
* [テンプレートの段落システムに `components` プロパティを定義する](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEMでは、次のようにページ上で段落システムを設定できます。 [ユーザーが（適切な）アセットをそのページのインスタンスにドラッグすると、新しいコンポーネントのインスタンスが自動的に作成されます](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （常に空のコンポーネントをページにドラッグする必要はありません）。

この動作と、必要なアセットとコンポーネントの関係は、次のように設定できます。

1. ページデザインの段落定義の下に表示されます。 次に例を示します。

   * `/etc/designs/<myApp>/page/par`

   新しいノードを作成します。

   * 名前：`cq:authoring`
   * 型：`nt:unstructured`


1. この下に、アセットとコンポーネントのマッピングをすべて保持する新しいノードを作成します。

   * 名前：`assetToComponentMapping`
   * 型：`nt:unstructured`

1. アセットとコンポーネントのマッピングごとに、ノードを作成します。

   * 名前：テキスト。アセットと関連するコンポーネントタイプを示す名前（例：image）にすることを推奨します。
   * 型：`nt:unstructured`

   それぞれが以下のプロパティを持ちます。

   *  `assetGroup`：

      * 型：`String`
      * 値：関連アセットが所属するグループ（例：`media`）
   *  `assetMimetype`：

      * 型：`String`
      * 値：関連アセットの MIME タイプ（例：`image/*`）
   *  `droptarget`：

      * 型：`String`
      * 値：ドロップターゲット（例：`image`）
   *  `resourceType`：

      * 型：`String`
      * 値：関連コンポーネントリソース（例：`foundation/components/image`）
   *  `type`：

      * 型：`String`
      * 値：タイプ（例：`Images`）






例えば、次を参照してください。

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-project-archetype プロジェクトを開く](https://github.com/adobe/aem-project-archetype)
* プロジェクトを [ZIP ファイル](https://github.com/adobe/aem-project-archetype/archive/master.zip)としてダウンロードします

>[!NOTE]
>
>コンポーネントインスタンスの自動作成は、[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)と編集可能テンプレートの使用時に UI 内で簡単に設定できるようになりました。特定のメディアタイプに自動的に関連付けるコンポーネントの定義について詳しくは、[ページテンプレートの作成](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)を参照してください。

## AEM Brackets 拡張の使用 {#using-the-aem-brackets-extension}

この [AEM Brackets Extension](/help/sites-developing/aem-brackets.md) は、AEMコンポーネントとクライアントライブラリを編集するためのスムーズなワークフローを提供します。 これは、 [Brackets](https://brackets.io/) コードエディター。

拡張機能：

* 同期を容易にして（Maven や File Vault は不要）、開発者の効率を向上させるだけでなく、AEM に関する知識が限られたフロントエンド開発者もプロジェクトに参加できるようにします。
* コンポーネント開発の単純化やセキュリティ向上のために設計されたテンプレート言語 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) を一部サポートしています。

>[!NOTE]
>
>Brackets は、コンポーネントを作成する際に推奨されるメカニズムです。 これは、クラシック UI 用に設計されたCRXDE Lite — コンポーネントを作成機能に代わるものです。

## クラシックコンポーネントからの移行 {#migrating-from-a-classic-component}

クラシック UI で使用するようにデザインされたコンポーネントを、タッチ操作対応 UI 専用または両方の UI で使用できるコンポーネントに移行する場合は、以下の問題を考慮する必要があります。

* HTL

   * [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) の使用は必須ではありません。ただし、コンポーネントを更新する必要がある場合は、[JSP から HTL への移行](/help/sites-developing/components-basics.md#htl-vs-jsp)を検討することをお勧めします。

* コンポーネント

   * クラシック UI 固有の関数を使用する [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) コードを移行します。
   * RTE プラグイン。詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。
   * クラシック UI 固有の関数を使用する[ `cq:listener` コードを移行](#migrating-cq-listener-code)します。

* ダイアログ

   * タッチ操作対応 UI で使用するダイアログを作成します。 ただし、タッチ操作対応 UI 用のダイアログが定義されていないときは、互換性のために、タッチ操作対応 UI でクラシック UI ダイアログの定義を使用できます。
   * [AEM 最新化ツール](/help/sites-developing/modernization-tools.md)を使用すると、既存のコンポーネントを拡張するのに役立ちます。
   * [ExtJS を Granite UI コンポーネントへマッピング](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components)では、ExtJS の xtype とノードタイプを、同等の Granite UI リソースタイプにマッピングする便利な概要について説明しています。
   * フィールドのカスタマイズ ( 詳しくは、 AEM Gems セッションの詳細を参照 ) [ダイアログフィールドのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
   * vtypes からに移行 [Granite UI の検証](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * JS リスナーの使用 ( 詳しくは、 [フィールドイベントの処理](#handling-field-events) とAEM Gems セッションが [ダイアログフィールドのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).

### cq:listener コードの移行 {#migrating-cq-listener-code}

クラシック UI 向けにデザインされたプロジェクトを移行する場合は、`cq:listener` コード（およびコンポーネントに関連するクライアント側ライブラリ）でクラシック UI 固有の関数（`CQ.wcm.*` など）を使用してください。移行するには、タッチ操作対応 UI で同等のオブジェクトまたは関数を使用して、このようなコードを更新する必要があります。

プロジェクトをタッチ操作対応 UI に完全に移行する場合は、タッチ操作対応 UI に関連するオブジェクトや関数を使用するために、このようなコードを置き換える必要があります。

ただし、移行期間中にプロジェクトがクラシック UI とタッチ操作対応 UI の両方に対応する必要がある場合（通常のシナリオ）は、適切なオブジェクトを参照する個別のコードを区別するためのスイッチを実装する必要があります。

このスイッチメカニズムは、次のように実装できます。

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## コンポーネントのドキュメント化 {#documenting-your-component}

開発者は、次の内容をすばやく理解できるように、コンポーネントドキュメントに簡単にアクセスしたいと考えています。

* 説明
* 使用目的
* コンテンツの構造とプロパティ
* 公開された API と拡張ポイント
* その他

このため、コンポーネント内で既存のドキュメントマークダウンを利用できるようにするのは簡単です。

場所 a `README.md` ファイルを作成します。 この Markdown は、 [コンポーネントコンソール](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

サポートしているマークダウンは、[コンテンツフラグメント](/help/assets/content-fragments/content-fragments-markdown.md)の場合と同じです。
