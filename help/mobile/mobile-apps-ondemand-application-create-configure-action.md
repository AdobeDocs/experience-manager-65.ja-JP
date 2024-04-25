---
title: アプリケーションの作成および設定アクション
description: アプリの作成は、多くの場合、AEM Mobile オンデマンド コンテンツを作成および管理するための最初のステップです。 詳しくは、このページを参照してください。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 11%

---

# アプリケーションの作成および設定アクション{#application-create-and-configuration-actions}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

## オンデマンドアプリケーションの作成 {#creating-an-on-demand-application}

アプリの作成は、多くの場合、AEM Mobile オンデマンド コンテンツを作成および管理するための最初のステップであり、AEM管理者レベルで行われます。 コンテンツシェルを表し、モバイルデバイスで表示可能で、作成者が作成したコンテンツ（記事、画像、コレクションなど）を表示する準備が整っています。

アプリの詳細は、ダッシュボードまたはAEM Mobile コントロールセンターで表示できます。

>[!NOTE]
>
>ダッシュボードは、アプリのコンテンツ、メタデータおよびAEM Mobile On-Demand 接続ステータスの概要を示す一連の便利なタイルです。
>
>参照： [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) を参照してください。

**オンデマンドアプリを作成するには：**

1. を選択 **モバイル** サイドパネルから。
1. を選択 **アプリ** ナビゲーションから。
1. クリック **作成** を選択して、 **アプリ** ドロップダウンから。
1. モバイルアプリテンプレートを選択し、 **次**.
1. 次のようなアプリプロパティを入力します **タイトル**, **名前**, **説明**.
1. 「**次へ**」をクリックします。
1. 既知の場合は、クラウド設定の詳細を入力し、既知の場合は **作成**.
1. クリック **完了** をクリックして、カタログに新しいAEM Mobile アプリを表示します。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>このプロセスにより、AEMでアプリインスタンスを作成できます。

## アプリテンプレートの使用 {#using-app-templates}

アプリテンプレートを使用すると、AEM内で新しいアプリを作成するために使用される、開発者が作成した既存のデザインを簡単に使用できます。

アプリテンプレートとは これは、アプリのベースラインまたは基盤を表すページテンプレートおよびコンポーネントのコレクションと考えることができます。
別のアプリのテンプレートに基づいてアプリを作成すると、そのアプリの作成元となったアプリを表す出発点を持つアプリが取得されます。

この機能を使用するには、既存のモバイルアプリテンプレート（またはアプリテンプレートがインストールされたアプリ）が必要です。

### 次のステップ {#the-next-step}

アプリケーションダッシュボードからオンデマンドアプリを作成したら、次にアプリをクラウド設定に関連付けます。

参照： [クラウド設定へのアプリの関連付け](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) を参照してください。

### 前に進む {#getting-ahead}

オンデマンドアプリケーションの作成と、そのアプリケーションのクラウド設定への関連付けについて詳しくは、以下を参照してください [コンテンツ管理アクション](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**コンテンツ管理アクション** 以下のコンテンツの作成と管理が含まれます。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEM Mobile On-demand Services用AEM コンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md)
