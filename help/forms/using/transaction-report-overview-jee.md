---
title: JEE における AEM Forms のトランザクションレポートの概要
description: 送信されたフォーム、レンダリングされたフォーム、別の形式に変換されたフォームの合計数を保持します
feature: Transaction Reports
exl-id: 77e95631-6b0d-406e-a1b8-78f8d9cceb63
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: ht
source-wordcount: '529'
ht-degree: 100%

---

# JEE 上の AEM Forms のトランザクションレポートの有効化と表示 {#transaction-reports-overview}

<!--Transaction reports in AEM Forms on JEE let you keep a count of all transactions taken place on your AEM Forms deployment. The objective is to provide information about product usage and helps business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of a document
* Rendition of a document
* Conversion of a document from one file format to another 

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis-jee.md). Transaction log helps you to gain information about the number of documents submitted, rendered, and converted.-->

## トランザクションレポートを有効にする {#enable-transaction-reporting}

デフォルトでは、トランザクションの記録は無効になっています。トランザクションレポートを有効にするには、次の手順を実行します。

1. JEE における AEM Forms で `/adminui`（例：`http://10.14.18.10:8080/adminui`）に移動します。
1. **管理者**&#x200B;としてログインします。
1. **設定**／**コアシステム設定**／**設定**&#x200B;に移動します。
1. 「**トランザクションレポートを有効にする**」チェックボックスをクリックし、設定を&#x200B;**保存**&#x200B;します。

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. サーバーを再起動します。
1. サーバー上での変更の他に、クライアント側でも、プロジェクトの `adobe-livecycle-client.jar` ファイルを更新する必要があります（同じファイルを使用する場合）。

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## トランザクションレポートを表示する {#view-transaction-report}

トランザクションレポートを有効にすると、[ダッシュボードを使用したトランザクションレポート](#transaction-report-dashboard)と[ログファイルを使用した詳細なトランザクションレポート](#transaction-report-logfile)から、トランザクション数に関する情報にアクセスできるようになります。この両方について以下で説明します。

### ダッシュボードを使用したトランザクションレポート {#transaction-report-dashboard}

ダッシュボードを使用したトランザクションレポートでは、トランザクションタイプごとにトランザクションの合計数が表示されます。例えば、画像に示すように、レンダリングされたフォーム、変換されたフォームおよび送信されたフォームの合計数に関する情報が得られます。トランザクションレポートを取得するには：

1. JEE における AEM Forms で `/adminui`（例：`http://10.13.15.08:8080/adminui`）に移動します。
1. **管理者**&#x200B;としてログインします。
1. ヘルスモニターをクリックします。
1. 「**トランザクションレポート**」タブに移動し、「**トランザクションの合計数を計算**」をクリックします。これで、送信された PDF フォーム、レンダリングされた PDF フォーム、変換された PDF フォームの数が円グラフで表されていることがわかります。

![sample-transaction-report-jee](assets/transaction-piechart.png)


### ログファイルを使用したトランザクションレポート {#transaction-report-logfile}

ログファイルを使用したトランザクションレポートには、各トランザクションに関する詳細な情報が表示されます。トランザクションログにアクセスするには、サーバー起動を基準とした相対コンテキストパスに従います。トランザクションは、デフォルトでは別個のログファイル `transaction_log.log` に取得されます。**ファイルパス** は、サーバー起動コンテキストを基準とした相対パスです。各種サーバーのデフォルトパスを以下に示します。

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

サンプルトランザクションレコードの例：
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### トランザクションレコード {#transaction-record-structure-jee}

トランザクションログ構造では、サービス、操作、トランザクションタイプなどの様々なパラメーターを使用して、各トランザクションの記録方法を定義します。それぞれの詳細について、以下で説明します。トランザクションレポートの構造は次のとおりです。

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **service**：サービスの名前。
* **operation**：操作名。
* **internalService**：内部呼び出しがある場合は呼び出し先の名前。それ以外の場合はサービス名と同じ。
* **internalOperation**：内部呼び出しがある場合は呼び出し先の名前。それ以外の場合は操作名と同じ。
* **transactionOperationType**：トランザクションのタイプ（送信、レンダリング、変換）。
* **transactionCount**：トランザクションの合計数。
* **elapsedTime**：呼び出しの開始から応答の受信までの時間。
* **transactionDate**：サービスがいつ呼び出されたかを示すタイムスタンプ。

**サンプルトランザクションログ**:

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## トランザクションの記録頻度 {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

トランザクションの記録頻度は、正常に送信、レンダリング、変換されたフォームごとに、サーバー上の更新操作によって決まります。

* **ダッシュボード** では、トランザクション数は定期的に更新されます。デフォルトは 1 分に設定されています。頻度を更新するには、`"com.adobe.idp.dsc.transaction.recordFrequency"` でシステムプロパティを設定します。例えば、JBoss® における JEE 向け AEM Forms では、`JAVA_OPTS` に `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` を追加して、更新頻度を 5 分に設定します。

* **トランザクションログ**&#x200B;では、フォームを正常に送信、レンダリング、または変換すると、各トランザクションの更新が即時に行われます。

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## 関連記事 {#related-articles}

* [JEE における AEM Forms の課金対象 API のリスト](../../forms/using/transaction-reports-billable-apis-jee.md)
* [JEE における AEM Forms のカスタムコンポーネント API のトランザクションの記録](/help/forms/using/record-transaction-custom-component-jee.md)
