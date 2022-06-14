---
title: 記事のエクスポート設定の作成
seo-title: Creating Article Export Configuration
description: このページでは、Adobe Experience Manager（AEM）からコンテンツを書き出して AEM Mobile にアップロードする方法について説明します。
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 71%

---

# 記事のエクスポート設定の作成{#creating-article-export-configuration}

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

以下のリソースでは、Adobe Experience Manager（AEM）からコンテンツを書き出して AEM Mobile にアップロードする方法について説明します。

記事には、書き出してアップロードする必要があるコンテンツが含まれています。このコンテンツの一部を記事の間で共有できます。

用途 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) コンテンツをまとめて ***共有リソース*** パッケージ。

次の場所に ContentSync 設定が見つかりました： **&lt;dps-exporttemplate>/dps-article>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

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
1. このパスを参照 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)、サンプルの共有リソースを表示します。

   以下の図に示すように、共有リソースを作成するのに必要なすべてのプロパティを表示できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>記事のコンテンツが変更された場合は、記事を AEM Mobile On-Demand Services にアップロードまたは書き出す必要があります。
