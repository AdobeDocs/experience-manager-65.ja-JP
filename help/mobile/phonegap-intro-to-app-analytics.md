---
title: Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング
seo-title: Track App Performance with Adobe Mobile Analytics
description: Adobe Mobile Services では、使用状況、アプリのクラッシュ、デバイスの詳細など、モバイルアプリの数ある重要な指標をトラッキングすることで、ユーザーがモバイルアプリをどのように使用しているかを把握できます。このページでは、この機能について詳しく見ていきます。
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 57%

---

# Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

顧客コンバージョンおよびロイヤルティを高めたいと考えています。

顧客に関連性の高い魅力的なエクスペリエンスを提供したい。

マーケティングキャンペーンにおいて AEM Mobile アプリはどのような役割を果たしていますか。

ユーザーに最適なエクスペリエンスを提供するために、どのようにモバイルアプリケーションを微調整できますか。

Adobe Mobile Services では、使用状況、アプリのクラッシュ、デバイスの詳細など、モバイルアプリの数ある重要な指標をトラッキングすることで、ユーザーがモバイルアプリをどのように使用しているかを把握できます。

Adobe Experience Manager Mobile では、AEM Mobile アプリケーションダッシュボードから直接モバイル分析の詳細を一目で確認できます。この **モバイル指標タイル** のダッシュボードには、モバイルアプリケーションのリアルタイム分析が用意されており、開発者、作成者および管理者はモバイルアプリの状態をすばやく把握できます。 分析を支えるカバーの下には、 [Adobeモバイル分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. AdobeMobile Analytics SDK は、ネイティブで、または Web ビュー用の PhoneGap ブリッジプラグインを通じて、アプリケーションにプラグインできます。 指標は収集され、デバイスが接続されるまでデバイス上でキャッシュされ、そのデータがAdobeの Mobile Services クラウドにプッシュされて、レポートと分析がおこなわれます。

Adobe Mobile Analytics SDK は、次の機能を提供します。

1. **モバイルチャネルに関するデータ収集** - すべての主要オペレーティングシステム上のモバイル Web サイトおよびアプリに関して総合的なデータを収集します。
1. **モバイルエンゲージメント分析**  — モバイルアプリ、Web サイトまたはビデオ内でのユーザーエンゲージメントを把握します。これには、消費者がチャネルを起動する頻度、チャネルから購入するかどうかなどが含まれます。
1. **モバイルアプリのダッシュボードとレポート**  — アプリやアプリストア指標のライフサイクル指標を含む使用状況レポートを取得します。ユーザー、起動回数、平均セッション長、リテンション長、クラッシュ回数のトレンドを確認できます。
1. **モバイルキャンペーン分析** - SMS、モバイル検索広告、モバイルディスプレイ広告、QR コードなど、モバイル固有のキャンペーンの効果を定量化します。
1. **位置情報分析**  — アプリのユーザーが起動した場所や、GPS の位置や目標地点によってモバイルエクスペリエンスとやり取りする場所を特定します。
1. **パス分析**  — ユーザーがアプリ内をどのように移動して、ユーザーを引き付けている画面や UI 要素を特定し、ユーザーをドロップオフにさせるかを確認します。

この節では、 [AEM Developers](#developers) 分析追跡を使用してAEM Mobileアプリを実装する方法を学ぶことができます。

最後に [AEM Administrators](#administrators) 学習内容：

* Adobe Mobile Services に対するクラウドサービスを作成します。
* モバイルサービス設定を作成し、レポートスイートを関連付けます。
* モバイルアプリにモバイルサービス設定を関連付けます。
* AEM アプリケーションコマンドセンターで指標を表示します。
* モバイルアプリに AMS SDK 設定を割り当てます。

## 開発者向け - アプリへの Analytics の統合 {#for-developers-integrate-analytics-into-your-app}

**前提条件：** AEM管理者は、Mobile Services クラウド設定Adobe、 [以下で説明するように](#amscloudserviceconfig).

開発者は [AEM Mobileアプリへの analytics の追加](/help/mobile/phonegap-add-analytics-to-apps.md) 必要に応じて、ユーザーがモバイルアプリコンテンツとどのように関わっているかを追跡、レポートおよび理解し、起動回数、アプリ内時間、クラッシュ率などの主要なライフサイクル指標を測定します。

## 管理者向け - Adobe Mobile Services クラウドサービスの設定 {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Mobile Services のAdobeを活用するには、AEMAdobeMobile ServicesCloud ServiceをAdobe Analyticsアカウント情報と共に設定する必要があります。 Apps コマンドセンターでは、 **指標を分析** クラウドサービスを作成し、モバイルアプリに関連付けることができるタイル。

モバイルアプリにクラウドサービスを設定するには、まず、指標を分析タイルにある歯車アイコンをクリックします。

![chlimage_1-125](assets/chlimage_1-125.png)

指標を分析タイルで歯車アイコンをクリックすると、Mobile Services 分析を設定モーダルダイアログが開きます。「Mobile Service 設定を選択」ドロップダウンから設定を選択します。 新しい設定を作成する必要がある場合は、設定ボタンをクリックします。

Adobe Mobile Services クラウドサービスを作成するには、サービスに接続することと、設定に割り当てるレポートスイートを選択することの 2 つの手順が必要です。

まず、ダッシュボードのクラウドサービスを管理タイルで + ボタンをクリックします。

![chlimage_1-126](assets/chlimage_1-126.png)

「**+**「 」ボタン、 **追加Cloud Service** ウィザードが表示されます。

![chlimage_1-127](assets/chlimage_1-127.png)

モバイルサービス設定を選択するか、または次のように必須フィールドに入力して新規モバイルサービス設定を作成します。AEM管理者が Mobile Services への接続を正常に作成するには、この情報が必要です。

![chlimage_1-128](assets/chlimage_1-128.png)

Mobile Services アカウント設定が完了したら、アプリを選択するように求められます。これにより、AdobeMobile Services 分析レポートがそのアプリケーションに接続されます。

目的のモバイルサービスを選択し、「更新」をクリックしてモバイルサービス設定を割り当ててから、ダイアログを閉じます。

AEM Mobile アプリにモバイルサービス設定を関連付けたので、タイルによって指標データの取得とレポートの作成が開始されます。

![chlimage_1-129](assets/chlimage_1-129.png)

### Adobe Mobile Services SDK 設定ファイル {#adobe-mobile-services-sdk-config-file}

この時点で、モバイルアプリケーションはクラウドサービスに関連付けられていますが、収集されたモバイル指標を Adobe Analytics に通信する方法をまだ認識していません。モバイルアプリをAdobe Analyticsにワイヤアップするには、AdobeMobile Services SDK 設定ファイルをAdobe Experience Managerに追加する必要があります。

指標を分析タイルから、矢印アイコンをクリックして「AMS SDK 設定をダウンロード」または「AMS SDK 設定をアップロード」メニューエントリを表示します。

![chlimage_1-130](assets/chlimage_1-130.png)

最初の手順では、Adobe Mobile Services から SDK 設定を取得します。「AMS SDK 設定をダウンロード」をクリックすると、設定ファイルをダウンロードできる Adobe Mobile Services の Web サイトにリダイレクトされます。ADBMobileConfig.json ファイルを取得したら、「AMS SDK 設定をアップロード」をクリックして、設定ファイルをAEMにアップロードします。

![chlimage_1-131](assets/chlimage_1-131.png)

「Adobe Mobile Services アプリ設定をアップロード」ボタンをクリックし、ADBMobileConfig.json ファイルを参照し、「アップロード」をクリックします。

モバイルアプリは、ADBMobileConfig.json ファイルにアクセスできるようになったので、Adobe Analytics に通信する方法を認識し、アプリの成功を促進するのに役立つ重要な指標値に関するレポートの作成を開始します。

## 次のステップ? {#what-s-next}

1. [AEM Mobile アプリを使ってみる](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツを管理する](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションをビルドする](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics でアプリケーションのパフォーマンスをトラッキングする](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target でパーソナライズされたアプリケーションエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [重要なメッセージをユーザーに送信する](/help/mobile/phonegap-push-notifications.md)
