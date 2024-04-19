---
title: JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションを記録します。
description: TransactionRecorder API を使用してカスタムコンポーネントのトランザクションを記録する方法について説明します。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションの記録 {#record-a-transaction-for-custom-components}

カスタムコンポーネントで課金対象の API を使用する場合は、コンポーネントのトランザクションレポートを有効にできます。 トランザクションレポートを有効にするには、 `component.xml` コンポーネントのファイルであり、トランザクションレポートを有効にする必要がある操作の下で以下に示すタグを追加します。

**タグ**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 古い操作タグ | 新しい操作タグ |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

API に対して複数のトランザクションを取得する必要がある場合（トランザクション数が入力数によって異なるバッチ API など）、API レベルでトランザクション数を処理します。

**変動トランザクション数を記録する手順は、次のとおりです。**

1. クラスをインポート `"com.adobe.idp.dsc.InvocationContextStack"` コード内。 クラスは、 `adobe-livecycle-client.jar` sdk ファイル。 SDK ファイルは、次の場所から入手できます。 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 既にバンドルされている場合は、クライアントプロジェクトで上記で共有されたクライアントファイルを新しいファイルで更新します。

1. 様々なトランザクションをログに記録する必要がある API:
   1. ロジックを追加して、トランザクション数を次のような整数変数に格納できます。 `transaction_count`.
   1. 操作に成功したら、次を追加します `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 関連記事

* [JEE 上のAEM Formsのトランザクションレポートの有効化と表示](/help/forms/using/transaction-report-overview-jee.md)
* [JEE 上のAEM Formsの課金対象 API のリスト](/help/forms/using/transaction-reports-billable-apis-jee.md)
