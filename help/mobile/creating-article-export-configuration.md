---
title: 記事の書き出し設定の作成
seo-title: 記事の書き出し設定の作成
description: このページでは、Adobe Experience Manager（AEM）からコンテンツを書き出して AEM Mobile にアップロードする方法について説明します。
seo-description: このページでは、Adobe Experience Manager（AEM）からコンテンツを書き出して AEM Mobile にアップロードする方法について説明します。
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 73%

---


# 記事の書き出し設定の作成{#creating-article-export-configuration}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

>[!CAUTION]
>
>**前提条件**：
>
>Prior to learn about creating and modifying shared resources, see [Content Sync](/help/mobile/mobile-ondemand-contentsync.md) to understand the basic concepts.

AEM Mobile のユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリ用の静的コンテンツとして書き出します。AEM Mobile からコンテンツを Mobile On-demand Services にアップロードしたときに書き出しがおこなわれます。

The property ***dps-exportTemplate*** mentioned in table above, defines the path to the app&#39;s export configs. 共有リソースを作成および変更するには、このプロパティを設定します。

以下のリソースでは、Adobe Experience Manager（AEM）からコンテンツを書き出して AEM Mobile にアップロードする方法について説明します。

記事には、書き出してアップロードする必要があるコンテンツが含まれています。このコンテンツの一部を記事の間で共有できます。

Use [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) to gather the content together and create a ***Shared Resources*** package.

The ContentSync configuration found at **&lt;dps-exportTemplate>/dps-article>** should be configured to export all the content an article required for property static rendering on device.

>[!CAUTION]
>
>以下に示す手順を実行して、サンプルの共有リソースを表示できます。ただし、以下の条件が必要です。
>
>* サンプルコンテンツをインストールしていること
>* AEM インスタンスを実行していること
>* カスタムコンテキストや異なるポートを設定していないこと

>



サンプルの共有リソースを表示するには、以下の手順に従います。

1. AEM サーバーで、CRXDE Lite を開きます。
1. Browse to this path [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), to view the sample shared resources.

   以下の図に示すように、共有リソースを作成するのに必要なすべてのプロパティを表示できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>記事のコンテンツが変更された場合は、記事を AEM Mobile On-Demand Services にアップロードまたは書き出す必要があります。

