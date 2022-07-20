---
title: Adobe Search&Promote との統合
description: Adobe Search&Promote と統合する方法について説明します。
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: ht
source-wordcount: '875'
ht-degree: 100%

---

# Adobe Search&amp;Promote との統合{#integrating-with-adobe-search-promote}

Web サイトから Adobe Search&amp;Promote サービスを呼び出すには、次のタスクを実行します。

1. クラウドの URL を指定します。
1. Search&amp;Promote サービスへの接続を設定します。
1. Search&amp;Promote コンポーネントをサイドキックに追加します.
1. コンポーネントを使用して、コンテンツを作成します。（[Web ページへの Search&amp;Promote 機能の追加](/help/sites-authoring/search-and-promote.md)を参照。）
1. バナーをページに追加します。バナー画像は、Search&amp;Promote データの影響を受けます。
1. Search&amp;Promote サービスが使用するサイトマップを生成します。

>[!NOTE]
>
>カスタムプロキシ構成で Search&amp;Promote を使用している場合、Adobe Experience Manager の一部の機能で 3.x API と 4.x API が使用されているので、両方の HTTP クライアントプロキシ構成を構成する必要があります。
>
>* 3.x は [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>


## Search&amp;Promote サービス URL の変更 {#changing-the-search-promote-service-url}

Search&amp;Promote サービス用に設定されるデフォルト URL は、`https://searchandpromote.omniture.com/px/` です。別のサービスを使用するには、OSGi コンソールを使用して別の URL を指定します。

1. OSGi コンソールを開いて「**[!UICONTROL 設定]**」タブをクリックします。（[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)）
1. 「Day CQ Search&amp;Promote 設定」項目をクリックします。
1. 「リモートサーバー URI」ボックスに URL を入力して、「**[!UICONTROL 保存]**」をクリックします。

## Search&amp;Promote との接続設定 {#configuring-the-connection-to-search-promote}

Search&amp;Promote への 1 つ以上の接続を設定して、Web ページがサービスとやり取りできるようにします。接続するには、Search&amp;Promote アカウントのメンバー ID とアカウント番号が必要です。

1. Experience Manager で、**[!UICONTROL ツール]**>**[!UICONTROL デプロイメント]**> **[!UICONTROL Cloud Services]** を選択します。

   ローカルマシンを使用している場合、ダッシュボードの URL は次のようになります。

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Cloud Services ページで、Adobe Search&amp;Promote リンクまたは Search&amp;Promote アイコンを選択します。

1. 初めて Adobe Search&amp;Promote を設定する場合は、「**[!UICONTROL 今すぐ設定]**」をクリックして、「設定を作成」パネルを開きます。

   Search&amp;Promote の詳細については、「**[!UICONTROL 詳細情報]**」を選択してください。

   ![](assets/chlimage_1-59.png)

1. ページ作成者が認識できる「**[!UICONTROL タイトル]**」を入力し、固有の「**[!UICONTROL 名前]**」を入力してください。
1. 「**[!UICONTROL 作成]**」を選択します。

   また、新しく作成した設定が、**Cloud Services ダッシュボード**&#x200B;の Adobe Search&amp;Promote リスト項目の「**利用可能な設定**」の下に表示されます。

   ![](assets/chlimage_1-60.png)

1. **[!UICONTROL コンポーネントを編集]**&#x200B;ダイアログボックスで、フィールドに次の項目を追加します。

   * **メンバー ID**
   * **アカウント番号**

   >[!NOTE]
   >
   >この情報を&#x200B;**自身で**&#x200B;取得するには、以下にログインする必要があります。
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >有効な Seach&amp;Promote 認証情報（メール／パスワード）を使用します。
   >次に、ブラウザーのアドレスバーで URL を確認する必要があります。このように表示されるはずです。
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**ここで**
   >
   >    * **XXXXXXXX** は**メンバー ID **を示します。
   >    * **spYYYYYYYY** は&#x200B;**アカウント番号**&#x200B;を示します。


1. 「**[!UICONTROL Search&amp;Promote に接続]**」を選択します。

   接続成功メッセージが表示されたら、「**[!UICONTROL OK]**」を選択します。

   （接続後、ボタンのテキストが「**Search&amp;Promote に再接続**」に変更されます。）

1. 「**[!UICONTROL OK]**」を選択します。作成した設定の Search&amp;Promote 設定ページが表示されます。

## データセンターの設定 {#configuring-the-data-center}

Search&amp;Promote アカウントがアジアまたはヨーロッパのものである場合、デフォルトのデータセンターを変更して、正しいデータセンターを指すようにする必要があります（デフォルトデータセンターは、北米アカウント向けです）。

**データセンターの設定**

1. Web コンソール（`https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`）にアクセスします。

   ![](assets/chlimage_1-61.png)

1. サーバーの場所に応じて、URI を次のいずれかに変更します。

   * 北米：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA：[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC：[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 「**[!UICONTROL 保存]**」を選択します。

## Search&amp;Promote コンポーネントをサイドキックに追加します {#adding-search-promote-components-to-sidekick}

デザインモードで、コンポーネント&#x200B;**ごとに**&#x200B;編集して、サイドキックの Search&amp;Promote コンポーネントを許可します（詳しくは、[コンポーネント](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)のドキュメントを参照）。

コンポーネントの使い方については、[Web ページへの Search&amp;Promote 機能の追加](/help/sites-authoring/search-and-promote.md)を参照してください。

## ページで使用する Search&amp;Promote サービスの指定 {#specifying-the-search-promote-service-that-your-pages-use}

特定の Search&amp;Promote サービスを使用できるように、web ページを設定します。Search&amp;Promote コンポーネントは、自動的にホストページのサービスを使用します。

ページの Search&amp;Promote プロパティを設定すると、すべての子ページが設定を継承します。必要に応じて、継承された設定を上書きするように子ページを設定できます。

>[!NOTE]
>
>事前にサービス接続を設定しておく必要があります。（[Search&amp;Promote への接続の設定](#connection)を参照）。

1. **[!UICONTROL ページプロパティ]**&#x200B;ダイアログボックスを開きます。例えば、** web サイト**ページで、ページを右クリックし、「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL Cloud Services]**」タブを選択します。
1. 親ページからのクラウドサービス設定の継承を無効にするには、継承パスの横にある南京錠アイコンを選択します。

   ![](assets/sandpinheritpadlock.png)

1. 「**[!UICONTROL サービスを追加]**」を選択します。
1. **[!UICONTROL Adobe Search&amp;Promote]** を選択し、「 **[!UICONTROL OK]**」を選択します。
1. Search&amp;Promote アカウントの接続設定を選択して、「**OK**」を選択します。

## 製品フィード {#product-feed}

Search&amp;Promote の統合により、次の操作を実行できます。

* もとになるリポジトリ構造やコマースプラットフォームと関係なく、eCommerce API を使用する。
* Search&amp;Promote のインデックスコネクタ機能を使用して、XML 形式の製品フィードを作成できます。
* Search&amp;Promote のリモート制御機能を利用して、製品フィードのオンデマンドリクエストまたはスケジュール済みリクエストを実行する。
* クラウドサービス設定として指定された、様々な Search&amp;Promote アカウント用のフィードを生成する。

詳しくは、[製品フィード](/help/sites-administering/product-feed.md)を参照してください。
