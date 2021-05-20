---
title: HTML5 フォームの Form Bridge API
seo-title: HTML5 フォームの Form Bridge API
description: 外部アプリケーションは FormBridge API を使用して XFA Mobile Form に接続します。API は親ウィンドウで FormBridgeInitialized イベントを送出します。
seo-description: 外部アプリケーションは FormBridge API を使用して XFA Mobile Form に接続します。API は親ウィンドウで FormBridgeInitialized イベントを送出します。
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 42%

---

# HTML5 フォームの Form Bridge API  {#form-bridge-apis-for-html-forms}

Form Bridge APIを使用して、XFAベースのHTML5フォームとお使いのアプリケーションの間の通信チャネルを開くことができます。 Form Bridge APIには、接続を作成する&#x200B;**connect** APIが用意されています。

**接続** API はハンドラーを引数として受け入れます。XFAベースのHTML5フォームとForm Bridge間の接続が正常に作成されると、ハンドルが呼び出されます。

次のサンプルコードを使用して接続を作成できます。

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>必ず接続を作成してから formRuntime.jsp ファイルを追加してください。

## 利用可能な Form Bridge API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

スクリプティングライブラリのバージョン番号を返す

* **入力**：なし
* **出力**:スクリプトライブラリのバージョン番号
* **エラー**：なし

**isConnected()** フォーム状態が初期化されたかどうかを確認します

* **入力**：なし
* **出力**: **** Trueif the XFA Form State has been initialized

* **エラー**：なし

**connect(handler, context)**  FormBridgeに接続し、接続が確立されてフォーム状態が初期化された後に関数を実行します

* **必要情報**:

   * **handler**：Form Bridge が接続された後に実行する関数
   * **コンテキスト**:handler関数のコンテキスト(this)を設定するオ ** ブジェクト。

* **出力**：なし
* **エラー**：なし

**getDataXML(options)** 現在のフォームデータをXML形式で返します

* **必要情報:**

   * **options：**&#x200B;次のプロパティが含まれている JavaScript オブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数。 この関数には *data* プロパティに XML が含まれているオブジェクトが渡されます。
      * **context**：*success*&#x200B;関数のコンテキスト（this）の設定対象オブジェクト
      * **validationChecker**:サーバーから受信した検証エラーを確認するための呼び出し関数。検証関数にはエラー文字列の配列が渡されます。
      * **formState**:データXMLを返す必要があるXFAフォームのJSON状態。指定されていない場合、現在のレンダリングされているフォームの XML のデータ。

* **出力：**&#x200B;なし
* **エラー**：なし

**registerConfig(configName, config)** ユーザー/ポータル固有の設定をFormBridgeに登録します。これらの設定はデフォルト設定をオーバーライドします。サポートされている設定は config セクションで指定されています。

* **必要情報:**

   * **configName:** オーバーライドする設定の名前

      * **widgetConfig:** ユーザーがフォーム内のデフォルトウィジェットをカスタムウィジェットで上書きできるようにします。設定は次のようにオーバーライドされます。

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 最初のページのみをレンダリングするというデフォルトの動作を上書きできるようにします。設定は次のようにオーバーライドされます。

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** ユーザーがログのレベル、カテゴリのログの無効化、ログコンソールを表示するかサーバーに送信するかを上書きできるようにします。設定は次のようにオーバーライドできます。

      ```javascript
      formBridge.registerConfig{
        "LoggerConfig" : {
      {
      "on":`<true *| *false>`,
      "category":`<array of categories>`,
      "level":`<level of categories>`, "
      type":`<"console"/"server"/"both">`
      }
        }
      ```

      * **SubmitServiceProxyConfig:** ユーザーが送信を登録し、プロキシサービスをロガーできるようにします。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config：**&#x200B;設定の値



* **出力：***data* プロパティに設定の元の値が含まれているオブジェクト。

* **エラー**：なし

**hideFields(fieldArray)**  fieldArrayでSOM式が提供されるフィールドを非表示にします。指定フィールドの presence プロパティを invisible に設定します

* **必要情報:**

   * **fieldArray:** 非表示にするフィールドのSOM式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**showFields(fieldArray)**  fieldArrayにSOM式が提供されるフィールドを表示します。提供されたフィールドの presence プロパティを visible に設定します

* **必要情報:**

   * **fieldArray:** 表示するフィールドのSOM式の配列

* **出力：**&#x200B;なし
* **エラー**：なし

**hideSubmitButtons()** フォーム内のすべての送信ボタンを非表示にします

* **入力**：なし
* **出力**：なし
* **エラー**：フォーム状態が初期化されていない場合、例外をスローする

**getFormState()** フォームの状態を表すJSONを返す

* **入力：**&#x200B;なし
* **出力：** datapropertyに現在のフォーム状態を表すJSONが格納されているオ ** ブジェクト。

* **エラー**：なし

**restoreFormState(options)** optionsオブジェクトで指定されたJSON状態からフォーム状態を復元します。状態が適用され、操作の完了後にサクセスまたはエラーハンドラーが呼び出されます。

* **必要情報:**

   * **オプション：** 次のプロパティを含むJavaScriptオブジェクト。

      * **error**：エラーハンドラー関数
      * **success**：サクセスハンドラー関数
      * **コンテキスト**:success関数のコンテキスト(this)を設定する ** オブジェクト
      * **formState**: フォームの JSON ステート。フォームがJSON状態に復元されます。

* **出力：**&#x200B;なし
* **エラー**：なし

**setFocus (som)**  SOM式で指定されたフィールドにフォーカスを置く

* **入力：** フォーカスを設定するフィールドのSOM式
* **出力：**&#x200B;なし
* **エラー：** SOM 式が間違っている場合、例外をスローする

**setFieldValue (som, value)** 指定されたSOM式のフィールドの値を設定

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列。フィールドの値を設定するSOM式。
   * **値：** som配列で提供されたSOM式に対応する値が含ま ****&#x200B;れる配列。値のデータ型がfieldTypeと同じでない場合、値は変更されません。

* **出力：**&#x200B;なし
* **エラー：** SOM式が正しくない場合に例外をスローする

**getFieldValue (som)** 指定されたSOM式のフィールドの値を返す

* **入力：** 値を取得する必要があるフィールドのSOM式を含む配列
* **出力：** 結果が配列としてdatapropertyに含まれるオブジ **** ェクト。

* **エラー**：なし

### getFieldValue() API の例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** SOM式で指定されたフィールドの指定されたプロパティの値のリストを取得

* **必要情報:**

   * **som：**&#x200B;フィールドの SOM 式が含まれている配列
   * **property：**&#x200B;値が要求されるプロパティの名前

* **出力：** 結果が配列としてdatapropertyに含まれるオブジ ** ェクト

* **エラー**：なし

**setFieldProperties(som, property, values)** SOM式で指定されたすべてのフィールドに対して、指定されたプロパティの値を設定します

* **必要情報:**

   * **som:** 値を設定する必要があるフィールドのSOM式が含まれている配列
   * **property：**&#x200B;値の設定が要求されるプロパティ
   * **値：** SOM式で指定されたフィールドの提供されたプロパティの値を含む配列

* **出力：**&#x200B;なし
* **エラー**：なし

## Form Bridge API の使用例 {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
