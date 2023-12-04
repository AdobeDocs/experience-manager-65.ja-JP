---
title: AEM アダプティブフォームのコアコンポーネントに基づいてアダプティブフォームにカスタムエラーハンドラーを追加
description: AEM Forms は、外部サービスを呼び出すように設定された REST エンドポイントを使用して、標準で使用できるサクセスハンドラーとエラーハンドラーをフォームに提供します。AEM アダプティブフォームには、デフォルトのエラーハンドラーや、カスタムのエラーハンドラーを追加できます。
keywords: カスタムエラーハンドラーを追加、デフォルトのエラーハンドラーを追加、フォームにエラーハンドラーを追加、ルールエディターのサービス呼び出しを使用してカスタムエラーハンドラーを追加、ルールエディターを設定してカスタムエラーハンドラーを追加、ルールエディターを使用してカスタムエラーハンドラーを追加
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
exl-id: 2118d77f-1314-48f1-88e3-e27dd8e9f17b
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 90%

---

# アダプティブForms（コアコンポーネント）のエラーハンドラー {#error-handlers-in-adaptive-form}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/add-custom-error-handler-adaptive-forms-core-components.html) |
| AEM 6.5 | この記事 |

AEM Forms には、すぐに使用できる、フォーム送信の成功ハンドラーと失敗ハンドラーが用意されています。また、エラーハンドラー関数をカスタマイズする機能もあります。例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。API を使用して外部サービスが呼び出されると、データが検証のためにサーバーに送信され、サーバーは送信の成功イベントまたはエラーイベントに関する情報と共に、応答をクライアントに返します。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。エラーハンドラーは、発生したエラーや検証の問題を管理したり表示したりするのに役立ちます。

![フォームへのカスタムエラーハンドラーの追加方法を理解するためのエラーハンドラーワークフロー](/help/forms/using/assets/error-handler-workflow.png)

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに指定された入力を検証し、外部サービスを呼び出すように設定された REST エンドポイントから返される様々なエラーを確認します。アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。例えば、RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、その値は他のデータソースに送信され、アダプティブフォームはエラーハンドラーを使用してエラーメッセージを表示します。 この方法と同様に、アダプティブフォームをカスタムエラーと統合して、データ検証を実行します。入力値が検証条件を満たさない場合、アダプティブフォームのフィールドレベルでエラーメッセージが表示されます。サーバーから返される検証エラーメッセージが、標準メッセージ形式の場合に発生します。


## エラーハンドラーの使用 {#uses-of-error-handler}

エラーハンドラーは、様々な目的で使用されます。エラーハンドラー関数の使用例の一部を以下に示します。

* **検証の実行**：事前定義されたルールや条件に対してユーザー入力を検証することで、エラー処理を開始します。ユーザーがアダプティブフォームに入力すると、エラーハンドラーは入力を検証し、必要な形式、長さ、その他の制約が満たされていることを確認します。

* **リアルタイムでのフィードバックの提供**：エラーが検出されると、エラーハンドラーは、対応するフォームフィールドの下にフィードバック（インラインエラーメッセージなど）を、ユーザーに即時に表示します。このフィードバックは、ユーザーがフォームを送信して応答を待たなくても、エラーを特定して修正するのに役立ちます。


* **エラーメッセージの表示**：アダプティブフォームの送信で検証エラーが発生すると、エラーハンドラーは適切なエラーメッセージを表示します。 エラーメッセージは、明確かつ簡潔で、注意が必要な特定のフィールドをハイライト表示する必要があります。

* **エラーのあるフィールドのハイライト表示**：特定の誤ったフィールドにユーザーの注意を引くために、エラーハンドラーは対応するフィールドをハイライト表示するか、視覚的に区別します。この処理は、背景色の変更、アイコンや境界線の追加、またはユーザーがエラーを迅速に見つけて対処する上で役立つ、その他の視覚的なヒントを追加することによって実行されます。


## 失敗／エラー応答形式 {#failure-response-format}

サーバー検証エラーメッセージが次の標準形式の場合、アダプティブフォームはフィールドレベルでエラーを表示します。
次のコードは、既存の失敗応答構造を示しています。

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


ここで、

