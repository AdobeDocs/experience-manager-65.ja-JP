---
title: PDFG ネットワークプリンターの設定（Windows のみ）
description: PDFG ネットワークプリンターの設定方法を説明します（ Windows のみ）
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 11%

---

# PDFG ネットワークプリンターの設定（Windows のみ） {#setting-up-a-pdfg-network-printer-windows-only}

PDFG ネットワークプリンターを使用すると、印刷をサポートする任意のPDFからアプリケーションドキュメントを生成できます。 PDFG ネットワークプリンターをインストールすると、*PDF Generator* という名前の新しいプリンターが Windows コントロールパネルの「プリンター」セクションに表示されます。同じ名前のプリンタが既に存在する場合は、別の名前を指定するように求められます。

任意のアプリケーションからこのプリンターに印刷すると、ドキュメントが（PostScript 形式で）PDF Generatorに送信され、PostScript ファイルがPDFに変換されます。 PDF Generatorの設定に応じて、PDFドキュメントが電子メールメッセージへの添付ファイルとしてユーザーに送信されるか、PDFドキュメントが指定のAEM forms サービスまたはプロセスに転送されるか、両方のアクションが実行されます。

PDFG ネットワークプリンターを設定するには、次の手順を実行する必要があります。

1. 電子メールを設定します。 ( 詳しくは、 [PDFG ネットワークプリンターの電子メール設定の指定](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. 管理コンソールで、「PDFG ネットワークプリンター」設定を指定します。 ( 詳しくは、 [PDFG ネットワークプリンターの設定](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. ユーザーがAEM forms データベース内の有効な電子メールアドレスを使用して設定され、各ユーザーに PDFGUserPermission を割り当てていることを確認します。 <!-- Fix broken link See Setting up and organizing users -->
1. 32 ビット JRE6 がユーザーのコンピュータにインストールされていることを確認します。
1. ユーザーのコンピューターにプリンターをインストールします。 ( 詳しくは、 [ユーザーのコンピューターに PDFG ネットワークプリンターをインストールする](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## PDFG ネットワークプリンターの電子メール設定の指定 {#configure-email-settings-for-pdfg-network-printer}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. 「サービスの管理」ページで、provider.email_sendmail_service をクリックし、SMTP 設定を指定して、「保存」をクリックします。

## PDFG ネットワークプリンターの設定 {#configure-the-pdfg-network-printer-settings}

1. 管理コンソールで、サービス/PDF Generator/PDFG ネットワークプリンターをクリックします。
1. 「 Adobe PDF設定」リストと「セキュリティ設定」リストで、生成される設定に適用するオプションをPDFします。 これらの設定の詳細については、 [Adobe PDFの設定](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) および [セキュリティ設定の指定](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. 変換後のPDFを再度ユーザーに送信するには、「変換後のPDFファイルを電子メールでユーザーに返す」オプションを選択し、次の情報を指定します。

   * ユーザーにPDFを送信する際に使用する電子メールアドレス
   * 電子メールメッセージの件名
   * 電子メールメッセージのヘッダー、本文およびフッター。 電子メールメッセージで、 &lt;receivername> は、ドキュメントを印刷したユーザーのフルネームに置き換えられます。

1. 変換後のPDFをAEM forms サービスまたはプロセスに送信するには、「Forward The Converted The ConvertedPDFTo The Specified AEM forms Service Or Process」オプションを選択し、以下の情報を指定します。

   * 呼び出すサービスの名前
   * 呼び出すサービスの操作の名前
   * サービスまたはプロセスの component.xml ファイルで指定された、入力パラメーターの名前。 PDFドキュメントは、その入力パラメーターの値として使用されます。

1. 「保存」をクリックします。

元のデフォルトの電子メールテキストに戻す場合は、[ 電子メールの内容を復元する ] をクリックします。

## ユーザーのコンピューターに PDFG ネットワークプリンターをインストールする {#install-pdfg-network-printer-on-a-user-s-computer}

「PDFG 管理者」または「PDFG ユーザー」の役割を持つユーザーは、PDFG ネットワークプリンターをインストールできます。 コンピューターに 32 ビット JDK がインストールされている必要があります。

1. （PDFG 管理者）管理コンソールで、サービス/PDF Generator/PDFG ネットワークプリンターをクリックします。

   （PDFG ユーザーの場合）`http(s)://[host]:'port'/pdfgui` にアクセスし、「PDFG ネットワークプリンターのインストール」にあるリンクをクリックします。

1. 「PDFG ネットワークプリンターのインストール」の下のリンクをクリックします。 ユーザーアカウント情報の入力を求められたら、手順 1 で使用したユーザー名とパスワードを指定してログインします。 プリンタが正常にインストールされたことを示すメッセージが表示されます。

   ***注意&#x200B;**：ユーザーのパスワードを変更した場合、ユーザーは PDFG ネットワークプリンターをコンピューターに再インストールする必要があります。 管理コンソールからパスワードを更新することはできません。*

1. 「OK」をクリックします。
