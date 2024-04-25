---
title: クラウド設定
description: オンデマンドアプリをクラウド設定に関連付けると、Adobe Experience Manager（AEM）は双方向リンクを確立することで、モバイルオンデマンドでホストされたプロジェクトと直接通信できます。 このページでは、この機能について詳しく見ていきます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 14%

---

# クラウド設定{#cloud-configuration}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

オンデマンドアプリをクラウド設定に関連付けると、Adobe Experience Manager（AEM）は双方向リンクを確立することで、モバイルオンデマンドでホストされたプロジェクトと直接通信できます。 アプリを Mobile On-Demand プロジェクトにリンクすると、AEM内で記事、バナー、コレクションなどのコンテンツ作成を実行できるだけでなく、そのコンテンツを Mobile On-Demand に提供することもできます。

ここから、コンテンツの公開、プレビューおよび管理が可能になります。 また、既存のモバイルオンデマンドコンテンツをAEMに読み込んで、コンテンツ編集を実行することもできます。

## クラウド設定のセットアップ {#setting-up-cloud-configuration}

>[!CAUTION]
>
>オンデマンドアプリ用のクラウド設定の設定を開始する前に、AEM Mobile On-demand ServicesのプロビジョニングとAEM Mobile Client の設定を理解しておく必要があります。
>
>詳しくは、を参照してください [AEM Mobile On-demand Servicesのセットアップ](/help/mobile/aem-mobile-setup.md) 「管理」セクションで以下を実行します。

モバイルオンデマンドCloud Serviceを設定するには、の右上隅にある上部の歯車をクリックします **接続を管理** アプリのダッシュボードからタイル表示します。

アプリダッシュボードと使用可能なタイルについて理解しておく必要があります。 参照： [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### クラウド設定へのリンクのセットアップ {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>既存のオンデマンドクライアントおよびクラウド設定があることを確認します。
>
>詳しくは、を参照してください [AEM Mobile On-demand Servicesのセットアップ](/help/mobile/aem-mobile-setup.md) 「管理」セクションで以下を実行します。

クラウド設定へのリンクをセットアップする手順は次のとおりです。

1. 送信元 **モバイル**、を選択 **アプリ** 次に、カタログからモバイルオンデマンドアプリを選択します。
1. の歯車アイコンをクリックします **接続を管理** タイル。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 既存の設定を入力するか、を入力して作成します。 **設定のタイトル**, **デバイス Id**、および **デバイストークン**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 1 度は **デバイス Id** および **デバイストークン** 検証済みであることを確認し、リストからオンデマンド プロジェクトを選択します。

   「**送信**」をクリックします。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   この **接続を管理** タイルにクラウド設定が表示されます。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >ダッシュボードでプロジェクトを切り替えている際に、このアプリが関連付けられているプロジェクトを変更しようとすると、次の図に示すように、コンテンツの整合性の問題に関する警告が表示されます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 次の手順 {#the-next-steps}

アプリのクラウド設定を指定したら、次のリソースを参照してコンテンツを管理します。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開/非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
