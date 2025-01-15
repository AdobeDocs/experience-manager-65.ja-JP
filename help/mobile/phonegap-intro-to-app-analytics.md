---
title: Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング
description: Adobeモバイルサービスを使用すると、モバイルアプリの使用状況、アプリのクラッシュ回数、デバイスの詳細など、モバイルアプリに関する多くの重要な指標をトラッキングして、ユーザーがモバイルアプリをどのように使用しているかに関するインサイトを得ることができます。 このページでは、この機能について詳しく見ていきます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 3%

---

# Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング{#track-app-performance-with-adobe-mobile-analytics}

{{ue-over-mobile}}

顧客コンバージョンとロイヤルティを高める必要があります。

顧客に関連性が高く魅力的なエクスペリエンスを提供したいと考えています。

AEM Mobile アプリはマーケティングキャンペーンに対して何を行っていますか？

ユーザーに最適なエクスペリエンスを提供するために、モバイルアプリケーションを微調整するにはどうすればよいですか？

Adobeモバイルサービスを使用すると、モバイルアプリの使用状況、アプリのクラッシュ回数、デバイスの詳細など、モバイルアプリに関する多くの重要な指標をトラッキングして、ユーザーがモバイルアプリをどのように使用しているかに関するインサイトを得ることができます。

Adobe Experience Manager Mobileでは、AEM Mobile アプリケーションダッシュボードから直接モバイル分析の詳細を確認できます。 ダッシュボードの **モバイル指標タイル** には、モバイルアプリケーションのReal-Time Analyticsが表示され、開発者、作成者および管理者がモバイルアプリの正常性を簡単に確認できます。 カバーの下で、分析の機能を強化するのは、[AdobeMobile Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html)SDKです。 Adobe Mobile Analytics SDKは、ネイティブで、または Web ビュー用 PhoneGap Bridge プラグインを通じてアプリケーションにプラグインできます。 指標が収集され、デバイスが接続されるまでデバイス上でキャッシュされます。接続された時点で、レポートと分析のためにデータがAdobe Mobile Services Cloud にプッシュされます。

Adobeモバイル分析SDKには、次の機能があります。

1. **モバイルチャネルのデータ収集** – すべての主要なオペレーティングシステムでモバイル web サイトやアプリの包括的なデータを収集します。
1. **モバイルエンゲージメント分析** - モバイルアプリ、web サイトまたはビデオ内のユーザーエンゲージメントを把握します。これには、消費者がチャネルを起動する頻度や、そのチャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリダッシュボードとレポート** - アプリのライフサイクル指標やアプリストア指標を含んだ使用状況レポートを取得します。ユーザーの傾向、起動数、平均セッション長、保持期間、クラッシュを確認します。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報の分析** - アプリのユーザーが起動した場所を見つけ、GPS の場所や目標地点によってモバイルエクスペリエンスとやり取りします。
1. **パス分析** - ユーザーがアプリ内をどのように移動するかを確認し、ユーザーを引き付けている画面と UI 要素、およびユーザーが離脱する原因を特定します。

