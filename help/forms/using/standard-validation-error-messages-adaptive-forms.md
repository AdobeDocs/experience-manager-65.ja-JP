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
feature: アダプティブフォーム
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 10%

---

# アダプティブフォームの標準検証エラーメッセージ{#standard-validation-error-messages}

アダプティブフォームは、事前設定された検証条件に基づいて、フィールドに入力した入力を検証します。 検証条件は、アダプティブフォーム内のフィールドに許容される入力値を指します。 アダプティブフォームで使用するデータソースに基づいて検証条件を設定できます。 例えば、RESTful Webサービスをデータソースとして使用する場合、Swagger定義ファイルで検証条件を定義できます。

入力値が検証条件を満たす場合、値がデータソースに送信されます。 それ以外の場合は、エラーメッセージがアダプティブフォームに表示されます。

この方法と同様に、アダプティブフォームをカスタムサービスと統合して、データ検証を実行できるようになりました。 入力値が検証条件を満たさず、サーバーが返す検証エラーメッセージが標準メッセージ形式の場合、エラーメッセージはフォームのフィールドレベルに表示されます。

入力値が検証条件を満たさず、サーバーの検証エラーメッセージが標準メッセージ形式でない場合、アダプティブフォームは検証エラーメッセージを標準形式に変換し、フォームのフィールドレベルで表示するメカニズムを提供します。 次の2つの方法のいずれかを使用して、エラーメッセージを標準形式に変換できます。

* アダプティブフォーム送信時にカスタムエラーハンドラーを追加する
* ルールエディターを使用して、「Invoke Service」アクションにカスタムハンドラーを追加する

この記事では、検証エラーメッセージの標準形式と、エラーメッセージをカスタム形式から標準形式に変換する手順について説明します。

## 標準検証エラーメッセージ形式{#standard-validation-message-format}

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
* `errors` 検証条件に失敗したフィールドのSOM式と検証エラーメッセージを指定する
* `originCode` 外部サービスから返されるエラーコードが含まれます。
* `originMessage` 外部サービスから返される生のエラーデータが含まれます

## カスタムハンドラー{#configure-adaptive-form-submission}を追加するためのアダプティブフォームの送信設定

サーバー検証エラーメッセージが標準形式で表示されない場合は、非同期送信を有効にし、アダプティブフォーム送信時にカスタムエラーハンドラーを追加して、メッセージを標準形式に変換できます。

### 非同期アダプティブフォーム送信の設定{#configure-asynchronous-adaptive-form-submission}

カスタムハンドラーを追加する前に、非同期送信用にアダプティブフォームを設定する必要があります。 以下の手順を実行します。

1. アダプティブフォームのオーサリングモードで、フォームコンテナオブジェクトを選択し、![アダプティブフォームのプロパティ](assets/configure_icon.png)をタップしてプロパティを開きます。
1. 「**[!UICONTROL 送信]**」プロパティセクションで、「**[!UICONTROL 非同期送信を使用]**」を有効にします。
1. 「**[!UICONTROL サーバーで再検証]**」を選択して、送信前にサーバー上の入力フィールド値を検証します。
1. 送信アクションを選択します。

   * **[!UICONTROL フォームデータモデル]**&#x200B;を使用して送信を選択し、適切なデータモデルを選択します（データソースとして[フォームデータモデル](work-with-form-data-model.md)をベースとするRESTful Webサービスを使用する場合）。
   * **[!UICONTROL Submit to REST endpoint]**&#x200B;を選択し、データソースとしてRESTful Webサービスを使用する場合は、**[!UICONTROL Redirect URL/Path]**&#x200B;を指定します。

   ![アダプティブフォーム送信プロパティ](assets/af_submission_properties.png)

1. 「![保存](assets/save_icon.png)」をタップして、プロパティを保存します。

### アダプティブフォーム送信時のカスタムエラーハンドラーの追加{#add-custom-error-handler-af-submission}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。フォームが送信されると、データが検証のためにサーバーに転送され、送信の成功またはエラーイベントに関する情報と共に、応答がクライアントに返されます。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。

