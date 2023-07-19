---
title: UI 文字列の国際化
seo-title: Internationalizing UI Strings
description: Java および JavaScript API を使用して文字列を国際化できます
seo-description: Java and JavaScript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 43%

---

# UI 文字列の国際化 {#internationalizing-ui-strings}

Java および JavaScript API を使用すると、次のタイプのリソースの文字列を国際化できます。

* Java ソースファイル。
* JSP スクリプト。
* クライアント側ライブラリまたはページソースの JavaScript。
* ダイアログおよびコンポーネント設定プロパティで使用される JCR ノードプロパティ値。

国際化とローカリゼーションのプロセスの概要については、 [コンポーネントの国際化](/help/sites-developing/i18n.md).

## Java および JSP コードでの文字列の国際化 {#internationalizing-strings-in-java-and-jsp-code}

`com.day.cq.i18n` Java パッケージを使用すると、ローカライズされた文字列を UI で表示できます。`I18n` クラスには、AEM の辞書からローカライズされた文字列を取得する `get` メソッドが用意されています。`get` メソッドの必須パラメーターは、英語の文字列リテラルのみです。英語は UI のデフォルトの言語です。次に、`Search` という単語をローカライズする例を示します。

`i18n.get("Search");`

英語での文字列の識別は、ID が文字列を識別し、実行時に文字列を参照するために使用される、一般的な国際化フレームワークとは異なります。 英語の文字列リテラルを使用すると、次の利点があります。

* コードがわかりやすくなります。
* デフォルト言語の文字列は常に使用可能です。

### ユーザーの言語の決定 {#determining-the-user-s-language}

ユーザーが希望する言語を決定する方法は 2 つあります。

* 認証済みユーザーの場合、ユーザーアカウントの環境設定から言語を指定します。
* 要求されたページのロケール。

より信頼性が高いので、ユーザーアカウントの language プロパティを使用することをお勧めします。 ただし、この方法を使用するには、ユーザーがログインしている必要があります。

#### I18n Java オブジェクトの作成 {#creating-the-i-n-java-object}

I18n クラスは、2 つのコンストラクタを提供します。 ユーザーの優先言語を決定する方法によって、使用するコンストラクタが決まります。

ユーザーアカウントで指定された言語で文字列を表示するには、`com.day.cq.i18n.I18n)` の読み込み後に次のコンストラクターを使用します。

```java
I18n i18n = new I18n(slingRequest);
```

このコンストラクターは、`SlingHTTPRequest` を使用して、ユーザーの言語設定を取得します。

ページロケールを使用して言語を決定するには、最初に要求されたページの言語の ResourceBundle を取得する必要があります。

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### 文字列の国際化 {#internationalizing-a-string}

`I18n` オブジェクトの `get` メソッドを使用して、文字列を国際化します。`get` メソッドの必須パラメーターは、国際化する文字列のみです。この文字列は、Translator 辞書の文字列に対応します。 get メソッドは、辞書内の文字列を検索し、現在の言語の翻訳を返します。

`get` メソッドの最初の引数は、次の規則に従ったものである必要があります。

* 値は文字列リテラルである必要があります。`String` タイプの変数は使用できません。
* 文字列リテラルは 1 行で表す必要があります。
* 文字列では大文字と小文字が区別されます。

```xml
i18n.get("Enter a search keyword");
```

#### 翻訳のヒントの使用 {#using-translation-hints}

辞書内で重複する文字列を識別できるようにするために、国際化される文字列の[翻訳のヒント](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)を指定します。翻訳のヒントを指定するには、`get` メソッドの 2 つ目のオプションパラメーターを使用します。翻訳のヒントは、辞書の項目のコメントプロパティと正確に一致させる必要があります。

例えば、文字列 `Request` が動詞と名詞としてそれぞれ 1 回ずつ、計 2 回辞書に記載されているとします。次のコードでは、`get` メソッドの引数として翻訳のヒントが記述されています。

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### ローカライズされた文に変数を含める {#including-variables-in-localized-sentences}

ローカライズされた文字列に変数を含めて、文にコンテキスト上の意味を作成します。 例えば、Web アプリケーションにログインした後、ホームページに「Welcome back Administrator.受信トレイに 2 通のメッセージがあります。」 ページコンテキストによって、ユーザー名とメッセージ数が決まります。

