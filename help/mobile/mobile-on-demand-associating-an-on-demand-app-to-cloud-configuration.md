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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 9%

---

# クラウド設定{#cloud-configuration}

{{ue-over-mobile}}

オンデマンドアプリをクラウド設定に関連付けると、Adobe Experience Manager（AEM）は双方向リンクを確立することで、モバイルオンデマンドでホストされたプロジェクトと直接通信できます。 アプリを Mobile On-Demand プロジェクトにリンクすると、AEM内で記事、バナー、コレクションなどのコンテンツ作成を実行できるだけでなく、そのコンテンツを Mobile On-Demand に提供することもできます。

ここから、コンテンツの公開、プレビューおよび管理が可能になります。 また、既存のモバイルオンデマンドコンテンツをAEMに読み込んで、コンテンツ編集を実行することもできます。

## クラウド設定のセットアップ {#setting-up-cloud-configuration}

>[!CAUTION]
>
>オンデマンドアプリ用のクラウド設定の設定を開始する前に、AEM Mobile On-demand ServicesのプロビジョニングとAEM Mobile Client の設定を理解しておく必要があります。
>
>詳しくは、管理の節の [AEM Mobile On-demand Servicesの設定 &#x200B;](/help/mobile/aem-mobile-setup.md) を参照してください。

モバイルオンデマンドCloud Serviceを行うには、アプリのダッシュボードで **接続を管理** タイルの右上隅にある上部の歯車をクリックします。

アプリダッシュボードと使用可能なタイルについて理解しておく必要があります。 詳しくは、[AEM Mobile アプリケーションダッシュボード &#x200B;](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### クラウド設定へのリンクのセットアップ {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>既存のオンデマンドクライアントおよびクラウド設定があることを確認します。
>
>詳しくは、管理の節の [AEM Mobile On-demand Servicesの設定 &#x200B;](/help/mobile/aem-mobile-setup.md) を参照してください。

クラウド設定へのリンクをセットアップする手順は次のとおりです。

1. **モバイル** から「**アプリ**」を選択し、カタログからモバイルオンデマンドアプリを選択します。
1. **接続を管理** タイルの歯車アイコンをクリックします。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 既存の設定を入力するか、**設定タイトル**、**デバイス ID**、**デバイストークン** を入力して設定を作成します。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. **デバイス ID** と **デバイストークン** の検証が完了したら、リストからオンデマンドプロジェクトを選択します。

   「**送信**」をクリックします。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **接続を管理** タイルに、クラウド設定が表示されます。

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
