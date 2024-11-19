---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Forms は、ユーザーがルールエディター内で独自の関数を作成および使用できるカスタム関数をサポートしています。
keywords: カスタム関数の追加, カスタム関数の使用, カスタム関数の作成, ルールエディターでのカスタム関数の使用.
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: ht
source-wordcount: '3385'
ht-degree: 100%

---

# アダプティブフォームのコアコンポーネントのカスタム関数

この記事では、次のような最新機能を備えた最新のアダプティブフォームのコアコンポーネントを使用してカスタム関数を作成する方法について説明します。

* カスタム関数のキャッシュ機能
* カスタム関数のグローバルスコープオブジェクトとフィールドオブジェクトのサポート
* let 関数や arrow 関数などの最新の JavaScript 機能のサポート（ES10 サポート）

カスタム関数の最新機能を使用するには、AEM Forms コアコンポーネント環境で[最新のフォームバージョン](https://github.com/adobe/aem-core-forms-components/tree/release/650)を設定する必要があります。</span>


| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | この記事 |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## はじめに

AEM Forms 6.5 には、ルールエディターを使用して複雑なビジネスルールを定義できる JavaScript 関数が含まれています。AEM Forms には標準の様々なカスタム関数が用意されていますが、多くのユースケースでは、複数のフォームで使用するのに独自のカスタム関数を定義する必要があります。これらのカスタム関数は、特定の要件を満たすことのにエントリ済みデータの操作と処理を有効にすることで、フォームの機能を強化します。また、定義済みの条件に基づいてフォームの動作を動的に変更することもできます。

### カスタム関数の使用 {#uses-of-custom-function}

アダプティブフォームのコアコンポーネントでカスタム関数を使用すると、次のようなメリットがあります。


* **データの管理**：カスタム関数は、フォームフィールドに対するエントリ済みデータを管理および処理します。
* **データの処理**：カスタム関数は、フォームフィールドに対するエントリ済みデータの処理に役立ちます。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的な動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。例えば、フィールドの表示／非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して、外部 API またはサービスと統合できます。外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

カスタム関数は、基本的に JavaScript ファイルに追加されるクライアントライブラリです。カスタム関数を作成すると、ルールエディターで使用でき、アダプティブフォームのユーザーが選択できるようになります。カスタム関数は、ルールエディターの JavaScript 注釈によって識別されます。

### カスタム関数でサポートされる JavaScript 注釈 {#js-annotations}

**JavaScript 注釈は、JavaScript コードのメタデータを提供します**。`/**` や `@` などの特定の記号で始まるコメントが含まれます。注釈は、コード内の関数、変数、その他の要素に関する重要な情報を提供します。アダプティブフォームは、カスタム関数に対して次の JavaScript 注釈をサポートしています。

#### 名前

**名前**&#x200B;は、アダプティブフォームのルールエディターでカスタム関数を識別するのに使用されます。カスタム関数に名前を付けるには、次の構文を使用します。

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` は関数の名前です。スペースは使用できません。
>`<Function Name>` アダプティブフォームのルールエディターでの関数の表示名です。
>関数名が関数自体の名前と同じ場合は、構文から `[functionName]` を省略できます。

#### パラメーター

**パラメーター**&#x200B;は、カスタム関数で使用される引数のリストです。関数は複数のパラメーターをサポートできます。カスタム関数のパラメーターを定義するには、次の構文を使用します。

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` は、パラメータータイプを表します。許可されているパラメータータイプは、以下のとおりです。

   * string：単一の文字列値を表します。
   * number：単一の数値を表します。
   * boolean：単一のブール値（true または false）を表します。
   * string[]：文字列値の配列を表します。
   * number[]：数値の配列を表します。
   * boolean[]：ブール値の配列を表します。
   * date：単一の日付値を表します。
   * date[]：日付値の配列を表します。
   * array：様々なタイプの値を含む汎用の配列を表します。
   * object：値を直接渡す代わりに、カスタム関数に渡されるフォームオブジェクトを表します。
   * scope：globals オブジェクトを表します。このオブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。これは JavaScript 注釈の最後のパラメーターとして宣言され、アダプティブフォームのルールエディターには表示されません。scope パラメーターは、フォームまたはコンポーネントのオブジェクトにアクセスして、フォームの処理に必要なルールまたはイベントをトリガーします。Globals オブジェクトとその使用方法について詳しくは、[こちらをクリック](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)してください。

パラメータータイプでは&#x200B;**大文字と小文字が区別されず**、パラメーター名にスペースは使用できません。

`<Parameter Description>` には、パラメーターの目的に関する詳細が含まれます。複数の単語を含めることができます。

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### 戻り値のタイプ

戻り値のタイプは、カスタム関数が実行後に返す値のタイプを指定します。カスタム関数の戻り値のタイプを定義するには、次の構文を使用します。

* `@return {type}`
* `@returns {type}`
  `{type}` は、関数の戻り値のタイプを表します。許可されている戻り値のタイプは、以下のとおりです。
* string：単一の文字列値を表します。
* number：単一の数値を表します。
* boolean：単一のブール値（true または false）を表します。
* string[]：文字列値の配列を表します。
* number[]：数値の配列を表します。
* boolean[]：ブール値の配列を表します。
* date：単一の日付値を表します。
* date[]：日付値の配列を表します。
* array：様々なタイプの値を含む汎用の配列を表します。
* object：値を直接表す代わりに、フォームオブジェクトを表します。

戻り値のタイプでは、大文字と小文字は区別されません。

#### プライベート

プライベートとして宣言されたカスタム関数は、アダプティブフォームのルールエディターのカスタム関数のリストに表示されません。デフォルトでは、カスタム関数はパブリックです。カスタム関数をプライベートとして宣言する構文は `@private` です。

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```
-->

## カスタム関数を作成する際のガイドライン {#considerations}

ルールエディターでカスタム関数をリストするには、次のいずれかの形式を使用できます。

### jsdoc コメントを含むまたは含まない関数ステートメント

jsdoc コメントを含むまたは含まないカスタム関数を作成できます。

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合は、ルールエディターに関数名でリストされます。ただし、カスタム関数の読みやすさを向上させるために、JavaScript 注釈を含めることをお勧めします。


### 必須の JavaScript 注釈またはコメントを含む矢印関数

矢印関数の構文を使用して、カスタム関数を作成できます。

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターにリストされません。

### 必須の JavaScript 注釈またはコメントを含む関数式

アダプティブフォームのルールエディターにカスタム関数をリストするには、次の形式でカスタム関数を作成します。アダプティブフォームのルールエディターでカスタム関数をリストするには、次の形式でカスタム関数を作成します。

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

ユーザーがカスタム関数に JavaScript 注釈を追加しない場合、カスタム関数はアダプティブフォームのルールエディターにリストされません。

### カスタム関数を作成するための前提条件

アダプティブフォームにカスタム関数を追加する前に、次のソフトウェアがマシンにインストールされていることを確認する必要があります。

* **プレーンテキストエディター（IDE）**：どのプレーンテキストエディターでも機能しますが、Microsoft Visual Studio Code などの統合開発環境（IDE）では、編集を簡単にする高度な機能が提供されます。

* **Git**：コードの変更を管理するには、このバージョン管理システムが必須です。インストール済みでない場合は、https://git-scm.com からダウンロードしてください。


## カスタム関数の作成 {#create-custom-function}

カスタム関数を作成する手順は次のとおりです。
1. [AEM プロジェクトアーキタイプを使用してクライアントサイドライブラリを作成し、カスタム関数を追加](#create-client-library-archetype)
または
   [CRXDE を通じてカスタム関数を作成](#create-add-custom-function)
1. [アダプティブフォームにクライアントライブラリを追加](#add-client-library)
1. [アダプティブフォームでカスタム関数を使用](#use-custom-functions)


### AEM プロジェクトアーキタイプを使用してクライアントライブラリを作成{#create-client-library-archetype}

[AEM プロジェクトアーキタイプを使用](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/using#getting-started)して作成したプロジェクトにクライアントライブラリを追加することで、カスタム関数を追加できます。
既存のプロジェクトがある場合は、<!--and have already the project structure as shown in the image below,-->ローカルプロジェクトに[カスタム関数](#create-add-custom-function)を直接追加できます。

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

アーキタイププロジェクトを作成するか、既存のプロジェクトを使用したら、クライアントライブラリを作成します。クライアントライブラリを作成するには、次の手順を実行します。

**クライアントライブラリフォルダーの追加**

[AEM プロジェクトディレクトリ] に新しいクライアントライブラリフォルダーを追加するには、次の手順に従います。

1. エディターで [AEM プロジェクトディレクトリ] を開きます。

   ![カスタム関数のフォルダー構造](assets/custom-library-folder-structure.png)

1. `ui.apps` を見つけます。
1. 新しいフォルダーを追加します。例えば、`experience-league` という名前のフォルダーを追加します。
1. `/experience-league/` フォルダーに移動し、`ClientLibraryFolder` を追加します。例えば、`customclientlibs` という名前のクライアントライブラリフォルダーを作成します。

   場所：`[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**クライアントライブラリフォルダーへのファイルとフォルダーの追加**

追加したクライアントライブラリフォルダーに以下を追加します。

* `.content.xml` ファイル
* `js.txt` ファイル
* `js` フォルダー

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. `.content.xml` で、次のコード行を追加します。

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > `client library folder` と `categories` プロパティには任意の名前を選択できます。

1. `js.txt` で、次のコード行を追加します。

   ```javascript
         #base=js
       function.js
   ```

1. `js` フォルダーで、カスタム関数を含む JavaScript ファイルを `function.js` として追加します。

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. ファイルを保存します。

![カスタム関数のフォルダー構造](assets/custom-function-added-files.png)

**新しいフォルダーを filter.xml に含める**：

1. [AEMaaCS プロジェクトディレクトリ]内の `/ui.apps/src/main/content/META-INF/vault/filter.xml` ファイルに移動します。

1. ファイルを開き、最後に次の行を追加します。

   `<filter root="/apps/experience-league" />`
1. ファイルを保存します。

   ![カスタム関数フィルター xml](assets/custom-function-filterxml.png)

1. [ビルドする方法](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build)の節の手順に従って、新しく作成したクライアントライブラリフォルダーを AEM 環境にビルドします。

## CRXDE を通じてカスタム関数を作成{#create-add-custom-function}

最新の AEM Forms および Forms アドオンを使用している場合は、CRXDE を通じてカスタム関数を作成し、カスタム関数の最新の更新を使用できます。これを行うには、次の手順を実行します。

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. `http://server:port/crx/de/index.jsp#` にログインします。
1. `/apps` フォルダーの下にフォルダーを作成します。例えば、`experience-league` という名前のフォルダーを作成します。
1. 変更を保存します。
1. 作成したフォルダーに移動し、タイプ `cq:ClientLibraryFolder` のノードを `clientlibs` として作成します。
1. 新しく作成した `clientlibs` フォルダーに移動し、`allowProxy` プロパティと `categories` プロパティを追加します。

   ![カスタムライブラリノードのプロパティ](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > `customfunctionsdemo` の代わりに任意の名前を指定できます。

1. 変更を保存します。

1. `clientlibs` フォルダーの下に `js` というフォルダーを作成します。
1. `js` フォルダーの下に `functions.js` という JavaScript ファイルを作成します。
1. `clientlibs` フォルダーの下に `js.txt` というファイルを作成します。
1. 変更を保存します。
作成したフォルダー構造は次のようになります。

   ![作成したクライアントライブラリフォルダー構造](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. `functions.js` ファイルをダブルクリックして、エディターを開きます。ファイルには、カスタム関数のコードが含まれています。
生年月日（YYYY-MM-DD）に基づいて年齢を計算するのに、JavaScript ファイルに次のコードを追加してみましょう。

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. `function.js` を保存します。
1. `js.txt` に移動し、次のコードを追加します。

   ```javascript
       #base=js
       functions.js
   ```

1. `js.txt` ファイルを保存します。

次の[カスタム関数](/help/forms/using/assets/customfunction.zip)フォルダーを参照できます。このフォルダーをダウンロードして AEM インスタンスにインストールします。

これで、クライアントライブラリを追加することで、アダプティブフォームでカスタム関数を使用できます。

## アダプティブフォームでのクライアントライブラリの追加{#add-client-library}

クライアントライブラリを AEM Forms 環境にデプロイしたら、その機能をアダプティブフォームで使用します。アダプティブフォームでクライアントライブラリを追加するには、次の手順に従います。

1. フォームを編集モードで開きます。フォームを編集モードで開くには、フォームを選択し、「**[!UICONTROL 編集]**」を選択します。
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナのプロパティアイコンをクリックします。アダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 基本]**」タブをクリックし、ドロップダウンリストから&#x200B;**[!UICONTROL クライアントライブラリカテゴリ]**&#x200B;の名前を選択します（この場合は、`customfunctionscategory` を選択します）。

   ![カスタム関数のクライアントライブラリを追加](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. 「**[!UICONTROL 完了]**」をクリックします。

これで、ルールエディターでカスタム関数を使用するルールを作成できます。

![カスタム関数のクライアントライブラリを追加](/help/forms/using//assets/calculateage-customfunction.png)

次に、[AEM Forms 6.5 でルールエディターのサービスの呼び出し](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)を使用して、カスタム関数を設定および使用する方法について説明します。

## アダプティブフォームでカスタム関数を使用 {#use-custom-functions}

アダプティブフォームでは、[ルールエディター内でカスタム関数](/help/forms/using/rule-editor-core-components.md)を使用できます。
生年月日（YYYY-MM-DD）に基づいて年齢を計算するために、JavaScript ファイル（`Function.js` ファイル）に次のコードを追加してみましょう。生年月日を入力として受け取り、年齢を返す `calculateAge()` というカスタム関数を作成します。

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

上記の例では、ユーザーが生年月日を（YYYY-MM-DD）形式で入力すると、カスタム関数 `calculateAge` が呼び出され、年齢が返されます。

![ルールエディターでの年齢のカスタム関数の計算](/help/forms/using/assets/custom-function-calculate-age.png)

フォームをプレビューして、ルールエディターを通じてカスタム関数がどのように実装されるかを確認しましょう。

![ルールエディターフォームプレビューでの年齢のカスタム関数の計算](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> 次の[カスタム関数](/help/forms/using/assets/customfunctions.zip)フォルダーを参照できます。[パッケージマネージャー](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager)を使用して、このフォルダーをダウンロードして AEM インスタンスにインストールします。

### カスタム関数での非同期関数のサポート {#support-of-async-functions}

非同期カスタム関数は、ルールエディターリストに表示されません。ただし、同期関数式を使用して作成されたカスタム関数内で、非同期関数を呼び出すことができます。

![同期および非同期カスタム関数](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> カスタム関数内で非同期関数を呼び出すメリットは、非同期関数では複数のタスクを同時に実行でき、各関数の結果がカスタム関数内で使用されることです。

カスタム関数を使用して非同期関数を呼び出す方法については、以下のコードを参照してください。

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

上記の例では、asyncFunction 関数は `asynchronous function` です。`https://petstore.swagger.io/v2/store/inventory` に `GET` リクエストを送信して非同期操作を実行します。`await` を使用して応答を待機し、`response.json()` を使用して応答本文を JSON として解析し、データを返します。`callAsyncFunction` 関数は、`asyncFunction` 関数を呼び出してコンソールに応答データを表示する同期カスタム関数です。`callAsyncFunction` 関数は同期関数ですが、非同期の asyncFunction 関数を呼び出し、その結果を `then` および `catch` ステートメントで処理します。

動作を確認するために、ボタンを追加し、ボタンのクリック時に非同期関数を呼び出すボタンのルールを作成しましょう。

![非同期関数のルールの作成](/help/forms/using/assets/rule-for-async-funct.png)

ユーザーが `Fetch` ボタンをクリックすると、カスタム関数 `callAsyncFunction` が呼び出され、次に非同期関数 `asyncFunction` が呼び出されることを示す次のコンソールウィンドウのイラストを参照してください。コンソールウィンドウを調べて、ボタンをクリックした際の応答を確認します。

![コンソールウィンドウ](/help/forms/using/assets/async-custom-funct-console.png)

カスタム関数の機能について詳しく見ていきましょう。

## カスタム関数の様々な機能

カスタム関数を使用して、フォームにパーソナライズされた機能を追加できます。これらの関数は、特定のフィールドの操作、グローバルフィールドの使用、キャッシュなどの様々な機能をサポートします。この柔軟性により、組織の要件に応じてフォームをカスタマイズできます。

### カスタム関数のフィールドおよびグローバルスコープオブジェクト {#support-field-and-global-objects}

フィールドオブジェクトとは、テキストフィールドやチェックボックスなど、フォーム内の個々のコンポーネントまたは要素を指します。Globals オブジェクトには、フォームインスタンス、ターゲットフィールドインスタンス、カスタム関数内でフォームの変更を実行するためのメソッドなどの読み取り専用変数が含まれています。

>[!NOTE]
>
> `param {scope} globals` は最後のパラメーターにする必要があり、アダプティブフォームのルールエディターには表示されません。

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

様々なユースケースで、どのように `Contact Us` フォームを使用して、カスタム関数がフィールドオブジェクトとグローバルオブジェクトを使用するかを学びましょう。

![お問い合わせフォーム](/help/forms/using/assets/contact-us-form.png)

#### **ユースケース**：`SetProperty` ルールを使用してパネルを表示

フォームフィールドを `Required` として設定するには、[カスタム関数の作成](#create-custom-function)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * `[form-path]/jcr:content/guideContainer.model.json` にある使用可能なプロパティを使用して、フィールドプロパティを設定できます。
> * Globals オブジェクトの `setProperty` メソッドを使用してフォームに行った変更は、本質的に非同期で、カスタム関数の実行中には反映されません。

この例では、ボタンをクリックすると `personaldetails` パネルの検証が行われます。パネルでエラーが検出されない場合は、ボタンをクリックすると別のパネルである `feedback` パネルが表示されます。

`personaldetails` パネルを検証し、ユーザーが `Next` ボタンをクリックした際に `feedback` パネルが表示されるようにする `Next` ボタンのルールを作成しましょう。

![プロパティの設定](/help/forms/using/assets/custom-function-set-property.png)

`Next` ボタンをクリックすると、`personaldetails` パネルが検証される場所を示す次のイラストを参照してください。`personaldetails` 内のすべてのフィールドを検証すると、`feedback` パネルが表示されます。

![プロパティフォームのプレビューを設定](/help/forms/using/assets/set-property-form-preview.png)

`personaldetails` パネルのフィールドにエラーがある場合は、`Next` ボタンをクリックする際にフィールドレベルでエラーが表示され、`feedback` パネルは非表示のままになります。

![プロパティフォームのプレビューを設定](/help/forms/using/assets/set-property-panel.png)

#### **ユースケース**：フィールドを検証。

フィールドを検証するには、[カスタム関数の作成](#create-custom-function)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> `validate()` 関数に引数が渡されない場合は、フォームが検証されます。

この例では、カスタム検証パターンが `contact` フィールドに適用されます。ユーザーは、`10` で始まり `8` 桁の電話番号を入力する必要があります。ユーザーが `10` で始まらない電話番号、または `8` 桁以上または未満の電話番号を入力した場合、ボタンをクリックすると検証エラーメッセージが表示されます。

![メールアドレスの検証パターン](/help/forms/using/assets/custom-function-validation-pattern.png)

次の手順では、ボタンのクリック時に `contact` フィールドを検証する `Next` ボタンのルールを作成します。

![検証パターン](/help/forms/using/assets/custom-function-validate.png)

ユーザーが `10` で始まらない電話番号を入力すると、フィールドレベルでエラーメッセージが表示されることを示す次のイラストを参照してください。

![メールアドレスの検証パターン](/help/forms/using/assets/custom-function-validate-error-message.png)

ユーザーが有効な電話番号を入力し、`personaldetails` パネルのすべてのフィールドが検証されると、`feedback` パネルが画面に表示されます。

![メールアドレスの検証パターン](/help/forms/using/assets/validate-form-preview-form.png)

#### **ユースケース**：パネルをリセット

パネルをリセットするには、[カスタム関数の作成](#create-custom-function)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> `reset()` 関数で引数を渡さない場合は、フォームが検証されます。

この例では、`Clear` ボタンをクリックすると `personaldetails` パネルがリセットされます。次のステップでは、ボタンのクリック時にパネルをリセットする `Clear` ボタンのルールを作成します。

![クリアボタン](/help/forms/using/assets/custom-function-reset-field.png)

ユーザーが `clear` ボタンをクリックすると、`personaldetails` パネルがリセットされることを示す次のイラストを参照してください。

![フォームをリセット](assets/custom-function-reset-form.png)

#### **ユースケース**：フィールドレベルでカスタムメッセージを表示し、フィールドを無効としてマークするには

`markFieldAsInvalid()` 関数を使用すると、フィールドを無効として定義し、フィールドレベルでカスタムエラーメッセージを設定できます。`fieldIdentifier` の値は、`fieldId`、`field qualifiedName` または `field dataRef` に指定できます。`option` という名前のオブジェクトの値は、`{useId: true}`、`{useQualifiedName: true}` または `{useDataRef: true}` に指定できます。
フィールドを無効としてマークし、カスタムメッセージを設定するために使用される構文は次のとおりです。

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

フィールドレベルでカスタムメッセージを有効にするには、[カスタム関数の作成](#create-custom-function)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

この例では、ユーザーがコメントテキストボックスに 15 文字未満を入力すると、フィールドレベルでカスタムメッセージが表示されます。

次の手順では、`comments` フィールドのルールを作成します。

![フィールドを無効としてマーク](/help/forms/using/assets/custom-function-invalid-field.png)

`comments` フィールドに否定的なフィードバックを入力すると、フィールドレベルでカスタムメッセージが表示されることを示す次のデモを参照してください。

![フィールドを無効なプレビューフォームとしてマーク](/help/forms/using/assets/custom-function-invalidfield-form.png)

ユーザーがコメントテキストボックスに 15 文字以上を入力すると、フィールドが検証され、フォームが送信されます。

![フィールドを有効なプレビューフォームとしてマーク](/help/forms/using/assets/custom-function-validfield-form.png)


#### **ユースケース**：変更されたデータをサーバーに送信

次のコード行：
`globals.functions.submitForm(globals.functions.exportData(), false);` は、操作後にフォームデータを送信するために使用されます。
* 最初の引数は、送信するデータです。
* 2 番目の引数は、フォームを送信する前に検証するかどうかを表します。これは `optional` であり、デフォルトでは `true` に設定されています。
* 3 番目の引数は送信の `contentType` です。これもオプションで、デフォルト値は `multipart/form-data` です。その他の値は、`application/json` と `application/x-www-form-urlencoded` に指定できます。

操作したデータをサーバーに送信するには、[カスタム関数の作成](#create-custom-function)の節の説明に従って、カスタム関数に次のコードを追加します。

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

この例では、ユーザーが `comments` テキストボックスを空のままにすると、フォームの送信時に `NA` がサーバーに送信されます。

次に、データを送信する `Submit` ボタンのルールを作成します。

![データを送信](/help/forms/using/assets/custom-function-submit-data.png)

ユーザーが `comments` テキストボックスを空のままにすると、サーバーに `NA` の値が送信されることを示す次の `console window` のイラストを参照してください。

![コンソールウィンドウでデータを送信](/help/forms/using/assets/custom-function-submit-data-form.png)

また、コンソールウィンドウを調べて、サーバーに送信されたデータを表示することもできます。

![ コンソール ウィンドウのデータを調べる](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## カスタム関数のキャッシュサポート

アダプティブフォームは、カスタム関数のキャッシュを実装して、ルールエディターでカスタム関数リストを取得する際の応答時間を短縮します。`error.log` ファイルに、`Fetched following custom functions list from cache` というメッセージが表示されます。

![キャッシュサポートを備えたカスタム関数](/help/forms/using/assets/custom-function-cache-error.png)

カスタム関数を変更すると、キャッシュは無効になり、解析されます。

## トラブルシューティング {#troubleshooting}

* ユーザーは、[コアコンポーネントと仕様のバージョンが最新バージョンに設定されている](https://github.com/adobe/aem-core-forms-components/tree/release/650)ことを確認する必要があります。ただし、既存の AEM プロジェクトとフォームの場合は、追加の手順を実行する必要があります。

   * AEM プロジェクトの場合、ユーザーは、`submitForm('custom:submitSuccess', 'custom:submitError')` のすべてのインスタンスを `submitForm()` に置き換えて、プロジェクトをデプロイする必要があります。

   * 既存のフォームについて、カスタム送信ハンドラーが正しく機能していない場合は、ユーザーはルールエディターを使用して「**送信**」ボタンの `submitForm` ルールを開いて保存する必要があります。このアクションは、フォーム内の既存のルールを `submitForm('custom:submitSuccess', 'custom:submitError')` から `submitForm()` に置き換えます。


* カスタム関数のコードを含む JavaScript ファイルにエラーがある場合、カスタム関数はアダプティブフォームのルールエディターにリストされません。カスタム関数リストを確認するには、エラーの `error.log` ファイルに移動します。エラーが発生した場合、カスタム関数リストは空で表示されます。

  ![エラーログファイル](/help/forms/using/assets/custom-function-list-error-file.png)

  エラーがない場合、カスタム関数が取得され、`error.log` ファイルに表示されます。`error.log` ファイルに、`Fetched following custom functions list` というメッセージが表示されます。

  ![適切なカスタム関数を使用したエラーログファイル](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## 考慮事項

* `parameter type` と `return type` は `None` をサポートしません。

* カスタム関数リストでサポートされていない関数は次のとおりです。
   * ジェネレーター関数
   * 非同期／待機関数
   * メソッドの定義
   * クラスメソッド
   * デフォルトのパラメーター
   * Rest パラメーター
