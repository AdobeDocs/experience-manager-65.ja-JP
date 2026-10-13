---
title: モバイルアプリケーションへの Adobe Analytics の追加
description: Adobe Mobile Servicesと連携して、Adobe Experience Manager アプリでモバイルアプリ分析を使用する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%
---
# モバイルアプリケーションへの Adobe Analytics の追加{#add-adobe-analytics-to-your-mobile-application}

{{ue-over-mobile}}

モバイルアプリケーションユーザー向けに、魅力的で関連性の高いエクスペリエンスを構築するには、 Adobe Mobile Services SDKを使用して、アプリケーションのライフサイクルと使用状況をモニタリングおよび測定していない場合、どのような判断を下すのでしょうか？ 最も忠実な顧客はどこにいるのか？ コンバージョンを最適化し、関連性を維持するにはどうすればよいでしょうか？

ユーザーはすべてのコンテンツにアクセスしていますか？ アプリを放棄しているか、その場合、どこで放棄しているか、などです。 どれくらいの頻度でアプリに滞在し、どれくらいの頻度でアプリを使用するために再訪問するか？ リテンションを高めるために、どのような変化を導入し、それを測定できますか？ クラッシュ率について、あなたのアプリはあなたのユーザーのためにクラッシュしていますか？

[Adobe Mobile Services](https://business.adobe.com/jp/products/campaign/mobile-marketing.html)と連携することで、Adobe Experience Manager（AEM）アプリの[&#x200B; モバイルアプリ分析](https://business.adobe.com/jp/products/analytics/mobile-marketing.html)を活用できます。

AEMアプリを計測することで、利用者がモバイルアプリやコンテンツにどのようにエンゲージしているのかを追跡、レポート、把握し、ローンチ、アプリ滞在時間、クラッシュ率などの主要なライフサイクル指標を測定できます。

この節では、AEM *Developers*&#x200B;が次の操作を実行する方法について説明します。

* モバイル分析をモバイルアプリケーションに統合
* Bloodhoundで分析トラッキングをテストする

## 前提条件 {#prerequisties}

AEM Mobileでは、アプリ内のトラッキングデータを収集およびレポートするためにAdobe Analytics アカウントが必要です。 設定の一部として、AEM *Administrator*&#x200B;は最初に次の操作を行う必要があります。

* Adobe Analytics アカウントを設定し、Mobile Servicesでアプリケーションのレポートスイートを作成します。
* Adobe Experience Manager（AEM）でAMS Cloud Serviceを設定します。

## 開発者向け – モバイル分析をアプリに統合する {#for-developers-integrate-mobile-analytics-into-your-app}

### 設定ファイルを取り込むためのContentSyncの設定 {#configure-contentsync-to-pull-in-configuration-file}

Analytics アカウントを設定したら、コンテンツ同期設定を作成して、コンテンツをモバイルアプリケーションに取り込みます。

詳しくは、コンテンツ同期コンテンツの設定を参照してください。 設定では、ADBMobileConfigを/www ディレクトリに配置するようにContent Syncに指示する必要があります。 例えば、Geometrixx Outdoors アプリのContent Sync設定は&#x200B;*/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*&#x200B;です。 開発のための構成もあります。 ただし、Geometrixx Outdoorsがある場合は、開発以外の設定と同じです。

Mobile Application AEM Apps ダッシュボードからADBMobileConfigをダウンロードする方法の詳細については、Analytics - Mobile Services - Adobe Mobile Services SDK Config Fileを参照してください。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

各プラットフォームでは、ADBMobileConfigを特定の場所にコピーする必要があります。

PhoneGap CLIでビルドする場合は、cordova ビルドフックスクリプトを使用します。 これは、次のGeometrixx Outdoors アプリで確認できます：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

IOSの場合、ファイルをXCode プロジェクトの&#x200B;**Resources** ディレクトリにコピーする必要があります（例：「platforms/ios/Geometrixx/Resources/ADBMobileConfig.json」）。 アプリがAndroid™を対象としている場合、コピー先のパスは「platforms/android/assets/ADBMobileConfig.json」になります。 PhoneGap CLIのビルド中にフックを使用する方法について詳しくは、[Cordova/PhoneGap プロジェクトに必要な3つのフック &#x200B;](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c)を参照してください。

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

### アプリにAMS プラグインを追加する {#add-the-ams-plugin-in-the-app}

アプリがデータを収集するには、Adobe Mobile Services （AMS）プラグインをアプリの一部として含める必要があります。 プラグインをアプリのconfig.xmlに機能として含めることで、PhoneGap ビルドプロセス中にプラグインを自動的に追加するために別のCordova フックを使用できます。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors アプリ config.xmlは、*/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*&#x200B;にあります。 上記の例では、「#」を追加し、次にプラグイン URLの後にタグ値を追加して、特定のバージョンのプラグインを使用するようにリクエストしています。 これは、ビルド中にテストされていないプラグインが追加されたために、予期しない問題が発生しないようにするためのベストプラクティスです。

これらの手順を実行すると、アプリはAdobe Analyticsが提供するすべてのライフサイクル指標をレポートできるようになります。 これには、ローンチ、クラッシュ、インストールなどのデータが含まれます。 それが唯一のデータであれば、終わりです。 カスタムデータを収集する場合は、コードを実装する必要があります。

### 完全なアプリ トラッキング用にコードをインストルメントする {#instrument-your-code-for-full-app-tracking}

[AMS Phonegap Plugin APIには、複数のトラッキング APIが用意されています。](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

これにより、ユーザーがアプリ内のどこに移動しているか、どのコントロールが最も頻繁に使用されているかなどの状態とアクションを追跡できます。 トラッキング用にアプリを計測する最も簡単な方法は、AMS プラグインが提供するAnalytics APIを使用することです。

* ADB.trackState （）
* ADB.trackAction （）

参考までに、Geometrixx Outdoors アプリのコードを参照してください。 Geometrixx Outdoors アプリでは、すべてのページナビゲーションがADB.trackState （） メソッドを使用して追跡されます。 詳しくは、/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.jsのソースコードを参照してください。

このメソッド呼び出しでソースコードを実装することで、アプリケーションに対する完全な指標を収集できます。

#### AMSに接続するためのプロパティ {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* lは、AMSに接続するための次のプロパティを公開します。

| **ラベル** | **説明** | **デフォルト** |
|---|---|---|
| API エンドポイント | Adobe Mobile Services HTTP APIのベース URL | https://api.omniture.com |
| 設定エンドポイント | 指定されたレポートスイート IDのADB Mobile Configを取得するために使用されるURL | /ams/1.0/app/config/ |
| Mobile Service Apps | ユーザー企業内のアプリのリストを取得します | /ams/1.0/apps |
