---
title: Adobe Analytics への接続とフレームワークの作成
seo-title: Adobe Analytics への接続とフレームワークの作成
description: SiteCatalyst への AEM の接続とフレームワークの作成について説明します。
seo-description: SiteCatalyst への AEM の接続とフレームワークの作成について説明します。
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 63%

---

# Adobe Analytics への接続とフレームワークの作成  {#connecting-to-adobe-analytics-and-creating-frameworks}

Adobe AnalyticsでAEMページのWebデータを追跡するには、Adobe Analytics Cloudサービス設定とAdobe Analyticsフレームワークを作成します。

* **Adobe Analyticsの設定：** Adobe Analyticsアカウントに関する情報。Adobe Analytics設定を使用すると、AEMはAdobe Analyticsに接続できます。 使用するアカウントごとに Adobe Analytics 設定を作成します。
* **Adobe Analytics Framework:** Adobe AnalyticsレポートスイートプロパティとCQ変数の間の一連のマッピング。フレームワークを使用して、Web サイトデータを Adobe Analytics レポートにどのように入力するかを設定します。フレームワークは、Adobe Analytics設定に関連付けられます。 設定ごとに複数のフレームワークを作成できます。

Webページをフレームワークに関連付けると、フレームワークはそのページとそのページの子孫の追跡を実行します。 ページビューは、Adobe Analytics から取得され、Sites コンソールに表示されます。

## 前提条件 {#prerequisites}

### Adobe Analytics アカウント  {#adobe-analytics-account}

Adobe AnalyticsでAEMデータを追跡するには、有効なAdobe Marketing Cloud Adobe Analyticsアカウントが必要です。

Adobe Analyticsアカウントでは、次の操作が必要です。

* **管理者** 権限がある
* **Web サービスアクセス**&#x200B;ユーザーグループに割り当てられている

>[!CAUTION]
>
>（Adobe Analytics 内の）**管理者**&#x200B;権限を持っているだけでは、AEM から Adobe Analytics に接続するのに十分ではありません。アカウントは、**Web サービスアクセス**&#x200B;権限も持っている必要があります。

![chlimage_1-67](assets/chlimage_1-67.png)

先に進む前に、お使いの資格情報で Adobe Analytics にログインできることを確認してください（次のどちらかから）。

