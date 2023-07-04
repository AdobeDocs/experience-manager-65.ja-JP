---
title: カスタム実装のトランザクションの記録
seo-title: Record a transaction for custom implementations
description: トランザクションとして自動的に計上されないアクションを記録するには、TransactionRecorder API を使用します
seo-description: Use the TransactionRecorder API to record actions which are not accounted as transactions automatically
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: ht
source-wordcount: '222'
ht-degree: 100%

---

# カスタム実装のトランザクションの記録 {#record-a-transaction-for-custom-implementations}

トランザクションとして自動的に計上されないアクションを記録するには、TransactionRecorder API を使用します

カスタムコードを使用すると、PDF フォームを送信したり、エージェント UI のプレビュー URL をエンドユーザーに送信してインタラクティブ通信をプレビューしたりできます。または、AEM Forms で提供される送信メソッドを使用する代わりに、カスタムメソッドを使用してフォームを送信することもできます。前述の AEM Forms API のすべてのアクションとカスタム実装は、トランザクションとはみなされません。AEM Forms には [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html) という API があり、トランザクションなどのアクションを記録することができます。

トランザクションを記録するには、 [標準 Sling サーブレット](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=ja) を書き込み、サーブレットをクライアントから呼び出してトランザクションを記録します。AJAX またはその以外の標準的な方法を使用して、サーブレットを呼び出すことができます。

## サーバー側コードのサンプル {#sample-server-sided-code}

以下のサンプルコードを使用すると、カスタム OSGi バンドルを使用して JAVA クラスから TransactionRecorder API を実行できます。

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## クライアントサイドコードのサンプル {#sample-client-side-code}

以下のサンプルコードを使用して、 `TransactionRecorder` API を持つサーブレットを

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](/help/forms/using/transaction-reports-overview.md)
* [トランザクションレポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [トランザクションレポート請求可能 API](/help/forms/using/transaction-reports-billable-apis.md)
