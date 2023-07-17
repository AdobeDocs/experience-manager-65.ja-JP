---
title: 共有リソースのエクスポート設定の作成
description: このページでは、Adobe Experience Manager(AEM) からAEM Mobileにアップロードする共有リソースを書き出す方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 4%

---

# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について学習する前に、 [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) を参照してください。

Adobe Experience Manager(AEM)Mobile ユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリで使用する静的コンテンツに書き出し、この書き出しは、AEM Mobileから Mobile On-Demand Services にコンテンツがアップロードされたときに発生します。

プロパティ ***dps-exportTemplate*** 上記の表で、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次のリソースでは、AEMからAEM Mobileにアップロードする共有リソースを書き出す方法について説明します。

共有HTMLリソースを使用すると、記事は、すべての記事で複製されるHTMLリソースを共有でき、アイコン、フォント、JavaScript および css を含めることができます。

コンテンツ同期設定が次の場所に見つかりました： **&lt;dps-exporttemplate>/dps-HTMLResources>** は、デバイス上のプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

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
1. このパスを参照 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*、サンプルの共有リソースを表示します。

   共有リソースの作成に必要なすべてのプロパティを次の図に示すように表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共有リソースのいずれかが変更された場合は、AEM Mobile On-demand Servicesにアップロードまたは書き出す必要があります。
