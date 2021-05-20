---
title: AEM PhoneGap の起動
seo-title: AEM PhoneGap の起動
description: このページでは、開発者向けスターターキットについて説明します。
seo-description: このページでは、開発者向けスターターキットについて説明します。
uuid: 952bf9f9-5c79-4212-91b7-1d3850ec2402
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 2ecf05ed-4e56-4e0b-89cf-5161741f9001
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 54%

---


# AEM PhoneGap の起動  {#starting-aem-phonegap}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

開発者にとって最も良いのは、githubのAdobe Experience Manager Mobile Starterkitを見てみることです

https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit

このスターターキットでは、プロジェクトの作成と管理、必要なツールのインストール、Maven アーキタイプの定義、ビルド、デプロイ、独自機能の作成など、AEM Mobile 開発の基礎知識を迅速に習得できます。

開発者は、このサンプルを基に、PhoneGap を使用した AEM Mobile アプリケーションを開発できます。スターターキットおよび参照アプリケーションを使用して学習することで、リッチなモバイルアプリケーションを作成するための基礎を確実に理解できます。

* [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)を使用して、AEM Mobileカタログに適したアプリを作成します。
* 既存のアプリをAEM Mobileに移行する場合も、新規に開始する場合も、AEM Mobileの新機能の多くを示す、完全なソースを持つ[参照アプリ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)が作成されました。
* すべてのサンプルはGitHubにあります。[https://github.com/Adobe-Marketing-Cloud-Apps](https://github.com/Adobe-Marketing-Cloud-Apps)を追加し、Mavenでプロジェクトをブートストラップする処理を含めます。
* ほとんどの会議トークでは、[Kitchen Sinkのチュートリアル](https://github.com/blefebvre/aem-phonegap-kitchen-sink)を活用します。これはGithubでも見つけることができ、Apache Cordovaのネイティブ拡張機能の使用に焦点を当てています。

>[!NOTE]
>
>スターターキットに慣れる機会を得たら、Adobe Experience Manager *のコンポーネントとテンプレートについて学ぶことが重要です。*

## テンプレートおよびコンポーネント {#templates-and-components}

AEM *テンプレート*&#x200B;と&#x200B;*コンポーネント*&#x200B;を使用すると、ビジネスオーナーはカスタムエクスペリエンスを作成できます。 テンプレートと&#x200B;*コンポーネント*&#x200B;は、両方とも標準で提供されています。または、既存のコンポーネントを拡張するか、グリーンフィールド（詳細）を作成することで、開発者がカスタム開発できます。 ** テンプレートとコン ** ポーネントを使用すると、AEMオーサーがドラッグ&amp;ドロップして、魅力的で関連性の高いエクスペリエンスを作成できます。

1. [コンポーネントの作成](/help/sites-developing/components.md)
1. [テンプレートの作成](/help/sites-developing/templates.md)

以上の 2 つの手順を確実に理解したら、次の各ページを参照してください。

1. [AEM Mobile アプリの構造](/help/mobile/phonegap-structure-an-app.md)
1. [AEM Mobile アプリの詳細な構造](/help/mobile/phonegap-apps-arch.md)
1. [既存のアプリの AEM Mobile 対応](/help/mobile/phonegap-adding-content-to-imported-app.md)

## 次の手順 {#the-next-steps}

1. [AEM Mobile アプリを使ってみる](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツを管理する](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションをビルドする](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics でアプリケーションのパフォーマンスをトラッキングする](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target でパーソナライズされたアプリケーションエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [重要なメッセージをユーザーに送信する](/help/mobile/phonegap-push-notifications.md)
