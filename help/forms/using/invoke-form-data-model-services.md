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

AEM Forms を使用すると、アダプティブフォームフィールド内からフォームデータモデルで構成されたサービスを呼び出すことで、フォーム作成者はフォームへの記入作業を簡略化および強化することができます。To invoke a data model service, you can either create a rule in the visual editor or specify a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API in the code editor of the [rule editor](/help/forms/using/rule-editor.md).

This document focuses on writing a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API to invoke a service.

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

The structure of the `guidelib.dataIntegrationUtils.executeOperation` API specifies details about the service operation. この構造の構文は以下のとおりです。

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
   <td>Maps one or more form objects to output values from the service operation to populate form fields<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>サービス操作の入力引数に基づいて値を返します。 コールバック関数として使用されるオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>successコールバック関数が入力引数に基づいて出力値を表示できない場合に、エラーメッセージを表示します。 コールバック関数として使用されるオプションのパラメーターです。<br /> </td>
  </tr>
 </tbody>
</table>

## サービスを呼び出すスクリプトのサンプル {#sample-script-to-invoke-a-service}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `getAccountById` service operation configured in the `employeeAccount` form data model.

The `getAccountById` operation takes the value in the `employeeID` form field as input for the `empId` argument and returns employee name, account number, and account balance for the corresponding employee. この出力値は指定されたフォームフィールドに入力されます。For example, the value in `name` argument is populated in the `fullName` form element and value for `accountNumber` argument in `account` form element.

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

## コールバック関数でのAPIの使用 {#using-the-api-callback}

APIとコールバック関数を使用してフォームデータモデルサービスを呼び出すこ `guidelib.dataIntegrationUtils.executeOperation` ともできます。 API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

コールバック関数は、 `success` および `failure` コールバック関数を持つことができます。

### 成功コールバック関数と失敗コールバック関数を含むサンプルスクリプト {#callback-function-success-failure}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `GETOrder` service operation configured in the `employeeOrder` form data model.

この `GETOrder` 操作は、フォームフィールド内の値を `Order ID` 引数の入力として受け取り、 `orderId``success` コールバック関数に注文数量の値を返します。  コールバック関数が注文数量を返さない場合、 `success` コールバック関数は `failure``Error occured` メッセージを表示します。

>[!NOTE]
>
> callback関数を使用する場合、出力値は指定したフォームフィールドに入力されません。 `success`

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