[辞書で](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings)の場合、変数は括弧で囲まれたインデックスとして文字列内に表されます。 変数の値は `get` メソッドの引数として指定します。引数は翻訳のヒントの後に配置され、インデックスは引数の順序に対応します。

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

国際化された文字列と翻訳のヒントは、辞書の文字列とコメントに完全に一致する必要があります。 2 つ目の引数に `null` 値を指定することで、翻訳のヒントを省略できます。

#### 静的 get メソッドの使用 {#using-the-static-get-method}

`I18N` クラスには、少数の文字列をローカライズする必要がある場合に役立つ静的 `get` メソッドが定義されています。この静的メソッドには、ユーザーの使用言語を特定する方法に応じて、オブジェクトの `get` メソッドのパラメーターに加え、`SlingHttpRequest` オブジェクトまたは使用する `ResourceBundle` が必要です。

* ユーザーの言語の環境設定を使用する場合：SlingHttpRequest を第 1 パラメーターとして指定します。

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* ページの言語を使用する場合：ResourceBundle を第 1 パラメーターとして指定します。

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### JavaScript コードの文字列の国際化 {#internationalizing-strings-in-javascript-code}

JavaScript API を使用すると、クライアント上の文字列をローカライズできます。 例： [Java と JSP](#internationalizing-strings-in-java-and-jsp-code) コードを使用すると、JavaScript API を使用して、ローカライズする文字列を識別し、ローカリゼーションのヒントを提供し、ローカライズされた文字列に変数を含めることができます。

この `granite.utils` [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md) は JavaScript API を提供します。 この API を使用するには、ページにこのクライアントライブラリフォルダーを含めます。ローカリゼーション関数は、`Granite.I18n` 名前空間を使用します。

ローカライズ対象の文字列を指定する前に、`Granite.I18n.setLocale` 関数を使用してロケールを設定する必要があります。この関数には、引数としてロケールの言語コードが必要です。

```
Granite.I18n.setLocale("fr");
```

ローカライズ対象の文字列を指定するには、`Granite.I18n.get` 関数を使用します。

```
Granite.I18n.get("string to localize");
```

次の例では、文字列「Welcome back」を国際化します。

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

関数のパラメーターは、Java I18n.get メソッドとは異なります。

* 1 つ目のパラメータは、ローカライズする文字列リテラルです。
* 2 番目のパラメーターは、文字列リテラルに挿入する値の配列です。
* 3 番目のパラメーターは、ローカライゼーションのヒントです。

次の例では、JavaScript を使用して「Welcome back Administrator」をローカライズしています。 受信トレイに 2 通のメッセージがあります。」 文：

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### JCR ノードからの文字列の国際化 {#internationalizing-strings-from-jcr-nodes}

UI 文字列は、多くの場合、JCR ノードのプロパティに基づいています。 例えば、ページの `jcr:title` プロパティは通常、ページコードの `h1` 要素のコンテンツとして使用されます。`I18n` クラスには、こうした文字列をローカライズするための `getVar` メソッドが用意されています。

次の例の JSP スクリプトは、リポジトリから `jcr:title` プロパティを取得し、ページにローカライズされた文字列を表示します。

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### JCR ノードの翻訳ヒントの指定 {#specifying-translation-hints-for-jcr-nodes}

類似 [Java API の翻訳のヒント](#using-translation-hints)を使用すると、辞書内の重複する文字列を区別するための翻訳のヒントを指定できます。 翻訳のヒントを、国際化されたプロパティを含むノードのプロパティとして指定します。 ヒントプロパティの名前は、国際化されたプロパティの名前と `_commentI18n` サフィックスで構成されます。

`${prop}_commentI18n`

例えば、`cq:page` ノードにローカライズされる jcr:title プロパティが含まれるとします。ヒントは、jcr:title_commentI18n という名前のプロパティの値として提供されます。

### 国際化対応のテスト {#testing-internationalization-coverage}

UI のすべての文字列が国際化されているかどうかをテストします。 対象となる文字列を確認するには、ユーザーの言語を zz_ZZ に設定し、Web ブラウザーで UI を開きます。 国際化された文字列は、次の形式のスタブ翻訳で表示されます。

`USR_*Default-String*_尠`

次の画像は、AEM ホームページのスタブ翻訳です。

![chlimage_1](assets/chlimage_1a.jpeg)

ユーザーの言語を設定するには、ユーザーアカウントの環境設定ノードの language プロパティを設定します。

ユーザーの環境設定ノードには、次のようなパスが含まれます。

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
