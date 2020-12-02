---
title: 統合に関する問題のトラブルシューティング
seo-title: 統合の問題のトラブルシューティング
description: 統合の問題をトラブルシューティングする方法を学びます。
seo-description: 統合の問題をトラブルシューティングする方法を学びます。
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 67%

---


# 統合の問題のトラブルシューティング{#troubleshooting-integration-issues}

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

### JavaScript エラーがないことを確認 {#ensure-there-are-no-javascript-errors}

ブラウザの JavaScript コンソールにエラーが表示されていないか確認してください。未処理のエラーにより、後続のコードが正しく実行されない可能性があります。エラーがある場合は、どのスクリプトがどの領域でエラーの原因となっているのか確認してください。スクリプトへのパスにより、そのスクリプトがどの機能に属しているかがわかる場合があります。

### コンポーネントレベルでのログ  {#logging-on-component-level}

コンポーネントレベルでステートメントを追加すると便利な場合があります。コンポーネントがレンダリングされることで、一時的なマークアップを追加して変数値を表示し、潜在的な問題を特定するのに役立ちます。次に例を示します。

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

ログ記録に関する詳細については、[ログ](/help/sites-deploying/configure-logging.md)ページおよび[監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)ページを参照してください。

## Analytics 統合の問題 {#analytics-integration-issues}

### レポートインポーターが原因で CPU／メモリ使用量が多い {#the-report-importer-causes-high-cpu-memory-usage}

レポートインポーターが原因で CPU／メモリの使用量が多くなる、または `OutOfMemoryError` 例外となる。

#### 解決策 {#solution}

この問題を解決するには、次の方法を試してください。

* 大量の PollingImporter が登録されていないことを確認します（下記の「PollingImporter が原因でシャットダウンに時間がかかる」を参照）。
* `ManagedPollingImporter`OSGi コンソール[で ](/help/sites-deploying/configuring-osgi.md) を設定する CRON 式を使用して、特定の時刻にレポートインポーターを実行します。

AEMでのカスタムデータインポーターサービスの作成について詳しくは、次の記事[https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/jp/experience-manager/using/polling.html)を参照してください。

### PollingImporter が原因でシャットダウンに時間がかかる {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics は継承メカニズムを念頭に置いて設計されています。通常、ページプロパティの「[クラウドサービス](/help/sites-developing/extending-cloud-config.md)」タブ内の Analytics 設定への参照を追加することで、サイトの Analytics を有効にします。ページで別の設定が必要な場合を除き、設定は再度参照する必要はなく、自動的にすべてのサブページに継承されます。サイトへの参照の追加により、複数のノードが自動的に作成されます(AEM 6.3以前の場合は12、AEM 6.4の場合は6)   以降)を`cq;PollConfig`型に変更します。この型は、AnalyticsデータのAEMへのインポートに使用するPollingImportersをインスタンス化します。 そのため、以下のようなことが起こりえます。

* Analytics を参照しているページがたくさんあると、大量の PollingImporter につながります。
* さらに、Analytics 設定への参照とともにページをコピーして貼り付けると、PollingImporters が重複します。

#### 解決策 {#solution-1}

まず、[error.log](/help/sites-deploying/configure-logging.md)を分析すると、アクティブなPollingImportersまたは登録されているPollingImportersの量を知ることができます。 次に例を示します。

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

次に、トップページ（階層の上位）のみに Analytics 設定が参照されていることを確認します。

AEMでのカスタムデータインポーターサービスの作成について詳しくは、次の記事[https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)を参照してください。

## DTM（レガシー）の問題 {#dtm-legacy-issues}

### DTM スクリプトタグがページソースにレンダリングされない {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

設定がページプロパティの[クラウドサービス](/help/sites-developing/extending-cloud-config.md)タブで参照されているにもかかわらず、[DTM](/help/sites-administering/dtm.md) スクリプトタグがページに正しく含まれていない。

#### 解決策 {#solution-2}

この問題を解決するには、次の方法を試してください。

* 暗号化されたプロパティが復号化できることを確認します（暗号化では各 AEM インスタンスで異なる自動生成キーが使用される可能性があることに注意してください）。詳細については、[構成プロパティの暗号化サポート](/help/sites-administering/encryption-support-for-configuration-properties.md)も参照してください。
* `/etc/cloudservices/dynamictagmanagement`にある設定を再公開します
* `/etc/cloudservices`上のACLをチェックします。 ACL は次のようになります。

   * allow; jcr:read; webservice-support-servicelibfinder
   * 許可；jcr:read;みんなrep:glob:&amp;ast;/defaults/&amp;ast;
   * 許可；jcr:read;みんなrep:glob:&amp;ast;/defaults
   * 許可；jcr:read;みんなrep:glob:&amp;ast;/public/&amp;ast;
   * 許可；jcr:read;みんなrep:glob:&amp;ast;/public

