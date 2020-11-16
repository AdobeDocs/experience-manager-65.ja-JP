---
title: デバイスの機能へのアクセス
seo-title: デバイスの機能へのアクセス
description: このページでは、デバイスの機能にアクセスする AEM コンポーネントのビルドについて説明します。AEM PhoneGap Kitchen Sink GitHub リポジトリは、多数のコア Cordova API の使用法を示す、機能 AEM アプリを開発者に提供します。
seo-description: このページでは、デバイスの機能にアクセスする AEM コンポーネントのビルドについて説明します。AEM PhoneGap Kitchen Sink GitHub リポジトリは、多数のコア Cordova API の使用法を示す、機能 AEM アプリを開発者に提供します。
uuid: 1996f017-21d3-4d90-9f55-95c626bc4c60
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 0019e367-8edc-4a23-bfa4-5beda266ace6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 69%

---


# デバイスの機能へのアクセス{#access-device-features}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

## デバイスの機能にアクセスする AEM コンポーネントのビルド {#building-aem-components-that-access-device-features}

The [AEM PhoneGap Kitchen Sink](https://github.com/blefebvre/aem-phonegap-kitchen-sink) Github repository provides developers with a functional AEM app that illustrates the use of a number of core Cordova APIs. iOS または Android で PhoneGap CLI からこのアプリを実行すると、次に示すように各デバイス API へのリンクが含まれている次のページが開きます。

![chlimage_1-107](assets/chlimage_1-107.png)

The source code for each of these device API components is [available on Github](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

For more detail on the usage of each API, I recommend taking a look at the [Cordova plugin documentation](https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html).

## 次の手順 {#the-next-steps}

See [Track App Performance with Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md).
