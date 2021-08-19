---
title: との統合AdobeSearch&Promote
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
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 33%

---

# との統合AdobeSearch&amp;Promote{#integrating-with-adobe-search-promote}

Web サイトから Adobe Search&amp;Promote サービスを呼び出すには、次のタスクを実行します。

1. クラウドの URL を指定します。
1. Search&amp;Promote サービスへの接続を設定します。
1. Search&amp;Promote コンポーネントをサイドキックに追加します。
1. コンポーネントを使用して、コンテンツを作成します([WebページへのSearch&amp;Promote機能の追加](/help/sites-authoring/search-and-promote.md)を参照)。
1. バナーをページに追加します。バナー画像は、Search&amp;Promote データの影響を受けます。
1. Search&amp;Promote サービスが使用するサイトマップを生成します。

>[!NOTE]
>
>カスタムプロキシ設定でSearch&amp;Promoteを使用する場合、Adobe Experience Managerの一部の機能は3.x APIを使用し、他の機能は4.x APIを使用するので、両方のHTTPクライアントプロキシを設定する必要があります。
>
>* 3.xは[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)で設定します。
>* 4.xは[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)で設定します。

>



## Search&amp;PromoteサービスURLの変更 {#changing-the-search-promote-service-url}

Search&amp;Promoteサービスに設定されるデフォルトのURLは`https://searchandpromote.omniture.com/px/`です。 別のサービスを使用するには、OSGi コンソールを使用して別の URL を指定します。

1. OSGiコンソールを開き、「**[!UICONTROL Configuration]**」タブを選択します。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 「 Day CQSearch&amp;Promote設定」項目を選択します。
1. 「Remote Server URI」ボックスにURLを入力し、「**[!UICONTROL Save]**」を選択します。

## Search&amp;Promoteへの接続の設定 {#configuring-the-connection-to-search-promote}

Search&amp;Promote への 1 つ以上の接続を設定して、Web ページがサービスとやり取りできるようにします。接続するには、Search&amp;Promote アカウントのメンバー ID とアカウント番号が必要です。

1. Experience Managerで、**[!UICONTROL ツール]** / **[!UICONTROL デプロイメント]** / **[!UICONTROL Cloud Services]**&#x200B;を選択します。

   ローカルマシンを使用している場合、ダッシュボードのURLは次のようになります。

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. Cloud Servicesページで、「AdobeSearch&amp;Promote」リンクまたはSearch&amp;Promoteアイコンを選択します。

1. 初めてAdobeSearch&amp;Promoteを設定する場合は、「**[!UICONTROL 今すぐ設定]**」を選択して、「設定を作成」パネルを開きます。

   Search&amp;Promoteの詳細を確認するには、「**[!UICONTROL 詳細]**」を選択します。

   ![](assets/chlimage_1-59.png)

1. ページ作成者が認識できる&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力し、一意の&#x200B;**[!UICONTROL 名前]**&#x200B;を入力します。
1. 「**[!UICONTROL 作成]**」を選択します。

   また、新しく作成した設定が、**クラウドサービスダッシュボード**&#x200B;の Adobe Search&amp;Promote リスト項目の「**利用可能な設定**」の下に表示されます。

   ![](assets/chlimage_1-60.png)

1. **[!UICONTROL コンポーネントを編集]**&#x200B;ダイアログボックスで、以下の内容をフィールドに追加します。

   * **メンバー ID**
   * **アカウント番号**

   >[!NOTE]
   >
   >**自分でこの情報を取得するには、まず**&#x200B;にログインする必要があります。
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >有効な Seach&amp;Promote 資格情報（電子メール／パスワード）を使用します。
   >次に、ブラウザーのアドレスバーにあるURLを確認する必要があります。このURLは次のようになります。
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**ここで、**
   >
   >    * **** XXXXXXXは、使用するメンバーID**に対応します**
   >    * **** spYYYYYYYYYはアカウント番 **号に対応します**


1. 「**[!UICONTROL Search&amp;Promoteに接続]**」を選択します。

   接続成功メッセージが表示されたら、「**[!UICONTROL OK]**」を選択します。

   (接続後、ボタンのテキストが「**Search&amp;Promoteに再接続**」に変わります)。

1. 「**[!UICONTROL OK]**」を選択します。作成した設定のSearch&amp;Promote設定ページが表示されます。

## データセンターの設定 {#configuring-the-data-center}

Search&amp;Promote・アカウントがアジアまたはヨーロッパにある場合、デフォルトのデータ・センターを変更して、適切なデータ・センターを指すようにする必要があります（デフォルトのデータ・センターは北米のアカウント用です）。

**データセンター：**

1. Webコンソール(`https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`)に移動します。

   ![](assets/chlimage_1-61.png)

1. サーバーの場所に応じて、URI を次のいずれかに変更します。

   * 北米：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA:[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC:[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 「**[!UICONTROL 保存]**」を選択します。

## サイドキックへのSearch&amp;Promoteコンポーネントの追加 {#adding-search-promote-components-to-sidekick}

デザインモードで、コンポーネント&#x200B;**ごとに**&#x200B;編集して、サイドキックの Search&amp;Promote コンポーネントを許可します（詳しくは、[コンポーネント](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode)のドキュメントを参照）。

コンポーネントの使用について詳しくは、「[WebページへのSearch&amp;Promote機能の追加](/help/sites-authoring/search-and-promote.md)」を参照してください。)

## ページで使用するSearch&amp;Promoteサービスの指定 {#specifying-the-search-promote-service-that-your-pages-use}

特定の Search&amp;Promote サービスを使用できるように、Web ページを設定します。Search&amp;Promote コンポーネントは、自動的にホストページのサービスを使用します。

ページの Search&amp;Promote プロパティを設定すると、すべての子ページが設定を継承します。必要に応じて、継承された設定を上書きするように子ページを設定できます。

>[!NOTE]
>
>事前にサービス接続を設定しておく必要があります。 （[Search&amp;Promote への接続の設定](#connection)を参照）。

1. **[!UICONTROL ページプロパティ]**&#x200B;ダイアログボックスを開きます。例えば、** Webサイト**ページで、ページを右クリックし、「**[!UICONTROL プロパティ]**」を選択します。
1. 「**[!UICONTROL クラウドサービス]**」タブを選択します。
1. 親ページからのクラウドサービス設定の継承を無効にするには、継承パスの横にある南京錠アイコンを選択します。

   ![](assets/sandpinheritpadlock.png)

1. 「**[!UICONTROL サービスを追加]**」を選択します。
1. 「**[!UICONTROL AdobeSearch&amp;Promote]**」を選択し、「**[!UICONTROL OK]**」を選択します。
1. Search&amp;Promoteアカウントの接続設定を選択し、「**OK**」を選択します。

## 製品フィード {#product-feed}

Search&amp;Promote統合により、次の操作を実行できます。

* 基になるリポジトリ構造やコマースプラットフォームとは独立して、eコマースAPIを使用します。
* XML形式の製品フィードを使用できるように、Search&amp;Promoteのインデックスコネクタ機能を使用します。
* 製品フィードに対してオンデマンドまたはスケジュール済みのリクエストを実行する場合は、Search&amp;Promoteのリモート制御機能を使用します。
* 様々なSearch&amp;Promoteアカウント用のフィードの生成（クラウドサービス設定として設定）。

詳しくは、[製品フィード](/help/sites-administering/product-feed.md)を参照してください。
