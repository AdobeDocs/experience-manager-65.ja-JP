---
title: AEM Adaptive Formsのコアコンポーネントに基づいて、アダプティブFormsにカスタムエラーハンドラーを追加します。
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms core components
description: AEM Formsは、外部サービスを呼び出すように設定された REST エンドポイントを使用して、フォームに対して標準で提供される成功およびエラーハンドラーを提供します。 AEMアダプティブフォームに、デフォルトのエラーハンドラーとカスタムエラーハンドラーを追加できます。
seo-description: Error handler function and Rule Editor in Adaptive Forms core components helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: カスタムエラーハンドラーの追加、デフォルトエラーハンドラーの追加、フォームのエラーハンドラーの追加、ルールエディターの呼び出しサービスを使用したカスタムエラーハンドラーの追加、ルールエディターの設定、ルールエディターを使用したカスタムエラーハンドラーの追加
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 6d6e74c61b2ecb13e7cc352d5278c40d2677d44d
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 7%

---


# アダプティブForms（コアコンポーネント）のエラーハンドラー {#error-handlers-in-adaptive-form}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/add-custom-error-handler-adaptive-forms-core-components.html) |
| AEM 6.5 | この記事 |

AEM Forms には、すぐに使用できる、フォーム送信の成功および失敗ハンドラーが用意されています。また、エラーハンドラ関数をカスタマイズする機能も提供します。 例えば、特定のエラーコードに対してバックエンドでカスタムワークフローを呼び出したり、サービスが停止していることを顧客に通知したりできます。 ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。API を使用して外部サービスが呼び出されると、データが検証用にサーバーに送信され、クライアントに応答を返して送信の成功またはエラーイベントに関する情報を返します。 この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。エラーハンドラーは、発生したエラーや検証の問題を管理および表示するのに役立ちます。

![フォームにカスタムエラーハンドラーを追加する方法を理解するためのエラーハンドラーワークフロー](/help/forms/using/assets/error-handler-workflow.png)

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに指定した入力を検証し、外部サービスを呼び出すように設定された REST エンドポイントから返される様々なエラーを確認します。 アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。 例えば、RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、その値がデータソースの他のデータソースに送信され、アダプティブフォームはエラーハンドラーを使用してエラーメッセージを表示します。 この方法と同様に、アダプティブFormsはカスタムエラーハンドラーと統合して、データ検証を実行します。 入力値が検証条件を満たさない場合、エラーメッセージはアダプティブフォームのフィールドレベルに表示されます。 これは、サーバーから返される検証エラーメッセージが標準メッセージ形式の場合に発生します。


## エラーハンドラーの使用 {#uses-of-error-handler}

エラーハンドラーは、様々な目的で使用されます。 エラーハンドラー関数の使用の一部を以下に示します。

* **検証の実行**：エラー処理は、事前定義されたルールまたは条件に対してユーザー入力を検証することから開始します。 ユーザーがアダプティブフォームに入力すると、エラーハンドラーは入力を検証し、必要な形式、長さ、またはその他の制約を満たすようにします。

* **リアルタイムでのフィードバックの提供**：エラーが検出されると、エラーハンドラーは、対応するフォームフィールドの下にインラインエラーメッセージなど、ユーザーに対する即時のフィードバックを表示します。 このフィードバックは、ユーザーがフォームを送信して応答を待たなくても、エラーを識別して修正するのに役立ちます。


* **エラーメッセージの表示**：アダプティブフォームの送信で検証エラーが発生すると、エラーハンドラーは適切なエラーメッセージを表示します。 エラーメッセージは、明確で簡潔で、注意が必要な特定のフィールドをハイライト表示する必要があります。

* **エラーのあるフィールドをハイライトします**：ユーザーが注意を払って、間違った特定のフィールドに入れるために、エラーハンドラーは、対応するフィールドを強調表示するか、視覚的に区別します。 この処理は、背景色を変更したり、アイコンや境界線を追加したり、ユーザーがエラーをすばやく見つけて対処するのに役立つその他の視覚的なキューを追加したりすることで実行されます。


