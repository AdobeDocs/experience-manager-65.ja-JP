---
title: SCF Handlebars ヘルパー
seo-title: SCF Handlebars ヘルパー
description: SCF の操作を円滑化するための Handlebars ヘルパーメソッド
seo-description: SCF の操作を円滑化するための Handlebars ヘルパーメソッド
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 55%

---

# SCF Handlebars ヘルパー  {#scf-handlebars-helpers}

| **[⇐ 機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|  | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |

Handlebars ヘルパーは、SCF コンポーネントの操作を円滑化する目的で Handlebars から呼び出すことができるメソッドです。

実装では、クライアント側定義とサーバー側定義を扱います。開発者がカスタムヘルパーを作成することもできます。

AEM Communities に付属のカスタム SCF ヘルパーは、次の[クライアントライブラリ](../../help/sites-developing/clientlibs.md)に定義されています。

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>[最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)をインストールしてください。

## 短縮 {#abbreviate}

maxWords および maxLength プロパティに準拠した省略形文字列を返すヘルパーです。

省略対象の文字列は context で指定します。コンテキストを指定しない場合は、空の文字列が返されます。

context は最初に maxLength にトリミングされ、その後、いくつかの単語に分割されてから maxWords まで縮小されます。

safeString を true に設定した場合は、SafeString が文字列として返されます。

### パラメーター {#parameters}

* **コンテキスト**:文字列

   （オプション）デフォルトは空の文字列です

* **maxLength**:数値

   （オプション）デフォルトはコンテキストの長さです。

* **maxWords**:数値

   （オプション）デフォルト値は、トリミングされた文字列内の単語数です。

* **safeString**:Boolean

   （オプション）trueの場合はHandlebars.SafeString()を返します。 デフォルト値は false です。

### 例 {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

div の下に 2 つの span を追加するヘルパーです。一方はフルテキスト表示用、もう一方は縮小テキスト表示用で、これらの 2 つのビューを切り替えることができます。

### パラメーター {#parameters-1}

* **コンテキスト**:文字列

   （オプション）デフォルトは空の文字列です。

* **numChars**:数値

   （オプション）フルテキストを表示しない場合に表示する文字数。 初期設定は 100 です。

* **moreText**:文字列

   （オプション）表示するテキストが増えたことを示す、表示するテキストです。 デフォルト値は「more」です。

* **ellipsesText**:文字列

   （オプション）非表示のテキストがあることを示すテキストです。 デフォルト値は「...」です。

* **safeString**:Boolean

   （オプション）結果を返す前にHandlebars.SafeString()を適用するかどうかを示すブール値。 デフォルト値は false です。

### 例 {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

書式設定済みの日付文字列を返すヘルパーです。

### パラメーター {#parameters-2}

* **コンテキスト**:数値

   （オプション）1970年1月1日（エポック）からのミリ秒オフセットの値。 デフォルトは現在の日付です。

* **形式**:文字列

   （オプション）適用する日付の形式。 初期設定は「YYYY-MM-DDTHH:mm:ss.sssZ」で、結果は「2015-03-18T18:17:13-07:00」と表示されます。

### 例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 次と等しい {#equals}

等価条件に応じてコンテンツを返すヘルパーです。

### パラメーター {#parameters-3}

* **lvalue**:文字列

   比較する左側の値。

* **rvalue**:文字列

   比較する右側の値。

### 例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

[WCM mode](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)の現在の値を、モードの文字列区切りリストと照合するブロックヘルパーです。

### パラメーター {#parameters-4}

* **コンテキスト**:文字列

   （オプション）翻訳する文字列。 default を指定しない場合は必須です。

* **モード**:文字列

   （オプション）設定されているかどうかをテストする[WCMモード](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html)のコンマ区切りリスト。

### 例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

このヘルパーは、Handlebars ヘルパー「i18n」をオーバーライドします。

[JavaScript コードの文字列の国際化](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)も参照してください。

### パラメーター {#parameters-5}

* **コンテキスト**:文字列

   （オプション）翻訳する文字列。 default を指定しない場合は必須です。

* **デフォルト**:文字列

   （オプション）翻訳するデフォルトの文字列。 context を指定しない場合は必須です。

* **comment**:文字列

   （オプション）翻訳のヒント

### 例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 含む {#include}

コンポーネントを存在しないリソースとしてテンプレートにインクルードするヘルパーです。

このようにすると、JCR ノードとして追加したリソースよりも、プログラムによるカスタマイズがはるかに容易になります。[コミュニティコンポーネントの追加またはインクルード](scf.md#add-or-include-a-communities-component)を参照してください。

コミュニティコンポーネントの中でも、インクルードできるのはごく一部です。AEM 6.1では、インクルード可能なコメントは[comments](essentials-comments.md)、[rating](rating-basics.md)、[reviews](reviews-basics.md)、[voting](essentials-voting.md)です。

このヘルパーは、サーバー側にのみ該当し、JSP スクリプト用の [cq:include](../../help/sites-developing/taglib.md) と同じ機能を備えています。

### パラメーター {#parameters-6}

* **コンテキスト**:文字列またはオブジェクト

   （相対パスを指定しない限り、オプション）

   `this`を使用して、現在のコンテキストを渡します。

   `this.id`を使用して、要求されたresourceTypeをレンダリングするための`id`のリソースを取得します。

* **resourceType**:文字列

   （オプション）リソースタイプは、デフォルトでコンテキストのリソースタイプに設定されます。

* **template**:文字列

   コンポーネントスクリプトへのパス。

* **パス**:文字列

   （必須）リソースへのパス。 パスが相対パスの場合、context を指定する必要があります。そうしないと、空の文字列が返されます。

* **authoringDisabled**:Boolean

   （オプション）デフォルトはfalseです。 内部でのみ使用されます。

### 例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

これにより、`this.id` + /commentsに新しいコメントコンポーネントが含まれます。

## IncludeClientLib {#includeclientlib}

AEM html クライアントライブラリとして js、css、または theme の各ライブラリをインクルードするヘルパーです。jsやcssなど、異なるタイプを複数含める場合は、このタグをHandlebarsスクリプトで複数回使用する必要があります。

このヘルパーは、サーバー側にのみ適用され、JSPスクリプトの[ui:includeClientLib](../../help/sites-developing/taglib.md)と似た機能を提供します。

### パラメーター {#parameters-7}

* **カテゴリ**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリスト。 指定したカテゴリの JavaScript ライブラリと CSS ライブラリがすべてインクルードされます。テーマ名は要求から抽出されます。

* **テーマ**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリスト。 指定したカテゴリのテーマに関連するライブラリ（CSS と JS の両方）がすべてインクルードされます。テーマ名は要求から抽出されます。

* **js**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリスト。 指定したカテゴリの JavaScript ライブラリがすべてインクルードされます。

* **css**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリスト。 指定したカテゴリの CSS ライブラリがすべてインクルードされます。

### 例 {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## プリティタイム{#pretty-time}

カットオフポイントに達するまでは経過時間を表示し、それ以降は通常の日付形式を表示するヘルパーです。

以下に例を示します。

* 12 時間前
* 7 日前

### パラメーター {#parameters-8}

* **コンテキスト**:数値

   過去に&#39;今&#39;と比較する時間。 時間は 1970 年 1 月 1 日（epoch）からのミリ秒単位のオフセットとして表されます。

* **daysCutofof**:数値

   実際の日付に切り替える前の日数。 初期設定は 60 です。

### 例 {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

XSS に対する保護として、HTML 要素コンテンツのソース文字列をエンコードするヘルパーです。

注意：これはバリデーターではなく、属性値の記述には使用されません。

### パラメーター {#parameters-9}

* **コンテキスト**:object

   エンコードするHTMLです。

### 例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS に対する保護として、HTML 属性値に記述するソース文字列をエンコードするヘルパーです。

注意：これはバリデーターではなく、実用的な属性（href、src、イベントハンドラー）の記述には使用されません。

### パラメーター {#parameters-10}

* **コンテキスト**:オブジェクト

   エンコードするHTMLです。

### 例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSS に対する保護として、JavaScript 文字列コンテンツに記述するソース文字列をエンコードするヘルパーです。

注意：これはバリデーターではなく、任意の JavaScript への記述には使用されません。

### パラメーター {#parameters-11}

* **コンテキスト**:オブジェクト

   エンコードするHTMLです。

### 例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS に対する保護として、HTML の href または src 属性値として記述する URL の不要部分を削除するヘルパーです。

注意：空の文字列が返される場合があります。

### パラメーター {#parameters-12}

* **コンテキスト**:オブジェクト

   不要部分を削除するURL。

### 例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js の基本的概要 {#handlebars-js-basic-overview}

[Handlebars.jsドキュメント](https://handlebarsjs.com/expressions.html)のヘルパー関数の概要を簡単に説明します。

* Handlebars ヘルパーを呼び出すには、単純な識別子（ヘルパーの名前&#x200B;**）を使用し、それに続けて 0 個以上のパラメーターをスペースで区切って指定します。
* パラメーターには、単純な文字列、数値、ブール値、または JSON オブジェクトを指定し、オプションで最後のパラメーターとして一連のキー／値ペア（ハッシュ引数）を指定します。
* ハッシュ引数内のキーは単純な識別子にする必要があります。
* ハッシュ引数内の値は Handlebars 式（単純な識別子、パス、または文字列）です。
* 現在のコンテキスト`this`は、常にHandlebarsヘルパーで使用できます。
* コンテキストは、文字列、数値、ブール値、JSONデータオブジェクトのいずれかです。
* `this.url` や `this.id` のように、現在のコンテキスト内にネストされているオブジェクトを context として渡すことができます（単純なヘルパーおよびブロックヘルパーを示す後述の例を参照）。

* ブロックヘルパーとは、テンプレート内の任意の場所から呼び出すことができる関数です。テンプレートのブロックは、毎回異なるコンテキストで0回以上呼び出すことができます。 {{#*name*}}と{{/*name*}}の間のコンテキストが含まれます。

* Handlebars では、ヘルパーに対する最後のパラメーターとして「options」を使用します。特別なオブジェクト「options」には、

   * オプションのプライベートデータ(options.data)
   * 呼び出しのオプションのキーと値のプロパティ(options.hash)
   * 自身を呼び出す機能(options.fn())
   * 逆関数を呼び出す機能(options.inverse())

* ヘルパーから返される HTML 文字列コンテンツは SafeString になるようにすることをお勧めします。

### Handlebars.jsドキュメントのシンプルなヘルパーの例を次に示します。{#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

レンダリング：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>ポスト！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.jsドキュメントのブロックヘルパーの例を次に示します。{#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

レンダリング：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## カスタム SCF ヘルパー {#custom-scf-helpers}

カスタムヘルパーは、特にデータを渡す場合に、クライアント側だけでなくサーバー側で実装する必要があります。SCFの場合、ページが要求されたときにサーバーが特定のコンポーネントのHTMLを生成するので、ほとんどのテンプレートはサーバー側でコンパイルおよびレンダリングされます。

### サーバー側カスタムヘルパー {#server-side-custom-helpers}

カスタムSCFヘルパーをサーバー側に実装して登録するには、Javaインターフェイス[TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)を実装し、[OSGi Service](../../help/sites-developing/the-basics.md#osgi)にして、OSGiバンドルの一部としてインストールします。

以下に例を示します。

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>サーバー側用に作成したヘルパーは、クライアント側用にも作成する必要があります。
>
>このコンポーネントは、ログインしているユーザーのクライアント側で再レンダリングされます。クライアント側ヘルパーが見つからない場合、このコンポーネントは表示されません。

### クライアント側カスタムヘルパー {#client-side-custom-helpers}

クライアント側ヘルパーは、`Handlebars.registerHelper()` () を呼び出すことによって登録する Handlebars スクリプトです。以下に例を示します。

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

カスタムクライアント側ヘルパーは、カスタムクライアントライブラリに追加する必要があります。
clientlib の条件は次のとおりです。

* `cq.social.scf`に依存関係を含めます。
* Handlebarsがロードされた後にロードします。
* [included](clientlibs.md)にしてください。

注意：SCFヘルパーは`/etc/clientlibs/social/commons/scf/helpers.js`で定義されます。

| **[⇐ 機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|  | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
