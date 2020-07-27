---
title: アダプティブフォームの非同期送信
seo-title: アダプティブフォームの非同期送信
description: ここでは、アダプティブフォームの非同期送信を設定する方法について説明します。
seo-description: ここでは、アダプティブフォームの非同期送信を設定する方法について説明します。
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 67%

---


# アダプティブフォームの非同期送信{#asynchronous-submission-of-adaptive-forms}

これまでの Web フォームは、同期送信用に設定されていました。同期送信では、ユーザーがフォームを送信すると、確認ページ、「ありがとうございます」ページ、または送信に失敗した場合はエラーページにリダイレクトされます。 しかし、現在では、単一ページアプリケーションなどの最新の Web エクスペリエンスが広く使用されるようになっています。こうしたアプリケーションでは、バックグラウンドでクライアントとサーバー間の通信が実行されている間は、Web ページが静的な状態のままになります。非同期送信を設定することにより、アダプティブフォームでこうした Web エクスペリエンスを実現することができます。

非同期送信では、ユーザーがフォームを送信するときに、フォーム開発者は別のフォームやWebサイトの別のセクションへのリダイレクトなど、別のエクスペリエンスにプラグインします。 作成者は、別のデータストアへのデータの送信やカスタム分析エンジンの追加など、別のサービスをプラグインすることもできます。非同期送信の場合、アダプティブフォームは、フォームを再読み込みしないか、送信したフォームデータの検証時にURLが変更されないため、単一ページアプリのように動作します。

ここからは、アダプティブフォームの非同期送信について詳しく説明します。

## 非同期送信の設定 {#configure}

アダプティブフォームの非同期送信を設定するには、以下の手順を実行します。

1. In adaptive form authoring mode, select the Form Container object and tap ![cmppr1](assets/cmppr1.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. 「**[!UICONTROL 送信時]**」セクションで、フォームが正常に送信された場合に実行するオプションを以下のどちらかから選択します。

   * **[!UICONTROL URL にリダイレクト]**：フォームの送信時に、指定の URL またはページにリダイレクトされます。You can specify a URL or browse to choose the path to a page in the **[!UICONTROL Redirect URL/Path]** field.
   * **[!UICONTROL メッセージを表示]**：フォームの送信時にメッセージが表示されます。「メッセージを表示」オプションの下のテキストフィールドにメッセージを書き込むことができます。 このテキストフィールドには、リッチテキスト形式でメッセージを入力することができます。

1. Tap ![check-button1](assets/check-button1.png) to save the properties.

## 非同期送信の仕組み {#how-asynchronous-submission-works}

AEM Forms には、フォーム送信が成功した場合と失敗した場合の処理を実行するハンドラーが用意されています。これらのハンドラーは、すぐに使用することができます。これらのハンドラーは、サーバーからの応答に従って実行されるクライアント側の関数です。フォームを送信すると、データが検証用としてサーバーに転送され、フォーム送信の成功イベントとエラーイベントに関する情報とともに、サーバーからクライアントに応答が返されます。この情報は、パラメーターとして関連するハンドラーに渡され、対応する関数が実行されます。

また、フォーム作成者や開発者は、フォームレベルでルールを記述して、デフォルトのハンドラーを上書きできます。 詳しくは、「[ルールを使用してデフォルトのハンドラーを上書きする](#custom)」を参照してください。

最初に、成功イベントとエラーイベントに対するサーバー応答について説明します。

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

フォームの送信が成功した場合、以下の情報がサーバーからの応答として返されます。

* フォームデータのフォーマットタイプ（XML または JSON）
* XML 形式または JSON 形式のフォームデータ
* 選択されたオプション（特定のページにリダイレクトするためのオプション、またはフォーム内に設定されているメッセージを表示するためのオプション）
* フォーム内に設定されているページの URL またはメッセージの内容

成功ハンドラーは、サーバーからの応答を読み取り、その内容に従って、指定されたページの URL へのリダイレクトやメッセージの表示を実行します。

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

フォームの送信が失敗した場合、以下の情報がサーバーからの応答として返されます。

* エラーの理由と、失敗した CAPTCHA またはサーバー側での検証結果
* 検証が失敗したフィールドの SOM 式と、対応するエラーメッセージが記載されたエラーオブジェクトのリスト

エラーハンドラーは、サーバーからの応答を読み取り、その内容に従って、エラーメッセージをフォーム上に表示します。

## ルールを使用してデフォルトのハンドラーを上書きする {#custom}

フォームの開発者と作成者は、コードエディターを使用してフォームレベルでルールを記述することにより、デフォルトのハンドラーを上書きすることができます。The server response for success and error events is exposed at form level, which developers can access using `$event.data` in rules.

成功イベントとエラーイベントを処理するためのルールをコードエディターで記述するには、以下の手順を実行します。

1. Open the adaptive form in authoring mode, select any form object, and tap ![edit-rules1](assets/edit-rules1.png) to open the rule editor.
1. フォームオブジェクトツリーで「**[!UICONTROL フォーム]**」選択し、「**[!UICONTROL 作成]**」をタップします。
1. モード選択ドロップダウンで「**[!UICONTROL コードエディター]**」を選択します。
1. コードエディターで「**[!UICONTROL コードを編集]**」をタップします。確認ダイアログで「**[!UICONTROL 編集]**」をタップします。
1. 「**[!UICONTROL イベント]**」ドロップダウンで、「**[!UICONTROL 送信成功]**」または「**[!UICONTROL 送信中のエラー]**」を選択します。
1. 選択したイベントのルールを記述し、「**[!UICONTROL 完了]**」をタップしてルールを保存します。

