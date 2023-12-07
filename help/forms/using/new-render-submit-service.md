---
title: 新しいレンダリングと送信サービス
description: Workbench でレンダリングサービスと送信サービスを定義して、XDP フォームを、アクセス元のデバイスに応じてHTMLまたはPDFとしてレンダリングします。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 45%

---

# 新しいレンダリングと送信サービス{#new-render-and-submit-service}

## はじめに {#introduction}

Workbench で `AssignTask` 操作を定義する場合は、特定のフォーム（XDP または PDF フォーム）を指定します。また、アクションプロファイルを介して一連のレンダリングサービスと送信サービスを指定します。

XDP は、フォームまたはHTMLフォームとしてPDFできます。 新しい機能には、次の機能が含まれます。

* XDP フォームをレンダリングしてHTMLとして送信
* XDP フォームをデスクトップ上でPDFとして、またモバイルデバイス ( 例えばiPad) 上でHTMLとしてレンダリングして送信する

### 新しいHTMLFormsサービス {#new-html-forms-service}

新しいHTMLFormsサービスは、Formsの新機能を使用して、XDP フォームのHTMLとしてのレンダリングをサポートします。 新しいHTMLFormsサービスでは、次のメソッドを公開します。

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

モバイルフォームプロファイルの詳細については、 [カスタムプロファイルの作成](/help/forms/using/custom-profile.md).

## 新しいHTMLフォームのレンダリングおよび送信プロセス {#new-html-form-render-amp-submit-processes}

すべての「AssignTask」操作に対して、フォームのレンダリングと送信プロセスを指定します。 カスタム処理ができるように、これらのプロセスは TaskManager `renderForm` および `submitForm` API によって呼び出されます。新しいプロセスフォームのためのこれらのプロセスのHTML:

### 新しいHTMLフォームをレンダリング {#render-a-new-html-form}

すべてのレンダリングプロセスと同様に、HTMLをレンダリングする新しいプロセスには次の I/O パラメータがあります。

必要情報 - `taskContext`

出力 - `runtimeMap`

出力 - `outFormDoc`

このメソッドは、NewHTMLFormsService の `renderHTMLForm` API の正確な動作をシミュレーションします。これは、`generateFormURL` API を呼び出してフォームの HTML 表示の URL を取得します。その後、次のキーまたは値を使用して runtimeMap を設定します。

new html form = true

newHTMLFormURL = `generateFormURL` API を呼び出した後で返された URL

### 新しいHTMLフォームを送信 {#submit-a-new-html-form}

新しいHTMLフォームを送信するこのプロセスは、次の I/O パラメータで動作します。

必要情報 - `taskContext`

出力 - `runtimeMap`

出力 - `outputDocument`

プロセスは、`outputDocument` を `taskContext` から取得した `inputDocument` に設定します。

## デフォルトのレンダリングまたは送信プロセスとアクションプロファイル {#default-render-or-submit-processes-and-action-profiles}

デフォルトのレンダリングと送信サービスを使用すると、デスクトップでPDFをレンダリングし、モバイルデバイス (iPad) でHTMLをレンダリングするサポートが可能になります。

### デフォルトのレンダリングフォーム {#default-render-form}

このプロセスでは、XDP フォームを複数のプラットフォーム上でシームレスにレンダリングします。 プロセスは、`taskContext` からユーザーエージェントを取得し、データを使用して HTML または PDF のいずれかをレンダリングするプロセスを呼び出します。

![default-render-form](assets/default-render-form.png)

### デフォルトの送信フォーム {#default-submit-form}

このプロセスでは、複数のプラットフォーム上で XDP フォームをシームレスに送信します。 `taskContext` からユーザーエージェントを取得し、データを使用して HTML または PDF のいずれかを送信するプロセスを呼び出します。

![default-submit-form](assets/default-submit-form.png)

## モバイルフォームのレンダリングをPDFからHTMLに切り替える {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

