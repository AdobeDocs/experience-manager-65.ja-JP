---
title: ページトラッカーとWebページの埋め込みコードの使用
description: ページトラッカーコードと埋め込み JavaScript コードを Web サイトコードに組み込んで、Adobe Analytics でアセットの使用状況データを収集できるようにする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: fc433851c24f9049e7ba6dfada24d6e552eb6d05
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 70%

---


# ページトラッカーと埋め込みコードをWebページで使用する{#using-page-tracker-and-embed-code-in-web-pages}

ページトラッカーはJavaScriptコードの1つで、Adobe AnalyticsがこれらのWebサイトの[!DNL Adobe Experience Manager Assets]付近の使用状況データを取り込めるようにするために、サードパーティWebサイトのコードに含めます。

アセット固有のイベント（クリックなど）を取得するには、サードパーティの Web サイトコードに埋め込みコードも含めます。

次のサンプルコードは、ページトラッカーコードと埋め込みコードの両方を含む Web ページです。

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## 追加ページトラッカーコード{#adding-page-tracker-code}

ページトラッカーコードは Web サイトコードのヘッダーセクションに追加します。次のコードスニペットは、サンプル Web ページに組み込まれたページトラッカーコードです。

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## 追加埋め込みコード{#add-embed-code}

埋め込みコードは Web サイトコードの本文に追加します。次のコードスニペットは、サンプル Web ページに組み込まれた埋め込みコードです。

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
