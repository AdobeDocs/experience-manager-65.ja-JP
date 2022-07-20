---
title: 製品フィード
seo-title: Product Feed
description: AEM 製品フィードについて説明します。
seo-description: Learn about the AEM Product Feed.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
exl-id: 11a3d636-040a-40bb-ad35-6b8430a81a49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 100%

---

# 製品フィード {#product-feed}

AEM と [Search&amp;Promote](https://www.adobe.com/jp/solutions/testing-targeting/searchandpromote.html) を統合すると、次のことが可能になります。

* 基になるリポジトリ構造やコマースプラットフォームと関係なく、e コマース API を使用する。
* Search&amp;Promote のインデックスコネクタ機能を利用して、XML 形式で製品フィードを提供する。
* Search&amp;Promote のリモート制御機能を利用して、製品フィードのオンデマンドリクエストまたはスケジュール済みリクエストを実行する。
* クラウドサービス設定として指定された、様々な Search&amp;Promote アカウント用のフィードを生成する。

有効なアカウントと、[Search&amp;Promote への接続の設定](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)が必要です。正しい[データセンター](/help/sites-administering/search-and-promote.md#configuring-the-data-center)を使用していることと、**リモートサーバー URI** が設定されていることも確認する必要があります。

## 製品フィードの設定 {#set-up-the-product-feed}

まず、Web サイトのルートと、識別子属性を入力する必要があります。これを行うには：

1. Search&amp;Promote 設定に移動します。
1. 「**[!UICONTROL 編集]**」をクリックします。
1. 「**[!UICONTROL インデックスコネクターフィード設定]**」タブをクリックします。
1. 「**[!UICONTROL Web サイトのルート]**」と「**[!UICONTROL 識別子の属性]**」を入力します。

   >[!NOTE]
   >
   >**[!UICONTROL Web サイトのルート]**&#x200B;は、e コマース web サイトのルートです（例：`/content/geometrixx-outdoors/en`）。
   >
   >**[!UICONTROL 識別子の属性]**&#x200B;は、製品を一意に識別する JCR プロパティです（例：`identifier`）。

1. 「**[!UICONTROL OK]**」をクリックします。

また、製品フィードを生成するには、Web コンソールで 2 つの設定を編集する必要があります。

### Geometrixx 用 Day CQ Search&amp;Promote 製品クローラ実装の設定 {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) に移動します。
1. 「**[!UICONTROL Day CQ Search&amp;Promote products crawler implementation for Geometrixx]**」をクリックします。
1. このクローラをリンクする Search&amp;Promote アカウント番号を指定します。アカウント番号は、このクローラが使用するクラウドサービス設定の検索に使用されます。
1. 「**[!UICONTROL 保存]**」をクリックします。

### Geometrixx 用 Day CQ Search&amp;Promote 製品フィードジェネレーターの設定 {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) に移動します。
1. 「**[!UICONTROL Day CQ Search&amp;Promote products feed generator for Geometrixx]**」をクリックします。
1. このジェネレーターをリンクする Search&amp;Promote アカウント番号を指定します。アカウント番号は、このジェネレーターが使用するクラウドサービス設定の検索に使用されます。
1. 「**[!UICONTROL 保存]**」をクリックします。

## 製品フィードのスケジュール設定 {#schedule-the-product-feed}

スケジュールされたフィードの生成を有効にするには、そのためのスケジューラーを設定する必要があります。
スケジューラーは、特定の Search&amp;Promote クラウドサービス設定の子設定として設定されます。

1. Search&amp;Promote 設定に移動します。
1. 「**[!UICONTROL スケジューラー設定]**」の横の「**[!UICONTROL +]**」をクリックします。
1. ページ作成者が認識できる&#x200B;**[!UICONTROL タイトル]**&#x200B;と、一意の&#x200B;**[!UICONTROL 名前]**&#x200B;を入力します。
1. 「**[!UICONTROL 作成]**」をクリックします。ダイアログが表示されます。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. 「**[!UICONTROL リモート制御のパスワード]**」を入力します。これは、Search&amp;Promote アカウントで設定したパスワードです。

   >[!NOTE]
   >
   >Search&amp;Promote アカウントのパスワードではありません。このパスワードを探して変更するには、Search&amp;Promote アカウントにログインし、**[!UICONTROL インデックス]**／**[!UICONTROL リモート制御]**&#x200B;に移動します。

1. 「**[!UICONTROL スケジュールを有効にする]**」ボックスをオンにします。
1. **[!UICONTROL スケジュール]**&#x200B;を選択します。これは、実際のフィード生成スケジュールです。
1. 「**[!UICONTROL オンデマンドのインデックス作成]**」を有効にします（または有効にしません）。この機能は、Search&amp;Promote のインデックスを手動で呼び出すために使用されます。「**[!UICONTROL すべての製品フィードをリクエスト]**」がオンの場合、Search&amp;Promote はすべての製品フィードをリクエストします。それ以外の場合は、増分製品フィードがリクエストされます。

   >[!NOTE]
   >
   >オンデマンドのインデックス作成機能は、Search&amp;Promote のリモート制御機能を利用します。リモートインデックス作成が呼び出されると、インデックス作成がただちに開始されるわけではありませんが、リモート制御機能を使用して、インデックス作成リクエストが Search&amp;Promote に送信されます。

1. 「**[!UICONTROL OK]**」をクリックします。

これで設定が完了したので、設定済み web サイトのルートの下に、すべての製品を含む XML ページが表示されます（[http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)）。
