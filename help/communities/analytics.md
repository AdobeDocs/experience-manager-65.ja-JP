---
title: コミュニティ機能のための Analytics の設定
seo-title: Analytics Configuration for Communities Features
description: Communities のための Analytics の設定
seo-description: Configure analytics for Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: 0f7d4aba0b8c79039918e1338007a4277a5030f2
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 47%

---

# コミュニティ機能のための Analytics の設定 {#analytics-configuration-for-communities-features}

## 概要 {#overview}

Adobe Analytics と Adobe Experience Manager（AEM）は、どちらも Adobe Marketing Cloud のソリューションです。

Adobe Analytics を AEM Communities と連携させ、サポートされるコミュニティ機能をメンバーが操作した際にイベントが Adobe Analytics に送信され、レポートが生成されるように設定することができます。

例えば、イネーブルメントコミュニティサイトのメンバーが自分に割り当てられているビデオリソースを再生すると、リソースプレイヤーによって、イベント（ビデオハートビートのデータを含む）が自動的に Analytics に送信されます。コミュニティサイトから、管理者はビデオの再生に関する様々なレポートを表示できます。

さらに、Analytics は以下の処理のために必要です。

* パブリッシュ環境では、次の操作を実行します。

   * コミュニティのレポート [トレンド](/help/communities/trends.md)
   * サイト訪問者に対し、「最も多く閲覧された」、「最もアクティブ」、「最も「いいね！」が多い」での並べ替えを許可
   * UGC リストでの表示回数

* オーサー環境では、次の操作をおこないます。

   * でのパーティシペーションデータの表示 [メンバー管理コンソール](/help/communities/members.md) （閲覧、投稿、フォロー、「いいね！」）
   * トレンドの概要、ビデオハートビート、イネーブルメントリソース用のビデオデバイス [レポート](/help/communities/reports.md)

サポートされるコミュニティ機能は以下のとおりです。

* [イネーブルメントリソース](/help/communities/resources.md)
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [ブログ](/help/communities/blog-feature.md)
* [ファイルライブラリ](/help/communities/file-library.md)
* [Calendar](/help/communities/calendar.md)

ドキュメントのこのセクションでは、Analytics のレポートスイートとコミュニティ機能を接続する方法について説明します。基本的な手順は以下のとおりです。

