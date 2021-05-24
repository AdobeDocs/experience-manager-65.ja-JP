---
title: コンポーネントへのAdobe Analyticsトラッキングの追加
seo-title: コンポーネントへのAdobe Analyticsトラッキングの追加
description: コンポーネントへのAdobe Analyticsトラッキングの追加
seo-description: 'null'
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 45%

---

# Adobe Analyticsトラッキングのコンポーネントへの追加{#adding-adobe-analytics-tracking-to-components}

## Adobe Analyticsモジュールをページコンポーネントに含める{#including-the-adobe-analytics-module-in-a-page-component}

ページテンプレートコンポーネント(例：`head.jsp, body.jsp`)ContextHubとAdobe Analytics統合(Cloud Servicesの一部)を読み込むには、JSPインクルードが必要です。 すべてには、読み込みJavaScriptファイルが含まれます。

ContextHubCloud Servicesは`<head>`タグのすぐ下、エントリは`<head>`セクションの`</body>`セクションの前に含める必要があります。例：

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

`<head>`要素の後に挿入する`contexthub`スクリプトによって、ContextHub機能がページに追加されます。

`<head>`セクションと`<body>`セクションに追加する`cloudservices`スクリプトは、ページに追加されるクラウドサービス設定に適用されます。 (ページで複数のCloud Services設定を使用する場合は、ContextHub jspとCloud Servicesjspを1回だけ含める必要があります)。

Adobe Analyticsフレームワークをページに追加すると、`cloudservices`スクリプトはAdobe Analytics関連のJavaScriptと、次の例のようなクライアント側ライブラリへの参照を生成します。

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

Geometrixx Outdoors をはじめ、すべての AEM サンプルサイトにはこのコードが含まれています。

### sitecatalystAfterCollect イベント  {#the-sitecatalystaftercollect-event}

`cloudservices`スクリプトは`sitecatalystAfterCollect`イベントをトリガーします。

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

このイベントは、ページの追跡が完了したことを示すために呼び出されます。このページに対して追加の追跡操作を実行する場合は、ドキュメント読み込みイベントやドキュメント準備完了イベントではなく、このイベントをリスンする必要があります。`sitecatalystAfterCollect`イベントを使用すると、衝突や予測できない動作を回避できます。

>[!NOTE]
>
>`/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js`ライブラリには、Adobe Analytics `s_code.js`ファイルのコードが含まれます。

## カスタムコンポーネントのAdobe Analyticsトラッキングの実装{#implementing-adobe-analytics-tracking-for-custom-components}

AEMコンポーネントがAdobe Analyticsフレームワークとやり取りできるようにします。 次に、Adobe Analyticsがコンポーネントデータを追跡するようにフレームワークを設定します。

Adobe Analyticsフレームワークとやり取りするコンポーネントは、フレームワークの編集時にサイドキックに表示されます。 コンポーネントをフレームワークにドラッグすると、コンポーネントのプロパティが表示され、Adobe Analyticsのプロパティにマッピングできます。 （&lt;A0/>基本的な追跡のためのフレームワークの設定&lt;A1/>を参照）。[](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework)

コンポーネントに`analytics`という名前の子ノードがある場合、コンポーネントはAdobe Analyticsフレームワークとやり取りできます。 `analytics` ノードには以下のプロパティがあります。

* `cq:trackevents`:コンポーネントが公開するCQイベントを識別します。（カスタムイベントを参照）。
* `cq:trackvars`:Adobe AnalyticsのプロパティにマッピングされるCQ変数の名前を指定します。
* `cq:componentName`：サイドキックに表示されるコンポーネントの名前。
* `cq:componentGroup`:コンポーネントを含むサイドキックのグループ。

コンポーネントの JSP のコードによって、追跡を呼び出し、追跡対象のデータを定義する Javascript がページに追加されます。JavaScriptで使用されるイベント名とデータ名は、`analytics`ノードプロパティの対応する値と一致する必要があります。

* ページの読み込み時にイベントデータを追跡するには、data-tracking 属性を使用します（[ページの読み込み時のカスタムイベントの追跡](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)を参照）。
* ユーザーがページの機能とやり取りするときにイベントデータを追跡するには、CQ_Analytics.record 関数を使用します（[ページの読み込み後のカスタムイベントの追跡](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)を参照）。

これらのデータトラッキングメソッドを使用する場合、Adobe Analytics統合モジュールは、Adobe Analyticsへの呼び出しを自動的に実行して、イベントとデータを記録します。

### 例：topnav クリック数の追跡 {#example-tracking-topnav-clicks}

基盤topnavコンポーネントを拡張して、Adobe Analyticsがページ上部のナビゲーションリンクのクリックを追跡できるようにします。 ナビゲーションリンクがクリックされると、Adobe Analyticsはクリックされたリンクと、そのリンクがクリックされたページを記録します。

以降の手順をおこなうには、以下のタスクを終えている必要があります。

* CQ アプリケーションの作成。
* Adobe Analytics設定とAdobe Analyticsフレームワークを作成しました。

#### topnav コンポーネントのコピー {#copy-the-topnav-component}

topnav コンポーネントを CQ アプリケーションにコピーします。この手順では、アプリケーションが CRXDE Lite で設定されている必要があります。

