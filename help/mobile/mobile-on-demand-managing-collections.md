---
title: コレクションの管理
description: コレクションとは、カバーのテーマに適した記事やバナーなどのコンテンツがいっぱいになった、適切に定義されたグループです。 このページでは、この機能について詳しく見ていきます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 0b4aa1a4-449a-4882-8f7c-3ceea6ac7f83
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 4%

---

# コレクションの管理{#managing-collections}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

コンテンツ管理アクションは、アプリケーション内のコンテンツの作成と管理に役立つ構成要素です。 アプリケーション内のコンテンツに対して、次のアクションが実行されます。

## コレクションの概要 {#collections-overview}

コレクションは、適切に定義された *バケット* カバーのテーマに合った記事やバナーなどのコンテンツがいっぱいになっています。

>[!NOTE]
>
>AEM Mobileアプリの次のトピックについては、オンラインヘルプの次のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [コレクションの管理](https://helpx.adobe.com/digital-publishing-solution/help/creating-collections.html)
>

## コレクションの作成 {#creating-a-collection}

コレクションを作成する一般的なワークフローを次に示します。

1. 選択 **モバイル** サイドレールから。
1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **コレクションを管理** タイル。
1. ウィザードの各手順を実行し、新しい記事の作成を続行します。
1. 準備が整ったら、「 **作成**.
1. 新しい記事が **コレクションを管理** タイル。

![chlimage_1-1](assets/chlimage_1-1.gif)

## 新しいコレクションの読み込み {#importing-a-new-collection}

既存の Mobile On-Demand コンテンツは、Mobile On-Demand からAEMにダウンロード（読み込み）できます。 これにより、ローカルのコンテンツの編集と表示が可能になります。

>[!NOTE]
>
>読み込み時に画像は含まれません。

新しいコレクションを読み込むためのワークフロー

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **コレクションを管理** タイルに表示され、「コレクションを読み込む」を選択します。
1. クリック **コレクションを読み込む** ダイアログで、「閉じる」を選択します。
1. Mobile On-Demand コレクションが **コレクションを管理** タイル。

>[!CAUTION]
>
>最初に Mobile On-Demand 接続を関連付ける必要があります。

## コレクションの編集 {#editing-a-collection}

組み込みのAEMドラッグ&amp;ドロップエディターを使用して、記事を追加または変更します。 テキストや画像などのコンポーネントを追加/削除できます。 DAM Assets からの画像を挿入できます。

コレクションを編集するワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 次の場所からAEMソースの記事を選択 **コレクションを管理** タイル。
1. リスト表示でハイライト表示されたコレクションをクリックして、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、コレクションのコンテンツ（原稿、画像、テキストなど）をドラッグします。

### コレクション内のメタデータの表示と編集 {#viewing-and-editing-the-metadata-within-a-collection}

コレクションには、タイトル、説明、画像などの多数のプロパティがあります。 このアクションは、これらのプロパティを表示および変更するために使用します。 オプションで、保存時にこれらの変更を Mobile On-Demand にアップロードできます。

コレクションを表示/編集する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 次の中からコレクションを選択： **コレクションを管理** タイル。

1. アクションバーから「**プロパティ**」を選択します。
1. その記事で使用可能なすべてのメタデータを表示します。
1. 必要に応じてメタデータを編集し、「 」をクリックします。 **保存** 完了したら、
1. オプションで、変更内容を直ちに Mobile On-Demand にアップロードします。

## コレクションのアップロード {#uploading-a-collection}

アップロードアクションは、選択したコンテンツをコピーして Mobile On-Demand プロジェクトに追加します。 既存の Mobile On-Demand コンテンツは、新しいバージョンに置き換えられます。

コレクションをアップロードする一般的なワークフロー：

1. 送信者 **モバイル**」で、カタログから Mobile On-Demand アプリを選択します。
1. Adobe Analytics の **コレクションを管理** タイルで、Mobile On-Demand にアップロードする記事を選択します。
1. 必要に応じて、リスト表示からコレクションを追加します。
1. 選択 **アップロード** アクションバーから、ダイアログの「アップロード」をクリックします。
1. コレクションが Mobile On-Demand にアップロードされました。

## コレクションの削除 {#deleting-a-collection}

この操作を実行すると、選択したコレクションが Mobile On-Demand から削除され、必要に応じてローカルのAEMインスタンスからも削除されます。

コレクションを削除する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. で削除する記事を選択します。 **コレクションを管理** タイル。
1. リストで選択されていることを確認します（必要に応じて、削除する他を選択します）。
1. クリック **削除** をクリックします。
1. AEMおよび Mobile On-Demand から削除する場合はオンにします。
1. 「**削除**」をクリックします。
1. コレクションがリストから削除されました。

## コレクションへのコンテンツの追加 {#adding-content-to-collections}

コレクションは基本的に関連コンテンツのカテゴリです。 記事やバナーなどのコンテンツを、アプリケーションのナビゲーション構造を定義するパッケージにまとめます。 コレクションはネストできます。

>[!NOTE]
>
>コンテンツをコレクションに追加する前に、Mobile On-Demand にアップロードする必要があります。

コレクションは基本的に関連コンテンツのカテゴリです。コレクションは、記事やバナーなどのコンテンツをまとめて、アプリケーションのナビゲーション構造を定義するパッケージにまとめます。 コレクションはネストできます。

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 以前にアップロードした記事（またはバナー/コレクション）を選択
1. アクションバーの「追加」を選択します。
1. ダイアログから、以前にアップロードしたコレクションを選択します。
1. クリック **更新** をクリックして、コレクションにコンテンツを追加します。

![chlimage_1-2](assets/chlimage_1-2.gif)

### 次の手順 {#the-next-steps}

コレクションの管理について詳しくは、

* [バナーの管理](/help/mobile/mobile-on-demand-managing-banners.md)
* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開/非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
