---
title: AEM PhoneGap の起動
description: Adobe Experience Manager Mobile開発の基本を学ぶためにstarterkitを使用する方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7d56b9f0-5aa5-4b68-a85e-7e80415cbc76
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
source-wordcount: '424'
ht-degree: 3%
---
# AEM PhoneGap の起動 {#starting-aem-phonegap}

{{ue-over-mobile}}

開発者向けには、まずgithubのAdobe Experience Manager Mobile Starterkitを確認することから始めましょう

https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit

スターターキットでは、AEM Mobile開発の基本を順を追って説明することで、すばやく実行できます。 まず、プロジェクトの構築とガバナンス、必要なツールのインストール、Maven アーキタイプの定義、構築、デプロイ、独自のエクスペリエンスの作成から始まります。

開発者は、この例を、PhoneGapを使用してAEM Mobile アプリケーションを試す出発点として使用できます。 スターターキットとリファレンスアプリケーションを実行すると、リッチモバイルアプリケーションを作成するための基本をしっかりと理解できます。

* [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)を使用して、AEM Mobile カタログに適したアプリケーションを作成します。
* 既存のアプリをAEM Mobileに移行する場合でも、新たに開始する場合でも、AEM Mobileの新機能の多くを示すフルソースの[参照アプリ ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference)が作成されました。
* すべてのサンプルはgithub: [https://github.com/Adobe-Marketing-Cloud-Apps](https://github.com/Adobe-Marketing-Cloud-Apps)で確認でき、Mavenを使用してプロジェクトをブートストラップできます。
* ほとんどのカンファレンスでは、[Kitchen Sink チュートリアル ](https://github.com/blefebvre/aem-phonegap-kitchen-sink)を使用しています。このチュートリアルはGitHubでも利用でき、Apache Cordovaのネイティブ拡張機能の使用に焦点を当てています。

>[!NOTE]
>
>スターターキットに慣れたら、*Adobe Experience Manager コンポーネントとテンプレート*&#x200B;について学ぶことが重要です。

## テンプレートとコンポーネント {#templates-and-components}

AEM *テンプレート*&#x200B;および&#x200B;*コンポーネント*&#x200B;を使用すると、事業部門の担当者がカスタムエクスペリエンスを作成できます。 *テンプレート*&#x200B;と* コンポーネント *の両方は、すぐに使用できるか、既存のコンポーネントを拡張するか、グリーンフィールド（詳細）を作成することで、開発者が独自に開発できます。 *テンプレート*&#x200B;と&#x200B;*コンポーネント*&#x200B;は、AEM オーサーがドラッグ&amp;ドロップ操作で魅力的で関連性の高いエクスペリエンスを作成できるようにするものです。

1. [コンポーネントの作成](/help/sites-developing/components.md)
1. [テンプレートの作成](/help/sites-developing/templates.md)

上記の2つのステップをしっかりと理解したら、次のステップに進みます。

1. [AEM Mobile アプリの構造](/help/mobile/phonegap-structure-an-app.md)
1. [AEM Mobileアプリの構造](/help/mobile/phonegap-apps-arch.md)
1. [既存のアプリはAEM Mobileに対応していますか？](/help/mobile/phonegap-adding-content-to-imported-app.md)

## 次の手順 {#the-next-steps}

1. [AEM Mobile アプリ体験を開始する](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツを管理](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションを作成](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analyticsでアプリのパフォーマンスを追跡する](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Targetでパーソナライズされたアプリ体験を提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [ユーザーに重要なメッセージを送信する](/help/mobile/phonegap-push-notifications.md)
