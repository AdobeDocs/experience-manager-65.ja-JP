---
title: Adobe Mobile Services クラウドサービスの設定
seo-title: Adobe Mobile Services クラウドサービスの設定
description: このページでは、Adobe Mobile Services クラウドサービスの設定について説明します。
seo-description: このページでは、Adobe Mobile Services クラウドサービスの設定について説明します。
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe Mobile Services クラウドサービスの設定 {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

The **Mobile Metrics Tile** on the command center provides real-time analytics for your mobile application.

[Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK は、PhoneGap プラグインを通じて使用できます。指標は、デバイスが接続されるまでデバイス上で収集およびキャッシュされ、その時点でデータがAdobe Mobile Services cloudにプッシュされ、レポートおよび分析されます。

Adobe Mobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルに関するデータ収集** - すべての主要オペレーティングシステム上のモバイル Web サイトおよびアプリに関して総合的なデータを収集します。
1. **モバイルエンゲージメント分析** — ユーザーがチャネルを起動する頻度、チャネルから購入するかどうかなど、モバイルアプリ、Webサイト、ビデオ内でのユーザーエンゲージメントを把握します。
1. **モバイルアプリのダッシュボードとレポート** — アプリとアプリストアの指標に関するライフサイクル指標を含む使用状況レポートを取得できます。 ユーザー、起動回数、セッションの平均長さ、リテンション期間、クラッシュ回数の傾向を確認します。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QRコードなど、モバイル専用のキャンペーンの効果を定量化します。
1. **位置情報分析** — アプリのユーザーが起動し、GPSの位置や目標地点でモバイルエクスペリエンスを操作する場所を探します。
1. **パス分析** — ユーザーがアプリ内をどのように移動して、ユーザーを惹きつける画面やUI要素、およびユーザーをドロップオフにさせる要因を特定するかを確認します。

>[!CAUTION]
>
>**指標を分析**&#x200B;タイルは、クラウドサービスを設定している場合にのみダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM コマンドセンター指標タイル

## クラウドサービスの設定 {#configuring-the-cloud-service}

Adobe Mobile Services 分析を利用するには、Adobe Analytics アカウント情報を使用して AEM Mobile Analytics クラウドサービスを設定する必要があります。

1. Click on the top right hand side icon to add or edit the Cloud Services from the **Manage Cloud Services** tile from the app dashboard.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. The **Add or Edit Cloud Services** screen displays. Select **Adobe Mobile Services** and click **Next**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Choose an existing configuration from the **Mobile Services** or choose **Create Configuration** to create a new one.

   新しい設定で、「**Mobile Services のプロパティ**」を入力し、「**検証**」をクリックします。

   ![chlimage_1-25](assets/chlimage_1-25.png)

   If the credentials are verified, the **Verify** button changes to **Verified**. 「**Mobile Services アプリを選択**」から Mobile Services アプリを選択できます。

   Click **Submit** for setting up your configuration.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定をおこなったら、ダッシュボードで設定を表示できます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定をおこなったら、アプリダッシュボードの&#x200B;**指標を分析**&#x200B;タイルを表示できます。

   ![chlimage_1-28](assets/chlimage_1-28.png)

