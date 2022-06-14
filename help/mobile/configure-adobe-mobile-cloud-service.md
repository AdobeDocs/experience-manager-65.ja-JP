---
title: Adobe Mobile Services Cloud Service の設定
seo-title: Configure your Adobe Mobile Services Cloud Service
description: このページでは、Adobe Mobile Services クラウドサービスの設定について説明します。
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 43%

---

# Adobe Mobile Services Cloud Service の設定 {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

この **モバイル指標タイル** コマンドセンターでは、モバイルアプリケーションのリアルタイム分析を提供します。

[Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK は、PhoneGap プラグインを通じて使用できます。指標は、デバイスが接続されるまで収集され、デバイス上でキャッシュされます。その時点で、データがAdobeの Mobile Services クラウドにプッシュされ、レポートと分析がおこなわれます。

Adobe Mobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルに関するデータ収集** - すべての主要オペレーティングシステム上のモバイル Web サイトおよびアプリに関して総合的なデータを収集します。
1. **モバイルエンゲージメント分析**  — モバイルアプリ、Web サイトまたはビデオ内でのユーザーエンゲージメントを把握します。これには、消費者がチャネルを起動する頻度、チャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリのダッシュボードとレポート**  — アプリやアプリストア指標のライフサイクル指標を含む使用状況レポートを取得します。ユーザー、起動回数、平均セッション長、リテンション長、クラッシュ回数のトレンドを確認できます。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報分析**  — アプリのユーザーが起動した場所や、GPS の位置や目標地点によってモバイルエクスペリエンスとやり取りする場所を特定します。
1. **パス分析**  — ユーザーがアプリ内をどのように移動して、ユーザーを引き付けている画面や UI 要素を特定し、ユーザーをドロップオフにさせるかを確認します。

>[!CAUTION]
>
>**指標を分析**&#x200B;タイルは、クラウドサービスを設定している場合にのみダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM コマンドセンター指標タイル

## クラウドサービスの設定 {#configuring-the-cloud-service}

Adobe Mobile Services 分析を利用するには、Adobe Analytics アカウント情報を使用して AEM Mobile Analytics クラウドサービスを設定する必要があります。

1. 右上のアイコンをクリックして、「 **Cloud Services** タイルをアプリダッシュボードから削除します。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. この **追加または編集Cloud Services** 画面が表示されます。 選択 **AdobeMobile Services** をクリックし、 **次へ**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 既存の設定を **Mobile Services** または選択 **設定を作成** 新しいものを作成するには

   新しい設定で、「**Mobile Services のプロパティ**」を入力し、「**検証**」をクリックします。

   ![chlimage_1-25](assets/chlimage_1-25.png)

   認証情報が検証された場合、 **検証** ボタンの変更 **検証済み**. 「**Mobile Services アプリを選択**」から Mobile Services アプリを選択できます。

   クリック **送信** を参照してください。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定をおこなったら、ダッシュボードで設定を表示できます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定をおこなったら、アプリダッシュボードの&#x200B;**指標を分析**&#x200B;タイルを表示できます。

   ![chlimage_1-28](assets/chlimage_1-28.png)
