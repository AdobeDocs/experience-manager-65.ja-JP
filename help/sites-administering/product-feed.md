---
title: 製品フィード
seo-title: 製品フィード
description: AEM 製品フィードについて説明します。
seo-description: AEM 製品フィードについて説明します。
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 71%

---


# 製品フィード {#product-feed}

AEMは[Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html)と統合され、次のことが可能です。

* 基になるリポジトリ構造やコマースプラットフォームと関係なく、e コマース API を使用する。
* Search&amp;Promote のインデックスコネクタ機能を利用して、XML 形式で製品フィードを提供する。
* Search&amp;Promote のリモート制御機能を利用して、製品フィードのオンデマンドリクエストまたはスケジュール済みリクエストを実行する。
* クラウドサービス設定として指定された、様々な Search&amp;Promote アカウント用のフィードを生成する。

有効なアカウントを持っていて、[Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)への接続を設定する必要があります。 また、正しい[データセンター](/help/sites-administering/search-and-promote.md#configuring-the-data-center)を使用していることを確認し、**リモートサーバーのURI **が設定されていることを確認する必要があります。

## 製品フィードの設定 {#set-up-the-product-feed}

まず、Web サイトのルートと、識別子属性を入力する必要があります。次の手順を実行します。

1. Search&amp;Promote 設定に移動します。
1. 「**[!UICONTROL 編集]**」をクリックします。
1. 「**[!UICONTROL インデックスコネクターフィード設定]**」タブをクリックします。
1. **[!UICONTROL Webサイトのルート]**&#x200B;と&#x200B;**[!UICONTROL 識別子属性]**&#x200B;を入力します。

   >[!NOTE]
   >
   >**[!UICONTROL Webサイトのルート]**&#x200B;は、eコマースWebサイトのルートです（例：`/content/geometrixx-outdoors/en`）。
   >
   >**[!UICONTROL Identifier属性]**&#x200B;は、製品を一意に識別するJCRプロパティです。`identifier`。

1. 「**[!UICONTROL OK]**」をクリックします。

また、製品フィードを生成するには、Web コンソールで 2 つの設定を編集する必要があります。

### Geometrixx 用 Day CQ Search&amp;Promote 製品クローラ実装の設定  {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) に移動します。
1. 「**[!UICONTROL Day CQ Search&amp;Promote products crawler implementation for Geometrixx]**」をクリックします。
1. このクローラをリンクする Search&amp;Promote アカウント番号を指定します。アカウント番号は、このクローラが使用するクラウドサービス設定の検索に使用されます。
1. 「**[!UICONTROL Save]**」をクリックします。

### Geometrixx 用 Day CQ Search&amp;Promote 製品フィードジェネレーターの設定  {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) に移動します。
1. 「**[!UICONTROL Day CQ Search&amp;Promote products feed generator for Geometrixx]**」をクリックします。
1. このジェネレーターをリンクする Search&amp;Promote アカウント番号を指定します。アカウント番号は、このジェネレーターが使用するクラウドサービス設定の検索に使用されます。
1. 「**[!UICONTROL Save]**」をクリックします。

## 製品フィードのスケジュール設定  {#schedule-the-product-feed}

スケジュール済みフィード生成を有効にするには、そのためのスケジューラーを設定する必要があります。スケジューラーは、特定の Search&amp;Promote クラウドサービス設定の子設定として設定されます。

1. Search&amp;Promote 設定に移動します。
1. 「**[!UICONTROL スケジューラー設定]**」の横の「**[!UICONTROL +]**」をクリックします。
1. ページ作成者が認識できる&#x200B;**[!UICONTROL タイトル]**&#x200B;と、一意の&#x200B;**[!UICONTROL 名前]**&#x200B;を入力します。
1. 「**[!UICONTROL 作成]**」をクリックします。ダイアログが表示されます。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. **[!UICONTROL リモートコントロールパスワード]**&#x200B;を入力します。 これは、Search&amp;Promote アカウントで設定したパスワードです。

   >[!NOTE]
   >
   >Search&amp;Promote アカウントのパスワードではありません。このパスワードは、Search&amp;Promoteアカウントにログインし、**[!UICONTROL Index]**&#x200B;に移動してから&#x200B;**[!UICONTROL Remote control]**&#x200B;に移動すると、見つけて変更できます。

1. 「**[!UICONTROL スケジュールを有効にする]**」ボックスをオンにします。
1. **[!UICONTROL スケジュール]**&#x200B;を選択します。これは、実際のフィード生成スケジュールです。
1. 「**[!UICONTROL オンデマンドのインデックス作成]**」を有効にします（または有効にしません）。この機能は、Search&amp;Promote のインデックスを手動で呼び出すために使用されます。**[!UICONTROL 製品フィード]**&#x200B;をすべてリクエストがオンになっている場合、Search&amp;Promoteは製品フィード全体をリクエストします。 それ以外の場合は、増分製品フィードがリクエストされます。

   >[!NOTE]
   >
   >オンデマンドのインデックス作成機能は、Search&amp;Promote のリモート制御機能を利用します。リモートインデックス作成が呼び出されると、インデックス作成がただちに開始されるわけではありませんが、リモート制御機能を使用して、インデックス作成リクエストが Search&amp;Promote に送信されます。

1. 「**[!UICONTROL OK]**」をクリックします。

すべての設定が完了したら、設定済みのWebサイトのルート下にあるすべての製品を含むXMLページが表示されます。[http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
