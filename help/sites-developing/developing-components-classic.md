---
title: Adobe Experience Manager コンポーネント（クラシック UI）の開発
description: クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。HTL は、 Adobe Experience Manager（AEM）の推奨スクリプティング言語ではありません。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '2340'
ht-degree: 100%

---

# Adobe Experience Manager（AEM）コンポーネント（クラシック UI）の開発{#developing-aem-components-classic-ui}

クラシック UI では、ExtJS を使用して、コンポーネントのルックアンドフィールを提供するウィジェットを作成します。これらのウィジェットの性質により、コンポーネントがクラシック UI と[タッチ操作対応 UI](/help/sites-developing/developing-components.md)とどのように相互作用するかにはいくつかの違いがあります。

>[!NOTE]
>
>コンポーネント開発の多くの側面はクラシック UI とタッチ操作向け UI に共通なので、このページを使用する](/help/sites-developing/components-basics.md)前に&#x200B;**、AEM コンポーネント - 基本**&#x200B;を必ずお読みください[。クラシック UI の詳細が記載されています。

>[!NOTE]
>
>クラシック UI 用のコンポーネントの開発には HTML テンプレート言語（HTL）と JSP のどちらも使用できますが、このページでは JSP を使用した開発について説明します。これは単に、クラシック UI 内では JSP が使用されてきたからです。
>
>現在では、HTL が AEM の推奨スクリプティング言語とされています。手法を比較するには、[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja) および [AEM コンポーネントの開発](/help/sites-developing/developing-components.md)を参照してください。

## 構造 {#structure}

