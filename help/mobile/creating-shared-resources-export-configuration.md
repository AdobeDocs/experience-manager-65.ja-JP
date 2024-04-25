---
title: 共有リソースのエクスポート設定の作成
description: ここでは、AEM Mobileにアップロードするために共有リソースをAdobe Experience Manager（AEM）から書き出す方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 11%

---

# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成および変更を学ぶ前に、次を参照してください [コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md) を参照して、基本概念を理解します。

Adobe Experience Manager（AEM）のモバイルユーザーは、コンテンツ同期を使用して、モバイルアプリで使用するためにライブコンテンツを静的コンテンツに書き出します。この書き出しは、コンテンツがAEM Mobileから Mobile On-Demand Services にアップロードされる際に行われます。

プロパティ ***dps-exportTemplate*** 上記の表で説明されている、はアプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次のリソースでは、AEMから共有リソースを書き出し、AEM Mobileにアップロードする方法について説明します。

共有HTMLーリソースを使用すると、すべてのアーティクルで重複するHTMLーリソースをアーティクルで共有できます。アイコン、フォント、JavaScript、CSS を含めることができます。

コンテンツ同期設定はにあります。 **&lt;dps-exporttemplate>/dps-HTMLResources>** は、デバイスでのプロパティの静的レンダリングに必要な記事のすべてのコンテンツを書き出すように設定する必要があります。

>[!CAUTION]
>
>以下の手順を実行してサンプルの共有リソースを表示できるのは、次のような場合のみです。
>
>* サンプルコンテンツがインストールされました
>* 実行中のAEM インスタンス
>* カスタム コンテキストが構成されていないか、別のポートがありません
>

サンプルの共有リソースを表示するには、以下の手順を参照してください。

1. AEM サーバーでCRXDE Liteを開きます。
1. このパスを参照 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*&#x200B;共有リソースのサンプルを表示します。

   次の図に示すように、共有リソースの作成に必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共有リソースに変化があった場合は、共有リソースをAEM Mobile On-demand Servicesにアップロードまたは書き出す必要があります。
