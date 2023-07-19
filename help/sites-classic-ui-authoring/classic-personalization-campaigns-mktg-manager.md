---
title: Marketing Campaign Manager の使用
seo-title: Working with the Marketing Campaign Manager
description: マーケティングキャンペーンマネージャー (MCM) は、マルチチャネルキャンペーンの管理に役立つコンソールです。 このマーケティングオートメーションソフトウェアを使用すると、すべてのブランド、キャンペーン、エクスペリエンスを、関連するセグメント、リスト、リード、レポートと共に管理できます。
seo-description: The Marketing Campaign Manager (MCM) is a console that helps you manage multi-channel campaigns. With this marketing automation software you can manage all your brands, campaigns and experiences together with the related segments, lists, leads, and reports.
uuid: 63b817e4-34b9-42b8-845b-e0b7d9af3a96
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 11ff8bb3-39eb-4f77-b3dc-720262fa7f3f
docset: aem65
exl-id: 0e13112b-d9df-4ba6-bd73-431c87890b79
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 38%

---

# Marketing Campaign Manager の使用 {#working-with-the-marketing-campaign-manager}

AEMのマーケティングキャンペーンマネージャー (MCM) は、マルチチャネルキャンペーンの管理に役立つコンソールです。 このマーケティングオートメーションソフトウェアを使用すると、すべてのブランド、キャンペーン、エクスペリエンスを、関連するセグメント、リスト、リード、レポートと共に管理できます。

MCM はAEMの様々な場所からアクセスできます。例えば、キャンペーンアイコンや URL を使用したようこそ画面では、次のように表示されます。

`https://<hostname>:<port>/libs/mcm/content/admin.html`

次に例を示します。

`https://localhost:4502/libs/mcm/content/admin.html`

![screen_shot_2012-02-21at114636am](assets/screen_shot_2012-02-21at114636am.png)

MCM から、以下にアクセスできます。