コンポーネントの基本構造については、タッチ操作対応 UI とクラシック UI の両方に適用される [AEM コンポーネント - 基本](/help/sites-developing/components-basics.md#structure)ページで説明しています。新しいコンポーネントでタッチ操作対応 UI の設定を使用する必要がない場合でも、この情報は既存のコンポーネントを継承する際に設定を把握するのに役立ちます。

## JSP スクリプト {#jsp-scripts}

JSP スクリプトまたはサーブレットを使用して、コンポーネントをレンダリングできます。Sling のリクエスト処理ルールに従って、デフォルトスクリプトの名前は次のようになります。

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP スクリプトファイル `global.jsp` は、コンポーネントのレンダリングに使用される JSP スクリプトファイルに対して、特定オブジェクトへの素早いアクセス（つまり、コンテンツへのアクセス）を提供するために使用されます。

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
   * `designer` - デザイン情報を取得するための Designer オブジェクト（`resourceResolver.adaptTo(Designer.class);`）。
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

CQ と Sling のタグライブラリを使用すると、テンプレートやコンポーネントの JSP スクリプトで使用する特定の機能にアクセスできます。

詳しくは、[タグライブラリ](/help/sites-developing/taglib.md)ドキュメントを参照してください。

## クライアント側 HTML ライブラリの使用 {#using-client-side-html-libraries}

最近の web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題に対処するために、AEM では、**クライアントサイドのライブラリフォルダー**&#x200B;が提供されています。これにより、クライアントサイドコードをリポジトリに格納し、カテゴリ別に整理し、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義することができます。その後、クライアントサイドライブラリシステムにより、最終的な web ページで、正しいコードを読み込むための正しいリンクが作成されます。

詳しくは、[クライアントサイド HTML ライブラリの使用](/help/sites-developing/clientlibs.md)ドキュメントを参照してください。

## ダイアログ {#dialog}

コンポーネントのコンテンツを作成者が追加したり設定できるようにするには、ダイアログが必要です。

詳しくは、[AEM コンポーネント - 基本](/help/sites-developing/components-basics.md#dialogs)を参照してください。

## 編集動作の設定 {#configuring-the-edit-behavior}

コンポーネントの編集動作を設定できます。コンポーネントに対して使用可能なアクションなどの属性、インプレースエディターの特性、コンポーネントに対するイベントに関連するリスナーについても説明します。固有の相違点は多少ありますが、設定はタッチ操作向け UI とクラシック UI の両方に共通です。

[コンポーネントの編集動作](/help/sites-developing/components-basics.md#edit-behavior)は、タイプ `cq:EditConfig` の `cq:editConfig` ノードをコンポーネントノード（タイプ `cq:Component`）の下に追加し、特定のプロパティと子ノードを追加して設定します。

## ExtJS ウィジェットの使用と拡張 {#using-and-extending-extjs-widgets}

詳しくは、[ExtJS ウィジェットの使用と拡張](/help/sites-developing/widgets.md)を参照してください。

## ExtJS ウィジェットに xtype を使用 {#using-xtypes-for-extjs-widgets}

詳しくは、[xtype の使用](/help/sites-developing/xtypes.md)を参照してください。

## 新しいコンポーネントの開発 {#developing-new-components}

この節では、独自のコンポーネントを作成し、それを段落システムに追加する方法について説明します。

既存のコンポーネントをコピーし、必要な変更を行うことが、開発を始めるうえで最も簡単な方法です。

コンポーネントの開発方法の例について詳しくは、「[テキストコンポーネントと画像コンポーネントの拡張 - 例](#extending-the-text-and-image-component-an-example)」を参照してください。

### 新しいコンポーネントの開発（既存のコンポーネントの利用） {#develop-a-new-component-adapt-existing-component}

既存のコンポーネントをベースに新しい AEM コンポーネントを開発するには、既存のコンポーネントをコピーし、新しいコンポーネント用の JavaScript ファイルを作成して、AEM からアクセスできる場所に保存します。[コンポーネントおよびその他の要素のカスタマイズ](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)も参照してください。

1. CRXDE Lite を使用して、新しいコンポーネントフォルダーを以下の場所に作成します。

   / `apps/<myProject>/components/<myComponent>`

   libs 内にあるものと同じノード構造を再作成してから、テキストコンポーネントなどの既存のコンポーネントの定義をコピーします。例えば、テキストコンポーネントをカスタマイズするには、次のようにコピーします。

   * コピー元：`/libs/foundation/components/text`
   * コピー先：`/apps/myProject/components/text`

1. `jcr:title` を変更して新しい名前を反映させます。
1. 新しいコンポーネントフォルダーを開き、必要な変更を行います。また、フォルダー内にある不要な情報を削除します。

   例えば、次のような変更を行うことができます。

   * ダイアログボックスへのフィールドの追加

      * `cq:dialog` - タッチ操作対応 UI 用ダイアログ
      * `dialog` - クラシック UI 用ダイアログ

   * `.jsp` ファイルの置換（新しいコンポーネントの作成後に名前を付けます）
   * または、コンポーネント全体の作成し直し（必要な場合）

   例えば、標準テキストコンポーネントのコピーを作成した場合は、ダイアログボックスにフィールドを追加して、`.jsp` を更新し、そこに追加された情報を処理します。

   >[!NOTE]
   >
   >使用するコンポーネント：
   >
   >* タッチ操作対応 UI では [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) コンポーネントを使用します
   >* クラシック UI では [ExtJS ウィジェット](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を使用します

   >[!NOTE]
   >
   >クラシック UI 用に定義したダイアログは、タッチ操作対応 UI 内で動作します。
   >
   >タッチ操作対応 UI 用に定義したダイアログは、クラシック UI 内では動作しません。
   >
   >インスタンスとオーサー環境によっては、コンポーネント用に両方のタイプのダイアログを定義する必要があるかもしれません。

1. 新しいコンポーネントを表示するには、次のいずれかのノードが存在し、適切に初期化されている必要があります。

   * `cq:dialog` - タッチ操作対応 UI 用ダイアログ
   * `dialog` - クラシック UI 用ダイアログ
   * `cq:editConfig` - 編集環境でのコンポーネントの動作（ドラッグ＆ドロップなど）
   * `design_dialog` - デザインモード用ダイアログ（クラシック UI のみ）

1. 次のどちらかの方法で、段落システムで新しいコンポーネントを利用できるようにします。

   * CRXDE Lite を使用して、ノード `/etc/designs/geometrixx/jcr:content/contentpage/par` の適切なコンポーネントに、値 `<path-to-component>`（`/apps/geometrixx/components/myComponent` など）を追加します。
   * [段落システムへの新しいコンポーネントの追加](#adding-a-new-component-to-the-paragraph-system-design-mode)の手順を実行します。

1. AEM WCM で、web サイトのページを開き、作成した新しいタイプの段落を挿入してコンポーネントが正常に動作することを確認します。

>[!NOTE]
>
>ページ読み込みのタイミングの統計を確認するには、Ctrl + Shift + U キーを、URL で設定されている `?debugClientLibs=true` と共に使用します。

### 段落システムへの新しいコンポーネントの追加（デザインモード） {#adding-a-new-component-to-the-paragraph-system-design-mode}

コンポーネントを開発したら、段落システムに追加します。この操作により、ページの編集時に、作成者がコンポーネントを選択して使用できるようになります。

1. 段落システムを使用するオーサリング環境でページにアクセスします（例：`<contentPath>/Test.html`）。
1. 次のどちらかの方法でデザインモードに切り替えます。

   * 以下の例のように、URL の最後に `?wcmmode=design` を追加し、再度アクセスします。

     `<contextPath>/ Test.html?wcmmode=design`

   * サイドキックで「デザイン」をクリックします。

   デザインモードになり、段落システムを編集できるようになります。

1. 「編集」をクリックします。

   その段落システムに所属するコンポーネントのリストが一覧表示されます。新しいコンポーネントも一覧に表示されます。

   これらのコンポーネントをアクティベートまたはアクティベート解除することで、ページの編集時に作成者に提供するコンポーネントを決定できます。

1. コンポーネントをアクティベートしたら、標準編集モードに戻り、利用可能かどうかを確認します。

### テキストコンポーネントと画像コンポーネントの拡張 - 例 {#extending-the-text-and-image-component-an-example}

この節では、広く利用されているテキストと画像の標準コンポーネントを、設定可能な画像配置機能を使用して拡張する方法について説明します。

テキストコンポーネントと画像コンポーネントの拡張により、エディターは、コンポーネントのすべての既存機能を使用できるだけでなく、次のどちらかの方法で画像の配置を指定できる追加のオプションも利用できます。

* テキストの左側（現在の動作および新しいデフォルト）
* 右側に

このコンポーネントを拡張したら、コンポーネントのダイアログボックスを使用して画像の配置を設定できます。

この演習では、以下の方法を説明します。

* 既存のコンポーネントノードのコピーとメタデータの変更
* コンポーネントのダイアログの変更（親ダイアログボックスからのウィジェットの継承を含む）
* 新機能を実装するためのコンポーネントのスクリプトの変更

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

1. コンポーネントのダイアログボックスを変更して、新しいオプションを含めます。新しいコンポーネントは、元のコンポーネントと同じダイアログボックスの部分を継承します。唯一の追加は「**詳細**」タブを拡張することで、**左**&#x200B;と&#x200B;**右**&#x200B;のオプションが付いた&#x200B;**画像の位置**&#x200B;ドロップダウンリストを追加します。

   * `textimage/dialog` プロパティは変更しません。

   `textimage/dialog/items` に、textimage ダイアログボックスの 4 つのタブを表す 4 つのサブノード（tab1 から tab4）があることを確認します。

   * 最初の 2 つのタブ（tab1 と tab2）：

      * xtype を cqinclude に変更します（標準コンポーネントから継承）。
      * `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json` 値および `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json` 値を持つパスプロパティをそれぞれ追加します。
      * その他のすべてのプロパティまたはサブノードを削除します。

   * tab3 の場合：

      * プロパティとサブノードは変更せずにそのままにします。
      * タイプ `cq:Widget` のノードの場所 `tab3/items` にフィールドの定義を追加します。
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

   強調表示したコードのフラグメント *%>&lt;div class=&quot;image&quot;>&lt;%* は、このタグのカスタムスタイルを生成する新しいコードで置き換えます。

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

コンポーネントを開発した後、段落システムに追加できます。これにより、作成者は、ページの編集時にコンポーネントを選択して使用できます。次の手順で、コンポーネントをテストできます。

1. 英語／会社などの Geometrixx でページを開きます。
1. サイドキックで「デザイン」をクリックし、デザインモードに切り替えます。
1. ページの中央の段落システムで、「編集」をクリックし、段落システムのデザインを編集します。段落システムに配置できるコンポーネントの一覧が表示されます。一覧には、新しく開発した Text Image (Extended) コンポーネントも含まれます。コンポーネントを選択し、「OK」をクリックして、段落システムに対してコンポーネントをアクティベートします。
1. 編集モードに戻します。
1. Text Image (Extended) 段落を段落システムに追加し、サンプルコンテンツでテキストと画像を初期化します。変更内容を保存します。
1. テキストと画像の段落のダイアログを開き、「詳細」タブで画像の位置を「右」に変更し、「OK」をクリックして変更を保存します。
1. 段落の右側に画像がレンダリングされます。
1. コンポーネントを使用する準備ができました。

コンポーネントには、会社ページの段落のコンテンツが格納されます。

### 画像コンポーネントのアップロード機能を無効にする {#disable-upload-capability-of-the-image-component}

この機能を無効にするには、標準画像コンポーネントをベースとして使用し、それに変更を加えます。Geometrixx の例のアプリケーションに新しいコンポーネントを保存します。

1. ターゲットノードの名前として画像を使用して、`/libs/foundation/components/image` から Geometrixx コンポーネントフォルダー（`/apps/geometrixx/components`）に標準の画像コンポーネントをコピーします。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. コンポーネントのメタデータを編集します。

   * **jcr:title** を `Image (Extended)` に設定します。

1. `/apps/geometrixx/components/image/dialog/items/image`に移動します。
1. プロパティを追加します。

   * **名前**：`allowUpload`
   * **型**：`String`
   * **値**：`false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 「**すべて保存**」をクリックします。コンポーネントをテストする準備ができました。
1. 英語／会社などの Geometrixx でページを開きます。
1. デザインモードに切り替え、Image (Extended) をアクティブ化します。
1. 編集モードに切り替え、画像を段落システムに追加します。次の画像で、元の画像コンポーネントと先ほど作成したコンポーネントの違いを確認できます。

   元の画像コンポーネント：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   新しい画像コンポーネント：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. コンポーネントを使用する準備ができました。