* `errorCausedBy` は失敗の理由を説明します.
* `errors` 検証エラーメッセージと共に、検証条件に失敗したフィールドの修飾フィールド名について言及します。
* `originCode` は AEM によって追加され、外部サービスから返された http ステータスコードが含まれます。
* `originMessage` フィールドは AEM によって追加され、外部サービスから返された生のエラーデータが含まれます。

AEM Forms バージョンの機能の改善とその後の更新に伴い、既存の失敗応答構造は、既存の失敗応答構造と下位互換性のある RFC7807 に基づく新しい形式に変更されました。

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - if there is SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - if there is SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * エラー応答構造に **fieldName** または **dataRef** が含まれていることを確認してください。
> * **ContentType** ヘッダーが **application/problem+json** であることを確認します。

ここで、
* `type (required)` は失敗のタイプを指定します。次のいずれかの値になります。
   * `SERVER_SIDE_VALIDATION` は、サーバーサイドの検証が原因でエラーが発生したことを示します。
   * `FORM_SUBMISSION` は、フォームの送信中にエラーが発生したことを示します
   * `SERVICE_INVOCATION` は、サードパーティのサービスの呼び出し中に失敗が発生したことを示します。
   * `FAILURE` は、一般的な失敗を示します。
   * `VALIDATION_ERROR` は、検証エラーが原因で失敗が発生したことを示します。

* `title (optional)` は、失敗のタイトルまたは簡単な説明を示します。
* `detail (optional)` は、必要に応じて、失敗に関する追加の詳細を示します。
* `instance (optional)` は、失敗に関連付けられたインスタンスまたは識別子を表し、特定の失敗の発生を追跡したり識別したりするのに役立ちます。
* `validationErrors (required)` には、検証エラーに関する情報が含まれています。次のフィールドが含まれています。
   * `fieldname` は、検証条件を満たさなかったフィールドの修飾フィールド名に言及します。
   * `dataRef` は、検証に失敗したフィールドの JSON パスまたは XPath を表します。
   * `details` には、検証エラーメッセージとエラーのあるフィールドが含まれています。
* `originCode (optional)` は、AEMによって追加されたフィールドで、外部サービスから返された http ステータスコードが含まれています。
* `originMessage (optional)` は、AEMによって追加されたフィールドで、外部サービスから返された生のエラーデータが含まれています。

### エラー応答形式のサンプル {#sample-error-response-format}

エラー応答を表示するオプションの一部を次に示します。

