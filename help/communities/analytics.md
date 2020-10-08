---
title: コミュニティ機能のための Analytics の設定
seo-title: コミュニティ機能のための Analytics の設定
description: Communities のための Analytics の設定
seo-description: Communities のための Analytics の設定
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 46%

---


# コミュニティ機能のための Analytics の設定 {#analytics-configuration-for-communities-features}

## 概要 {#overview}

Adobe Analytics と Adobe Experience Manager（AEM）は、どちらも Adobe Marketing Cloud のソリューションです。

Adobe Analytics を AEM Communities と連携させ、サポートされるコミュニティ機能をメンバーが操作した際にイベントが Adobe Analytics に送信され、レポートが生成されるように設定することができます。

例えば、イネーブルメントコミュニティサイトのメンバーが自分に割り当てられているビデオリソースを再生すると、リソースプレイヤーによって、イベント（ビデオハートビートのデータを含む）が自動的に Analytics に送信されます。コミュニティサイトでは、管理者はビデオの再生に関する様々なレポートを閲覧できます。

さらに、Analytics は以下の処理のために必要です。

* 公開環境で次の操作を行います。

   * Reporting on community [trends](/help/communities/trends.md)
   * サイト訪問者が「最も頻繁に閲覧」、「最もアクティブ」、「最も「いいね！」をクリック」で並べ替えられるようにする
   * UGCリストでの表示数

* 作成者環境で、次の操作を行います。

   * Display of participation data in the [members management console](/help/communities/members.md) (views, posts, follows, likes)
   * Trend summary, video heartbeat and video device for enablement resource [reports](/help/communities/reports.md)

サポートされるコミュニティ機能は以下のとおりです。

* [有効化リソース](/help/communities/resources.md)
* [フォーラム](/help/communities/forum.md)
* [Q&amp;A](/help/communities/working-with-qna.md)
* [ブログ](/help/communities/blog-feature.md)
* [ファイルライブラリ](/help/communities/file-library.md)
* [カレンダー](/help/communities/calendar.md)

ドキュメントのこのセクションでは、Analytics のレポートスイートとコミュニティ機能を接続する方法について説明します。基本的な手順は以下のとおりです。

