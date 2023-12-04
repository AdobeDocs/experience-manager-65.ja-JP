---
title: アダプティブフォームの非同期送信
description: アダプティブフォームの非同期送信を設定する方法を説明します。
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: bd0589e2-b15a-4f0e-869c-2da4760b1ff4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 70%

---

# アダプティブフォームの非同期送信{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html) |
| AEM 6.5 | この記事 |

これまでの Web フォームは、同期送信用に設定されていました。同期送信では、ユーザーがフォームを送信すると、確認確認ページ、「ありがとうございます」ページ、または送信エラーが発生した場合はエラーページにリダイレクトされます。 しかし、現在では、単一ページアプリケーションなどの最新の Web エクスペリエンスが広く使用されるようになっています。こうしたアプリケーションでは、バックグラウンドでクライアントとサーバー間の通信が実行されている間は、Web ページが静的な状態のままになります。非同期送信を設定することにより、アダプティブフォームでこうした Web エクスペリエンスを実現することができます。

非同期送信では、ユーザーがフォームを送信すると、フォーム開発者は、別のフォームや Web サイトの別のセクションにリダイレクトするなど、別のエクスペリエンスを提供します。また、作成者は、別のデータストアへのデータ送信やカスタム解析エンジンの追加など、別のサービスを差し込むこともできます。非同期送信がある場合、アダプティブフォームは単一ページアプリケーションのように動作します。送信されたフォームデータがサーバー上で検証されても、フォームが再読み込みされないか、URL が変更されないからです。

アダプティブフォームでの非同期送信の詳細については、以下を参照してください。

## 非同期送信の設定 {#configure}

アダプティブフォームの非同期送信を設定するには、次の手順を実行します。

1. アダプティブフォームのオーサリングモードで、フォームコンテナオブジェクトを選択し、 ![cmppr1](assets/cmppr1.png) をクリックしてプロパティを開きます。
1. 「**[!UICONTROL 送信]**」プロパティセクションで、「**[!UICONTROL 非同期送信を使用]**」を有効にします。
1. 「**[!UICONTROL 送信時]**」セクションで、フォームが正常に送信された場合に実行するオプションを以下のどちらかから選択します。

   * **[!UICONTROL URL にリダイレクト]**：フォームの送信時に、指定の URL またはページにリダイレクトされます。「**[!UICONTROL リダイレクト URL / パス]**」フィールドで URL を指定することも、ページのパスを参照して選択することもできます。
   * **[!UICONTROL メッセージを表示]**：フォームの送信時にメッセージを表示します。「メッセージを表示」オプションの下のテキストフィールドにメッセージを入力できます。このテキストフィールドは、リッチテキスト形式をサポートします。

1. 選択 ![check-button1](assets/check-button1.png) をクリックしてプロパティを保存します。

## 非同期送信の仕組み {#how-asynchronous-submission-works}

AEM Forms には、すぐに使用できる、フォーム送信の成功および失敗ハンドラーが用意されています。ハンドラーは、サーバー応答に基づいて実行されるクライアントサイド関数です。フォームが送信されると、データが検証のためにサーバーに転送され、送信の成功またはエラーイベントに関する情報と共に、応答がクライアントに返されます。この情報は、関連するハンドラーにパラメーターとして渡され、関数が実行されます。

また、フォームの作成者と開発者は、フォームレベルでルールを記述して、デフォルトのハンドラーを上書きできます。詳しくは、「[ルールを使用したデフォルトハンドラーの上書き](#custom)」を参照してください。

最初に、成功およびエラーイベントに対するサーバー応答について説明します。

### 送信成功イベントに対するサーバー応答 {#server-response-for-submission-success-event}

送信成功イベントに対するサーバー応答は、以下のような構造になっています。

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

フォームの送信が成功した場合のサーバーの応答には、次のものが含まれます。

* フォームデータのフォーマットタイプ：XML または JSON
* XML 形式または JSON 形式のフォームデータ
* フォームに設定された、ページにリダイレクトするかメッセージを表示するために選択されたオプション
* フォームに設定された、ページの URL またはメッセージの内容

成功ハンドラーは、サーバー応答を読み取り、それに応じて、設定されたページ URL にリダイレクトしたりメッセージを表示したりします。

### 送信エラーイベントに対するサーバー応答 {#server-response-for-submission-error-event}

送信エラーイベントに対するサーバー応答は、以下のような構造になっています。

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

フォームの送信時にエラーが発生した場合のサーバーの応答には、次のものが含まれます。

* エラーの理由、失敗した CAPTCHA またはサーバーサイド検証
* 検証が失敗したフィールドの SOM 式と、対応するエラーメッセージを含む、エラーオブジェクトのリスト

エラーハンドラーは、サーバー応答を読み取り、それに応じて、フォーム上にエラーメッセージを表示します。

## ルールを使用したデフォルトハンドラーの上書き {#custom}

フォーム開発者と作成者は、フォームレベルで、コードエディターでルールを記述して、デフォルトのハンドラーを上書きできます。 成功イベントおよびエラーイベントに対するサーバー応答は、フォームレベルで公開されます。開発者は、ルール内で `$event.data` を使用してサーバー応答にアクセスできます。

成功イベントとエラーイベントを処理するためのルールをコードエディターで記述するには、以下の手順を実行します。

1. アダプティブフォームをオーサリングモードで開き、任意のフォームオブジェクトを選択して、 ![edit-rules1](assets/edit-rules1.png) をクリックして、ルールエディターを開きます。
1. 選択 **[!UICONTROL フォーム]** フォームオブジェクトツリーで「 」を選択し、 **[!UICONTROL 作成]**.
1. 選択 **[!UICONTROL コードエディター]** 「モード選択」ドロップダウンから、次の操作をおこないます。
1. コードエディターで、「 **[!UICONTROL コードを編集]**. 選択 **[!UICONTROL 編集]** をクリックします。
1. 選択 **[!UICONTROL 送信成功]** または **[!UICONTROL 送信中にエラーが発生しました]** から **[!UICONTROL イベント]** 」ドロップダウンリストから選択できます。
1. 選択したイベントのルールを作成し、「 」を選択します。 **[!UICONTROL 完了]** 」と入力してルールを保存します。
