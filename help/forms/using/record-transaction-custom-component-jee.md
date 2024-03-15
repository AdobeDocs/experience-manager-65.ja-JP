---
title: JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションを記録します。
description: カスタムコンポーネントのトランザクションを記録するには、TransactionRecorder API を使用します。
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションの記録 {#record-a-transaction-for-custom-components}

カスタムコンポーネントで課金対象 API を使用する場合、そのコンポーネントのトランザクションレポートを有効にすることができます。 トランザクションレポートを有効にするには、 `component.xml` コンポーネントのファイルを開き、トランザクションレポートを有効にする必要がある操作の下に、以下のタグを追加します。

**タグ**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 古い操作タグ | 新しい操作タグ |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

1 つの API の複数のトランザクションを取得する必要がある場合（例えば、トランザクション数が入力数によって異なるバッチ API の場合）。この場合、API レベルでトランザクション数を処理する必要があります。 次に、様々なトランザクション数を記録する手順を示します。

1. クラスをインポート `"com.adobe.idp.dsc.InvocationContextStack"` を設定します。 このクラスは、 `adobe-livecycle-client.jar` sdk ファイル。 SDK ファイルは、次の場所にあります。 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 既にバンドルされている場合に備えて、クライアントプロジェクトで上で共有されているクライアントファイルを新しいファイルで更新します。

1. 様々なトランザクションをログに記録する必要がある API で、次の手順を実行します。
   1. トランザクション数を何らかの整数変数（例： ）に格納するロジックを追加します。 `transaction_count`.
   1. 操作が正常に完了したら、 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 関連記事

* [JEE 上のAEM Formsのトランザクションレポートの有効化と表示](/help/forms/using/transaction-report-overview-jee.md)
* [JEE 上のAEM Formsの課金対象 API のリスト](/help/forms/using/transaction-reports-billable-apis-jee.md)


