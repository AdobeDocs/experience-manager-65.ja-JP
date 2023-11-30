---
title: Adobe Analytics への接続とフレームワークの作成
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: AEM と SiteCatalyst の接続およびフレームワークの作成について説明します。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: bbd18486a77d7b46454aacff23147b38860bd895
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 93%

---

# Adobe Analytics への接続とフレームワークの作成 {#connecting-to-adobe-analytics-and-creating-frameworks}

Adobe Analytics で AEM ページからの web データを追跡するには、Adobe Analytics Cloud サービス設定と Adobe Analytics フレームワークを作成します。

* **Adobe Analytics 設定：** Adobe Analytics アカウントに関する情報。Adobe Analytics 設定を使用して、AEM を Adobe Analytics に接続できます。使用するアカウントごとに Adobe Analytics 設定を作成します。
* **Adobe Analytics フレームワーク：** Adobe Analytics レポートスイートプロパティと CQ 変数の間にある一連のマッピングです。フレームワークを使用して、web サイトデータを Adobe Analytics レポートにどのように入力するかを設定します。フレームワークは Adobe Analytics 設定と関連付けられています。設定ごとに複数のフレームワークを作成できます。

web ページをフレームワークに関連付けると、フレームワークがそのページおよび子ページの追跡を実行します。ページビューは、Adobe Analytics から取得され、Sites コンソールに表示されます。

## 前提条件 {#prerequisites}

### Adobe Analytics アカウント {#adobe-analytics-account}

Adobe Analytics で AEM データを追跡するには、有効な Adobe Experience Cloud Adobe Analytics アカウントが必要です。

Adobe Analytics アカウントには次の要件があります。

* **管理者**&#x200B;権限がある
* **Web サービスアクセス**&#x200B;ユーザーグループに割り当てられている

>[!CAUTION]
>
>（Adobe Analytics 内の）**管理者**&#x200B;権限を提供するだけでは、ユーザーが AEM から Adobe Analytics に接続するのに十分ではありません。また、アカウントには **web サービスへのアクセス**&#x200B;権限も必要です。

![chlimage_1-67](assets/chlimage_1-67.png)

先に進む前に、お使いの資格情報で Adobe Analytics にログインできることを確認してください。次のいずれかの方法を使用します。