1. `/libs/foundation/components/topnav`ノードを右クリックし、「コピー」をクリックします。
1. アプリケーションフォルダーの下の Components フォルダーを右クリックして、「貼り付け」をクリックします。
1. 「すべて保存」をクリックします。

#### TopnavとAdobe Analyticsフレームワークの統合{#integrating-topnav-with-the-adobe-analytics-framework}

topnav コンポーネントを設定し、追跡するイベントとデータを定義するように JSP ファイルを編集します。

1. topnav ノードを右クリックして、作成／ノードを作成をクリックします。次のプロパティ値を指定して、「OK」をクリックします。

   * 名前：`analytics`
   * 型：`nt:unstructured`

1. 次のプロパティを analytics ノードに追加して、追跡するイベントに名前を付けます。

   * 名前：cq:trackevents
   * タイプ：String
   * 値：topnavClick

1. 次のプロパティを analytics ノードに追加して、データ変数に名前を付けます。

   * 名前：cq:trackvars
   * タイプ：String
   * 値：topnavTarget、topnavLocation

1. 次のプロパティを analytics ノードに追加して、サイドキックのコンポーネントに名前を付けます。

   * 名前：cq:componentName
   * タイプ：String
   * 値：topnav（追跡）

1. 次のプロパティを analytics ノードに追加して、サイドキックのコンポーネントグループに名前を付けます。

   * 名前：cq:componentGroup
   * タイプ：String
   * 値：一般

1. 「すべて保存」をクリックします。
1. `topnav.jsp`ファイルを開きます。
1. 要素内で、次の属性を追加します。

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. ページの下部に以下の Javascript コードを追加します。

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. 「すべて保存」をクリックします。

`topnav.jsp`ファイルの内容は次のようになります。

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>多くの場合、ContextHubからのデータを追跡することが望ましいです。 JavaScriptを使用してこの情報を取得する方法について詳しくは、[ContextHubの値へのアクセス](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)を参照してください。

#### サイドキックへの追跡コンポーネントの追加 {#adding-the-tracking-component-to-sidekick}

Adobe Analyticsでの追跡を有効にするコンポーネントをサイドキックに追加して、フレームワークに追加できるようにします。

1. Adobe Analytics設定からAdobe Analyticsフレームワークを開きます。 （[http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html)）。
1. サイドキックでデザインボタンをクリックします。

   ![](assets/chlimage_1a.png)

1. 「リンクトラッキング設定」領域で、「継承を設定」をクリックします。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 許可されたコンポーネントリストで、「一般」セクションの「topnav（追跡）」を選択して、「OK」をクリックします。
1. サイドキックを展開して編集モードに入ります。コンポーネントが一般グループに表示されるようになっています。

#### topnav コンポーネントのフレームワークへの追加  {#adding-the-topnav-component-to-your-framework}

topnavコンポーネントをAdobe Analyticsフレームワークにドラッグし、コンポーネント変数とイベントをAdobe Analytics変数とイベントにマッピングします。 （&lt;A0/>基本的な追跡のためのフレームワークの設定&lt;A1/>を参照）。[](/help/sites-administering/adobeanalytics-connect.md)

![chlimage_1-1](assets/chlimage_1-1a.png)

topnavコンポーネントがAdobe Analyticsフレームワークと統合されました。 ページにコンポーネントを追加する場合、上部のナビゲーションバーの項目をクリックすると、トラッキングデータがAdobe Analyticsに送信されます。

### s.productsデータをAdobe Analyticsに送信する{#sending-s-products-data-to-adobe-analytics}

コンポーネントは、Adobe Analyticsに送信されるs.products変数のデータを生成できます。 s.products変数に貢献するようにコンポーネントをデザインします。

* 特定の構造の `product` という値を記録します。
* Adobe Analyticsフレームワーク内のAdobe Analytics変数とマッピングできるように、値`product`のデータメンバーを公開します。

Adobe Analytics s.products変数は、次の構文を使用します。

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics統合モジュールは、AEMコンポーネントが生成する`product`値を使用して`s.products`変数を構築します。 AEMコンポーネントが生成するJavaScriptの`product`値は、次の構造を持つ値の配列です。

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

`product` 値からデータ項目を省略すると、s.products 内の空の文字列として送信されます。

>[!NOTE]
>
>製品値にイベントが関連付けられていない場合、Adobe Analyticsはデフォルトで`prodView`イベントを使用します。

コンポーネントの`analytics`ノードは、`cq:trackvars`プロパティを使用して変数名を公開する必要があります。

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

e コマースモジュールには、s.products 変数データを生成するいくつかのコンポーネントがあります。例えば、submitorder コンポーネント（[http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)）は、以下の例のような Javascript を生成します。

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### トラッキングコールのサイズの制限  {#limiting-the-size-of-tracking-calls}

一般的に、Web ブラウザーでは GET リクエストのサイズが制限されます。CQ の product と SKU の値はリポジトリのパスなので、複数の値を含む product 配列はリクエストサイズの制限を超えることがあります。したがって、各`CQ_Analytics.record function`の`product`配列内の項目数はコンポーネントで制限する必要があります。 追跡する必要がある項目数が制限を超える可能性がある場合は、複数の関数を作成します。

例えば、e コマースの submitorder コンポーネントでは、1 つのコール内の `product` 項目数が 4 に制限されています。カートに 5 つ以上の製品が含まれると、このコンポーネントは複数の `CQ_Analytics.record` 関数を生成します。
