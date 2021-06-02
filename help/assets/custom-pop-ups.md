---
title: クイックビューを使用したカスタムポップアップの作成
seo-title: クイックビューを使用したカスタムポップアップの作成
description: e コマースエクスペリエンスではデフォルトのクイックビューが使用され、ポップアップに購入を促す商品情報が表示されます。このようなポップアップにカスタムコンテンツが表示されるように設定できます。
seo-description: e コマースエクスペリエンスではデフォルトのクイックビューが使用され、ポップアップに購入を促す商品情報が表示されます。このようなポップアップにカスタムコンテンツが表示されるように設定できます。
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: ビューア
role: Business Practitioner, Administrator
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: a4e9a4003bf0ce686578d3f8b3fddc19bc49dfb4
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 72%

---

# クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

e コマースエクスペリエンスではデフォルトのクイックビューが使用され、ポップアップに購入を促す商品情報が表示されます。ただし、このようなポップアップにカスタムコンテンツが表示されるように設定できます。ビューアに応じて、この機能を使用して、ユーザーはホットスポット、サムネール画像、画像マップをタップして、情報や関連コンテンツを表示できます。

クイックビューは、Dynamic Media の以下のビューアでサポートされています。

* インタラクティブ画像（クリック可能なホットスポット）
* インタラクティブビデオ（ビデオの再生中にクリック可能なサムネール画像）
* カルーセルバナー（クリック可能なホットスポットまたは画像マップ）

各ビューアの機能は異なりますが、サポートされる 3 つすべてのビューアでクイックビューの作成手順は同じです。

**クイックビューを使用してカスタムポップアップを作成するには:**

1. アップロードしたアセット用にクイックビューを作成します。

   一般には、使用しているビューアでアセットを使用するために編集するときにクイックビューを作成します。

   <table>
    <tbody>
    <tr>
    <td><strong>使用しているビューア</strong></td>
    <td><strong>クイックビューを作成する場合は、次の手順を実行します</strong></td>
    </tr>
    <tr>
    <td>インタラクティブ画像</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">画像バナーへのホットスポットの追加</a></td>
    </tr>
    <tr>
    <td>インタラクティブビデオ</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">ビデオへのインタラクティブ機能の追加</a>.</td>
    </tr>
    <tr>
    <td>カルーセルバナー</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">バナーへのホットスポットまたは画像マップの追加</a><br /> </td>
    </tr>
    </tbody>
   </table>

1. ビューアの埋め込みコードを取得し、Web サイトにビューアを統合します。

   <table>
    <tbody>
    <tr>
    <td><strong>使用しているビューア</strong><br /> </td>
    <td><strong>ビューアをWebサイトに統合する場合は、次の手順を実行します</strong></td>
    </tr>
    <tr>
    <td>インタラクティブ画像</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">インタラクティブ画像の Web サイトへの統合</a>.<br /> </td>
    </tr>
    <tr>
    <td>インタラクティブビデオ<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">インタラクティブビデオの Web サイトへの統合</a>.<br /> </td>
    </tr>
    <tr>
    <td>カルーセルバナー</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Web サイトページへのカルーセルバナーの追加</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. 現在使用しているビューアは、クイックビューの使用方法を認識している必要があります。

   ビューアは `QuickViewActive` というハンドラーを使用します。

   ****
