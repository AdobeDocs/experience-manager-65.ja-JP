---
title: SCF Handlebars ヘルパー
description: Handlebars SCFの作業を促進するHelper メソッド
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 6%

---

# SCF Handlebars ヘルパー {#scf-handlebars-helpers}

| **[⇐機能エッセンシャル](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |

Handlebars Helpers （ヘルパー）は、SCF コンポーネントの操作を容易にするためにHandlebars スクリプトから呼び出せるメソッドです。

実装には、クライアントサイドとサーバーサイドの定義が含まれます。 開発者がカスタムヘルパーを作成することも可能です。

AEM Communitiesで配信されるカスタム SCF ヘルパーは、[&#x200B; クライアントライブラリ &#x200B;](../../help/sites-developing/clientlibs.md)で定義されます。

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>最新のコミュニティ機能パック [を必ずインストールしてください](deploy-communities.md#latestfeaturepack)。

## 省略形 {#abbreviate}

maxWordsおよびmaxLength プロパティに準拠した省略文字列を返すヘルパー。

省略化する文字列はコンテキストとして指定します。 コンテキストが指定されていない場合は、空の文字列が返されます。

まず、コンテキストがmaxLengthにトリミングされ、次にコンテキストが単語にスライスされ、maxWordsに縮小されます。

safeStringがtrueに設定されている場合、返される文字列はSafeStringです。

### パラメーター {#parameters}

* **context**：文字列

  （オプション）デフォルトは空の文字列です

* **maxLength**：数値

  （オプション）デフォルトはコンテキストの長さです。

* **maxWords**：数値

  （オプション）デフォルトは、トリミングされた文字列内の文字数です。

* **safeString**: ブール値

  （オプション） trueの場合、Handlebars.SafeString （）を返します。 デフォルトはfalseです。

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

2つのビューを切り替えることができる、divの下に2つのスパンを追加するヘルパー（1つはフルテキスト用、もう1つは少ないテキスト用）。

### パラメーター {#parameters-1}

* **context**：文字列

  （オプション）デフォルトは空の文字列です。

* **numChars**：番号

  （オプション）全文を表示しない場合に表示する文字数。 初期設定は 100 です。

* **moreText**：文字列

  （オプション）表示するテキストが多いことを示すテキスト。 デフォルトは「more」です。

* **ellipsesText**：文字列

  （オプション）非表示のテキストがあることを示す表示するテキスト。 デフォルトは「。..」

* **safeString**: ブール値

  （オプション）結果を返す前にHandlebars.SafeString （）を適用するかどうかを示すブール値。 デフォルトはfalseです。

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

書式設定された日付文字列を返すヘルパー。

### パラメーター {#parameters-2}

* **context**：数値

  （オプション） 1970年1月1日（epoch）からのミリ秒値のオフセット。 デフォルトは現在の日付です。

* **format**：文字列

  （オプション）適用する日付形式。 デフォルトは「`YYYY-MM-DDTHH:mm:ss.sssZ`」で、結果は「`2015-03-18T18:17:13-07:00`」と表示されます

### 例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 等号 {#equals}

等価条件に応じてコンテンツを返すヘルパー。

### パラメーター {#parameters-3}

* **lvalue**：文字列

  比較する左側の値。

* **rvalue**：文字列

  比較する右側の値。

### 例 {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

[WCM モード &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html)の現在の値を、文字列区切りのモードのリストに対してテストするブロックヘルパー。

### パラメーター {#parameters-4}

* **context**：文字列

  （オプション）翻訳する文字列。 デフォルトが指定されていない場合は必須です。

* **mode**：文字列

  （オプション）設定されている場合にテストする[WCM モード &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html)のコンマ区切りリスト。

### 例 {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

このヘルパーは、Handlebars ヘルパー「i18n」を上書きします。

JavaScript コードの文字列の国際化[も参照してください](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)。

### パラメーター {#parameters-5}

* **context**：文字列

  （オプション）翻訳する文字列。 デフォルトが指定されていない場合は必須です。

* **default**：文字列

  （オプション）翻訳するデフォルトの文字列。 コンテキストが指定されていない場合は必須です。

* **comment**：文字列

  （オプション）翻訳のヒント

### 例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 次を含む {#include}

テンプレート内の既存でないリソースとしてコンポーネントを含めるヘルパー。

このメソッドを使用すると、JCR ノードとして追加されたリソースよりも簡単に、リソースをプログラムによってカスタマイズできます。 [&#x200B; コミュニティコンポーネントを追加または含める](scf.md#add-or-include-a-communities-component)を参照してください。

一部のCommunities コンポーネントのみを含めることができます。<!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

このヘルパーは、サーバーサイドでのみ適切で、JSP スクリプトに[cq:include](../../help/sites-developing/taglib.md)と同様の機能を提供します。

### パラメーター {#parameters-6}

* **context**：文字列またはオブジェクト

  （相対パスを指定しない限り、オプション）

  現在のコンテキストを渡すには、`this`を使用します。

  要求されたresourceTypeのレンダリング用に`id`でリソースを取得するには、`this.id`を使用します。

* **resourceType**：文字列

  （オプション） リソースタイプのデフォルトは、コンテキストからリソースタイプに設定されます。

* **template**：文字列

  コンポーネントスクリプトへのパス。

* **path**：文字列

  （必須） リソースへのパス。 pathが相対パスの場合は、コンテキストを指定する必要があります。指定しない場合は、空の文字列が返されます。

* **authoringDisabled**: ブール値

  （オプション）デフォルトはfalseです。 内部使用のみ。

### 例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

`this.id` + /commentsに新しいコメントコンポーネントが含まれます。

## IncludeClientLib {#includeclientlib}

AEM html クライアントライブラリを含むヘルパー。js、css、テーマライブラリを指定できます。 jsやcssなど、異なるタイプの複数のインクルージョンの場合、このタグはHandlebars スクリプトで複数回使用する必要があります。

このヘルパーは、サーバーサイドでのみ適切で、JSP スクリプトに[ui:includeClientLib](../../help/sites-developing/taglib.md)と同様の機能を提供します。

### パラメーター {#parameters-7}

* **categories**：文字列

  （オプション）コンマ区切りのクライアントライブラリのカテゴリのリスト。 特定のカテゴリのすべてのJavaScriptおよびCSS ライブラリを含めます。 テーマ名はリクエストから抽出されます。

* **theme**：文字列

  （オプション）コンマ区切りのクライアントライブラリのカテゴリのリスト。 特定のカテゴリのすべてのテーマ関連ライブラリ（CSSとJSの両方）を含めます。 テーマ名はリクエストから抽出されます。

* **js**：文字列

  （オプション）コンマ区切りのクライアントライブラリのカテゴリのリスト。 特定のカテゴリのすべてのJavaScript ライブラリが含まれます。

* **css**：文字列

  （オプション）コンマ区切りのクライアントライブラリのカテゴリのリスト。 指定されたカテゴリのすべてのCSS ライブラリが含まれます。

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

カットオフポイントまでの経過時間を表示するヘルパー。その後、通常の日付形式が表示されます。

例：

* 12時間前
* 7日前

### パラメーター {#parameters-8}

* **context**：数値

  過去の時間を「今」と比較します。 時間は、1970年1月1日（エポック）からのオフセットされたミリ秒の値として表されます。

* **daysCutoff**：数値

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

XSSから保護するために、HTML要素のコンテンツのソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではなく、属性値の書き込みに使用しないでください。

### パラメーター {#parameters-9}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSSから保護するために、HTML属性値に書き込むためのソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではなく、実用的な属性（href、src、イベントハンドラー）の書き込みに使用しないでください。

### パラメーター {#parameters-10}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSSから保護するために、JavaScript文字列コンテンツに書き込むためのソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではなく、任意のJavaScriptへの書き込みに使用しないでください。

### パラメーター {#parameters-11}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSSから保護するために、HTMLのhrefまたはsrce属性値として書き込むURLをサニタイズするヘルパー。

メモ：このヘルパーは空の文字列を返す場合があります。

### パラメーター {#parameters-12}

* **context**: オブジェクト

  サニタイズするURL。

### 例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.jsの基本概要 {#handlebars-js-basic-overview}

* Handlebars ヘルパー呼び出しは、単純な識別子（ヘルパーの&#x200B;*name*）の後に、0個以上のスペース区切りパラメーターが続きます。
* パラメーターには、単純な文字列、数値、ブール値、JSON オブジェクトのほか、最後のパラメーターとしてキーと値のペア（ハッシュ引数）のオプションのシーケンスを指定できます。
* ハッシュ引数のキーは単純な識別子である必要があります。
* ハッシュ引数の値は、Handlebars式（単純な識別子、パス、または文字列）です。
* 現在のコンテキスト `this`は、Handlebars ヘルパーにいつでも使用できます。
* コンテキストは、文字列、数値、ブール値、またはJSON データオブジェクトです。
* 現在のコンテキスト内にネストされたオブジェクトを、`this.url`や`this.id`などのコンテキストとして渡すことができます（次の単純ヘルパーとブロックヘルパーの例を参照）。

* ブロックヘルパーは、テンプレート内の任意の場所から呼び出すことができる関数です。 テンプレートのブロックは、毎回異なるコンテキストで0回以上呼び出すことができます。 `{{#*name*}}`と`{{/*name*}}`の間のコンテキストが含まれています。

* Handlebarsは、「options」という名前のヘルパーに最終的なパラメーターを提供します。 特殊オブジェクト「options」には

   * オプションのプライベートデータ（options.data）
   * 呼び出し（options.hash）からのオプションのキー値プロパティ
   * 自分自身を呼び出す機能（options.fn （））
   * 自身の逆を呼び出す機能（options.inverse （））

* ヘルパーから返されるHTML文字列コンテンツはSafeStringであることをお勧めします。

### Handlebars.js ドキュメントのシンプルなヘルパーの例： {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

レンダリングされます：

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>投稿！&lt;/a>&lt;/li>
&lt;/ul>

### Handlebars.js ドキュメントのブロックヘルパーの例： {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

レンダリングされます：
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## カスタム SCF ヘルパー {#custom-scf-helpers}

カスタムヘルパーは、特にデータを渡す際に、サーバーサイドとクライアントサイドに実装する必要があります。 SCFの場合、ほとんどのテンプレートは、ページが要求されたときに特定のコンポーネントのHTMLがサーバー側で生成されるため、サーバー側でコンパイルおよびレンダリングされます。

### サーバーサイドのカスタムヘルパー {#server-side-custom-helpers}

サーバーサイドでカスタム SCF ヘルパーを実装して登録するには、Java™ インターフェイス [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)を実装し、[OSGi サービス &#x200B;](../../help/sites-developing/the-basics.md#osgi)にして、OSGi バンドルの一部としてインストールします。

例：

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
>サーバーサイド用に作成されたヘルパーも、クライアントサイド用に作成する必要があります。
>
>コンポーネントは、ログインしたユーザーのクライアントサイドで再レンダリングされ、クライアントサイドヘルパーが見つからない場合、コンポーネントは消えます。

### クライアントサイドのカスタムヘルパー {#client-side-custom-helpers}

クライアント側ヘルパーは、`Handlebars.registerHelper()`を呼び出して登録されたHandlebars スクリプトです。
例：

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

カスタムクライアントサイドヘルパーは、カスタムクライアントライブラリに追加する必要があります。
clientlibは以下を行う必要があります。

* `cq.social.scf`への依存関係を含めます。
* Handlebarsが読み込まれた後に読み込みます。
* [を含める](clientlibs.md)。

注意：SCF ヘルパーは`/etc/clientlibs/social/commons/scf/helpers.js`で定義されています。

| **[⇐機能エッセンシャル](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
