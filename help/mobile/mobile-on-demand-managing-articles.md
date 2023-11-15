---
title: 記事の管理
description: このページでは、記事の作成と管理について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: ea6c8aa3-f86e-4878-8550-fe1662f10696
source-git-commit: 69a249e63e2e6b96ba08f9846baa3e91d42b865f
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 3%

---

# 記事の管理{#managing-articles}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

コンテンツ管理アクションは、アプリケーション内で記事を作成および管理するのに役立つ構築ブロックです。 アプリケーション内の記事に対して、次のアクションが実行されます。

## 記事の概要 {#articles-overview}

記事は、テキストベースを表し、情報を伝えるアートを表します。

>[!NOTE]
>
>AEM Mobileアプリの次のトピックについては、オンラインヘルプの次のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [記事の管理](https://helpx.adobe.com/digital-publishing-solution/help/creating-articles.html)
>

## 記事の作成 {#creating-an-article}

記事を作成する一般的なワークフローは次のとおりです。

1. 選択 **モバイル** サイドレールから。
1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **記事を管理** タイル。
1. 記事テンプレートを選択し、「 **次へ**.
1. ウィザードの各手順を実行し、新しい記事の作成を続行します。
1. 準備が整ったら、「 **作成**.
1. 新しい記事が **記事を管理** タイル。

## 新しい記事の読み込み {#importing-a-new-article}

既存の Mobile On-Demand コンテンツは、Mobile On-Demand からAEMにダウンロード（読み込み）できます。 これにより、ローカルのコンテンツの編集と表示が可能になります。

>[!NOTE]
>
>読み込み時に画像は含まれません。

新しい記事を読み込むためのワークフロー

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **記事を管理** タイルに表示され、「記事を読み込む」を選択します。
1. クリック **記事を読み込む** ダイアログで、「閉じる」を選択します。
1. Mobile On-Demand の記事が **記事を管理** タイル。

>[!CAUTION]
>
>最初に Mobile On-Demand 接続を関連付ける必要があります。

![chlimage_1-3](assets/chlimage_1-3.gif)

## 記事の編集 {#editing-an-article}

組み込みのAEMドラッグ&amp;ドロップエディターを使用して、記事を追加または変更します。 テキストや画像などのコンポーネントを追加/削除できます。 DAM Assets からの画像を挿入できます。

>[!CAUTION]
>
>AEMで作成された記事のみ、エディターで開くことができます。

記事を編集するワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 次の場所からAEMソースの記事を選択 **記事を管理** タイル。
1. リスト表示でハイライト表示された記事をクリックして、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、記事のコンテンツ（原稿、画像、テキストなど）をドラッグします。

### 記事内のメタデータの表示と編集 {#viewing-and-editing-the-metadata-within-an-article}

記事やバナーなどのコンテンツには、タイトル、説明、画像などの多数のプロパティがあります。 このアクションは、これらのプロパティを表示および変更するために使用します。 オプションで、保存時にこれらの変更を Mobile On-Demand にアップロードできます。

記事を表示または編集する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 次の中から記事を選択します： **記事を管理** タイル。

1. 選択 **プロパティを表示** をクリックします。
1. その記事で使用可能なすべてのメタデータを表示します。
1. 必要に応じてメタデータを編集し、「 」をクリックします。 **保存** 完了したら、
1. オプションで、変更内容を直ちに Mobile On-Demand にアップロードします。

## 記事のアップロード {#uploading-an-article}

アップロードアクションは、選択したコンテンツをコピーして Mobile On-Demand プロジェクトに追加します。 既存の Mobile On-Demand コンテンツは、新しいバージョンに置き換えられます。

記事をアップロードする一般的なワークフロー：

1. 送信者 **モバイル**」で、カタログから Mobile On-Demand アプリを選択します。
1. Adobe Analytics の **記事を管理** タイルで、Mobile On-Demand にアップロードする記事を選択します。
1. 必要に応じて、リスト表示から他の記事を追加します。
1. 選択 **アップロード** アクションバーから、ダイアログの「アップロード」をクリックします。
1. 記事が Mobile On-Demand にアップロードされました。

![chlimage_1-4](assets/chlimage_1-4.gif)

## 記事の削除 {#deleting-an-article}

この操作を実行すると、選択したコンテンツが Mobile On-Demand から削除され、オプションでローカルのAEMインスタンスからも削除されます。

記事を削除する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. で削除する記事を選択します。 **記事を管理** タイル。
1. リストで選択されていることを確認します。必要に応じて、削除する他を選択します。
1. クリック **削除** をクリックします。
1. AEMと Mobile On-Demand からを削除する場合はオンにします。
1. 「**削除**」をクリックします。
1. これで、記事がリストから削除されました。

![chlimage_1-5](assets/chlimage_1-5.gif)

### 次の手順 {#the-next-steps}

記事の管理について学習したら、

* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開/非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