ACL 管理の詳細については、[ユーザー管理とセキュリティ](/help/sites-administering/security.md#permissions-in-aem)ページを参照してください。

## Target 統合の問題  {#target-integration-issues}

### カスタムページコンポーネントを使用しているときに Target コンテンツがプレビューモードで表示されない {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

この問題は、カスタムページコンポーネントに Target DTM 統合を処理する正しい JSP またはクライアントライブラリが含まれていないために発生します。

#### 解決策 {#solution-3}

次の解決策を試してください。

* カスタム`headlibs.jsp` （`/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`が含まれる場合）に次の内容が含まれていることを確認します。

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* カスタム`head.html` （任意の`/apps/<CUSTOM-COMPONENTS-PATH>/head.html`の場合） ****&#x200B;が、次の例のように特定の統合ヘッドライブを選択的に&lt;a0/>含めないようにします。

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

この `servicelibs.jsp` によって、必要な分析用 Javascript オブジェクトが追加され、Web サイトに関連付けられているクラウドサービスライブラリが読み込まれます。ターゲットサービスの場合、ライブラリは`/libs/cq/analytics/components/testandtarget/headlibs.jsp`を介して読み込まれます

読み込まれるライブラリのセットは、Target の設定で使用されているターゲットクライアントライブラリのタイプ（`mbox.js` または `at.js`）によって異なります。

`mbox.js` または `at.js` 送信に DTM を使用する場合、コンテンツがレンダリングされる前にライブラリがロードされていることを確認してください。これらのライブラリを非同期的にロードするタグ管理システムを使用すると、ターゲット固有の JavaScript コードの実行に問題が生じる可能性があります。

追加情報については、[ターゲットコンテンツ向けの開発](/help/sites-developing/target.md#understanding-the-target-component)ページを参照してください。

### 「Missing Report Suite ID in AppMeasurement initialization」というエラーがブラウザーコンソールに表示される  {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

この問題は、Adobe AnalyticsがDTMを使用してWebサイトに実装され、カスタムコードを使用している場合に発生する可能性があります。 原因は、`s = new AppMeasurement()`を使用して`s`オブジェクトをインスタンス化することです。

#### 解決策 {#solution-4}

`new AppMeasurement`インスタンス化メソッドの代わりに`s_gi`を使用します。 次に例を示します。

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 正しいオファーではなく、デフォルトのオファーがランダムに表示される  {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

この問題には複数の原因が考えられます。

* サードパーティのTag Management Systemを使用してターゲットのクライアントライブラリ（`mbox.js`または`at.js`）を非同期的に読み込むと、ターゲティングがランダムに中断する場合があります。 ターゲットライブラリはページヘッドに同期的にロードされることになっています。ライブラリが AEM から配信される場合、これは常に当てはまります。

* 2つのターゲットクライアントライブラリ(`at.js`)を同時に読み込む(例えば、DTMを使用するライブラリとAEMのターゲット設定を使用するライブラリ)。 `adobe.target` バージョンが異なる場合、これが原因で `at.js` の定義がクラッシュする可能性があります。

#### 解決策 {#solution-5}

次の解決策を試してください。

* DTM のようなライブラリをロードするカスタムコード（Target ライブラリを順番にロードする）が、[ページヘッド](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages) で同期的に実行されることを確認します。
* サイトがDTMを使用してターゲットライブラリを配信するように設定されている場合は、サイトの[ターゲット設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html)で、**DTM**&#x200B;が配信するClientlibがオンになっていることを確認してください。

### AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}を使用する場合、正しいオファーの代わりにデフォルトのオファーが常に表示されます。

標準の AEM 6.2 および 6.3 は、AT.js バージョン 1.3.0 以降と互換性がありません。AT.jsバージョン1.3.0では、APIのパラメーター検証が導入されているので、`adobe.target.applyOffer()`には、`atjs-itegration.js`コードで提供されていない「mbox」パラメーターが必要です。

#### 解決策 {#solution-6}

この問題を解決するには、`atjs-itegration.js`を編集し、`adobe.target.applyOffer()`のパラメーターオブジェクトに次のように`"mbox": mboxName`フィールドを追加します。

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 目標と設定ページにレポートソースセクションが表示されない {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

この問題は、[A4TAnalytics Cloud構成](/help/sites-administering/target-configuring.md)のプロビジョニングの問題である可能性が高くなります。

#### 解決策 {#solution-7}

AEM に次の確認要求を発行して、Target アカウントに対して A4T が正しく有効になっていることを確認する必要があります。

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

応答に `a4tEnabled:false` という行が含まれている場合、[アドビカスタマーケア](https://helpx.adobe.com/jp/contact.html)に連絡して、アカウントを正しくプロビジョニングするようご依頼ください。

### 参考 Target API {#helpful-target-apis}

Target の問題をトラブルシューティングするときに、以下の 2 つのTarget API が参考になるかもしれません。

* 特定のクライアントコードのTarget エンドポイントを取得する

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* クライアントのプロファイルを取得する

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```

