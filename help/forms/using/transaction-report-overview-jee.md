---
title: JEE 上のAEM Formsのトランザクションレポートの概要
description: 送信されたフォーム、レンダリングされたドキュメント、ある形式から別の形式へ変換されたドキュメントなど、すべてのフォームの数を保持する
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# JEE 上のAEM Formsのトランザクションレポートの有効化と表示 {#transaction-reports-overview}

<!--Transaction reports in AEM Forms on JEE let you keep a count of all transactions taken place on your AEM Forms deployment. The objective is to provide information about product usage and helps business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of a document
* Rendition of a document
* Conversion of a document from one file format to another 

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis-jee.md). Transaction log helps you to gain information about the number of documents submitted, rendered, and converted.-->

## トランザクションレポートを有効にする {#enable-transaction-reporting}

デフォルトでは、トランザクションの記録は無効になっています。 トランザクション・レポートを有効にするには、次の手順に従います。

1. 次に移動： `/adminui` JEE 上のAEM Formsで、例えば `http://10.14.18.10:8080/adminui`.
1. 次としてログイン： **管理者**.
1. に移動します。 **設定** > **コアシステム設定** > **設定**.
1. チェックボックスをクリックして **トランザクションレポートを有効にする** および **保存** 設定を指定します。

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. サーバーを再起動します。
1. サーバー上の変更に加え、クライアント側では、 `adobe-livecycle-client.jar` ファイルをプロジェクト内で使用する場合は、ファイルを参照してください。

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## トランザクションレポートの表示 {#view-transaction-report}

トランザクションレポートを有効にすると、トランザクション数に関する情報には、 [ダッシュボードを使用したトランザクションレポート](#transaction-report-dashboard) そして詳細な [ログ・ファイルを使用したトランザクション・レポート](#transaction-report-logfile). 両方について以下に説明します。

### ダッシュボードを使用したトランザクションレポート {#transaction-report-dashboard}

ダッシュボードを使用したトランザクションレポートには、トランザクションの各タイプのトランザクションの合計数が表示されます。 例えば、画像で示すように、レンダリング、変換、送信されたフォームの合計数に関する情報を取得します。 取引レポートを取得する手順は、次のとおりです。

1. 次に移動： `/adminui` JEE 上のAEM Formsで、次の例を参照してください。 `http://10.13.15.08:8080/adminui`.
1. 次としてログイン： **管理者**.
1. [ ヘルスモニタ ] をクリックします。
1. に移動します。 **トランザクションレポーター** タブ、クリック **トランザクションの合計を計算**&#x200B;を見ると、円グラフが送信済み、レンダリング済みまたは変換済みのPDF formsの数を表していることがわかります。

![sample-transaction-report-jee](assets/transaction-piechart.png)


### ログファイルを使用したトランザクションレポート {#transaction-report-logfile}

ログ・ファイルを介したトランザクション・レポートには、各トランザクションに関する詳細情報が表示されます。 トランザクションログにアクセスするには、サーバーの起動に関連するコンテキストパスに従います。 トランザクションは、別のログファイルにキャプチャされます `transaction_log.log` デフォルトでは。 The **ファイルパス** は、サーバーの開始コンテキストに対する相対パスです。 異なるサーバーのデフォルトのパスは次のとおりです。

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

サンプルのトランザクションレコードの例：
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service=‘GeneratePDFService’, operation=‘HtmlFileToPDF’, internalService=‘GeneratePDFService’, internalOperation=‘HtmlFileToPDF’, transactionOperationType=‘CONVERT’, transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### トランザクションレコード {#transaction-record-structure-jee}

トランザクションログ構造は、サービス、操作、トランザクションタイプなどの様々なパラメータを使用して、各トランザクションを記録する方法を定義します。 それぞれの詳細は以下の通りです。 トランザクションレコードの構造は次のとおりです。

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

* **サービス**：サービスの名前。
* **操作**：操作名。
* **internalService**：内部呼び出しの場合は呼び出し元の名前。それ以外の場合はサービス名と同じ。
* **internalOperation**：内部呼び出しの場合は呼び出しの名前。それ以外は操作名と同じです。
* **transactionOperationType**：トランザクションのタイプ（送信、レンダリング、変換）。
* **transactionCount**：トランザクションの合計数。
* **elapsedTime**：呼び出しの開始から受信した応答までの時間。
* **transactionDate**：サービスが呼び出された日時を示すタイムスタンプ。

**トランザクションログの例**:

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

トランザクションの記録頻度は、送信、レンダリングまたは変換が成功したフォームごとに、サーバー上の更新操作によって決まります。

* In **dashboard** トランザクション数は定期的に更新され、デフォルトは 1 分に設定されます。 頻度は、次の場所でシステムプロパティを設定することで更新できます。 `"com.adobe.idp.dsc.transaction.recordFrequency"`. 例えば、JBoss®上の JEE のAEM Formsで、 `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` in `JAVA_OPTS` 更新頻度を 5 分に設定する場合。

* In **トランザクションログ**&#x200B;フォームの送信、レンダリング、変換が正常に完了すると、各トランザクションの更新が即座におこなわれます。

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

* [JEE 上のAEM Formsの課金対象 API のリスト](../../forms/using/transaction-reports-billable-apis-jee.md)
* [JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションの記録](/help/forms/using/record-transaction-custom-component-jee.md)
