---
title: ターゲットコンテンツの開発
seo-title: Developing for Targeted Content
description: コンテンツターゲティングで使用するコンポーネントの作成に関するトピック
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 97%

---

# ターゲットコンテンツの開発{#developing-for-targeted-content}

ここでは、コンテンツターゲティングで使用するコンポーネントの作成に関するトピックを取り上げます。

* Adobe Target との統合については、[Adobe Target との統合](/help/sites-administering/target.md)を参照してください。
* ターゲットコンテンツのオーサリングについては、[ターゲット設定モードを使用したターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md)を参照してください。

>[!NOTE]
>
>AEM オーサーインスタンスでコンポーネントをターゲット設定すると、そのコンポーネントが、キャンペーンの登録、オファーの設定、Adobe Target セグメントの取得（設定されている場合）を行うために、Adobe Target に対して一連のサーバー側呼び出しを実行します。AEM パブリッシュから Adobe Target にサーバー側呼び出しは作成されません。

## ページ上での Adobe Target によるターゲット設定の有効化 {#enabling-targeting-with-adobe-target-on-your-pages}

ページ内のターゲットコンポーネントを使用して Adobe Target とやり取りするには、&lt;head> 要素に特定のクライアントサイドコードを含めます。

### head セクション {#the-head-section}

ページの &lt;head> セクションに次の両方のコードブロックを追加します。

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

このコードによって、必要な分析用 Javascript オブジェクトが追加され、Web サイトに関連付けられているクラウドサービスライブラリが読み込まれます。Target のサービスでは、ライブラリは `/libs/cq/analytics/components/testandtarget/headlibs.jsp` によって読み込まれます。

読み込まれるライブラリのセットは、Target の設定で使用されているターゲットクライアントライブラリのタイプ（mbox.js または at.js）によって異なります。

**デフォルトの mbox.js の場合**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**カスタムの mbox.js の場合**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**at.js の場合**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>製品と共に出荷された `at.js` のバージョンのみがサポートされます。製品と共に出荷された `at.js` のバージョンは、次の場所の `at.js` ファイルで取得できます。
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**。

**カスタムの at.js の場合**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

Target のクライアントサイド機能は、`CQ_Analytics.TestTarget` オブジェクトによって管理されます。そのため、ページには次の例のような init コードが含まれます。

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

この JSP によって、必要な分析 JavaScript オブジェクトと参照がクライアント側の JavaScript ライブラリに追加されます。testandtarget.js ファイルには、mbox.js 関数が含まれています。このスクリプトが生成する HTML は、次の例のようになります。

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### body セクション（開始） {#the-body-section-start}

ClientContext 機能をページに追加するには、&lt;body> タグの直後に次のコードを追加します。

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### body セクション（終了） {#the-body-section-end}

&lt;/body> 終了タグの直前に次のコードを追加します。

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

