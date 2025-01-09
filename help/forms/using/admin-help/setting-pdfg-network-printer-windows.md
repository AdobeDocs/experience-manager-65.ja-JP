---
title: PDFG ネットワークプリンターの設定（Windows のみ）
description: PDFG ネットワークプリンターの設定方法について説明します（Windows のみ）
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '616'
ht-degree: 100%

---

# PDFG ネットワークプリンターの設定（Windows のみ） {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

PDFG ネットワークプリンターを使用すると、印刷をサポートしているアプリケーションであれば、どのアプリケーションからでも PDF ドキュメントを生成できます。PDFG ネットワークプリンターをインストールすると、*PDF Generator* という名前の新しいプリンターが Windows コントロールパネルの「プリンター」セクションに表示されます。同じ名前のプリンターが既に存在する場合は、別の名前を指定することを促すメッセージが表示されます。

アプリケーションからこのプリンターに出力すると、（PostScript 形式の）ドキュメントが PDF Generator に送信され、そこで PostScript ファイルが PDF に変換されます。この PDF ドキュメントは、PDF Generator の設定に応じて、ユーザーにメールの添付ファイルとして送信されるか、指定された AEM forms のサービスまたはプロセスに転送されるか、あるいはその両方のアクションが実行されます。

PDFG ネットワークプリンターを設定するには、次の手順を実行する必要があります。

1. メールを設定します。（[PDFG ネットワークプリンターのメール設定の指定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)を参照）。
1. 管理コンソールで、PDFG ネットワークプリンターの設定を指定します（[PDFG ネットワークプリンターの設定の指定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)を参照）。
1. AEM Forms データベース内の有効なメールアドレスを使用してユーザーを設定し、各ユーザーに PDFGUserPermission を割り当てます。<!-- Fix broken link See Setting up and organizing users -->
1. 32 ビット JRE6 がユーザーのコンピューターにインストールされていることを確認します。
1. ユーザーのコンピューターにプリンターをインストールします（[ユーザーのコンピューターへの PDFG ネットワークプリンターのインストール](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)を参照）。

## PDFG ネットワークプリンターのメール設定の指定 {#configure-email-settings-for-pdfg-network-printer}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、provider.email_sendmail_service をクリックし、SMTP 設定を指定し、「保存」をクリックします。

## PDFG ネットワークプリンターの設定の指定 {#configure-the-pdfg-network-printer-settings}

1. 管理コンソールで、サービス／PDF Generator／PDFG ネットワークプリンターをクリックします。
1. 「Adobe PDF 設定」および「セキュリティ設定」リストで、生成された PDF に適用するオプションを選択します。これらの設定について詳しくは、[Adobe PDF 設定の指定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings)および[セキュリティ設定の指定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)を参照してください。
1. 変換された PDF をユーザーに返送するには、「変換された PDF ファイルをユーザーにメールで戻します」オプションを選択し、次の情報を指定します。

   * ユーザーへの PDF の送付に使用するメールアドレス。
   * メールメッセージの件名。
   * メールメッセージのヘッダー、本文およびフッター。メール内の &lt;receiverName> は、ドキュメントを印刷したユーザーのフルネームに置き換わります。

1. 変換された PDF を AEM Forms のサービスまたはプロセスに送信するには、「変換した PDF を指定された AEM Forms のサービスまたはプロセスに転送する」オプションを選択し、以下の情報を指定します。

   * 呼び出すサービスの名前。
   * 呼び出すサービスの操作の名前。
   * サービスまたはプロセスの component.xml ファイルに指定される、入力パラメーターの名前。PDF ドキュメントは、この入力パラメーターの値として使用されます。

1. 「保存」をクリックします。

元のデフォルトのメールテキストに戻す場合は、「メールコンテンツを復元」をクリックします。

## ユーザーのコンピューターへの PDFG ネットワークプリンターのインストール {#install-pdfg-network-printer-on-a-user-s-computer}

PDFG 管理者ロールまたは PDFG ユーザーロールのいずれかを持つユーザーは、PDFG ネットワークプリンターをインストールできます。コンピューターに 32 ビット JDK をインストールしておく必要があります。

1. （PDFG 管理者の場合）管理コンソールで、サービス／PDF Generator／PDFG ネットワークプリンターをクリックします。

   （PDFG ユーザーの場合）`http(s)://[host]:'port'/pdfgui` にアクセスし、「PDFG ネットワークプリンターのインストール」にあるリンクをクリックします。

1. 「PDFG ネットワークプリンターのインストール」にあるリンクをクリックします。ユーザーアカウント情報が求められたら、手順 1 で使用したユーザー名とパスワードを指定してログインします。プリンターが正常にインストールされたことを示すメッセージが表示されます。

   ***メモ&#x200B;**：ユーザーのパスワードを変更する場合、ユーザーは PDFG ネットワークプリンターをコンピューターに再インストールする必要があります。パスワードを管理コンソールから更新することはできません。*

1. 「OK」をクリックします。
