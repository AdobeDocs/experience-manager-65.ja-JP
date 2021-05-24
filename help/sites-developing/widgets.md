---
title: ウィジェットの使用および拡張（クラシック UI）
seo-title: ウィジェットの使用および拡張（クラシック UI）
description: AEM の Web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術が使用されています。これらの技術により、作成者は、Web ページ上でコンテンツの WYSIWYG 編集や書式設定をおこなうことができます
seo-description: AEM の Web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術が使用されています。これらの技術により、作成者は、Web ページ上でコンテンツの WYSIWYG 編集や書式設定をおこなうことができます
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4965'
ht-degree: 63%

---

# ウィジェットの使用および拡張（クラシック UI）{#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>このページでは、AEM 6.4で廃止されたクラシックUIでのウィジェットの使用方法について説明します。
>
>アドビでは、[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) および [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components) をベースとした最新の[タッチ操作対応 UI](/help/sites-developing/touch-ui-concepts.md) の使用を推奨しています。

Adobe Experience Manager の Web ベースインターフェイスでは、AJAX やその他の最新のブラウザー技術が使用されています。これらの技術により、作成者は、Web ページ上でコンテンツの WYSIWYG 編集や書式設定を行うことができます。

Adobe Experience Manager（AEM）では、[ExtJS](https://www.sencha.com/) ウィジェットライブラリが使用されています。このライブラリのユーザーインターフェイス要素は、主要なすべてのブラウザーで動作するだけではなく、デスクトップクラスの UI の操作性も実現でき、非常に洗練されたものとなっています。

これらのウィジェットは AEM に組み込まれており、AEM 自体でも使用されていますが、AEM で作成したすべての Web サイトでも使用できます。

AEM で使用可能なすべてのウィジェットについて詳しくは、[ウィジェット API ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)または[既存の xtype のリスト](/help/sites-developing/xtypes.md)を参照してください。また、ExtJS フレームワークを所有している [Sencha](https://www.sencha.com/products/extjs/examples/) のサイトには、ExtJS フレームワークの使用方法を示す例が多数掲載されています。

このページをご覧になると、ウィジェットを使用したり、拡張したりする方法についてのヒントが得られます。このページでは、最初に、[クライアント側コードをページに組み込む](#including-the-client-sided-code-in-a-page)方法が説明されています。次に、基本的な使用と拡張の方法を説明するために作成されたサンプルコンポーネントが示されています。これらのコンポーネントは、**パッケージ共有**&#x200B;の **Using ExtJS Widgets**&#x200B;パッケージで提供されています。

このパッケージには、次の例が含まれています。

* すぐに使用できるウィジェットで作成した[基本ダイアログ](#basic-dialogs)。
* すぐに使用できるウィジェットとカスタマイズ済みの Javascript ロジックで作成した[動的ダイアログ](#dynamic-dialogs)。
* [カスタムウィジェット](#custom-widgets)に基づくダイアログ。
* 特定のパスの下に JCR ツリーを表示する[ツリーパネル](#tree-overview)。
* 表形式でデータを表示する[グリッドパネル](#grid-overview)。

>[!NOTE]
>
>Adobe Experience Manager のクラシック UI は、[ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/) をベースに構築されています。

## クライアント側コードのページへの組み込み {#including-the-client-sided-code-in-a-page}

クライアント側のJavaScriptとスタイルシートコードは、クライアントライブラリに配置する必要があります。

クライアントライブラリを作成するには：

1. `/apps/<project>`の下に、次のプロパティを持つノードを作成します。

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. `clientlib`の下に、`css`フォルダーと`js`フォルダー(nt:folder)を作成します。

1. `clientlib`の下に、`css.txt`ファイルと`js.txt`ファイル(nt:files)を作成します。 これらの .txt ファイルには、ライブラリに組み込むファイルを記述します。

1. `js.txt`を編集：「 `#base=js` 」で始まり、CQクライアントライブラリサービスによって集計されるファイルのリストが続く必要があります。例：

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. `css.txt`を編集：「 `#base=css` 」で始まり、CQクライアントライブラリサービスによって集計されるファイルのリストが続く必要があります。例：

   ```
   #base=css
    components.css
   ```

1. `js` フォルダーの下に、ライブラリに属する Javascript ファイルを配置します。

1. `css`フォルダーの下に、`.css`ファイルと、CSSファイルで使用されるリソース(例：`my_icon.png`)です。

>[!NOTE]
>
>前述のスタイルシートの処理は、必要に応じておこないます。

ページコンポーネント jsp にクライアントライブラリを組み込むには：

* Javascript コードとスタイルシートの両方を組み込むには：
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
条件 
`<category-nameX>` はクライアント側ライブラリの名前です。

* Javascript コードのみを組み込むには：
   `<ui:includeClientLib js="<category-name>"/>`

詳しくは、[&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) タグの説明を参照してください。

クライアントライブラリは、オーサーモードでのみ使用可能にして、パブリッシュモードでは除外することが必要な場合があります。これをおこなうには、次のように設定します。

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### サンプルの使用  {#getting-started-with-the-samples}

このページのチュートリアルに従うには、**Using ExtJS Widgets**&#x200B;という名前のパッケージをローカルのAEMインスタンスにインストールし、コンポーネントが含まれるサンプルページを作成します。 この作業を行うには、以下の手順を実行します。

1. AEMインスタンスで、パッケージ共有から&#x200B;**Using ExtJS Widgets (v01)**&#x200B;という名前のパッケージをダウンロードし、インストールします。 リポジトリ内の`/apps`の下にプロジェクト`extjstraining`が作成されます。
1. **Geometrixx**ブランチの新しいページにサンプルコンポーネントを含めるので、geometrixxページjspのheadタグに、スクリプト(js)とスタイルシート(css)を含むクライアントライブラリを含めます。
**CRXDE Lite**&#x200B;で、ファイル`/apps/geometrixx/components/page/headlibs.jsp`を開き、次のように`cq.extjstraining`カテゴリを既存の`<ui:includeClientLib>`タグに追加します。
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. `/content/geometrixx/en/products`の下の&#x200B;**Geometrixx**&#x200B;ブランチに新しいページを作成し、**Using ExtJS Widgets**&#x200B;と呼び出します。
1. デザインモードに切り替え、**Using ExtJS Widgets** という名前のグループのすべてのコンポーネントを Geometrixx のデザインに追加します。
1. 編集モードに戻ります。**Using ExtJS Widgets**&#x200B;グループのコンポーネントは、サイドキックで使用できます。

>[!NOTE]
>
>このページの例は、Geometrixx サンプルコンテンツに基づいています。これは現在、AEM には付属しておらず、We.Retail に置き換えられています。Geometrixxをダウンロードしてインストールする方法については、ドキュメント[We.Retail参照実装](/help/sites-developing/we-retail.md#we-retail-geometrixx)を参照してください。

### 基本ダイアログ {#basic-dialogs}

通常、ダイアログは、コンテンツを編集するために使用されますが、情報の表示のみをおこなうこともできます。ダイアログを完全に表示する簡単な方法は、その JSON 形式の表現にアクセスすることです。これをおこなうには、ブラウザーで次のように指定します。

`https://localhost:4502/<path-to-dialog>.-1.json`

サイドキックにある **Using ExtJS Widgets** グループの最初のコンポーネントは、**1.Dialog Basics** という名前で、4 つの基本ダイアログが入っています。これらのダイアログは、すぐに使用できるウィジェットで作成されており、カスタマイズした Javascript ロジックは含まれていません。ダイアログは`/apps/extjstraining/components/dialogbasics`の下に保存されます。 基本ダイアログを次に示します。

*  ダイアログ（`full`full ノード）：3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。
* Single Panel ダイアログ（`singlepanel` ノード）：1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。
* Multi Panel ダイアログ（`multipanel` ノード）：表示内容は Full ダイアログと同じですが、ダイアログの作成の仕方が異なります。
*  ダイアログ（`design`design ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折り畳み可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折り畳み可能なフィールドセットがあります。

次の手順に従って、**1.Dialog Basics** コンポーネントをサンプルページに組み込みます。

1. **1.**&#x200B;サイドキック&#x200B;**の**「Using ExtJS Widgets **」タブからサンプルページにDialog Basics**&#x200B;コンポーネントを追加します。
1. このコンポーネントには、タイトル、テキストおよび&#x200B;**プロパティ**&#x200B;リンクが表示されます。リンクをクリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-60](assets/chlimage_1-60.png)

#### 例 1：Full ダイアログ {#example-full-dialog}

**Full** ダイアログには、3 つのタブを持つウィンドウが表示されます。各タブには、2 つのテキストフィールドがあります。これは、**Dialog Basics** コンポーネントのデフォルトダイアログです。特性は次のとおりです。

* ノードによって定義されます。node type = `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`。
* 3つのタブが表示されます(node type = `cq:Panel`)。
* 各タブには2つのテキストフィールドがあります（ノードタイプ= `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* ノードによって定義されます：
   `/apps/extjstraining/components/dialogbasics/full`
* 次を要求することで、JSON形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

このダイアログは、次のように表示されます。

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### 例 2：Single Panel ダイアログ {#example-single-panel-dialog}

**Single Panel** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのテキストフィールドがあります。特性は次のとおりです。

* 1つのタブを表示します(node type = `cq:Dialog`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* このタブには2つのテキストフィールドがあります（ノードタイプ= `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）
* ノードによって定義されます：
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* **Full ダイアログ**&#x200B;の利点の 1 つは、必要な設定が少ないことです。
* 推奨される用途：情報を表示するだけの、またはフィールドが数個しかない単純なダイアログ。

Single Panel ダイアログを使用するには：

1. **Dialog Basics** コンポーネントのダイアログを **Single Panel** ダイアログに置き換えます。
   1. **CRXDE Lite**&#x200B;で、ノードを削除します。`/apps/extjstraining/components/dialogbasics/dialog`
   1. 「**すべて保存**」をクリックして変更を保存します。
   1. ノードをコピーします。`/apps/extjstraining/components/dialogbasics/singlepanel`
   1. コピーしたノードを次の場所に貼り付けます。`/apps/extjstraining/components/dialogbasics`
   1. ノードを選択します。`/apps/extjstraining/components/dialogbasics/Copy of singlepanel`と名前を`dialog`に変更します。
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### 例 3：Multi Panel ダイアログ {#example-multi-panel-dialog}

**Multi Panel** ダイアログは、**Full** ダイアログと同じ表示内容ですが、ダイアログの作成の仕方が異なります。特性は次のとおりです。

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`）。
* 3つのタブが表示されます(node type = `cq:Panel`)。
* 各タブには2つのテキストフィールドがあります（ノードタイプ= `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`）。
* ノードによって定義されます：
   `/apps/extjstraining/components/dialogbasics/multipanel`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* **Full ダイアログ**&#x200B;の利点の一つは、構造が簡単であることです。
* 推奨される用途：複数のタブを持つダイアログ。

マルチパネルダイアログを使用するには：

1. **Dialog Basics**&#x200B;コンポーネントのダイアログを&#x200B;**Multi Panel**ダイアログに置き換えます。
[例2で説明されている手順に従います。シングルパネルダイアログ](#example-single-panel-dialog)
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### 例 4：Rich ダイアログ {#example-rich-dialog}

**Rich** ダイアログには、2 つのタブを持つウィンドウが表示されます。最初のタブには、テキストフィールド、ドロップダウンメニューおよび折り畳み可能なテキスト領域があります。2 番目のタブには、4 つのテキストフィールドを含むフィールドセットと、2 つのテキストフィールドを含む折り畳み可能なフィールドセットがあります。特性は次のとおりです。

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 2つのタブが表示されます(node type = `cq:Panel`)。
* 最初のタブには、` [textfield](/help/sites-developing/xtypes.md#textfield)`と3つのオプションを持つ` [selection](/help/sites-developing/xtypes.md#selection)`ウィジェットを持つ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`ウィジェットと、` [textarea](/help/sites-developing/xtypes.md#textarea)`ウィジェットを持つ折りたたみ可能な` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`ウィジェットがあります。
* 2番目のタブには、4つの` [textfield](/help/sites-developing/xtypes.md#textfield)`ウィジェットを持つ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`ウィジェットと、2つの` [textfield](/help/sites-developing/xtypes.md#textfield)`ウィジェットを持つ折りたたみ可能な`dialogfieldset`ウィジェットがあります。
* ノードによって定義されます：
   `/apps/extjstraining/components/dialogbasics/rich`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

**Rich** ダイアログを使用するには：

1. **Dialog Basics**&#x200B;コンポーネントのダイアログを&#x200B;**Rich**ダイアログに置き換えます。
[例2で説明されている手順に従います。シングルパネルダイアログ](#example-single-panel-dialog)
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-01-31at50429](assets/screen_shot_2012-01-31at50429pm.png) ![pmscreen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Dynamic Dialogs {#dynamic-dialogs}

サイドキックにある **Using ExtJS Widgets** グループの 2 番目のコンポーネントは、**2.Dynamic Dialogs** という名前で、3 つの動的ダイアログが含まれています。これらのダイアログは、すぐに使用できるウィジェットと、**カスタマイズされた Javascript ロジック**&#x200B;から作成されています。ダイアログは`/apps/extjstraining/components/dynamicdialogs`の下に保存されます。 動的ダイアログは次のとおりです。

* Switch Tabs ダイアログ（`switchtabs` ノード）：2 つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。
*  ダイアログ（`arbitrary`arbitrary ノード）：1 つのタブを持つウィンドウが表示されます。このタブには、2 つのフィールドがあります。一つは、アセットをドロップまたはアップロードするためのフィールド、もう一つは、コンポーネントを含むページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。
* [フィールドの切り替え]ダイアログ（ `togglefield`ノード）:1つのタブを持つウィンドウが表示されます。 このタブには、1 つのチェックボックスがあります。このチェックボックスを選択すると、2 つのテキストフィールドを含むフィールドセットが表示されます。

**2. Dynamic Dialogs** コンポーネントをサンプルページに組み込むには：

1. **2.  Dynamic Dialogs** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブから）。
1. このコンポーネントには、タイトル、テキストおよび&#x200B;**プロパティ**&#x200B;リンクが表示されます。リンクをクリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。

このコンポーネントは、次のように表示されます。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 例 1：Switch Tabs ダイアログ {#example-switch-tabs-dialog}

**Switch Tabs** ダイアログには、2 つのタブを持つウィンドウが表示されます。最初のタブでは、ラジオボタンにより、3 つのオプションのいずれかを選択できます。オプションを選択すると、選択したオプションに関連付けられているタブが表示されます。2 番目のタブには、2 つのテキストフィールドがあります。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 次の2つのタブが表示されます(node type = `cq:Panel`)。「1」タブの場合、「2」タブの場合は、「1」タブでの選択内容（「3」オプション）に応じて異なります。
* 3つのオプションのタブ(node type = `cq:Panel`)があり、各タブには2つのテキストフィールドがあります(node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)。 「オプション」タブは、同時に 1 つしか表示されません。
* 次の場所にある`switchtabs`ノードによって定義されます。
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* ダイアログノードには、ダイアログが表示される前に、すべてのオプションのタブを非表示にする「`beforeshow`」リスナーがあります。
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` 選択パネルと3つのオプションパネルを含むタブパネルを取得します。
* `Ejst.x2`オブジェクトは、次の場所にある`exercises.js`ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.manageTabs()`メソッドでは、`index`の値が —1なので、すべてのオプションのタブが非表示になります(1 ～ 3)。
* 「選択範囲」タブには、2 つのリスナーがあります。一つは、ダイアログのロード（「`loadcontent`」イベント）時に選択済みのタブを表示するリスナー、もう一つは、選択内容の変更（「`selectionchanged`」イベント）時に選択済みのタブを表示するリスナーです。
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* `Ejst.x2.showTab()`メソッドで、次の操作を実行します。
   `field.findParentByType('tabpanel')` すべてのタブを含むタブパネルを取得しま `field` す（選択ウィジェットを表す）。
   `field.getValue()` 選択の値を取得します。例：tab2
   `Ejst.x2.manageTabs()` 選択したタブが表示されます。
* 各「オプション」タブには、「`render`」イベントでタブを非表示にするリスナーがあります。
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* `Ejst.x2.hideTab()`メソッドで、次の操作を実行します。
   `tabPanel` は、すべてのタブを含むタブパネルです
   `index` はオプションのタブのインデックスです
   `tabPanel.hideTabStripItem(index)` タブを非表示

次のように表示されます。

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### 例 2：Arbitrary ダイアログ {#example-arbitrary-dialog}

ほとんどの場合、ダイアログには、基になるコンポーネントからのコンテンツが表示されます。ここで説明する **Arbitrary** ダイアログは、別のコンポーネントからコンテンツを取り込みます。

**Arbitrary** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、2 つのフィールドがあります。一つは、アセットをドロップまたはアップロードするためのフィールド、もう一つは、コンポーネントを含むページに関する情報とアセットに関する情報（アセットが参照されている場合）を表示するフィールドです。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 1つのパネル(node type = `cq:Panel`)を含む1つのtabpanelウィジェット(node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)を表示します。
* このパネルには、smartfileウィジェット(node type = `cq:Widget`、xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`)とownerdrawウィジェット(node type = `cq:Widget`、xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)があります。
* 次の場所にある`arbitrary`ノードによって定義されます。
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* ownerdrawウィジェットには、コンポーネントを含むページに関する情報と、コンテンツの読み込み時にsmartfileウィジェットが参照するアセットに関する情報を表示する「`loadcontent`」リスナーがあります。
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` ownerdrawオブジェクトを使用して設定します。
   `path` コンポーネントのコンテンツパスを使用して設定します(例：/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* `Ejst.x2`オブジェクトは、次の場所にある`exercises.js`ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.showInfo()`メソッドで、次の操作を実行します。
   `pagePath` は、コンポーネントを含むページのパスです。
   `pageInfo` は、ページプロパティをjson形式で表します。
   `reference` は参照先のアセットのパスです。
   `metadata` アセットのメタデータをjson形式で表します。
   `ownerdraw.getEl().update(html);` 作成したhtmlがダイアログに表示されます。

**Arbitrary** ダイアログを使用するには：

1. **ダイナミックダイアログ**&#x200B;コンポーネントのダイアログを&#x200B;**任意の**ダイアログに置き換えます。
[例2で説明されている手順に従います。シングルパネルダイアログ](#example-single-panel-dialog)
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### 例 3：Toggle Fields ダイアログ {#example-toggle-fields-dialog}

**Toggle Fields** ダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、1 つのチェックボックスがあります。このチェックボックスを選択すると、2 つのテキストフィールドを含むフィールドセットが表示されます。

このダイアログの主な特徴を次に示します。

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 1つのパネル(node type = `cq:Panel`)を持つ1つのtabpanelウィジェット(node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`)を表示します。
* このパネルには、2つのtextfieldウィジェット(node type = `cq:Widget`、xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)でデフォルトで非表示になる、selection/checkboxウィジェット(node type = `cq:Widget`、xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`、type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`)と折りたたみ可能なdialogfieldsetウィジェット(node type = `cq:Widget`、xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`)があります。
* 次の場所にある`togglefields`ノードによって定義されます。
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

ロジックは、次のようにイベントリスナーと Javascript コードによって実装されています。

* 「選択」タブには、2つのリスナーがあります。コンテンツの読み込み時にdialogfieldsetを表示するもの（「`loadcontent`」イベント）と、選択が変更されたときにdialogfieldsetを表示するもの（「`selectionchanged`」イベント）を次に示します。
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* `Ejst.x2`オブジェクトは、次の場所にある`exercises.js`ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/exercises.js`
* `Ejst.x2.toggleFieldSet()`メソッドで、次の操作を実行します。
   `box` は選択オブジェクトです。
   `panel` は、選択およびdialogfieldsetウィジェットを含むパネルです。
   `fieldSet` dialogfieldsetオブジェクト
   `show` には、&#39; &#39;に基づく選択範囲の値（trueまたはfalse）を指定しま `show`す。dialogfieldsetは表示されるか、表示されません

**フィールドの切り替え**&#x200B;ダイアログを使用するには：

1. **ダイナミックダイアログ**&#x200B;コンポーネントのダイアログを、**フィールドの切り替え**ダイアログに置き換えます。
[例2で説明されている手順に従います。シングルパネルダイアログ](#example-single-panel-dialog)
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### カスタムウィジェット {#custom-widgets}

AEM に付属しているすぐに使用できるウィジェットは、ほとんどのケースに対応できます。ただし、プロジェクト固有の要件をカバーするためにカスタムウィジェットを作成する必要が生じる場合があります。 カスタムウィジェットは、既存のウィジェットを拡張して作成できます。こうしたカスタマイズをおこなう際の手助けとなるように、**Using ExtJS Widgets** パッケージには、3 つの異なるカスタムウィジェットを使用する 3 つのダイアログが含まれています。

* Multi Field ダイアログ（`multifield` ノード）。1 つのタブを持つウィンドウが表示されます。このタブには、カスタマイズされた multifield ウィジェットがあり、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドが含まれています。このタブは、すぐに使用できる `multifield` ウィジェット（テキストフィールドのみを持つ）に基づいているので、`multifield` ウィジェットの機能をすべて使用できます。
* Tree Browse ダイアログ（`treebrowse` ノード）。このダイアログに表示されるウィンドウには、パス参照ウィジェットを含む 1 つのタブがあります。このウィジェットで矢印をクリックすると、ウィンドウが開き、階層を参照しながら項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。
* リッチテキストエディタープラグインベースのダイアログ（`rteplugin` ノード）。リッチテキストエディターにカスタムボタンを追加したもので、メインテキストにカスタムテキストを挿入できます。`richtext` ウィジェット（RTE）と、RTE プラグインメカニズムを通じて追加されたカスタム機能から構成されています。

カスタムウィジェットとプラグインは、**3.Custom Widgets**（**Using ExtJS Widgets** パッケージに属する）という名前のコンポーネントに含まれています。このコンポーネントをサンプルページに組み込むには：

1. **3.  Custom Widgets** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブから）。
1. このコンポーネントには、タイトルとテキストが表示されます。また、**プロパティ**&#x200B;リンクをクリックすると、リポジトリに保存されている段落のプロパティも表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。このコンポーネントは、次のように表示されます。

![chlimage_1-62](assets/chlimage_1-62.png)

#### 例 1：Custom Multifield ウィジェット {#example-custom-multifield-widget}

**Custom Multifield** ウィジェットベースのダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、カスタマイズされた multifield ウィジェットがあります。標準の multifield ウィジェットには 1 つのフィールドがありますが、このウィジェットには、2 つのオプションを選択できるドロップダウンメニューとテキストフィールドという 2 つのフィールドがあります。

**Custom Multifield** ウィジェットベースのダイアログ：

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 1つのパネル(node type = `cq:Widget`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)を含む1つのtabpanelウィジェット(node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)を表示します。
* このパネルには、`multifield`ウィジェット(node type = `cq:Widget`、xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`)があります。
* `multifield`ウィジェットには、カスタムxtype &#39; `ejstcustom`&#39;に基づくfieldconfig (node type = `nt:unstructured`、xtype = `ejstcustom`、optionsProvider = `Ejst.x3.provideOptions`)があります。
   * 「 `fieldconfig` 」は` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)`オブジェクトの設定オプションです。
   * 「 `optionsProvider` 」は`ejstcustom`ウィジェットの設定です。 これは、`exercises.js`で次の場所に定義されている`Ejst.x3.provideOptions`メソッドを使用して設定されます。
      `/apps/extjstraining/clientlib/js/exercises.js`
とは、2つのオプションを返します。
* 次の場所にある`multifield`ノードによって定義されます。
   `/apps/extjstraining/components/customwidgets/multifield`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Custom Multifield ウィジェット（xtype = `ejstcustom`）：

* `Ejst.CustomWidget` という名前の Javascript オブジェクトです。
* 次の場所にある `CustomWidget.js` Javascript ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)`ウィジェットを拡張します。
* 次の3つのフィールドがあります。`hiddenField`（テキストフィールド）、`allowField`(ComboBox)、`otherField`（テキストフィールド）
* `CQ.Ext.Component#initComponent`を上書きして3つのフィールドを追加します。
   * `allowField` は [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) タイプ「select」のSelectionobjectです。optionsProviderは、ダイアログで定義されたCustomWidgetのoptionsProvider設定でインスタンス化されるSelectionオブジェクトの設定です
   * `otherField` は、[CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) オブジェクトです。
* [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)のメソッド`setValue`、`getValue`および`getRawValue`を上書きして、次の形式のCustomWidgetの値を設定および取得します。
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`
* 自分自身を&#39; `ejstcustom`&#39; xtypeとして登録します。
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

**Custom Multifield** ウィジェットベースのダイアログは、次のように表示されます。

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### 例 2：カスタム Treebrowse ウィジェット {#example-custom-treebrowse-widget}

カスタム **Treebrowse** ウィジェットベースのダイアログには、1 つのタブを持つウィンドウが表示されます。このタブには、カスタムパス参照ウィジェットが含まれています。このウィジェットで矢印をクリックすると、ウィンドウが開き、階層を参照しながら項目を選択できます。項目を選択すると、そのパスがパスフィールドに追加され、ダイアログを閉じても保持され続けます。

カスタム treebrowse ダイアログ：

* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`）。
* 1つのパネル(node type = `cq:Widget`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)を含む1つのtabpanelウィジェット(node type = `cq:Widget`、xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`)を表示します。
* このパネルにはカスタムウィジェット(node type = `cq:Widget`、xtype = `ejstbrowse`)があります。
* 次の場所にある`treebrowse`ノードによって定義されます。
   `/apps/extjstraining/components/customwidgets/treebrowse`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

カスタム treebrowse ウィジェット（xtype = `ejstbrowse`）：

* `Ejst.CustomWidget` という名前の Javascript オブジェクトです。
* 次の場所にある `CustomBrowseField.js` Javascript ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`を拡張します。
* `browseWindow` という名前の参照ウィンドウを定義します。
* ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick`を上書きして、矢印をクリックしたときに参照ウィンドウを表示します。
* [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) オブジェクトを定義します。
   * `/bin/wcm/siteadmin/tree.json`に登録されたサーブレットを呼び出すことで、データを取得します。
   * ルートは「`apps/extjstraining`」です。
* `window`オブジェクト(` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)を定義します。
   * 事前定義済みのパネルに基づいています。
   * 選択されたパスの値を設定し、パネルを非表示にする「**OK**」ボタンを組み込みます。
* ウィンドウは、「**パス**」フィールドの下に固定されます。
* 選択されたパスは、`show` イベントが発生したときに、参照フィールドからウィンドウに渡されます。
* 自分自身を&#39; `ejstbrowse`&#39; xtypeとして登録します。
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

**Custom Treebrowse**&#x200B;ウィジェットベースのダイアログを使用するには：

1. **カスタムウィジェット**&#x200B;コンポーネントのダイアログを、**カスタムツリー参照**ダイアログに置き換えます。
[例2で説明されている手順に従います。シングルパネルダイアログ](#example-single-panel-dialog)
1. コンポーネントを編集します。次のようなダイアログが表示されます。

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### 例 3：リッチテキストエディター（RTE）プラグイン {#example-rich-text-editor-rte-plug-in}

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは、大括弧内にカスタムテキストを挿入するためのカスタムボタンがあるリッチテキストエディターベースのダイアログです。カスタムテキストをサーバー側ロジックで解析し、例えば、特定のパスで定義されたテキストを追加することができます（この例では、サーバー側ロジックは実装されていません）。

**RTE プラグイン**&#x200B;ベースのダイアログ：

* 次の場所にあるrtepluginノードによって定義されます。
   `/apps/extjstraining/components/customwidgets/rteplugin`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* `rtePlugins`ノードには、プラグインの名前にちなんだ子ノード`inserttext`（ノードタイプ= `nt:unstructured`）があります。 このノードには、RTE で使用可能なプラグイン機能を定義する `features` という名前のプロパティがあります。

RTE プラグイン：

* `Ejst.InsertTextPlugin` という名前の Javascript オブジェクトです。
* 次の場所にある `InsertTextPlugin.js` Javascript ファイルで定義されます。
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`オブジェクトを拡張します。
* 次のメソッドは、` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` オブジェクトを定義するもので、プラグインの実装時に上書きされます。
   * `getFeatures()` は、プラグインが使用可能にするすべての機能の配列を返します。
   * `initializeUI()` RTEツールバーに新しいボタンを追加します。
   * `notifyPluginConfig()` ボタンにカーソルを合わせると、タイトルとテキストが表示されます。
   * `execute()` が呼び出され、プラグインのアクションが実行されます。含めるテキストを定義するウィンドウが表示されます。
* `insertText()` 対応するダイアログオブジェクトを使用してテキ `Ejst.InsertTextPlugin.Dialog` ストを挿入します（後で参照）。
* `executeInsertText()` は、ダイアログの `apply()` メソッドによって呼び出され、「 **** OK」ボタンがクリックされたときにトリガーされます。
* 自分自身を「`inserttext`」プラグインとして登録します。
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* `Ejst.InsertTextPlugin.Dialog` オブジェクトは、プラグインのボタンがクリックされたときに開くダイアログを定義します。このダイアログは、1 つのパネル、1 つのフォーム、1 つのテキストフィールドおよび 2 つのボタン（「**OK**」と「**キャンセル**」）から構成されます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログを使用するには：

1. **Custom Widgets** コンポーネントのダイアログを&#x200B;**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログに置き換えます。[例 2：Single Panel ダイアログ](#example-single-panel-dialog)で説明されている手順に従います。
1. コンポーネントを編集します。
1. 右側の最後のアイコン（4つの矢印の付いたアイコン）をクリックします。 パスを入力し、「**OK**」をクリックします。
パスは角括弧([)で囲んで表示されます。 ])をクリックします。
1. 「**OK**」をクリックしてリッチテキストエディターを閉じます。

**リッチテキストエディター（RTE）プラグイン**&#x200B;ベースのダイアログは、次のように表示されます。

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>この例は、ロジックのクライアント側の部分の実装方法を示しています。プレースホルダー(*[text]*)は、サーバー側で明示的に解析する必要があります（例：コンポーネントJSP内）。

### Tree Overview {#tree-overview}

すぐに使用できる ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` オブジェクトは、ツリー構造のデータをツリー構造 UI として表示できます。**Using ExtJS Widgets** パッケージに含まれている Tree Overview コンポーネントを見ると、`TreePanel` オブジェクトを使用して特定のパスの下に JCR ツリーを表示する方法がわかります。このウィンドウ自体は、ドッキングすることも、ドッキング解除することもできます。この例の場合、ウィンドウのロジックは、コンポーネント jsp の &lt;script> タグと &lt;/script> タグの間に埋め込まれています。

**Tree Overview** コンポーネントをサンプルページに組み込むには：

1. **4.  Tree Overview** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブで）。
1. このコンポーネントには、次のものが表示されます。
   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク。クリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。
   * リポジトリをツリーで表現した浮動ウィンドウ。このツリーは展開可能です。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Tree Overview コンポーネント：

* 次で定義されます。
   `/apps/extjstraining/components/treeoverview`

* このコンポーネントのダイアログでは、ウィンドウサイズの設定やウィンドウのドッキング、ドッキング解除が可能です（以下を参照）。

コンポーネント jsp：

* リポジトリから幅、高さ、ドッキングの各プロパティを取得します。
* ツリー概要のデータ形式に関するテキストを表示します。
* ウィンドウのロジックをコンポーネント jsp の Javascript タグの間に埋め込みます。
* 次で定義されます。
   `apps/extjstraining/components/treeoverview/content.jsp`

コンポーネント jsp に埋め込まれた Javascript コード：

* ページからツリーウィンドウの取得を試みることにより、`tree` オブジェクトを定義します。
* ツリーを表示するウィンドウが存在しない場合は、`treePanel`([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel))が作成されます。
   * `treePanel` には、ウィンドウの作成に使用されるデータが含まれています。
   * データは、次で登録されたサーブレットを呼び出すことにより、取得されます。
      `/bin/wcm/siteadmin/tree.json`
* `beforeload`リスナーは、クリックされたノードが読み込まれたことを確認します。
* `root`オブジェクトは、パス`apps/extjstraining`をツリーのルートとして設定します。
* `tree` (  ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`)は事前定義に基づいて設定さ `treePanel`れ、次のように表示されます。
   `tree.show();`
* ウィンドウが既に存在する場合、ウィンドウは、リポジトリから取得した幅、高さ、ドッキングの各プロパティに基づいて表示されます。

コンポーネントダイアログ：

* ツリー概要ウィンドウのサイズ（幅と高さ）を設定するための 2 つのフィールドとウィンドウをドッキング、ドッキング解除するための 1 つのフィールドを持つ 1 つのタブを表示します。
* ノードによって定義されます（ノードタイプ= `cq:Dialog`、xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`）。
* このパネルには、sizefieldウィジェット(node type = `cq:Widget`、xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`)と、2つのオプション(true/false)を持つ選択ウィジェット(node type = `cq:Widget`、xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`、type = `radio`)があります。
* 次の場所にあるdialogノードによって定義されます。
   `/apps/extjstraining/components/treeoverview/dialog`
* 次を要求することにより、JSON 形式でレンダリングされます。
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* 次のように表示されます。

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Grid Overview {#grid-overview}

グリッドパネルには、データが行と列の表形式で表示されます。このパネルは、次の内容から構成されています。

* ストア：データレコード（行）を保持しているモデル。
* 列モデル：列の構成。
* ビュー：ユーザーインターフェイスが含まれます。
* 選択モデル：選択の動作。

**Using ExtJS Widgets**&#x200B;パッケージに含まれるGrid Overviewコンポーネントでは、データを表形式で表示する方法を示します。

* 例 1 では、静的データを使用しています。
* 例2では、リポジトリから取得したデータを使用します。

Grid Overviewコンポーネントをサンプルページに含めるには：

1. **5.  Grid Overview** コンポーネントをサンプルページに追加します（**サイドキック**&#x200B;にある「**Using ExtJS Widgets**」タブで）。
1. このコンポーネントには、次のものが表示されます。
   * タイトルとテキスト
   * **プロパティ**&#x200B;リンク。クリックすると、リポジトリに保存されている段落のプロパティが表示されます。リンクをもう一度クリックすると、プロパティが非表示になります。
   * 表形式のデータを含む浮動ウィンドウ。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### 例 1：デフォルトグリッド {#example-default-grid}

すぐに使用できるバージョンの場合、**Grid Overview** コンポーネントには、静的データが表形式で含まれているウィンドウが表示されます。この例の場合、ロジックは、コンポーネント jsp に 次の 2 つの方法で埋め込まれます。

* 一般的なロジックは、&lt;script> タグと &lt;/script> タグの間に定義されます。
* 特定のロジックは、個別の .js ファイルで用意され、jsp にリンクされます。このような設定であるので、&lt;script> タグを必要に応じてコメント化すれば、2 つのロジック（静的／動的）を簡単に切り替えることができます。

Grid Overview コンポーネント：

* 次で定義されます。
   `/apps/extjstraining/components/gridoverview`
* このコンポーネントのダイアログでは、ウィンドウサイズの設定やウィンドウのドッキング、ドッキング解除が可能です。

コンポーネント jsp：

* リポジトリから幅、高さ、ドッキングの各プロパティを取得します。
* グリッド概要のデータ形式の紹介としてテキストを表示します。
* GridPanel オブジェクトを定義する Javascript コードを参照します。
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` では、一部の静的データをGridPanelオブジェクトの基礎として定義します。
* GridPanel オブジェクトを使用する Window オブジェクトを Javascript コードで定義して、Javascript タグの間に埋め込みます。
* 次で定義されます。
   `apps/extjstraining/components/gridoverview/content.jsp`

コンポーネント jsp に埋め込まれた Javascript コード：

* ページからウィンドウコンポーネントの取得を試みることにより、`grid` オブジェクトを定義します。
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* `grid`が存在しない場合、[CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)オブジェクト(`gridPanel`)は、`getGridPanel()`メソッドを呼び出すことで定義されます（以下を参照）。 このメソッドは、`defaultgrid.js` で定義されます。
* `grid` は、事前 ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` 定義済みのGridPanelに基づくオブジェクトで、次のように表示されます。  `grid.show();`
* `grid` が既に存在する場合、grid は、リポジトリから取得した幅、高さ、ドッキングの各プロパティに基づいて表示されます。

コンポーネントjspで参照されるJavaScriptファイル( `defaultgrid.js` )では、JSPに埋め込まれたスクリプトによって呼び出され、静的データに基づいて` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`オブジェクトを返す`getGridPanel()`メソッドを定義します。 ロジックを次に示します。

* `myData` は、静的データの配列で、5 列 x 4 行の表として書式設定されています。
* `store` は、を使用す `CQ.Ext.data.Store` るオブジェクトで `myData`す。
* `store` はメモリに読み込まれます。
   `store.load();`
* `gridPanel` は、次を使用す ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` るオブジェクトで `store`す。
   * 列幅は常に再調整されます。
      `forceFit: true`
   * 選択できる行は一度に 1 つのみです。
      `singleSelect:true`

#### 例 2：参照検索グリッド {#example-reference-search-grid}

パッケージをインストールすると、**Grid Overview**&#x200B;コンポーネントの`content.jsp`に、静的データに基づくグリッドが表示されます。 次の特徴を持つグリッドを表示するようにコンポーネントを変更することが可能です。

* 3 つの列を持つ。
* サーブレットを呼び出すことにより、リポジトリから取得したデータを基礎にする。
* 最後の列のセルを編集できる。この値は、先頭の列に表示されたパスで定義されたノードの下にある `test` プロパティに保持されます。

前の節で説明したように、windowオブジェクトは、`defaultgrid.js`ファイル(`/apps/extjstraining/components/gridoverview/defaultgrid.js`)で定義されている`getGridPanel()`メソッドを呼び出して、` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`オブジェクトを取得します。 **Grid Overview **コンポーネントは、`/apps/extjstraining/components/gridoverview/referencesearch.js`にある`referencesearch.js`ファイルで定義される、`getGridPanel()`メソッドに対して異なる実装を提供します。 コンポーネント jsp で参照される .js ファイルを切り替えることにより、グリッドは、リポジトリから取得したデータに基づくようになります。

コンポーネント jsp で参照される .js ファイルを切り替えます。

1. **CRXDE Lite** で、コンポーネントの `content.jsp` ファイル内にある `defaultgrid.js` ファイルを含む行をコメント化します。次のようになります。
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. `referencesearch.js` ファイルを含む行からコメントを削除します。次のようになります。
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. 変更内容を保存します。
1. サンプルページを更新します。

このコンポーネントは、次のように表示されます。

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

コンポーネントjspで参照されるJavaScriptコード(`referencesearch.js`)は、コンポーネントjspから呼び出される`getGridPanel()`メソッドを定義し、リポジトリから動的に取得されるデータに基づいて` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`オブジェクトを返します。 `referencesearch.js` のロジックでは、一部の動的データが GridPanel の基礎として定義されています。

* `reader` は、JSON 形式のサーブレット応答を読み取る 3 列用の ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` オブジェクトです。
* `cm` は3列 ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` のオブジェクトです。「テスト」列のセルは、editor で定義されているので、編集することが可能です。
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* 列は並べ替え可能です。
   `cm.defaultSortable = true;`
* `store` はオブジェクト ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` です。
   * クエリのフィルタリングに使用するパラメーターをいくつか指定して、「 `/bin/querybuilder.json` 」に登録されたサーブレットを呼び出すことで、データを取得します
   * 前に定義した `reader` に基づきます。
   * 表は、「**jcr:path**」列に従って、昇順で並べ替えられます。
* `gridPanel` は、編集 ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` 可能なオブジェクトです。
   * 事前定義済みの `store` と列モデル `cm` に基づいています。
   * 選択できる行は一度に 1 つのみです。
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * `afteredit` リスナーは、「**テスト**」列のセルが編集されたことを確認します。
      * 「**jcr:path**」列で定義されたパスにあるノードのプロパティ「`test`」は、セルの値を使用してリポジトリに設定されます
      * POST が成功した場合は、値が `store` オブジェクトに追加されます。POST が失敗した場合は、値が拒否されます。
