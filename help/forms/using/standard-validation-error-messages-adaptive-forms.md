---
title: アダプティブフォームの標準検証エラーメッセージ
seo-title: Standard validation error messages for adaptive forms
description: カスタムエラーハンドラーを使用して、アダプティブフォームの検証エラーメッセージを標準形式に変換する
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1108'
ht-degree: 100%

---

# アダプティブフォームの標準検証エラーメッセージ {#standard-validation-error-messages}

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 検証条件は、アダプティブフォーム内のフィールドに指定できる入力値を指します。 アダプティブフォームで使用するデータソースに基づいて、検証条件を設定できます。 例えば、RESTful web サービスをデータソースとして使用する場合、Swagger 定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、値がデータソースに送信されます。 それ以外の場合は、アダプティブフォームにエラーメッセージが表示されます。

この方法と同様に、アダプティブフォームをカスタムサービスと統合して、データ検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーが返す検証エラーメッセージが標準メッセージ形式の場合、エラーメッセージはフォームのフィールドレベルに表示されます。

入力値が検証条件を満たさず、サーバーの検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームは検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムを提供します。 次の 2 つの方法のいずれかを使用して、エラーメッセージを標準形式に変換できます。

* アダプティブフォーム送信時にカスタムエラーハンドラーを追加する
* ルールエディターを使用して「サービスの呼び出しアクション」にカスタムハンドラーを追加する

この記事では、検証エラーメッセージの標準形式と、エラーメッセージをカスタム形式から標準形式に変換する手順について説明します。

## 標準検証エラーメッセージ形式 {#standard-validation-message-format}

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

* `errorCausedBy` は失敗の理由を説明します
* `errors` は、検証条件に失敗したフィールドの SOM 式と検証エラーメッセージに言及します
* `originCode` には外部サービスから返されたエラーコードが含まれます
* `originMessage` には外部サービスから返された生のエラーデータが含まれます

## カスタムハンドラーを追加するためのアダプティブフォームの送信設定 {#configure-adaptive-form-submission}

サーバーの検証エラーメッセージが標準形式で表示されない場合は、非同期送信を有効にし、アダプティブフォーム送信にカスタムエラーハンドラーを追加して、メッセージを標準形式に変換できます。

### アダプティブフォームの非同期送信設定 {#configure-asynchronous-adaptive-form-submission}

カスタムハンドラーを追加する前に、非同期送信用にアダプティブフォームを設定する必要があります。 以下の手順を実行します。

1. アダプティブフォームのオーサリングモードでフォームコンテナーオブジェクトを選択し、![アダプティブフォームのプロパティ](assets/configure_icon.png)をタップしてプロパティを開きます。
1. **[!UICONTROL 送信]**&#x200B;プロパティセクションで、**[!UICONTROL 非同期送信を使用]**&#x200B;を有効にします。
1. **[!UICONTROL サーバーで再検証]**&#x200B;を選択して、送信前にサーバー上で入力フィールド値を検証してください。
1. 送信アクションを選択します。

   * データソースとして RESTful web サービスベースの[フォームデータモデル](work-with-form-data-model.md)を使用している場合、**[!UICONTROL フォームデータモデルを使用して送信]**&#x200B;を選択し、適切なデータモデルを選択してください。
   * データソースとして RESTful web サービスを使用している場合は、**[!UICONTROL REST エンドポイントに送信]**&#x200B;を選択し、**[!UICONTROL リダイレクト URL／パス]**&#x200B;を指定してください。

   ![アダプティブフォーム送信プロパティ](assets/af_submission_properties.png)

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

### アダプティブフォーム送信時にカスタムエラーハンドラーを追加する {#add-custom-error-handler-af-submission}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。フォームが送信されると、データが検証のためにサーバーに転送され、送信の成功またはエラーイベントに関する情報と共に、応答がクライアントに返されます。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。

アダプティブフォームの送信時にカスタムエラーハンドラーを追加するには、以下の手順を実行してください。

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択して <!--![Rule Editor](assets/af_edit_rules.png)--> をタップしてください。この操作により、ルールエディターが起動します。
1. フォームオブジェクトツリーで&#x200B;**[!UICONTROL フォーム]**&#x200B;選択し、**[!UICONTROL 作成]**&#x200B;をタップしてください。
1. イベントドロップダウンリストから&#x200B;**[!UICONTROL 送信中のエラー]**&#x200B;を選択します。
1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「**[!UICONTROL 完了]**」をタップしてルールを保存してください。

カスタムエラー構造を標準エラー構造に変換するサンプルコードを以下に示します。

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

`var som_map` には、標準形式に変換するアダプティブフォームフィールドの SOM 式が一覧表示されます。アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップして、**[!UICONTROL SOM 式を表示]**&#x200B;を選択してください。

アダプティブフォームは、このカスタムエラーハンドラーを使用して、`var som_map` に一覧表示されたフィールドを標準のエラーメッセージ形式に変更します。 その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルに表示されます。

## サービスの呼び出しアクションを使用してカスタムハンドラーを追加する

次の手順を実行して、エラーハンドラーを追加し、[ルールエディター](rule-editor.md)のサービスの呼び出しアクションを使用してカスタムエラー構造を標準エラー構造に変換してください。

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択してから、![ルールエディター](assets/rule_editor_icon.png)をタップしてルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの&#x200B;**[!UICONTROL 条件]**&#x200B;セクションで条件を作成します。例えば、[フィールド名]が変更された場合という条件が考えられます。**[!UICONTROL 状態の選択]**&#x200B;ドロップダウンリストから「**[!UICONTROL 変更済み]**」を選択し、この条件を設定します。
1. 「**[!UICONTROL Then]**」セクションの&#x200B;**[!UICONTROL アクションの選択]**&#x200B;ドロップダウンリストで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. 「**[!UICONTROL 入力]**」セクションから、Post サービスとそれに対応するデータ連結を選択します。例えば、アダプティブフォームの&#x200B;**名前**、**ID** および&#x200B;**ステータス**&#x200B;の各フィールドを検証する場合は、「**[!UICONTROL 入力]**」セクションで Post サービス（pet）を選択し、pet.name、pet.id および pet.status を選択します。

このルールの結果、手順 2 で定義したフィールドを変更し、フォームのこのフィールドからタブを移動すると、**名前**、**ID** および **ステータス**&#x200B;の各フィールドに入力した値が検証されます。

1. モード選択ドロップダウンリストで「**[!UICONTROL コードエディター]**」を選択します。
1. 「**[!UICONTROL コードを編集]**」をタップします。
1. 既存のコードから次の行を削除します。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「**[!UICONTROL 完了]**」をタップしてルールを保存します。
例えば、カスタムエラー構造を標準エラー構造に変換するには、末尾に次のサンプルコードを追加します。

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

   `var som_map` には、標準形式に変換するアダプティブフォームフィールドの SOM 式をリストします。アダプティブフォーム内の任意のフィールドの SOM 式を表示するには、フィールドをタップして、**[!UICONTROL その他のオプション]**（...）メニューから「**[!UICONTROL SOM 式を表示]**」を選択します。

   次のサンプルコード行をカスタムエラーハンドラーにコピーしてください。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation API は、`null` パラメーターと、新しいカスタムエラーハンドラーに基づく `errorHandler` パラメーターを含みます。

   アダプティブフォームは、このカスタムエラーハンドラーを使用して、`var som_map` にリストしたフィールドを標準のエラーメッセージ形式に変更します。その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルに表示されます。
