---
title: リダイレクトページの設定
seo-title: リダイレクトページの設定
description: アダプティブフォーム入力後、フォーム作成時にフォーム作成者が設定可能な Web ページへ、ユーザーをリダイレクトさせることができます。
seo-description: アダプティブフォーム入力後、フォーム作成時にフォーム作成者が設定可能な Web ページへ、ユーザーをリダイレクトさせることができます。
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 74%

---


# リダイレクトページの設定{#configuring-redirect-page}

フォーム作成者は、フォーム送信後にユーザーがリダイレクトされるページを各フォームに設定することができます。

1. In the edit mode, select a component, then click ![field-level](assets/field-level.png) > **Adaptive Form Container**, and then click ![cmppr](assets/cmppr.png).

1. サイドバーで、「**送信**」をクリックします。

1. 送信セクションの「ありがとうございました」ページで、リダイレクトページの URL を指定します。
1. オプションとして、「送信アクション」で、「REST エンドポイントへの送信」の送信アクションについて、リダイレクトページに渡されるパラメーターを設定することができます。

![リダイレクトページ設定](assets/thank-you-setting-1.png)

リダイレクトページ設定

フォーム作成者は、「ありがとうございます」ページに渡される次のパラメーターを使用することができます。For all the available submit actions, `status` and `owner` parameters are passed. これら 2 つのパラメーターの他に、追加のパラメーターが次の送信アクションに渡されます。

* **コンテンツ保存アクション** （非推奨）: `contentPath`— 送信されたデータが保存されるリポジトリ内のノードのパス — が渡されます。

* **PDFの保存アクション** （非推奨）: `contentPath`— 送信されたデータと、リポジトリにPDFファイルが格納されているノードのパス — が渡されます。

* **フォームワークフローへの送信**：フォームワークフローから返される出力パラメーターが渡されます。

* **REST エンドポイントへの送信**：フィールド内にパラメーターマッピングのため追加されたパラメータが渡されます。`status` および `owner` パラメーターは、この送信アクションでは渡されません。詳しくは、[送信アクション「REST エンドポイントへの送信」の設定](../../forms/using/configuring-submit-actions.md)を参照してください。 