## 失敗/エラー応答の形式 {#failure-response-format}

サーバーの検証エラーメッセージが次の標準形式の場合、アダプティブフォームは、フィールドレベルでエラーを表示します。
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
* `originCode` 外部サービスが返す http ステータスコードを含む、AEMによって追加されたフィールド。
* `originMessage` 外部サービスから返される生のエラーデータを含む、AEMによって追加されたフィールド。

AEM Formsバージョンの機能の改善とその後の更新に伴い、既存の失敗応答構造は、既存の失敗応答構造との下位互換性を持つ RFC7807 に基づいて新しい形式に変更されました。

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
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * エラー応答構造に次のいずれかが含まれていることを確認します。 **fieldName** または **dataRef**.
> * 次の点を確認します。 **ContentType** ヘッダーは次のとおりです。 **application/problem+json**.

ここで、
* `type (required)` 失敗のタイプを指定します。 次のいずれかの値を指定できます。
   * `SERVER_SIDE_VALIDATION` は、サーバー側の検証が原因でエラーが発生したことを示します。
   * `FORM_SUBMISSION` フォームの送信中にエラーが発生したことを示します
   * `SERVICE_INVOCATION` サードパーティのサービスの呼び出し中にエラーが発生したことを示します。
   * `FAILURE` 一般的なエラーを示します。
   * `VALIDATION_ERROR` は、検証エラーが原因でエラーが発生したことを示します。

* `title (optional)` 失敗のタイトルまたは簡単な説明を示します。
* `detail (optional)` 必要に応じて、失敗に関する追加の詳細を示します。
* `instance (optional)` は、失敗に関連付けられたインスタンスまたは識別子を表し、失敗の特定の発生を追跡したり識別したりするのに役立ちます。
* `validationErrors (required)` には、検証エラーに関する情報が含まれています。 次のフィールドが含まれます。
   * `fieldname` では、検証条件に失敗したフィールドの修飾フィールド名が示されます。
   * `dataRef` は、検証に失敗したフィールドの JSON パスまたは XPath を表します。
   * `details` には、エラーフィールドを含む検証エラーメッセージが含まれています。
* `originCode (optional)` 外部サービスによって返された http ステータスコードを含む、AEMによって追加されたフィールド
* `originMessage (optional)` 外部サービスから返される生のエラーデータを含む、AEMによって追加されたフィールド。

### エラー応答形式のサンプル {#sample-error-response-format}

エラー応答を表示するオプションの一部を次に示します。

+++  アダプティブフォームの fieldName プロパティに基づく


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


+++ アダプティブフォームの dataRef プロパティに基づく

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