1. すべての AEM インスタンス上で暗号化や復号化が正しく実行されるよう、[暗号鍵をレプリケート](#replicate-the-crypto-key)する
1. Adobe Analytics の[レポートスイート](#adobe-analytics-report-suite-for-video-reporting)を準備する
1. AEM Analytics [クラウドサービス](#aem-analytics-cloud-service-configuration)と[フレームワーク](#aem-analytics-framework-configuration)を作成する

1. [コミュニティサイトでのAnalytics](#enable-analytics-for-a-community-site) の有効化
1. Analytics と AEM 変数との間のマッピングを&#x200B;[**検証**](#verify-analytics-to-aem-variable-mapping)&#x200B;する
1. Identify [primary publisher](#primary-publisher)
1. [コミュニティサイトの公開](#publish-community-site-and-analytics-cloud-service)
1. Configure [import of report data](#obtaining-reports-from-analytics) from Adobe Analytics to the community site

## 前提条件 {#prerequisites}

Analytics をコミュニティ機能と連携するよう設定するには、アカウント担当者と協力して Adobe Analytics アカウントと[レポートスイート](#adobe-analytics-report-suite-for-video-reporting)をセットアップする必要があります。設定が完了したら、次の情報を使用できます。

* **会社名**

   Adobe Analyticsアカウントに関連付けられている会社です。

* **User Name**

   Analyticsアカウントを管理する権限を持つユーザーのログインユーザー名（Webサービスアクセス権限を含む必要があります）。

* **パスワード**

   認証済みユーザーのログインパスワード。

* **Analyticsデータセンター**

   アカウントのAnalyticsデータセンターのURL。

* **レポートスイート**

   使用する Analytics レポートスイートの名前。

## Adobe Analytics Report Suite for Video Reporting {#adobe-analytics-report-suite-for-video-reporting}

Using the Adobe Marketing Cloud&#39;s [Report Suite Manager](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html), Analytics report suites can be configured so that a community site may be enabled to provide reports for Communities features.

By signing in to [Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) with [Company Name and User name](/help/communities/analytics.md#prerequisites), it is possible to configure a new or existing report suite to have:

* [11コンバージョン変数](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVar)

   * **`evar1`** 有効 **`evar11`** にする

   * 既存のeVarを再利用（名前変更）したり、Communitiesの機能で使用する新しいeVarを作成したりできます。

* [7 個の成功イベント](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html)（event）

   * **`event1`** 有効 **`event7`** にする

   * type **`Counter`**

      * **string not required****`Counter (no subrelations)`**
   * 既存のイベントを再利用（名前変更）したり、Communities機能で使用する新しいユーザーを作成できます。


* [ビデオ管理](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * ビデオレポートコンソール

      * Enable（有効） `Video Core`
      * 「保存」を選択します
   * ビデオコア測定コンソール

      *  `Use Solution Variables`
      * 「保存」を選択します


**新しいレポートスイート**&#x200B;を使用する場合、新しいレポートスイートには、4 個の evar と 6 個の event 変数しかないことに注意してください。コミュニティサイトでは 11 個の ever と 7 個の event 変数が必要です。

**既存のレポートスイート**&#x200B;を使用する場合は、コミュニティサイト用の Analytics フレームワークをアクティベートする前に、[変数マッピングを変更](#modifying-analytics-variable-mapping)する必要があります。Communities専用の変数に関する懸念は、アカウント担当者にお問い合わせください。

>[!CAUTION]
>
>**以下の範囲内の変数を使用している既存のレポートスイートを使用する場合は、**
>
>* **`evar1`** から **`evar11`** まで
   >
   >
* **`event1`** から **`event7`** まで
>
>
**次に、コミュニティサイトが公開される前に** 、Analyticsがコミュニティサイトに対して有効にされたときにAnalytics変数に自動的にマッピングされたAEM変数を移動して、既存のマッピングを復元することが重要です。
>
>To restore the pre-existing mapping and move AEM variables to other Analytics variables, see the section on [Modifying Analytics Variable Mapping](#modifying-analytics-variable-mapping).
>
>この作業をしておかないと、修復不可能なデータ損傷が発生することがあります。

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Video Heartbeat Analyticsのライセンスを受けると、が割り当てら `Marketing Cloud Org Id` れます。

To enable Video Heartbeat reporting after [configuring the Analytics report suite for video reporting](#adobe-analytics-report-suite-for-video-reporting):

* [Analyticsクラウドサービスの作成](#aem-analytics-cloud-service-configuration)
* Enable [Analytics for a community site](#enable-analytics-for-a-community-site)
* をコミュニティサイト `Marketing Cloud Org Id` に関連付ける

The `Marketing Cloud Org Id` may be entered at the time of [community site creation](/help/communities/sites-console.md#enablement) or later by [modifying](/help/communities/sites-console.md#modifying-site-properties) the community site properties. [](#aem-analytics-cloud-service-configuration)

![marketing-org-id](assets/marketing-org-id.png)

ビデオハートビート分析が有効な場合、ビデオプレーヤーのJavaScript(JS)コードは、ビデオハートビートライブラリコード（同じJS）をインスタンス化します。このコードは、10秒ごと（設定不可）にビデオステータス更新を送信するロジックを処理します。

有効にしない場合、Video Heartbeat コードはインスタンス化されず、ビデオの再生状況と再開位置の追跡のみが報告のために SRP に維持されます。

## AEM Analytics クラウドサービス設定 {#aem-analytics-cloud-service-configuration}

作成者インスタンスの標準UIを使用して、Adobe AnalyticsをAEMコミュニティサイトと統合する、新しいAnalytics統合を作成するには：

* From global navigation: **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**
* Scroll-down to **[!UICONTROL Adobe Analytics]**
* Select **[!UICONTROL Configure Now]** or **[!UICONTROL Show Configurations]**

![cloud-config](assets/cloud-config1.png)

### 設定を作成ダイアログ {#create-configuration-dialog}

* Select `[+]` icon next to **[!UICONTROL Available Configurations]** to create a new configuration

設定を作成ダイアログでは、設定を識別するための値を入力します。

![create-cloud-config](assets/cloud-config2.png)

* **タイトル**

   （必須）設定の表示タイトル。
For example, enter *Enablement Community Analytics*

* **名前**

   （オプション）指定しなかった場合、名前はデフォルトでタイトルから派生した有効なノード名になります。
例えば、「communities」と入力します。**

* **テンプレート**

    `Adobe Analytics Configuration`

* 「**作成**」を選択します。

   * 設定ページを起動し、 `Analytics Settings` ダイアログを開く

### Analytics 設定ダイアログ {#analytics-settings-dialog}

新しい Analytics 設定を初めて作成したときには、その設定と、Analytics 設定を入力するための新しいダイアログが表示されます。This dialog requires the [prerequisite account information](#prerequisites) obtained from the account representative.

![analytics-settings](assets/analytics-settings.png)

* **会社**

   Adobe Analyticsアカウントに関連付けられている会社です。

* **ユーザー名**

   Analyticsアカウントの管理を承認されたユーザーのログインユーザー名。

* **パスワード**

   認証済みユーザーのログインパスワード。

* **データセンター**

   レポートスイートをホストするAnalyticsデータセンターを選択します。

* **ページに追跡タグを追加しない**

   デフォルトのまま（選択解除）

* **AppMeasurement を使用**

   デフォルトのまま（選択解除）

* **ページインプレッション数を夜間に読み込まない (作成者)**

   デフォルトのまま（選択解除）

* **ページインプレッション数を夜間に読み込まない (発行)**

   デフォルトのまま（選択解除）

設定を保存するには：

* Select **Connect to Analytics**

   * 成功しなかった場合、

      * 入力内容の先頭にスペースがないことを確認します。
      * 別のデータセンターを試してみてください。
      * アカウント担当者にお問い合わせください。

* 「**OK**」を選択します。

   ![analytics-enablement-settings](assets/analytics-settings1.png)

### フレームワークの作成 {#create-framework}

Adobe Analytics への基本的な接続を正しく設定したら、コミュニティサイトのフレームワークを作成または編集する必要があります。フレームワークの目的は、Communities機能(AEM)変数をAnalytics（レポートスイート）変数にマッピングすることです。

* Select `[+]` icon next to **[!UICONTROL Available Frameworks]** to create a new framework

   ![analytics-framework](assets/analytics-framework.png)

* **タイトル**

   (Required) A display title for the framework
For example, enter *Enablement Community Framework*.

* **名前**

   （オプション）指定しなかった場合、名前はデフォルトでタイトルから派生した有効なノード名になります。
For example, enter *communities*.

* *テンプレート*

    `Adobe Analytics Framework`.

* 「**作成**」を選択します。

Analytics フレームワークを作成すると、フレームワークを設定するための画面が開きます。

## AEM Analytics フレームワーク設定 {#aem-analytics-framework-configuration}

フレームワークの目的は、AEM変数をAnalytics変数(eVarおよびイベント)にマッピングすることです。 The Analytics variables available for mapping are [defined in the report suite](#adobe-analytics-report-suite-for-video-reporting).

![analytics-enablement-framework](assets/analytics-framework1.png)

### レポートスイートの選択 {#select-report-suite}

ビデオレポート用にセットアップされているレポートスイートを選択します。

If a report suite has not yet been created or not properly set up, see the previous section:
[Adobe Analytics Report Suite for Video Reporting](#adobe-analytics-report-suite-for-video-reporting)

サイドキックは必要ないので、レポートスイート設定にアクセスするときの邪魔にならないよう最小化しておくことができます。

#### 「項目を追加」選択前および選択後のレポートスイートダイアログ {#report-suites-dialog-before-and-after-selecting-add-item}

![レポートスイート](assets/report-suite.png)

1. [ **追加Item +**]を選択します。

   2つのドロップダウンボックスが表示されます。

1. 選択肢 `Report suite.`

   会社アカウントに関連付けられたレポートスイートを選択できます。

1. 開いたダイアログで **「はい** 」を選択します。

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. を選択し `Run Mode`ます。

1. 「**発行**」を選択します。

![analytics-framework2](assets/analytics-framework2.png)

これで Analytic クラウドサービスとフレームワークの準備が完了しました。マッピングは、このAnalyticsサービスを有効にしてコミュニティサイトを作成すると定義されます。

## コミュニティサイトに対する Analytics の有効化 {#enable-analytics-for-a-community-site}

### 新しいコミュニティサイトに対する有効化 {#enable-for-new-community-site}

[新しいコミュニティサイトの作成](/help/communities/sites-console.md)中に Analytics クラウドサービスを追加するには：

* 手順3の「 [解析」タブで、次の操作を行います](/help/communities/sites-console.md#analytics)。
   * 「Analyticsを **有効にする** 」チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* Analytics フレームワーク設定に戻り、変数マッピングを調整します（オプション）。

### 既存のコミュニティサイトに対する有効化 {#enable-for-existing-community-site}

Analytics クラウドサービスを[既存のコミュニティサイト](/help/communities/sites-console.md#modifying-site-properties)に追加するには：

* Navigate to the **Communities > Sites** console.
* コミュニティサイトの[サイトの編集]アイコンを選択します。
* 設定を選択します。
* 「解析」セクションで、次の操作を行います。
   * 「Analyticsを **有効にする** 」チェックボックスをオンにします。
   * ドロップダウンボックスからフレームワークを選択します。

* Analytics フレームワーク設定に戻り、変数マッピングを調整します（オプション）。

### カスタマイズされたサイトに対する有効化 {#enable-for-customized-sites}

コミュニティサイトで Analytics の追跡とインポートが正常に機能するようにするには、`scf-js-site-title` クラスと href 属性のページ要素が存在する必要があります。Only one such element should exist on the page, such as it does in an unmodified `sitepage.hbs` script for a community site. The value of `siteUrl` is extracted and sent to Adobe Analytics as the *site path*.

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

For a **customized community site** that overlays the `sitepage.hbs` script, ensure the element is present. The `siteUrl` variable will be set when rendered on the server before serving to the client.

Communities コンポーネントが含まれているが[サイト作成ウィザード](/help/communities/sites-console.md)で作成されていない&#x200B;**一般的な AEM サイト**&#x200B;の場合は、要素を追加する必要があります。hrefの値は、サイトへのパスである必要があります。 For example, if the site path is `/content/my/company/en`, then use:

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

The author environment&#39;s [OSGi configuration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, provides a listing of the components that have been instrumented for Analytics. 変数の自動マッピングは、リストに表示されているコンポーネントによって決まります。

Analytics 用の新しいカスタムコンポーネントを作成した場合は、この設定済みコンポーネントのリストに追加する必要があります。

### コンポーネントの設定 {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>ジャーナルコンポーネントは、ブログ機能の実装に使用されます。

### Analytics と AEM 変数とのマッピング {#mapped-analytics-to-aem-variables}

Analyticsを有効にしてコミュニティサイトを保存し、クラウド設定フレームワークを選択すると、AEM変数は、evar1とイベント1で始まり、それぞれ1ずつ増分されるAnalytics eVarとイベントに自動的にマッピングされます。

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
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate（投稿）</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(E)</em></td>
   <td><em>（f）</em></td>
   <td><em>（g）</em></td>
   <td><em>（h）</em></td>
   <td><em>(i)</em></td>
   <td><em>（j）</em></td>
  </tr>
 </tbody>
</table>

**eVar の値の例：**

* *[MIME type](https://www.iana.org/assignments/media-types)*:video/mp4
* *[コミュニティサイトのタイトル](/help/communities/sites-console.md#step13asitetemplate)*:Geometrixxコミュニティ
* *[コミュニティ関数名](/help/communities/functions.md)*:フォーラム
* *[コミュニティグループ名](/help/communities/creating-groups.md#creating-a-new-group)*:ハイキング
* *コミュニティグループコンテンツへのパス*: `/content/sites/<site name>/en/groups/hiking`
* *[UGCコンポーネントresourceType](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *UGCコンポーネントタイトル*:トピックのハイク
* *login (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *UGCへのSRPパス*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
または 
*次に従うコンポーネントのパス*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *コミュニティサイトコンテンツへのパス*: `/content/sites/<site name>/en`

### Analytics 変数のマッピングの変更 {#modifying-analytics-variable-mapping}

Analytics eVarとAEM変数のマッピングは、コミュニティサイトでAnalyticsを有効にした後、フレームワーク設定から確認できます。

Analytics を有効にした後、コミュニティサイトを公開する前に、フレームワーク内で必要な Analytics の evar または event を左のレールからマッピングテーブルの適切な行にドラッグ＆ドロップすることで、マッピングを変更できます。

マッピングの重複を避けるために、置き換えられた Analytics の evar または event は列から削除するようにしてください（削除するには、カーソルを合わせたときに Analytics 変数要素の右に表示される「X」を選択します）。

CommunitiesのeVarおよびイベントがレポートスイートに以前存在したマッピングを上書きする場合、データの損失を防ぐために、Communities機能のAEM変数を他のAnalytics eVarまたはイベントに割り当て、元のマッピングを復元します。

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
   >
* **`event1`** から **`event7`** まで
>
>
**次に、コミュニティサイトが公開される前に** 、既存のマッピングを復元し、自動的にマップされたCommunities AEM変数（コミュニティサイトでAnalyticsが有効な場合）を、他のAnalytics変数に移動することが重要です。 この再マッピングは、すべてのCommunitiesコンポーネントで一貫している必要があります。
>
>この作業をしておかないと、修復不可能なデータ損傷が発生することがあります。

### プライマリパブリッシャー {#primary-publisher}

選択したデプロイメントが[パブリッシュファーム](/help/communities/topologies.md#tarmk-publish-farm)の場合は、レポートデータのポーリングをおこなう Adobe Analytics が [SRP](/help/communities/working-with-srp.md) に書き込めるよう、1 つの AEM パブリッシュインスタンスをプライマリパブリッシャーに指定する必要があります。

By default, the `AEM Communities Publisher Configuration` OSGi configuration identifies its publish instance as the primary publisher, such that all publish instances in a publish farm would self-identify as the primary.

Therefore, it is necessary to edit the configuration on all secondary publish instances to deselect the **Primary Publisher** check box.

For specific instructions, see the primary publisher section of [Deploying Communities](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>複数の発行インスタンスからのポーリングを防ぐようにプライマリ発行者を設定することが重要です。

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

Adobe Analytics の資格情報は暗号化されます。作成者と発行者間で暗号化された解析資格情報のレプリケーションまたは送信を容易にするには、すべてのAEMインスタンスで同じプライマリ暗号化キーを共有する必要があります。

To do so, follow the instructions at [Replicate the Crypto Key](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### コミュニティサイトと Analytics クラウドサービスの公開 {#publish-community-site-and-analytics-cloud-service}

Analytics クラウドサービスをコミュニティサイトに対して有効にし、また必要に応じて [Analytics 変数と AEM 変数とのマッピングを調整](#mapped-analytics-to-aem-variables)したら、[コミュニティサイトの（再）公開](/help/communities/sites-console.md#publishing-the-site)をおこない、設定をパブリッシュ環境にレプリケートする必要があります。

## Analytics からのレポートの取得 {#obtaining-reports-from-analytics}

### レポート管理 {#report-management}

作成者およびプライマリパブリッシャーの [OSGi設定](/help/sites-deploying/configuring-osgi.md)( `AEM Communities Analytics Report Management`OSGi設定)は、Analyticsのクエリに使用されます。

オーサー環境では、リアルタイムレポートを入手するにはクエリを使用します。

プライマリパブリッシャーでは、レポートインポーターの分析データ読み込みに備えた情報提供のためにクエリを使用します。

クエリの間隔は、デフォルトで 10 秒間です。

### レポートインポーター {#report-importer}

Once an Analytics enabled community site has been published, the primary publisher&#39;s [OSGi configuration](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, may be configured to set the default polling interval for those configurations which are not individually configured in CRXDE.

The polling interval controls the frequency of requests to Adobe Analytics for data to be pulled and saved into [SRP](/help/communities/working-with-srp.md).

データが「ビッグデータ」に類するものである場合は、ポーリングの頻度を上げるとコミュニティサイトに大きな負荷がかかる場合があります。

デフォルトのポーリングの&#x200B;**読み込みインターバル**&#x200B;は、12 時間に設定されています。

![report-importer](assets/report-importer.png)

### コンポーネントレポートのカスタマイズ {#component-report-customization}

現在、追跡する指標をカスタマイズするには、リポジトリ内にノードを作成し、その指標に関するレポートを生成する期間を定義します。

現在、このカスタマイズの例を確認できるのはフォーラムトピックのみです。

* プライマリパブリッシャーで、管理者権限でサインインします。
* Navigate to [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). For example, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* 言語ルートのjcr:contentノードの下(例えば、Analyticsレポート用に設定されたコンポーネントに `/content/sites/engage/en/jcr:content),`移動します)。
例：**`analytics/reportConfigs/social_forum_components_hbs_topic`**

* 作成された期間に注意してください。

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Notice the `total`node.

   * この **`interval`** プロパティを変更すると、レポートインポーターの間隔が上書きされます。
   * 値は秒単位で、4時間（14400秒）に設定します。

![component-report](assets/component-report.png)

## Analytics でのユーザーデータの管理 {#manage-user-data-in-analytics}

Adobe Analytics は、ユーザーデータのアクセス、書き出し、削除をおこなう API を提供しています。詳しくは、[アクセス要求および削除要求の送信](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)を参照してください。

## リソース {#resources}

* Adobe Experience Cloud: [Analytics Help and Reference](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integrating with Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics with External Providers](/help/sites-administering/external-providers.md)
