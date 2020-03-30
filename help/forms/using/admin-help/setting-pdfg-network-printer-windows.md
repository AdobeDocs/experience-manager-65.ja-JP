---
title: PDFG ネットワークプリンターの設定（Windows のみ）
seo-title: PDFG ネットワークプリンターの設定（Windows のみ）
description: PDFG ネットワークプリンターの設定方法について説明します。（Windows のみ）
seo-description: PDFG ネットワークプリンターの設定方法について説明します。（Windows のみ）
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# PDFG ネットワークプリンターの設定（Windows のみ）{#setting-up-a-pdfg-network-printer-windows-only}

PDFG ネットワークプリンターを使用すると、印刷をサポートしているアプリケーションであれば、どのアプリケーションからでも PDF ドキュメントを生成できます。PDFG ネットワークプリンターをインストールすると、*PDF Generator* という名前の新しいプリンターが Windows コントロールパネルの「プリンター」セクションに表示されます。同じ名前のプリンターが既に存在する場合は、別の名前を指定することを促すメッセージが表示されます。

アプリケーションからこのプリンターに出力すると、（PostScript 形式の）ドキュメントが PDF Generator に送信され、そこで PDF に変換されます。この PDF ドキュメントは、PDF Generator の設定に応じて、ユーザーに電子メールの添付ファイルとして送信されるか、指定された AEM forms のサービスまたはプロセスに転送されるか、あるいはその両方のアクションが実行されます。

PDFG ネットワークプリンターを設定するには、次の手順を実行する必要があります。

1. 電子メールを設定します（[PDFG ネットワークプリンターの電子メール設定の指定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)を参照）。
1. 管理コンソールで、PDFG ネットワークプリンターの設定を指定します（[PDFG ネットワークプリンターの設定の指定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)を参照）。
1. AEM forms データベース内の有効な電子メールアドレスを使用してユーザーを設定し、各ユーザーに PDFGUserPermission を割り当てます<!-- Fix broken link See Setting up and organizing users -->
1. 32 ビット JRE6 がユーザーのコンピューターにインストールされていることを確認します。
1. ユーザーのコンピューターにプリンターをインストールします（[ユーザーのコンピューターへの PDFG ネットワークプリンターのインストール](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)を参照）。

## PDFG ネットワークプリンターの電子メール設定の指定 {#configure-email-settings-for-pdfg-network-printer}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、provider.email_sendmail_service をクリックし、SMTP 設定を指定し、「保存」をクリックします。

## PDFG ネットワークプリンターの設定の指定 {#configure-the-pdfg-network-printer-settings}

1. 管理コンソールで、サービス／PDF Generator／PDFG ネットワークプリンターをクリックします。
1. 「Adobe PDF 設定」および「セキュリティ設定」リストで、生成された PDF に適用するオプションを選択します。これらの設定について詳しくは、[Adobe PDF 設定の指定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings)および[セキュリティ設定の指定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)を参照してください。
1. 変換された PDF をユーザーに返送するには、「変換された PDF ファイルをユーザーに電子メールで戻します」オプションを選択し、次の情報を指定します。

   * ユーザーへの PDF の送付に使用する電子メールアドレス。
   * 電子メールメッセージの件名。
   * 電子メールメッセージのヘッダー、本文およびフッター。電子メール内の &lt;receiverName> は、ドキュメントを印刷したユーザーのフルネームに置き換わります。

1. 変換された PDF を AEM forms のサービスまたはプロセスに送信するには、「変換した PDF を指定された AEM forms のサービスまたはプロセスに転送します」オプションを選択し、以下の情報を指定します。

   * 呼び出すサービスの名前。
   * 呼び出すサービスの操作の名前。
   * サービスまたはプロセスの component.xml ファイルに指定される、入力パラメーターの名前。PDF ドキュメントは、この入力パラメーターの値として使用されます。

1. 「保存」をクリックします。

元のデフォルトの電子メールテキストに戻す場合は、「電子メールコンテンツを復元」をクリックします。

## ユーザーのコンピューターへの PDFG ネットワークプリンターのインストール {#install-pdfg-network-printer-on-a-user-s-computer}

PDFG 管理者ロールまたは PDFG ユーザーロールのいずれかを持つユーザーは、PDFG ネットワークプリンターをインストールできます。コンピューターに 32 ビット JDK をインストールしておく必要があります。

1. （PDFG 管理者の場合）管理コンソールで、サービス／PDF Generator／PDFG ネットワークプリンターをクリックします。

   (PDFG Users) Go to `http(s)://[host]:'port'/pdfgui` and click the link under PDFG Network Printer Installation.

1. 「PDFG ネットワークプリンターのインストール」にあるリンクをクリックします。ユーザーアカウント情報が求められたら、手順 1 で使用したユーザー名とパスワードを指定してログインします。プリンターが正常にインストールされたことを示すメッセージが表示されます。

   ***注意&#x200B;**：ユーザーのパスワードを変更する場合、ユーザーは PDFG ネットワークプリンターをコンピューターに再インストールする必要があります。パスワードを管理コンソールから更新することはできません。*

1. 「OK」をクリックします。

