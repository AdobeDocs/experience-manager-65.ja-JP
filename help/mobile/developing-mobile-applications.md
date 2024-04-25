---
title: AEM でのモバイルアプリケーションの開発
description: このページでは、Adobe PhoneGap Enterprise を使用してAEMでモバイルアプリケーションの開発を開始する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 19%

---

# AEM でのモバイルアプリケーションの開発 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

AEMでは、Adobe PhoneGapおよびAdobe公開ソリューションを使用して、コンテンツに富んだアプリケーションとユーティリティベースのクロスプラットフォームモバイルアプリケーションの両方を作成および管理できます。

* すべての会社のモバイルアプリを 1 か所で管理できます。
* プロビジョニングプロファイルを複雑にすることなく、開発環境やステージング環境でアプリをレビューし、共有のためにアプリを作成してアップロードする手間を省きます。
* AEM オーサリング環境を使用して、アプリ用のリッチコンテンツを作成および管理します。
* HTML5 とAdobe PhoneGapを使用して、デバイスネイティブ機能で豊富なエクスペリエンスを作成します。
* 新規または既存のユーザーにHTML 5 の Web ビューを導入 **ネイティブ** cordova WebViews を使用したアプリケーション。
* Web、モバイル Web、モバイルアプリ、印刷など、あらゆる配信チャネルにわたって、リッチなマルチメディアコンテンツを作成、キュレーションおよび共有します。

AEMはAdobe PhoneGap Build サービス（`https://build.phonegap.com/`）を使用して、アプリケーションのビルドおよびデプロイプロセスを簡略化できます。

**Adobe ContentSync** を使用すると、アプリケーションを再インストールしたり、appStore、Google Playまたはその他のアプリソースからダウンロードしたりしなくても、ページおよびコンテンツのアップデートを Over-the-Air （OTA）でデバイスに簡単にダウンロードできます。

**Adobe Analytics** はAEM アプリに完全に統合されており、配布、位置情報、オペレーティングシステム、デバイス、クリックストリーム、iBeacon のトラッキングなどの詳細なトラッキングが可能です。

## アプリの作成 {#creating-apps}

開発者は、 [AEM PhoneGap スターターキット](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) と、に記載されている追加リソース [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) cordova Web ビューを実行する参照ネイティブアプリを含め、AEM アプリを PhoneGap でブートストラップする。

スターターキット Git リポジトリの Readme には、スターターキットを使用するためのチュートリアルが含まれています。

* ブランディングのカスタマイズ
* Maven サンプルのビルドおよびデプロイメントターゲット
* ソース管理リポジトリの設定
* ローカルまたはリモートのAEM インスタンスへのインストールとデプロイ
* AEMからアンインストール

>[!NOTE]
>
>ラボを含む参照実装のソースは GitHub にあります [こちら](https://github.com/adobe-marketing-cloud-apps) 「キッチン・シンク」のソース [こちら](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## iOS 9 および HTTP ホスト向けの開発 {#developing-for-ios-and-http-hosts}

IOS開発者は、iOS 9 上で動作する Cordova アプリケーションのオープンな問題を認識しておく必要があります。 この問題により、安全でないホスト（例えば、 *http://localhost:4502*）に設定します。 この問題は、cordova-ios の今後のリリース（Cordova CLI によって使用）で解決される予定ですが、当面、2 つの回避策が利用可能です。

1. すぐに対処できるように、iOS 8 シミュレータを問題なく使用できます。
1. iOS 9 を使用する必要がある場合は、 `cordova platform add ios` 。対象：&quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;）ファイルを手動で編集して、次のプロパティを含めることができます。

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>「アプリ転送セキュリティ」について詳しくは、の次の節を参照してください [AppleのiOS9 プレリリースドキュメント](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) この [スタック オーバーフローの説明](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

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

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
