---
title: SCF Handlebars ヘルパー
description: SCF での作業を容易にする Handlebars ヘルパーメソッド
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 4%

---

# SCF Handlebars ヘルパー {#scf-handlebars-helpers}

| **[⇐機能の基本事項](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |

Handlebars ヘルパー（ヘルパー）は、SCF コンポーネントの操作を容易にするために Handlebars スクリプトから呼び出すことができるメソッドです。

この実装には、クライアントサイドとサーバーサイドの定義が含まれています。 また、開発者がカスタムヘルパーを作成することもできます。

AEM Communitiesで提供されるカスタム SCF ヘルパーは、[ クライアントライブラリ ](../../help/sites-developing/clientlibs.md) で定義されます。

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>[ 最新の Communities 機能パック ](deploy-communities.md#latestfeaturepack) をインストールしてください。

## 短縮 {#abbreviate}

maxWords および maxLength プロパティに準拠した、略語の文字列を返すヘルパー。

短縮する文字列はコンテキストとして提供されます。 コンテキストが指定されていない場合は、空の文字列が返されます。

最初に、コンテキストが maxLength までトリミングされ、次にコンテキストが単語に分割されて maxWords に縮小されます。

safeString が true に設定されている場合、返される文字列は SafeString です。

### パラメーター {#parameters}

* **context**：文字列

  （オプション）デフォルトは空の文字列です

* **maxLength**：数値

  （オプション）デフォルトは、コンテキストの長さです。

* **maxWords**：数値

  （オプション）デフォルトは、トリミングされた文字列の単語数です。

* **safeString**：ブール値

  （オプション） true の場合、Handlebars.SafeString （）を返します。 デフォルトは false です。

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

div の下に 2 つのスパンを追加するヘルパー。1 つはフルテキスト用、もう 1 つは less テキスト用で、2 つのビューを切り替える機能があります。

### パラメーター {#parameters-1}

* **context**：文字列

  （オプション）デフォルトは空の文字列です。

* **numChars**：数値

  （任意）フルテキストを表示しない場合に表示する文字数。 初期設定は 100 です。

* **moreText**：文字列

  （オプション）表示するテキストが他にもあることを示す、表示するテキスト。 デフォルトは「その他」です。

* **ellipsesText**：文字列

  （任意）非表示のテキストがあることを示すために表示するテキストです。 デフォルトは「。..」です。

* **safeString**：ブール値

  （任意）結果を返す前に Handlebars.SafeString （）を適用するかどうかを示すブール値。 デフォルトは false です。

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

  （任意） 1970 年 1 月 1 日（エポック）からオフセットされたミリ秒値。 デフォルトは現在の日付です。

* **format**：文字列

  （任意）適用する日付形式。 デフォルトは「`YYYY-MM-DDTHH:mm:ss.sssZ`」で、結果は「`2015-03-18T18:17:13-07:00`」と表示されます

### 例 {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## 次に等しい {#equals}

等値条件に応じてコンテンツを返すヘルパー。

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

[WCM モード ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) の現在の値を、モードの文字列区切りリストに対してテストするブロックヘルパー。

### パラメーター {#parameters-4}

* **context**：文字列

  （オプション）翻訳する文字列。 デフォルト値が指定されていない場合は必須です。

* **mode**：文字列

  （オプション）設定されている場合にテストする [WCM モード ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) のコンマ区切りリスト。

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

[JavaScript コードでの文字列の国際化 ](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code) も参照してください。

### パラメーター {#parameters-5}

* **context**：文字列

  （オプション）翻訳する文字列。 デフォルト値が指定されていない場合は必須です。

* **default**：文字列

  （任意）翻訳するデフォルトの文字列。 コンテキストが指定されていない場合は必須です。

* **comment**：文字列

  （オプション）翻訳のヒント

### 例 {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## 包含 {#include}

コンポーネントを存在しないリソースとしてテンプレートに含めるためのヘルパー。

このメソッドを使用すると、JCR ノードとして追加されたリソースの場合よりも、プログラムによるリソースのカスタマイズが容易になります。 [ コミュニティコンポーネントを追加または含める ](scf.md#add-or-include-a-communities-component) を参照してください。

組み込むことができる Communities コンポーネントは一部のみです。<!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

このヘルパーは、サーバーサイドでのみ使用でき、JSP スクリプトに対して [cq:include](../../help/sites-developing/taglib.md) のような機能を提供します。

### パラメーター {#parameters-6}

* **context**：文字列またはオブジェクト

  （相対パスを指定しない場合はオプション）

  `this` を使用して、現在のコンテキストを渡します。

  `this.id` を使用して、リクエストされた resourceType をレンダリングするための `id` にあるリソースを取得します。

* **resourceType**：文字列

  （オプション）リソースタイプのデフォルトは、コンテキストのリソースタイプです。

* **template**：文字列

  コンポーネントスクリプトへのパス。

* **path**：文字列

  （必須） リソースへのパス。 パスが相対パスの場合は、コンテキストを指定する必要があります。指定しない場合は、空の文字列が返されます。

* **authoringDisabled**：ブール値

  （オプション）デフォルトは false です。 内部のみで使用します。

### 例 {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

`this.id` + /comments に新しいコメントコンポーネントが含まれます。

## IncludeClientLib {#includeclientlib}

AEM html クライアントライブラリ（js、css または theme の各ライブラリ）を含むヘルパー。 異なるタイプ（例：js と css）の複数のインクルードがある場合は、Handlebars スクリプトでこのタグを複数回使用する必要があります。

このヘルパーはサーバーサイドにのみ適しており、JSP スクリプトには [ui:includeClientLib](../../help/sites-developing/taglib.md) のような機能が用意されています。

### パラメーター {#parameters-7}

* **categories**：文字列

  （オプション）クライアントライブラリのカテゴリのコンマ区切りのリスト。 指定されたカテゴリのJavaScriptおよび CSS ライブラリをすべて含めます。 テーマ名はリクエストから抽出されます。

* **theme**：文字列

  （オプション）クライアントライブラリのカテゴリのコンマ区切りのリスト。 指定されたカテゴリに対して、すべてのテーマ関連ライブラリ（CSS と JS の両方）を含めます。 テーマ名はリクエストから抽出されます。

* **js**：文字列

  （オプション）クライアントライブラリのカテゴリのコンマ区切りのリスト。 指定されたカテゴリのすべてのJavaScript ライブラリが含まれます。

* **css**：文字列

  （オプション）クライアントライブラリのカテゴリのコンマ区切りのリスト。 指定されたカテゴリのすべての CSS ライブラリが含まれます。

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

カットオフポイントまでの時間を表示するヘルパー。この時間を超えると、通常の日付形式が表示されます。

次に例を示します。

* 12 時間前
* 7 日前

### パラメーター {#parameters-8}

* **context**：数値

  過去の時間を「現在」と比較します。 時間は、1970 年 1 月 1 日（エポック）からオフセットされたミリ秒単位の値で表されます。

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

XSS から保護するために、HTML要素コンテンツのソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではないため、属性値の書き込みに使用しないでください。

### パラメーター {#parameters-9}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

XSS を防ぐために、HTML属性値に書き込むためのソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではないため、アクションにつながる属性（href、src、イベントハンドラー）の記述には使用しないでください。

### パラメーター {#parameters-10}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

XSS 対策としてJavaScript文字列コンテンツへの書き込み用のソース文字列をエンコードするヘルパー。

メモ：このヘルパーはバリデーターではないため、任意のJavaScriptへの書き込みに使用しないでください。

### パラメーター {#parameters-11}

* **context**: オブジェクト

  エンコードするHTML。

### 例 {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

XSS から保護するために、HTML href または srce 属性値として書き込む URL の非表示情報をすべて削除するヘルパー。

メモ：このヘルパーは、空の文字列を返す場合があります。

### パラメーター {#parameters-12}

* **context**: オブジェクト

  不要部分を削除する URL。

### 例 {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js の基本概要 {#handlebars-js-basic-overview}

* Handlebars ヘルパー呼び出しは、単純な識別子（ヘルパーの *名前* の後に、0 個以上のスペース区切りパラメーターを続けたものです。
* パラメーターは、単純な文字列、数値、ブール値、JSON オブジェクトのほか、オプションでキーと値のペアのシーケンス（ハッシュ引数）を最後のパラメーターとすることができます。
* ハッシュ引数のキーは、単純な識別子にする必要があります。
* ハッシュ引数の値は Handlebars 式（単純な識別子、パス、文字列）です。
* 現在のコンテキスト `this` は、Handlebars ヘルパーで常に使用できます。
* コンテキストには、文字列、数値、ブール値、JSON データオブジェクトを使用できます。
* 現在のコンテキスト内にネストされたオブジェクト（`this.url` や `this.id` など）をコンテキストとして渡すことができます（以下の単純ヘルパーとブロックヘルパーの例を参照）。

* ブロックヘルパーは、テンプレートのどこからでも呼び出すことができる関数です。 テンプレートのブロックを、異なるコンテキストで 0 回以上呼び出すことができます。 `{{#*name*}}` と `{{/*name*}}` の間のコンテキストが含まれます。

* Handlebars は、「options」という名前のヘルパーに最終的なパラメーターを提供します。 特殊オブジェクト「options」には次が含まれます

   * オプションの非公開データ（options.data）
   * 呼び出しのオプションのキー値プロパティ（options.hash）
   * 自身を呼び出す機能（options.fn （））
   * 自身の逆を呼び出す機能（options.inverse （））

* ヘルパーから返されるHTML文字列コンテンツは、SafeString にすることをお勧めします。

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

次をレンダリングします。

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Post!&lt;/a>&lt;/li>
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

次をレンダリングします。
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;> アラン &lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## カスタム SCF ヘルパー {#custom-scf-helpers}

カスタムヘルパーは、サーバーサイドとクライアントサイドで実装する必要があります（特に、データを渡す場合）。 SCF では、ページが要求されると、サーバーが特定のコンポーネントのHTMLを生成するので、ほとんどのテンプレートがサーバーサイドでコンパイルおよびレンダリングされます。

### サーバーサイドのカスタムヘルパー {#server-side-custom-helpers}

カスタムの SCF ヘルパーをサーバーサイドで実装して登録するには、Java™ インターフェイス [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html) を実装し、[OSGi サービス ](../../help/sites-developing/the-basics.md#osgi) として作成してから、OSGi バンドルの一部としてインストールします。

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
>サーバーサイド用に作成したヘルパーは、クライアントサイドにも作成する必要があります。
>
>このコンポーネントは、ログインしたユーザーに対してクライアントサイドで再レンダリングされます。クライアントサイドのヘルパーが見つからない場合、このコンポーネントは表示されなくなります。

### クライアントサイドのカスタムヘルパー {#client-side-custom-helpers}

クライアントサイドヘルパーは、`Handlebars.registerHelper()` を呼び出して登録された Handlebars スクリプトです。
次に例を示します。

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
クライアントライブラリには次の条件があります。

* `cq.social.scf` に依存関係を含めます。
* Handlebars の読み込み後に読み込みます。
* [ この値を含む ](clientlibs.md)。

注記：SCF ヘルパーは `/etc/clientlibs/social/commons/scf/helpers.js` で定義されます。

| **[⇐機能の基本事項](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
