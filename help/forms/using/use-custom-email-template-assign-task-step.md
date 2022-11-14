---
title: タスクの割り当て手順におけるカスタムの電子メールテンプレートの使用
seo-title: Use custom email templates in an Assign Task step
description: Forms ワークフローの電子メール通知のカスタム電子メールテンプレート
seo-description: Custom email templates for forms workflow email notifications
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 100%

---

# タスク割り当て手順でのカスタムメールテンプレートの使用{#use-custom-email-templates-in-an-assign-task-step}

ユーザーまたはグループにタスクを作成して割り当てるには、タスクの割り当て手順を使用します。ユーザーまたはグループにタスクが割り当てられると、電子メール通知が指定されたユーザーまたは指定されたグループのメンバーに送信されます。一般的な電子メール通知には、割り当てられたタスクのリンクと、タスクに関連する情報が含まれています。次の画像は、サンプルの電子メール通知を示します。

![デフォルトのテンプレートを使用したメール通知](do-not-localize/default_email_template_new.png)

電子メール通知では、外観をカスタマイズしてカスタムメタデータを使用することができます。AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。初期設定済みテンプレートをカスタマイズするか、新しいテンプレートをゼロから作成することができます。

電子メール通知テンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)をベースにしています。これらの電子メールは、様々な電子メールクライアントや画面サイズに対応します。さらに、電子メールのスタイルはテンプレート内で定義されます。

次の画像は、カスタマイズされたメール通知です。

![カスタムテンプレートを使用したメール通知](do-not-localize/customized-email.png)

## 既存テンプレートのカスタマイズ {#customize-the-existing-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。テンプレートをカスタマイズして外観を変更することができます。次の手順を実行してテンプレートをカスタマイズします。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. htmlEmailTemplate.txt ファイルを開きます。これにはデフォルトのテンプレートが含まれています。

1. htmlEmailTemplate.txt ファイルのコンテンツをカスタムコンテンツと置き換えます。

   メール通知テンプレートは、[HTML 形式のメール](https://en.wikipedia.org/wiki/HTML_email)です。既存の HTML コードをカスタムコードで置き換えることで、テンプレートの外観を変更することができます。

1. ファイルを保存します。これでカスタマイズされたテンプレートが使用できるようになります。

## 電子メールテンプレートの作成 {#create-an-email-template}

AEM Forms には電子メール通知用の初期設定済みテンプレートが用意されています。テンプレートには、タイトルの説明、期限、優先度、ワークフロー名、割り当てられたタスクのリンクが含まれています。また、タスクの割り当て手順にカスタムの電子メールテンプレート（独自のテンプレート）を追加できます。次の手順を実行して、カスタムの電子メールテンプレートを追加します。

1. 管理者アカウントで CRXDE にログインします。

1. /libs/fd/dashboard/templates/email に移動します。

1. .txt ファイルを作成します。例えば、EmailOnTaskAssign.txt などです。

1. カスタムの HTML コードをファイルに追加します。

   メール通知テンプレートは、[HTML 形式の電子メール](https://en.wikipedia.org/wiki/HTML_email)です。カスタムの HTML コードをファイルに追加して、新しいテンプレートを作成します。

1. ファイルを保存します。テンプレートが、タスクの割り当て手順で使用できるようになりました。

## タスクの割り当て手順における電子メールテンプレートの使用 {#use-an-email-template-in-an-assign-task-step}

タスクの割り当て手順では、初期状態でデフォルトテンプレート htmlEmailTemplate.txt を使用するように設定されています。カスタムのテンプレートを使用するように選択できます。テンプレートの場所を変更するには：

1. タスクの割り当て手順を開きます。

1. 「担当者」／「HTML メールテンプレート」に移動します。

1. 新しく作成された HTML メールテンプレートを選択します。

1. 「OK」をクリックします。テンプレートが変更されました。

電子メール通知では、[メタデータ](../../forms/using/use-metadata-in-email-notifications.md)も使用します。例えば、期限、優先度、ワークフロー名などです。[カスタムメタデータ](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)を使用するために、テンプレートを設定することもできます。