* [Adobe Experience Cloud Sign In](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe Analytics Sign In](https://sc.omniture.com/login/)

### Adobe Analytics データセンターを使用するように AEM を設定 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [データセンター](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored)は、Adobe Analyticsレポートスイートに関連付けられたデータを収集、処理、保存します。 Adobe Analyticsレポートスイートをホストするデータセンターを使用するようにAEMを設定する必要があります。 次の表に、使用可能なデータセンターとその URL を示します。

| データセンター | URL |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| ダラス | https://api2.omniture.com/admin/1.4/rest/ |
| ロンドン | https://api3.omniture.com/admin/1.4/rest/ |
| シンガポール | https://api4.omniture.com/admin/1.4/rest/ |
| オレゴン | https://api5.omniture.com/admin/1.4/rest/ |

AEM は、デフォルトではサンノゼのデータセンター（https://api.omniture.com/admin/1.4/rest/）を使用します。

[Web コンソールを使用して OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)してください（**Adobe AEM Analytics HTTP Client**）。AEMページでデータを収集するレポートスイートをホストするデータセンターの&#x200B;**データセンターURL**&#x200B;を追加します。

![aa-07](assets/aa-07.png)

1. Web コンソールを Web ブラウザーで開きます([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. コンソールにアクセスするための資格情報を入力します。

   >[!NOTE]
   >
   >このコンソールへのアクセス権があるかどうかを確認するには、サイト管理者にお問い合わせください。

1. **Adobe AEM Analytics HTTP Client** という設定項目を選択します。
1. データセンターのURLを追加するには、**データセンターのURL**&#x200B;リストの横にある+ボタンを押し、ボックスにURLを入力します。

1. リストから URL を削除するには、URL の横の「-」ボタンをクリックします。
1. 「Save」をクリックします。

## Adobe Analytics への接続の設定  {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>Adobe Analytics](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html)が提供する[ActivityMapプラグインを使用する必要があります。

## Activity Map の設定 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)が提供する[ActivityMapプラグインを使用する必要があります。

## Adobe Analytics フレームワークの作成 {#creating-a-adobe-analytics-framework}

使用するレポートスイート ID（RSID）に関して、レポートスイートにデータを入力するサーバーインスタンス（作成者、発行または両方）を制御できます。

* **すべて**：オーサーインスタンスとパブリッシュインスタンスの両方からの情報がレポートスイートに入力されます。
* **オーサー**：オーサーインスタンスからの情報のみがレポートスイートに入力されます。
* **パブリッシュ**：パブリッシュインスタンスからの情報のみがレポートスイートに入力されます。

>[!NOTE]
>
>サーバーインスタンスのタイプを選択することによって、Adobe Analytics への呼び出しは制限されません。RSID を含める呼び出しを制御するだけです。
>
>例えば、*diiweretail* レポートスイートを使用するようにフレームワークを設定し、サーバーインスタンスとして作成者を選択します。ページをフレームワークと共に公開すると、引き続き Adobe Analytics に対して呼び出しがおこなわれますが、その呼び出しに RSID は含まれません。作成者インスタンスからの呼び出しにのみ RSID が含まれます。

1. **ナビゲーション**&#x200B;を使用して、**ツール**、**クラウドサービス**&#x200B;を選択し、**従来のクラウドサービス**&#x200B;を選択します。
1. **Adobe Analytics**&#x200B;までスクロールし、「**設定を表示**」を選択します。
1. Adobe Analytics設定の横にある&#x200B;**[+]**&#x200B;リンクをクリックします。

1. **フレームワークを作成**&#x200B;ダイアログで、次の操作を実行します。

   * 「**タイトル**」を指定します。
   * オプションで、リポジトリにフレームワークの詳細を保存するノードの&#x200B;**名前**&#x200B;を指定できます。
   * **Adobe Analytics Framework**&#x200B;を選択します。

   「**作成**」をクリックします。

   フレームワークが編集用に開きます。

1. サイドポッド（メインパネルの右側）の「**レポートスイート**」セクションで、「**項目を追加**」をクリックします。次に、ドロップダウンを使用して、フレームワークがやり取りするレポートスイートID（`geometrixxauth`など）を選択します。

   >[!NOTE]
   >
   >左側のコンテンツファインダーでは、レポートスイートIDを選択すると、Adobe Analytics変数(SiteCatalyst変数)が設定されます。

1. 次に、**実行モード**&#x200B;ドロップダウン（レポートスイート ID の横）を使用して、レポートスイートに情報を送信するサーバーインスタンスを選択します。

   ![aa-framework-01](assets/aa-framework-01.png)

1. サイトのパブリッシュインスタンスでフレームワークを使用できるようにするには、サイドキックの「**ページ**」タブで「**フレームワークをアクティベート**」をクリックします。

### Adobe Analytics のサーバー設定の設定 {#configuring-server-settings-for-adobe-analytics}

フレームワークシステムを使用すると、各Adobe Analyticsフレームワーク内のサーバー設定を変更できます。

>[!CAUTION]
>
>これらの設定は、データの送信先と送信方法を決定するので、*これらの設定*&#x200B;を変更せず、代わりにAdobe Analyticsの担当者に設定してもらう必要があります。

まず、パネルを開きます。「**サーバー**」の横の下向き矢印を押します。

![server_001](assets/server_001.png)

* **トラッキングサーバー**

   * Adobe Analytics呼び出しの送信に使用するURLが含まれます。

      * cname — デフォルトはAdobe Analyticsアカウントの&#x200B;*会社名*&#x200B;です。
      * d1 - 情報が送信されるデータセンターに対応しています（d1、d2 または d3 ）。
      * sc.omtrdc.net — ドメイン名

* **トラッキングサーバーを保護**

   * トラッキングサーバーと同じセグメントが格納されています。
   * セキュリティ保護されているページ（https://）からのデータ送信に使用されます。

* **訪問者の名前空間**

   * 名前空間は、トラッキング URL の最初の部分を決定します。
   * 例えば、名前空間を&#x200B;**CNAME**&#x200B;に変更すると、Adobe Analyticsに対する呼び出しは、デフォルトではなく&#x200B;**CNAME.d1.omtrdc.net**&#x200B;のようになります。

## Adobe Analytics フレームワークへのページの関連付け {#associating-a-page-with-a-adobe-analytics-framework}

ページがAdobe Analyticsフレームワークに関連付けられている場合、ページはページの読み込み時にAdobe Analyticsにデータを送信します。 ページに設定される変数は、フレームワークの Adobe Analytics 変数からマッピングされ、取得されます。例えば、ページビューは Adobe Analytics から取得されます。

ページの子は、フレームワークとの関連付けを継承します。例えば、サイトのルートページをフレームワークに関連付けると、サイトのすべてのページがそのフレームワークに関連付けられます。

1. **サイト**&#x200B;コンソールから、トラッキングを設定するページを選択します。
1. コンソールから直接、またはページエディターから&#x200B;**[ページのプロパティ](/help/sites-authoring/editing-page-properties.md)**&#x200B;を開きます。
1. 「**Cloud Services**」タブを開きます。

1. 「**設定を追加**」ドロップダウンを使用して、使用可能なオプションから「**Adobe Analytics**」を選択します。 継承が設定されている場合、セレクターが使用可能になる前に無効にする必要があります。

1. **Adobe Analytics** のドロップダウンセレクターに、利用可能なオプションが追加されます。これを使用して、必要なフレームワーク設定を選択します。

1. 「**保存して閉じる**」を選択します。
1. ページを&#x200B;**[公開](/help/sites-authoring/publishing-pages.md)**&#x200B;して、ページおよび接続された設定／ファイルをアクティベートします。
1. 最後に、パブリッシュインスタンス上のページを訪問し、**検索**&#x200B;コンポーネントを使用してキーワード（例：aubergine）を検索します。
1. その後、適切なツールを使用して、Adobe Analyticsへの呼び出しを確認できます。例えば、[Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html)とします。
1. 提供されている呼び出しの例では、入力された値（例：aubergine）が eVar7 に格納され、イベントリストが event3 に格納されます。

### ページビュー {#page-views}

ページがAdobe Analyticsフレームワークに関連付けられている場合、ページビュー数をサイトコンソールのリスト表示に表示できます。

詳しくは、[ページ分析データの表示](/help/sites-authoring/page-analytics-using.md)を参照してください。

### 読み込み間隔の設定  {#configuring-the-import-interval}

**Adobe AEM ポーリング設定管理**&#x200B;サービスの適切なインスタンスを設定します。

* **ポール間隔**：サービスが Adobe Analytics からページビューデータを取得する間隔（秒）。デフォルトの間隔は 43200000 ms（12 時間）です。

* **有効にする**：サービスを有効または無効にします。デフォルトでは、このサービスは有効です。

このOSGiサービスを設定するには、[Webコンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または[リポジトリ内のosgiConfigノード（サービスPIDは`com.day.cq.polling.importer.impl.ManagedPollConfigImpl`）を使用します。](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)

## Adobe Analytics 設定やフレームワークの編集 {#editing-adobe-analytics-configurations-and-or-frameworks}

Adobe Analytics 設定またはフレームワークを作成する場合のように、（従来の）**クラウドサービス**&#x200B;画面に移動します。「**設定を表示**」を選択して、更新する特定の設定へのリンクをクリックします。

Adobe Analytics設定の編集時に、**コンポーネントを編集**&#x200B;ダイアログを開くには、設定ページ自体が表示されているときに「**Edit**」ボタンを押す必要もあります。

## Adobe Analytics フレームワークの削除 {#deleting-adobe-analytics-frameworks}

Adobe Analytics フレームワークを削除するには、まず、[編集するためにフレームワークを開きます](#editing-adobe-analytics-configurations-and-or-frameworks)。

次に、サイドキックの「**ページ**」タブから、「**フレームワークを削除**」を選択します。
