---
title: モバイルアプリケーションへの Adobe Analytics の追加
seo-title: モバイルアプリケーションへの Adobe Analytics の追加
description: このページでは、Mobile App Analytics を Adobe Mobile Services と統合し、AEM アプリで使用する方法について説明します。
seo-description: このページでは、Mobile App Analytics を Adobe Mobile Services と統合し、AEM アプリで使用する方法について説明します。
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 65%

---


# モバイルアプリケーションへの Adobe Analytics の追加{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

モバイルアプリケーションユーザーにとって魅力的で関連性の高いエクスペリエンスを生成したいとお考えですか。アプリケーションのライフサイクルと使用状況の監視や測定に Adobe Mobile Services SDK を使用しないとしたら、何に基づいて決定を下すのでしょうか。ロイヤルティの最も高いお客様はどこにいますか。どのようにして確実に関連性の高さを維持し、コンバージョンを最適化しますか。

ユーザーは、すべてのコンテンツにアクセスしていますか。ユーザーはアプリの使用を中止していますか。中止している場合、その場所はどこですか。ユーザーがアプリに留まる頻度と戻ってくる頻度はどのくらいですか。どのような変更を導入でき、どのようにして定着率を測定しますか。クラッシュ率はどうなっていますか。ユーザーに対してクラッシュが発生していますか。

[Adobe Mobile Servicesとの連携により、AEMアプリの](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) モバイルアプリAnalytics [を活用できます](https://www.adobe.com/marketing-cloud/mobile-marketing.html)。

AEMアプリを実装して、モバイルアプリやコンテンツに対するユーザーの関与を追跡、レポート、理解し、起動回数、アプリ内時間、クラッシュ率などの主要なライフサイクル指標を測定します。

この節では、AEM 開発者が次の操作を実行する方法について説明します。**

* モバイルアプリケーションへの Mobile Analytics の統合
* Bloodhound による Analytics トラッキングのテスト

## 前提条件 {#prerequisties}

AEM Mobile では、アプリでのトラッキングデータを収集してレポートするには Adobe Analytics アカウントが必要です。設定の一環として、AEM *管理者は* 、まず次の操作を行う必要があります。

* Adobe Analytics アカウントを設定し、Mobile Services にアプリケーションのレポートスイートを作成します。
* Adobe Experience Manager（AEM）に AMS クラウドサービスを設定します。

## 開発者向け - アプリへの Mobile Analytics の統合 {#for-developers-integrate-mobile-analytics-into-your-app}

### ContentSync での設定ファイルの取り込みの設定 {#configure-contentsync-to-pull-in-configuration-file}

Analytics アカウントを設定したら、コンテンツをモバイルアプリケーションに取り込むためにコンテンツ同期設定を作成する必要があります。

詳しくは、「コンテンツ同期コンテンツの設定」を参照してください。 この設定は、コンテンツ同期に対して、ADBMobileConfig を /www ディレクトリに取り込むように指示する必要があります。For example in the Geometrixx Outdoors App the Content Sync configuration is located at: */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. 開発向けの設定もありますが、Geometrixx Outdoors の場合には開発以外の設定と同じものです。

モバイルアプリケーションのAEM AppsダッシュボードからADBMobileConfigをダウンロードする方法について詳しくは、「Analytics- Mobile Services - Adobe Mobile Services SDK Configファイル」を参照してください。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

プラットフォームごとに、固有の場所に ADBMobileConfig をコピーする必要があります。

PhoneGap CLI を使用してビルドする場合は、Cordova ビルドフックスクリプトを使用します。This can be seen intheGeometrixx Outdoors App at:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

For iOS the file will need to be copied to the XCode project&#39;s **Resources** directory (eg. platforms/ios/Geometrixx/Resources/ADBMobileConfig.json）にコピーする必要があります。アプリが Android 向けの場合、コピー先のパスは「platforms/android/assets/ADBMobileConfig.json」です。For further details on using hooks during the PhoneGap CLI build refer to [Three hooks your Cordova/PhoneGap project needs](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### アプリでの AMS プラグインの追加 {#add-the-ams-plugin-in-the-app}

アプリがデータを収集するには、アプリの一部としてAdobe Mobile Services(AMS)プラグインを含める必要があります。 アプリの config.xml にプラグインを 1 つの機能としてインクルードすることで、別の Cordova フックを使用して、PhoneGap Build プロセスでプラグインを自動的に追加できます。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

The Geometrixx Outdoors App config.xml is located at */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. 上記の例では、プラグイン URL の後に「#」とタグ値を追加することで、使用するプラグインの特定のバージョンを要求しています。これは、未テストのプラグインがビルド時に追加されても予期しない問題が発生しないようにする場合に効果的です。

これらの手順を実行すると、アプリでは Adobe Analytics で提供されるすべてのライフサイクル指標をレポートできるようになります。これには例えば、起動、クラッシュ、インストールなどのデータが含まれます。関心があるデータがこれだけの場合、操作は完了です。カスタムデータを収集する場合は、そのためのコードを実装する必要があります。

### アプリを完全にトラッキングするためのコードの実装 {#instrument-your-code-for-full-app-tracking}

There are several tracking APIs provided in the [AMS Phonegap Plugin API.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

これらを使用すると、ユーザーがアプリ内でどのページに移動しているか、どのコントロールが最も使用されているかなど、状態およびアクションをトラッキングできます。アプリを計測して追跡する最も簡単な方法は、AMSプラグインが提供するAnalyticsAPIを利用することです。

* ADB.trackState()
* ADB.trackAction()

Geometrixx Outdoors アプリのコードを見ると参考になります。Geometrixx Outdoors アプリでは、ADB.trackState() メソッドを使用して、すべてのページ移動をトラッキングしています。詳しくは、/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.jsのソースコードを参照してください。

ソースコードにこれらのメソッドの呼び出しを実装することで、アプリケーションに対する完全な指標を収集できます。

#### AMS への接続のプロパティ {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImpl* は、AMS への接続用の以下のプロパティを公開しています。

| **ラベル** | **説明** | **デフォルト** |
|---|---|---|
| APIエンドポイント | Adobe Mobile Services HTTP APIのベースURL | https://api.omniture.com |
| 設定エンドポイント | 指定したレポートスイートIDのADBモバイル設定を取得するために使用されるURL | /ams/1.0/app/config/ |
| Mobile Service Apps | ユーザー会社ー内のアプリのリストの取得 | /ams/1.0/apps |