この節では、[Analytics Developers](#developers) でAEM トラッキングを使用してAEM Mobile アプリを実装する方法について説明します。

最後に、[AEM管理者は次の ](#administrators) とを学習します。

* mobile Services をAdobeにするクラウドサービスの作成
* モバイルサービス設定の作成とレポートスイートの関連付け
* モバイルサービス設定のモバイルアプリへの関連付け
* AEM Apps Command Center を使用した指標の表示
* ams SDK設定のモバイルアプリへの割り当て

## 開発者向け – Analytics のアプリへの統合 {#for-developers-integrate-analytics-into-your-app}

**前提条件：** AEM管理者は、（以下で説明するように [Mobile Services Adobeのクラウド設定を行う必要があり ](#amscloudserviceconfig) す。

デベロッパーは、必要に応じて [AEM Mobile アプリに分析を追加 ](/help/mobile/phonegap-add-analytics-to-apps.md) し、モバイルアプリのコンテンツに対するユーザーのエンゲージメントを追跡、レポートおよび理解し、ローンチ、アプリ内時間、クラッシュ率などの主要ライフサイクル指標を測定する責任があります。

## 管理者向け – Adobe Mobile Services のCloud Serviceを設定します {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Adobeの Mobile Services を活用するには、AEM Adobeの Mobile Services 設定にAdobe Analytics アカウント情報をCloud Serviceする必要があります。 Apps コマンドセンターには「**指標を分析**」タイルがあり、クラウドサービスを作成してモバイルアプリに関連付けることができます。

モバイルアプリに Cloud Service を設定するには、まず「指標を分析」タイルの歯車アイコンをクリックします。

![chlimage_1-125](assets/chlimage_1-125.png)

指標を分析タイルの歯車アイコンをクリックすると、「Mobile Services Analytics の設定」モーダルダイアログが開きます。 「Mobile Service 設定を選択」ドロップダウンから設定を選択します。 設定を作成する必要がある場合は、レンチ ボタンをクリックします。

AdobeMobile Service Cloud Service を作成するには、サービスに接続する手順と、設定に割り当てるレポートスイートを選択する手順の 2 つが必要です。

開始するには、ダッシュボードのCloud Serviceを管理タイルの「+」ボタンをクリックします。

![chlimage_1-126](assets/chlimage_1-126.png)

「**+**」ボタンをクリックすると、「Cloud Serviceを追加 **ウィザードが表示さ** ます。

![chlimage_1-127](assets/chlimage_1-127.png)

以下に示すように、必須フィールドに入力して、モバイルサービス設定を選択または作成します。 Adobe Mobile Services への接続を正しく確立するには、AEM管理者がこの情報を必要とします。

![chlimage_1-128](assets/chlimage_1-128.png)

Mobile Services アカウントの設定が完了したら、アプリを選択するように求められます。 これにより、Adobeの Mobile Service 分析レポートがそのアプリケーションに接続されます。

目的のモバイルサービスを選択し、「更新」をクリックしてモバイルサービス設定を割り当て、ダイアログを閉じます。

これで、モバイルサービス設定をAEM Mobile アプリに関連付けたので、タイルを開始して指標データを取得し、レポートを開始します。

![chlimage_1-129](assets/chlimage_1-129.png)

### Mobile Services SDKAdobeファイル {#adobe-mobile-services-sdk-config-file}

この時点では、モバイルアプリケーションは Cloud Service に関連付けられていますが、収集したモバイル指標をAdobe Analyticsに送り返す方法がまだモバイルアプリケーションにわかっていません。 モバイルアプリをAdobe Analyticsにワイヤアップするには、Adobe Mobile Services SDK設定ファイルをAdobe Experience Managerに追加する必要があります。

「指標を分析」タイルから、矢印アイコンをクリックして、「AMS SDK設定のダウンロード/アップロード」メニューエントリを表示します。

![chlimage_1-130](assets/chlimage_1-130.png)

最初の手順では、Adobe Mobile Services からSDK設定を取得します。 「AMS SDK設定をダウンロード」をクリックして、設定ファイルをダウンロードできるAdobe Mobile Services web サイトにリダイレクトします。 ADBMobileConfig.json ファイルを取得したら、「Upload AMS SDK Config」をクリックして、設定ファイルをAEMにアップロードします。

![chlimage_1-131](assets/chlimage_1-131.png)

「Adobe Mobile Services Application Config をアップロード」ボタンをクリックして、ADBMobileConfig.json ファイルを参照し、「アップロード」をクリックします。

モバイルアプリが ADBMobileConfig.json ファイルにアクセスできるようになったので、Adobe Analyticsに戻って通信し、アプリの成功を促す重要な指標値のレポートを開始する方法に関する知識が得られました。

## 次の手順 {#what-s-next}

1. [AEM Mobile アプリのエクスペリエンスを開始](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツの管理](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションの構築](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobeモバイル分析を使用してアプリのパフォーマンスを追跡する](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Targetでパーソナライズされたアプリエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [ユーザーへの重要なメッセージの送信](/help/mobile/phonegap-push-notifications.md)
