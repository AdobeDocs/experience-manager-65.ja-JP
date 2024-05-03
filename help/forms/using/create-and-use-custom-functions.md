---
title: アダプティブフォームでのカスタム関数の作成と追加
description: AEM Formsは、ルールエディター内で独自の関数を作成および使用できるカスタム関数をサポートしています。
keywords: ルールエディターでカスタム関数を使用して、カスタム関数の追加、カスタム関数の使用、カスタム関数の作成をおこないます。
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 50%

---


# アダプティブForms（コアコンポーネント）のカスタム関数

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | この記事 |

## はじめに

AEM Forms 6.5 では、ルールエディターを使用した複雑なビジネスルールの定義に使用できる JavaScript 関数を定義する機能が導入されました。 AEM Formsでは、すぐに使用できる多数のカスタム関数が用意されていますが、独自のカスタム関数を定義して複数のフォームで使用する必要があります。

カスタム関数は、入力したデータの操作や処理を容易にし、指定された要件を満たすことで、フォームの機能を拡張します。 定義済みの条件に基づいてフォームの動作を動的に変更することもできます。
アダプティブFormsでは、内でカスタム関数を使用できます [アダプティブフォームのルールエディター](/help/forms/using/rule-editor.md) フォームフィールドに特定の検証ルールを作成する場合
ユーザーがメールアドレスを入力するカスタム関数の使用を理解します。入力したメールアドレスが特定の形式に従っていることを確認します（「@」記号とドメイン名が含まれます）。 カスタム関数「ValidateEmail」を作成します。この関数は、メールアドレスを入力として受け取り、有効な場合は true を、それ以外の場合は false を返します。

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

上記の例では、ユーザーがフォームを送信しようとすると、カスタム関数「ValidateEmail」を呼び出して、入力されたメールアドレスが有効かどうかを確認します。

## カスタム関数の使用 {#uses-of-custom-function}

アダプティブFormsでカスタム関数を使用するメリットは次のとおりです。

* **データの操作**：カスタム関数は、フォームフィールドに入力されたデータを操作および処理します。
* **データの検証**：カスタム関数を使用すると、フォームの入力に対してカスタムチェックを実行し、指定したエラーメッセージを提供できます。
* **動的動作**：カスタム関数を使用すると、特定の条件に基づいてフォームの動的な動作を制御できます。 例えば、フィールドの表示/非表示、フィールド値の変更、フォームロジックの調整を動的に行うことができます。
* **統合**：カスタム関数を使用して外部の API やサービスと統合できます。 外部ソースからのデータの取得、外部 Rest エンドポイントへのデータの送信、外部イベントに基づくカスタムアクションの実行に役立ちます。

## サポートされる JS 注釈

