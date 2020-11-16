---
title: AEM でのモバイルアプリの開発
seo-title: AEM でのモバイルアプリの開発
description: Adobe PhoneGap Enterprise を使用して AEM でモバイルアプリケーションの開発を開始するには、このページの説明に従います。
seo-description: Adobe PhoneGap Enterprise を使用して AEM でモバイルアプリケーションの開発を開始するには、このページの説明に従います。
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 76%

---


# AEM でのモバイルアプリの開発 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

AEM では、Adobe PhoneGap および Adobe Publishing Solution を利用することにより、コンテンツが豊富でユーティリティベースの次のようなクロスプラットフォームモバイルアプリケーションを作成し、管理できます。

* 社内のすべてのモバイルアプリを 1 箇所で管理します。
* 開発環境およびステージング環境でアプリをレビューします。プロファイルのプロビジョニングに伴う複雑さやアプリのビルドおよび共有用のアップロードを行う作業は不要です。
* AEM オーサリング環境を使用して、アプリ向けのリッチコンテンツを作成および管理します。
* Adobe PhoneGap で HTML5 を使用して、デバイスネイティブの機能による充実したエクスペリエンスを生成します。
* Cordova WebView による新規または既存の&#x200B;**ネイティブ**&#x200B;アプリケーションに HTML5 WebView を導入します。
* リッチなマルチメディアコンテンツを作成および管理して、Web、モバイル Web、モバイルアプリ、印刷物などすべての配信チャネルで共有します。

AEM は、Adobe **[PhoneGap Build サービス](https://build.phonegap.com/)と統合され、アプリケーションをビルドしてデプロイするプロセスの簡素化を実現しています。**

**Adobe ContentSync** を使用すると、ユーザーはアプリケーションを再インストールしたり、AppStore や Google Play やその他のアプリ提供元からダウンロードしたりすることなく、ページおよびコンテンツの更新を自分のデバイスに無線（OTA）で簡単にダウンロードできます。

**Adobe Analytics**&#x200B;は、AEM アプリに完全に統合されており、配布、位置情報、オペレーティングシステム、デバイス、クリックストリーム、iBeacon の詳細なトラッキングを行うことができます。

## アプリの作成 {#creating-apps}

Developers can use the [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) along with additional resources found in [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) to bootstrap AEM apps with PhoneGap, including a reference native app running Cordova Webviews.

Starter Kit Git リポジトリの readme には、スターターキットを使用するためのチュートリアルが含まれています。

* ブランディングのカスタマイズ
* Maven サンプルビルドおよびデプロイメントターゲット
* ソース制御リポジトリの設定
* ローカルまたはリモートのAEMインスタンスへのインストールとデプロイ
* AEM からのアンインストール

>[!NOTE]
>
>Additional reference implementation source, including labs, can be found on GitHub [here](https://github.com/adobe-marketing-cloud-apps) and, the &quot;kitchen-sink&quot; source [here](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## iOS 9 ホストおよび HTTP ホスト用の開発 {#developing-for-ios-and-http-hosts}

iOS の開発者は、iOS 9 で Cordova アプリを実行した場合の未解決の問題に留意する必要があります。This issue prevents requests from being made to insecure hosts (such as *http://localhost:4502*). この問題は、（Cordova CLI で利用される）cordova-ios の今後のリリースで解決される予定ですが、それまでは次の方法で回避できます。

1. すぐに解決できる方法として、問題なくiOS 8シミュレーターを使用できます。
1. If you must use iOS 9, your apps -Info.plist (found after running `cordova platform add ios` in “&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist”) file can be manually edited to include the following property:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>For more detail on “App Transport Security”, see the following section of [Apple’s iOS9 prerelease docs](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) and this [Stack Overflow discussion](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## AEM でのモバイルアプリの開発 {#developing-mobile-applications-in-aem-1}

* [AEM PhoneGap の起動](/help/mobile/starting-aem-phonegap-app.md)
* [モバイルアプリケーションのビルド](/help/mobile/building-app-mobile-phonegap.md)
* [アプリの構造](/help/mobile/phonegap-structure-an-app.md)
* [アプリコンソールを使用したアプリの作成および編集](/help/mobile/phonegap-apps-console.md)
* [シングルページアプリケーション](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI によるアプリの開発](/help/mobile/phonegap-apps-pg-cli.md)
* [デバイスの機能へのアクセス](/help/mobile/phonegap-access-device-features.md)
* [Adobe Mobile Analytics によるアプリパフォーマンスのトラッキング](/help/mobile/phonegap-intro-to-app-analytics.md)
* [モバイルアプリケーションへの Adobe Analytics の追加](/help/mobile/phonegap-add-analytics-to-apps.md)
* [プッシュ通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile のコンテンツパーソナライゼーション](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [アプリの詳細な構造](/help/mobile/phonegap-apps-arch.md)
* [ハイブリッドアプリの AEM Mobile 対応状況](/help/mobile/phonegap-adding-content-to-imported-app.md)

### その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM での Adobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM での Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
