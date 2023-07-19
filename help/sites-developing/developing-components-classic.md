---
title: AEM コンポーネントの開発（クラシック UI）
seo-title: Developing AEM Components (Classic UI)
description: クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。 HTL は、AEMの推奨スクリプティング言語ではありません。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2393'
ht-degree: 56%

---

# AEM コンポーネントの開発（クラシック UI）{#developing-aem-components-classic-ui}

クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。 これらのウィジェットの性質により、クラシック UI と [タッチ操作対応 UI](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>コンポーネント開発の多くの側面はクラシック UI とタッチ操作向け UI に共通なので、このページを使用する](/help/sites-developing/components-basics.md)前に&#x200B;**、AEM コンポーネント - 基本**&#x200B;を必ずお読みください[。クラシック UI の詳細が記載されています。

>[!NOTE]
>
>クラシック UI 用のコンポーネントの開発には HTML テンプレート言語（HTL）と JSP のどちらも使用できますが、このページでは JSP を使用した開発について説明します。これは単に、クラシック UI 内では JSP が使用されてきたからです。
>
>現在では、HTL が AEM の推奨スクリプティング言語とされています。手法を比較するには、[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) および [AEM コンポーネントの開発](/help/sites-developing/developing-components.md)を参照してください。

## 構造 {#structure}

