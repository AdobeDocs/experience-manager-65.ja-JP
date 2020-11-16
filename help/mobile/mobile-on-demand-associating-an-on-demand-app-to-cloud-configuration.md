---
title: クラウド設定
seo-title: クラウド設定
description: On-Demand アプリをクラウド設定に関連付けることで、Adobe Experience Manager（AEM）は、双方向のリンクを確立し、Mobile On-Demand にホストされたプロジェクトと直接通信できます。このページでは、この機能について詳しく見ていきます。
seo-description: On-Demand アプリをクラウド設定に関連付けることで、Adobe Experience Manager（AEM）は、双方向のリンクを確立し、Mobile On-Demand にホストされたプロジェクトと直接通信できます。このページでは、この機能について詳しく見ていきます。
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 86%

---


# クラウド設定{#cloud-configuration}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

On-Demand アプリをクラウド設定に関連付けることで、Adobe Experience Manager（AEM）は、双方向のリンクを確立し、Mobile On-Demand にホストされたプロジェクトと直接通信できます。アプリを Mobile On-Demand プロジェクトにリンクすることにより、記事、バナー、コレクションなどのコンテンツの作成を AEM 内で実行できるだけでなく、そのコンテンツを Mobile On-Demand に提供できます。

そこからコンテンツの公開、プレビュー、管理をおこなえます。また、既存の Mobile On-Demand コンテンツを AEM に読み込み、コンテンツの編集をおこなうこともできます。

## クラウド設定の実行 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>On-Demandアプリのクラウド設定を開始する前に、「AEM MobileプロビジョニングとAEM Mobile On-demand Servicesクライアントの設定」を理解しておく必要があります。
>
>For details, See [Setting up AEM Mobile On-Demand Services](/help/mobile/aem-mobile-setup.md) in the Administering section.

Mobile On-Demand クラウドサービスを設定するには、アプリダッシュボードの&#x200B;**接続を管理**&#x200B;タイルの右上隅にある歯車をクリックします。

アプリダッシュボードや、利用できるタイルについて理解している必要があります。詳しくは、[AEM Mobile アプリケーションダッシュボード](/help/mobile/mobile-apps-ondemand-application-dashboard.md)を参照してください。

### クラウド設定へのリンクの設定 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>On-Demand クライアントおよびクラウドを設定済みであることを確認します。
>
>For details, See [Setting up AEM Mobile On-Demand Services](/help/mobile/aem-mobile-setup.md) in the Administering section.

以下に、クラウド設定へのリンクの設定手順について説明します。

1. 「**モバイル**」で「**アプリ**」を選択し、カタログから Mobile On-Demand アプリを選択します。
1. Click the gear icon on the **Manage Connection** tile.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 既存の設定を入力するか、「**設定のタイトル**」、「**デバイス ID**」および「**デバイストークン**」を入力して新しい設定を作成します。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 「**デバイス ID**」および「**デバイストークン**」を確認したら、リストから On-Demand プロジェクトを選択します。

   「**送信**」をクリックします。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **接続を管理**&#x200B;タイルにクラウド設定が表示されます。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >ダッシュボードでプロジェクトを切り替え、このアプリを関連付けるプロジェクトを変更しようとすると、以下のようにコンテンツの整合性の問題についての警告が表示されます。

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 次の手順 {#the-next-steps}

アプリのクラウド設定が完了したら、コンテンツの管理について以下のリソースを参照してください。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
