---
title: タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用
seo-title: タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用
description: 'Forms ワークフローの電子メール通知のカスタム電子メールテンプレート '
seo-description: 'Forms ワークフローの電子メール通知のカスタム電子メールテンプレート '
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 96%

---


# タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用{#use-custom-email-templates-in-an-assign-task-step}

ユーザーまたはグループにタスクを作成して割り当てるには、タスクの割り当て手順を使用します。ユーザーまたはグループにタスクが割り当てられると、電子メール通知が指定されたユーザーまたは指定されたグループのメンバーに送信されます。一般的な電子メール通知には、割り当てられたタスクのリンクと、タスクに関連する情報が含まれています。次の画像は、サンプルの電子メール通知を示します。

![初期設定済みテンプレートを使用した電子メール通知](do-not-localize/default_email_template_new.png)

電子メール通知では、外観をカスタマイズしてカスタムメタデータを使用することができます。AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。初期設定済みテンプレートをカスタマイズするか、新しいテンプレートをゼロから作成することができます。

電子メール通知テンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)をベースにしています。これらの電子メールは、様々な電子メールクライアントや画面サイズに対応します。さらに、電子メールのスタイルはテンプレート内で定義されます。

次の画像は、カスタマイズされた電子メール通知を表示します。

![カスタムテンプレートを使用した電子メール通知](do-not-localize/customized-email.png)

## 既存テンプレートのカスタマイズ {#customize-the-existing-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。テンプレートをカスタマイズして外観を変更することができます。次の手順を実行してテンプレートをカスタマイズします。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. htmlEmailTemplate.txt ファイルを開きます。これにはデフォルトのテンプレートが含まれています。

1. htmlEmailTemplate.txt ファイルのコンテンツをカスタムのコンテンツと置き換えます。

   電子メール通知のテンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)です。既存の html コードをカスタムのコードで置き換えることで、テンプレートの外観を変更することができます。

1.  ファイルを保存します。これでカスタマイズされたテンプレートが使用できるようになります。

## 電子メールテンプレートの作成 {#create-an-email-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。また、タスクの割り当て手順にカスタムの電子メールテンプレート（独自のテンプレート）を追加できます。次の手順を実行して、カスタムの電子メールテンプレートを追加します。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. .txt ファイルを作成します。例えば、EmailOnTaskAssign.txt のようにします。

1. カスタムの HTML コードをファイルに追加します。

   電子メール通知のテンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)です。カスタムの HTML コードをファイルに追加して、新しいテンプレートを作成します。

1.  ファイルを保存します。テンプレートは、タスクの割り当て手順で使用することができます。

## タスクの割り当て手順における電子メールテンプレートの使用 {#use-an-email-template-in-an-assign-task-step}

タスクの割り当て手順では、初期状態でデフォルトテンプレート htmlEmailTemplate.txt を使用するように設定されています。カスタムのテンプレートを使用するように選択できます。テンプレートの場所を変更するには：

1. タスクの割り当て手順を開きます。

1. 担当者／HTML 電子メールテンプレートに移動します。

1. 新規作成された HTML 電子メールテンプレートを選択します。

1. 「OK」をクリックします。テンプレートが変更されました。

電子メール通知では、[メタデータ](../../forms/using/use-metadata-in-email-notifications.md)も使用します。例えば、期限、優先度、ワークフロー名などです。You can also configure the template to use [custom metadata](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification).