コンポーネントの基本構造については、タッチ操作対応 UI とクラシック UI の両方に適用される [AEM コンポーネント - 基本](/help/sites-developing/components-basics.md#structure)ページで説明しています。新しいコンポーネントでタッチ操作対応 UI の設定を使用する必要がない場合でも、既存のコンポーネントから継承する際に、設定を認識するのに役立ちます。

## JSP スクリプト {#jsp-scripts}

JSP スクリプトまたはサーブレットを使用して、コンポーネントをレンダリングできます。 Sling のリクエスト処理ルールに従って、デフォルトスクリプトの名前は次のようになります。

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP スクリプトファイルの `global.jsp` は、コンポーネントのレンダリングに使用される任意の JSP スクリプトの特定オブジェクト（コンテンツ）にすばやくアクセスするために使用されます。

したがって、`global.jsp` で提供される 1 つ以上のオブジェクトを使用する場合は、JSP スクリプトをレンダリングするすべてのコンポーネントに `global.jsp` を含める必要があります。

デフォルトの `global.jsp` は次の場所にあります。

`/libs/foundation/global.jsp`

>[!NOTE]
>
>CQ 5.3 以前のバージョンで使用されたパス `/libs/wcm/global.jsp` は、現在廃止されています。

### global.jsp、使用される API および Taglib の機能 {#function-of-global-jsp-used-apis-and-taglibs}

デフォルトの `global.jsp` から提供される最も重要なオブジェクトを次に示します。

概要：

* `<cq:defineObjects />`

   * `slingRequest` - ラップされたリクエストオブジェクト（`SlingHttpServletRequest`）。
   * `slingResponse` - ラップされた応答オブジェクト（`SlingHttpServletResponse`）。
   * `resource` - Sling リソースオブジェクト（`slingRequest.getResource();`）。
   * `resourceResolver` - Sling リソースリゾルバーオブジェクト（`slingRequest.getResoucreResolver();`）。
   * `currentNode` - リクエストに対して解決された JCR ノード。
   * `log` - デフォルトの logger ()。
   * `sling` - Sling スクリプトヘルパー。
   * `properties` - 指定されたリソースのプロパティ（`resource.adaptTo(ValueMap.class);`）。
   * `pageProperties` - 指定されたリソースのページのプロパティ。
   * `pageManager` - AEM コンテンツページにアクセスするためのページマネージャー（`resourceResolver.adaptTo(PageManager.class);`）。
   * `component` - 現在の AEM コンポーネントのコンポーネントオブジェクト。
   * `designer` - デザイン情報を取得するためのデザイナーオブジェクト（`resourceResolver.adaptTo(Designer.class);`）。
   * `currentDesign` - 指定されたリソースのデザイン。
   * `currentStyle` - 指定されたリソースのスタイル。

### コンテンツへのアクセス {#accessing-content}

AEM WCM のコンテンツにアクセスするには、次の 3 つの方法があります。

* `global.jsp` に設定されているプロパティオブジェクト経由：

  プロパティオブジェクトは、ValueMap のインスタンス（[Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html) を参照）で、現在のリソースのプロパティがすべて含まれています。

  例：ページコンポーネントのレンダリングスクリプト内で使用される `String pageTitle = properties.get("jcr:title", "no title");`

  例：標準の段落コンポーネントのレンダリングスクリプト内で使用される `String paragraphTitle = properties.get("jcr:title", "no title");`

* `global.jsp` に設定されている `currentPage` オブジェクト経由：

  `currentPage` オブジェクトは、ページのインスタンスです（[AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) を参照）。ページクラスには、コンテンツにアクセスするためのメソッドがいくつかあります。

  例：`String pageTitle = currentPage.getTitle();`

* `global.jsp` に導入されている `currentNode` オブジェクト経由：

  `currentNode` オブジェクトは、ノードのインスタンスです（[JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html) を参照）。ノードのプロパティには、`getProperty()` メソッドによってアクセスできます。

  例：`String pageTitle = currentNode.getProperty("jcr:title");`

## JSP タグライブラリ {#jsp-tag-libraries}

CQ および Sling タグライブラリを使用すると、テンプレートおよびコンポーネントの JSP スクリプトで使用する特定の関数にアクセスできます。

詳しくは、[タグライブラリ](/help/sites-developing/taglib.md)ドキュメントを参照してください。

## クライアント側 HTML ライブラリの使用 {#using-client-side-html-libraries}

最近の web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題への対処に役立つように、AEM では、**クライアント側ライブラリフォルダー**&#x200B;が提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義することができます。その後、クライアントサイドライブラリシステムにより、最終的な web ページで、正しいコードを読み込むための正しいリンクが作成されます。

詳しくは、[クライアントサイド HTML ライブラリの使用](/help/sites-developing/clientlibs.md)ドキュメントを参照してください。

## ダイアログ {#dialog}

作成者がコンテンツを追加および設定するためのダイアログがコンポーネントに必要です。

詳しくは、[AEM コンポーネント - 基本](/help/sites-developing/components-basics.md#dialogs)を参照してください。

## 編集動作の設定 {#configuring-the-edit-behavior}

コンポーネントの編集動作を設定できます。 これには、コンポーネントで使用可能なアクションなどの属性、インプレースエディターの特性、コンポーネント上のイベントに関連するリスナーなどが含まれます。 この設定は、特定の違いはあるものの、タッチ操作対応 UI とクラシック UI の両方に共通です。

[コンポーネントの編集動作](/help/sites-developing/components-basics.md#edit-behavior)は、タイプ `cq:EditConfig` の `cq:editConfig` ノードをコンポーネントノード（タイプ `cq:Component`）の下に追加し、特定のプロパティと子ノードを追加して設定します。

## ExtJS ウィジェットの使用と拡張 {#using-and-extending-extjs-widgets}

詳しくは、[ExtJS ウィジェットの使用と拡張](/help/sites-developing/widgets.md)を参照してください。

## ExtJS ウィジェットに xtype を使用 {#using-xtypes-for-extjs-widgets}

詳しくは、 [xtype の使用](/help/sites-developing/xtypes.md) を参照してください。

## 新しいコンポーネントの開発 {#developing-new-components}

この節では、独自のコンポーネントを作成して段落システムに追加する方法について説明します。

既存のコンポーネントをコピーし、必要な変更を加える方法を簡単に開始できます。

コンポーネントの開発方法の例について詳しくは、 [テキストおよび画像コンポーネントの拡張 — 例。](#extending-the-text-and-image-component-an-example)

### 新しいコンポーネントの開発（既存のコンポーネントの適応） {#develop-a-new-component-adapt-existing-component}

既存のコンポーネントに基づいてAEM用の新しいコンポーネントを開発するには、コンポーネントをコピーし、新しいコンポーネントの JavaScript ファイルを作成して、AEMがアクセス可能な場所に保存します ( [コンポーネントおよびその他の要素のカスタマイズ](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. CRXDE Liteを使用して、次の場所に新しいコンポーネントフォルダーを作成します。

   / `apps/<myProject>/components/<myComponent>`

   libs 内のノード構造を再作成し、テキストコンポーネントなどの既存のコンポーネントの定義をコピーします。 例えば、テキストコンポーネントをカスタマイズするには、次のようにコピーします。

   * コピー元：`/libs/foundation/components/text`
   * コピー先：`/apps/myProject/components/text`

1. `jcr:title` を変更して新しい名前を反映させます。
1. 新しいコンポーネントフォルダーを開き、必要な変更を行います。 また、フォルダー内の不要な情報を削除します。

   次のような変更を行うことができます。

   * ダイアログボックスでの新しいフィールドの追加

      * `cq:dialog` - タッチ操作対応 UI 用ダイアログ
      * `dialog` - クラシック UI 用ダイアログ

   * `.jsp` ファイルの置換（新しいコンポーネントの作成後に名前を付けます）
   * または、コンポーネント全体の作成し直し（必要な場合）

   例えば、標準テキストコンポーネントのコピーを作成した場合は、ダイアログボックスにフィールドを追加して、`.jsp` を更新し、そこに追加された情報を処理します。

   >[!NOTE]
   >
   >使用するコンポーネント：
   >
   >* タッチ操作対応 UI では [Granite](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) コンポーネントを使用します
   >* クラシック UI の使用 [ExtJS ウィジェット](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)

   >[!NOTE]
   >
   >クラシック UI 用に定義されたダイアログは、タッチ操作対応 UI 内で動作します。
   >
   >タッチ操作対応 UI 用に定義されたダイアログは、クラシック UI 内では動作しません。
   >
   >インスタンスとオーサー環境によっては、コンポーネント用に両方のタイプのダイアログを定義する必要が生じる場合があります。

1. 新しいコンポーネントを表示するには、次のいずれかのノードが存在し、適切に初期化されている必要があります。

   * `cq:dialog` - タッチ操作対応 UI 用ダイアログ
   * `dialog` - クラシック UI 用ダイアログ
   * `cq:editConfig`  — 編集環境でのコンポーネントの動作（ドラッグ&amp;ドロップなど）
   * `design_dialog` - デザインモード用ダイアログ（クラシック UI のみ）

1. 次のどちらかの方法で、段落システムで新しいコンポーネントを利用できるようにします。

   * CRXDE Lite を使用して、ノード `/etc/designs/geometrixx/jcr:content/contentpage/par` の適切なコンポーネントに、値 `<path-to-component>`（`/apps/geometrixx/components/myComponent` など）を追加します。
   * 次の [段落システムへの新しいコンポーネントの追加](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. AEM WCM で、Web サイトのページを開き、作成したタイプの新しい段落を挿入して、コンポーネントが正しく動作していることを確認します。

>[!NOTE]
>
>ページ読み込みのタイミングの統計を確認するには、Ctrl + Shift + U キーを、URL で設定されている `?debugClientLibs=true` と共に使用します。

### 段落システム（デザインモード）への新しいコンポーネントの追加 {#adding-a-new-component-to-the-paragraph-system-design-mode}

コンポーネントを開発したら、段落システムに追加します。これにより、作成者は、ページの編集時にコンポーネントを選択して使用できます。

1. 段落システムを使用するオーサリング環境でページにアクセスします（例：`<contentPath>/Test.html`）。
1. 次のどちらかの方法でデザインモードに切り替えます。

   * 以下の例のように、URL の最後に `?wcmmode=design` を追加し、再度アクセスします。

     `<contextPath>/ Test.html?wcmmode=design`

   * 「デザイン」Sidekick

   これでデザインモードになり、段落システムを編集できます。

1. 「編集」をクリックします。

   段落システムに属するコンポーネントのリストが表示されます。 新しいコンポーネントも表示されます。

   ページの編集時に作成者に提供されるコンポーネントを決定するには、コンポーネントをアクティベート（またはアクティベートを解除）します。

1. コンポーネントをアクティベートして、通常の編集モードに戻り、使用可能であることを確認します。

### テキストおよび画像コンポーネントの拡張 — 例 {#extending-the-text-and-image-component-an-example}

この節では、設定可能な画像配置機能を使用して、広く使用されているテキストおよび画像標準コンポーネントを拡張する方法の例を示します。

テキストおよび画像コンポーネントの拡張機能を使用すると、エディターはコンポーネントの既存の機能をすべて使用でき、さらに次のいずれかの方法で画像の配置を指定する追加のオプションを持ちます。

* テキストの左側（現在の動作と新しいデフォルト）
* 右側の

このコンポーネントを拡張した後、コンポーネントのダイアログボックスを使用して画像の配置を設定できます。

この練習では、次の方法について説明します。

* 既存のコンポーネントノードをコピーし、そのメタデータを変更する
* 親ダイアログボックスからのウィジェットの継承を含む、コンポーネントのダイアログの変更
* 新しい機能を実装するためのコンポーネントのスクリプトの変更

>[!NOTE]
>
>この例は、クラシック UI を対象としています。

>[!NOTE]
>
>この例は、Geometrixx サンプルコンテンツに基づいています。これは、AEM に付属されなくなり、We.Retail に置き換えられました。Geometrixx のダウンロードおよびインストール方法については、[We.Retail 参照実装](/help/sites-developing/we-retail.md#we-retail-geometrixx)を参照してください。

#### 既存の textimage コンポーネントの拡張 {#extending-the-existing-textimage-component}

新しいコンポーネントを作成するには、標準の textimage コンポーネントをベースとして使用し、それに変更を加えます。ここでは、Geometrixx AEM WCM の例のアプリケーションに新しいコンポーネントを保存します。

1. 標準の textimage コンポーネントを `/libs/foundation/components/textimage` から Geometrixx のコンポーネントフォルダー（`/apps/geometrixx/components`）に、ターゲットノードの名前として textimage を使用してコピーします（コンポーネントに移動し、右クリックして「コピー」を選択し、ターゲットディレクトリをブラウジングすることでコンポーネントをコピーします）。

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. この例ではシンプルに保つために、コピーしたコンポーネントに移動し、新しい textimage ノードから、以下に示すサブノードを除く、すべてのサブノードを削除してください。

   * ダイアログの定義：`textimage/dialog`
   * コンポーネントのスクリプト：`textimage/textimage.jsp`
   * 設定の編集ノード（アセットのドラッグ＆ドロップの許可）：`textimage/cq:editConfig`

   >[!NOTE]
   >
   >ダイアログの定義は、UI に依存します。
   >
   >* タッチ操作対応 UI：`textimage/cq:dialog`
   >* クラシック UI：`textimage/dialog`

1. コンポーネントのメタデータを編集します。

   * コンポーネント名

      * `jcr:description` を `Text Image Component (Extended)` に設定
      * `jcr:title` を `Text Image (Extended)` に設定

   * サイドキック内でコンポーネントが一覧表示されるグループ（修正しない）

      * `componentGroup` を `General` に設定したままにする

   * 新しいコンポーネントの親コンポーネント（標準の textimage コンポーネント）

      * `sling:resourceSuperType` を `foundation/components/textimage` に設定

   この手順を終えると、コンポーネントのノードは以下のようになります。

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 画像の編集設定ノードの `sling:resourceType` プロパティ（プロパティ：`textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`）を `geometrixx/components/textimage.` に変更する

   これで、画像がページ上のコンポーネントにドロップされると、拡張された textimage コンポーネントの `sling:resourceType` プロパティが `geometrixx/components/textimage.` に設定されます。

1. コンポーネントのダイアログボックスを修正して、新しいオプションを含めます。 新しいコンポーネントは、元のコンポーネントと同じダイアログボックスの部分を継承します。 追加するのは、 **詳細** タブ、追加 [ たぶ、ついか ] **画像の位置** ドロップダウンリストとオプション **左** および **右**:

   * `textimage/dialog` プロパティは変更しません。

   `textimage/dialog/items` に、textimage ダイアログボックスの 4 つのタブを表す 4 つのサブノード（tab1 から tab4）があることを確認します。

   * 最初の 2 つのタブ（tab1 と tab2）:

      * xtype を cqinclude に変更します（標準コンポーネントから継承します）。
      * `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json` 値および `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json` 値を持つパスプロパティをそれぞれ追加します。
      * その他のすべてのプロパティまたはサブノードを削除します。

   * tab3 の場合：

      * プロパティとサブノードは変更せずにそのままにします。
      * 新しいフィールドの定義として、`cq:Widget` タイプのノードの場所を `tab3/items` に追加します。
      * 新しい `tab3/items/position` ノードに以下のプロパティ（String タイプ）を設定します。

         * `name`：`./imagePosition`
         * `xtype`：`selection`
         * `fieldLabel`：`Image Position`
         * `type`：`select`

      * 画像の配置の選択肢を 2 つ表すために、`cq:WidgetCollection` タイプのサブノード `position/options` を追加し、その下に、`nt:unstructured` タイプの 2 つのノード（o1 および o2）を作成します。
      * `position/options/o1` ノードの場合、`text` プロパティを `Left` に設定して、`value` プロパティを `left.` に設定します。
      * `position/options/o2` ノードの場合 、プロパティ `text` を `Right` に設定し、プロパティ `value` を `right` に設定します。

   * tab4 を削除します。

   画像の位置は、`textimage` の段落を表すノードの `imagePosition` プロパティとしてコンテンツ内で保持されます。これらの手順を終えると、コンポーネントのダイアログボックスは以下のようになります。

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. コンポーネントのスクリプト、`textimage.jsp` を拡張し、新しいパラメーターの処理を追加します。

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   強調表示したコードのフラグメント *%>&lt;div class=&quot;image&quot;>&lt;%* は、このタグのカスタムスタイルを生成する新しいコードで置き換える予定です。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. コンポーネントをリポジトリに保存します。コンポーネントをテストする準備ができました。

#### 新しいコンポーネントの確認 {#checking-the-new-component}

コンポーネントを開発した後、段落システムに追加できます。これにより、作成者は、ページの編集時にコンポーネントを選択して使用できます。 以下の手順で、コンポーネントをテストできます。

1. 「英語/会社」などのGeometrixxでページを開きます。
1. デザインモードに切り替えるには、[Sidekick] の [ デザイン ] をクリックします。
1. ページの中央にある段落システムの「編集」をクリックして、段落システムのデザインを編集します。 段落システムに配置できるコンポーネントのリストが表示されます。新しく開発したテキスト画像（拡張）が含まれている必要があります。 段落システムを選択し、「 OK 」をクリックしてアクティブにします。
1. 編集モードに戻ります。
1. 段落システムに「テキスト画像（拡張） 」段落を追加し、サンプルコンテンツを使用してテキストと画像を初期化します。 変更内容を保存します。
1. テキストおよび画像段落のダイアログを開き、「詳細」タブの「画像の位置」を「右」に変更し、「 OK 」をクリックして変更を保存します。
1. 段落は、右側に画像が表示された状態でレンダリングされます。
1. コンポーネントを使用する準備ができました。

このコンポーネントは、その内容を会社ページ上の段落に保存します。

### 画像コンポーネントのアップロード機能を無効にする {#disable-upload-capability-of-the-image-component}

アップロード機能を無効にするには、標準の画像コンポーネントをベースとして使用し、それに変更を加えます。Geometrixx の例のアプリケーションに新しいコンポーネントを保存します。

1. ターゲットノードの名前として画像を使用して、`/libs/foundation/components/image` から Geometrixx コンポーネントフォルダー（`/apps/geometrixx/components`）に標準の画像コンポーネントをコピーします。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. コンポーネントのメタデータを編集します。

   * **jcr:title** を `Image (Extended)` に設定します。

1. `/apps/geometrixx/components/image/dialog/items/image`に移動します。
1. 新しいプロパティを追加します。

   * **名前**：`allowUpload`
   * **型**：`String`
   * **値**：`false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 「**すべて保存**」をクリックします。コンポーネントをテストする準備ができました。
1. 「英語/会社」などのGeometrixxでページを開きます。
1. デザインモードに切り替えて、画像（拡張）を有効にします。
1. 編集モードに戻し、段落システムに追加します。 次の画像では、元の画像コンポーネントと先ほど作成した画像コンポーネントの違いを確認できます。

   元の画像コンポーネント：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   新しい画像コンポーネント：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. コンポーネントを使用する準備ができました。
