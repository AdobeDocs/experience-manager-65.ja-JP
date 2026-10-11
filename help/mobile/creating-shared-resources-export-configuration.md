---
title: 共有リソースのエクスポート設定の作成
description: Adobe Experience Manager（AEM）からAEM Mobileへのアップロード用の共有リソースの書き出しについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%
---
# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について詳しくは、[ コンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)を参照して、基本的な概念を理解してください。

Adobe Experience Manager（AEM）モバイルユーザーは、コンテンツシンクを使用して、モバイルアプリで使用するためにライブコンテンツを静的コンテンツに書き出します。この書き出しは、コンテンツがAEM MobileからMobile On-Demand Servicesにアップロードされるときに行われます。

上記の表に記載されているプロパティ ***dps-exportTemplate***&#x200B;は、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次の資料では、AEM MobileにアップロードするためのAEMからの共有リソースの書き出しについて説明します。

Shared HTML Resourcesを使用すると、すべての記事で重複するHTML リソースを記事で共有できます。これには、アイコン、フォント、JavaScript、cssが含まれます。

**&lt;dps-exportTemplate>/dps-HTMLResources>**&#x200B;にあるコンテンツ同期設定は、デバイスでのプロパティの静的レンダリングに必要なすべてのコンテンツと記事を書き出すように設定する必要があります。

>[!CAUTION]
>
>次の手順を実行して、サンプルの共有リソースを表示できます。ただし、次の手順を実行できるのは、次の条件に該当する場合だけです。
>
>* サンプルコンテンツをインストールしました
>* AEM インスタンスの実行
>* カスタムコンテキストまたは別のポートが設定されていません
>

共有リソースのサンプルを表示するには、次の手順を参照してください。

1. AEM サーバーでCRXDE Liteを開きます。
1. このパス *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*&#x200B;を参照して、サンプルの共有リソースを表示します。

   次の図に示すように、共有リソースの作成に必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共有リソースのいずれかが変更されたときに、共有リソースをアップロードするか、AEM Mobile On-demand Servicesに書き出す必要があります。
