---
title: AEM PhoneGap の起動
description: Starterkit を使用して、Adobe Experience Manager Mobile開発の基本を実行する方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7d56b9f0-5aa5-4b68-a85e-7e80415cbc76
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 8%

---

# AEM PhoneGap の起動 {#starting-aem-phonegap}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

開発者向けに、まずは github のAdobe Experience Manager Mobile Starterkit を参照することをお勧めします

https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit

Starterkit を使用すると、AEM Mobileの開発の基本を簡単に説明できるので、作業を素早く進めることができます。 まず、プロジェクトの作成とガバナンスから始め、必要なツールをインストールし、Maven アーキタイプを定義します。次に、ビルド、デプロイしてから、独自のエクスペリエンスを作成します。

開発者は、PhoneGap を使用してAEM Mobile アプリケーションを試す際の出発点として、この例を使用できます。 Starterkit と参照アプリケーションを実行することで、豊富なモバイルアプリケーションを作成するための基本を明確に理解できます。

* の使用 [AEM PhoneGap スターターキット](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) AEM Mobileカタログに適したアプリを作成する。
* A [参照アプリ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 既存のアプリをAEM Mobileに移行する場合でも、新しく開始する場合でも、AEM Mobileの新機能の多くを示す完全なソースが作成されました。
* すべてのサンプルは、次の github で入手できます。 [https://github.com/Adobe-Marketing-Cloud-Apps](https://github.com/Adobe-Marketing-Cloud-Apps) また、Maven を使用したプロジェクトのブートストラップも含まれます。
* ほとんどの電話会議では、 [キッチン シンク チュートリアル](https://github.com/blefebvre/aem-phonegap-kitchen-sink)は GitHub にもあり、Apache Cordova ネイティブ拡張機能の使用に重点を置いています。

>[!NOTE]
>
>スターターキットに慣れる機会が得られたら、Adobe Experience Managerについて学ぶことが重要です *コンポーネントとテンプレート。*

## テンプレートとコンポーネント {#templates-and-components}

AEM *テンプレート* および *Components* 事業部門の所有者がカスタムエクスペリエンスを作成できるようにします。 両方*テンプレート*および *Components* は、すぐに使用できますが、既存のコンポーネントを拡張するか、グリーンフィールド（詳細）を作成して、開発者がカスタムで開発することもできます。 *テンプレート* および *Components* AEM オーサーはをドラッグ&amp;ドロップして、魅力的で関連性の高いエクスペリエンスを作成できます。

1. [コンポーネントの作成](/help/sites-developing/components.md)
1. [テンプレートの作成](/help/sites-developing/templates.md)

上記の 2 つの手順をよく理解したら、次の場所に移動します。

1. [AEM Mobile アプリケーションの構造](/help/mobile/phonegap-structure-an-app.md)
1. [AEM Mobile アプリの詳細な構造](/help/mobile/phonegap-apps-arch.md)
1. [既存のアプリは、AEM Mobileに対応していますか？](/help/mobile/phonegap-adding-content-to-imported-app.md)

## 次の手順 {#the-next-steps}

1. [AEM Mobile アプリのエクスペリエンスを開始](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツの管理](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションの構築](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobeモバイル分析を使用してアプリのパフォーマンスを追跡する](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Targetでパーソナライズされたアプリエクスペリエンスを提供する](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [ユーザーへの重要なメッセージの送信](/help/mobile/phonegap-push-notifications.md)
