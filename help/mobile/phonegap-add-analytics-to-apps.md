---
title: モバイルアプリケーションへの Adobe Analytics の追加
description: Adobeの Mobile Services と統合することで、Adobe Experience Manager アプリで Mobile App Analytics を使用する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# モバイルアプリケーションへの Adobe Analytics の追加{#add-adobe-analytics-to-your-mobile-application}

{{ue-over-mobile}}

モバイルアプリケーションユーザーにとって魅力的で関連性の高いエクスペリエンスを構築したいと考えていますか？ アプリケーションのライフサイクルと使用状況の監視と測定にAdobe Mobile Services SDKを使用していない場合は、何に基づいて意思決定を行っているのでしょうか？ 常連客はどこにいますか？ コンバージョンの関連性を維持し、最適化することを、どのようにして保証できますか？

ユーザーはすべてのコンテンツにアクセスしていますか？ ユーザーがアプリを放棄しているかどうか、放棄している場合はどこにいるか。 アプリに留まる頻度と、アプリを使用するために戻ってくる頻度は？ 保持率を高めるためにどのような変更を導入して測定できますか？ クラッシュ率はどうですか。アプリがユーザーに対してクラッシュしていますか。

[2&rbrace;Adobeの Mobile Services](https://business.adobe.com/products/analytics/mobile-marketing.html) と統合することで、Adobe Experience Manager（AEM）アプリで [&#128279;](https://business.adobe.com/products/campaign/mobile-marketing.html) モバイルアプリ分析 &rbrace; を活用できます。

AEM アプリを実装して、ユーザーがモバイルアプリやコンテンツとどのように関わっているかを追跡、レポートおよび理解し、ローンチ、アプリ内時間、クラッシュ率などの主要なライフサイクル指標を測定します。

この節では、AEM *開発者* が以下を行う方法について説明します。

* モバイルアプリケーションへの Mobile Analytics の統合
* Bloodhound を使用した分析トラッキングのテスト

## 前提条件 {#prerequisties}

AEM Mobileでアプリのトラッキングデータを収集しレポートするには、Adobe Analytics アカウントが必要です。 設定の一環として、まずAEM *管理者* が以下を行う必要があります。

* Adobe Analytics アカウントを設定し、Mobile Services でアプリケーションのレポートスイートを作成します。
* Adobe Experience Manager（AEM）で AMSCloud Serviceを設定します。

## 開発者向け – モバイル分析をアプリに統合します {#for-developers-integrate-mobile-analytics-into-your-app}

### 設定ファイルを取り込むためのコンテンツ同期の設定 {#configure-contentsync-to-pull-in-configuration-file}

Analytics アカウントを設定したら、コンテンツ同期設定を作成して、モバイルアプリケーションにコンテンツを取り込みます。

詳しくは、コンテンツ同期コンテンツの設定を参照してください。 設定では、ADBMobileConfig を/www ディレクトリに配置するようにコンテンツ同期に指示する必要があります。 例えば、Geometrixx Outdoorsアプリでは、コンテンツ同期の設定は、*/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig* にあります。 開発用の設定もあります。 ただし、Geometrixx Outdoorsがある場合は、非開発用の設定と同じになります。

Mobile Application AEM Apps ダッシュボードから ADBMobileConfig をダウンロードする方法について詳しくは、Analytics - Mobile Services - Adobe Mobile Services SDK Config ファイルを参照してください。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

各プラットフォームでは、ADBMobileConfig を特定の場所にコピーする必要があります。

PhoneGap CLI を使用してビルドする場合は、cordova ビルドフックスクリプトを使用して行うことができます。 これは、Geometrixx Outdoors アプリ（*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*）で確認できます。

iOSの場合、ファイルを XCode プロジェクトの **Resources** ディレクトリ（例：「platforms/ios/Geometrixx/Resources/ADBMobileConfig.json」）にコピーする必要があります。 アプリケーションがAndroid™ を対象としている場合は、コピー先のパスは「platforms/android/assets/ADBMobileConfig.json」です。 PhoneGap CLI ビルド中のフックの使用について詳しくは、[Cordova/PhoneGap プロジェクトに必要な 3 つのフック ](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c) を参照してください。

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

### AMS プラグインのアプリへの追加 {#add-the-ams-plugin-in-the-app}

アプリでデータを収集するには、Adobe Mobile Services （AMS）プラグインをアプリの一部として含める必要があります。 プラグインをアプリの config.xml の機能として含めることで、PhoneGap のビルド処理中に別の Cordova フックを使用してプラグインを自動的に追加できます。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoorsアプリ config.xml は、*/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml* にあります。 上記の例では、特定のバージョンのプラグインをリクエストする際、プラグインの URL の後に「#」を付加し、続けてタグ値を付加します。 これは、ビルド中に追加されたテストされていないプラグインが原因で予期しない問題が発生しないようにするために、従うことをお勧めします。

これらの手順を実行すると、アプリが有効になり、Adobe Analyticsで提供されるすべてのライフサイクル指標をレポートできるようになります。 これには、ローンチ、クラッシュ、インストールなどのデータが含まれます。 それが気になる唯一のデータであれば、完了です。 カスタムデータを収集する場合は、コードを実装する必要があります。

### 完全なアプリトラッキングのためのコードの実装 {#instrument-your-code-for-full-app-tracking}

[AMS Phonegap Plugin API.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md) には、複数のトラッキング API が用意されています。

これらを使用すると、ユーザーがアプリ内で移動するページの状態やアクションなどを追跡でき、どのコントロールが最も多く使用されているかなどを把握できます。 トラッキング用にアプリを実装する最も簡単な方法は、AMS プラグインが提供する Analytics API を使用することです。

* ADB.trackState()
* ADB.trackAction()

詳しくは、Geometrixx Outdoorsアプリのコードを参照してください。 Geometrixx Outdoorsアプリでは、すべてのページナビゲーションが ADB.trackState （） メソッドを使用して追跡されます。 詳しくは、/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.jsのソースコードを参照してください。

このメソッド呼び出しを使用してソースコードを実装することで、アプリケーションに対する完全な指標を収集できます。

#### AMS に接続するためのプロパティ {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l は、AMS に接続するために次のプロパティを公開します。

| **ラベル** | **説明** | **デフォルト** |
|---|---|---|
| API エンドポイント | Adobe Mobile Services HTTP API のベース URL | https://api.omniture.com |
| 設定エンドポイント | 指定されたレポートスイート ID の ADB モバイル設定を取得するために使用される URL | /ams/1.0/app/config/ |
| Mobile Service アプリ | ユーザー会社内のアプリのリストを取得します | /ams/1.0/apps |
