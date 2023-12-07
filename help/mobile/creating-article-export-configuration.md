---
title: 記事のエクスポート設定の作成
description: このページでは、Adobe Experience Manager(AEM) からAEM Mobileにアップロードするコンテンツを書き出す方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 4%

---

# 記事のエクスポート設定の作成{#creating-article-export-configuration}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について詳しくは、 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) を参照してください。

AEM Mobileのユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリで使用する静的コンテンツに書き出します。この書き出しは、AEM Mobileから Mobile On-Demand Services にコンテンツがアップロードされたときに発生します。

プロパティ ***dps-exportTemplate*** 上記の表で、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次のリソースでは、Adobe Experience Manager(AEM) からコンテンツを書き出してAEM Mobileにアップロードする方法について説明します。

記事には、書き出しとアップロードが必要なコンテンツが含まれています。 このコンテンツの一部は、記事間で共有できます。

用途 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) コンテンツをまとめて ***共有リソース*** パッケージ。

次の場所に ContentSync 設定が見つかりました： **&lt;dps-exporttemplate>/dps-article>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

>[!CAUTION]
>
>以下の手順を実行して、以下の場合に限り、サンプルの共有リソースを表示できます。
>
>* サンプルコンテンツをインストール済み
>* 実行中のAEMインスタンス
>* カスタムコンテキストが設定されていないか、別のポートがありません
>

サンプルの共有リソースを表示するには、以下の手順を参照してください。

1. AEMサーバーのCRXDE Liteを開きます。
1. このパスを参照 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)、サンプルの共有リソースを表示します。

   共有リソースの作成に必要なすべてのプロパティを次の図に示すように表示できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>記事のコンテンツが変更された場合は、AEM Mobile On-demand Servicesに記事をアップロードまたは書き出す必要があります。
