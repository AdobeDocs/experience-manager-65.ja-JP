---
title: クラウド設定
seo-title: Cloud Configuration
description: On-Demand アプリをクラウド設定に関連付けると、Adobe Experience Manager(AEM) は双方向リンクを確立することで、Mobile On-Demand がホストするプロジェクトと直接通信できます。 このページでは、この機能について詳しく見ていきます。
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 8%

---

# クラウド設定{#cloud-configuration}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

On-Demand アプリをクラウド設定に関連付けると、Adobe Experience Manager(AEM) は双方向リンクを確立することで、Mobile On-Demand がホストするプロジェクトと直接通信できます。 アプリを Mobile On-Demand プロジェクトにリンクすることで、AEM内で記事、バナー、コレクションなどのコンテンツ作成を実行できるだけでなく、そのコンテンツを Mobile On-Demand に提供することができます。

ここから、コンテンツの公開、プレビュー、管理が可能になります。 また、既存の Mobile On-Demand コンテンツをAEMに読み込み、コンテンツ編集を実行することもできます。

## クラウド設定のセットアップ {#setting-up-cloud-configuration}

>[!CAUTION]
>
>On-Demand アプリ用のクラウド設定を開始する前に、AEM MobileのプロビジョニングとAEM Mobile On-demand Services Client の設定に関する知識が必要です。
>
>詳しくは、 [AEM Mobile On-demand Servicesの設定](/help/mobile/aem-mobile-setup.md) （管理の節）を参照してください。

Mobile On-DemandCloud Serviceを設定するには、 **接続を管理** タイルをアプリダッシュボードから削除します。

アプリダッシュボードと使用可能なタイルについて理解している必要があります。 詳しくは、 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### クラウド設定へのリンクの設定 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>既存の On-Demand クライアントおよびクラウド設定があることを確認します。
>
>詳しくは、 [AEM Mobile On-demand Servicesの設定](/help/mobile/aem-mobile-setup.md) （管理の節）を参照してください。

次の手順で、クラウド設定へのリンクを設定します。

1. 送信者 **モバイル**&#x200B;を選択します。 **アプリ** 次に、カタログから Mobile On-Demand アプリを作成します。
1. の歯車アイコンをクリックします。 **接続を管理** タイル。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 既存の設定を入力するか、 **設定のタイトル**, **デバイス ID**、および **デバイストークン**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 一度、 **デバイス ID** および **デバイストークン** が検証されている場合は、リストから On-Demand プロジェクトを選択します。

   「**送信**」をクリックします。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   The **接続を管理** タイルにクラウド設定が表示されます。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >このアプリが関連付けられているプロジェクトを変更しようとすると、ダッシュボードでプロジェクトを切り替える際に、次の図に示すように、コンテンツの整合性に関する警告が表示されます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 次の手順 {#the-next-steps}

アプリのクラウド設定を完了したら、次のコンテンツ管理リソースを参照してください。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開/非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
