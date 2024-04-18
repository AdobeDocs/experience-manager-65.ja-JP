---
title: UI 文字列の国際化
description: Java&trade；および JavaScript API を使用して、文字列を国際化できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 36%

---

# UI 文字列の国際化 {#internationalizing-ui-strings}

Java™ および JavaScript API を使用すると、次のタイプのリソースで文字列を国際化できます。

* Java™ ソースファイル。
* JSP スクリプト。
* クライアントサイドライブラリまたはページソースでの JavaScript
* ダイアログおよびコンポーネント設定プロパティで使用される JCR ノードプロパティの値

国際化およびローカリゼーションのプロセスの概要については、を参照してください。 [コンポーネントの国際化](/help/sites-developing/i18n.md).

## Java™ および JSP コードにおける文字列の国際化 {#internationalizing-strings-in-java-and-jsp-code}

この `com.day.cq.i18n` Java™ パッケージを使用すると、ローカライズされた文字列を UI で表示できます。 この `I18n` クラスは、を提供します `get` Adobe Experience Manager（AEM）の辞書からローカライズされた文字列を取得するメソッド。 `get` メソッドの必須パラメーターは、英語の文字列リテラルのみです。英語は UI のデフォルト言語です。 次に、`Search` という単語をローカライズする例を示します。

`i18n.get("Search");`

英語での文字列の識別は、ID が文字列を識別し、実行時に文字列を参照するために使用される一般的な国際化フレームワークとは異なります。 英語の文字列リテラルを使用すると、次の利点があります。

* コードは理解しやすい。
* デフォルト言語の文字列は常に利用できます。

### ユーザーの言語の決定 {#determining-the-user-s-language}

ユーザーが好む言語を決定する方法は 2 つあります。

* 認証済みユーザーの場合、ユーザーアカウントの環境設定から言語を決定します。
* リクエストされたページのロケール。

ユーザーアカウントの言語プロパティの方が信頼性が高いので、このプロパティの方が望ましい方法です。 ただし、この方法を使用するには、ユーザーがログインする必要があります。

#### I18n Java™ オブジェクトの作成 {#creating-the-i-n-java-object}

I18n クラスは、2 つのコンストラクタを提供します。 ユーザーの優先言語を決定する方法によって、使用するコンストラクターが決まります。

ユーザーアカウントで指定された言語で文字列を表示するには、`com.day.cq.i18n.I18n)` の読み込み後に次のコンストラクターを使用します。

```java
I18n i18n = new I18n(slingRequest);
```

このコンストラクターは、`SlingHTTPRequest` を使用して、ユーザーの言語設定を取得します。

