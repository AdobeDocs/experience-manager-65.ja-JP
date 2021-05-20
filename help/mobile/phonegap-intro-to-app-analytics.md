---
title: Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング
seo-title: Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング
description: Adobe Mobile Services では、使用状況、アプリのクラッシュ、デバイスの詳細など、モバイルアプリの数ある重要な指標をトラッキングすることで、ユーザーがモバイルアプリをどのように使用しているかを把握できます。このページでは、この機能について詳しく見ていきます。
seo-description: Adobe Mobile Services では、使用状況、アプリのクラッシュ、デバイスの詳細など、モバイルアプリの数ある重要な指標をトラッキングすることで、ユーザーがモバイルアプリをどのように使用しているかを把握できます。このページでは、この機能について詳しく見ていきます。
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 58%

---


# Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

顧客コンバージョンおよびロイヤルティを高めたいと考えています。

顧客に関連性の高い魅力的なエクスペリエンスを提供したい。

マーケティングキャンペーンにおいて AEM Mobile アプリはどのような役割を果たしていますか。

ユーザーに最適なエクスペリエンスを提供するために、どのようにモバイルアプリケーションを微調整できますか。

Adobe Mobile Services では、使用状況、アプリのクラッシュ、デバイスの詳細など、モバイルアプリの数ある重要な指標をトラッキングすることで、ユーザーがモバイルアプリをどのように使用しているかを把握できます。

Adobe Experience Manager Mobile では、AEM Mobile アプリケーションダッシュボードから直接モバイル分析の詳細を一目で確認できます。ダッシュボードの&#x200B;**モバイル指標タイル**&#x200B;は、モバイルアプリケーションのリアルタイム分析を提供し、開発者、作成者、管理者がモバイルアプリの状態をすばやく把握できます。 分析を支えるカバーの下には、[Adobeモバイル分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDKがあります。 AdobeのMobile Analytics SDKは、ネイティブで、またはWebビュー用のPhoneGapブリッジプラグインを通じて、アプリケーションにプラグインできます。 指標は、デバイスが接続されるまで収集され、デバイスにキャッシュされます。データは、レポートや分析のためにMobile Services Cloudにプッシュされます。

Adobe Mobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルに関するデータ収集** - すべての主要オペレーティングシステム上のモバイル Web サイトおよびアプリに関して総合的なデータを収集します。
1. **モバイルエンゲージメント分析**  — 消費者がチャネルを起動する頻度や、チャネルから購入するかどうかなど、モバイルアプリ、Webサイトまたはビデオ内でのユーザーエンゲージメントを把握します。
1. **モバイルアプリのダッシュボードとレポート**  — アプリとアプリストアの指標のライフサイクル指標を含む使用状況レポートを取得します。ユーザー、起動回数、平均セッション長、リテンション期間、クラッシュの傾向を確認します。
1. **モバイルキャンペーン分析**  - SMS、モバイル検索広告、モバイルディスプレイ広告、QRコードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報分析**  - GPSの位置または目標地点によって、アプリユーザーがどこで起動し、モバイルエクスペリエンスとやり取りするかを見つけます。
1. **パス分析**  — ユーザーがアプリ内をどのように移動して、ユーザーを引き付けている画面やUI要素、およびユーザーをドロップオフにさせる要素を特定するかを確認します。

