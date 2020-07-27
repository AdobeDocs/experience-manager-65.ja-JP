---
title: フォームポータルで送信済みフォームを操作するための API
seo-title: フォームポータルで送信済みフォームを操作するための API
description: AEM Forms はフォームポータルで送信済みフォームデータに対してクエリーやアクションを実行する際に使用できる API を提供します。
seo-description: AEM Forms はフォームポータルで送信済みフォームデータに対してクエリーやアクションを実行する際に使用できる API を提供します。
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 95%

---


# フォームポータルで送信済みフォームを操作するための API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms はフォームポータル経由で送信されたフォームデータに対してクエリーを実行する際に使用できる API を提供します。また、この文書で説明されている API を使用し、送信済みフォームに対してコメントを投稿したりプロパティを更新したりできます。

>[!NOTE]
>
>Users who will invoke the APIs must be added to the reviewers group as described in [Associating submission reviewers to a form](/help/forms/using/adding-reviewers-form.md).

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

すべての有効なフォームのリストを返します。

### URL パラメーター {#url-parameters}

この API はその他のパラメーターを必要としません。

### 回答 {#response}

この応答オブジェクトにはフォーム名とそのリポジトリパスを含む JSON 配列が含まれています。応答の構造は次のとおりです。

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 例 {#example}

**要求 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**応答**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

すべての送信済みフォームの詳細を返します。ただし、URL パラメーターを使用して結果を制限できます。

### URL パラメーター {#url-parameters-1}

要求 URL で次のパラメーターを指定します。

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>フォームが常駐する CRX リポジトリパスを指定します。フォームパスを指定しない場合、空の応答を返します。<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (オプション)</td>
   <td>結果セットのインデックスでスタートポイントを指定します。デフォルト値は <strong>0</strong> です。</td>
  </tr>
  <tr>
   <td><code>limit</code> (オプション)</td>
   <td>結果の数を制限します。デフォルト値は <strong>30</strong> です。</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (オプション)</td>
   <td>結果を並べ替えるプロパティを指定します。デフォルト値は <strong>jcr:lastModified</strong> で、最終変更時刻に基づいて結果を並べ替えます。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (オプション)</td>
   <td>結果を並べ替える順序を指定します。デフォルト値は <strong>desc</strong> で、結果を降順で並べ替えます。<code>asc</code> を指定すると、結果を昇順で並べ替えできます。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (オプション)</td>
   <td>結果に含めるフォームプロパティのコンマ区切りリストを指定します。デフォルトのプロパティは次のとおりです。<br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (オプション)</td>
   <td>フォームプロパティで指定した値で検索し、一致する値を持つフォームを返します。デフォルト値は <strong>""</strong> です。</td>
  </tr>
 </tbody>
</table>

### 回答 {#response-1}

応答オブジェクトには指定したフォームの詳細を含む JSON 配列が含まれています。応答の構造は次のとおりです。

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 例 {#example-1}

**要求 URL**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**応答**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

指定した送信インスタンスにコメントを追加します。

### URL パラメーター {#url-parameters-2}

要求 URL で次のパラメーターを指定します。

| パラメーター | 説明 |
|---|---|
| `submitID` | 送信インスタンスに関連付けられているメタデータ ID を指定します。 |
| `Comment` | 指定した送信インスタンスに追加するコメントのテキストを指定します。 |

### 回答 {#response-2}

コメントが正常に投稿されるとコメント ID を返します。

### 例 {#example-2}

**要求 URL**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**応答**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments   {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

指定した送信インスタンスに投稿したすべてのコメントを返します。

### URL パラメーター {#url-parameters-3}

要求 URL で次のパラメーターを指定します。

| パラメーター | 説明 |
|---|---|
| `submitID` | 送信インスタンスのメタデータ ID を指定します。 |

### 回答 {#response-3}

応答オブジェクトには、指定した送信 ID に関連付けられているすべてのコメントを含む JSON 配列が含まれています。応答の構造は次のとおりです。

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 例 {#example-3}

**要求 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**応答**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

指定した送信済みフォームインスタンスの指定したプロパティの値を更新します。

### URL パラメーター {#url-parameters-4}

要求 URL で次のパラメーターを指定します。

| パラメーター | 説明 |
|---|---|
| `submitID` | 送信インスタンスに関連付けられているメタデータ ID を指定します。 |
| `property` | 更新対象のフォームプロパティを指定します。 |
| `value` | 更新対象のフォームプロパティの値を指定します。 |

### 回答 {#response-4}

投稿された更新に関する情報を持つ JSON オブジェクトを返します。

### 例 {#example-4}

**要求 URL**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**応答**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```