ページのロケールを使用して言語を決定するには、まず、リクエストされたページの言語の ResourceBundle を取得します。

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 文字列の国際化 {#internationalizing-a-string}

`I18n` オブジェクトの `get` メソッドを使用して、文字列を国際化します。`get` メソッドの必須パラメーターは、国際化する文字列のみです。Translator ディクショナリの文字列に対応する文字列。 get メソッドは辞書内の文字列を検索し、現在の言語の翻訳を返します。

`get` メソッドの最初の引数は、次の規則に従ったものである必要があります。

* 値は文字列リテラルである必要があります。`String` タイプの変数は使用できません。
* 文字列リテラルは、1 行で表現する必要があります。
* この文字列は、大文字と小文字が区別されます。

```xml
i18n.get("Enter a search keyword");
```

#### 翻訳ヒントの使用 {#using-translation-hints}

辞書内で重複する文字列を識別できるようにするために、国際化される文字列の[翻訳のヒント](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)を指定します。翻訳のヒントを指定するには、`get` メソッドの 2 つ目のオプションパラメーターを使用します。翻訳のヒントは、辞書の項目のコメントプロパティと正確に一致させる必要があります。

例えば、辞書にはという文字列が含まれます `Request` 2 回：1 回は動詞、1 回は名詞。 次のコードでは、`get` メソッドの引数として翻訳のヒントが記述されています。

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### ローカライズされた文への変数の組み込み {#including-variables-in-localized-sentences}

ローカライズされる文字列に変数を追加し、センテンスに文脈に応じた意味を持たせます。例えば、Web アプリケーションにログインした後、ホームページに「Welcome back Administrator.インボックスには 2 つのメッセージがあります。」 ページのコンテキストに応じて、ユーザー名とメッセージ数が決定されます。

[辞書の内容](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)、変数は括弧で囲まれたインデックスとして文字列で表されます。 変数の値は `get` メソッドの引数として指定します。引数は翻訳のヒントに従って配置され、インデックスは引数の順序に対応します。

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

国際化される文字列と翻訳のヒントは、辞書の文字列およびコメントと完全に一致させる必要があります。 2 つ目の引数に `null` 値を指定することで、翻訳のヒントを省略できます。

#### 静的 get メソッドの使用 {#using-the-static-get-method}

この `I18N` クラスは静的なを定義します `get` いくつかの文字列をローカライズする必要がある場合に役立つメソッド。 この静的メソッドには、ユーザーの使用言語を特定する方法に応じて、オブジェクトの `get` メソッドのパラメーターに加え、`SlingHttpRequest` オブジェクトまたは使用する `ResourceBundle` が必要です。

* ユーザーの言語の環境設定を使用する場合：SlingHttpRequest を第 1 パラメーターとして指定します。

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* ページの言語を使用する場合：ResourceBundle を第 1 パラメーターとして指定します。

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### JavaScript コードでの文字列の国際化 {#internationalizing-strings-in-javascript-code}

JavaScript API を使用すると、クライアント上で文字列をローカライズできます。 例： [Java™ と JSP](#internationalizing-strings-in-java-and-jsp-code) コード、JavaScript API を使用すると、ローカライズ対象の文字列を識別したり、翻訳のヒントを指定したり、ローカライズする文字列に変数を追加したりできます。

この `granite.utils` [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md) は JavaScript API を提供します。 この API を使用するには、ページにこのクライアントライブラリフォルダーを含めます。ローカリゼーション関数は、`Granite.I18n` 名前空間を使用します。

ローカライズ対象の文字列を指定する前に、 `Granite.I18n.setLocale` 関数。 この関数には、引数としてロケールの言語コードが必要です。

```
Granite.I18n.setLocale("fr");
```

ローカライズ対象の文字列を指定するには、`Granite.I18n.get` 関数を使用します。

```
Granite.I18n.get("string to localize");
```

次の例では、「Welcome back」という文字列を国際化しています。

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

関数のパラメーターは、Java™ I18n.get メソッドとは異なります。

* 最初のパラメーターは、ローカライズする文字列リテラルです。
* 2 番目のパラメーターは、文字列リテラルに挿入する値の配列です。
* 3 番目のパラメーターは、翻訳のヒントです。

次の例では、JavaScript を使用して「Welcome back Administrator. インボックスには 2 つのメッセージがあります。」 文：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### JCR ノードからの文字列の国際化 {#internationalizing-strings-from-jcr-nodes}

UI 文字列は、多くの場合、JCR ノードプロパティに基づいています。 例えば、ページの `jcr:title` プロパティは通常、ページコードの `h1` 要素のコンテンツとして使用されます。`I18n` クラスには、こうした文字列をローカライズするための `getVar` メソッドが用意されています。

次の例の JSP スクリプトは、リポジトリから `jcr:title` プロパティを取得し、ページにローカライズされた文字列を表示します。

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### JCR ノードの翻訳ヒントの指定 {#specifying-translation-hints-for-jcr-nodes}

類似 [java™ API の翻訳のヒント](#using-translation-hints)を使用すると、辞書内の重複文字列を区別するための翻訳ヒントを指定できます。 国際化されたプロパティを含むノードのプロパティとして、翻訳のヒントを指定します。 ヒントプロパティの名前は、国際化されたプロパティの名前をで構成します。 `_commentI18n` サフィックス：

`${prop}_commentI18n`

例えば、`cq:page` ノードにローカライズされる jcr:title プロパティが含まれるとします。ヒントは、jcr:title_commentI18n という名前のプロパティの値として提供されます。

### 国際化の対象範囲のテスト {#testing-internationalization-coverage}

UI 内のすべての文字列を国際化したかどうかをテストします。 どの文字列がカバーされているかを確認するには、ユーザー言語を zz_ZZ に設定し、web ブラウザーで UI を開きます。 国際化された文字列は、次の形式でスタブ翻訳と共に表示されます。

`USR_*Default-String*_尠`

次の画像は、AEM ホームページのスタブ翻訳です。

![chlimage_1](assets/chlimage_1a.jpeg)

ユーザーの言語を設定するには、ユーザーアカウントの環境設定ノードの言語プロパティを設定します。

ユーザーの環境設定ノードには、次のようなパスがあります。

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