1. すべての AEM インスタンス上で暗号化や復号化が正しく実行されるよう、[暗号鍵をレプリケート](#replicate-the-crypto-key)する
1. Adobe Analytics の[レポートスイート](#adobe-analytics-report-suite-for-video-reporting)を準備する
1. AEM Analytics [クラウドサービス](#aem-analytics-cloud-service-configuration)と[フレームワーク](#aem-analytics-framework-configuration)を作成する

1. [Analytics を有効にする](#enable-analytics-for-a-community-site) コミュニティサイトの
1. Analytics と AEM 変数との間のマッピングを&#x200B;[**検証**](#verify-analytics-to-aem-variable-mapping)&#x200B;する
1. 特定 [主発行者](#primary-publisher)
1. [公開](#publish-community-site-and-analytics-cloud-service) コミュニティサイト
1. 設定 [レポートデータのインポート](#obtaining-reports-from-analytics) Adobe Analyticsからコミュニティサイトへ

## 前提条件 {#prerequisites}

Analytics をコミュニティ機能と連携するよう設定するには、アカウント担当者と協力して Adobe Analytics アカウントと[レポートスイート](#adobe-analytics-report-suite-for-video-reporting)をセットアップする必要があります。設定が完了したら、次の情報を利用できるようになります。

* **会社名**

   Adobe Analyticsアカウントに関連付けられている会社。

* **User Name**

   Analytics アカウントの管理権限を持つユーザーのログインユーザー名です（Web サービスへのアクセス権限を含める必要があります）。

* **パスワード**

   認証済みユーザーのログインパスワード。

* **Analytics データセンター**

   アカウントの Analytics データセンターの URL。

* **レポートスイート**

   使用する Analytics レポートスイートの名前。

## ビデオレポートのための Adobe Analytics レポートスイート {#adobe-analytics-report-suite-for-video-reporting}

Adobe Marketing Cloud の [Report Suite Manager](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)を設定すると、コミュニティサイトでコミュニティ機能のレポートを提供できるように、Analytics レポートスイートを設定できます。

にサインインする [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) と [会社名とユーザー名](/help/communities/analytics.md#prerequisites)を使用する場合、以下の項目を含む新しいレポートスイートまたは既存のレポートスイートを設定できます。

* [11 個のコンバージョン変数](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 経由 **`evar11`** 有効

   * 既存の eVar を再利用（名前を変更）したり、新しい eVar を作成してコミュニティ機能に使用したりできます。

* [7 個の成功イベント](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/success-events/success-event.html)（event）

   * **`event1`** 経由 **`event7`** 有効

   * type **`Counter`**

      * **string not required****`Counter (no subrelations)`**
   * 既存のイベントを転用（名前を変更）したり、新しいイベントを作成してコミュニティ機能に使用したりできます


* [ビデオ管理](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)

   * ビデオレポートコンソール

      * Enable（有効） `Video Core`
      * 保存を選択
   * ビデオコア測定コンソール

      * 選択 `Use Solution Variables`
      * 保存を選択


**新しいレポートスイート**&#x200B;を使用する場合、新しいレポートスイートには、4 個の evar と 6 個の event 変数しかないことに注意してください。コミュニティサイトでは 11 個の ever と 7 個の event 変数が必要です。

**既存のレポートスイート**&#x200B;を使用する場合は、コミュニティサイト用の Analytics フレームワークをアクティベートする前に、[変数マッピングを変更](#modifying-analytics-variable-mapping)する必要があります。

コミュニティ専用の変数に関するご不明な点は、アカウント担当者にお問い合わせください。

>[!CAUTION]
>
>**以下の範囲内の変数を使用している既存のレポートスイートを使用する場合は、**
>
>* **`evar1`** から **`evar11`** まで
>
>* **`event1`** から **`event7`** まで
>
>**次に、コミュニティサイトが公開される前に、** Analytics がコミュニティサイトに対して有効になっている場合に、Analytics 変数に自動的にマッピングされたAEM変数を移動して、既存のマッピングを復元することが重要です。
>
>既存のマッピングを復元し、AEM変数を他の Analytics 変数に移動するには、 [Analytics 変数のマッピングの変更](#modifying-analytics-variable-mapping).
>
>この作業をしておかないと、修復不可能なデータ損傷が発生することがあります。

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Video Heartbeat Analytics のライセンスが必要な場合、 `Marketing Cloud Org Id` が割り当てられます。

次の後にビデオハートビートレポートを有効にするには [ビデオレポート用の Analytics レポートスイートの設定](#adobe-analytics-report-suite-for-video-reporting):

* の作成 [Analytics クラウドサービス](#aem-analytics-cloud-service-configuration)
* 有効にする [コミュニティサイトの分析](#enable-analytics-for-a-community-site)
* を関連付ける `Marketing Cloud Org Id` コミュニティサイトで

この `Marketing Cloud Org Id` は [コミュニティサイトの作成](/help/communities/sites-console.md#enablement) または後から [修正](/help/communities/sites-console.md#modifying-site-properties) コミュニティサイトのプロパティ。

![marketing-org-id](assets/marketing-org-id.png)

Video Heartbeat Analytics が有効な場合、ビデオプレーヤーの JavaScript(JS) コードが、（JS でも）Video Heartbeat ライブラリコードをインスタンス化します。このコードは、10 秒ごとに（設定できない）Analytics ビデオトラッキングサーバーにビデオステータスの更新を送信するすべてのロジックを処理します。

有効にしない場合、Video Heartbeat コードはインスタンス化されず、ビデオの再生状況と再開位置の追跡のみが報告のために SRP に維持されます。

## AEM Analytics クラウドサービス設定 {#aem-analytics-cloud-service-configuration}

オーサーインスタンスの標準 UI を使用して、Adobe AnalyticsとAEMコミュニティサイトを統合する新しい Analytics 統合を作成するには、次の手順を実行します。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL Cloud Services]**
* 下にスクロールして **[!UICONTROL Adobe Analytics]**
* 選択 **[!UICONTROL 今すぐ設定]** または **[!UICONTROL 設定を表示]**

![cloud-config](assets/cloud-config1.png)

### 設定を作成ダイアログ {#create-configuration-dialog}

* 選択 `[+]` 隣のアイコン **[!UICONTROL 利用可能な設定]** 新しい設定を作成するには

設定を作成ダイアログでは、設定を識別するための値を入力します。

![create-cloud-config](assets/cloud-config2.png)

* **タイトル**

   （必須）設定の表示タイトル。
例えば、 *イネーブルメントコミュニティ分析*

* **名前**

   （オプション）指定しない場合、名前はデフォルトで、タイトルから派生した有効なノード名になります。
例えば、「communities」と入力します。**

* **テンプレート**

   選択 `Adobe Analytics Configuration`

* 「**作成**」を選択します。

   * 設定ページを起動して開きます `Analytics Settings` ダイアログ

### Analytics 設定ダイアログ {#analytics-settings-dialog}

新しい Analytics 設定を初めて作成したときには、その設定と、Analytics 設定を入力するための新しいダイアログが表示されます。このダイアログでは、 [前提条件のアカウント情報](#prerequisites) アカウント担当者から取得します。

![analytics-settings](assets/analytics-settings.png)

* **Company（会社）**

   Adobe Analyticsアカウントに関連付けられている会社。

* **ユーザー名**

   Analytics アカウントの管理を許可されたユーザーのログインユーザー名。

* **パスワード**

   認証済みユーザーのログインパスワード。

* **データセンター**

   レポートスイートをホストしている Analytics データセンターを選択します。

* **ページに追跡タグを追加しない**

   デフォルト（選択解除）のままにします。

* **AppMeasurement を使用**

   デフォルト（選択解除）のままにします。

* **ページインプレッション数を夜間に読み込まない (作成者)**

   デフォルト（選択解除）のままにします。

* **ページインプレッション数を夜間に読み込まない (発行)**

   デフォルト（選択解除）のままにします。

設定を保存するには：

* 選択 **Analytics に接続**

   * 成功しなかった場合、

      * エントリの先頭にスペースが含まれていないことを確認します。
      * 別のデータセンターを試してみてください。

* 「**OK**」を選択します。

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### フレームワークの作成 {#create-framework}

Adobe Analytics への基本的な接続を正しく設定したら、コミュニティサイトのフレームワークを作成または編集する必要があります。このフレームワークの目的は、コミュニティ機能 (AEM) 変数を Analytics（レポートスイート）変数にマッピングすることです。

* 選択 `[+]` 隣のアイコン **[!UICONTROL 使用可能なフレームワーク]** 新しいフレームワークを作成するには

   ![analytics-framework](assets/analytics-framework.png)

* **タイトル**

   （必須）フレームワークの表示タイトル。例えば、次のように入力します。 *イネーブルメントコミュニティフレームワーク*.

* **名前**

   （オプション）指定しない場合、名前はデフォルトで、タイトルから派生した有効なノード名になります。
例えば、 *コミュニティ*.

* *テンプレート*

   選択 `Adobe Analytics Framework`.

* 「**作成**」を選択します。

Analytics フレームワークを作成すると、フレームワークを設定するための画面が開きます。

## AEM Analytics フレームワーク設定 {#aem-analytics-framework-configuration}

このフレームワークの目的は、AEM変数を Analytics 変数（eVar およびイベント）にマッピングすることです。 マッピングに使用できる Analytics 変数は次のとおりです [レポートスイートで定義される](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### レポートスイートの選択 {#select-report-suite}

ビデオレポート用にセットアップされているレポートスイートを選択します。

レポートスイートがまだ作成されていない、または適切に設定されていない場合は、前の節を参照してください。
[ビデオレポート用のAdobe Analyticsレポートスイート](#adobe-analytics-report-suite-for-video-reporting)

サイドキックは必要ないので、レポートスイート設定にアクセスするときの邪魔にならないよう最小化しておくことができます。

#### 「項目を追加」選択前および選択後のレポートスイートダイアログ {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

1. 選択 **項目を追加+**.

   2 つのドロップダウンボックスが表示されます。

1. を選択します。 `Report suite.`

   会社アカウントに関連付けられているレポートスイートを選択できます。

1. 選択 **はい** 表示されるダイアログで、次の操作を実行します。

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. を選択します。 `Run Mode`.

1. 「**発行**」を選択します。

![analytics-framework2](assets/analytics-framework2.png)

これで Analytic クラウドサービスとフレームワークの準備が完了しました。マッピングは、この Analytics サービスを有効にしてコミュニティサイトを作成した後に定義されます。

## コミュニティサイトに対する Analytics の有効化 {#enable-analytics-for-a-community-site}

### 新しいコミュニティサイトに対する有効化 {#enable-for-new-community-site}

[新しいコミュニティサイトの作成](/help/communities/sites-console.md)中に Analytics クラウドサービスを追加するには：

* 手順 3 で、 [「ANALYTICS」タブ](/help/communities/sites-console.md#analytics):
   * を選択します。 **Analytics を有効にする** チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* Analytics フレームワーク設定に戻り、変数マッピングを調整します（オプション）。

### 既存のコミュニティサイトに対する有効化 {#enable-for-existing-community-site}

Analytics クラウドサービスを[既存のコミュニティサイト](/help/communities/sites-console.md#modifying-site-properties)に追加するには：

* 次に移動： **コミュニティ/サイト** コンソール。
* コミュニティサイトのサイトを編集アイコンを選択します。
* 設定を選択します。
* 「Analytics」セクションで、以下の操作をおこないます。
   * を選択します。 **Analytics を有効にする** チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* Analytics フレームワーク設定に戻り、変数マッピングを調整します（オプション）。

### カスタマイズされたサイトに対する有効化 {#enable-for-customized-sites}

コミュニティサイトで Analytics の追跡とインポートが正常に機能するようにするには、`scf-js-site-title` クラスと href 属性のページ要素が存在する必要があります。そのような要素は、変更されていないページ内に存在するなど、1 つだけページ上に存在する必要があります `sitepage.hbs` コミュニティサイト用のスクリプト の値 `siteUrl` 抽出され、Adobe Analyticsに *サイトパス*.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

の **カスタマイズされたコミュニティサイト** が `sitepage.hbs` スクリプトを使用する場合は、要素が存在することを確認します。 この `siteUrl` 変数は、クライアントに提供される前にサーバーでレンダリングされる際に設定されます。

Communities コンポーネントが含まれているが[サイト作成ウィザード](/help/communities/sites-console.md)で作成されていない&#x200B;**一般的な AEM サイト**&#x200B;の場合は、要素を追加する必要があります。href の値は、サイトへのパスにする必要があります。 例えば、サイトのパスが `/content/my/company/en`、次を使用します。

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## コミュニティ機能のための Analytics {#analytics-for-communities-features}

Analytics は複数のコミュニティ機能で自動的に使用されます。

オーサー環境の [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`は、Analytics 用に実装されたコンポーネントの一覧を提供します。 変数の自動マッピングは、リストされているコンポーネントによって決定されます。

Analytics 用の新しいカスタムコンポーネントを作成した場合は、この設定済みコンポーネントのリストに追加する必要があります。

### コンポーネントの設定 {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>ジャーナルコンポーネントは、ブログ機能の実装に使用されます。

### Analytics と AEM 変数とのマッピング {#mapped-analytics-to-aem-variables}

Analytics を有効にし、クラウド設定フレームワークを選択した状態でコミュニティサイトを保存すると、AEM変数は、evar1 と event1 で始まる Analytics eVar およびイベントに自動的にマッピングされ、1 ずつ増分されます。

evar1 ～ evar11 および event1 ～ event7 の範囲内のいずれかの変数がマップされた既存のレポートスイートを使用する場合は、[AEM 変数を再マップ](#modifying-analytics-variable-mapping)して、元のマッピングを復元する必要があります。

[使用の手引きのチュートリアル](/help/communities/getting-started-enablement.md)に従った場合のデフォルトのマッピング例を以下に示します。

![map-analytics](assets/map-analytics1.png)

#### 各イベントと共に送信される eVars のマップ {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>イネーブルメント<br />リソース<br />のタイプ</strong></td>
   <td><strong><br />サイトのタイトル</strong></td>
   <td><strong>機能<br />のタイプ</strong></td>
   <td><strong>グループ<br />のタイトル</strong></td>
   <td><strong><br />グループのパス</strong></td>
   <td><strong>UGC<br />のタイプ</strong></td>
   <td><strong>UGC<br />のタイトル</strong></td>
   <td><strong>ユーザー<br />（メンバー）</strong></td>
   <td><strong>UGC<br />のパス</strong></td>
   <td><strong><br />サイトのパス</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> リソース再生</strong></td>
   <td><em>(a)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>(i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(a)</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate（投稿）</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>一</em></td>
   <td><em>（j）</em></td>
  </tr>
 </tbody>
</table>

**eVar の値の例：**

* *[MIME タイプ](https://www.iana.org/assignments/media-types)*:video/mp4
* *[コミュニティサイトのタイトル](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixxコミュニティ
* *[コミュニティ機能名](/help/communities/functions.md)*:フォーラム
* *[コミュニティグループ名](/help/communities/creating-groups.md#creating-a-new-group)*:ハイキング
* *コミュニティグループコンテンツのパス*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC コンポーネント resourceType](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGC コンポーネントのタイトル*:ハイキングトピック
* *login (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *UGC への SRP パス*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
または 
*フォローするコンポーネントのパス*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *コミュニティサイトコンテンツのパス*: `/content/sites/<site name>/en`

### Analytics 変数のマッピングの変更 {#modifying-analytics-variable-mapping}

Analytics の eVar およびイベントとAEM変数とのマッピングは、Analytics をコミュニティサイトで有効にした後、フレームワーク設定から表示されます。

Analytics を有効にした後、コミュニティサイトを公開する前に、フレームワーク内で必要な Analytics の evar または event を左のレールからマッピングテーブルの適切な行にドラッグ＆ドロップすることで、マッピングを変更できます。

マッピングの重複を避けるために、置き換えられた Analytics の evar または event は列から削除するようにしてください（削除するには、カーソルを合わせたときに Analytics 変数要素の右に表示される「X」を選択します）。

コミュニティの eVar とイベントがレポートスイートに以前存在したマッピングを上書きする場合、データの損失を避けるために、コミュニティ機能のAEM変数を他の Analytics eVar またはイベントに割り当て、元のマッピングを復元します。

>[!CAUTION]
>
>Analytics を有効にしたコミュニティサイトを[公開](#publishing-the-community-site)する前に再マップすることが重要です。そうしないと、データが損失するおそれがあります。

#### 手順 1 の例：Analytics の evar14 をマッピングテーブルにドラッグ {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 手順 2 の例：「x」を選択し、置き換える evar11 を削除 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 手順 3 の例：AEM 変数 eventdata.siteId を Analytics の evar14 に再マップ {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## コミュニティサイトの公開 {#publishing-the-community-site}

### Analytics と AEM 変数とのマッピングの検証 {#verify-analytics-to-aem-variable-mapping}

コミュニティサイトの公開前に、変数マッピングを確認することを推奨します。サイトの公開時には、Analytics クラウドサービスとフレームワークも公開されます。

以下の節を参照してください。

* [Analytics と AEM 変数とのマッピング](#mapped-analytics-to-aem-variables)
* [Analytics 変数のマッピングの変更](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**以下の範囲内の変数を使用している既存のレポートスイートを使用する場合は、**
>
>* **`evar1`** から **`evar11`** まで
>
>* **`event1`** から **`event7`** まで
>
>**次に、コミュニティサイトが公開される前に、** 既存のマッピングを復元し、（Analytics がコミュニティサイトで有効になっている場合に）自動的にマッピングされた Communities AEM変数を他の Analytics 変数に移動することが重要です。 この再マッピングは、すべてのコミュニティコンポーネントで一貫している必要があります。
>
>この作業をしておかないと、修復不可能なデータ損傷が発生することがあります。

### プライマリパブリッシャー {#primary-publisher}

選択したデプロイメントが[パブリッシュファーム](/help/communities/topologies.md#tarmk-publish-farm)の場合は、レポートデータのポーリングをおこなう Adobe Analytics が [SRP](/help/communities/working-with-srp.md) に書き込めるよう、1 つの AEM パブリッシュインスタンスをプライマリパブリッシャーに指定する必要があります。

デフォルトでは、 `AEM Communities Publisher Configuration` OSGi 設定では、パブリッシュインスタンスがプライマリパブリッシャーとして識別されます。これにより、パブリッシュファーム内のすべてのパブリッシュインスタンスがプライマリとして自己識別されます。

したがって、すべてのセカンダリパブリッシュインスタンスの設定を編集し、 **プライマリ発行者** チェックボックスをオンにします。

具体的な手順については、 [コミュニティのデプロイ](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>複数のパブリッシュインスタンスからのポーリングを防ぐように、プライマリパブリッシャーを設定することが重要です。

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

Adobe Analytics の資格情報は暗号化されます。オーサーとパブリッシャー間で暗号化された Analytics 資格情報のレプリケーションまたは送信を容易にするには、すべてのAEMインスタンスが同じプライマリ暗号化キーを共有する必要があります。

それには、 [暗号鍵のレプリケート](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### コミュニティサイトと Analytics クラウドサービスの公開 {#publish-community-site-and-analytics-cloud-service}

Analytics クラウドサービスをコミュニティサイトに対して有効にし、また必要に応じて [Analytics 変数と AEM 変数とのマッピングを調整](#mapped-analytics-to-aem-variables)したら、[コミュニティサイトの（再）公開](/help/communities/sites-console.md#publishing-the-site)をおこない、設定をパブリッシュ環境にレプリケートする必要があります。

## Analytics からのレポートの取得 {#obtaining-reports-from-analytics}

### レポート管理 {#report-management}

作成者およびプライマリパブリッシャーの [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`は、Analytics に対するクエリに使用されます。

オーサー環境では、リアルタイムレポートを入手するにはクエリを使用します。

プライマリパブリッシャーでは、レポートインポーターの分析データ読み込みに備えた情報提供のためにクエリを使用します。

クエリの間隔は、デフォルトで 10 秒間です。

### レポートインポーター {#report-importer}

Analytics が有効なコミュニティサイトが公開されると、プライマリパブリッシャーは [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`CRXDE で個別に設定されない設定に対して、デフォルトのポーリング間隔を設定するように設定できます。

ポーリング間隔は、データを取り込んでに保存するためのAdobe Analyticsへのリクエストの頻度を制御します [SRP](/help/communities/working-with-srp.md).

データが「ビッグデータ」に類するものである場合は、ポーリングの頻度を上げるとコミュニティサイトに大きな負荷がかかる場合があります。

デフォルトのポーリングの&#x200B;**読み込みインターバル**&#x200B;は、12 時間に設定されています。

![report-importer](assets/report-importer.png)

### コンポーネントレポートのカスタマイズ {#component-report-customization}

現在、追跡する指標をカスタマイズするには、リポジトリ内にノードを作成し、その指標に関するレポートを生成する期間を定義します。

現在、このカスタマイズの例を確認できるのはフォーラムトピックのみです。

* プライマリパブリッシャーで、管理者権限でログインします。
* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) に移動します。例： [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* 言語ルートの jcr:content ノードの下 ( 例： `/content/sites/engage/en/jcr:content),`Analytics レポート用に設定されたコンポーネントに移動します。
例：**`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 作成された期間に注意してください。

   * `last30Days`
   * `last90Days`
   * `thisYear`

* 注意： `total`ノード。

   * の変更 **`interval`** プロパティは、レポートインポーターの間隔よりも優先されます。
   * 値は秒単位で、4 時間 (14400秒 ) に設定されます。

![component-report](assets/component-report.png)

## Analytics でのユーザーデータの管理 {#manage-user-data-in-analytics}

Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

## リソース {#resources}

* Adobe Experience Cloud: [Analytics ヘルプとリファレンス](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [Adobe Analyticsとの統合](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics と外部プロバイダー](/help/sites-administering/external-providers.md)
