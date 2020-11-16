---
title: コレクションの管理
seo-title: コレクションの管理
description: コレクションは、カバーのテーマに適した記事やバナーなどのコンテンツを集めた、適切に定義されたグループです。このページでは、この機能について詳しく見ていきます。
seo-description: コレクションは、カバーのテーマに適した記事やバナーなどのコンテンツを集めた、適切に定義されたグループです。このページでは、この機能について詳しく見ていきます。
uuid: 1d2e9769-d2cc-4d43-a428-e962a51eb5d0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: 64c6d198-983f-4a52-9c83-560206363868
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 84%

---


# コレクションの管理{#managing-collections}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

コンテンツ管理アクションは、アプリケーション内でコンテンツを作成および管理するのに役立つ構築ブロックです。アプリケーション内のコンテンツに対して以下のアクションを実行します。

## コレクションの概要 {#collections-overview}

Collections represent a well defined *bucket* filled with content such as articles or banners that suits the cover&#39;s theme.

>[!NOTE]
>
>AEM Mobile アプリの以下のトピックについては、オンラインヘルプの以下のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/jp/digital-publishing-solution/help/design-app.html)
   >
   >
* [コレクションの管理](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-collections.html)

>



## コレクションの作成 {#creating-a-collection}

コレクションを作成する一般的なワークフローは以下のとおりです。

1. サイドレールから「**モバイル**」を選択します。
1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **コレクションを管理**&#x200B;タイルの右上隅にある下矢印をクリックします。
1. ウィザードの各ステップで必要な情報を入力して、新しいコレクションの作成を続行します。
1. 準備ができたら、「**作成**」をクリックします。
1. **コレクションを管理**&#x200B;タイルに新しいコレクションが表示されます。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 新しいコレクションの読み込み {#importing-a-new-collection}

既存の Mobile On-Demand コンテンツを Mobile On-Demand から AEM にダウンロードする（読み込む）ことができます。これにより、ローカルのコンテンツを編集および表示できます。

>[!NOTE]
>
>読み込みには画像は含まれません。

新しいコレクションを読み込むワークフローは以下のとおりです。

1. Mobileで、カタログからMobile On-Demand Appを選択します。
1. **コレクションを管理**&#x200B;タイルの右上隅にある下矢印をクリックして、「コレクションを読み込む」を選択します。
1. ダイアログで「**コレクションを読み込む**」をクリックし、「閉じる」をクリックします。
1. Your Mobile On-Demand collections now appear in the **Manage Collections** tile.

>[!CAUTION]
>
>最初に Mobile On-Demand の接続を関連付ける必要があります。

## コレクションの編集 {#editing-a-collection}

記事を追加または変更するには、組み込みの AEM ドラッグ＆ドロップエディターを使用します。テキストや画像などのコンポーネントを追加したり、削除したりすることができます。DAM アセットの画像を挿入することもできます。

コレクションを編集するワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. Select an AEM sourced article from the **Manage Collections** tile.
1. リスト表示で、ハイライトされたコレクションをクリックし、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、コレクションの内容（原稿、画像、テキストなど）をドラッグします。

### コレクション内のメタデータの表示および編集 {#viewing-and-editing-the-metadata-within-a-collection}

コレクションには、タイトル、説明、画像など多くのプロパティがあります。このようなプロパティを表示および変更するには、この操作を使用します。オプションで、保存時に Mobile On-Demand に変更内容をアップロードすることもできます。

コレクションを表示／編集する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. Choose a collection from the **Manage Collections** tile.

1. アクションバーから「**プロパティ**」を選択します。
1. コレクションの使用可能なすべてのメタデータを確認します。
1. 必要に応じてメタデータを編集し、終わったら「**保存**」をクリックします。
1. 必要に応じて、変更内容を即座にMobile On-Demandにアップロードします。

## コレクションのアップロード {#uploading-a-collection}

アップロード操作では、選択したコンテンツがコピーされ、 Mobile On-Demand プロジェクトに追加されます。既存の Mobile On-Demand コンテンツは新しいバージョンに置き換えられます。

コレクションをアップロードする一般的なワークフローは以下のとおりです。

1. From **Mobile**, choose your Mobile On-Demand app from the catalog.
1. In the **Manage Collections** tile, select an article for upload to Mobile On-Demand.
1. 必要に応じて、リスト表示からさらにコレクションを追加します。
1. アクションバーから「**アップロード**」を選択し、ダイアログで「アップロード」をクリックします。
1. コレクションがMobile On-Demandにアップロードされました。

## コレクションの削除 {#deleting-a-collection}

この操作により、選択したコレクションがMobile On-Demandから削除されます。また、オプションでローカルのAEMインスタンスからも削除されます。

コレクションを削除する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **コレクションを管理**&#x200B;タイルで、削除するコレクションを選択します。
1. 削除するコレクションがリスト内で選択されていることを確認します（必要に応じて、削除する他のコレクションを選択します）。
1. アクションバーから「**削除**」をクリックします。
1.  Mobile On-Demand だけでなく、AEM からも削除するかどうかを確認します。
1. 「**削除**」をクリックします。
1. コレクションがリストから削除されます。

## コレクションへのコンテンツの追加 {#adding-content-to-collections}

コレクションは基本的に、関連するコンテンツのカテゴリです。コレクションによって、アプリケーションのナビゲーション構造を定義するパッケージに記事やバナーなどのコンテンツが収集されます。コレクションはネスト可能です。

>[!NOTE]
>
>コンテンツをMobile On-Demandにアップロードしてから、コレクションに追加する必要があります。

コレクションは基本的に、関連するコンテンツのカテゴリです。コレクションによって、アプリケーションのナビゲーション構造を定義するパッケージに記事やバナーなどのコンテンツが収集されます。コレクションはネスト可能です。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 以前にアップロードした記事（またはバナー／コレクション）を選択します。
1. アクションバーから「追加」を選択します。
1. 以前にアップロードしたコレクションをダイアログから選択します。
1. 「**更新**」をクリックして、コレクションにコンテンツを追加します。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 次の手順 {#the-next-steps}

コレクションの管理について学習したら、以下を参照してください。

* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
