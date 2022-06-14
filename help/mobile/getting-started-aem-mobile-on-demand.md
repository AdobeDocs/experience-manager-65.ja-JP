---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 新しい AEM Mobile アプリエクスペリエンスを開始し、コンテンツを編集できるようになるまでには、複数の役割を持つメンバーが一体となって作業することが必要です。このページでは、AEM Mobile On-demand Services の概要について説明します。
seo-description: Starting a new AEM Mobile app experience requires a cohesion of roles before it is ready for content editing. Follow this page to get started with AEM mobile On-Demand services.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 52%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

>[!NOTE]
>
>AEMをコンテンツ管理ソースとして使用していない場合は、 [AEM Mobile On-demand Services Help](https://helpx.adobe.com/jp/digital-publishing-solution/topics.html).

AEM には、コンテンツをモバイルアプリに統合するための複数のツールがあります。

以下の図に、AEM Mobile と On-Demand Services の様々なコンポーネントがどのように連携してモバイルアプリにコンテンツを配信するかを示します。

AEM Preflight アプリは、アプリおよびコンテンツを公開前にプレビューするテスト環境です。AEM Mobile アプリは、配信用に最終的にビルドされるアプリです。

>[!NOTE]
>
>プリフライトアプリについて詳しくは、 [AEM Preflight アプリの使用](https://helpx.adobe.com/jp/digital-publishing-solution/help/preflight-app.html) (AEM Mobile On-demand Servicesヘルプ )

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>上の図の AEM パブリッシュインスタンスは、AEM Mobile On-Demand Services への通常のデプロイシナリオでは必要ありません。

## 新しい Mobile アプリの開始 {#starting-a-new-mobile-app}

AEM Mobile は、完全な AEM プラットフォームを構成する 1 つの柱に過ぎません。

新しい AEM Mobile アプリエクスペリエンスを開始し、コンテンツを編集できるようになるまでには、複数の役割を持つメンバーが一体となって作業することが必要です。以下の役割は、新しい AEM Mobile アプリケーションを作成する開始点となります。

* **管理者**
* **開発者**
* **作成者**

>[!NOTE]
>
>AEM Mobile を操作して、この使用の手引きに記載された手順を実行する前に、ユーザーは AEM について十分に理解しておく必要があります。AEM の基本については[こちら](/help/sites-deploying/deploy.md)を参照してください。

### AEM Mobile アプリケーションダッシュボードについて {#understanding-the-aem-mobile-application-dashboard}

役割と責任を理解する前に、ユーザーは **AEM Mobile Control Center** または **アプリケーションダッシュボード**. 詳しくは、[こちら](/help/mobile/mobile-apps-ondemand-application-dashboard.md)を参照してください。

### AEM 管理者 {#aem-administrator}

An ***AEM administrator*** は、作成ウィザードを使用して新しいアプリを作成するか、既存のアプリを読み込むことで、AEM Mobileカタログに新しいアプリを追加します。 AEM Mobileを使用して新しいアプリを作成するAEM管理者 *作成ウィザード* 通常は、あらかじめ用意されている参照サンプルから目的のアプリテンプレートを 1 つ選択するか、（ほとんどの場合は） *AEM開発者。*

AEM 管理者は、AEM Mobile On-Demand Services を使用してアプリを作成する際に以下のタスクを担当します。

* [AEM Mobile の設定](/help/mobile/aem-mobile-setup.md)
* [ユーザーとユーザーグループの設定](/help/mobile/aem-mobile-configure-users.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)

管理者の役割と責任の使用を開始するには、 [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md).

## AEM 開発者 {#aem-developer}

An **AEM developer** は、カスタムの Web テンプレートおよびコンポーネントを拡張して作成することで、AEM オーサーインスタンスを活用して美しく魅力的なモバイルエクスペリエンスを作成できます。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけではありません。ただし、デバイスとAEMサーバー（任意のリモートサーバー）の両方をオムニチャネルサービスエンドポイントに通信します。 AEMの組み込みコンテンツエディターは、 *AEM 作成者* ：アプリ内で、他のAdobe Marketing Cloudとの統合を含む、豊富で関連性の高いエクスペリエンスを作成します。

AEM 開発者は、AEM Mobile On-Demand Services を使用してアプリを作成するときに以下のタスクを担当します。

* [アプリのテンプレートとコンポーネント](/help/mobile/app-templates-and-components1.md)
* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [コンテンツプロパティとコンテンツの書き出し](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile コンテンツサービスの開発](/help/mobile/developing-content-services.md)

開発者の役割と責務の概要については、 [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM developer&#39;s* の役割は、テンプレートとコンポーネントの開発で始まったり終わったりしません。 An *AEM developer* では、標準の参照実装サンプルを単に拡張するのではなく、まったく新しいアプリを作成できます。

## コンテンツ作成者 {#aem-author}

An ***AEM オーサー* ( または *マーケター*)**は、カスタムで開発または標準搭載のテンプレートおよびコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント）の追加をおこないます。 AEMの組み込みコンテンツエディターは、 *AEM 作成者* ：アプリ内で、他のAdobe Marketing Cloudとの統合を含む、豊富で関連性の高いエクスペリエンスを作成します。

AEM 作成者は、AEM Mobile On-Demand Services を使用してアプリを作成する場合、以下のトピックについて理解しておく必要があります。

* [AEM Mobile アプリケーションのダッシュボード](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [クラウド設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [コンテンツサービス概要](/help/mobile/develop-content-as-a-service.md)

作成者の役割と責務の概要については、 [AEM Mobile On-demand Servicesアプリ用AEMコンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>また、AEM 作成者は、権利付与の設定、カードおよびレイアウトの作成、プッシュ通知の送信も担当します。AEM Mobile でのコンテンツのオーサリング、記事およびコレクションの管理、バナー、カード、レイアウトの作成方法について詳しくは、[AEM Mobile On-Demand ポータル](https://helpx.adobe.com/jp/digital-publishing-solution/topics.html#dynamicpod_reference_2)を参照してください。
