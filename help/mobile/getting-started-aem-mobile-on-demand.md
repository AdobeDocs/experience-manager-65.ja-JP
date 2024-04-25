---
title: Adobe Experience Manager Mobile オンデマンド
description: 新しいAdobe Experience Manager（AEM）モバイルアプリエクスペリエンスを開始するには、コンテンツ編集の準備を整える前に、いくつかの役割で協力する必要があります。 このページでは、AEM Mobile On-Demand サービスの使用を開始する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 7%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>Adobe Experience Manager（AEM）をコンテンツ管理ソースとして使用していない場合は、を参照してください [AEM Mobile On-demand Services ヘルプ](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEMには、コンテンツをモバイルアプリケーションに統合するためのいくつかのツールが用意されています。

次の図は、AEM Mobileと On-Demand Services の様々なコンポーネントを組み合わせて、モバイルアプリにコンテンツを配信する方法を示しています。

AEM Preflight アプリは、公開前にアプリとコンテンツをプレビューするテスト環境と見なすことができます。一方、AEM Mobile アプリは、配布用に構築された最終的なアプリです。

>[!NOTE]
>
>Preflight アプリについて詳しくは、 [AEM Preflight アプリの使用](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) （AEM Mobile On-demand Services ヘルプ）。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>上の図では、AEM Mobile On-demand Servicesへの一般的なデプロイメントシナリオにAEM パブリッシュインスタンスは必要ありません。

## 新しいモバイルアプリの開始 {#starting-a-new-mobile-app}

AEM Mobileは、AEM プラットフォーム全体を構成する 1 つの柱にすぎません。

AEM Mobile アプリの新しいエクスペリエンスを開始するには、コンテンツ編集の準備を整える前に、いくつかの役割で協力する必要があります。 AEM Mobile アプリケーションを作成するための開始点となる役割は次のとおりです。

* **管理者**
* **開発者**
* **作成者**

>[!NOTE]
>
>AEM Mobileを使用してこの入門ガイドの手順に従う前に、AEMについて理解しておく必要があります。 AEMの基本について説明します [こちら](/help/sites-deploying/deploy.md).

### AEM Mobile Application Dashboard について {#understanding-the-aem-mobile-application-dashboard}

役割と責務を理解する前に、ユーザーは次の点に関する十分な知識が必要です **AEM Mobileコントロールセンター** または **アプリケーション ダッシュボード**. クリック [こちら](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### AEM 管理者 {#aem-administrator}

An ***AEM管理者*** は、作成ウィザードを使用してアプリを作成するか、既存のアプリケーションを読み込むことにより、AEM Mobile カタログにアプリケーションを追加する役割を担っています。 AEM Mobileを使用してアプリを作成するAEM管理者 *作成ウィザード* 通常は、Adobeの標準提供の参照サンプルまたは（通常は）によって作成されたカスタムアプリテンプレートから、目的のアプリテンプレートの 1 つを選択します。 *AEM開発者。*

AEM管理者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを担当します。

* [AEM Mobileのセットアップ](/help/mobile/aem-mobile-setup.md)
* [ユーザーおよびユーザーグループの設定](/help/mobile/aem-mobile-configure-users.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)

管理者の役割と責任を開始するには、を参照してください。 [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md).

## AEM開発者 {#aem-developer}

An **AEM開発者** は、カスタム web テンプレートおよびコンポーネントを拡張して作成するので、*AEM オーサー*は美しく魅力的なモバイルエクスペリエンスを作成できます。 これらのテンプレートとコンポーネントは、モバイルアプリ用に最適化されるだけでなく、デバイスとAEM サーバー（任意のリモートサーバー）の両方に通信して、オムニチャネルサービスのエンドポイントに提供されます。 AEMの組み込みコンテンツエディターの利用者 *AEM オーサー* Adobe Experience Cloudの他の部分との統合など、アプリ内で充実した適切なエクスペリエンスを作成できます。

AEM開発者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを担当します。

* [アプリのテンプレートとコンポーネント](/help/mobile/app-templates-and-components1.md)
* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [コンテンツのプロパティとコンテンツの書き出し](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile コンテンツサービスの開発](/help/mobile/developing-content-services.md)

開発者の役割と責任を開始するには、を参照してください。 [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM開発者* 役割の出発点や終了点は、テンプレートやコンポーネントの開発ではありません。 An *AEM開発者* 標準提供のリファレンス実装サンプルを単に拡張するのではなく、まったく新しいアプリを作成できます。

## AEM オーサー {#aem-author}

An ***AEM オーサー* （または *マーケター*）**は、カスタムで開発された、または標準のテンプレートおよびコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、画像、ビデオ、テキストフラグメント（コンテンツフラグメント）など、DAM からのすべてのタイプのメディアの追加を行います。 その後、AEMの組み込みコンテンツエディターはによって使用されます *AEM オーサー* Adobe Experience Cloudの他の部分との統合など、アプリ内で充実した適切なエクスペリエンスを作成できます。

AEM オーサーは、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のトピックを理解する必要があります。

* [AEM Mobile アプリケーションのダッシュボード](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [クラウド設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [コンテンツサービスの概要](/help/mobile/develop-content-as-a-service.md)

作成者の役割と責任の基本を学ぶには、を参照してください。 [AEM Mobile On-demand Services アプリケーション用AEM コンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>また、AEM オーサーは、使用権限の設定、カードとレイアウトの作成、プッシュ通知の送信も担当します。 また、AEM Mobileでのコンテンツのオーサリング、記事とコレクションの管理、バナー、カード、レイアウトの作成についても説明します。 [AEM Mobile オンデマンドポータル](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
