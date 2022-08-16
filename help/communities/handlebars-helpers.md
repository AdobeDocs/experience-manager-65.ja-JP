---
title: SCF Handlebars ヘルパー
seo-title: SCF Handlebars Helpers
description: SCF の操作を円滑化するための Handlebars ヘルパーメソッド
seo-description: Handlebars Helper methods to facilitate work with SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 56%

---

# SCF Handlebars ヘルパー {#scf-handlebars-helpers}

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

省略対象の文字列は context で指定します。コンテキストを指定しない場合、空の文字列が返されます。

context は最初に maxLength にトリミングされ、その後、いくつかの単語に分割されてから maxWords まで縮小されます。

safeString を true に設定した場合は、SafeString が文字列として返されます。

### パラメーター {#parameters}

* **context**:文字列

   （オプション）デフォルトは空の文字列です。

* **maxLength**:数値

   （オプション）デフォルトはコンテキストの長さです。

* **maxWords**:数値

   （オプション）デフォルトは、トリミングされた文字列内の単語数です。

* **safeString**:ブール値

   （オプション）true の場合、Handlebars.SafeString() を返します。 デフォルト値は false です。

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

* **context**:文字列

   （オプション）デフォルトは空の文字列です。

* **numChars**:数値

   （オプション）全文を表示しない場合に表示する文字数。 初期設定は 100 です。

* **moreText**:文字列

   （オプション）表示するテキストが増えたことを示す、表示するテキストです。 デフォルト値は「more」です。

* **ellipsesText**:文字列

   （オプション）非表示のテキストがあることを示す、表示するテキストです。 デフォルト値は「...」です。

* **safeString**:ブール値

   （オプション）結果を返す前に Handlebars.SafeString() を適用するかどうかを示すブール値。 デフォルト値は false です。

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

* **context**:数値

   （オプション）1970 年 1 月 1 日（エポック）からのミリ秒のオフセット値。 初期設定は現在の日付です。

* **形式**:文字列

   （オプション）適用する日付フォーマット。 デフォルトは「YYYY-MM-DDTHH」です。:mm:ss.sssZ と表示され、結果は「2015-03-18T18」と表示されます。:17:13-07:00&quot;

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

の現在の値をテストするブロックヘルパー [WCM モード](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) を、文字列区切りのモードのリストに対して設定します。

### パラメーター {#parameters-4}

* **context**:文字列

   （オプション）翻訳する文字列です。 default を指定しない場合は必須です。

* **mode**:文字列

   （オプション） [WCM モード](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) をテストします。

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

* **context**:文字列

   （オプション）翻訳する文字列です。 default を指定しない場合は必須です。

* **デフォルト**:文字列

   （オプション）翻訳するデフォルトの文字列です。 context を指定しない場合は必須です。

* **コメント**:文字列

   （オプション）翻訳のヒント

### 例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 含む {#include}

コンポーネントを存在しないリソースとしてテンプレートにインクルードするヘルパーです。

