---
title: Adobe Search&Promote との統合
seo-title: Adobe Search&Promote との統合
description: Adobe Search&Promote と統合する方法について説明します。
seo-description: Adobe Search&Promote と統合する方法について説明します。
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 77%

---


# Adobe Search&amp;Promote との統合{#integrating-with-adobe-search-promote}

Web サイトから Adobe Search&amp;Promote サービスを呼び出すには、次のタスクを実行します。

1. クラウドの URL を指定します。
1. Search&amp;Promote サービスへの接続を設定します。
1. Search&amp;Promote コンポーネントをサイドキックに追加します。
1. コンポーネントを使用して、コンテンツを作成します（[Web ページへの Search&amp;Promote 機能の追加](/help/sites-authoring/search-and-promote.md)を参照）。
1. バナーをページに追加します。バナー画像は、Search&amp;Promote データの影響を受けます。
1. Search&amp;Promote サービスが使用するサイトマップを生成します。

>[!NOTE]
>
>カスタムプロキシ設定で Search&amp;Promote を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x is configured with [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x is configured with [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Search&amp;Promote サービス URL の変更 {#changing-the-search-promote-service-url}

The default URL that is configured for the Search&amp;Promote service is `https://searchandpromote.omniture.com/px/`. 別のサービスを使用するには、OSGi コンソールを使用して別の URL を指定します。

1. OSGi コンソールを開いて「Configuration」タブをクリックします([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Day CQ Search&amp;Promote 設定項目をクリックします。
1. 「Remote Server URI」ボックスに URL を入力して、「Save」をクリックします。

## Search&amp;Promote への接続の設定 {#configuring-the-connection-to-search-promote}

Search&amp;Promote への 1 つ以上の接続を設定して、Web ページがサービスとやり取りできるようにします。接続するには、Search&amp;Promote アカウントのメンバー ID とアカウント番号が必要です。

1. **ツール** アイコン **/**&#x200B;導入 **から、** Cloud Servicesを選択します。

   これにより、クラウドサービスダッシュボードが表示されます。ローカルマシンの場合、ダッシュボードの URI は、次のようになります。

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. クラウドサービスページで、Adobe Search&amp;Promote リンクまたは Search&amp;Promote アイコンをクリックします。

1. If this is the first time you are configuring Adobe Search&amp;Promote, click **Configure Now** to open the Create Configuration panel.

   If you would like to learn more about Search&amp;Promote click **Learn More** instead.

   ![](assets/chlimage_1-59.png)

1. ページ作成者が認識可能な&#x200B;**タイトル**&#x200B;を入力し、一意の&#x200B;**名前**&#x200B;を入力したら、「**作成**」をクリックします。

   **コンポーネントを編集**&#x200B;ウィンドウが開きます。

   また、新しく作成した設定が、**クラウドサービスダッシュボード**&#x200B;の Adobe Search&amp;Promote リスト項目の「**利用可能な設定**」の下に表示されます。

   ![](assets/chlimage_1-60.png)

1. **コンポーネントを編集**&#x200B;ダイアログボックスのフィールドに次を追加します。

   * **メンバー ID**
   * **アカウント番号**

   >[!NOTE]
   >
   >In order to get this information **yourself,** first you need to log into
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >有効な Seach&amp;Promote 資格情報（電子メール／パスワード）を使用します。
   >次に、ブラウザーのアドレスバーにある URI を調べる必要があります。次のようになります。
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**この場合：**
   >
   >    * **XXXXXXXXXX** は、お使いの**メンバid**に対応します
   >    * **spYYYYYYYYYY** は、使用する **アカウント番号に対応します**


1. 「**Search&amp;Promote に接続**」をクリックします。

   接続成功メッセージが表示されたら、「**OK**」をクリックします。

   (接続後、ボタンのテキストは「**Search&amp;Promoteに再接続**」に変わります)。

1. 「**OK**」をクリックします。今作成した設定の Search&amp;Promote 設定ページが表示されます。

## データセンターの設定 {#configuring-the-data-center}

Search&amp;Promote アカウントがアジアまたはヨーロッパのものである場合、正しいデータセンターを指せるように、デフォルトデータセンターを変更する必要があります（デフォルトデータセンターは、北米アカウント向けです）。

データセンター：

1. Navigate to the Web console at `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. サーバーの場所に応じて、URI を次のいずれかに変更します。

   * North America: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 「**Save**」をクリックします。

## Search&amp;Promote コンポーネントのサイドキックへの追加 {#adding-search-promote-components-to-sidekick}

デザインモードで、コンポーネント&#x200B;**ごとに**&#x200B;編集して、サイドキックの Search&amp;Promote コンポーネントを許可します（詳しくは、[コンポーネント](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)のドキュメントを参照）。

For information about using the components, see See [Adding Search&amp;Promote Features to a Web Page](/help/sites-authoring/search-and-promote.md).)

## ページで使用する Search&amp;Promote サービスの指定 {#specifying-the-search-promote-service-that-your-pages-use}

特定の Search&amp;Promote サービスを使用できるように、Web ページを設定します。Search&amp;Promote コンポーネントは、自動的にホストページのサービスを使用します。

ページの Search&amp;Promote プロパティを設定すると、すべての子ページが設定を継承します。必要に応じて、継承された設定を上書きするように子ページを設定できます。

>[!NOTE]
>
>サービス接続は、既に設定されている必要があります（[Search&amp;Promote への接続の設定](#connection)を参照）。

1. **ページプロパティ**&#x200B;ダイアログボックスを開きます。For example, on the** Websites** page, right-click the page and click **Properties**.
1. 「**クラウドサービス**」タブをクリックします。
1. 親ページからのクラウドサービス設定の継承を無効にするには、継承パスの横にある南京錠アイコンをクリックします。

   ![](assets/sandpinheritpadlock.png)

1. 「**サービスを追加**」をクリックし、「**Adobe Search&amp;Promote**」を選択して、「**OK**」をクリックします。
1. Search&amp;Promote アカウントの接続設定を選択して、「**OK**」をクリックします。

## 製品フィード {#product-feed}

Search&amp;Promote 統合を使用すると、次のことができます。

* 基になるリポジトリ構造やコマースプラットフォームと関係なく、e コマース API を使用する。
* Search&amp;Promote のインデックスコネクタ機能を利用して、XML 形式で製品フィードを提供する。
* Search&amp;Promote のリモート制御機能を利用して、製品フィードのオンデマンドリクエストまたはスケジュール済みリクエストを実行する。
* クラウドサービス設定として指定された、様々な Search&amp;Promote アカウント用のフィードを生成する。

詳しくは、[製品フィード](/help/sites-administering/product-feed.md)を参照してください。
