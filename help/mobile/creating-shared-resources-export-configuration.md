---
title: 共有リソースのエクスポート設定の作成
seo-title: Creating Shared Resources Export Configuration
description: このページでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順の詳細について説明します。
seo-description: Follow this page to learn about exporting shared resources from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 67%

---

# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について詳しくは、 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) を参照してください。

AEM Mobile のユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリ用の静的コンテンツとして書き出します。AEM Mobile からコンテンツを Mobile On-demand Services にアップロードしたときに書き出しがおこなわれます。

プロパティ ***dps-exportTemplate*** 上記の表で、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

以下のリソースでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順について説明しています。

共有HTMLリソースを使用すると、HTMLリソースを共有できます。記事が共有されていない場合は、すべての記事で複製する必要があります。また、アイコン、フォント、JavaScript、CSS を含めることができます。

コンテンツ同期設定が次の場所に見つかりました： **&lt;dps-exporttemplate>/dps-HTMLResources>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

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
1. このパスを参照 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*、サンプルの共有リソースを表示します。

   以下の図に示すように、共有リソースを作成するのに必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>いずれかの共有リソースが変更された場合は、共有リソースを AEM Mobile On-demand Services にアップロードするか、書き出す必要があります。
