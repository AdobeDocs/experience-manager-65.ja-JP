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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 10%

---

# Adobe Mobile Services Cloud Service の設定 {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

この **モバイル指標タイル** コマンドセンターのを使用すると、モバイルアプリケーションのリアルタイム分析を利用できます。

この [Mobile Analytics のAdobe](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK は PhoneGap プラグインを通じて使用可能になります。 指標が収集され、デバイスに接続するまでデバイス上でキャッシュされます。接続された時点で、レポートと分析のためにデータがAdobe Mobile Services クラウドにプッシュされます。

Adobe Mobile Analytics SDK は次を提供します。

1. **モバイルチャネルのデータ収集**  – すべての主要なオペレーティングシステムでモバイル web サイトやアプリの包括的なデータを収集します。
1. **モバイルエンゲージメント分析** - モバイルアプリ、web サイトまたはビデオ内のユーザーエンゲージメントを把握します。これには、消費者がチャネルを立ち上げる頻度や、チャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリのダッシュボードとレポート** - アプリのライフサイクル指標やアプリストア指標を含んだ使用状況レポートを取得します – ユーザーのトレンド、起動数、平均セッション長、保持期間、クラッシュを確認します。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **ジオロケーション分析** - アプリのユーザーが起動する場所を見つけ、GPS の場所や目標地点によってモバイルエクスペリエンスとやり取りします。
1. **パス分析** - ユーザーがアプリ内をどのように移動して、どの画面と UI 要素がユーザーを引き付け、どの画面がユーザーを離脱させるかを決定するかを確認します。

>[!CAUTION]
>
>この **指標の分析** タイルは、クラウドサービスを設定した場合にのみ、ダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics タイル

## Cloud Serviceの設定 {#configuring-the-cloud-service}

Adobeの Mobile Services Analytics を利用するには、Adobe Analytics アカウント情報を使用してAEM Mobile Analytics Cloud サービスを設定する必要があります。

1. 右上のアイコンをクリックして、Cloud Serviceを追加 **Cloud Serviceの管理** アプリダッシュボードからタイル表示します。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. この **Cloud Serviceを追加または編集** 画面が表示されます。 を選択 **Mobile Services のAdobe** をクリックして、 **次**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 「」から既存の設定を選択 **モバイル サービス** または次を選択 **設定の作成** をクリックして作成します。

   新しい設定の場合は、 **Mobile Services プロパティ**&#x200B;をクリックして、**確認します。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   認証情報が検証された場合、 **検証** ボタンの変更先 **検証済み**. から Mobile Service アプリを選択できます **モバイルアプリサービスを選択**.

   クリック **Submit** （設定のセットアップ用）。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定を設定すると、ダッシュボードで同じ設定を表示できます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定を設定すると、以下を表示できます **指標の分析** アプリのダッシュボードでタイル表示します。

   ![chlimage_1-28](assets/chlimage_1-28.png)
