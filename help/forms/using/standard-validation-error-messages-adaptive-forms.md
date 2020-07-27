---
title: アダプティブフォームの標準検証エラーメッセージ
seo-title: アダプティブフォームの標準検証エラーメッセージ
description: アダプティブフォームの検証エラーメッセージを、カスタムエラーハンドラーを使用して標準形式に変換
seo-description: アダプティブフォームの検証エラーメッセージを、カスタムエラーハンドラーを使用して標準形式に変換
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 9%

---


# アダプティブフォームの標準検証エラーメッセージ {#standard-validation-error-messages}

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 検証条件は、アダプティブフォーム内のフィールドに許容される入力値を参照します。 アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。 例えば、RESTful Webサービスをデータソースとして使用する場合、Swagger定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、値がデータソースに送信されます。 そうでない場合は、アダプティブフォームにエラーメッセージが表示されます。

この方法と同様に、アダプティブフォームはカスタムサービスと統合して、データの検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーから返される検証エラーメッセージが標準メッセージ形式の場合、エラーメッセージはフォームのフィールドレベルで表示されます。

入力値が検証条件を満たさず、サーバー検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームには、検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムが用意されています。 次の2つの方法のいずれかを使用して、エラーメッセージを標準の形式に変換できます。

* アダプティブフォーム送信時の追加カスタムエラーハンドラー
* ルールエディターを使用してサービス操作を呼び出す追加ためのカスタムハンドラー

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
* `errors` 検証条件に失敗したフィールドのSOM式と検証エラーメッセージについて言及する
* `originCode` 外部サービスから返されたエラーコードが含まれます。
* `originMessage` 外部サービスから返された生のエラーデータが含まれます。

## カスタムハンドラーを追加するためのアダプティブフォーム送信の設定 {#configure-adaptive-form-submission}

サーバー検証エラーメッセージが標準形式で表示されない場合は、非同期送信を有効にし、アダプティブフォームの送信時にカスタムエラーハンドラーを追加して、メッセージを標準形式に変換できます。

### Configure asynchronous adaptive form submission {#configure-asynchronous-adaptive-form-submission}

カスタムハンドラーを追加する前に、アダプティブフォームで非同期送信を設定する必要があります。 以下の手順を実行します。

1. In adaptive form authoring mode, select the Form Container object and tap ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. 送信前にサーバー上の入力フィールドの値を検証するには、 **[!UICONTROL 「サーバーで再検証]** 」を選択します。
1. 送信アクションを選択します。

   * 「 **[!UICONTROL Submit using Form Data Model]** 」を選択し、適切なデータモデルを選択します(データソースとしてRESTful Webサービスベースの [フォームデータモデルを使用している場合](work-with-form-data-model.md) )。
   * RESTful Webサービスをデータソースとして使用する場合は、 **[!UICONTROL 「RESTエンドポイントに]** 送信」を選択し **[!UICONTROL 、]**&#x200B;リダイレクトURL/パスを指定します。

   ![アダプティブフォーム送信プロパティ](assets/af_submission_properties.png)

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

### アダプティブフォーム送信時の追加カスタムエラーハンドラー {#add-custom-error-handler-af-submission}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。これらのハンドラーは、サーバーからの応答に従って実行されるクライアント側の関数です。フォームを送信すると、データが検証用としてサーバーに転送され、フォーム送信の成功イベントとエラーイベントに関する情報とともに、サーバーからクライアントに応答が返されます。この情報は、パラメーターとして関連するハンドラーに渡され、対応する関数が実行されます。

次の手順を実行して、アダプティブフォームの送信時にカスタムエラーハンドラーを追加します。

1. Open the adaptive form in authoring mode, select any form object, and tap <!--![Rule Editor](assets/af_edit_rules.png)--> to open the rule editor.
1. フォームオブジェクトツリーで「**[!UICONTROL フォーム]**」選択し、「**[!UICONTROL 作成]**」をタップします。
1. 「イベント」ドロップダウンリストから **[!UICONTROL 、「送信で]** エラーが発生しました」を選択します。
1. カスタムのエラー構造を標準のエラー構造に変換するルールを作成し、「 **[!UICONTROL 完了]** 」をタップしてルールを保存します。

次に、カスタムのエラー構造を標準のエラー構造に変換するためのサンプルコードを示します。

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

標準形式に変換するアダプティブフォームフィールドのSOM式を `var som_map` リストします。 フィールドをタップし、 **[!UICONTROL 表示SOM式を選択することで、アダプティブフォーム内の任意のフィールドのSOM式を表示できます]**。

アダプティブフォームは、このカスタムエラーハンドラーを使用して、に示すフィールドを標準エラーメッセージ形式 `var som_map` に変換します。 その結果、検証エラーメッセージはアダプティブフォームのフィールドレベルで表示されます。

## Invoke Serviceアクションを使用した追加カスタムハンドラー

次の手順を実行して、カスタムエラー構造を標準エラー構造に変換するエラーハンドラを追加します。このエラーハンドラは、 [ルールエディタの](rule-editor.md) 「Invoke Service」アクションを使用して実行します。

1. Open the adaptive form in authoring mode, select any form object, and tap ![Rule Editor](assets/rule_editor_icon.png) to open the rule editor.
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの「 **[!UICONTROL When]** 」セクションで条件を作成します。 例えば、フィールド[のWhenName] を変更するとします。 「選択」 **[!UICONTROL は]** 、「状態を **[!UICONTROL 選択]** 」ドロップダウンリストから変更され、この条件を満たすようになりました。
1. 「**[!UICONTROL Then]**」セクションの「**[!UICONTROL アクションの選択]**」ドロップダウンリストで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. 「 **[!UICONTROL Input]** 」セクションからPostサービスとそれに対応するデータ連結を選択します。 例えば、アダプティブフォームの **名前**、 **ID**、 **ステータスフィールドを検証する場合は、投稿サービス(pet)を選択し、pet name、pet.id、pet.statusの各セクションを選択し****** ます。

このルールの結果、 **名前**、 **ID**、 **** ステータスフィールドに入力した値は、手順2で定義したフィールドが変更され、フォームのフィールド外にタブ移動した直後に検証されます。

1. Select **[!UICONTROL Code Editor]** from the mode selection drop-down list.
1. 「コード **[!UICONTROL を編集]**」をタップします。
1. 既存のコードから次の行を削除します。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. カスタムのエラー構造を標準のエラー構造に変換するルールを作成し、「 **[!UICONTROL 完了]** 」をタップしてルールを保存します。
例えば、カスタムエラー構造を標準エラー構造に変換するために、最後に次のサンプルコードを追加します。

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

   標準形式に変換するアダプティブフォームフィールドのSOM式を `var som_map` リストします。 フィールドをタップし、 **[!UICONTROL その他のオプション]** (...)メニューから「 **[!UICONTROL 表示SOM式]** 」を選択すると、アダプティブフォーム内の任意のフィールドのSOM式を表示できます。

   次のサンプルコード行をカスタムエラーハンドラーにコピーしてください。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation APIには、新しいカスタムエラーハンドラーに基づ `null` くパラメーターと `errorHandler` パラメーターが含まれます。

   アダプティブフォームは、このカスタムエラーハンドラーを使用して、に示すフィールドを標準エラーメッセージ形式 `var som_map` に変換します。 その結果、検証エラーメッセージはアダプティブフォームのフィールドレベルで表示されます。