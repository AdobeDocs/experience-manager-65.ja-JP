---
title: JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションを記録します。
description: TransactionRecorder API を使用してカスタムコンポーネントのトランザクションを記録する方法について説明します。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 5%

---

# JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションの記録 {#record-a-transaction-for-custom-components}

カスタムコンポーネントで課金対象の API を使用する場合は、コンポーネントのトランザクションレポートを有効にできます。 トランザクションレポートを有効にするには、コンポーネントの `component.xml` ファイルを変更し、トランザクションレポートを有効にする必要がある操作の下に以下のタグを追加します。

**タグ**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 古い操作タグ | 新しい操作タグ |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

API に対して複数のトランザクションを取得する必要がある場合（トランザクション数が入力数によって異なるバッチ API など）、API レベルでトランザクション数を処理します。

**変更されたトランザクション数を記録するには、次の手順に従います。**

1. コード内のクラス `"com.adobe.idp.dsc.InvocationContextStack"` をインポートします。 クラスは、`adobe-livecycle-client.jar` sdk ファイルの一部です。 SDK ファイルは `<AEM_Forms_JEE_Install>\sdk\client-libs\common` で入手できます。

   >[!NOTE]
   > 既にバンドルされている場合は、クライアントプロジェクトで上記で共有されたクライアントファイルを新しいファイルで更新します。

1. 様々なトランザクションをログに記録する必要がある API:
   1. トランザクション数を `transaction_count` などの整数変数に格納できるロジックを追加します。
   1. 操作に成功したら、`InvocationContextStack.recordTransactionCount(transaction_count)` を追加します。

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 関連記事

* [JEE 上のAEM Formsのトランザクションレポートの有効化と表示](/help/forms/using/transaction-report-overview-jee.md)
* [JEE 版 AEM Forms の課金対象 API のリスト](/help/forms/using/transaction-reports-billable-apis-jee.md)