* [環境でのアダプティブフォームコアコンポーネントの有効化](enable-adaptive-forms-core-components.md).
* 基本知識 [カスタム関数の作成](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* 最新リリースのをインストールする [Apache Maven](https://maven.apache.org/download.cgi).

## ルールエディターを使用してエラーハンドラーを追加 {#add-error-handler-using-rule-editor}

の使用 [ルールエディターの Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 「 」アクションでは、アダプティブフォームで使用するデータソースに基づいて検証条件を定義します。 RESTful Web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。 アダプティブFormsのエラーハンドラー関数とルールエディターを使用すると、エラー処理を効果的に管理およびカスタマイズできます。 ルールエディターを使用して条件を定義し、ルールがトリガーされたときに実行するアクションを設定します。 アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 入力値が検証条件を満たさない場合、エラーメッセージはアダプティブフォームのフィールドレベルに表示されます。

>[!NOTE]
>
> * ルールエディターの Invoke サービスアクションでエラーハンドラーを使用するには、フォームデータモデルを使用して Adaptive Formsを設定します。
> * エラー応答が標準のスキーマにある場合に、フィールドにエラーメッセージを表示するデフォルトのエラーハンドラーが提供されます。 デフォルトのエラーハンドラーは、カスタムエラーハンドラー関数から呼び出すこともできます。

ルールエディターを使用して、次の操作を実行できます。

* [デフォルトのエラーハンドラー関数を追加](#add-default-errror-handler)
* [カスタムエラーハンドラー関数を追加](#add-custom-errror-handler)


### デフォルトのエラーハンドラー関数を追加 {#add-default-errror-handler}

デフォルトのエラーハンドラーは、エラー応答が標準のスキーマの場合、またはサーバー側の検証エラーの場合に、フィールドにエラーメッセージを表示する機能がサポートされています。
デフォルトのエラーハンドラーを使用する方法を理解するには、 [ルールエディターの Invoke Service](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 「 」アクションでは、2 つのフィールドを持つ簡単なアダプティブフォームの例を見てみましょう。 **ペット ID** および **ペット名** デフォルトのエラーハンドラを **ペット ID** 外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーを確認するフィールド。例えば、 `200 - OK`,`404 - Not Found`, `400 - Bad Request`. ルールエディターの「サービスを起動」アクションを使用してデフォルトのエラーハンドラーを追加するには、次の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択して、 **[!UICONTROL ルールエディター]** をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの&#x200B;**条件**&#x200B;セクションで条件を作成します。例： **条件[ペット ID フィールドの名前]** が変更されました。 「 」を **状態を選択** 」ドロップダウンリストから選択できます。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. を選択します。 **ポストサービス** と、対応するデータバインディングが **入力** 」セクションに入力します。 例えば、検証する場合は、次のようにします。 **ペット ID**&#x200B;を選択し、 **ポストサービス** as **GET/pet/{petId}** を選択し、 **ペット ID** （内） **入力** 」セクションに入力します。
1. からデータ連結を選択します。 **出力** 」セクションに入力します。 選択 **ペット名** （内） **出力** 」セクションに入力します。
1. 選択 **[!UICONTROL デフォルトのエラーハンドラー]** から **エラーハンドラー** 」セクションに入力します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![フォーム内のフィールド検証チェックにデフォルトのエラーハンドラーを追加する](/help/forms/using/assets/default-error-handler.png)

このルールの結果、 **ペット ID** 検証を確認 **ペット名** REST エンドポイントによって呼び出された外部サービスを使用する。 データソースに基づく検証条件が失敗した場合は、エラーメッセージがフィールドレベルで表示されます。

![デフォルトのエラーメッセージを表示するには、エラー応答を処理するためのフォームにデフォルトのエラーハンドラーを追加します](/help/forms/using/assets/default-error-message.png)

### カスタムエラーハンドラー関数を追加 {#add-custom-errror-handler}

カスタムエラーハンドラー関数を追加して、次のようなアクションを実行できます。

* 非標準または標準のエラー応答を使用するエラー応答を処理します。 これらの非標準的なエラー応答は、 [エラー応答の標準スキーマ](#failure-response-format).
* analytics イベントを任意の analytics プラットフォームに送信します。 例：Adobe Analytics.
* エラーメッセージが表示されるモーダルダイアログを表示します。

上記のアクションに加えて、カスタムエラーハンドラーを使用して、特定のユーザー要件を満たすカスタマイズされた関数を実行できます。

カスタムエラーハンドラーは、外部サービスから返されたエラーに応答し、カスタマイズされた応答をエンドユーザーに配信するように設計された関数（クライアントライブラリ）です。 注釈付きの任意のクライアントライブラリ `@errorHandler` は、カスタムエラーハンドラー関数と見なされます。 この注釈は、 `.js` ファイル。

を使用してカスタムエラーハンドラーを作成し、使用する方法を理解するには、次の手順を実行します。 [ルールエディターの Invoke サービス [ るーるえでぃたーの Invoke さーびす ]](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) 「 」アクションでは、2 つのフィールドを持つアダプティブフォームの例を見てみましょう。 **ペット ID** および **ペット名** を使用し、 **ペット ID** 外部サービスを呼び出すように設定された REST エンドポイントが返す様々なエラーを確認するフィールド。例えば、 `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

アダプティブフォームにカスタムエラーハンドラーを追加して使用するには、次の手順を実行します。

1. [カスタムエラーハンドラーを作成する](#create-custom-error-message)
1. [ルールエディターを使用してカスタムエラーハンドラーを設定する](#use-custom-error-handler)

#### 1.カスタムエラーハンドラーを作成する {#create-custom-error-message}

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
1. 変更を保存します。作成したフォルダー構造は次のようになります。

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

次に、AEM Formsのルールエディターの Invoke サービスを使用して、カスタムエラーハンドラーを設定して使用する方法を説明します。

#### 2.ルールエディターを使用して、カスタムエラーハンドラーを設定します {#use-custom-error-handler}

アダプティブフォームにカスタムエラーハンドラーを実装する前に、クライアントライブラリ名が **[!UICONTROL クライアントライブラリカテゴリ]** は、 `.content.xml` ファイル。

![アダプティブフォームコンテナ設定にクライアントライブラリの名前を追加する](/help/forms/using/assets/client-library-category-name-core-component.png)

この場合、クライアントライブラリ名は `customfunctionsdemo` （内） `.content.xml` ファイル。

カスタムエラーハンドラーを使用するには、 **[!UICONTROL ルールエディターの Invoke Service]** アクション：

1. アダプティブフォームをオーサリングモードで開き、フォームコンポーネントを選択して、 **[!UICONTROL ルールエディター]** をクリックして、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの&#x200B;**条件**&#x200B;セクションで条件を作成します。例えば、 **[ペット ID フィールドの名前]** が変更された場合は、「 **変更済み** から **状態を選択** 」ドロップダウンリストから選択できます。
1. 「**Then**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**サービスの呼び出し**」を選択します。
1. を選択します。 **ポストサービス** と、対応するデータバインディングが **入力** 」セクションに入力します。 例えば、検証する場合は、次のようにします。 **ペット ID**&#x200B;を選択し、 **ポストサービス** as **GET/pet/{petId}** を選択し、 **ペット ID** （内） **入力** 」セクションに入力します。
1. からデータ連結を選択します。 **出力** 」セクションに入力します。 例えば、「 **ペット名** （内） **出力** 」セクションに入力します。
1. 選択 **[!UICONTROL カスタムエラーハンドラー]** から **[!UICONTROL エラーハンドラー]** 」セクションに入力します。
1. 「**[!UICONTROL 完了]**」をクリックします。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/using/assets/custom-error-handler.png)

このルールの結果、 **ペット ID** 検証を確認 **ペット名** REST エンドポイントによって呼び出された外部サービスを使用する。 データソースに基づく検証条件が失敗した場合は、エラーメッセージがフィールドレベルで表示されます。

![エラー応答を処理するためのカスタムエラーハンドラーをフォームに追加します](/help/forms/using/assets/custom-error-handler-message-core-component.png)

ブラウザーコンソールを開き、REST サービスエンドポイントから受け取った応答とヘッダーで、検証エラーメッセージを確認します。

カスタムエラーハンドラー関数は、エラー応答に基づいて、モーダルダイアログの表示や Analytics イベントの送信など、追加のアクションを実行します。 カスタムエラーハンドラー関数を使用すると、特定のユーザー要件に合わせて柔軟にエラー処理をカスタマイズできます。

## 関連トピック {#see-also}

* [スタンドアロンのコアコンポーネントベースのアダプティブフォームを作成する](/help/forms/using/create-an-adaptive-form-core-components.md)
* [フォームのスタイルまたはテーマを作成する](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
* [AEM Sites ページへのアダプティブフォームの作成または追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)