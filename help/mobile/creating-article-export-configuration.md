---
title: 記事のエクスポート設定の作成
description: このページでは、Adobe Experience Manager（AEM）からコンテンツを書き出し、AEM Mobileにアップロードする方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 3%

---

# 記事のエクスポート設定の作成{#creating-article-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**前提条件**:
>
>共有リソースの作成と変更について学ぶ前に、[&#x200B; コンテンツ同期 &#x200B;](/help/mobile/mobile-ondemand-contentsync.md) を参照して、基本的な概念を理解してください。

AEM Mobile ユーザーはコンテンツ同期を使用して、モバイルアプリで使用するためにライブコンテンツを静的コンテンツに書き出します。この書き出しは、コンテンツがAEM Mobileから Mobile On-Demand Services にアップロードされる際に行われます。

上記の表で説明したプロパティ ***dps-exportTemplate*** は、アプリの書き出し設定へのパスを定義します。 共有リソースを作成および変更するには、このプロパティを設定します。

以下のリソースでは、AEM MobileにアップロードするためにAdobe Experience Manager（AEM）からコンテンツを書き出す方法について説明します。

記事には、書き出しとアップロードが必要なコンテンツがあります。 このコンテンツの一部は、記事間で共有できます。

[ContentSync](/help/mobile/mobile-ondemand-contentsync.md) を使用してコンテンツを収集し、***共有リソース*** パッケージを作成します。

**&lt;dps-exportTemplate>/dps-article>** にある ContentSync 設定は、デバイスでのプロパティの静的レンダリングに必要な記事をすべてのコンテンツにエクスポートするように設定する必要があります。

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
1. このパス [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article) を参照して、サンプルの共有リソースを表示します。

   次の図に示すように、共有リソースの作成に必要なすべてのプロパティを表示できます。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>アーティクルは、アーティクルのコンテンツが変更されたときに、AEM Mobile On-demand Servicesにアップロードまたはエクスポートしてください。
