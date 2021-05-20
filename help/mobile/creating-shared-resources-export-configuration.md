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
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
>**前提条件**:
>
>共有リソースの作成と変更について学習する前に、[コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)を参照して、基本的な概念を理解してください。

AEM Mobile のユーザーは、コンテンツ同期を使用して、ライブコンテンツをモバイルアプリ用の静的コンテンツとして書き出します。AEM Mobile からコンテンツを Mobile On-demand Services にアップロードしたときに書き出しがおこなわれます。

上記の表に示したプロパティ&#x200B;***dps-exportTemplate***&#x200B;は、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

以下のリソースでは、Adobe Experience Manager（AEM）から共有リソースを書き出して AEM Mobile にアップロードする手順について説明しています。

共有HTMLリソースを使用すると、HTMLリソースを共有できます。HTMLリソースを共有する場合は、すべての記事に複製する必要があります。また、アイコン、フォント、JavaScript、CSSを含めることもできます。

**&lt;dps-exportTemplate>/dps-HTMLResources>**&#x200B;にあるコンテンツ同期設定は、デバイス上でのプロパティ静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

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
1. このパス&#x200B;*[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*&#x200B;を参照して、サンプルの共有リソースを表示します。

   以下の図に示すように、共有リソースを作成するのに必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>いずれかの共有リソースが変更された場合は、共有リソースを AEM Mobile On-demand Services にアップロードするか、書き出す必要があります。
