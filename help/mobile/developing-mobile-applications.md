---
title: AEM でのモバイルアプリケーションの開発
description: Adobe PhoneGap Enterpriseを使用して、AEMでモバイルアプリケーションの開発を開始するには、次のページに従います。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
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
source-wordcount: '600'
ht-degree: 14%
---
# AEM でのモバイルアプリケーションの開発 {#developing-mobile-applications-in-aem}

{{ue-over-mobile}}

AEMでは、Adobe PhoneGapとAdobe Publishing Solutionsを使用して、豊富なコンテンツを備えたモバイルアプリケーションと、ユーティリティベースのモバイルアプリケーションの両方を作成および管理できます。

* モバイルアプリを一元管理。
* プロビジョニングのプロファイルを作成する複雑さや、アプリを構築してアップロードして共有するための追加作業なしに、開発環境やステージング環境にあるアプリを確認できます。
* AEM オーサリング環境を使用すると、アプリのリッチコンテンツを作成および管理できます。
* HTML 5とAdobe PhoneGapを組み合わせて利用すれば、デバイスネイティブな能力を利用してリッチなエクスペリエンスを構築できます。
* Cordova WebViewsを通じて、新しいアプリケーションまたは既存の&#x200B;**ネイティブ** アプリケーションにHTML5 Web ビューを導入します。
* webやモバイル web、モバイルアプリ、印刷物など、あらゆる配信チャネルでリッチマルチメディアコンテンツを作成、キュレーションして共有できます。

AEMは、Adobe PhoneGap Build サービス （`https://build.phonegap.com/`）と統合して、アプリケーションのビルドとデプロイのプロセスを簡素化します。

**Adobe ContentSync**&#x200B;を使用すると、アプリケーションを再インストールしたり、appStore、Google Play、その他のアプリソースからダウンロードしたりすることなく、ページやコンテンツの更新を無線（OTA）で簡単にデバイスにダウンロードできます。

**Adobe Analytics**&#x200B;は、AEM アプリに完全に統合されており、配信、位置情報、オペレーティングシステム、デバイス、クリックストリーム、iBeacon トラッキングなどの詳細なトラッキングが可能です。

## アプリの作成 {#creating-apps}

開発者は、[AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)と[https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)に含まれる追加リソースを使用して、Cordova Webviewsを実行する参照ネイティブアプリなど、PhoneGapを使用してAEM アプリをブートストラップできます。

スターターキット Git リポジトリのreadmeには、スターターキットを使用するためのチュートリアルが含まれています。

* ブランディングのカスタマイズ
* Mavenのサンプルビルドとデプロイメントターゲット
* Source control repository configuration
* ローカルまたはリモートのAEM インスタンスをインストールしてデプロイする
* AEMからアンインストールする

>[!NOTE]
>
>ラボを含む追加の参照実装ソースは、GitHub [ここ](https://github.com/adobe-marketing-cloud-apps)および「キッチン流し」ソース [ここ](https://github.com/blefebvre/aem-phonegap-kitchen-sink)にあります。

## IOS 9およびHTTP ホストの開発 {#developing-for-ios-and-http-hosts}

IOSの開発者は、iOS 9で実行されているCordova アプリに関するオープンな問題を認識しておく必要があります。 この問題により、安全でないホスト （*http://localhost:4502*&#x200B;など）に対するリクエストが行われなくなります。 この問題は、cordova-iosの今後のリリース（Cordova CLIで消費）で解決されますが、その間に2つの回避策があります。

1. 直ちに対処する方法として、iOS 8のシミュレータは問題なく使用できます。
1. IOS 9を使用する必要がある場合、apps -Info.plist （「&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist」で`cordova platform add ios`を実行した後に見つかる）ファイルを手動で編集して、次のプロパティを含めることができます。

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>「アプリトランスポートセキュリティ」について詳しくは、[AppleのiOS9 プレリリースドキュメント &#x200B;](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14)の次の節と、この[&#x200B; スタックオーバーフローに関するディスカッション &#x200B;](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)を参照してください。

## AEM でのモバイルアプリケーションの開発 {#developing-mobile-applications-in-aem-1}

* [AEM PhoneGap の起動](/help/mobile/starting-aem-phonegap-app.md)
* [モバイルアプリケーションのビルド](/help/mobile/building-app-mobile-phonegap.md)
* [アプリの構造](/help/mobile/phonegap-structure-an-app.md)
* [アプリコンソールを使用したアプリの作成および編集](/help/mobile/phonegap-apps-console.md)
* [単一ページアプリケーション](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI によるアプリの開発](/help/mobile/phonegap-apps-pg-cli.md)
* [デバイス機能へのアクセス](/help/mobile/phonegap-access-device-features.md)
* [Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング](/help/mobile/phonegap-intro-to-app-analytics.md)
* [モバイルアプリケーションへの Adobe Analytics の追加](/help/mobile/phonegap-add-analytics-to-apps.md)
* [プッシュ通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile のコンテンツパーソナライゼーション](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [アプリの詳細な構造](/help/mobile/phonegap-apps-arch.md)
* [ハイブリッドアプリの AEM Mobile 対応](/help/mobile/phonegap-adding-content-to-imported-app.md)

### その他のリソース {#additional-resources}

管理者と開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [Adobe PhoneGap EnterpriseとAEMのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
