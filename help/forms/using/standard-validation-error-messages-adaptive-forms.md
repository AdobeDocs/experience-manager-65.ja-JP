---
title: アダプティブフォームの標準検証エラーメッセージ
seo-title: アダプティブフォームの標準検証エラーメッセージ
description: カスタムエラーハンドラーを使用して、アダプティブフォームの検証エラーメッセージを標準形式に変換する
seo-description: カスタムエラーハンドラーを使用して、アダプティブフォームの検証エラーメッセージを標準形式に変換する
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
translation-type: tm+mt
source-git-commit: 48cd21915017da96015df4e7619611ebf775c5fb

---


# アダプティブフォームの標準検証エラーメッセージ {#standard-validation-error-messages}

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 検証条件は、アダプティブフォーム内のフィールドに対して許容される入力値を参照します。 検証条件は、アダプティブフォームで使用するデータソースに基づいて設定できます。 例えば、RESTful webサービスをデータソースとして使用する場合、Swagger定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、値はデータソースに送信されます。 そうでない場合は、アダプティブフォームにエラーメッセージが表示されます。

このアプローチと同様に、アダプティブフォームはカスタムサービスと統合して、データ検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーが返す検証エラーメッセージが標準メッセージ形式の場合、エラーメッセージはフォームのフィールドレベルで表示されます。

入力値が検証条件を満たさず、サーバー検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームは検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムを提供します。 次の2つの方法のいずれかを使用して、エラーメッセージを標準形式に変換できます。

* アダプティブフォーム送信時のカスタムエラーハンドラの追加
* ルールエディターを使用して、「サービスを呼び出し」アクションにカスタムハンドラーを追加します

この記事では、検証エラーメッセージの標準形式と、エラーメッセージをカスタム形式から標準形式に変換する手順について説明します。

## 標準検証エラーメッセージの形式 {#standard-validation-message-format}

サーバー検証エラーメッセージが次の標準形式の場合、アダプティブフォームはフィールドレベルでエラーを表示します。

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

ここで、

* `errorCausedBy` 失敗の理由を説明する
* `errors` 検証エラーメッセージと共に、検証条件に合わなかったフィールドのSOM式に言及する
* `originCode` 外部サービスから返されたエラーコードが含まれます。
* `originMessage` 外部サービスから返された生のエラーデータが含まれます。

## カスタムハンドラーを追加するアダプティブフォーム送信の設定 {#configure-adaptive-form-submission}

サーバー検証エラーメッセージが標準形式で表示されない場合は、非同期送信を有効にし、アダプティブフォーム送信にカスタムエラーハンドラーを追加して、メッセージを標準形式に変換できます。

### 非同期アダプティブフォーム送信の設定 {#configure-asynchronous-adaptive-form-submission}

カスタムハンドラーを追加する前に、アダプティブフォームの非同期送信を設定する必要があります。 次の手順を実行します。

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. 送信前 **[!UICONTROL にサーバー上の入力フィールドの値を検証する場合は]** 、「サーバーで再検証」を選択します。
1. 送信アクションを選択します。

   * RESTful webサー **[!UICONTROL ビスベースのフォームデータモデルをデータソースとして使用する場合は、「]** Submit using Form Data Model [](work-with-form-data-model.md) 」を選択し、適切なデータモデルを選択します。
   * RESTful webサービ **[!UICONTROL スをデータソースとして使用する場合は]** 、「RESTエンドポイントに送信」を選択し、リダイレクトURL ****/パスを指定します。
   ![アダプティブフォーム送信プロパティ](assets/af_submission_properties.png)

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

### アダプティブフォーム送信時のカスタムエラーハンドラの追加 {#add-custom-error-handler-af-submission}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。これらのハンドラーは、サーバーからの応答に従って実行されるクライアント側の関数です。フォームを送信すると、データが検証用としてサーバーに転送され、フォーム送信の成功イベントとエラーイベントに関する情報とともに、サーバーからクライアントに応答が返されます。この情報は、パラメーターとして関連するハンドラーに渡され、対応する関数が実行されます。

