---
title: API を使用した Web ページ上のフォームの一覧表示
seo-title: API を使用した Web ページ上のフォームの一覧表示
description: プログラムから Forms Manager にクエリを 実行し、フィルターが適用されたフォームを取得して、自分の Web ページに表示します。
seo-description: プログラムから Forms Manager にクエリを 実行し、フィルターが適用されたフォームを取得して、自分の Web ページに表示します。
uuid: e51cb2d4-816f-4e6d-a081-51e4999b00ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 515ceaf6-c132-4e1a-b3c6-5d2c1ccffa7c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 84%

---


# API を使用した Web ページ上のフォームの一覧表示 {#listing-forms-on-a-web-page-using-apis}

AEM Forms では REST ベースの検索 API を備えており、これにより Web 開発者はクエリーを実行し、検索条件に合う一連のフォームを取得できます。API を使用することで、様々なフィルターに基づいてフォームを検索できます。応答オブジェクトには、フォームの属性、プロパティ、フォームのレンダリングエンドポイントなどがあります。

To search forms using the REST API, send a GET request to the server at `https://'[server]:[port]'/libs/fd/fm/content/manage.json` with query parameters described below.

## クエリーパラメーター {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>属性名<br /> </strong></td>
   <td><strong>説明<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>呼び出す関数を指定します。フォームを検索するには、<code>func </code> 属性の値を <code>searchForms</code> に設定します。</p> <p>例： <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>注意：</strong><em>このパラメーターは必須です。</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>フォームを検索するアプリケーションパスを指定します。デフォルトでは、appPath 属性はルートノードレベルで使用可能なすべてのアプリケーションを検索します。<br /> </p> <p>1 つの検索クエリーで複数のアプリケーションパスを指定できます。複数のパスを区切る場合はパイプ（|）文字を使用します。 </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>アセットと一緒に取得するプロパティを指定します。アスタリスク（*）を使用するとすべてのプロパティを一度に取得できます。複数のプロパティを指定する場合はパイプ（|）演算子を使用します。 </p> <p>例： <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>注意</strong>： </p>
    <ul>
     <li><em>ID、パス、名前などのプロパティは、常に取得されます。 </em></li>
     <li><em>アセットごとにプロパティのセットが異なります。formUrl、pdfUrl、guideUrl などのプロパティは cutPoints 属性に依存しません。これらのプロパティはアセットタイプに依存し、アセットタイプに応じて取得されます。 </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>検索結果とともに取得する関連アセットを指定します。以下のオプションからいずれか 1 つを選択して、関連アセットを取得できます。
    <ul>
     <li><strong>NO_RELATION</strong>：関連アセットを取得しません。</li>
     <li><strong>IMMEDIATE</strong>：検索結果に直接関連するアセットを取得します。</li>
     <li><strong>ALL</strong>：直接関連するアセットと間接的に関連するアセットを取得します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>取得するフォームの最大数を指定します。</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>開始からスキップするフォームの数を指定します。</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>指定した条件に一致する検索結果を返すかどうかを指定します。 </td>
  </tr>
  <tr>
   <td>statements</td>
   <td><p>文のリストを指定します。クエリーは、JSON 形式で指定した文のリストに対して実行されます。 </p> <p>例：</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>上記の例では、 </p>
    <ul>
     <li><strong>name</strong>：検索するプロパティの名前を指定します。</li>
     <li><strong>value</strong>：検索するプロパティの値を指定します。</li>
     <li><strong>operator</strong>：検索時に適用する演算子を指定します。次の演算子がサポートされています。
      <ul>
       <li>EQ — 次と等しい </li>
       <li>NEQ - 次と等しくない</li>
       <li>GT - 次の値より大きい</li>
       <li>LT - 次の値より小さい</li>
       <li>GTEQ - 次の値よりも大きいか等しい</li>
       <li>LTEQ - 次の値よりも小さいか等しい</li>
       <li>CONTAINS - B が A の一部である場合、A に B が含まれる</li>
       <li>FULLTEXT - フルテキスト検索</li>
       <li>STARTSWITH - B が A の最初の部分である場合、A は B で始まる</li>
       <li>ENDSWITH - B が A の最後の部分である場合、A は B で終わる</li>
       <li>LIKE - LIKE 演算子を実装する</li>
       <li>AND - 複数の文を組み合わせる</li>
      </ul> <p><strong>注意：</strong><em>GT、LT、GTEQ、LTEQ 演算子は、LONG、DOUBLE、DATE などの線形型のプロパティに適用されます。</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>orderings<br /> </td>
   <td><p>検索結果の順序条件を指定します。条件は JSON 形式で定義されます。複数のフィールドの検索結果を並べ替えることができます。検索結果は、フィールドがクエリー内で表示されている順番のとおりに並べ替えられています。</p> <p>例：</p> <p>タイトルプロパティで昇順に並べ替えられたクエリ結果を取得するには、次のパラメーターを追加します。 </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>：検索結果の並べ替えに使用するプロパティの名前を指定します。</li>
     <li><strong>criteria</strong>：結果の順序を指定します。順序属性には次の値を指定できます。
      <ul>
       <li>ASC - ASC を使用すると、結果を昇順に並べ替えます。<br /> </li>
       <li>DES - DESを使用して、結果を降順に並べ替えます。</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>バイナリコンテンツを取得するかどうかを指定します。The <code>includeXdp</code> attribute is applicable for assets of type <code>FORM</code>, <code>PDFFORM</code>, and <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>発行されたすべてのアセットから取得するアセットのタイプを指定します。複数のアセットタイプを指定するには、パイプ（|）演算子を使用します。有効なアセットタイプは FORM、PDFFORM、PRINTFORM、RESOURCE、GUIDE です。</td>
  </tr>
 </tbody>
</table>

## サンプルリクエスト {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :“lastModifiedDate“:”order”:”ASC”}]
```

## サンプル応答 {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)