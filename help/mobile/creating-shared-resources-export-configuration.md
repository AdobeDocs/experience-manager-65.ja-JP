---
title: 共有リソースの書き出し設定の作成
seo-title: 共有リソースの書き出し設定の作成
description: このページでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順の詳細について説明します。
seo-description: このページでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順の詳細について説明します。
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 69%

---


# 共有リソースの書き出し設定の作成{#creating-shared-resources-export-configuration}

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

以下のリソースでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順について説明しています。

共有HTMLリソースを使用すると、記事でHTMLリソースを共有できます。このHTMLリソースは、すべての記事で複製が必要になり、アイコン、フォント、javascript、cssを含むことができます。

The Content Sync configuration found at **&lt;dps-exportTemplate>/dps-HTMLResources>** should be configured to export all the content an article required for property static rendering on device.

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
1. Browse to this path *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, to view the sample shared resources.

   以下の図に示すように、共有リソースを作成するのに必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>いずれかの共有リソースが変更された場合は、共有リソースを AEM Mobile On-demand Services にアップロードするか、書き出す必要があります。