次の手順を実行して、アダプティブフォームの送信時にカスタムエラーハンドラーを追加します。

1. Open the adaptive form in authoring mode, select any form object, and tap <!--![Rule Editor](assets/af_edit_rules.png)--> to open the rule editor.
1. フォームオブジェクトツリーで「**[!UICONTROL フォーム]**」選択し、「**[!UICONTROL 作成]**」をタップします。
1. 「イベ **[!UICONTROL ント」ドロップダウンリストから]** 、「送信でエラー」を選択します。
1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「完了」を **[!UICONTROL タップして]** 、ルールを保存します。

次に、カスタムエラー構造を標準エラー構造に変換するサンプルコードを示します。

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

に、標 `var som_map` 準形式に変換するアダプティブフォームフィールドのSOM式を示します。 アダプティブフォーム内の任意のフィールドのSOM式を表示するには、フィールドをタップし、「 **[!UICONTROL SOM式を表示」を選択します]**。

アダプティブフォームは、このカスタムエラーハンドラーを使用して、に示すフィールドを標準エラーメ `var som_map` ッセージ形式に変換します。 その結果、検証エラーメッセージはアダプティブフォームのフィールドレベルで表示されます。

## 「サービスを呼び出し」アクションを使用したカスタムハンドラーの追加

次の手順を実行して、ルールエディターの [](rule-editor.md) Invoke Serviceアクションを使用して、カスタムエラー構造を標準エラー構造に変換するエラーハンドラーを追加します。

1. Open the adaptive form in authoring mode, select any form object, and tap ![Rule Editor](assets/rule_editor_icon.png) to open the rule editor.
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの「 **[!UICONTROL When]** 」セクションに条件を作成します。 例えば、フィー[ルドのWhenNameは] 、変更されます。 「選択 **[!UICONTROL 」は]** 、「状態 **[!UICONTROL を選択]** 」ドロップダウンリストから変更され、この条件を満たします。
1. In the **[!UICONTROL Then]** section, select **[!UICONTROL Invoke Service]** from the **[!UICONTROL Select Action]** drop-down list.
1. 「 **[!UICONTROL Input]** 」セクションからPostサービスと対応するデータ連結を選択します。 例えば、アダプティブフォームの **Name**、 **ID**、 **Status****** の各フィールドを検証する場合は、Postサービス(pet)を選択し、InputInputセクションでpet name、pet.id、pet.statusを選択します。

このルールの結果、手順2で定義したフィールドが変更され、 **Name**、 **ID**、 **Status** の各フィールドに入力した値が検証されると、フォーム内のフィールドからTabキーで移動します。

1. Select **[!UICONTROL Code Editor]** from the mode selection drop-down list.
1. 「コード **[!UICONTROL の編集」をタップしま]**&#x200B;す。
1. 既存のコードから次の行を削除します。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「完了」を **[!UICONTROL タップして]** 、ルールを保存します。
例えば、カスタムエラー構造を標準エラー構造に変換するには、次のサンプルコードを末尾に追加します。

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   に、標 `var som_map` 準形式に変換するアダプティブフォームフィールドのSOM式を示します。 アダプティブフォーム内の任意のフィールドのSOM式を表示するには、フィールドをタップし、その他のオプション **[!UICONTROL (...)メニューから「]** SOM式を表示 **** 」を選択します。

   必ず、サンプルコードの次の行をカスタムエラーハンドラーにコピーしてください。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation APIには、新しいカスタムエラ `null` ーハン `errorHandler` ドラーに基づくパラメーターとパラメーターが含まれます。

   アダプティブフォームは、このカスタムエラーハンドラーを使用して、に示すフィールドを標準エラーメ `var som_map` ッセージ形式に変換します。 その結果、検証エラーメッセージはアダプティブフォームのフィールドレベルで表示されます。