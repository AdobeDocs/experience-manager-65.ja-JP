---
title: JEE 上の AEM Forms のカスタムコンポーネント API のトランザクションの記録
description: TransactionRecorder API を使用してカスタムコンポーネントのトランザクションを記録する方法について説明します。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: bcb3e79d-a57e-59a4-ad50-e03803c9f153
    internal-label: Transaction Reports
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%
---
# JEE における AEM Forms のカスタムコンポーネント API のトランザクションの記録 {#record-a-transaction-for-custom-components}

カスタムコンポーネントで課金対象 API を使用する場合は、コンポーネントのトランザクションレポートを有効にできます。 トランザクションレポートを有効にするには、コンポーネントの `component.xml` ファイルを変更し、トランザクションレポートを有効にする必要がある操作の下に以下のタグを追加します。

**タグ**：`<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 古い操作タグ | 新しい操作タグ |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

トランザクション数が入力数に応じて異なるバッチ API など、API に対して複数のトランザクションを記録する必要がある場合は、API レベルでトランザクション数を処理します。

**異なるトランザクション数を記録するには：**

1. コードでクラス `"com.adobe.idp.dsc.InvocationContextStack"` を読み込みます。 クラスは、`adobe-livecycle-client.jar` SDK ファイルの一部です。 SDK ファイルは `<AEM_Forms_JEE_Install>\sdk\client-libs\common` に格納されています。

   >[!NOTE]
   > 既にバンドルされている場合は、クライアントプロジェクトで上記で共有されたクライアントファイルを新しいファイルで更新します。

1. 様々なトランザクションをログに記録する必要がある API の場合：
   1. トランザクション数を `transaction_count` などの整数変数に格納できるようにロジックを追加します。
   1. 操作が成功したら、`InvocationContextStack.recordTransactionCount(transaction_count)` を追加します。

<!--
For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.
-->

## 関連記事

* [JEE 上の AEM Forms のトランザクションレポートの有効化と表示](/help/forms/using/transaction-report-overview-jee.md)
* [JEE における AEM Forms の課金対象 API のリスト](/help/forms/using/transaction-reports-billable-apis-jee.md)
