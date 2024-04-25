---
title: コミュニティ機能のための Analytics の設定
description: サポートされている Communities の機能をメンバーがやり取りする際にイベントがAEM Communitiesに送信されるように、Adobe Analytics用にAdobe Analyticsを設定する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2658'
ht-degree: 2%

---

# コミュニティ機能のための Analytics の設定 {#analytics-configuration-for-communities-features}

## 概要 {#overview}

Adobe AnalyticsとAdobe Experience Manager（AEM）は、どちらもAdobe Experience Cloudのソリューションです。

Adobe AnalyticsをAEM Communities用に設定すると、メンバーがサポートされている Communities の機能を操作する際に、イベントがAdobe Analyticsに送信され、そこからレポートが生成されるようになります。

例えば、コミュニティサイトから、管理者はビデオの再生に関する様々なレポートを表示できます。

さらに、以下を行うには分析が必要です。

* パブリッシュ環境で、次の操作を行います。

   * コミュニティのレポート [トレンド](/help/communities/trends.md)
   * サイト訪問者が「最も多く閲覧」、「最もアクティブ」、「最も高評価」で並べ替えられるようにする
   * UGC （ユーザー生成コンテンツ）リストの表示数

* オーサー環境で、次の操作を行います。

   * のパーティシペーション データの表示 [メンバー管理コンソール](/help/communities/members.md) （views, posts, follows, like）
   * イネーブルメントリソースのトレンドサマリ、ビデオハートビートおよびビデオデバイス [報告書](/help/communities/reports.md)

次の Communities 機能がサポートされています。

* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [ブログ](/help/communities/blog-feature.md)
* [ファイルライブラリ](/help/communities/file-library.md)
* [Calendar](/help/communities/calendar.md)

この節では、Analytics レポートスイートを Communities 機能と接続する方法について説明します。 基本的な手順は次のとおりです。

