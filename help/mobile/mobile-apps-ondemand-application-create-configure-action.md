---
title: アプリケーションの作成および設定アクション
seo-title: Application Create and Configuration Actions
description: 多くの場合、アプリを作成することは、AEM Mobile On-Demand コンテンツを作成および管理するための最初の手順です。 このページでは、この機能について詳しく見ていきます。
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 8%

---

# アプリケーションの作成および設定アクション{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

## On-Demand アプリケーションの作成 {#creating-an-on-demand-application}

アプリの作成は、AEM Mobile On-Demand コンテンツの作成と管理のための最初の手順です。多くの場合、AEM管理者レベルで実行されます。 これは、モバイルデバイスで表示可能なコンテンツシェルを表し、作成者が作成したコンテンツ（記事、画像、コレクションなど）を表示する準備が整います。

アプリの詳細は、ダッシュボードまたはAEM Mobileコントロールセンターで確認できます。

>[!NOTE]
>
>ダッシュボードは、アプリのコンテンツ、メタデータ、AEM Mobile On-Demand 接続ステータスの概要を示す一連の便利なタイルです。
>
>詳しくは、 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 」を参照してください。

**オンデマンドアプリを作成するには：**

1. 選択 **モバイル** サイドレールから。
1. 選択 **アプリ** をクリックします。
1. クリック **作成** を選択し、 **アプリ** 」をドロップダウンから選択します。
1. 「モバイルアプリ」テンプレートを選択し、 **次へ**.
1. 次のようなアプリのプロパティを入力します。 **タイトル**, **名前**, **説明**.
1. 「**次へ**」をクリックします。
1. 既知の場合は、クラウド設定の詳細を入力し、それ以外の場合は「 **作成**.
1. クリック **完了** 新しいAEM Mobileアプリをカタログに表示します。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>このプロセスにより、AEMでアプリインスタンスを作成できます。

## アプリテンプレートの使用 {#using-app-templates}

アプリテンプレートを使用すると、AEM内での新しいアプリの作成に使用される、デベロッパーが作成した既存のデザインを簡単に活用できます。

アプリテンプレートとは これは、アプリのベースラインまたは基盤を表すページテンプレートおよびコンポーネントの集まりと考えてください。
別のアプリのテンプレートに基づいて新しいアプリを作成する場合、作成元のアプリを表す開始点を持つアプリが表示されます。

この機能を利用するには、既存のモバイルアプリテンプレート（またはアプリテンプレートを持つアプリ）がインストールされている必要があります。

### 次のステップ {#the-next-step}

アプリケーションダッシュボードから On-Demand アプリを作成したら、次の手順は、アプリをクラウド設定に関連付けることです。

詳しくは、 [アプリをクラウド設定に関連付け](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) を参照してください。

### 先に進む {#getting-ahead}

オンデマンドアプリケーションの作成と、そのアプリのクラウド設定への関連付けについて詳しくは、 [コンテンツ管理アクション](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**コンテンツ管理アクション** 次のコンテンツの作成と管理を含みます。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEM Mobile On-demand Services向けAEMコンテンツの開発](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Servicesを使用するコンテンツの管理](/help/mobile/aem-mobile.md)
