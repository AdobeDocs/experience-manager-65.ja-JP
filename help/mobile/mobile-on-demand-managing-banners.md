---
title: バナーの管理
seo-title: Managing Banners
description: バナーは、通常、グラフィカルなプロモーションリンクを表します。 このページでは、この機能について詳しく見ていきます。
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 5%

---

# バナーの管理{#managing-banners}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

コンテンツ管理アクションは、アプリケーション内のコンテンツの作成と管理に役立つ構成要素です。 アプリケーション内のコンテンツに対して、次のアクションが実行されます。

## バナーの概要 {#banners-overview}

バナーは、通常、グラフィカルなプロモーションリンクを表します。

>[!NOTE]
>
>AEM Mobileアプリの次のトピックについては、オンラインヘルプの次のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/digital-publishing-solution/help/design-app.html)
>
>* [バナーの作成](https://helpx.adobe.com/digital-publishing-solution/help/creating-banners.html)
>

## バナーの作成 {#creating-a-banner}

記事を作成する一般的なワークフローは次のとおりです。

1. 選択 **モバイル** サイドレールから。
1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **バナーを管理** タイル。
1. ウィザードの各手順を実行して、新しいバナーの作成を続行します。
1. 準備が整ったら、「 **作成**.
1. 新しいバナーが **バナーを管理** タイル。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 新しいバナーの読み込み {#importing-a-new-banner}

既存の Mobile On-Demand コンテンツは、Mobile On-Demand からAEMにダウンロード（読み込み）できます。 これにより、ローカルのコンテンツの編集と表示が可能になります。

>[!NOTE]
>
>読み込み時に画像は含まれません。

新しい記事を読み込むためのワークフロー

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. の右上隅にある下向き矢印をクリックします。 **バナーを管理** タイルとバナーを読み込むを選択します。
1. クリック **バナーを読み込み** ダイアログで、「閉じる」を選択します。
1. Mobile On-Demand の記事が **バナーを管理** タイル。

>[!CAUTION]
>
>最初に Mobile On-Demand 接続を関連付けます。

## バナーの編集 {#editing-a-banner}

組み込みのAEMドラッグ&amp;ドロップエディターを使用して、記事を追加または変更します。 テキストや画像などのコンポーネントを追加/削除できます。 DAM Assets からの画像を挿入できます。

>[!CAUTION]
>
>AEMで作成されたバナーのみ、エディターで開くことができます。

記事を編集するワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 「**バナーを管理**」タイルで、バナーを管理するAEMをソースとするバナーを選択します。
1. リスト表示でハイライト表示されたバナーをクリックして、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、バナーのコンテンツ（原稿、画像、テキストなど）をドラッグします。

### バナー内のメタデータの表示と編集 {#viewing-and-editing-the-metadata-within-a-banner}

バナーには、タイトル、説明、画像など、多数のプロパティがあります。 このアクションは、これらのプロパティを表示および変更するために使用します。 オプションで、保存時にこれらの変更を Mobile On-Demand にアップロードできます。

記事を表示または編集する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. 次の中からバナーを選択： **バナーを管理** タイル。

1. アクションバーから「**プロパティ**」を選択します。
1. その記事で使用可能なすべてのメタデータを表示します。
1. 必要に応じてメタデータを編集し、「 」をクリックします。 **保存** 完了したら、
1. オプションで、変更内容を直ちに Mobile On-Demand にアップロードします。

## バナーのアップロード {#uploading-a-banner}

アップロードアクションは、選択したコンテンツをコピーして Mobile On-Demand プロジェクトに追加します。 既存の Mobile On-Demand コンテンツは、新しいバージョンに置き換えられます。

バナーをアップロードする一般的なワークフロー：

1. 送信者 **モバイル**」で、カタログから Mobile On-Demand アプリを選択します。
1. Adobe Analytics の **バナーを管理** タイルで、Mobile On-Demand にアップロードするバナーを選択します。
1. 必要に応じて、リスト表示からバナーを追加します。
1. 選択 **アップロード** アクションバーから、ダイアログの「アップロード」をクリックします。
1. バナーが Mobile On-Demand にアップロードされました。

![chlimage_1-7](assets/chlimage_1-7.gif)

## バナーの削除 {#deleting-a-banner}

この操作を実行すると、選択したバナーが Mobile On-Demand から削除され、必要に応じてローカルのAEMインスタンスからも削除されます。

バナーを削除する一般的なワークフロー：

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. で削除するバナーを選択します。 **バナーを管理** タイル。
1. リストで選択されていることを確認します（必要に応じて、削除する他を選択します）。
1. クリック **削除** をクリックします。
1. AEMと Mobile On-Demand からを削除する場合はオンにします。
1. 「**削除**」をクリックします。
1. これで、バナーがリストから削除されました。

### 次の手順 {#the-next-steps}

バナーの管理について学習した後は、

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開/非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