次の手順を実行して、アダプティブフォーム送信時にカスタムエラーハンドラーを追加します。

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択してから、<!--![Rule Editor](assets/af_edit_rules.png)-->をタップしてルールエディターを開きます。
1. フォームオブジェクトツリーで「**[!UICONTROL フォーム]**」選択し、「**[!UICONTROL 作成]**」をタップします。
1. 「イベント」ドロップダウンリストから「送信中のエラー&#x200B;**[!UICONTROL 」を選択します。]**
1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「**[!UICONTROL 完了]**」をタップしてルールを保存します。

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

`var som_map`には、標準形式に変換するアダプティブフォームフィールドのSOM式が一覧表示されます。 アダプティブフォーム内の任意のフィールドのSOM式を表示するには、フィールドをタップして「**[!UICONTROL SOM式を表示]**」を選択します。

アダプティブフォームは、このカスタムエラーハンドラーを使用して、`var som_map`に示すフィールドを標準のエラーメッセージ形式に変換します。 その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルで表示されます。

## 「サービスを呼び出し」アクションを使用したカスタムハンドラーの追加

次の手順を実行して、カスタムエラー構造を標準エラー構造に変換し、[ルールエディターの「サービスを呼び出し」アクションを使用します。](rule-editor.md)

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択して、「![ルールエディター](assets/rule_editor_icon.png)」をタップし、ルールエディターを開きます。
1. 「**[!UICONTROL 作成]**」をタップします。
1. ルールの&#x200B;**[!UICONTROL When]**&#x200B;セクションに条件を作成します。 例えば、When[Name of field]が変更されたとします。 この条件を満たすには、**[!UICONTROL 状態を選択]**&#x200B;ドロップダウンリストから「**[!UICONTROL 変更]**」を選択します。
1. 「**[!UICONTROL Then]**」セクションの「**[!UICONTROL アクションの選択]**」ドロップダウンリストで「**[!UICONTROL サービスの呼び出し]**」を選択します。
1. **[!UICONTROL Input]**&#x200B;セクションから、Postサービスと対応するデータバインディングを選択します。 例えば、アダプティブフォームの&#x200B;**名前**、**ID**、**ステータス**&#x200B;フィールドを検証する場合は、ポストサービス(pet)を選択し、**[!UICONTROL 入力]**&#x200B;セクションでpet.name、pet.idおよびpet.statusを選択します。

このルールの結果、**名前**、**ID**、**ステータス**&#x200B;の各フィールドに入力した値は、手順2で定義したフィールドが変更され、フォームのフィールドからタブを離すとすぐに検証されます。

1. 「モード選択」ドロップダウンリストから「**[!UICONTROL コードエディター]**」を選択します。
1. 「**[!UICONTROL コードを編集]**」をタップします。
1. 既存のコードから次の行を削除します。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. カスタムエラー構造を標準エラー構造に変換するルールを作成し、「**[!UICONTROL 完了]**」をタップしてルールを保存します。
例えば、カスタムエラー構造を標準エラー構造に変換するために、末尾に次のサンプルコードを追加します。

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

   `var som_map`には、標準形式に変換するアダプティブフォームフィールドのSOM式が一覧表示されます。 アダプティブフォーム内の任意のフィールドのSOM式を表示するには、フィールドをタップし、**[!UICONTROL その他のオプション]**(...)メニューから「**[!UICONTROL SOM式]**&#x200B;を表示」を選択します。

   次のサンプルコード行をカスタムエラーハンドラーにコピーしてください。

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   executeOperation APIには、新しいカスタムエラーハンドラーに基づく`null`パラメーターと`errorHandler`パラメーターが含まれます。

   アダプティブフォームは、このカスタムエラーハンドラーを使用して、`var som_map`に示すフィールドを標準のエラーメッセージ形式に変換します。 その結果、検証エラーメッセージは、アダプティブフォームのフィールドレベルで表示されます。
