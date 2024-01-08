---
title: Adobe Experience Manager Mobile On-Demand
description: 新しいAdobe Experience Manager(AEM) モバイルアプリエクスペリエンスを開始するには、コンテンツ編集の準備が整う前に、役割が連携する必要があります。 このページでは、AEM Mobile On-Demand サービスの概要について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 4%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>Adobe Experience Manager(AEM) をコンテンツ管理ソースとして使用していない場合は、 [AEM Mobile On-demand Services Help](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEMには、コンテンツをモバイルアプリケーションに統合するためのツールがいくつか用意されています。

次の図は、AEM Mobileと On-Demand Services の様々なコンポーネントがどのように組み合わされて、モバイルアプリにコンテンツを配信するかを示しています。

AEM Preflight アプリは、公開前にアプリとコンテンツをプレビューするテスト環境と見なすことができます。一方、AEM Mobile App は、配布用に構築された最終的なアプリです。

>[!NOTE]
>
>プリフライトアプリについて詳しくは、 [AEM Preflight アプリの使用](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) (AEM Mobile On-demand Servicesヘルプ )

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>上の図では、AEM Mobile On-demand Servicesへの一般的なデプロイメントシナリオには、AEMパブリッシュインスタンスは必要ありません。

## 新しいモバイルアプリの開始 {#starting-a-new-mobile-app}

AEM Mobileは、AEMプラットフォーム全体を構成する 1 つの柱に過ぎません。

新しいAEM Mobileアプリエクスペリエンスを開始するには、コンテンツ編集の準備が整う前に、複数の役割を組み合わせる必要があります。 次の役割は、AEM Mobileアプリケーションの作成の出発点となります。

* **管理者**
* **開発者**
* **作成者**

>[!NOTE]
>
>AEM Mobileを操作し、この入門ガイドの手順に従う前に、AEMに関する知識が必要です。 AEMの基本を学ぶ [ここ](/help/sites-deploying/deploy.md).

### AEM Mobile Application Dashboard について {#understanding-the-aem-mobile-application-dashboard}

役割と責任を理解する前に、ユーザーは **AEM Mobile Control Center** または **アプリケーションダッシュボード**. クリック [ここ](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

### AEM 管理者 {#aem-administrator}

An ***AEM administrator*** は、作成ウィザードを使用してアプリを作成するか、既存のアプリケーションを読み込むことで、AEM Mobileカタログにアプリケーションを追加します。 AEM Mobileを使用してアプリを作成するAEM管理者 *作成ウィザード* 通常は、Adobeの標準の参照サンプルから目的のアプリテンプレートを 1 つ選択するか、（通常は） *AEM開発者。*

AEM管理者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを実行します。

* [AEM Mobileの設定](/help/mobile/aem-mobile-setup.md)
* [ユーザーおよびユーザーグループの設定](/help/mobile/aem-mobile-configure-users.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [コンテンツサービスの管理](/help/mobile/developing-content-services.md)

管理者の役割と責任の使用を開始するには、 [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md).

## AEM Developer {#aem-developer}

An **AEM developer** は、カスタムの Web テンプレートおよびコンポーネントを拡張および作成して、AEMオーサーを使用して美しく魅力的なモバイルエクスペリエンスを作成できます。 これらのテンプレートとコンポーネントは、モバイルアプリの世界に最適化されているだけでなく、デバイスとAEMサーバー（任意のリモートサーバー）の両方とオムニチャネルサービスエンドポイントとの通信も可能です。 AEMの組み込みコンテンツエディターは、 *AEM Authors* ：アプリ内で、他のAdobe Experience Cloudとの統合を含む、リッチで関連性の高いエクスペリエンスを作成します。

AEM開発者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のタスクを実行します。

* [アプリのテンプレートとコンポーネント](/help/mobile/app-templates-and-components1.md)
* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [コンテンツプロパティとコンテンツの書き出し](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile Content Services の開発](/help/mobile/developing-content-services.md)

開発者の役割と責務の概要については、 [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM developer&#39;s* の役割は、テンプレートとコンポーネントの開発で始まったり終わったりしません。 An *AEM developer* では、標準の参照実装サンプルを単に拡張するのではなく、まったく新しいアプリを作成できます。

## AEM オーサー {#aem-author}

An ***AEM Author* ( または *マーケター*)**は、カスタムで開発または標準搭載のテンプレートおよびコンポーネントを使用して、ページの追加と編集、コンポーネントのドラッグ&amp;ドロップ、DAM からのすべてのタイプのメディア（画像、ビデオ、テキストフラグメント）の追加をおこないます。 AEMの組み込みコンテンツエディターは、 *AEM Authors* ：アプリ内で、他のAdobe Experience Cloudとの統合を含む、リッチで関連性の高いエクスペリエンスを作成します。

AEMの作成者は、AEM Mobile On-demand Servicesを使用してアプリを作成する際に、次のトピックを理解する必要があります。

* [AEM Mobile アプリケーションのダッシュボード](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [アプリケーションの作成および設定アクション](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [クラウド設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [コンテンツ管理](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [コンテンツサービスの概要](/help/mobile/develop-content-as-a-service.md)

作成者の役割と責務の概要については、 [AEM Mobile On-demand Servicesアプリ用のAEMコンテンツのオーサリング](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>また、AEMの作成者は、権限の設定、カードとレイアウトの作成、プッシュ通知の送信も担当します。 また、コンテンツのオーサリング方法、記事とコレクションの管理、AEM Mobileでのバナー、カード、レイアウトの作成について詳しくは、 [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
