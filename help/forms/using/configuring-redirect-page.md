---
title: リダイレクトページの設定
seo-title: Configuring redirect page
description: アダプティブフォームに入力すると、フォームの作成時にフォーム作成者が設定できる Web ページにユーザーがリダイレクトされます。
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 82%

---

# リダイレクトページの設定{#configuring-redirect-page}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | この記事 |

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

1. 編集モードで、コンポーネントを選択し、![フィールドレベル](assets/field-level.png)／**アダプティブフォームコンテナ**&#x200B;をクリックしてから、 ![cmppr](assets/cmppr.png) をクリックします。

1. サイドバーで、「**送信**」をクリックします。

1. 送信セクションの「ありがとうございました」ページで、リダイレクトページの URL を指定します。
1. オプションとして、「送信アクション」で、「REST エンドポイントへの送信」の送信アクションについて、リダイレクトページに渡されるパラメーターを設定することができます。

![リダイレクトページ設定](assets/thank-you-setting-1.png)

リダイレクトページ設定

フォーム作成者は、次のパラメーターを使用して「ありがとうございました」ページに渡すことができます。 使用可能なすべての送信アクションに対して、`status` と `owner` のパラメーターが渡されます。これら 2 つのパラメーターの他に、追加のパラメーターが次の送信アクションに渡されます。

* **コンテンツを格納アクション**（非推奨）：送信されたデータが格納されるリポジトリのノードのパス `contentPath` が渡されます。

* **PDF の保存アクション**（非推奨）：送信されたデータと、リポジトリで PDF ファイルを保存しているノードのパス `contentPath` が渡されます。

* **フォームワークフローへの送信**：フォームワークフローから返される出力パラメーターが渡されます。

* **REST エンドポイントへの送信**：フィールド内にパラメーターマッピングのため追加されたパラメータが渡されます。`status` および `owner` パラメーターは、この送信アクションでは渡されません。詳しくは、[送信アクション「REST エンドポイントへの送信」の設定](../../forms/using/configuring-submit-actions.md)を参照してください。 
