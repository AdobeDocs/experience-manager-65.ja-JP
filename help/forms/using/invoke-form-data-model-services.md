---
title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
seo-title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
description: アダプティブフォームフィールド内から WSDL で記述された、Web サービスを呼び出す API について説明します。
seo-description: アダプティブフォームフィールド内から WSDL で記述された、Web サービスを呼び出す API について説明します。
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 34%

---


# アダプティブフォームからフォームデータモデルサービスを呼び出すための API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概要 {#overview}

AEM Forms を使用すると、アダプティブフォームフィールド内からフォームデータモデルで構成されたサービスを呼び出すことで、フォーム作成者はフォームへの記入作業を簡略化および強化することができます。データモデルサービスを呼び出すには、ビジュアルエディターでルールを作成するか、[ルールエディター](/help/forms/using/rule-editor.md)のコードエディターで`guidelib.dataIntegrationUtils.executeOperation` APIを使用してJavaScriptを指定します。

このドキュメントでは、`guidelib.dataIntegrationUtils.executeOperation` APIを使用してサービスを呼び出すJavaScriptの作成に重点を置いています。

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` APIの構造はサービス操作の詳細を指定します。 この構造の構文は以下のとおりです。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API 構造は、サービス操作の以下の詳細を指定します。

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>フォームデータモデルの識別子、操作タイトル、操作名を指定する構造</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>名前を含むフォームデータモデルへのリポジトリパスを指定します</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>実行するサービス操作の名前を指定します</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>1つ以上のフォームオブジェクトをサービス操作の入力引数にマップします</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>1つ以上のフォームオブジェクトを、サービス操作の出力値にマップして、フォームフィールドに入力します。<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>サービス操作の入力引数に基づいて値を返します。 コールバック関数として使用されるオプションのパラメータです。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>successコールバック関数が入力引数に基づいて出力値を表示できない場合に、エラーメッセージを表示します。 コールバック関数として使用されるオプションのパラメータです。<br /> </td>
  </tr>
 </tbody>
</table>

## サービスを呼び出すスクリプトのサンプル {#sample-script-to-invoke-a-service}

次のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` APIを使用して、`employeeAccount`フォームデータモデルで設定された`getAccountById`サービス操作を呼び出します。

`getAccountById`演算は、`empId`引数の入力として`employeeID`フォームフィールドの値を受け取り、対応する従業員の従業員名、口座番号、口座残高を返します。 この出力値は指定されたフォームフィールドに入力されます。例えば、`name`引数の値が`fullName`フォーム要素に入力され、`account`フォーム要素の`accountNumber`引数の値が入力されます。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## コールバック関数{#using-the-api-callback}でAPIを使用する

`guidelib.dataIntegrationUtils.executeOperation` APIとコールバック関数を使用してフォームデータモデルサービスを呼び出すこともできます。 API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

コールバック関数は、`success`および`failure`コールバック関数を持つことができます。

### 成功コールバック関数と失敗コールバック関数を持つサンプルスクリプト{#callback-function-success-failure}

次のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` APIを使用して、`employeeOrder`フォームデータモデルで設定された`GETOrder`サービス操作を呼び出します。

`GETOrder`操作は、`orderId`引数の入力として`Order ID`フォームフィールドの値を受け取り、`success`コールバック関数に注文数量の値を返します。  `success`コールバック関数が注文数を返さない場合、`failure`コールバック関数は`Error occured`メッセージを表示します。

>[!NOTE]
>
> `success`コールバック関数を使用する場合、指定したフォームフィールドに出力値が入力されません。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