記述したカスタム関数には、必ずが付随しています。 `jsdoc` その上に、カスタム設定と説明が必要な場合に備えています。 で関数を宣言する方法はいくつかあります。 `JavaScript,` とコメントを使用して、関数を追跡できます。 詳しくは、[usejsdoc.org](https://jsdoc.app/) を参照してください。

サポートされる`jsdoc`タグ：

* **プライベート**
構文：`@private`
プライベート関数は、カスタム関数として含まれていません。

* **名前**
構文：`@name funcName <Function Name>`
或いは`,` `@function funcName <Function Name>` **または** `@func` `funcName <Function Name>` を使用できます。
  `funcName` ：関数の名前です（スペースは使用不可）。
  `<Function Name>`：関数の表示名です。

* **メンバー**
構文：`@memberof namespace`
関数に名前空間を追加します。

* **パラメーター**
構文：`@param {type} name <Parameter Description>`
或いは、`@argument` `{type} name <Parameter Description>` **または** `@arg` `{type}` `name <Parameter Description>` を使用できます。
関数で使用されるパラメーターを表示します。関数には、複数のパラメータタグを設けることができます。各パラメーターは、実行順序に応じて 1 個のタグを設けることができます。
  `{type}` は、パラメータータイプを表します。許可されているパラメータータイプは、以下のとおりです。

   1. 文字列
   2. 数値
   3. ブール値
   4. 対象範囲

  範囲を使用して、アダプティブフォームのフィールドを参照します。フォームが遅延読み込みを使用している場合は、`scope`を使用してフィールドにアクセスできます。フィールドは、フィールドが読み込まれたときか、フィールドがグローバルとしてマークされているときにアクセスできます。

  他のすべてのパラメータータイプは、上記のいずれかに分類されます。「なし」はサポートされていません。必ず上記のタイプのいずれかを選択してください。タイプでは大文字と小文字が区別されません。パラメーター `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>` では、スペースは使用できません。

* **戻り値のタイプ**
構文：`@return {type}`
または、`@returns {type}` を使用できます。
目的などの、関数に関する情報を追加します。{type} は、関数の戻り値のタイプを表します。許可されている戻り値のタイプは次のとおりです。

   1. 文字列
   1. 数値
   1. ブール値

  他のすべての戻り値のタイプは、上記のいずれかに分類されます。「なし」はサポートされていません。必ず上記のタイプのいずれかを選択してください。戻り値のタイプでは、大文字と小文字が区別されません。

* **This**
構文：`@this currentComponent`

  ルールが記述されているアダプティブフォームコンポーネントを参照するには、@this を使用します。

  次の例は、フィールド値に基づいています。次の例では、ルールによりフォーム内のフィールドが非表示になります。`this.value`の`this`部分は、ルールが記述されている基になるアダプティブフォームコンポーネントを参照します。

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
  >カスタム関数の前のコメントは、概要で使用されます。概要は複数の行に拡張することができます。終端にはタグを使用します。説明を簡潔にするため、ルールビルダーでは 1 行以内に抑えるように心がけてください。

## 関数の宣言でサポートされるタイプ {#function-declaration-supported-types}

**文関数**

```javascript
function area(len) {
    return len*len;
}
```

この関数は、`jsdoc` コメント無しで追加されています。

**関数式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**関数式と文関数**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**変数としての関数宣言**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

制限事項：カスタム関数は、変数リストから最初の関数宣言のみを選択します（共に使用する場合）。関数式は、すべての関数宣言に使用することができます。

**オブジェクトとしての関数宣言**

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

## カスタム関数の作成 {#create-custom-function}

カスタム関数を作成するには、次の手順を実行します。

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
1. `functions.js` ファイルをダブルクリックして、エディターを開きます。ファイルは、カスタム関数のコードを含みます。
JavaScript ファイルに次のコードを追加して、生年月日（YYYY-MM-DD）に基づいて年齢を計算しましょう。

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

次を参照してください。 [カスタム関数](/help/forms/using/assets/customfunction.zip) フォルダー。 このフォルダーをダウンロードしてAEM インスタンスにインストールします。

これで、クライアントライブラリを追加して、アダプティブフォームでカスタム関数を使用できるようになりました。

## アダプティブフォームへのクライアントライブラリの追加{#use-custom-function}

クライアントライブラリをForms CS 環境にデプロイしたら、アダプティブフォームでその機能を使用します。 アダプティブフォームにクライアントライブラリを追加するには、次の手順に従います

1. フォームを編集モードで開きます。フォームを編集モードで開くには、フォームを選択し、以下を選択します。 **[!UICONTROL 編集]**.
1. コンテンツブラウザーを開き、アダプティブフォームの&#x200B;**[!UICONTROL ガイドコンテナ]**&#x200B;コンポーネントを選択します。
1. ガイドコンテナのプロパティアイコンをクリックします。 アダプティブフォームコンテナダイアログボックスが開きます。
1. を開きます **[!UICONTROL 基本]** タブをクリックして、の名前を選択 **[!UICONTROL クライアントライブラリカテゴリ]** ドロップダウンリストから（この場合は、 `customfunctionscategory`）に設定します。

   ![カスタム関数をクライアントライブラリを追加する](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. クリック **[!UICONTROL 完了]** .

これで、ルールエディターでカスタム関数を使用するルールを作成できます。

![カスタム関数をクライアントライブラリを追加する](/help/forms/using//assets/calculateage-customfunction.png)

次に、 [AEM Formsでのルールエディターのサービスの呼び出し](/help//forms/using/rule-editor.md).
