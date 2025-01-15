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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---

# 共有リソースのエクスポート設定の作成{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更を行う前に、[ コンテンツ同期 ](/help/mobile/mobile-ondemand-contentsync.md) を参照して、基本的な概念を理解してください。

Adobe Experience Manager（AEM）のモバイルユーザーは、コンテンツ同期を使用して、モバイルアプリで使用するためにライブコンテンツを静的コンテンツに書き出します。この書き出しは、コンテンツがAEM Mobileから Mobile On-Demand Services にアップロードされる際に行われます。

上記の表で説明したプロパティ ***dps-exportTemplate*** は、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

次のリソースでは、AEMから共有リソースを書き出し、AEM Mobileにアップロードする方法について説明します。

共有HTMLリソースを使用すると、すべての記事で重複するHTMLリソースを記事で共有できます。アイコン、フォント、JavaScript、css を含めることができます。

**&lt;dps-exportTemplate>/dps-HTMLResources>** にあるコンテンツ同期設定は、デバイスでのプロパティ静的レンダリングに必要な記事をすべてのコンテンツにエクスポートするように設定する必要があります。

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
1. このパス *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* を参照して、サンプルの共有リソースを表示します。

   次の図に示すように、共有リソースの作成に必要なすべてのプロパティを表示できます。

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共有リソースに変化があった場合は、共有リソースをAEM Mobile On-demand Servicesにアップロードまたは書き出す必要があります。
