---
title: カスタム実装用のトランザクションの記録
seo-title: カスタム実装用のトランザクションの記録
description: TransactionRecorder APIを使用して、トランザクションとして計上されないアクションを自動的に記録します
seo-description: TransactionRecorder APIを使用して、トランザクションとして計上されないアクションを自動的に記録します
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# カスタム実装用のトランザクションの記録 {#record-a-transaction-for-custom-implementations}

TransactionRecorder APIを使用して、トランザクションとして計上されないアクションを自動的に記録します

カスタムコードを使用してPDFフォームを送信したり、エージェントUIプレビューURLをエンドユーザーに送信してインタラクティブ通信をプレビューしたり、AEM Formsで提供される送信メソッドを使用する代わりに、カスタムメソッドを使用してフォームを送信したりできます。 AEM Forms APIの前述のすべてのアクションおよびカスタム実装は、トランザクションと見なされません。 AEM Formsには、トランザクションなどのアクシ [ョンを記録する](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)API TransactionRecorderが用意されています。

トランザクションを記録するには、標準のスリング [サーブレットを書き込み](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) 、クライアントからサーブレットを呼び出してトランザクションを記録します。 サーブレットは、AJAXまたはその他の標準的な方法を使用して呼び出すことができます。

## サーバー側コードの例 {#sample-server-sided-code}

以下のサンプルコードを使用して、カスタムOSGiバンドルを使用してJAVAクラスからTransactionRecorder APIを実行できます。

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

## クライアント側コードの例 {#sample-client-side-code}

以下のサンプルコードを使用して、 `TransactionRecorder`APIを持つサーブレットを呼び出すことができます。

```
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
* [取引レポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [トランザクションレポート請求可能API](/help/forms/using/transaction-reports-billable-apis.md)