* [Adobe Experience Cloud へのログイン](https://experience.adobe.com/#/@login/home)

* [Adobe Analytics へのログイン](https://sc.omniture.com/login/)

### Adobe Analytics データセンターを使用するように AEM を設定 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [データセンター](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=ja)では、Adobe Analytics レポートスイートに関連付けられたデータを収集、処理および格納します。Adobe Analytics レポートスイートをホストしているデータセンターを使用するように、AEM を設定します。データセンターに関しては、契約に記載されています。この情報については、組織の管理者にお問い合わせください。

必要に応じて、`https://api.omniture.com/` を使用して正しいデータセンターにルーティングします。

組織で特定のデータセンターからのデータ収集または取得が必要な場合は、以下を使用します。

| データセンター | URL |
|---|---|
| ロンドン | `https://api3.omniture.com/` |
| シンガポール | `https://api4.omniture.com/` |
| オレゴン | `https://api5.omniture.com/` |

[Web コンソールを使用して OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)します（**Adobe AEM Analytics HTTP Client**）。**データセンター URL** を追加してください。このデータセンターでは、AEM ページがデータを収集するレポートスイートをホスティングします。

![aa-07](assets/aa-07.png)

1. Web コンソールを Web ブラウザーで開きます。([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. コンソールにアクセスするには、資格情報を入力します。

   >[!NOTE]
   >
   >このコンソールにアクセスできるかどうかを確認するには、サイト管理者に問い合わせてください。

1. **Adobe AEM Analytics HTTP Client** という名前の設定項目を選択します。
1. データセンターの URL を追加するには、「**データセンター URL**」リストの横にある + ボタンを押して、ボックスに URL を入力します。

1. リストから URL を削除するには、URL の横の「-」ボタンをクリックします。
1. 「保存」をクリックします。

## Adobe Analytics への接続の設定 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Adobe Analytics API のセキュリティが変更され、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>[Adobe Analytics が提供する ActivityMap プラグイン](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ja)を使用する必要があります。

## Activity Map の設定 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Adobe Analytics API のセキュリティが変更され、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>[Adobe Analytics が提供する ActivityMap プラグイン](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ja)を使用する必要があります。

## Adobe Analytics フレームワークの作成 {#creating-a-adobe-analytics-framework}

使用するレポートスイート ID（RSID）について、レポートスイートにデータを入力するサーバーインスタンス（作成、公開、または両方）を制御できます。

* **すべて**：オーサーインスタンスとパブリッシュインスタンスの両方からの情報がレポートスイートに入力されます。
* **オーサー**：オーサーインスタンスからの情報のみがレポートスイートに入力されます。
* **パブリッシュ**：パブリッシュインスタンスからの情報のみがレポートスイートに入力されます。

>[!NOTE]
>
>サーバーインスタンスのタイプを選択しても、Adobe Analytics への呼び出しは制限されません。どの呼び出しが RSID を含むかを制御するだけです。
>
>例えば、*diiweretail* レポートスイートを使用するようにフレームワークが設定されていて、選択したサーバーインスタンスがオーサーである場合を考えます。このフレームワークでページを公開すると、引き続き Adobe Analytics に対して呼び出しが行われますが、その呼び出しに RSID は含まれません。オーサーインスタンスからの呼び出しにのみ RSID が含まれます。

1. **ナビゲーション**&#x200B;を使用して、「**ツール**」／「**クラウドサービス**」から「**従来のクラウドサービス**」を選択します。
1. スクロールして「**Adobe Analytics**」を選択し、「**設定を表示**」を選択します。
1. Adobe Analytics の設定の横にある **+** リンクをクリックします。

1. **フレームワークを作成**&#x200B;ダイアログで、以下を行います。

   * 「**タイトル**」を指定します。
   * オプションで、リポジトリにフレームワークの詳細を保存するノードの&#x200B;**名前**&#x200B;を指定できます。
   * 「**Adobe Analytics フレームワーク**」を選択します。

   「**作成**」をクリックします。

   フレームワークが編集用に開きます。

1. サイドポッド（メインパネルの右側）の「**レポートスイート**」セクションで、「**項目を追加**」をクリックします。次に、ドロップダウンを使用して、フレームワークでやり取りするレポートスイート ID（例えば、`geometrixxauth`）を選択します。

   >[!NOTE]
   >
   >レポートスイート ID を選択すると、左側のコンテンツファインダーに Adobe Analytics 変数（SiteCatalyst 変数）が設定されます。

1. レポートスイートに情報を送信するサーバーインスタンスを選択するには、 **実行モード** （レポートスイート ID の横にある）」ドロップダウンリストを使用して、製品内で利用できます。

   ![aa-framework-01](assets/aa-framework-01.png)

1. サイトのパブリッシュインスタンスでフレームワークを使用できるようにするには、サイドキックの「**ページ**」タブで「**フレームワークをアクティベート**」をクリックします。

### Adobe Analytics のサーバー設定 {#configuring-server-settings-for-adobe-analytics}

フレームワークの仕組みを利用すると、各 Adobe Analytics フレームワーク内でサーバーの設定を変更できます。

>[!CAUTION]
>
>データの送信先と送信方法を判断するための設定なので、*これらの設定には手を加えない*&#x200B;でください。代わりに Adobe Analytics 担当者に設定してもらってください。

まず、パネルを開きます。**サーバー**&#x200B;の横の下向き矢印を押します。

![server_001](assets/server_001.png)

* **トラッキングサーバー**

   * Adobe Analytics の呼び出しを送信するための URL が格納されています。

      * `cname` - デフォルト値は Adobe Analytics アカウントの「*会社名*」です。
      * `d1` - 情報の送信先のデータセンター（`d1`、`d2`、`d3` のいずれか）に対応しています
      * `sc.omtrdc.net` - ドメイン名

* **トラッキングサーバーを保護**

   * トラッキングサーバーと同じセグメントが指定されています。
   * セキュリティで保護されているページ（`https://`）からのデータ送信に使用されます。

* **訪問者の名前空間**

   * 名前空間は、トラッキング URL の最初の部分を決定します。
   * 例えば、名前空間を **CNAME** に変更すると、Adobe Analytics に対して行われる呼び出しは、デフォルトではなく **CNAME.d1.omtrdc.net** のようになります。

## Adobe Analytics フレームワークへのページの関連付け {#associating-a-page-with-a-adobe-analytics-framework}

ページを Adobe Analytics フレームワークに関連付けると、ページの読み込み時にページが Adobe Analytics にデータを送信します。ページに設定される変数は、フレームワークの Adobe Analytics 変数からマッピングされ取得されます。例えば、ページビュー数は Adobe Analytics から取得されます。

ページの子は、フレームワークとの関連付けを継承します。例えば、サイトのルートページをフレームワークに関連付けると、サイトのすべてのページがそのフレームワークに関連付けられます。

1. **Sites** コンソールから、トラッキングを設定したいページを選択します。
1. コンソールから直接、またはページエディターから&#x200B;**[ページのプロパティ](/help/sites-authoring/editing-page-properties.md)**&#x200B;を開きます。
1. 「クラウドサービス」タブを開きます。

1. 以下を使用します。 **設定を追加** ドロップダウンで選択 **Adobe Analytics** を選択します。 継承が設定されている場合、セレクターが使用可能になる前に無効にします。

1. **Adobe Analytics** のドロップダウンセレクターが、使用可能なオプションに追加されます。必要なフレームワーク設定を選択します。

1. 「**保存して閉じる**」を選択します。
1. ページおよび接続されている設定やファイルをアクティベートするには、ページを&#x200B;**[公開](/help/sites-authoring/publishing-pages.md)**&#x200B;します。
1. 最後に、パブリッシュインスタンス上のページにアクセスし、**検索**&#x200B;コンポーネントを使用してキーワード（例：aubergine）を検索します。
1. [Adobe Experience Cloud デバッガー](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=ja)などの適切なツールを使用して、Adobe Analytics への呼び出しを確認できます。
1. 提供されている呼び出しの例では、入力された値（aubergine）が eVar7 に格納され、イベントリストに event3 が含まれています。

### ページ表示 {#page-views}

ページを Adobe Analytics フレームワークに関連付けると、ページビュー数を Sites コンソールのリストビューに表示できます。

詳しくは、[ページ分析データの表示](/help/sites-authoring/page-analytics-using.md)を参照してください。

### 読み込み間隔の設定 {#configuring-the-import-interval}

適切な **AdobeAEM Analytics Report Sling Importer** サービス：

* **取得の試行**：キューに格納されたレポートを取得しようとした回数。
デフォルトは、`6` です。

* **取得遅延**：キューに格納されたレポートを取得しようとするまでのミリ秒数。
デフォルトは`10000` です。ミリ秒単位なので、10 秒に相当します。

* **取得頻度**: A `cron` 式を使用して、Analytics レポートを取得する頻度を指定します。
デフォルトはです。 `0 0 0/12 * * ?`これは、1 時間ごとの 12 個の取得に相当します。

この OSGi サービスは、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または[リポジトリ内の osgiConfig ノード](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)（サービス PID は `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`）を使用して設定できます。

## Adobe Analytics 設定やフレームワークの編集 {#editing-adobe-analytics-configurations-and-or-frameworks}

Adobe Analytics 設定またはフレームワークを作成する場合と同様に、（従来の）**クラウドサービス**&#x200B;画面に移動します。「**設定を表示**」を選択して、更新する特定の設定へのリンクをクリックします。

Adobe Analytics 設定を編集する場合は、設定ページ自体で「**編集**」を押して、**コンポーネントを編集**&#x200B;ダイアログを開きます。

## Adobe Analytics フレームワークの削除 {#deleting-adobe-analytics-frameworks}

Adobe Analytics フレームワークを削除するには、まず、[編集用に開きます](#editing-adobe-analytics-configurations-and-or-frameworks)。

次に、サイドキックの「**ページ**」タブから、「**フレームワークを削除**」を選択します。
