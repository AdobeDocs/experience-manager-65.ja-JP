---
title: AEM でのモバイルアプリケーションの開発
seo-title: Developing Mobile Applications in AEM
description: ここでは、Adobe PhoneGap Enterprise を使用したAEMでのモバイルアプリケーションの開発を開始します。
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 15%

---

# AEM でのモバイルアプリケーションの開発 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEMは、Adobe PhoneGapとAdobePublishing Solutions を活用し、コンテンツに富んだユーティリティベースのクロスプラットフォームモバイルアプリケーションを作成および管理できます。

* すべての会社のモバイルアプリを 1 か所で管理します。
* プロファイルのプロビジョニングの複雑さや、共有用にアプリを作成およびアップロードする追加の手間を必要とせずに、開発環境およびステージング環境でアプリをレビューできます。
* AEMオーサリング環境を使用して、アプリのリッチコンテンツを作成および管理します。
* HTML5 とAdobe PhoneGapを使用して、デバイスネイティブ機能を備えたリッチなエクスペリエンスを作成します。
* 新規または既存のHTMLに Web ビューを導入する **ネイティブ** Cordova WebViews を介したアプリケーション。
* Web、モバイル Web、モバイルアプリ、印刷など、あらゆる配信チャネルにわたって、リッチなマルチメディアコンテンツを作成、キュレーションおよび共有します。

AEMとAdobe PhoneGap Buildサービスの統合 (`https://build.phonegap.com/`) を使用して、アプリケーションのビルドとデプロイのプロセスを簡略化できます。

**AdobeContentSync** を使用すると、アプリを再インストールしたり、appStore、Google Play、その他のアプリソースからダウンロードしたりしなくても、Over-the-Air(OTA) をデバイスに簡単にページやコンテンツの更新をダウンロードできます。

**Adobe Analytics** はAEMアプリに完全に統合され、配布、位置情報、オペレーティングシステム、デバイス、クリックストリーム、iBeacon トラッキングなどの詳細な追跡が可能です。

## アプリの作成 {#creating-apps}

開発者は、 [AEM PhoneGap スターターキット](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) で見つかった追加リソースと共に [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) Cordova Webviews を実行する参照用ネイティブアプリを含め、AEMアプリを PhoneGap でブートストラップする場合。

Starter Kit Git リポジトリの readme には、スターターキットの使用に関するチュートリアルが含まれています。

* ブランディングのカスタマイズ
* Maven のサンプルビルドおよびデプロイメントターゲット
* ソース管理リポジトリの設定
* ローカルまたはリモートのAEMインスタンスへのインストールとデプロイ
* AEMからのアンインストール

>[!NOTE]
>
>ラボを含むその他の参照用実装ソースは、GitHub にあります [ここ](https://github.com/adobe-marketing-cloud-apps) そして、「台所流し台」の源 [ここ](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## IOS 9 および HTTP ホスト用の開発 {#developing-for-ios-and-http-hosts}

iOSの開発者は、iOS 9 で実行される Cordova アプリのオープンな問題を認識している必要があります。 この問題により、安全でないホスト ( *http://localhost:4502*) をクリックします。 この問題は、（Cordova CLI で使用される）cordova-ios の今後のリリースで解決されますが、それまでの間に、次の 2 つの回避策が用意されています。

1. 即時の回避策として、iOS 8 シミュレーターを問題なく使用できます。
1. iOS 9 を使用する必要がある場合は、 apps -Info.plist （実行後に見つかります） `cordova platform add ios` 」の&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;) ファイルを手動で編集して、次のプロパティを含めることができます。

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>「App Transport Security」について詳しくは、 [AppleのiOS9 プレリリースドキュメント](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) そして [スタックオーバーフローの議論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

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

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