+++  アダプティブフォームの fieldName プロパティに基づく場合


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```


+++


+++ アダプティブフォームの dataRef プロパティに基づく場合

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

+++

## 前提条件 {#prerequisites}

アダプティブFormsでエラーハンドラーを使用する前に、次の手順を実行します。

* [環境でのアダプティブFormsコアコンポーネントの有効化](enable-adaptive-forms-core-components.md).
* 基本知識 [カスタム関数の作成](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* [Apache Maven](https://maven.apache.org/download.cgi) の最新リリースをインストールします。

## ルールエディターを使用してエラーハンドラーを追加 {#add-error-handler-using-rule-editor}

[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke)アクションを使用して、アダプティブフォームで使用するデータソースに基づいて検証条件を定義します。RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。アダプティブフォームのエラーハンドラー関数とルールエディターを利用すると、エラー処理を効果的に管理およびカスタマイズできます。ルールエディターを使用して条件を定義し、ルールがトリガーされたときに実行するアクションを設定します。アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した内容を検証します。入力値が検証条件を満たさない場合、エラーメッセージはアダプティブフォームのフィールドレベルで表示されます。

>[!NOTE]
>
> * ルールエディターのサービスの呼び出しアクションでエラーハンドラーを使用するには、フォームデータモデルを使用してアダプティブフォームを設定します。
> * デフォルトのエラーハンドラーは、エラー応答が標準スキーマにある場合にフィールドにエラーメッセージを表示するために使用します。デフォルトのエラーハンドラーは、カスタムエラーハンドラー関数から呼び出すこともできます。

ルールエディターを使用して、次の操作を実行できます。

* [デフォルトのエラーハンドラー関数を追加](#add-default-errror-handler)
* [カスタムエラーハンドラー関数を追加](#add-custom-errror-handler)


### デフォルトのエラーハンドラー関数を追加 {#add-default-errror-handler}

デフォルトのエラーハンドラーは、エラー応答が標準スキーマの場合、またはサーバーサイドの検証エラーの場合に、フィールドにエラーメッセージを表示する機能をサポートしています。
[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke) action, take an example of a simple Adaptive Form with two fieldsアクションを使用してカスタムエラーハンドラーを作成および使用する方法を理解するために、「**ペット ID**」および「**ペット名**」という 2 つのフィールドを持つアダプティブフォームを例に、「**ペット ID**」でカスタムエラーハンドラーを使用して、`200 - OK`、`404 - Not Found`、`400 - Bad Request` などの外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーをチェックしましょう。ルールエディターのサービスの呼び出しアクションを使用してデフォルトのエラーハンドラーを追加するには、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択して、 **[!UICONTROL ルールエディター]** をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ルールの&#x200B;**条件**&#x200B;セクションで条件を作成します。例： **条件[ペット ID フィールドの名前]** が変更されました。 「 」を **状態を選択** 」ドロップダウンリストから選択できます。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. 「**入力**」セクションから、**Post サービス**&#x200B;とそれに対応するデータ連結を選択します。例えば、**ペット ID** を検証する場合は、**Post サービス**&#x200B;を **GET /pet/{petId}** として選択し、「**入力**」セクションで「**ペット ID**」を選択します。
1. 「**出力**」セクションからデータ連結を選択します。例えば、「**出力**」セクションで「**ペット名**」を選択します。
1. 「**[!UICONTROL エラーハンドラー]**」セクションから「**カスタムエラーハンドラー**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![フォーム内のフィールド検証チェックにデフォルトのエラーハンドラーを追加する](/help/forms/using/assets/default-error-handler.png)

このルールの結果、REST エンドポイントによって呼び出された外部サービスを使用して、**ペット ID** に入力した値が&#x200B;**ペット名**&#x200B;の検証をチェックします。データソースに基づく検証条件が失敗した場合は、エラーメッセージがフィールドレベルで表示されます。

![デフォルトのエラーメッセージを表示するには、エラー応答を処理するためのフォームにデフォルトのエラーハンドラーを追加します](/help/forms/using/assets/default-error-message.png)

### カスタムエラーハンドラー関数を追加 {#add-custom-errror-handler}

カスタムエラーハンドラー関数を追加して、次のようなアクションを実行できます。

* 非標準または標準のエラー応答を使用するエラー応答を処理します。これらの非標準のエラー応答は、[エラー応答の標準スキーマ](#failure-response-format)に準拠していないことに注意する必要があります。
* 分析イベントを任意の分析プラットフォームに送信します。例：Adobe Analytics.
* エラーメッセージが表示されるモーダルダイアログを表示します。

上記のアクションに加えて、カスタムエラーハンドラーを使用して、特定のユーザー要件を満たすカスタマイズされた関数を実行できます。

カスタムエラーハンドラーは、外部サービスから返されたエラーに応答し、カスタマイズされた応答をエンドユーザーに配信するように設計された関数（クライアントライブラリ）です。注釈 `@errorHandler` 付きのクライアントライブラリは、カスタムエラーハンドラー関数と見なされます。この注釈は、 `.js` ファイル。

[ルールエディターのサービスの呼び出し](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=ja#invoke)アクションを使用してカスタムエラーハンドラーを作成および使用する方法を理解するために、「**ペット ID**」および「**ペット名**」という 2 つのフィールドを持つアダプティブフォームを例に、「**ペット ID**」でカスタムエラーハンドラーを使用して、`200 - OK`、`404 - Not Found`、`400 - Bad Request` などの外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーをチェックしましょう。

アダプティブフォームにカスタムエラーハンドラーを追加して使用するには、次の手順を実行します。

1. [カスタムエラーハンドラーを作成](#create-custom-error-message)
1. [ルールエディターを使用してカスタムエラーハンドラーを設定](#use-custom-error-handler)

#### 1. カスタムエラーハンドラーを作成 {#create-custom-error-message}

カスタムエラー関数を作成するには、次の手順を実行します。

1. ログイン `http://server:port/crx/de/index.jsp#`.
1. の下にフォルダーを作成します。 `/apps` フォルダー。 例えば、という名前のフォルダーを作成します。 `experience-league`.
1. 変更を保存します。
1. 作成したフォルダーに移動し、タイプのノードを作成します。 `cq:ClientLibraryFolder` as `clientlibs`.
1. 新しく作成された `clientlibs` フォルダーを作成し、 `allowProxy` および `categories` プロパティ：

   ![カスタムライブラリノードのプロパティ](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > 次の場所の代わりに任意の名前を指定できます。 `customfunctionsdemo`.

1. 変更を保存します。

1. という名前のフォルダーを作成します。 `js` の下に `clientlibs` フォルダー。
1. という名前の JavaScript ファイルを作成します。 `functions.js` の下に `js` フォルダー
1. という名前のファイルを作成します。 `js.txt` の下に `clientlibs` フォルダー。
1. 変更を保存します。
作成したフォルダー構造は次のようになります。

   ![作成されたクライアントライブラリフォルダー構造](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. 次をダブルクリックします。 `functions.js` ファイルを開き、エディターを開きます。 ファイルには、カスタムエラーハンドラーのコードが含まれています。
次のコードを JavaScript ファイルに追加して、REST サービスエンドポイントから受け取った応答とヘッダーをブラウザーコンソールに表示します。

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           alert("CustomErrorHandler - Please enter valid PetId.")
           globals.invoke('defaultErrorHandler',response, headers)
           console.log("Custom Error Handler processing end...");
       }
   ```

   カスタムエラーハンドラーからデフォルトのエラーハンドラーを呼び出すには、サンプルコードの次の行が使用されます。
   `globals.invoke('defaultErrorHandler',response, headers) `

1. 保存 `function.js`.
1. に移動します。 `js.txt` 次のコードを追加します。

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` ファイルを保存します。

次に、ルールエディターのサービスの呼び出しを AEM Forms で使用して、カスタムエラーハンドラーを設定して使用する方法を説明します。

#### 2. ルールエディターを使用して、カスタムエラーハンドラーを設定 {#use-custom-error-handler}

アダプティブフォームにカスタムエラーハンドラーを実装する前に、クライアントライブラリ名が **[!UICONTROL クライアントライブラリカテゴリ]** は、 `.content.xml` ファイル。

![アダプティブフォームコンテナ設定にクライアントライブラリの名前を追加する](/help/forms/using/assets/client-library-category-name-core-component.png)

この場合、クライアントライブラリ名は `customfunctionsdemo` （内） `.content.xml` ファイル。

**[!UICONTROL ルールエディターのサービスの呼び出し]**&#x200B;アクションを使用してカスタムエラーハンドラーを使用するには、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択して、 **[!UICONTROL ルールエディター]** をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ルールの&#x200B;**条件**&#x200B;セクションで条件を作成します。例えば、**[ペット ID の名前フィールド]**&#x200B;が変更された場合は、「**状態を選択** 」ドロップダウンリストから「**変更済み**」を選択します。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. 「**入力**」セクションから、**Post サービス**&#x200B;とそれに対応するデータ連結を選択します。例えば、**ペット ID** を検証する場合は、**Post サービス**&#x200B;を **GET /pet/{petId}** として選択し、「**入力**」セクションで「**ペット ID**」を選択します。
1. 「**出力**」セクションからデータ連結を選択します。例えば、「**出力**」セクションで「**ペット名**」を選択します。
1. 「**[!UICONTROL エラーハンドラー]**」セクションから「**[!UICONTROL カスタムエラーハンドラー]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/using/assets/custom-error-handler.png)

このルールの結果、REST エンドポイントによって呼び出された外部サービスを使用して、**ペット ID** に入力した値が&#x200B;**ペット名**&#x200B;の検証をチェックします。データソースに基づく検証条件が失敗した場合は、エラーメッセージがフィールドレベルで表示されます。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/using/assets/custom-error-handler-message-core-component.png)

ブラウザーコンソールを開き、REST サービスエンドポイントから受け取った応答とヘッダーで、検証エラーメッセージを確認します。

カスタムエラーハンドラー関数は、エラー応答に基づいて、モーダルダイアログの表示や分析イベントの送信など、追加のアクションを実行します。カスタムエラーハンドラー関数を使用すると、特定のユーザー要件に合わせて柔軟にエラー処理をカスタマイズできます。

## 関連トピック {#see-also}

* [スタンドアロンのコアコンポーネントベースのアダプティブフォームを作成](/help/forms/using/create-an-adaptive-form-core-components.md)
* [フォームのスタイルまたはテーマを作成](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
* [AEM Sites ページへのアダプティブフォームの作成または追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)
