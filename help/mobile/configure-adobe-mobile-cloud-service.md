---
title: Adobe Mobile Services Cloud Service の設定
seo-title: Configure your Adobe Mobile Services Cloud Service
description: このページでは、Mobile Services のAdobeCloud Serviceを設定します。
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Adobe Mobile Services Cloud Service の設定 {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

この **モバイル指標タイル** コマンドセンターでは、モバイルアプリケーションのリアルタイム分析を提供します。

この [Adobeモバイル分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK は、PhoneGap プラグインを通じて使用できるようになります。 指標は、デバイスが接続されるまで収集され、デバイス上でキャッシュされます。その時点で、データがAdobeの Mobile Services クラウドにプッシュされ、レポートと分析がおこなわれます。

AdobeMobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルのデータ収集**  — すべての主要なオペレーティングシステム上のモバイル Web サイトやアプリの包括的なデータを収集します。
1. **モバイルエンゲージメント分析**  — モバイルアプリ、Web サイトまたはビデオ内でのユーザーエンゲージメントを把握します。これには、消費者がチャネルを起動する頻度、チャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリのダッシュボードとレポート**  — アプリやアプリストア指標のライフサイクル指標を含む使用状況レポートを取得します。ユーザー、起動回数、平均セッション長、リテンション長、クラッシュ回数のトレンドを確認できます。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報分析**  — アプリのユーザーが起動した場所や、GPS の位置や目標地点によってモバイルエクスペリエンスとやり取りする場所を特定します。
1. **パス分析**  — ユーザーがアプリ内をどのように移動して、ユーザーを引き付けている画面や UI 要素を特定し、ユーザーをドロップオフにさせるかを確認します。

>[!CAUTION]
>
>この **指標を分析** タイルは、クラウドサービスを設定済みの場合にのみ、ダッシュボードに表示されます。

![chlimage_1-22](assets/chlimage_1-22.png)

AEMコマンドセンター指標タイル

## Cloud Service {#configuring-the-cloud-service}

Mobile Services Analytics を活用するには、AEM Mobile Analytics CloudAdobeをAdobe Analyticsアカウント情報で設定する必要があります。

1. 右上のアイコンをクリックして、「 **Cloud Services** タイルをアプリダッシュボードから削除します。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. この **追加または編集Cloud Services** 画面が表示されます。 選択 **AdobeMobile Services** をクリックし、 **次へ**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 既存の設定を **Mobile Services** または選択 **設定を作成** 新しいものを作成するには

   新しい設定の場合は、 **Mobile Services プロパティ**&#x200B;をクリックし、**確認します。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   認証情報が検証された場合、 **検証** ボタンの変更 **検証済み**. 次の中からモバイルサービスアプリを選択できます。 **モバイルアプリサービスを選択**.

   クリック **送信** を参照してください。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. クラウド設定をセットアップすると、ダッシュボードにも同じ設定が表示されます。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >クラウド設定を行うと、 **指標を分析** アプリダッシュボードにタイルを表示します。

   ![chlimage_1-28](assets/chlimage_1-28.png)
