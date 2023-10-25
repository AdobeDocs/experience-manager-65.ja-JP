---
title: 統合に関する問題のトラブルシューティング
seo-title: Troubleshooting Integration Issues
description: Adobe Experience Managerとの統合時の問題のトラブルシューティング方法について説明します。
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 45%

---

# 統合に関する問題のトラブルシューティング{#troubleshooting-integration-issues}

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

### JavaScript エラーがないことを確認します。 {#ensure-there-are-no-javascript-errors}

ブラウザーの JavaScript コンソールにエラーが表示されるかどうかを確認します。 未処理のエラーにより、後続のコードが正しく実行されない可能性があります。 エラーが発生した場合は、エラーの原因となっているスクリプトと対象領域を確認します。 スクリプトのパスによって、スクリプトが属する機能が示される場合があります。

### コンポーネントレベルでのログ {#logging-on-component-level}

場合によっては、コンポーネントレベルで文を追加すると便利です。 コンポーネントがレンダリングされるので、一時的なマークアップを追加して、潜在的な問題を特定するのに役立つ変数値を表示できます。 次に例を示します。

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

ログについて詳しくは、[ログ](/help/sites-deploying/configure-logging.md)ページと[監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)ページを参照してください。

## Analytics 統合に関する問題 {#analytics-integration-issues}

### レポートインポーターが原因で CPU/メモリ使用量が高くなる {#the-report-importer-causes-high-cpu-memory-usage}

レポートインポーターが原因で CPU／メモリの使用量が多くなる、または `OutOfMemoryError` 例外となる。

#### 解決策 {#solution}

この問題を修正するには、次の操作を試してください。

* 大量の PollingImporters が登録されていないことを確認します（以下の「PollingImporter によるシャットダウンに時間がかかる」の節を参照）。
* `ManagedPollingImporter`OSGi コンソール[で ](/help/sites-deploying/configuring-osgi.md) を設定する CRON 式を使用して、特定の時刻にレポートインポーターを実行します。