この節では、[AEM Developers](#developers)がAEM Mobileアプリに分析トラッキングを実装する方法を説明します。

最後に、[AEM Administrators](#administrators)は次のことを学習します。

* Adobe Mobile Services に対するクラウドサービスを作成します。
* モバイルサービス設定を作成し、レポートスイートを関連付けます。
* モバイルアプリにモバイルサービス設定を関連付けます。
* AEM アプリケーションコマンドセンターで指標を表示します。
* モバイルアプリに AMS SDK 設定を割り当てます。

## 開発者向け - アプリへの Analytics の統合  {#for-developers-integrate-analytics-into-your-app}

**前提条件：** AEM管理者は、以下の説明に従って、Mobile ServicesクラウドAdobeを設定す [る必要があります](#amscloudserviceconfig)。

開発者は、必要に応じて[AEM Mobileアプリ](/help/mobile/phonegap-add-analytics-to-apps.md)に分析を追加し、モバイルアプリコンテンツとの関わり方を追跡、レポート、理解し、起動回数、アプリ内時間、クラッシュ率などの主要なライフサイクル指標を測定します。

## 管理者向け - Adobe Mobile Services クラウドサービスの設定 {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Mobile Servicesを利用するには、Adobe AnalyticsのAdobe情報を使用してAEMAdobeMobile ServicesCloud Serviceを設定する必要があります。 アプリコマンドセンターには、クラウドサービスを作成してモバイルアプリに関連付けるための&#x200B;**指標の分析**&#x200B;タイルが用意されています。

モバイルアプリにクラウドサービスを設定するには、まず、指標を分析タイルにある歯車アイコンをクリックします。

![chlimage_1-125](assets/chlimage_1-125.png)

指標を分析タイルで歯車アイコンをクリックすると、Mobile Services 分析を設定モーダルダイアログが開きます。「Mobile Service設定を選択」ドロップダウンから設定を選択します。 新しい設定を作成する必要がある場合は、設定ボタンをクリックします。

Adobe Mobile Services クラウドサービスを作成するには、サービスに接続することと、設定に割り当てるレポートスイートを選択することの 2 つの手順が必要です。

まず、ダッシュボードのクラウドサービスを管理タイルで + ボタンをクリックします。

![chlimage_1-126](assets/chlimage_1-126.png)

「**+**」ボタンをクリックすると、**Cloud Serviceの追加**&#x200B;ウィザードが表示されます。

![chlimage_1-127](assets/chlimage_1-127.png)

モバイルサービス設定を選択するか、または次のように必須フィールドに入力して新規モバイルサービス設定を作成します。AEM管理者がMobile Servicesへの接続を正常に作成するには、この情報が必要になります。

![chlimage_1-128](assets/chlimage_1-128.png)

Mobile Services アカウント設定が完了したら、アプリを選択するように求められます。これにより、AdobeMobile Service分析レポートがそのアプリケーションに接続されます。

目的のモバイルサービスを選択し、「更新」をクリックしてモバイルサービス設定を割り当ててから、ダイアログを閉じます。

AEM Mobile アプリにモバイルサービス設定を関連付けたので、タイルによって指標データの取得とレポートの作成が開始されます。

![chlimage_1-129](assets/chlimage_1-129.png)

### Adobe Mobile Services SDK 設定ファイル {#adobe-mobile-services-sdk-config-file}

この時点で、モバイルアプリケーションはクラウドサービスに関連付けられていますが、収集されたモバイル指標を Adobe Analytics に通信する方法をまだ認識していません。モバイルアプリをAdobe Analyticsにワイヤアップするには、AdobeMobile Services SDK設定ファイルをAdobe Experience Managerに追加する必要があります。

指標を分析タイルから、矢印アイコンをクリックして「AMS SDK 設定をダウンロード」または「AMS SDK 設定をアップロード」メニューエントリを表示します。

![chlimage_1-130](assets/chlimage_1-130.png)

最初の手順では、Adobe Mobile Services から SDK 設定を取得します。「AMS SDK 設定をダウンロード」をクリックすると、設定ファイルをダウンロードできる Adobe Mobile Services の Web サイトにリダイレクトされます。ADBMobileConfig.jsonファイルを取得したら、「AMS SDK設定をアップロード」をクリックして、設定ファイルをAEMにアップロードします。

![chlimage_1-131](assets/chlimage_1-131.png)

「Adobe Mobile Services アプリ設定をアップロード」ボタンをクリックし、ADBMobileConfig.json ファイルを参照し、「アップロード」をクリックします。

モバイルアプリは、ADBMobileConfig.json ファイルにアクセスできるようになったので、Adobe Analytics に通信する方法を認識し、アプリの成功を促進するのに役立つ重要な指標値に関するレポートの作成を開始します。

## 次の手順  {#what-s-next}

1. [AEM Mobile アプリを使ってみる](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツを管理する](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションをビルドする](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics でアプリケーションのパフォーマンスをトラッキングする](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target でパーソナライズされたアプリケーションエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [重要なメッセージをユーザーに送信する](/help/mobile/phonegap-push-notifications.md)