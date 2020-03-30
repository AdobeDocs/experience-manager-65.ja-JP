---
title: Document Security Web ページの使用
seo-title: Document Security Web ページの使用
description: Document Security Web ページのログイン、移動、および使用方法について説明します。
seo-description: Document Security Web ページのログイン、移動、および使用方法について説明します。
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Document Security Web ページの使用 {#using-the-document-security-webpages}

ユーザーと管理者は、Document Security Web ページを使用して、ポリシーの作成と管理、ポリシーで保護されたドキュメントの管理およびポリシーで保護されたドキュメントに関連するイベントの監視を行います。管理者は Web ページを使用して、ポリシーセットの作成とポリシーセットコーディネーターの指定、Document Security のデフォルト値の設定、招待ユーザーの登録とアカウントの管理およびサーバー、ポリシー、ユーザー、ドキュメント関連イベントの監視と管理も行います。

>[!NOTE]
>
>ユーザーログインアカウントを使用して、Acrobat および他のクライアントアプリケーションから Document Security にログインすることもできます（[クライアントアプリケーションから Document Security へのアクセスの設定](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)を参照）。

Web ページを開くには、ブラウザー、URL および Document Security のログイン情報が必要です。ユーザー用の URL と管理者用の URL は異なります。

Document Security では、ユーザー情報を探す際に組織の既存のディレクトリが参照されるので、Document Security ログイン情報は、ネットワークや他のアプリケーションにログインするときに使用する情報と同じである場合があります。アカウント情報については、システム管理者または管理者に問い合わせてください。

管理者としてログインするには、管理者ロールが割り当てられている必要があります。インストールプロセス時に作成される、デフォルトの上級管理者アカウントを使用できます。

## Web ページへのログイン {#log-in-to-the-web-pages}

ブラウザーを使用して Web ページにログインするには、Document Security URL とアカウントが必要です。ユーザー用の URL と管理者用の URL は異なります。管理者はユーザーページにログインして、ポリシーを作成することもできます。

Document Security の複数のインストール環境にアクセスする場合は、アクセスする Document Security のインスタンスに該当する URL が必要です。この情報を持っていない場合は、管理者に問い合わせてください。The default URL for the user pages is `https://[host]:[port]/edc`. 場合によっては、ポート番号が必要でないことがあります。詳しくは、システム管理者に確認してください。

The default URL for administrators is `https://[host]:[port]/adminui`.

管理者の場合、インストール時にデフォルトの上級管理者アカウントが作成されます。Document Security を最初にインストールするときは、このアカウントを使用してログインできます。

>[!NOTE]
>
>Web ページには、Acrobat や他のクライアントアプリケーションからアクセスすることもできます。（詳しくは、Acrobat のヘルプまたは適切な Acrobat Reader DC Extensions のヘルプを参照）。

1. ブラウザーに URL を入力します。

   ドキュメントセキュリティURL: `https://[host]:[port]/edc`

   または管理コンソールのURL: `https://[host]:[port]/adminui`

1. ログインウィンドウで、ユーザー名とパスワードを入力して「OK」をクリックします。
1. 管理コンソールで、サービス／Document Security をクリックします。

>[!NOTE]
>
>Web ページで作業している場合は、「戻る」ボタン、「更新」ボタン、「戻る」矢印、「進む」矢印などのブラウザーボタンを使用しないでください。これらのボタンを使用すると、望ましくないデータ取得やデータ表示の問題が起きる可能性があります。

## Web ページでの移動 {#navigating-the-web-pages}

ユーザー Web ページにログインすると、ポリシー、ドキュメント、およびイベントというユーザーページへのリンクが表示されます。

管理コンソールにログインし、Document Security メインページに移動すると、1 つまたは 2 つの追加リンクが表示される場合があります。これらのリンクは、設定ページへのリンクと、招待ユーザーおよびローカルユーザーページへのリンクです。招待ユーザーおよびローカルユーザーページは、招待ユーザー登録が有効な場合にのみ表示されます。

これらのリンクを使用して各種ページにアクセスし、ポリシーおよびポリシーで保護されるドキュメントを作成および管理できます。

**ページの表示**

1. ページの名前をクリックします。例えば、「ポリシー」をクリックします。

**前のページに戻る**

1. ページの上部で、戻り先のページの移動リンクをクリックします。

**ページ上のデータリストの更新**

1. メインページで、更新するページへのリンクをクリックします。

>[!NOTE]
>
>Web ページで作業している場合は、「戻る」ボタン、「更新」ボタン、「戻る」矢印、「進む」矢印などのブラウザーボタンを使用しないでください。これらのボタンを使用すると、望ましくないデータ取得やデータ表示の問題が起きる可能性があります。

## クライアントアプリケーションから Document Security へのアクセスの設定 {#setting-up-access-to-document-security-from-client-applications}

ドキュメントを保護し、ポリシーで保護されたドキュメントを開き、Document Security Web ページに接続するには、クライアントアプリケーションを Document Security に接続するように設定する必要があります。クライアントアプリケーションにおける接続の設定について詳しくは、*Acrobat ヘルプ*&#x200B;または適切な *Rights Management Extension ヘルプ*&#x200B;を参照してください。

Document Security には、Secure Sockets Layer（SSL）経由でアクセスします。クライアントアプリケーションを使用して Document Security にアクセスできるようにするには、証明書ストアに Web サイトの証明書をインストールする必要があります。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

これらの説明は Internet Explorer について述べたものです。ただし、サポートされている任意の Web ブラウザーを使用して証明書をインストールすることができます。詳しくは、お使いのブラウザーのヘルプを参照してください。

**Internet Explorer でのサーバー証明書のインストール**

1. Web ブラウザーを開いて、「アドレス」ボックスに Document Security のベース URL を入力します。For example, type `https://[host]:[port]`. セキュリティの警告ダイアログボックスが表示されます。
1. 「証明書の表示」、「証明書のインストール」の順にクリックして、インストールのデフォルト証明書を選択します。証明書は、「信頼されたルート証明機関」にインストールする必要があります。
1. ブラウザーセッションを閉じます。
1. 別のブラウザーウィンドウを開き、「アドレス」ボックスに同じ URL を入力します。セキュリティの警告ダイアログボックスが表示されます。このテストで、証明書が正しくインストールされていることを確認できます。

## Web ページからのログアウト {#log-out-of-the-web-pages}

Web ページの使用が終了したら、別の目的で Web ブラウザーを安全に使用できるように、ログアウトします。Document Security の設定によっては、完全にログアウトするにはブラウザーを閉じる必要があります。

1. ページの右上隅にある「ログアウト」をクリックします。
1. ログアウトページにメッセージが表示される場合は、ブラウザーウィンドウを閉じて完全にログアウトします。それ以外の場合は、ブラウザーをそのまま他の目的で使用できます。

