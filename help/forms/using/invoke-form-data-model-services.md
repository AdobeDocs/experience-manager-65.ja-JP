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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# アダプティブフォームからフォームデータモデルサービスを呼び出すための API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## 概要 {#overview}

AEM Forms を使用すると、アダプティブフォームフィールド内からフォームデータモデルで構成されたサービスを呼び出すことで、フォーム作成者はフォームへの記入作業を簡略化および強化することができます。To invoke a data model service, you can either create a rule in the visual editor or specify a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API in the code editor of the [rule editor](/help/forms/using/rule-editor.md).

This document focuses on writing a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API to invoke a service.

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

この API には以下のパラメーターが必要です。

| パラメーター | 説明 |
|---|---|
| `operationInfo` | フォームデータモデルの識別子、操作タイトル、操作名を指定する構造 |
| `inputs` | サービス操作に値が入力されるフォームオブジェクトを指定する構造 |
| `outputs` | サービス操作から返される値を使用して入力されるフォームオブジェクトを指定する構造 |

The structure of the `guidelib.dataIntegrationUtils.executeOperation` API specifies details about the service operation. この構造の構文は以下のとおりです。

```
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
   <td><code>forDataModelId</code></td>
   <td>フォームデータモデルへのリポジトリパスをその名前も含めて指定する</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>実行するサービス操作の名前を指定する</td>
  </tr>
  <tr>
   <td><code>input</code></td>
   <td>1 つ以上のフォームオブジェクトをサービス操作の入力引数にマップする</td>
  </tr>
  <tr>
   <td>出力</td>
   <td>1 つ以上のフォームオブジェクトをサービス操作からの出力値にマップしてフォームフィールドを埋め込む<br /> </td>
  </tr>
 </tbody>
</table>

## サービスを呼び出すスクリプトのサンプル {#sample-script-to-invoke-a-service}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `getAccountById` service operation configured in the `employeeAccount` form data model.

The `getAccountById` operation takes the value in the `employeeID` form field as input for the `empId` argument and returns employee name, account number, and account balance for the corresponding employee. この出力値は指定されたフォームフィールドに入力されます。For example, the value in `name` argument is populated in the `fullName` form element and value for `accountNumber` argument in `account` form element.

```
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