* **[ダッシュボード](#dashboard)**
以下の 4 つのウィンドウに分かれています。

   * [リスト](#lists)
このウィンドウには作成済みのリストと、そのリスト内のリード数が表示されます。このウィンドウから直接新しいリストを作成したり、リードを読み込んで新しいリストを作成することができます。
特定のリストを選択すると「[リスト](#lists)」セクションに移動し、リストの詳細が表示されます。

   * [セグメント](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#anoverviewofsegmentation)
このパネルには定義済みのセグメントが表示されます。セグメントを使用して、特定の特性を共有する訪問者のコレクションに対してその特徴を設定できます。
特定のセグメントを選択すると、セグメント定義ページが開きます。

   * [レポート](/help/sites-administering/reporting.md)
インスタンスの状態を分析したり監視したりする際に役立つ各種のレポートが提供されます。この MCM パネルにはレポートが一覧表示されます。
レポートを選択すると、レポートページが開きます。

   * [キャンペーン](#campaigns)
このウィンドウには[ニュースレター](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)や[ティーザー](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)などのキャンペーンエクスペリエンスが一覧表示されます。

* **[リード](#leads)**
このウィンドウでリードを管理できます。リードの作成または読み込みを行ったり、個別のリードの詳細を編集したり、不要になった場合は削除したりできます。リードをリストと呼ばれる様々なグループに配置することもできます。**注意：**この機能が今後強化される予定はありません。
[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **[リスト](#lists)**
このウィンドウで（リードの）リストを管理できます。**注意：**この機能が今後強化される予定はありません。
[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

* **[キャンペーン](#campaigns)**
ここからブランド、キャンペーンおよびエクスペリエンスを管理できます。

## ダッシュボード {#dashboard}

ダッシュボードには、（リードの）リスト、セグメント、レポートおよびキャンペーンの概要を示す 4 つのペインが表示されます。 これらの基本機能には、こちらからもアクセスできます。

![mcm_dashboard](assets/mcm_dashboard.png)

### リード数 {#leads}

>[!NOTE]
>
>この機能（リードの管理）がさらに強化される予定はありません。
>[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

AEM MCM では、リードを手動で入力するか、コンマ区切りのリストを読み込むことで、リードを整理して追加できます。例えば、メーリングリストなどです。 リードを生成するその他の方法は、ニュースレターのサインアップまたはコミュニティのサインアップです ( 設定に応じて、リードを入力するワークフローをトリガーできます )。 通常、リードは分類され、リストに入れられ、後でリスト全体に対してアクションを実行できるようになります。例えば、特定のリストにカスタム e メールを送信する場合などです。

の下 **リード** 左側のウィンドウでは、リードの作成、インポート、編集、削除を行い、必要に応じてアクティベートまたはアクティベート解除を行うことができます。 リードをリストに追加したり、既にリードが属しているリストを確認したりできます。

>[!NOTE]
>
>特定の作業について詳しくは、[リードの使用](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithleads)を参照してください。

![screen_shot_2012-02-21at114748am-1](assets/screen_shot_2012-02-21at114748am-1.png)

### リスト {#lists}

>[!NOTE]
>
>この機能（リストの管理）がさらに強化される予定はありません。
>[Adobe Campaign や AEM との統合を利用](/help/sites-administering/campaign.md)することをお勧めします。

リストを使用して、リードをグループに整理できます。 リストを使用すると、選択した人々のグループに対してマーケティングキャンペーンのターゲットを設定できます。例えば、対象のニュースレターをリストに送信できます。

の下 **リスト**&#x200B;を使用すると、必要に応じてリストを作成、読み込み、編集、結合および削除してリストを管理できます。リストは必要に応じて有効化または非アクティブ化できます。 また、リスト内のリードを表示したり、リストが別のリストのメンバーか、説明を表示したりすることもできます。

>[!NOTE]
>
>特定の作業について詳しくは、[リストの使用](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)を参照してください。

![screen_shot_2012-02-21at124828pm-1](assets/screen_shot_2012-02-21at124828pm-1.png)

### キャンペーン {#campaigns}

>[!NOTE]
>
>特定の作業について詳しくは、[ティーザーと戦略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)、[キャンペーンの設定](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupyourcampaign)および[ニュースレター](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)を参照してください。

既存のキャンペーンにアクセスするには、MCM で「**キャンペーン**」をクリックします。

![screen_shot_2012-02-21at11106pm](assets/screen_shot_2012-02-21at11106pm.png)

* **左側のパネル**：
すべてのブランドとキャンペーンのリストが表示されます。
ブランドをシングルクリックすると、次の両方がおこなわれます。

   * リストを展開して、左側のウィンドウに関連するすべてのキャンペーンを表示します。このリストには、各キャンペーンに存在するエクスペリエンスの数も表示されます。
   * 右側のウィンドウで「ブランドの概要」を開きます。

* **右側のパネル**：
ブランドごとにアイコンが表示されます（過去のキャンペーンは表示されません）。
これらをダブルクリックすると、ブランドの概要が表示されます。

#### ブランドの概要 {#brand-overview}

![mcm_brandoverview](assets/mcm_brandoverview.png)

ここから次の操作ができます。

* このブランドに存在するキャンペーンおよびエクスペリエンスの数（左側のパネルに表示される数）を確認します。
* の作成 **新規…** キャンペーンを作成します。

* 表示されている期間を変更する。選択 **週**, **月** または **四半期**、矢印を使用して特定の期間を選択するか、または次の期間に戻ります。 **今日**.

* （右側のウィンドウで）キャンペーンを選択して、次の操作を実行します。

   * を編集します。 **プロパティ…**
   * **削除** キャンペーン。

* キャンペーンの概要を開きます（右側のウィンドウでキャンペーンをダブルクリックするか、左側のウィンドウでシングルクリックします）。

#### キャンペーンの概要 {#campaign-overview}

個々のキャンペーンに対して、次の 2 つのビューを使用できます。

1. **カレンダー表示**

   アイコンを使用します。

   ![カレンダー表示](do-not-localize/mcm_iconcalendarview.png)

   すべてのタッチポイント（グレー）のリストと、そのタッチポイントに接続されたエクスペリエンス（緑）の水平期間が表示されます。

   ![mcm_banner_calendarview](assets/mcm_banner_calendarview.png)

   ここから次の操作ができます。

   * 矢印を使用して表示している期間を変更するか、またはに戻ります。 **今日**.

   * 用途 **タッチポイントを追加…** 既存のエクスペリエンスに新しいタッチポイントを追加する場合。

   * （右側のウィンドウで）ティーザーをクリックして、 **オンタイム** および **オフタイム**.

1. **リスト表示**

   アイコンを使用します。

   ![リスト表示](do-not-localize/mcm_icon_listview.png)

   選択したキャンペーンのすべてのエクスペリエンス（ティーザーやニュースレターなど）が一覧表示されます。

   ![mcm_banner_listview](assets/mcm_banner_listview.png)

   ここから次の操作ができます。

   * 「**新規...**」を使用して、Adobe Target オファー、ティーザー、ニュースレターなどの新しいエクスペリエンスを作成します。
   * **編集** 特定のティーザーページまたはニュースレターの詳細（ダブルクリックも使用できます）。
   * 次を定義： **プロパティ…** 特定のティーザーページまたはニュースレター用。
   * 「**シミュレート**」を使用して、エクスペリエンス（ティーザーページやニュースレター）のルックアンドフィールをシミュレートします。
シミュレーションされたページが開いたら、サイドキックを開いて、そのページの編集モードに切り替えることができます。

   * **分析…** ページに対して生成されたインプレッション。

   * **削除** 不要になった項目
   * 「**検索**」を使用して、テキストを検索します（エクスペリエンスのタイトルフィールドが検索されます）。
   * 用途 **詳細** 検索を実行して、検索にフィルターを適用します。

### キャンペーンエクスペリエンスのシミュレーション {#simulating-your-campaign-experiences}

MCM で、 **キャンペーン**. リストビューがアクティブになっていることを確認し、必要なキャンペーンエクスペリエンスを選択して、 **シミュレート**. タッチポイント（ティーザーまたはニュースレターページ）が開き、選択したエクスペリエンスが訪問者に表示されるので、そのエクスペリエンスが表示されます。

![mcm_simulateexperience](assets/mcm_simulateexperience.png)

ここから、サイドキックを開き（小さい下矢印をクリック）、ページを更新するための編集モードに切り替えることもできます。

### キャンペーンエクスペリエンスの分析 {#analyzing-your-campaign-experiences}

MCM で、 **キャンペーン**. リスト表示がアクティブであることを確認し、必要なキャンペーンエクスペリエンスを選択して、 **分析…**. ページインプレッション数の推移のグラフが表示されます。

![mcm_campaignanalyze](assets/mcm_campaignanalyze.png)