1. [暗号鍵をレプリケートします](#replicate-the-crypto-key) これにより、すべてのAEM インスタンスで暗号化/復号化が正しく行われることを確認できます
1. Adobe Analyticsの準備 [レポートスイート](#adobe-analytics-report-suite-for-video-reporting)
1. AEM Analytics の作成 [クラウドサービス](#aem-analytics-cloud-service-configuration) および [フレームワーク](#aem-analytics-framework-configuration)

1. [Analytics の有効化](#enable-analytics-for-a-community-site) コミュニティサイト用
1. [**検証**](#verify-analytics-to-aem-variable-mapping) Analytics からAEMへの変数マッピング
1. 識別 [プライマリ発行者](#primary-publisher)
1. [公開](#publish-community-site-and-analytics-cloud-service) コミュニティサイト
1. 設定 [レポートデータのインポート](#obtaining-reports-from-analytics) Adobe Analyticsからコミュニティサイト

## 前提条件 {#prerequisites}

Analytics for Communities の機能を設定するには、アカウント担当者と協力してAdobe Analytics アカウントを設定する必要があります。 [レポートスイート](#adobe-analytics-report-suite-for-video-reporting). 設定が完了すると、次の情報が利用できるようになります。

* **会社名**

  Adobe Analytics アカウントに関連付けられている会社。

* **ユーザー名**

  Analytics アカウントの管理を許可されたユーザーのログインユーザー名（web サービスのアクセス権限を含む必要があります）。

* **パスワード**

  許可されたユーザーのログインパスワード。

* **Analytics データセンター**

  アカウントの Analytics データセンターの URL。

* **レポートスイート**

  使用する Analytics レポートスイートの名前。

## ビデオレポート用のAdobe Analytics レポートスイート {#adobe-analytics-report-suite-for-video-reporting}

Adobe Experience Cloudの使用 [レポートスイートマネージャー](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/new-report-suite.html?lang=ja)を使用すると、コミュニティサイトでコミュニティ機能のレポートを提供できるように、Analytics レポートスイートを設定できます。

にログインする [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=ja) （を使用） [会社名とユーザー名](/help/communities/analytics.md#prerequisites)新規または既存のレポートスイートに次の情報を設定できます。

* [11 コンバージョン変数](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/conversion-var-admin.html?lang=ja) （eVars）

   * **`evar1`** から **`evar11`** enabled

   * 既存の eVar の再利用（名前変更）や、Communities 機能に使用する eVar の作成が可能

* [7 成功イベント](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/success-events/success-event.html?lang=ja) （イベント）

   * **`event1`** から **`event7`** enabled

   * type **`Counter`**

      * ではない **`Counter (no subrelations)`**

   * 既存のイベントを再利用（名前変更）したり、コミュニティ機能に使用するイベントを作成したりできます。

* [ビデオ管理](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=ja)

   * ビデオレポートコンソール

      * Enable （有効） `Video Core`
      * 「保存」を選択します。

   * ビデオコア測定コンソール

      * `Use Solution Variables` を選択します。
      * 「保存」を選択します。

を使用する場合 **新しいレポートスイート**&#x200B;の場合、新しいレポートスイートには 4 つの evar と 6 つのイベント変数のみを含めることができますが、コミュニティには 11 つの evar と 7 つのイベント変数が必要です。

を使用する場合 **既存のレポートスイート**&#x200B;の場合、次が必要になる可能性があります [変数マッピングの変更](#modifying-analytics-variable-mapping) コミュニティサイト用の Analytics フレームワークをアクティブ化する前に。

Communities 専用の変数に関するご懸念は、アカウント担当者にお問い合わせください。

>[!CAUTION]
>
>**内で変数を使用している既存のレポートスイートを使用する場合**
>
>* **`evar1`** から **`evar11`** まで
>
>* **`event1`** から **`event7`** まで
>
>**その後、コミュニティサイトを公開する前に、** コミュニティサイトに対して Analytics が有効になっている場合に、Analytics 変数に自動的にマッピングされたAEM変数を移動して、既存のマッピングを復元することが重要です。
>
>既存のマッピングを復元し、AEM変数を他の Analytics 変数に移動するには、の節を参照してください。 [Analytics 変数マッピングの変更](#modifying-analytics-variable-mapping).
>
>これに従わないと、回復不可能なデータ損失が発生する可能性があります。

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Video Heartbeat Analytics のライセンスがある場合、 `Marketing Cloud Org Id` が割り当てられています。

次の手順でビデオハートビートレポートを有効にします [ビデオレポート用の Analytics レポートスイートの設定](#adobe-analytics-report-suite-for-video-reporting):

* を作成 [Analytics Cloud サービス](#aem-analytics-cloud-service-configuration)
* Enable （有効） [コミュニティサイトの分析](#enable-analytics-for-a-community-site)
* を関連付けます `Marketing Cloud Org Id` コミュニティサイトを使用

この `Marketing Cloud Org Id` の時点で入力できます [コミュニティサイトの作成](/help/communities/sites-console.md) またはそれ以降の基準 [変更中](/help/communities/sites-console.md#modifying-site-properties) コミュニティサイトのプロパティ。

![marketing-org-id](assets/marketing-org-id.png)

ビデオハートビート分析が有効になっていると、ビデオプレーヤーの JavaScript （JS）コードがビデオハートビートライブラリコード（これも JS にある）をインスタンス化します。 このコードは、10 秒ごとに Analytics ビデオトラッキングサーバーにビデオステータスの更新を送信するすべてのロジックを処理します（設定はできません）。 最終的には、ビデオセッションの累積レポートがメインの Analytics サーバーに送信されます。

有効にしない場合、ビデオハートビートコードはインスタンス化されず、ビデオの進行状況と再開位置のトラッキングのみがレポート用に SRP に保持されます。

## AEM Analytics Cloud サービスの設定 {#aem-analytics-cloud-service-configuration}

オーサーインスタンスの標準 UI を使用して、Adobe AnalyticsをAEM コミュニティサイトと統合する Analytics 統合を作成するには、次のようにします。

* グローバルナビゲーションから： **[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL Cloud Service]**
* Scroll-down to **[!UICONTROL Adobe Analytics]**
* を選択 **[!UICONTROL 今すぐ設定]** または **[!UICONTROL 設定を表示]**

![cloud-config](assets/cloud-config1.png)

### 設定を作成ダイアログ {#create-configuration-dialog}

* を選択 `[+]` アイコンの隣 **[!UICONTROL 利用可能な設定]** そのため、設定を作成できます。

設定を作成ダイアログで、入力する値が設定を識別します。

![create-cloud-config](assets/cloud-config2.png)

* **タイトル**

  （必須）設定の表示タイトル。
例えば、 *コミュニティ分析*

* **名前**

  （オプション）指定しない場合、名前はデフォルトでタイトルから派生した有効なノード名になります。
例えば、 *コミュニティ*

* **テンプレート**

  `Adobe Analytics Configuration` を選択します。

* 「**作成**」を選択します。

   * ローンチ設定ページと開封数 `Analytics Settings` dialog

### Analytics 設定ダイアログ {#analytics-settings-dialog}

新しい Analytics 設定を最初に作成すると、設定が表示され、Analytics 設定を入力するための新しいダイアログが表示されます。 このダイアログには、 [前提条件のアカウント情報](#prerequisites) アカウント担当者から取得します。

![analytics-settings](assets/analytics-settings.png)

* **会社**

  Adobe Analytics アカウントに関連付けられている会社。

* **ユーザー名**

  Analytics アカウントの管理を許可されたユーザーのログインユーザー名。

* **パスワード**

  許可されたユーザーのログインパスワード。

* **データセンター**

  レポートスイートをホストする Analytics データセンターを選択します。

* **ページにトラッキングタグを追加しない**

  デフォルトのままにします（選択解除）。

* **AppMeasurementを使用**

  デフォルトのままにします（選択解除）。

* **毎晩ページインプレッションをインポートしない（オーサー）**

  デフォルトのままにします（選択解除）。

* **夜間にページインプレッションを読み込まない（公開）**

  デフォルトのままにします（選択解除）。

設定を保存するには：

* を選択 **Analytics への接続**

   * 成功しなかった場合、

      * エントリの先頭にスペースが含まれていないことを確認します。
      * 別のデータセンターを試してください。

* 「**OK**」を選択します。

  ![analytics-settings](assets/analytics-settings1.png)

### フレームワークを作成 {#create-framework}

Adobe Analyticsへの基本的な接続が正常に設定されたら、コミュニティサイトのフレームワークを作成または編集する必要があります。 フレームワークの目的は、Communities 機能（AEM）変数を Analytics （レポートスイート）変数にマッピングすることです。

* を選択 `[+]` アイコンの隣 **[!UICONTROL 使用可能なフレームワーク]** そのため、フレームワークを作成できます。

  ![analytics-framework](assets/analytics-framework.png)

* **タイトル**

  （必須） フレームワークの表示タイトル。例： *コミュニティフレームワーク*.

* **名前**

  （オプション）指定しない場合、名前はデフォルトでタイトルから派生した有効なノード名になります。
例えば、 *コミュニティ*.

* *テンプレート*

  `Adobe Analytics Framework` を選択します。

* 「**作成**」を選択します。

Analytics フレームワークを作成すると、設定用のフレームワークが開きます。

## AEM Analytics フレームワークの設定 {#aem-analytics-framework-configuration}

フレームワークの目的は、AEM変数を Analytics 変数（eVar とイベント）にマッピングすることです。 マッピングに使用できる Analytics 変数は次のとおりです [レポートスイートで定義](#adobe-analytics-report-suite-for-video-reporting).

![analytics-framework](assets/analytics-framework1.png)

### レポートスイートの選択 {#select-report-suite}

ビデオレポート用に設定されたレポートスイートを選択します。

レポートスイートがまだ作成されていない場合や、適切に設定されていない場合は、前の節を参照してください。
[ビデオレポート用のAdobe Analytics レポートスイート](#adobe-analytics-report-suite-for-video-reporting)

Sidekickは不要で、レポートスイート設定へのアクセスの妨げにならないように最小化できます。

#### 「項目を追加」を選択する前後のレポートスイートダイアログ {#report-suites-dialog-before-and-after-selecting-add-item}

![report-suite](assets/report-suite.png)

1. を選択 **項目を追加+**.

   2 つのドロップダウンボックスが表示されます。

1. を選択 `Report suite.`

   会社アカウントに関連付けられているレポートスイートを選択できます。

1. を選択 **はい** 開いたダイアログで、次の操作を行います。

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. を選択 `Run Mode`.

1. 「**公開**」を選択します。

![analytics-framework2](assets/analytics-framework2.png)

これで、Analytic Cloud サービスとフレームワークが完了しました。 マッピングは、この Analytics サービスを有効にしてコミュニティサイトを作成した後に定義されます。

## コミュニティサイトに対して Analytics を有効にする {#enable-analytics-for-a-community-site}

### 新しいコミュニティサイトを有効にする {#enable-for-new-community-site}

次の場合にAnalytics Cloud サービスを追加します [コミュニティサイトの作成](/help/communities/sites-console.md):

* 手順 3 で、の下の [「ANALYTICS」タブ](/help/communities/sites-console.md#analytics):
   * 「」を選択します **Analytics の有効化** チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* オプションで、Analytics フレームワーク設定に戻って変数のマッピングを調整します。

### 既存のコミュニティサイトに対して有効にする {#enable-for-existing-community-site}

にAnalytics Cloud サービスを追加するには [既存のコミュニティサイト](/help/communities/sites-console.md#modifying-site-properties):

* に移動します。 **コミュニティ / サイト** コンソール。
* コミュニティサイトのサイトを編集アイコンを選択します。
* 設定を選択します。
* 「Analytics」セクションで、
   * 「」を選択します **Analytics の有効化** チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* オプションで、Analytics フレームワーク設定に戻って変数のマッピングを調整します。

### カスタマイズされたサイトで有効にする {#enable-for-customized-sites}

Analytics でのトラッキングと読み込みがコミュニティサイトで正しく機能するようにするには、ページ要素に `scf-js-site-title` class 属性と href 属性が存在する必要があります。 変更されていない場合のように、このような要素は 1 つだけページに存在する必要があります `sitepage.hbs` コミュニティサイト用のスクリプト。 次の値 `siteUrl` が抽出され、としてAdobe Analyticsに送信されます *サイトパス*.

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

の場合 **カスタマイズされたコミュニティサイト** をオーバーレイ `sitepage.hbs` スクリプトを使用します。要素が存在することを確認してください。 この `siteUrl` 変数は、クライアントに提供する前にサーバーでレンダリングされるときに設定されます。

の場合 **汎用AEM サイト** これには Communities コンポーネントが含まれますが、 [サイト作成ウィザード](/help/communities/sites-console.md)を作成する場合は、要素を追加する必要があります。 href の値は、サイトへのパスである必要があります。 例えば、サイトのパスがの場合 `/content/my/company/en`を設定する場合は、次を使用します。

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Analytics for Communities の機能 {#analytics-for-communities-features}

Analytics は、複数の Communities 機能で自動的に使用されます。

オーサー環境 [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`は、Analytics 用に実装されたコンポーネントのリストを提供します。 変数の自動マッピングは、リストされるコンポーネントによって決まります。

Analytics 用に実装された新しいカスタムコンポーネントが作成された場合は、設定済みコンポーネントのこのリストに追加してください。

### コンポーネント設定 {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>ジャーナルコンポーネントは、ブログ機能を実装するために使用されます。

### Analytics からAEMへのマッピング変数 {#mapped-analytics-to-aem-variables}

Analytics を有効にし、クラウド設定フレームワークを選択して、コミュニティサイトを保存すると、AEM変数が Analytics の eVar とイベントに自動的にマッピングされます。 evar1 と event1 で始まり、それぞれ 1 ずつ増分されます。

evar1 から evar11 および event1 から event7 内の変数のいずれかをマッピングした既存のレポートスイートを使用する場合、次が必要になります。 [AEM変数の再マッピング](#modifying-analytics-variable-mapping) 元のマッピングを復元します。

デフォルトのマッピングの例を次に示します。

![map-analytics](assets/map-analytics1.png)

#### 各イベントで送信された eVar のマップ {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>イネーブルメント<br /> Resource<br /> タイプ</strong></td>
   <td><strong>サイト<br /> タイトル</strong></td>
   <td><strong>関数<br /> タイプ</strong></td>
   <td><strong>グループ<br /> タイトル</strong></td>
   <td><strong>グループ<br /> パス</strong></td>
   <td><strong>UGC<br /> タイプ</strong></td>
   <td><strong>UGC<br /> タイトル</strong></td>
   <td><strong>ユーザー<br /> （社員）</strong></td>
   <td><strong>UGC<br /> パス</strong></td>
   <td><strong>サイト<br /> パス</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>EVAR4</strong></td>
   <td><strong>EVAR5</strong></td>
   <td><strong>EVAR6</strong></td>
   <td><strong>EVAR7</strong></td>
   <td><strong>EVAR8</strong></td>
   <td><strong>EVAR9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> リソース再生</strong></td>
   <td><em>イ</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>（1）</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFVview</strong></td>
   <td><em>イ</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate （Post）</strong></td>
   <td><em>-</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>ロ</em></td>
   <td><em>ハ</em></td>
   <td><em>ニ</em></td>
   <td><em>ホ</em></td>
   <td><em>（へ）</em></td>
   <td><em>（g）</em></td>
   <td><em>（チ）</em></td>
   <td><em>（1）</em></td>
   <td><em>（ヌ）</em></td>
  </tr>
 </tbody>
</table>

**eVar値の例は次のとおりです。**

* *[MIME タイプ](https://www.iana.org/assignments/media-types/media-types.xhtml)*: video/mp4
* *[コミュニティサイトのタイトル](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixxコミュニティ
* *[コミュニティ関数名](/help/communities/functions.md)*：フォーラム
* *[コミュニティグループ名](/help/communities/creating-groups.md#creating-a-new-group)*：ハイキング
* *コミュニティグループコンテンツへのパス*: `/content/sites/<site name>/en/groups/hiking`
* *[UGC コンポーネント resourceType](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGC コンポーネントタイトル*：ハイキングのトピック
* *ログイン （authorizableId）*: `aaron.mcdonald@mailinator.com`
* *UGC への SRP パス*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
または *フォローするコンポーネントのパス*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *コミュニティサイトコンテンツへのパス*: `/content/sites/<site name>/en`

### Analytics 変数マッピングの変更 {#modifying-analytics-variable-mapping}

コミュニティサイトに対して Analytics を有効にすると、Analytics eVar とイベントのAEM変数へのマッピングがフレームワーク設定に表示されます。

Analytics を有効にした後、コミュニティサイトを公開する前に、フレームワークでマッピングを変更できます。 目的の Analytics eVar またはイベントを左パネルからドラッグし、マッピングテーブルの関連する行にドロップするだけです。

マッピングの重複を避けるには、置き換えた Analytics evar またはイベントにカーソルを合わせ、Analytics 変数要素の右側に表示される「X」を選択して、その行から削除してください。

Communities の eVar とイベントで、レポートスイートに以前に存在したマッピングが上書きされる場合、データの損失を避けるために、Communities の機能のAEM変数を他の Analytics eVar またはイベントに割り当て、元のマッピングを復元します。

>[!CAUTION]
>
>コミュニティサイトをマッピングし直す前に再マッピングすることが重要です [公開日](#publishing-the-community-site) analytics を有効にすると、データが失われるリスクがあります。

#### 例 1:Analytics evar14 のマッピングテーブルへのドラッグ {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### 例ステップ 2:「x」を選択して、置き換えられた evar11 を削除 {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### 例 3:AEM var eventdata.siteId が Analytics evar14 に再マッピングされる {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## コミュニティサイトの公開 {#publishing-the-community-site}

### Analytics からAEMへの変数マッピングの検証 {#verify-analytics-to-aem-variable-mapping}

コミュニティサイトでは、Analytics Cloud サービスおよびフレームワークも公開します。その前に、変数マッピングを確認することをお勧めします。

セクションを参照：

* [Analytics からAEMへのマッピング変数](#mapped-analytics-to-aem-variables)
* [Analytics 変数マッピングの変更](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**内で変数を使用している既存のレポートスイートを使用する場合**
>
>* **`evar1`** から **`evar11`** まで
>
>* **`event1`** から **`event7`** まで
>
>**その後、コミュニティサイトを公開する前に、** 既存のマッピングを復元します。 （コミュニティサイトに対して Analytics が有効になっている場合に）自動的にマッピングされた Communities AEM変数を他の Analytics 変数に移動します。 この再マッピングは、すべてのコミュニティコンポーネントで一貫している必要があります。
>
>これに従わないと、回復不可能なデータ損失が発生する可能性があります。

### プライマリ発行者 {#primary-publisher}

選択したデプロイメントが [パブリッシュファーム](/help/communities/topologies.md#tarmk-publish-farm)に設定した場合は、1 つのAEM パブリッシュインスタンスを、書き込むレポートデータのAdobe Analyticsへのポーリング用のプライマリパブリッシャーとして識別する必要があります [SRP](/help/communities/working-with-srp.md).

デフォルトでは、 `AEM Communities Publisher Configuration` OSGi 設定では、自身のパブリッシュインスタンスをプライマリパブリッシャーとして識別します。これにより、パブリッシュファーム内のすべてのパブリッシュインスタンスが自身をプライマリとして識別します。

したがって、選択を解除するには、すべてのセカンダリパブリッシュインスタンスで設定を編集する必要があります **プライマリ発行者** チェックボックスをオンにします。

詳しい手順については、のプライマリパブリッシャーの節を参照してください [Communities のデプロイ](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>複数のパブリッシュインスタンスからのポーリングを防ぐようにプライマリパブリッシャーを設定することが重要です。

### 暗号鍵をレプリケート {#replicate-the-crypto-key}

Adobe Analyticsの資格情報は暗号化されます。 暗号化された分析資格情報のオーサーとパブリッシャー間でのレプリケーションまたは転送を容易にするために、すべてのAEM インスタンスは同じプライマリ暗号化キーを共有する必要があります。

それには、次の手順に従います。 [暗号鍵をレプリケート](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### コミュニティサイトとAnalytics Cloud サービスを公開する {#publish-community-site-and-analytics-cloud-service}

コミュニティサイトに対してAnalytics Cloud サービスを有効にした後、必要に応じて、 [analytics からAEMへの変数のマッピングが調整されていること](#mapped-analytics-to-aem-variables)、次の方法で設定をパブリッシュ環境にレプリケートします。 [コミュニティサイトの（再）公開](/help/communities/sites-console.md#publishing-the-site).

## Analytics からのレポートの取得 {#obtaining-reports-from-analytics}

### レポート管理 {#report-management}

オーサーおよびプライマリパブリッシャー [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`は、Analytics のクエリに使用されます。

オーサー環境では、クエリはリアルタイムレポート用です。

プライマリ・パブリッシャでは、Report Importer の分析データ・インポートに備えて、クエリーを使用して情報を提供します。

クエリ間隔のデフォルトは 10 秒です。

### レポートインポーター {#report-importer}

Analytics が有効なコミュニティサイトを公開すると、プライマリ公開者は [OSGi 設定](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`は、CRXDE で個別に設定されない設定に対してデフォルトのポーリング間隔を設定するように設定できます。

ポーリングインターバルは、データをに取り込んで保存する、Adobe Analyticsへのリクエストの頻度を制御します [SRP](/help/communities/working-with-srp.md).

データが「ビッグデータ」に分類される場合、ポーリングの頻度が増えると、コミュニティサイトに大きな負荷がかかる可能性があります。

デフォルトのポーリング **読み込み間隔** は 12 時間に設定されています。

![report-importer](assets/report-importer.png)

### コンポーネントのレポートのカスタマイズ {#component-report-customization}

現在、追跡する指標をカスタマイズするために、その指標に関するレポートを生成する期間を定義するノードがリポジトリーに作成されています。

現在、このカスタマイズの唯一の例は、フォーラムトピックです。

* プライマリパブリッシャーで、管理者権限でログインします。
* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) に移動します。例： [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* の下 `jcr:content` 言語ルートのノード（例： `/content/sites/engage/en/jcr:content`）、Analytics レポート用に設定されているコンポーネントに移動します。
例えば、**`analytics/reportConfigs/social_forum_components_hbs_topic`** のように指定します。

* 期間が作成されていることに注意してください。

   * `last30Days`
   * `last90Days`
   * `thisYear`

* に注意してください。 `total`ノード。

   * の変更 **`interval`** このプロパティは、レポート インポーターの間隔を上書きします。
   * 値は秒単位で、4 時間（14400 秒）に設定されます。

![component-report](assets/component-report.png)

## Analytics でのユーザーデータの管理 {#manage-user-data-in-analytics}

Adobe Analyticsは、ユーザーデータへのアクセス、ユーザーデータの書き出し、ユーザーデータの削除を可能にする API を提供します。 詳しくは、を参照してください [アクセス要求および削除要求の送信](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=ja).

## リソース {#resources}

* Adobe Experience Cloud: [Analytics ヘルプおよびリファレンス](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [Adobe Analyticsとの統合](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics と外部プロバイダー](/help/sites-administering/external-providers.md)
