---
title: Adobe Analytics との統合
description: Adobe Experience Manager（AEM）と Adobe Analytics を統合する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 93%
---
# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM の統合により、web ページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* Adobe Analytics レポートスイートに送信されたデータはフレームワークで特定されます。

データには、次のようなページおよびユーザーデータが含まれます。

* AEM コンポーネントで収集されるデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問されるページの数

統合の設定に役立つ情報は、次のページにあります。

* [Adobe Analytics への接続とフレームワークの作成](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics のリンクトラッキングの設定](/help/sites-administering/adobeanalytics-link.md)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics のビデオトラッキングの設定](/help/sites-administering/adobeanalytics-video.md)
* [Adobe Classifications](/help/sites-administering/adobeanalytics-classifications.md)

また、[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を実行できます。

>[!NOTE]
>
>方法については、[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=ja)も参照してください。

## その他の情報 {#further-information}

次のページを参照してください。

* ユーザーデータを収集するコンポーネントの開発と Adobe Analytics フレームワークのカスタマイズに関する情報については、[Adobe Analytics 統合の拡張](/help/sites-developing/extending-analytics.md)を参照してください。

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、（例えば、Web コンソールで）**Apache HTTP Client** プロキシ設定に必要な [2 つの OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md)する必要があります。 AEM の一部の機能では 3.x API を使用し、他の機能では 4.x API を使用するので、両方とも必要です。 設定：
>
>* **Day Commons HTTP Client 3.1**（3.x API を設定）。
>  例：[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP コンポーネントプロキシ設定**（4.x API を設定）。
>  例：[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