AEM でカスタムデータインポーターサービスを作成について詳しくは、以下の記事を参照してください。[https://helpx.adobe.com/jp/experience-manager/using/polling.html](https://helpx.adobe.com/jp/experience-manager/using/polling.html)

### PollingImporter が原因で、シャットダウンに時間がかかります {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics は、継承メカニズムを考慮して設計されています。 通常、ページプロパティ内の Analytics 設定への参照を追加することで、サイトの Analytics を有効にします [Cloud Service](/help/sites-developing/extending-cloud-config.md) タブをクリックします。 その後、ページで異なる設定が必要な場合を除き、設定はすべてのサブページに自動的に継承され、再度参照する必要はありません。 サイトへの参照を追加すると、タイプ `cq;PollConfig` の複数のノード（AEM 6.3 以前の場合は 12、AEM 6.4 以降の場合は 6）も自動的に作成されます。これは、Analytics データを AEM にインポートするために使用される PollingImporters をインスタンス化します。これにより、以下を実現できます。

* Analytics を参照するページが多数ある場合、大量の PollingImporters が発生します。
* また、Analytics 設定を参照してページをコピー&amp;ペーストすると、PollingImporters が重複しています。

#### 解決策 {#solution-1}

まず、[error.log](/help/sites-deploying/configure-logging.md) を分析することで、アクティブまたは登録済みの PollingImporters の量について、何らかのインサイトを得られることがあります。次に例を示します。

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

次に、上位のページ（階層の上位）に参照されている Analytics 設定のみがあることを確認します。

AEM でのカスタムデータインポーターサービスの作成について詳しくは、以下の記事を参照してください。[https://helpx.adobe.com/jp/experience-manager/using/polling.html](https://helpx.adobe.com/jp/experience-manager/using/polling.html)

## DTM（レガシー）の問題 {#dtm-legacy-issues}

### DTM スクリプトタグがページのソースでレンダリングされない {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

The [DTM](/help/sites-administering/dtm.md) ページプロパティで設定が参照されているにもかかわらず、スクリプトタグがページに適切に含まれていない [Cloud Service](/help/sites-developing/extending-cloud-config.md) タブをクリックします。

#### 解決策 {#solution-2}

この問題を修正するには、次の操作を試してみてください。

* 暗号化されたプロパティが復号化できることを確認します ( 暗号化ではAEMインスタンスごとに異なる自動生成キーを使用する場合があることに注意してください )。 詳しくは、 [設定プロパティの暗号化のサポート](/help/sites-administering/encryption-support-for-configuration-properties.md).
* `/etc/cloudservices/dynamictagmanagement` で検索された設定の再公開
* `/etc/cloudservices` 上の ACL をチェックします。ACL は次のようにする必要があります。

   * allow;jcr:read; webservice-support-servicelibfinder
   * allow; jcr:read; everyone; rep:glob:&amp;ast;/defaults/&amp;ast;
   * allow; jcr:read; everyone; rep:glob:&amp;ast;/defaults
   * allow; jcr:read; everyone; rep:glob:&amp;ast;/public/&amp;ast;
   * allow; jcr:read; everyone; rep:glob:&amp;ast;/public

ACL 管理の詳細については、 [ユーザー管理とセキュリティ](/help/sites-administering/security.md#permissions-in-aem) ページに貼り付けます。

## Target の統合に関する問題 {#target-integration-issues}

### カスタムページコンポーネントを使用している場合に、プレビューモードでターゲットコンテンツが表示されない {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

この問題は、カスタムページコンポーネントに Target DTM 統合を処理する正しい JSP またはクライアントライブラリが含まれていないために発生します。

#### 解決策 {#solution-3}

次のソリューションを試すことができます。

* カスタム `headlibs.jsp`（もしあれば `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`）に次が含まれていることを確認します。

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 以下の例のように、カスタム `head.html`（もしあれば `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`）に特定の統合 headlib が選択的に含まれて&#x200B;**いない**&#x200B;ことを確認します。

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

この `servicelibs.jsp` によって、必要な分析用 Javascript オブジェクトが追加され、Web サイトに関連付けられているクラウドサービスライブラリが読み込まれます。Target サービスでは、ライブラリは `/libs/cq/analytics/components/testandtarget/headlibs.jsp` で読み込まれます。

読み込まれるライブラリのセットは、Target の設定で使用されているターゲットクライアントライブラリのタイプ（`mbox.js` または `at.js`）によって異なります。

`mbox.js` または `at.js` 送信に DTM を使用する場合、コンテンツがレンダリングされる前にライブラリがロードされていることを確認してください。これらのライブラリを非同期で読み込むTag Management Systems を使用すると、Target 固有の JavaScript コードを実行する際に問題が発生する可能性があります。

詳しくは、 [ターゲットコンテンツ用の開発](/help/sites-developing/target.md#understanding-the-target-component) ページに貼り付けます。

### ブラウザーのコンソールに、「AppMeasurementの初期化でレポートスイート ID が見つかりません」というエラーが表示されます。 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

この問題は、Adobe Analytics が DTM を使用して web サイトに実装され、カスタムコードを使用している場合に発生することがあります。原因は、`s = new AppMeasurement()` を使用して `s` オブジェクトをインスタンス化しているためです。

#### 解決策 {#solution-4}

インスタンス化メソッドに `new AppMeasurement` ではなく `s_gi` を使用します。次に例を示します。

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### デフォルトのオファーは、正しいオファーの代わりにランダムに表示されます {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

この問題には、次の複数の原因が考えられます。

* Target クライアントライブラリ（`mbox.js` または `at.js`）をサードパーティのタグ管理システムを使用して非同期にロードすると、ターゲティングがランダムに解除される可能性があります。Target ライブラリは、ページの先頭で同期的に読み込まれるはずです。 ライブラリがAEMから配信される場合、これは常に当てはまります。

* 2 つの Target クライアントライブラリ（`at.js`）を同時にロード（例えば、1 つは DTM を使用し、もう 1 つは AEM のTarget の設定を使用）。`adobe.target` バージョンが異なる場合、これが原因で `at.js` の定義がクラッシュする可能性があります。

#### 解決策 {#solution-5}

次のソリューションを試すことができます。

* DTM に似たライブラリを読み込むカスタマーコード（これらのライブラリを順に読み込む）が、 [ページヘッド](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* サイトが DTM を使用して Target ライブラリを配信するように設定されている場合は、サイトの [Target の設定](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/package-manager.html)で「**DTM によって提供される Clientlib**」オプションがオンになっていることを確認します。

### AT.js 1.3 以降を使用する場合、デフォルトのオファーは、正しいオファーではなく常に表示されます {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

標準のAEM 6.2 および 6.3 は、AT.js バージョン 1.3.0 以降と互換性がありません。 API のパラメータ検証が導入された AT.js バージョン 1.3.0 では、`adobe.target.applyOffer()` が要求する「mbox」パラメーターが `atjs-itegration.js` コードで提供されません。

#### 解決策 {#solution-6}

この問題を解決するには、次のように `atjs-itegration.js` を編集して `adobe.target.applyOffer()` のパラメーターオブジェクトに `"mbox": mboxName` フィールドを追加します。

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

この問題は [A4T Analytics クラウド設定](/help/sites-administering/target-configuring.md)のプロビジョニングの問題であると思われます。

#### 解決策 {#solution-7}

AEMに次の検証リクエストを発行して、A4T が Target アカウントに対して正しく有効になっていることを確認する必要があります。

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

### 役立つ Target API {#helpful-target-apis}

以下に、Target の問題のトラブルシューティングに役立つ Target API を 2 つ示します。

* 特定のクライアントコードの Target エンドポイントを取得します

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* クライアントのプロファイルの取得

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
