---
title: 記事の管理
seo-title: 記事の管理
description: このページでは、記事の作成と管理について説明します。
seo-description: このページでは、記事の作成と管理について説明します。
uuid: 72b86cd7-3016-41b6-a001-9dce4084e9db
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: b46058f9-4691-4fba-a656-0f8507875a79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 89%

---


# 記事の管理{#managing-articles}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

コンテンツ管理アクションは、アプリケーション内で記事を作成および管理するのに役立つ構築ブロックです。アプリケーション内の記事に対して、以下のアクションが実行されます。

## 記事の概要 {#articles-overview}

記事は、情報を伝えるためのアートと共に、テキストを表します。

>[!NOTE]
>
>AEM Mobile アプリの以下のトピックについては、オンラインヘルプの以下のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/jp/digital-publishing-solution/help/design-app.html)
   >
   >
* [記事の管理](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-articles.html)

>



## 記事の作成 {#creating-an-article}

記事を作成する一般的なワークフローは以下のとおりです。

1. サイドレールから「**モバイル**」を選択します。
1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **記事を管理**&#x200B;タイルの右上隅にある下矢印をクリックします。
1. 記事のテンプレートを選択し、「**次へ**」をクリックします。
1. ウィザードの各ステップで必要な情報を入力して、新しい記事の作成を続行します。
1. 準備ができたら、「**作成**」をクリックします。
1. **記事を管理**&#x200B;タイルに新しい記事が表示されます。

## 新しい記事の読み込み {#importing-a-new-article}

既存の Mobile On-Demand コンテンツを Mobile On-Demand から AEM にダウンロードする（読み込む）ことができます。これにより、ローカルのコンテンツを編集および表示できます。

>[!NOTE]
>
>読み込みには画像は含まれません。

新しい記事を読み込むワークフローは以下のとおりです。

1. Mobileで、カタログからMobile On-Demand Appを選択します。
1. **記事を管理**&#x200B;タイルの右上隅にある下矢印をクリックし、「記事を読み込む」を選択します。
1. ダイアログで「**記事を読み込む**」をクリックし、「閉じる」をクリックします。
1. Your Mobile On-Demand articles now appear in the **Manage Articles** tile.

>[!CAUTION]
>
>最初に Mobile On-Demand の接続を関連付ける必要があります。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 記事の編集 {#editing-an-article}

記事を追加または変更するには、組み込みの AEM ドラッグ＆ドロップエディターを使用します。テキストや画像などのコンポーネントを追加したり、削除したりすることができます。DAM アセットの画像を挿入することもできます。

>[!CAUTION]
>
>エディターで開くことができるのは、AEM で作成された記事のみです。

記事を編集するワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **記事を管理**&#x200B;タイルで、AEM で作成した記事を選択します。
1. リスト表示で、ハイライトされた記事をクリックし、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、記事の内容（原稿、画像、テキストなど）をドラッグします。

### 記事内のメタデータの表示および編集 {#viewing-and-editing-the-metadata-within-an-article}

記事やバナーのようなコンテンツには、タイトル、説明、画像などの多数のプロパティがあります。このようなプロパティを表示および変更するには、この操作を使用します。オプションで、保存時に Mobile On-Demand に変更内容をアップロードすることもできます。

記事を表示／編集する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. Choose an article from the **Manage Articles** tile.

1. アクションバーから「**プロパティを表示**」を選択します。
1. コレクションの使用可能なすべてのメタデータを確認します。
1. 必要に応じてメタデータを編集し、終わったら「**保存**」をクリックします。
1. 必要に応じて、変更内容を即座にMobile On-Demandにアップロードします。

## 記事のアップロード {#uploading-an-article}

アップロード操作では、選択したコンテンツがコピーされ、 Mobile On-Demand プロジェクトに追加されます。既存の Mobile On-Demand コンテンツは新しいバージョンに置き換えられます。

記事をアップロードする一般的なワークフローは以下のとおりです。

1. From **Mobile**, choose your Mobile On-Demand app from the catalog.
1. In the **Manage Articles** tile, select an article for upload to Mobile On-Demand.
1. 必要に応じて、リスト表示からさらに記事を追加します。
1. アクションバーから「**アップロード**」を選択し、ダイアログで「アップロード」をクリックします。
1. 記事が Mobile On-Demand にアップロードされます。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 記事の削除 {#deleting-an-article}

この操作では、選択したコンテンツが Mobile On-Demand から削除され、さらにオプションでローカルの AEM インスタンスからも削除されます。

記事を削除する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **記事を管理**&#x200B;タイルで、削除する記事を選択します。
1. 削除する記事がリスト内で選択されていることを確認します（必要に応じて、削除する他の記事を選択します）。
1. アクションバーから「**削除**」をクリックします。
1.  Mobile On-Demand だけでなく、AEM からも削除するかどうかを確認します。
1. 「**削除**」をクリックします。
1. 記事がリストから削除されます。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 次の手順 {#the-next-steps}

記事の管理について学習したら、以下を参照してください。

* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
