---
title: Document Security Web ページの使用
description: Document Security Web ページにログイン、移動、および使用する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 3%

---

# Document Security Web ページの使用 {#using-the-document-security-webpages}

ユーザーと管理者は、Document Security Web ページを使用して、ポリシーの作成と管理、ポリシーで保護されたドキュメントの管理、およびポリシーで保護されたドキュメントに関連するイベントの監視をおこないます。 また、管理者は Web ページを使用してポリシーセットを作成し、ポリシーセットコーディネーターを指定し、Document Security のデフォルト設定を構成し、招待ユーザーの登録とアカウントを管理し、サーバー、ポリシー、ユーザー、ドキュメント関連のイベントを監視および管理します。

>[!NOTE]
>
>ユーザーログインアカウントを使用して、Acrobatや他のクライアントアプリケーションから Document Security にログインすることもできます。 ( 詳しくは、 [クライアントアプリケーションから Document Security へのアクセスの設定](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Web ページを開くには、Document Security のブラウザと URL およびログイン情報が必要です。 ユーザーの URL は管理者の URL とは異なります。

Document Security は、組織の既存のディレクトリを参照してユーザー情報を確認するので、Document Security のログイン情報は、ネットワークや他のアプリケーションへのログインに使用する情報と同じである場合があります。 アカウント情報については、システム管理者または管理者にお問い合わせください。

管理者としてログインするには、管理者の役割が割り当てられている必要があります。 インストールプロセス中に作成されたデフォルトのスーパー管理者アカウントを使用できます。

## Web ページにログインします。 {#log-in-to-the-web-pages}

ブラウザーを使用して Web ページにログインするには、Document Security URL とアカウントが必要です。 ユーザーの URL は管理者の URL とは異なります。 管理者は、ユーザーページにログインして、ポリシーを作成することもできます。

Document Security の複数のインストールにアクセスできる場合は、アクセスする Document Security のインスタンスの URL が必要です。 この情報を持っていない場合は、管理者に問い合わせてください。 ユーザーページのデフォルトの URL は、`https://[host]:[port]/edc` です。場合によっては、ポート番号が必要でないことがあります。 詳しくは、管理者に問い合わせてください。

管理者用のデフォルトの URL は、`https://[host]:[port]/adminui` です。

管理者の場合、インストール時にデフォルトの上級管理者アカウントが作成されます。 Document Security が初めてインストールされる場合は、このアカウントを使用してログインできます。

>[!NOTE]
>
>Web ページには、Acrobatや他のクライアントアプリケーションからアクセスすることもできます。 詳しくは、 Acrobatのヘルプまたは適切なAcrobat Reader DC拡張機能のヘルプを参照してください。

1. ブラウザーに URL を入力します。

   Document Security URL： `https://[host]:[port]/edc`

   または管理コンソールの URL：`https://[host]:[port]/adminui`

1. ログインウィンドウで、ユーザー名とパスワードを入力し、「OK」をクリックします。
1. 管理コンソールで、サービス/Document Security をクリックします。

>[!NOTE]
>
>Web ページを操作する場合は、戻るボタン、更新ボタン、戻る矢印や進む矢印などのブラウザーボタンを使用しないでください。この操作により、データの取得とデータの表示に関する不要な問題が発生する可能性があります。

## Web ページの移動 {#navigating-the-web-pages}

ユーザー Web ページにログインすると、ポリシー、ドキュメント、イベントの各ユーザーページへのリンクが表示されます。

管理コンソールにログインして Document Security のメインページに移動すると、追加のリンクが 1 つまたは 2 つ表示されます。1 つは設定ページ用、もう 1 つは招待ユーザーとローカルユーザーのページ用です。 招待ユーザーとローカルユーザーページは、招待ユーザーの登録が有効な場合にのみ表示されます。

これらのリンクを使用して様々なページにアクセスし、ポリシーおよびポリシーで保護されたドキュメントを作成および管理します。

**ページを表示**

1. ページの名前（「ポリシー」のクリックなど）をクリックします。

**前のページに戻る**

1. 戻るページのページ上部にあるナビゲーションリンクをクリックします。

**ページ上のデータリストを更新する**

1. メインページで、更新するページへのリンクをクリックします。

>[!NOTE]
>
>Web ページを操作する場合は、戻るボタン、更新ボタン、戻る矢印や進む矢印などのブラウザーボタンを使用しないでください。この操作により、データの取得とデータの表示に関する不要な問題が発生する可能性があります。

## クライアントアプリケーションから Document Security へのアクセスの設定 {#setting-up-access-to-document-security-from-client-applications}

ドキュメントを保護し、ポリシーで保護されたドキュメントを開き、Document Security Web ページに接続するには、クライアントアプリケーションを Document Security に接続するように設定する必要があります。 詳しくは、 *Acrobat Help* または適切な *RightsManagementExtension ヘルプ* を参照してください。

Document Security には、Secure Sockets Layer(SSL) を介してアクセスします。 Web サイトの証明書を証明書ストアにインストールして、クライアントアプリケーションを使用して Document Security にアクセスできるようにします。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

これらの手順は Internet Explorer に固有のものですが、サポートされている任意の Web ブラウザーを使用して証明書をインストールできます。 詳細については、ご使用のブラウザのヘルプを参照してください。

**Internet Explorer を使用したサーバー証明書のインストール**

1. Web ブラウザーを開き、「アドレス」ボックスに Document Security のベース URL を入力します。 例えば、`https://[host]:[port]` と入力します。[ セキュリティの警告 ] ダイアログボックスが表示されます。
1. [ 証明書の表示 ] をクリックし、[ 証明書のインストール ] をクリックして、インストールの既定値を選択します。 証明書は、信頼されたルート証明機関にインストールする必要があります。
1. ブラウザーセッションを閉じます。
1. 別のブラウザーウィンドウを開き、「アドレス」ボックスに同じ URL を入力します。 [ セキュリティの警告 ] ダイアログボックスは表示されません。 このテストでは、証明書が正しくインストールされていることを確認します。

## Web ページからのログアウト {#log-out-of-the-web-pages}

他の目的で Web ブラウザーを安全に使用できるよう、Web ページの使用が終了したらログアウトします。 Document Security の設定によっては、完全にログアウトするには、ブラウザを閉じる必要があります。

1. ページの右上隅にある「ログアウト」をクリックします。
1. ログアウトページにメッセージが表示された場合は、ブラウザーウィンドウを閉じて、完全にログアウトします。 それ以外の場合は、ブラウザーを他の目的で使用することもできます。
