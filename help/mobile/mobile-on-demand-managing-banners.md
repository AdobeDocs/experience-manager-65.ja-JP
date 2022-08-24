---
title: バナーの管理
seo-title: Managing Banners
description: バナーは、通常、グラフィカルなプロモーションリンクです。このページでは、この機能について詳しく見ていきます。
seo-description: Banners represent typically graphical promotional links. Follow this page to learn more.
uuid: 593fe2ef-84df-42e2-8a03-897fb67a896d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: fb1abaa0-9c02-4f20-aa7c-073def067452
exl-id: c65a24e6-3041-4774-aeed-8e188ea19b78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 85%

---

# バナーの管理{#managing-banners}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

コンテンツ管理アクションは、アプリケーション内でコンテンツを作成および管理するのに役立つ構築ブロックです。アプリケーション内のコンテンツに対して以下のアクションを実行します。

## バナーの概要 {#banners-overview}

バナーは、通常、グラフィカルなプロモーションリンクです。

>[!NOTE]
>
>AEM Mobile アプリの以下のトピックについては、オンラインヘルプの以下のリソースを参照してください。
>
>* [デザインに関する考慮事項](https://helpx.adobe.com/jp/digital-publishing-solution/help/design-app.html)
>
>* [バナーの作成](https://helpx.adobe.com/jp/digital-publishing-solution/help/creating-banners.html)
>


## バナーの作成 {#creating-a-banner}

バナーを作成する一般的なワークフローは以下のとおりです。

1. サイドレールから「**モバイル**」を選択します。
1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **バナーを管理**&#x200B;タイルの右上隅にある下矢印をクリックします。
1. ウィザードの各ステップで必要な情報を入力して、新しいバナーの作成を続行します。
1. 準備ができたら、「**作成**」をクリックします。
1. **バナーを管理**&#x200B;タイルに新しいバナーが表示されます。

![chlimage_1-6](assets/chlimage_1-6.gif)

## 新しいバナーの読み込み {#importing-a-new-banner}

既存の Mobile On-Demand コンテンツを Mobile On-Demand から AEM にダウンロードする（読み込む）ことができます。これにより、ローカルのコンテンツを編集および表示できます。

>[!NOTE]
>
>読み込みには画像は含まれません。

新しい記事を読み込むワークフローは以下のとおりです。

1. Mobile から、カタログから Mobile On-Demand アプリを選択します。
1. **バナーを管理**&#x200B;タイルの右上隅にある下矢印をクリックして、「バナーを読み込む」を選択します。
1. ダイアログで「**バナーを読み込む**」をクリックし、「閉じる」をクリックします。
1. Mobile On-Demand の記事が **バナーを管理** タイル。

>[!CAUTION]
>
>最初に Mobile On-Demand の接続を関連付ける必要があります。

## バナーの編集 {#editing-a-banner}

記事を追加または変更するには、組み込みの AEM ドラッグ＆ドロップエディターを使用します。テキストや画像などのコンポーネントを追加したり、削除したりすることができます。DAM アセットの画像を挿入することもできます。

>[!CAUTION]
>
>エディターで開くことができるのは、AEM で作成されたバナーのみです。

バナーを編集するワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 「**バナーを管理**」タイルで、バナーを管理するAEMを選択します。
1. リスト表示で、ハイライトされたバナーをクリックし、コンテンツエディターで開きます。
1. コンテンツエディターを使用して、バナーの内容（原稿、画像、テキストなど）をドラッグします。

### バナー内のメタデータの表示および編集 {#viewing-and-editing-the-metadata-within-a-banner}

バナーには、タイトル、説明、画像など多くのプロパティがあります。このようなプロパティを表示および変更するには、この操作を使用します。オプションで、保存時に Mobile On-Demand に変更内容をアップロードすることもできます。

記事を表示／編集する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. 次からバナーを選択： **バナーを管理** タイル。

1. アクションバーから「**プロパティ**」を選択します。
1. コレクションの使用可能なすべてのメタデータを確認します。
1. 必要に応じてメタデータを編集し、終わったら「**保存**」をクリックします。
1. オプションで、変更内容を直ちに Mobile On-Demand にアップロードします。

## バナーのアップロード {#uploading-a-banner}

アップロード操作では、選択したコンテンツがコピーされ、 Mobile On-Demand プロジェクトに追加されます。既存の Mobile On-Demand コンテンツは新しいバージョンに置き換えられます。

バナーをアップロードする一般的なワークフローは以下のとおりです。

1. 送信者 **モバイル**」で、カタログから Mobile On-Demand アプリを選択します。
1. 内 **バナーを管理** タイルで、Mobile On-Demand にアップロードするバナーを選択します。
1. 必要に応じて、リスト表示からさらにバナーを追加します。
1. アクションバーから「**アップロード**」を選択し、ダイアログで「アップロード」をクリックします。
1. バナーが Mobile On-Demand にアップロードされました。

![chlimage_1-7](assets/chlimage_1-7.gif)

## バナーの削除 {#deleting-a-banner}

この操作を実行すると、選択したバナーが Mobile On-Demand から削除され、必要に応じてローカルのAEMインスタンスからも削除されます。

バナーを削除する一般的なワークフローは以下のとおりです。

1. モバイルで、カタログから Mobile On-Demand アプリを選択します。
1. **バナーを管理**&#x200B;タイルで、削除するバナーを選択します。
1. 削除するバナーがリスト内で選択されていることを確認します（必要に応じて、削除する他のバナーを選択します）。
1. アクションバーから「**削除**」をクリックします。
1.  Mobile On-Demand だけでなく、AEM からも削除するかどうかを確認します。
1. 「**削除**」をクリックします。
1. バナーがリストから削除されます。

### 次の手順 {#the-next-steps}

バナーの管理について学習したら、以下を参照してください。

* [記事の管理](/help/mobile/mobile-on-demand-managing-articles.md)
* [コレクションの管理](/help/mobile/mobile-on-demand-managing-collections.md)
* [共有リソースのアップロード](/help/mobile/mobile-on-demand-shared-resources.md)
* [コンテンツの公開／非公開](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [プリフライトによるプレビュー](/help/mobile/aem-mobile-manage-ondemand-services.md)