例Webページでインタラクティブ画像用に以下のサンプル埋め込みコードを使用するとします。

   ![chlimage_1-291](assets/chlimage_1-291.png)

   ハンドラーは `setHandlers` を使用してビューアに読み込まれます。

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **上記のサンプル埋め込みコードの例を使用すると、次のコードが表示されます。**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   `setHandlers()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html?lang=ja)
   * インタラクティブビデオビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html?lang=ja)

1. 次に、`quickViewActivate`ハンドラーを設定する必要があります。

   `quickViewActivate` ハンドラーはビューアのクイックビューを制御します。このハンドラーには、クイックビューで使用する変数のリストと関数呼び出しが含まれています。埋め込みコードは、クイックビューのSKU変数セットとサンプルの`loadQuickView`関数呼び出しのマッピングを提供します。

   **変数マッピング** Web ページで使用する変数を SKU 値とクイックビューに含まれる一般変数にマッピングします。

   `var *variable1*= inData.*quickviewVariable*`

   提供された埋め込みコードには、SKU 変数用のサンプルマッピングが含まれています。

   `var sku=inData.sku`

   以下のように、クイックビューからの追加変数もマッピングします。

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **関数呼び出し**&#x200B;ハンドラーには、クイックビューを機能させるために関数呼び出しも必要です。この関数は、ホストページからアクセスできることが前提となります。埋め込みコードは、サンプル関数呼び出しを提供します。

   `loadQuickView(sku)`

   このサンプル関数呼び出しは、関数 `loadQuickView()` が存在しアクセス可能であることが前提となります。

   `quickViewActivate` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html?lang=ja)
   * インタラクティブビデオビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html?lang=ja)
   * インタラクティブビデオビューアでのインタラクティブデータのサポート：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html?lang=ja)

1. 以下の操作を実行してください。

   * 埋め込みコードの setHandlers セクションのコメントアウトを解除します。
   * クイックビューに含まれる追加変数をマッピングします。

      * 変数を追加する場合は、`loadQuickView(sku,*var1*,*var2*)` 呼び出しを更新します。
   * ビューア外でページにシンプルな `loadQuickView` () 関数を作成します。

      例えば、以下の場合は、ブラウザーのコンソールに SKU の値が書き込まれます。

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Web サーバーにテスト HTML ページをアップロードし、開きます。

       クイックビューからの変数がマッピングされ、関数呼び出しが追加された状態で、ブラウザーコンソールは提供されたサンプル関数を使用してブラウザーコンソールに変数値を書き込みます。



1. これで、関数を使用してクイックビューでシンプルなポップアップを起動できるようになりました。以下の例では、ポップアップに `DIV` を使用しています。
1. ポップアップの `DIV` を以下のようなスタイルにします。必要に応じて独自のスタイルを追加します。

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. HTML ページのボディにポップアップの `DIV` を配置します。

   要素の1つに、ユーザーがクイックビューを起動したときにSKU値で更新されるIDが設定されます。 この例にはこれに加え、ポップアップを表示後に再び隠すための単純なボタンも含まれています。

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. ポップアップのSKU値を更新できる関数を追加します。手順5で作成したシンプルな関数を置き換えて、ポップアップを表示します。 ポップアップを表示させます。

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Web サーバーにテスト HTML ページをアップロードし、開きます。ユーザーがクイックビューを起動すると、ビューアにポップアップの `DIV` が表示されます。
1. **全画面表示モードでカスタムポップアップを表示する方法**

   インタラクティブビデオビューアなどの一部のビューアでは、全画面表示モードでの表示をサポートしています。ただし、前の手順で説明したポップアップを使用すると、全画面表示モード中はビューアの背後に表示されるようになります。

   標準モードと全画面表示モードの両方でポップアップを表示させるには、ビューアのコンテナにポップアップをアタッチします。2つ目のハンドラメソッド`initComplete`を使用します。

   `initComplete` ハンドラーは、ビューアの初期化後に呼び出されます。

   ```xml
   "initComplete":function() { code block }
   ```

   `init()` メソッドについて詳しくは、以下を参照してください。

   * インタラクティブ画像ビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html?lang=ja)
   * インタラクティブビデオビューア：[https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html?lang=ja)

1. 前の手順で説明したポップアップをビューアにアタッチするには、次のコードを使用します。

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   上記のコードでは、次の処理が行われました。

   * カスタムポップアップを識別しました。
   * DOM からの削除
   * ビューアコンテナの指定
   * ビューアコンテナへのポップアップのアタッチ

1. setHandlersコード全体は、次のようになります（インタラクティブビデオビューアを使用）。

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. ハンドラーを読み込んだ後で、ビューアを初期化します。

   `*viewerInstance.*init()`

   **例**：この例では、インタラクティブ画像ビューアを使用します。

   `s7interactiveimageviewer.init()`

   ホストページにビューアを埋め込んだ後で、`init()` を使用してビューアを起動する前に、ビューアインスタンスが作成され、ハンドラーが読み込まれていることを確認してください。