このようにすると、JCR ノードとして追加したリソースよりも、プログラムによるカスタマイズがはるかに容易になります。[コミュニティコンポーネントの追加またはインクルード](scf.md#add-or-include-a-communities-component)を参照してください。

コミュニティコンポーネントの中でも、インクルードできるのはごく一部です。AEM 6.1 の場合、インクルード可能なものは次のとおりです。 [コメント](essentials-comments.md), [評価](rating-basics.md), [レビュー](reviews-basics.md)、および [投票](essentials-voting.md).

このヘルパーは、サーバー側にのみ該当し、JSP スクリプト用の [cq:include](../../help/sites-developing/taglib.md) と同じ機能を備えています。

### パラメーター {#parameters-6}

* **context**:文字列またはオブジェクト

   （相対パスを指定しない場合はオプション）

   用途 `this` 現在のコンテキストを渡す

   用途 `this.id` 資源を得る `id` リクエストされた resourceType をレンダリングするために使用します。

* **resourceType**:文字列

   （オプション）リソースタイプは、デフォルトでコンテキストからリソースタイプに設定されます。

* **テンプレート**:文字列

   コンポーネントスクリプトのパス。

* **パス**:文字列

   （必須）リソースへのパス。 パスが相対パスの場合、context を指定する必要があります。そうしないと、空の文字列が返されます。

* **authoringDisabled**:ブール値

   （オプション）デフォルトは false です。 内部でのみ使用されます。

### 例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

これにより、次の場所に新しいコメントコンポーネントが含まれます： `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

AEM html クライアントライブラリとして js、css、または theme の各ライブラリをインクルードするヘルパーです。js や css など、異なるタイプの複数のインクルージョンの場合、このタグを Handlebars スクリプトで複数回使用する必要があります。

このヘルパーは、サーバー側にのみ適用され、次のような機能を提供します。 [ui:includeClientLib](../../help/sites-developing/taglib.md) （JSP スクリプト用）

### パラメーター {#parameters-7}

* **カテゴリ**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリストです。 指定したカテゴリの JavaScript ライブラリと CSS ライブラリがすべてインクルードされます。テーマ名は要求から抽出されます。

* **テーマ**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリストです。 指定したカテゴリのテーマに関連するライブラリ（CSS と JS の両方）がすべてインクルードされます。テーマ名は要求から抽出されます。

* **js**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリストです。 指定したカテゴリの JavaScript ライブラリがすべてインクルードされます。

* **css**:文字列

   （オプション）クライアントライブラリカテゴリのコンマ区切りリストです。 指定したカテゴリの CSS ライブラリがすべてインクルードされます。

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

## プリティタイム {#pretty-time}

カットオフポイントに達するまでは経過時間を表示し、それ以降は通常の日付形式を表示するヘルパーです。

次に例を示します。

* 12 時間前
* 7 日前

### パラメーター {#parameters-8}

* **context**:数値

   「今」と比較する過去の時間。 時間は 1970 年 1 月 1 日（epoch）からのミリ秒単位のオフセットとして表されます。

* **daysCutofof**:数値

   実際の日付に切り替えるまでの日数。 初期設定は 60 です。

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

* **context**:object

   エンコードするHTML。

### 例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS に対する保護として、HTML 属性値に記述するソース文字列をエンコードするヘルパーです。

注意：これはバリデーターではなく、実用的な属性（href、src、イベントハンドラー）の記述には使用されません。

### パラメーター {#parameters-10}

* **context**:オブジェクト

   エンコードするHTML。

### 例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSS に対する保護として、JavaScript 文字列コンテンツに記述するソース文字列をエンコードするヘルパーです。

注意：これはバリデーターではなく、任意の JavaScript への記述には使用されません。

### パラメーター {#parameters-11}

* **context**:オブジェクト

   エンコードするHTML。

### 例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS に対する保護として、HTML の href または src 属性値として記述する URL の不要部分を削除するヘルパーです。

注意：空の文字列が返される場合があります。

### パラメーター {#parameters-12}

* **context**:オブジェクト

   不要部分を削除する URL。

### 例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js の基本的概要 {#handlebars-js-basic-overview}

* Handlebars ヘルパーを呼び出すには、単純な識別子（ヘルパーの名前&#x200B;**）を使用し、それに続けて 0 個以上のパラメーターをスペースで区切って指定します。
* パラメーターには、単純な文字列、数値、ブール値、または JSON オブジェクトを指定し、オプションで最後のパラメーターとして一連のキー／値ペア（ハッシュ引数）を指定します。
* ハッシュ引数内のキーは単純な識別子にする必要があります。
* ハッシュ引数内の値は Handlebars 式（単純な識別子、パス、または文字列）です。
* 現在のコンテキスト `this`は、常に Handlebars ヘルパーで使用できます。
* コンテキストは、文字列、数値、ブール値、JSON データオブジェクトのいずれかです。
* `this.url` や `this.id` のように、現在のコンテキスト内にネストされているオブジェクトを context として渡すことができます（単純なヘルパーおよびブロックヘルパーを示す後述の例を参照）。

* ブロックヘルパーとは、テンプレート内の任意の場所から呼び出すことができる関数です。毎回、異なるコンテキストで、0 回以上テンプレートのブロックを呼び出すことができます。 次の間のコンテキストを含みます。 {{#*name*}} and {{/*name*}}.

* Handlebars では、ヘルパーに対する最後のパラメーターとして「options」を使用します。特別なオブジェクト「options」が次を含みます

   * オプションのプライベートデータ (options.data)
   * 呼び出しからのオプションのキーと値のプロパティ (options.hash)
   * 自身を呼び出す機能 (options.fn())
   * 逆関数を呼び出す機能 (options.inverse())

* ヘルパーから返される HTML 文字列コンテンツは SafeString になるようにすることをお勧めします。

### Handlebars.js ドキュメントで紹介されている単純なヘルパーの例を次に示します。 {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

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
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>投稿！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js ドキュメントで紹介されているブロックヘルパーの例を次に示します。 {#an-example-of-a-block-helper-from-handlebars-js-documentation}

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
&lt;li>&lt;a href=&quot;/people/2&quot;>イェフダ&lt;/a>&lt;/li>
&lt;/ul>

## カスタム SCF ヘルパー {#custom-scf-helpers}

カスタムヘルパーは、特にデータを渡す場合に、クライアント側だけでなくサーバー側で実装する必要があります。SCF の場合、ページが要求されたときにサーバーが特定のコンポーネントのHTMLを生成するので、ほとんどのテンプレートはサーバー側でコンパイルおよびレンダリングされます。

### サーバー側カスタムヘルパー {#server-side-custom-helpers}

カスタム SCF ヘルパーをサーバー側に実装して登録するには、Java インターフェイスを実装するだけです [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)、作成 [OSGi サービス](../../help/sites-developing/the-basics.md#osgi) OSGi バンドルの一部としてインストールします。

次に例を示します。

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

クライアント側ヘルパーは、`Handlebars.registerHelper()` () を呼び出すことによって登録する Handlebars スクリプトです。次に例を示します。

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

カスタムのクライアント側ヘルパーは、カスタムのクライアントライブラリに追加する必要があります。
clientlib の条件は次のとおりです。

* 依存関係を含める `cq.social.scf`.
* Handlebars が読み込まれた後に読み込みます。
* Be [含む](clientlibs.md).

注意：SCF ヘルパーは、 `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ 機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|  | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
