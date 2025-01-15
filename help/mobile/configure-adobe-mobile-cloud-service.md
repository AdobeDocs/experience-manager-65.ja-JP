---
title: Adobe Mobile Services Cloud Service の設定
description: このページでは、Adobeの Mobile Services をCloud Serviceします。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 6%

---

# Adobe Mobile Services Cloud Service の設定 {#configure-your-adobe-mobile-services-cloud-service}

{{ue-over-mobile}}

コマンドセンターの **モバイル指標タイル** は、モバイルアプリケーションのリアルタイム分析を提供します。

[Adobeモバイル分析 ](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html)SDKは、PhoneGap プラグインを通じて利用できるようになります。 指標が収集され、デバイスに接続するまでデバイス上でキャッシュされます。接続された時点で、レポートと分析のためにデータがAdobe Mobile Services クラウドにプッシュされます。

Adobeモバイル分析SDKには、次の機能があります。

1. **モバイルチャネルのデータ収集** – すべての主要なオペレーティングシステムでモバイル web サイトやアプリの包括的なデータを収集します。
1. **モバイルエンゲージメント分析** - モバイルアプリ、web サイトまたはビデオ内のユーザーエンゲージメントを把握します。これには、消費者がチャネルを起動する頻度や、そのチャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリダッシュボードとレポート** - アプリのライフサイクル指標やアプリストア指標を含んだ使用状況レポートを取得します。ユーザーの傾向、起動数、平均セッション長、保持期間、クラッシュを確認します。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報の分析** - アプリのユーザーが起動した場所を見つけ、GPS の場所や目標地点によってモバイルエクスペリエンスとやり取りします。
1. **パス分析** - ユーザーがアプリ内をどのように移動するかを確認し、ユーザーを引き付けている画面と UI 要素、およびユーザーが離脱する原因を特定します。

>[!CAUTION]
>
>**指標を分析** タイルは、クラウドサービスが設定されている場合にのみ、ダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics タイル

## Cloud Serviceの設定 {#configuring-the-cloud-service}

Adobeの Mobile Services Analytics を利用するには、Adobe Analytics アカウント情報を使用してAEM Mobile Analytics Cloud サービスを設定する必要があります。

1. アプリのダッシュボードの **Cloud Serviceを管理** タイルのCloud Serviceを追加または編集するには、右上のアイコンをクリックします。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. **Cloud Serviceを追加または編集** 画面が表示されます。 「**AdobeMobile Services**」を選択し、「**次へ** をクリックします。

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. **Mobile Services** から既存の設定を選択するか、「**設定を作成**」を選択して設定を作成します。

   新しい設定の場合は、「**Mobile Services プロパティ** を入力し、「確認 **」をクリックします。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   資格情報が検証された場合、「**検証**」ボタンが **検証済み** に変わります。 **モバイルアプリサービスを選択** からモバイルサービスアプリを選択できます。

   **送信** をクリックして、設定をセットアップします。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定を設定すると、ダッシュボードで同じ設定を表示できます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定を設定したら、アプリダッシュボードで **指標を分析** タイルを表示できます。

   ![chlimage_1-28](assets/chlimage_1-28.png)
