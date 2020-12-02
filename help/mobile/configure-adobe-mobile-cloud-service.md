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
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 45%

---


# Adobe Mobile Services クラウドサービスの設定  {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

コマンドセンターの&#x200B;**モバイル指標タイル**&#x200B;は、モバイルアプリケーションのリアルタイム分析を提供します。

[Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK は、PhoneGap プラグインを通じて使用できます。指標は収集され、デバイスに接続されるまでデバイス上にキャッシュされます。接続されると、データはAdobeのMobile Services Cloudにプッシュされ、レポートと分析が行われます。

Adobe Mobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルに関するデータ収集** - すべての主要オペレーティングシステム上のモバイル Web サイトおよびアプリに関して総合的なデータを収集します。
1. **モバイルエンゲージメントの分析**  — ユーザーがモバイルアプリ、Webサイトまたはビデオ内で行うエンゲージメントを把握します。例えば、チャネルを起動する頻度や、消費者がアプリから購入するかどうかなどを把握できます。
1. **モバイルアプリのダッシュボードとレポート**  — アプリやアプリストアの指標のライフサイクル指標を含む使用状況レポートを取得します。ユーザー、起動回数、セッションの平均長さ、リテンション期間、クラッシュの傾向を確認できます。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QRコードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報分析**  — アプリのユーザーが起動し、GPSの位置や目標地点でモバイルエクスペリエンスを操作する場所を探します。
1. **パス分析**  — ユーザーがアプリ内をどのように移動して、ユーザーを惹きつける画面やUI要素、およびユーザーの離脱の原因を特定するかを確認します。

>[!CAUTION]
>
>**指標を分析**&#x200B;タイルは、クラウドサービスを設定している場合にのみダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM コマンドセンター指標タイル

## クラウドサービスの設定  {#configuring-the-cloud-service}

Adobe Mobile Services 分析を利用するには、Adobe Analytics アカウント情報を使用して AEM Mobile Analytics クラウドサービスを設定する必要があります。

1. 右上のアイコンをクリックし、アプリダッシュボードの&#x200B;**Cloud Servicesの管理**&#x200B;タイルからCloud Servicesを追加または編集します。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. **追加またはCloud Servicesを編集**&#x200B;画面が表示されます。 「**AdobeMobile Services**」を選択し、「**次へ**」をクリックします。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. **Mobile Services**&#x200B;から既存の設定を選択するか、**設定を作成**&#x200B;を選択して新しい設定を作成します。

   新しい設定で、「**Mobile Services のプロパティ**」を入力し、「**検証**」をクリックします。

   ![chlimage_1-25](assets/chlimage_1-25.png)

   秘密鍵証明書が検証されると、「**検証**」ボタンが「**検証済み**」に変わります。 「**Mobile Services アプリを選択**」から Mobile Services アプリを選択できます。

   「**送信**」をクリックして設定を行います。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定をおこなったら、ダッシュボードで設定を表示できます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定をおこなったら、アプリダッシュボードの&#x200B;**指標を分析**&#x200B;タイルを表示できます。

   ![chlimage_1-28](assets/chlimage_1-28.png)