このコンポーネントの JSP スクリプトは、Target JavaScript API への呼び出しを生成し、その他の必要な設定を実装します。このスクリプトが生成する HTML は、次の例のようになります。

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
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
</div>
```

### カスタムターゲットライブラリファイルの使用 {#using-a-custom-target-library-file}

>[!NOTE]
>
>DTM または別のターゲットマーケティングシステムを使用していない場合は、カスタムターゲットライブラリファイルを使用できます。

>[!NOTE]
>
>デフォルトでは mbox は非表示です。この設定は、mboxDefault クラスによって決まります。mbox が非表示の場合は、入れ替えられる前にデフォルトコンテンツが訪問者に表示されません。ただし、体感パフォーマンスに影響が生じます。

mbox の作成に使用されるデフォルトの mbox.js ファイルは、/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js にあります。カスタムの mbox.js ファイルを使用するには、このファイルを Target クラウド設定に追加します。mbox.js ファイルを追加するには、そのファイルがファイルシステム上で使用可能になっている必要があります。

例えば、[Marketing Cloud ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html)を使用する場合は、mbox.js をダウンロードし、使用するテナントに基づいて `imsOrgID` 変数に適切な値を格納する必要があります。この変数は、Marketing Cloud ID サービスとの統合に必須です。詳しくは、[Adobe Target のレポートソースとしての Adobe Analytics](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) および[実装する前に](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html)を参照してください。

>[!NOTE]
>
>Target 設定でカスタム mbox が定義されている場合は、すべてのユーザーにパブリッシュサーバー上の **/etc/cloudservices** への読み取りアクセス権限が必要です。このアクセス権限がないと、発行 web サイト上の mbox.js ファイルの読み込みが 404 エラーになります。

1. CQ の&#x200B;**ツール**&#x200B;ページに移動して、**クラウドサービス**&#x200B;を選択してください。（[https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)）
1. ツリーで「Adobe Target」を選択し、設定リストの中から目的の Target 設定をダブルクリックします。
1. 設定ページで「編集」をクリックします。
1. カスタム mbox.js プロパティの場合は、「参照」をクリックし、ファイルを選択します。
1. 変更を適用するには、Adobe Target アカウントのパスワードを入力し、「Adobe Target に再接続」をクリックして、接続が成功したら「OK」をクリックします。次に、コンポーネントを編集ダイアログボックスで「OK」をクリックします。

Target 設定にカスタム mbox.js ファイルが含まれます。これはページの [head セクション内に必要なコード](/help/sites-developing/target.md#p-the-head-section-p)で、testandtarget.js ライブラリへの参照の代わりに、クライアントライブラリフレームワークにファイルを追加するものです。

## コンポーネントに対する「ターゲット」コマンドの無効化 {#disabling-the-target-command-for-components}

大部分のコンポーネントは、コンテキストメニューで「ターゲット」コマンドを使用して、ターゲットコンポーネントに変換することができます。

![chlimage_1-21](assets/chlimage_1-21.png)

コンテキストメニューから「ターゲット」コマンドを削除するには、コンポーネントの cq:editConfig ノードに次のプロパティを追加します。

* 名前：cq:disableTargeting
* 型：ブール値
* 値：True

例えば、Geometrixx デモサイトページのタイトルコンポーネントに対するターゲット設定を無効化するには、このプロパティを /apps/geometrixx/components/title/cq:editConfig ノードに追加します。

![chlimage_1-22](assets/chlimage_1-22.png)

## Adobe Target への注文確認情報の送信 {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>DTM を使用していない場合は、注文確認を Adobe Target に送信します。

Web サイトのパフォーマンスを追跡するには、注文確認ページから Adobe Target に購入情報を送信します（Adobe Target ドキュメントの [orderConfirmPage mbox の作成](https://experienceleague.adobe.com/docs/dtm/implementing/target/configure-target/mboxes/order-confirmation-mbox.html)を参照）。mbox が `orderConfirmPage` という名前を持ち、以下の特定のパラメーター名を使用している場合は、Adobe Target が mbox データを注文確認データとして認識します。

* productPurchasedId：購入された商品を識別する ID のリスト。
* orderId：注文の ID。
* orderTotal：購入の合計金額。

レンダリングされた HTML ページ上の mbox を作成するコードは、次の例のようになります。

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

各パラメーターの値は注文ごとに異なります。そのため、購入のプロパティに基づいてコードを生成するコンポーネントが必要です。CQ の [e コマース統合フレームワーク](/help/commerce/cif-classic/administering/ecommerce.md)を使用すると、商品カタログを統合し、買い物かごとチェックアウトページを実装できます。

Geometrixx Outdoors のサンプルでは、訪問者が商品を購入すると、以下の確認ページが表示されます。

![chlimage_1-23](assets/chlimage_1-23.png)

以下に示すコードは、買い物かごのプロパティにアクセスして、mbox を作成するためのコードを出力するコンポーネントの JSP スクリプトです。

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

このコンポーネントが前述の例のチェックアウトページに含まれている場合、ページのソースには、mbox を作成する以下のスクリプトが含まれます。

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Target コンポーネントについて {#understanding-the-target-component}

Target コンポーネントを使用すると、CQ コンテンツコンポーネントから動的 mbox を作成できます（[コンテンツのターゲティング](/help/sites-authoring/content-targeting-touch.md)を参照）。Target コンポーネントは、/libs/cq/personalization/components/target にあります。

target.jsp スクリプトは、ページのプロパティにアクセスして、コンポーネントに使用するターゲティングエンジンを決定し、適切なスクリプトを実行します。

* Adobe Target：/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target（AT.JS を使用）](/help/sites-administering/target.md)：/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md)：/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* クライアントサイドのルール／ContextHub：/libs/cq/personalization/components/target/engine_cq.jsp

### mbox の作成 {#the-creation-of-mboxes}

>[!NOTE]
>
>デフォルトでは mbox は非表示です。この設定は、mboxDefault クラスによって決まります。mbox が非表示の場合は、入れ替えられる前にデフォルトコンテンツが訪問者に表示されません。ただし、体感パフォーマンスに影響が生じます。

Adobe Target がコンテンツターゲティングをおこなうときには、engine_tnt.jsp スクリプトが、ターゲット設定されたエクスペリエンスのコンテンツを格納する mbox を作成します。

* Adobe Target API の要求に応じて、`mboxDefault` クラスの `div` 要素を追加します。

* `div` 要素の内側に mbox コンテンツ（ターゲット設定されたエクスペリエンスのコンテンツ）を追加します。

`mboxDefault` div 要素の後に、mbox を作成する JavaScript が挿入されます。

* mbox 名、ID および場所は、コンポーネントのリポジトリパスに基づきます。
* スクリプトが ClientContext のパラメーター名と値を取得します。
* mbox を作成するために、mbox.js および他のクライアントライブラリが定義する関数への呼び出しがおこなわれます。

#### コンテンツのターゲティングのためのクライアントライブラリ {#client-libraries-for-content-targeting}

利用できる clientlib カテゴリは次のとおりです。

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
