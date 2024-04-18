---
title: ウィジェットの使用および拡張（クラシック UI）
description: Adobe Experience Manager の web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術を使用しています。これらの技術により、作成者は、web ページ上でコンテンツの WYSIWYG 編集や書式設定を行うことができます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 100%

---

# ウィジェットの使用および拡張（クラシック UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>このページでは、AEM 6.4 で廃止されたクラシック UI でのウィジェットの使用方法について説明します。
>
>アドビでは、[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) と [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components) をベースとした、最新の[タッチ操作対応 UI](/help/sites-developing/touch-ui-concepts.md) の使用を推奨しています。

Adobe Experience Manager（AEM）の web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術を使用しています。これらの技術により、作成者は、web ページ上でコンテンツの WYSIWYG 編集や書式設定を行うことができます。

AEM は [ExtJS](https://www.sencha.com/) ウィジェットライブラリを使用しています。このライブラリは、高度に洗練されたユーザーインターフェイス要素を提供するものであり、すべての重要なブラウザーで機能し、デスクトップグレードの UI エクスペリエンスを作成できます。

これらのウィジェットは AEM に組み込まれており、AEM 自体でも使用されていますが、AEM で作成した任意の web サイトでも使用できます。

AEM で使用可能なすべてのウィジェットについて詳しくは、[ウィジェット API ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)または[既存の xtype のリスト](/help/sites-developing/xtypes.md)を参照してください。また、ExtJS フレームワークを所有している [Sencha](https://examples.sencha.com/extjs/7.6.0/) のサイトには、ExtJS フレームワークの使用方法の例が多数掲載されています。

このページでは、ウィジェットの使用方法と拡張方法に関するインサイトを提供します。まず、[ページにクライアントサイドコードを含める](#including-the-client-sided-code-in-a-page)方法を説明します。次に、いくつかのコンポーネントの例を使用して、基本的な使用と拡張について説明します。これらのコンポーネントは、**Package Share** の **Using ExtJS Widgets** というパッケージにあります。

このパッケージには、次の例が含まれています。

* すぐに使用できるウィジェットで作成した[基本ダイアログ](#basic-dialogs)。
* すぐに使用できるウィジェットとカスタマイズされた Javascript ロジックで作成した[動的ダイアログ](#dynamic-dialogs)。
* [カスタムウィジェット](#custom-widgets)を基にしたダイアログ。
* 特定のパスの下に JCR ツリーを表示する[ツリーパネル](#tree-overview)。
* 表形式でデータを表示する[グリッドパネル](#grid-overview)。

>[!NOTE]
>
>Adobe Experience Manager のクラシック UI は、[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/) をベースに構築されています。

## クライアントサイドのコードをページに含める {#including-the-client-sided-code-in-a-page}

クライアントサイドの JavaScript とスタイルシートのコードをクライアントライブラリに配置します。

クライアントライブラリを作成するには：

1. `/apps/<project>` の下にノードを作成し、次のプロパティを設定します。

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. `clientlib` の下に `css` フォルダーと `js` フォルダー（nt:folder）を作成します。

1. `clientlib` の下に `css.txt` ファイルと `js.txt` ファイル（nt:file）を作成します。これらの .txt ファイルには、ライブラリに組み込むファイルを記述します。

1. `js.txt` を編集します。このファイルは、先頭に「`#base=js`」を指定し、その後に CQ クライアントライブラリサービスによって集約されるファイルのリストを指定する必要があります。以下に例を示します。

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. `css.txt` を編集します。このファイルは、先頭に「`#base=css`」を指定し、その後に CQ クライアントライブラリサービスによって集約されるファイルのリストを指定する必要があります。以下に例を示します。

   ```
   #base=css
    components.css
   ```

1. `js` フォルダーの下に、ライブラリに属する JavaScript ファイルを配置します。

1. `css` フォルダーの下に、`.css` ファイルと、css ファイルが使用するリソース（`my_icon.png` など）を配置します。

>[!NOTE]
>
>前述のスタイルシートの処理は、必要に応じて行います。

ページコンポーネント jsp にクライアントライブラリを組み込むには：

* JavaScript コードとスタイルシートの両方を組み込むには：
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
`<category-nameX>` はクライアントサイドのライブラリの名前です。

* JavaScript コードのみを組み込むには：
  `<ui:includeClientLib js="<category-name>"/>`

詳しくは、[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) タグの説明を参照してください。

クライアントライブラリは、オーサーモードでしか使用できず、パブリッシュモードでは除外する必要が生じる場合があります。これを行うには、次のように設定します。

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### サンプルの概要 {#getting-started-with-the-samples}

このページのチュートリアルに従うには、**Using ExtJS Widgets** というパッケージをローカル AEM インスタンスにインストールして、コンポーネントを組み込むサンプルページを作成します。これを行うには、次の手順を実行します。

1. AEM インスタンスで、Package Share から **Using ExtJS Widgets (v01)** というパッケージをダウンロードしてインストールします。リポジトリの `/apps` の下に `extjstraining` という名前のプロジェクトが作成されます。
1. スクリプト（js）とスタイルシート（css）を含むクライアントライブラリを、Geometrixx ページ jsp の head タグに含めます。サンプルコンポーネントを **Geometrixx** ブランチの新しいページに含めることになります。
**CRXDE Lite** で `/apps/geometrixx/components/page/headlibs.jsp` ファイルを開き、`cq.extjstraining` カテゴリを既存の `<ui:includeClientLib>` タグに次のように追加します。
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. `/content/geometrixx/en/products` の下にある **Geometrixx** ブランチに新しいページを作成し、**Using ExtJS Widgets** という名前を付けます。
1. デザインモードに切り替え、**Using ExtJS Widgets** という名前のグループのすべてのコンポーネントを Geometrixx のデザインに追加します。
1. 編集モードに戻ります。サイドキックで **Using ExtJS Widgets**&#x200B;グループのコンポーネントが使用可能になります。

>[!NOTE]
>
>このページの例は、Geometrixx サンプルコンテンツに基づいています。これは現在、AEM には付属しておらず、We.Retail に置き換えられています。Geometrixx のダウンロード方法とインストール方法については、[We.Retail 参照の実装](/help/sites-developing/we-retail.md#we-retail-geometrixx)を参照してください。

### 基本ダイアログ {#basic-dialogs}

通常、ダイアログはコンテンツの編集に使用されますが、情報の表示も可能です。完全なダイアログを簡単に表示するには、JSON 形式の表現にアクセスします。これを行うには、ブラウザーで次のように指定します。

`https://localhost:4502/<path-to-dialog>.-1.json`

サイドキックにある **Using ExtJS Widgets** グループの最初のコンポーネントは、**1. ダイアログの基本**&#x200B;という名前で、4 つの基本ダイアログが入っています。これらのダイアログは、すぐに使用できるウィジェットで作成されており、カスタマイズした Javascript ロジックは含まれていません。ダイアログは、`/apps/extjstraining/components/dialogbasics` の下に保存されています。基本的なダイアログを次に示します。

* フルダイアログ（`full` ノード）：3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。
* 単一パネルダイアログ（`singlepanel` ノード）：1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。
* 複数パネルダイアログ（`multipanel` ノード）：表示内容はフルダイアログと同じですが、ダイアログの作成の仕方が異なります。
* Design ダイアログ（`design` ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折りたたみ可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折りたたみ可能なフィールドセットがあります。

次の手順に従って、**1. ダイアログの基本**&#x200B;コンポーネントをサンプルページに組み込みます。

1. **1 を追加します。Dialog Basics** コンポーネントを&#x200B;**サイドキック**&#x200B;の「**ExtJS ウィジェットの使用**」タブからサンプルページに追加します。
1. このコンポーネントには、タイトル、テキスト、**プロパティ**&#x200B;リンクが表示されます。リンクを選択すると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-60](assets/chlimage_1-60.png)

#### 例 1：フルダイアログ {#example-full-dialog}

**Full** ダイアログには、3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。これは、**ダイアログの基本**&#x200B;コンポーネントのデフォルトダイアログです。特性は次のとおりです。

* ノード（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）によって定義されます。
* タブ（node type = `cq:Panel`）を 3 つを表示します。
* 各タブには、テキストフィールドが 2 つあります（node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* ノードによって定義されます。
  `/apps/extjstraining/components/dialogbasics/full`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

ダイアログが次のように表示されます。

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 例 2：単一パネルダイアログ {#example-single-panel-dialog}

**単一パネル**&#x200B;ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。特性は次のとおりです。

* タブ（node type = `cq:Dialog`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）を 1 つ表示します。
* このタブには、2 つのテキストフィールド（node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）があります。
* ノードによって定義されます。
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* **フルダイアログ**&#x200B;の利点の一つは、必要な設定が少ないことです。
* 推奨される用途：情報を表示するだけの、またはフィールドが数個しかない単純なダイアログ。

単一パネルダイアログを使用するには：

1. **ダイアログの基本**&#x200B;コンポーネントのダイアログを **単一パネル**&#x200B;ダイアログに置き換えます。
   1. **CRXDE Lite** で、次のノードを削除します。`/apps/extjstraining/components/dialogbasics/dialog`
   1. 「**すべて保存**」をクリックして変更を保存します。
   1. 次のノードをコピーします。`/apps/extjstraining/components/dialogbasics/singlepanel`
   1. コピーしたノードを次に貼り付けます。`/apps/extjstraining/components/dialogbasics`
   1. ノード `/apps/extjstraining/components/dialogbasics/Copy of singlepanel` を選択して、名前を `dialog` に変更します。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 例 3：複数パネルダイアログ {#example-multi-panel-dialog}

**複数パネルl** ダイアログは、**フル**&#x200B;ダイアログと同じ表示内容ですが、ダイアログの作成の仕方が異なります。特性は次のとおりです。

* ノード（node type = `cq:Dialog`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）によって定義されます。
* タブ（node type = `cq:Panel`）を 3 つを表示します。
* 各タブには、テキストフィールドが 2 つあります（node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* ノードによって定義されます。
  `/apps/extjstraining/components/dialogbasics/multipanel`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* **フルダイアログ**&#x200B;より有利な点は、構造が簡単なことです。
* 複数のタブを持つダイアログでの使用を推奨します。

複数パネルダイアログを使用するには：

1. **ダイアログの基本**&#x200B;コンポーネントのダイアログを&#x200B;**複数パネル**ダイアログに置き換えます。
[例 2：単一パネルダイアログ](#example-single-panel-dialog)で説明している手順に従います。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 例 4：リッチダイアログ {#example-rich-dialog}

**リッチ**&#x200B;ダイアログには、2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折りたたみ可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折りたたみ可能なフィールドセットがあります。特性は次のとおりです。

* ノード（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）によって定義されます。
* 3 つのタブ（node type = `cq:Panel`）が表示されます。
* 最初のタブには、` [textfield](/help/sites-developing/xtypes.md#textfield)` を含む ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` ウィジェットと 3 つのオプションを含む ` [selection](/help/sites-developing/xtypes.md#selection)` ウィジェットに加え、` [textarea](/help/sites-developing/xtypes.md#textarea)` ウィジェットを含む折りたたみ可能な ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` があります。
* 2 つ目のタブには、4 つの ` [textfield](/help/sites-developing/xtypes.md#textfield)` ウィジェットを含む ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` ウィジェットと、2 つの ` [textfield](/help/sites-developing/xtypes.md#textfield)` ウィジェットを含む折りたたみ可能な `dialogfieldset` があります。
* ノードによって定義されます。
  `/apps/extjstraining/components/dialogbasics/rich`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

**リッチ**&#x200B;ダイアログを使用するには：

1. **ダイアログの基本**&#x200B;コンポーネントのダイアログを&#x200B;**リッチ**ダイアログに置き換えます。
[例 2：単一パネルダイアログ](#example-single-panel-dialog)で説明している手順に従います。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### 動的ダイアログ {#dynamic-dialogs}

サイドキックにある **Using ExtJS Widgets** グループの 2 番目のコンポーネントは、**2. Dynamic Dialogs** という名前で、3 つの動的ダイアログが含まれています。これらのダイアログは、すぐに使用できるウィジェットと、**カスタマイズされた Javascript ロジック**&#x200B;から作成されています。ダイアログは、`/apps/extjstraining/components/dynamicdialogs` の下に保存されます。動的ダイアログは次のようになります。

* タブ切り換えダイアログ（`switchtabs` ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。
*  任意ダイアログ（`arbitrary` ノード）。タブが 1 つあるウィンドウが表示されます。このタブには、フィールドが 2 つあります。一つは、アセットをドロップまたはアップロードするためのフィールド、もう一つは、コンポーネントを含むページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。
* フィールド切り換えダイアログ（`togglefield` ノード）：タブが 1 つあるウィンドウが表示されます。このタブには、チェックボックスが 1 つあります。このチェックボックスを選択すると、テキストフィールドを 2 つ含むフィールドセットが表示されます。

**2. 動的ダイアログ**&#x200B;コンポーネントをサンプルページに組み込むには：

1. **2. Dynamic Dialogs** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブから）。
1. このコンポーネントには、タイトル、テキスト、**プロパティ**&#x200B;リンクが表示されます。リンクを選択すると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 例 1：Switch Tabs ダイアログ {#example-switch-tabs-dialog}

**Switch Tabs** ダイアログには、２ つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。

このダイアログの主な特徴を次に示します。

* ノード（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）によって定義されます。
* タブが 2 つ表示されます（node type = `cq:Panel`）。1 つ目は選択タブです。2 つ目のタブは、1 つ目のタブで 3 つのオプションのどれを選択したかによって変わります。
* オプションタブが 3 つあります（node type = `cq:Panel`）。それぞれのオプションタブには、2 つのテキストフィールドがあります（node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。オプションタブは、同時に 1 つしか表示されません。
* 次の場所にある `switchtabs` ノードによって定義されます。
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

ロジックは、次のようにイベントリスナーと JavaScript コードによって実装されています。

* ダイアログノードには、ダイアログを表示する前にすべてのオプションタブを非表示にする「`beforeshow`」リスナーがあります。
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` は、selection パネルと 3 つのオプションパネルを含んだ `tabpanel` を取得します。
* `Ejst.x2` オブジェクトは、次の場所にある `exercises.js` ファイルで定義します。
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.manageTabs()` メソッドで `index` の値を -1 にすると、すべてのオプションタブが非表示になります（i は 1 から 3 です）。
* selection タブにはリスナーが 2 つあります。ダイアログの読み込み（「`loadcontent`」イベント）時に選択済みのタブを表示するリスナーと、selection の変更（「`selectionchanged`」イベント）時に選択済みのタブを表示するリスナーです。
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* `Ejst.x2.showTab()` メソッドの場合、
  `field.findParentByType('tabpanel')` は、すべてのタブを含んだ `tabpanel` を取得します（`field` は selection ウィジェットを表します）。
  `field.getValue()` は、selection の値（例：tab2）を取得します。
  `Ejst.x2.manageTabs()` は選択したタブを表示します。
* 各オプションタブには、「`render`」イベントでタブを非表示にするリスナーがあります。
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* `Ejst.x2.hideTab()` メソッドの場合、
  `tabPanel` は、すべてのタブを含んだ `tabpanel` です。
  `index` はオプションタブのインデックスです
  `tabPanel.hideTabStripItem(index)` はタブを非表示にします

次のように表示されます。

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 例 2：任意ダイアログ {#example-arbitrary-dialog}

ほとんどの場合、ダイアログには、基になるコンポーネントからのコンテンツが表示されます。ここで説明する&#x200B;**任意**&#x200B;ダイアログは、別のコンポーネントからコンテンツを取り込みます。

**Arbitrary** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのフィールドがあります。アセットをドロップまたはアップロードするためのフィールドと、コンポーネントを含んだページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。

このダイアログの主な特徴を次に示します。

* ノード（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）によって定義されます。
* 1 つの `tabpanel` ウィジェット（node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）と 1 つのパネル（node type = `cq:Panel`）を表示します。
* パネルには、smartfile ウィジェット（node type = `cq:Widget`、xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`）と ownerdraw ウィジェット（node type = `cq:Widget`、xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`）があります。
* 次の場所にある `arbitrary` ノードによって定義されます。
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

ロジックは、次のようにイベントリスナーと JavaScript コードによって実装されています。

* `ownerdraw` ウィジェットには、コンポーネントを含んだページに関する情報を表示する「`loadcontent`」リスナーがあります。つまり、コンテンツの読み込み時に smartfile ウィジェットで参照されるアセットです。
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` は `ownerdraw` オブジェクトで設定されます。
  `path` は、コンポーネントのコンテンツパス（例：`/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`）で設定されます。
* `Ejst.x2` オブジェクトは、次の場所にある `exercises.js` ファイルで定義されます。
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.showInfo()` メソッドの場合、
  `pagePath` は、コンポーネントを含んだページのパスです。
  `pageInfo` は、ページプロパティを JSON 形式で表します。
  `reference` は、参照されるアセットのパスです。
  `metadata` は、アセットのメタデータを JSON 形式で表します。
  `ownerdraw.getEl().update(html);` は、作成した html をダイアログに表示

**任意** ダイアログを使用するには：

1. **動的ダイアログ**&#x200B;コンポーネントのダイアログを&#x200B;**任意の**ダイアログに置き換えます。
[例 2：単一パネルダイアログ](#example-single-panel-dialog)で説明している手順に従います。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 例 3：Toggle Fields ダイアログ {#example-toggle-fields-dialog}

**Toggle Fields** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、チェックボックスが 1 つあります。このチェックボックスを選択すると、テキストフィールドを 2 つ含むフィールドセットが表示されます。

このダイアログの主な特徴を次に示します。

* ノード（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）によって定義されます。
* 1 つの `tabpanel` ウィジェット（node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`）と 1 つのパネル（node type = `cq:Panel`）を表示します。
* このパネルには、selection／checkbox ウィジェット（node type = `cq:Widget`、xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`、type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`）と、2 つの textfield ウィジェット（node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）を持つ折り畳み可能な dialogfieldset ウィジェット（node type = `cq:Widget`、xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`）があります。後者はデフォルトで非表示になっています。
* 次の場所にある `togglefields` ノードによって定義されます。
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

ロジックは、次のようにイベントリスナーと JavaScript コードによって実装されています。

* selection タブにはリスナーが 2 つあります。コンテンツの読み込み（「`loadcontent`」イベント）時に dialogfieldset を表示するリスナーと、selection の変更（「`selectionchanged`」イベント）時に dialogfieldset を表示するリスナーです。
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2` オブジェクトは、次の場所にある `exercises.js` ファイルで定義します。
  `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.toggleFieldSet()` メソッドの場合、
  `box` は selection オブジェクトです。
  `panel` は、selection ウィジェットと dialogfieldset ウィジェットを含んだパネルです。
  `fieldSet` は dialogfieldset オブジェクトです。
  `show` は selection の値（true または false）です。
「`show`」に基づいて dialogfieldset が表示されているかどうかが決まります。

**Toggle Fields** ダイアログを使用するには、次の手順を実行します。

1. **動的ダイアログ**&#x200B;コンポーネントのダイアログを&#x200B;**フィールドを切り換え**ダイアログに置き換えます。
[例 2：単一パネルダイアログ](#example-single-panel-dialog)で説明している手順に従います。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### カスタムウィジェット {#custom-widgets}

AEM 付属のすぐに使用できるウィジェットは、ほとんどのユースケースに対応しています。ただし、プロジェクト固有の要件に対応するために、カスタムウィジェットの作成が必要になることもあります。カスタムウィジェットは、既存のウィジェットを拡張して作成できます。こうしたカスタマイズを行う際の手助けとなるように、**`Using ExtJS Widgets`** パッケージには、3 つの異なるカスタムウィジェットを使用する 3 つのダイアログが含まれています。

* 複数フィールドダイアログ（`multifield` ノード）は、タブが 1 つあるウィンドウを表示します。このタブには、カスタマイズされた multifield ウィジェットがあり、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドが含まれています。このタブは、デフォルトの `multifield` ウィジェット（テキストフィールドのみを持つ）に基づいているので、`multifield` ウィジェットの機能をすべて使用できます。
* ツリー参照ダイアログ（`treebrowse` ノード）。このダイアログに表示されるウィンドウには、パス参照ウィジェットを含む 1 つのタブがあります。矢印をクリックすると、ウィンドウが開き、階層を参照しながら項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。
* リッチテキストエディタープラグインベースのダイアログ（`rteplugin` ノード）。リッチテキストエディターにカスタムボタンを追加したもので、メインテキストにカスタムテキストを挿入できます。`richtext` ウィジェット（RTE）と、RTE プラグインメカニズムを通じて追加されたカスタム機能から構成されています。

カスタムウィジェットとプラグインは、**3. Custom Widgets**（**Using ExtJS Widgets** パッケージに属する）という名前のコンポーネントに含まれています。このコンポーネントをサンプルページに組み込むには：

1. **3. Custom Widgets** コンポーネントを、**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブからサンプルページに追加します。
1. このコンポーネントには、タイトルとテキストが表示されます。また、**PROPERTIES** リンクをクリックすると、リポジトリに格納されている段落のプロパティも表示されます。もう一度クリックすると、プロパティが非表示になります。
このコンポーネントは、次のように表示されます。

![chlimage_1-62](assets/chlimage_1-62.png)

#### 例 1：Custom Multifield ウィジェット {#example-custom-multifield-widget}

**Custom Multifield** ウィジェットベースのダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、カスタマイズされた multifield ウィジェットがあります。標準の multifield ウィジェットには 1 つのフィールドがありますが、このウィジェットには、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドがあります。

**Custom Multifield** ウィジェットベースのダイアログ：

* ノードで定義されます（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* パネル（node type = `cq:Widget`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）を含んだ 1 つの `tabpanel` ウィジェット（node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）を表示します。
* このパネルには、`multifield` ウィジェット（node type = `cq:Widget`、xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`）があります。
* `multifield` ウィジェットには、カスタム xtype 「`ejstcustom`」に基づく fieldconfig（node type = `nt:unstructured`、xtype = `ejstcustom`、optionsProvider = `Ejst.x3.provideOptions`）があります。
   * 「`fieldconfig`」は、` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)` オブジェクトの設定オプションです。
   * 「`optionsProvider`」は、`ejstcustom` ウィジェットの設定です。`Ejst.x3.provideOptions` メソッドで設定されます。このメソッドは、次の場所にある `exercises.js` で定義されます。
     `/apps/extjstraining/clientlib/js/exercises.js`
2 つのオプションを返します。
* 次の場所にある `multifield` ノードによって定義されます。
  `/apps/extjstraining/components/customwidgets/multifield`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

カスタム `multifield` ウィジェット（xtype = `ejstcustom`）：

* `Ejst.CustomWidget` という名前の JavaScript オブジェクトです。
* 次の場所にある `CustomWidget.js` JavaScript ファイルで定義されます。
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` ウィジェットを拡張します。
* `hiddenField`（テキストフィールド）、`allowField`（コンボボックス）および `otherField`（テキストフィールド）という 3 つのフィールドがあります。
* `CQ.Ext.Component#initComponent` を上書きして 3 つのフィールドを追加します。
   * `allowField` は「select」型のオブジェクト [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) です。optionsProvider は、ダイアログで定義された CustomWidget の optionsProvider 設定でインスタンス化される Selection オブジェクトの設定です。
   * `otherField` は、[CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField) オブジェクトです。
* [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) のメソッド `setValue`、`getValue`、`getRawValue` を上書きして、次の形式の CustomWidget の値を設定および取得します。
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`。
* 自分自身を「`ejstcustom`」 xtype として登録します。
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**Custom Multifield** ウィジェットベースのダイアログは、次のように表示されます。

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 例 2：カスタム `Treebrowse` ウィジェット {#example-custom-treebrowse-widget}

カスタム **`Treebrowse`** ウィジェットベースのダイアログには、カスタムパスの参照ウィジェットを含む 1 つのタブを持つウィンドウが表示されます。矢印を選択すると、ウィンドウが開き、階層を参照して項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。

カスタム `treebrowse` ダイアログ：

* ノードによって定義されます（node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* パネル（node type = `cq:Widget`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）を含む 1 つの `tabpanel` ウィジェット（node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）を表示します。
* このパネルには、カスタムウィジェット（node type = `cq:Widget`、xtype = `ejstbrowse`）があります。
* 次の場所にある `treebrowse` ノードによって定義されます。
  `/apps/extjstraining/components/customwidgets/treebrowse`
* 次をリクエストすることにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

カスタム treebrowse ウィジェット（xtype = `ejstbrowse`）：

* `Ejst.CustomWidget` という名前の JavaScript オブジェクトです
* 次の場所にある `CustomBrowseField.js` JavaScript ファイルに定義されています。
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)` を拡張します。
* `browseWindow` という名前の参照ウィンドウを定義します。
* 矢印がクリックされたときに参照ウィンドウを表示するように ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` を上書きします。
* [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) オブジェクトを定義します。
   * このオブジェクトのデータを取得するには、`/bin/wcm/siteadmin/tree.json` に登録されたサーブレットを呼び出します。
   * このオブジェクトのルートは、「`apps/extjstraining`」です。
* `window` オブジェクト（` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`）を定義します。
   * 事前定義済みのパネルに基づいています。
   * 選択されたパスの値を設定し、パネルを非表示にする「**OK**」ボタンを組み込みます。
* ウィンドウは、「**パス**」フィールドの下に固定されます。
* 選択されたパスは、`show` イベントが発生したときに、参照フィールドからウィンドウに渡されます。
* それ自体を「`ejstbrowse`」xtype として登録します。
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

**カスタム Treebrowse** ウィジェットベースのダイアログを使用するには：

1. **カスタムウィジェット**&#x200B;コンポーネントのダイアログを&#x200B;**カスタム Treebrowse** ダイアログに置き換えます。
[例 2：Single Panel ダイアログ](#example-single-panel-dialog)で説明されている手順に従います。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 例 3：リッチテキストエディター（RTE）プラグイン {#example-rich-text-editor-rte-plug-in}

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは、リッチテキストエディターベースのダイアログで、カスタムテキストを角括弧内に挿入するカスタムボタンが備わっています。カスタムテキストをサーバー側ロジックで解析し、例えば、特定のパスで定義されたテキストを追加することができます（この例では、サーバー側ロジックは実装されていません）。

**RTE プラグイン**&#x200B;ベースのダイアログ：

* 次の場所にある rteplugin ノードによって定義されます。
  `/apps/extjstraining/components/customwidgets/rteplugin`
* 次を要求することにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins` ノードには、プラグインにちなんで命名された子ノード `inserttext`（ノードタイプ = `nt:unstructured`）があります。このノードには、RTE で使用可能なプラグイン機能を定義する `features` という名前のプロパティがあります。

RTE プラグイン：

* `Ejst.InsertTextPlugin` という名前の JavaScript オブジェクトです
* 次の場所にある `InsertTextPlugin.js` JavaScript ファイルに定義されています。
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` オブジェクトを拡張します。
* 次のメソッドは、` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` オブジェクトを定義するもので、プラグインの実装時に上書きされます。
   * `getFeatures()` は、プラグインによって使用可能になるすべての機能の配列を返します。
   * `initializeUI()` は、RTE ツールバーに新しいボタンを追加します。
   * `notifyPluginConfig()` は、ボタンにマウスポインターが置かれたときにタイトルとテキストを表示します。
   * `execute()` は、ボタンのクリック時に呼び出されるもので、含めるテキストを定義するためのウィンドウを表示するというプラグインのアクションを実行します。
* `insertText()` は、対応するダイアログオブジェクト `Ejst.InsertTextPlugin.Dialog`（後述）を使用してテキストを挿入します。
* `executeInsertText()` は、ダイアログの `apply()` メソッドで呼び出されます。これは「**OK**」ボタンをクリックしたときにトリガーされます。
* それ自体を「`inserttext`」プラグインとして登録します。
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog` オブジェクトは、プラグインのボタンがクリックされたときに開くダイアログを定義します。このダイアログは、1 つのパネル、1 つのフォーム、1 つのテキストフィールドおよび 2 つのボタン（「**OK**」と「**キャンセル**」）から構成されます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログを使用するには：

1. **カスタムウィジェット**&#x200B;コンポーネントのダイアログを&#x200B;**リッチテキストエディター（RTE）プラグイン**ベースのダイアログに置き換えます。
[例 2：Single Panel ダイアログ](#example-single-panel-dialog)で説明されている手順に従います。
1. コンポーネントを編集します。
1. 右端のアイコン（4 つの矢印が付いているアイコン）をクリックします。パスを入力して「**OK**」をクリックします。
パスが角括弧（[ ]）内に表示されます。
1. 「**OK**」をクリックして、リッチテキストエディタを閉じます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは次のように表示されます。

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>この例は、クライアント側のロジックの実装方法のみを示しています。プレースホルダー（*[text]*）は、サーバーサイド（コンポーネント JSP など）でも明示的に解析する必要があります。

### Tree Overview {#tree-overview}

すぐに使用できる ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` オブジェクトは、ツリー構造のデータをツリー構造 UI として表示できます。**Using ExtJS Widgets** パッケージに含まれている Tree Overview コンポーネントを見ると、`TreePanel` オブジェクトを使用して特定のパスの下に JCR ツリーを表示する方法がわかります。このウィンドウ自体は、ドッキングすることも、ドッキング解除することもできます。この例の場合、ウィンドウのロジックは、コンポーネント jsp の &lt;script> タグと &lt;/script> タグの間に埋め込まれています。

**Tree Overview** コンポーネントをサンプルページに組み込むには：

1. **4. Tree Overview** コンポーネントをサンプルページに追加します。これは、**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブでおこないます。
1. このコンポーネントには、次のものが表示されます。
   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク：クリックして、リポジトリに保存されている段落のプロパティを表示します。もう一度クリックすると、プロパティが非表示になります。
   * 展開可能なリポジトリのツリー表現を持つフローティングウィンドウ。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Tree Overview コンポーネント：

* 次で定義されます。
  `/apps/extjstraining/components/treeoverview`

* このダイアログでは、ウィンドウのサイズを設定したり、ウィンドウをドッキングまたはドッキング解除したりできます（詳細は以下を参照）。

コンポーネント jsp：

* リポジトリから幅、高さおよびドッキングされたプロパティを取得します。
* Tree Overview のデータ形式に関するテキストを表示します。
* ウィンドウのロジックをコンポーネント jsp の JavaScript タグの間に埋め込みます。
* 次で定義されます。
  `apps/extjstraining/components/treeoverview/content.jsp`

コンポーネント jsp に埋め込まれた JavaScript コード：

* ページからツリーウィンドウの取得を試みることにより、`tree` オブジェクトを定義します。
* ツリーを表示しているウィンドウが存在しない場合は、`treePanel`（[CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)）が作成されます。
   * `treePanel` には、ウィンドウの作成に使用されるデータが含まれています。
   * データは、次で登録されたサーブレットを呼び出すことにより、取得されます。
     `/bin/wcm/siteadmin/tree.json`
* `beforeload` リスナーにより、選択されたノードがロードされます。
* `root` オブジェクトは、パス `apps/extjstraining` をツリーのルートとして設定します。
* `tree`（` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`）は、事前定義済みの `treePanel` に基づいて設定され、次のように表示されます。
  `tree.show();`
* ウィンドウが存在する場合、ウィンドウは、リポジトリから取得した幅、高さ、ドッキングの各プロパティに基づいて表示されます。

コンポーネントダイアログ：

* ツリー概要ウィンドウのサイズ（幅と高さ）を設定するための 2 つのフィールドとウィンドウをドッキング、ドッキング解除するための 1 つのフィールドを持つ 1つのタブを表示
* ノードによって定義されます（node type = `cq:Dialog`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* パネルには、サイズフィールドウィジェット（node type = `cq:Widget`、xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`）と、２ つのオプション（true または false）がある選択ウィジェット（node type = `cq:Widget`、xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`、type = `radio`）があります。
* 次の場所にあるダイアログノードによって定義されます。
  `/apps/extjstraining/components/treeoverview/dialog`
* 次のことを要求することにより、JSON 形式でレンダリングされます。
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 次のように表示されます。

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### グリッドの概要 {#grid-overview}

グリッドパネルは、データを行と列の表形式で表します。これは、次の内容で構成されます。

* ストア：データレコード（行）を保持しているモデル。
* 列モデル：列の構成。
* ビュー：ユーザーインターフェイスが含まれます。
* 選択モデル：選択の動作。

**Using ExtJS Widgets** パッケージに含まれている Grid Overview コンポーネントを見ると、データを表形式で表示する方法がわかります。

* 例 1 では、静的データを使用しています。
* 例 2 では、リポジトリから取得したデータを使用しています。

Grid Overview コンポーネントをサンプルページに組み込むには：

1. **5 を追加します。Grid Overview** コンポーネントを、**サイドキック**&#x200B;の **Using ExtJS Widgets** タブからサンプルページに追加します。
1. このコンポーネントには、次のものが表示されます。
   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク：クリックして、リポジトリに保存されている段落のプロパティを表示します。もう一度クリックすると、プロパティが非表示になります。
   * 表形式のデータを含むフローティングウィンドウ。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 例 1：デフォルトのグリッド {#example-default-grid}

標準バージョンでは、**Grid Overview** コンポーネントは、静的データが含まれるウィンドウを表形式で表示します。この例では、ロジックは次の 2 つの方法でコンポーネント jsp に埋め込まれます。

* 一般的なロジックは、&lt;script>&lt;/script> タグの間に定義されます。
* 特定のロジックは、別の .js ファイルで使用でき、jsp 内でリンクされます。この設定により、必要な &lt;script> タグをコメントすることで、2 つのロジック（static/dynamic）を簡単に切り替えることができます。

Grid Overview コンポーネント：

* 次で定義されます。
  `/apps/extjstraining/components/gridoverview`
* このダイアログでは、ウィンドウのサイズを設定したり、ウィンドウをドッキングまたはドッキング解除したりできます。

コンポーネント jsp：

* リポジトリから幅、高さおよびドッキングされたプロパティを取得します。
* グリッド概要のデータ形式の紹介としてテキストを表示します。
* GridPanel オブジェクトを定義する JavaScript コードを参照します。
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` では、一部の静的データを GridPanel オブジェクトのベースとして定義します。
* GridPanel オブジェクトを使用して Window オブジェクトを定義する JavaScript タグの間に JavaScript コードを埋め込みます。
* 次で定義されます。
  `apps/extjstraining/components/gridoverview/content.jsp`

コンポーネント jsp に埋め込まれた JavaScript コード：

* ページからウィンドウコンポーネントの取得を試みることにより、`grid` オブジェクトを定義します。
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* `grid` が存在しない場合、[CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) オブジェクト（`gridPanel`）は、`getGridPanel()` メソッド（以下を参照）を呼び出すことにより定義されます。このメソッドは、`defaultgrid.js` で定義されます。
* `grid` は、事前定義済みの GridPanel に基づく ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` オブジェクトであり、次のように表示されます：`grid.show();`
* `grid` が存在する場合、リポジトリから取得した幅、高さ、ドッキングされたプロパティに基づいて表示されます。

コンポーネント jsp で参照される JavaScript ファイル（`defaultgrid.js`）には、`getGridPanel()` メソッドが定義されています。このメソッドは、JSP に埋め込まれたスクリプトによって呼び出され、静的データに基づいて ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` オブジェクトを返します。ロジックを次に示します。

* `myData` は、静的データの配列で、5 列 x 4 行の表として書式設定されています。
* `store` は、`myData` を使用する `CQ.Ext.data.Store` オブジェクトです。
* `store` は、メモリにロードされます。
  `store.load();`
* `gridPanel` は、`store` を使用する ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` オブジェクトです。
   * 列幅は常に再調整されます。
     `forceFit: true`
   * 選択できる行は一度に 1 つのみです。
     `singleSelect:true`

#### 例 2：参照検索グリッド {#example-reference-search-grid}

パッケージをインストールすると、**Grid Overview** コンポーネントの `content.jsp` により、静的データに基づくグリッドが表示されます。次の特徴を持つグリッドを表示するようにコンポーネントを変更できます。

* 3 列ある。
* サーブレットを呼び出すことにより、リポジトリから取得したデータを基礎にする。
* 最後の列のセルを編集できます。この値は、先頭の列に表示されたパスで定義されたノードの下にある `test` プロパティに保持されます。

前の節で説明したように、ウインドウオブジェクトは、`/apps/extjstraining/components/gridoverview/defaultgrid.js` の `defaultgrid.js` ファイルで定義された `getGridPanel()` メソッドを呼び出して、その ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` オブジェクトを取得します。Grid Overview コンポーネントでは、`getGridPanel()` メソッドを別の方法で実装することができます。これは、`/apps/extjstraining/components/gridoverview/referencesearch.js` にある `referencesearch.js` ファイルで定義されます。コンポーネント jsp で参照される .js ファイルを切り替えることにより、グリッドは、リポジトリから取得したデータに基づいています。

コンポーネント jsp で参照される .js ファイルを切り替えるには、次の手順を行います。

1. **CRXDE Lite** で、コンポーネントの `content.jsp` ファイル内にある `defaultgrid.js` ファイルを含む行を、次のようにコメント化します。
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. `referencesearch.js` ファイルを含む行のコメント化を、次のように解除します。
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 変更内容を保存します。
1. サンプルページを更新します。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

コンポーネント jsp で参照されている JavaScript コード（`referencesearch.js`）は、コンポーネント jsp から呼び出される `getGridPanel()` メソッドを定義しており、リポジトリから動的に取得されるデータに基づいて ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` オブジェクトを返します。`referencesearch.js` のロジックでは、一部の動的データが GridPanel の基礎として定義されています。

* `reader` は、JSON 形式のサーブレット応答を読み取る 3 列用の ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` オブジェクトです。
* `cm` は、3 列用の ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` オブジェクトです。
「テスト」列のセルは、エディターで定義されているので編集することが可能です。
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 列は並べ替え可能です。
  `cm.defaultSortable = true;`
* `store` は ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` オブジェクトで、次のような特徴があります。
   * クエリをフィルター処理するためのパラメーターをいくつか指定し、「`/bin/querybuilder.json`」に登録されているサーブレットを呼び出すことで、データを取得します
   * 前に定義した `reader` に基づきます
   * 表は、「**jcr:path**」列に従って、昇順で並べ替えられます。
* `gridPanel` は編集可能な ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` オブジェクトで、次のような特徴があります。
   * 事前定義済みの `store` と列モデル `cm` に基づいています。
   * 選択できる行は一度に 1 つのみです。
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit` リスナーは、「**テスト**」列のセルが編集されたことを確認します。
      * 「**jcr:path**」列で定義されたパスにあるノードのプロパティ「`test`」は、セルの値とともにリポジトリに設定されます。
      * POST が成功した場合は、値が `store` オブジェクトに追加されます。POST が失敗した場合は、値が拒否されます。