ブラウザーは、Adobe AcrobatおよびAdobe Acrobat Reader用のプラグインを含む、NPAPI ベースのプラグインのサポートを徐々に廃止しています。 次の手順を使用して、モバイルフォームのレンダリングをPDFからHTMLに変更できます。

1. 有効なユーザーとして Workbench にログインします。
1. **File**／**Get Applications** を選択します。

   Get Applications ダイアログが表示されます。

1. モバイルフォームのレンダリングを変更する対象のアプリケーションを選択し、「**OK**」をクリックします。
1. レンダリングを変更する対象のプロセスを開きます。
1. 対象のスタートポイント／タスクを開き、「Presentation &amp; Data」セクションに移動して、「**Manage Action Profiles**」をクリックします。

   Manage Action Profiles ダイアログが表示されます。
1. デフォルトのレンダリングプロファイル設定を PDF から HTML に変更し、「**OK**」をクリックします。
1. プロセスをチェックインします。
1. 手順を繰り返して、他のプロセスのレンダリングを変更します。
1. 変更したプロセスに関連するアプリケーションをデプロイします。

### デフォルトのアクションプロファイル {#default-action-profile}

デフォルトのアクションプロファイルにより、XDP フォームがPDFとしてレンダリングされました。 この動作は、「デフォルトのレンダリングフォーム」と「デフォルトの送信フォーム」の処理を使用するように変更されました。

アクションプロファイルに関するよくある質問の一部を次に示します。

![gen_question_b_20](assets/gen_question_b_20.png) **どのようなレンダリング/ 送信プロセスが追加設定なしで使用できますか？**

* Guide のレンダリング（Guide は推奨されていません）
* Render Form ガイド
* レンダリングPDFフォーム
* レンダリングHTMLフォーム
* 新規HTMLフォームをレンダリング（新規）
* デフォルトのレンダリングフォーム（新規）

また、同等の送信プロセスにも対応します。

![gen_question_b_20](assets/gen_question_b_20.png) **どのようなアクションプロファイルが追加設定なしで使用できますか？**

XDP Formsの場合：

* デフォルト（新しい「デフォルトのレンダリング/送信」プロセスを使用したレンダリング/送信）

![gen_question_b_20](assets/gen_question_b_20.png) **フォームをデバイス上では HTML およびデスクトップ上では PDF にレンダリングされるようにするには、プロセスデザイナーは何を行う必要がありますか？**

何も。 デフォルトの「アクションプロファイル」が自動的に選択され、レンダリングのモードも自動的に処理されます。

![gen_question_b_20](assets/gen_question_b_20.png) **フォームをデスクトップ上で HTML にレンダリングされるようにするには、何を行う必要がありますか？**

ユーザーは、デフォルトプロファイルで HTML ラジオボタンを選択する必要があります。

![gen_question_b_20](assets/gen_question_b_20.png) **デフォルトのアクションプロファイルの動作を変更すると、アップグレードに何らかの影響がありますか？**

はい。デフォルトのアクションプロファイルに関連付けられた以前のレンダリングと送信サービスは異なるため、それらは既存のフォームのカスタマイズとして処理されます。「**デフォルトを復元**」をクリックすると、デフォルトのレンダリングと送信サービスが代わりに設定されます。

既存のレンダリングまたは送信PDFフォームサービスを変更した場合、またはカスタムサービス（custom1 など）を作成した場合に、HTMLレンディションで同じ機能を使用したい場合。 新しいレンダリングまたは送信サービス（custom2 など）をレプリケートし、これらに類似したカスタマイズを適用する必要があります。 次に、レンダリングまたは送信用の custom1 の代わりに custom2 サービスを使用して XDP のアクションプロファイルを変更します。

デバイス上では HTML、デスクトップ上では PDF にフォームをレンダリングする場合、プロセスデザイナーは何を行う必要がありますか？
デバイス上では HTML、デスクトップ上では PDF にフォームをレンダリングする場合、プロセスデザイナーは何を行う必要がありますか？
