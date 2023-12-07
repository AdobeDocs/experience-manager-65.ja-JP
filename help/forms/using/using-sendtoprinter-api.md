---
title: sendToPrinter API の使用
description: sendToPrinter サービスを使用して、ドキュメントをプリンターに送信します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 58%

---

# sendToPrinter API の使用 {#using-the-sendtoprinter-api}

## 概要 {#overview}

AEM Formsでは、 SendToPrinter サービスを使用して、ドキュメントをプリンターに送信できます。 SendToPrinter サービスは、次の印刷アクセスメカニズムをサポートしています。

* **直接アクセス型プリンター** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **間接アクセス型プリンター** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  ドキュメントをプリンターに送信する場合は、次のいずれかの印刷プロトコルを指定します。 

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**：Output サービスは、Common Internet File System（CIFS）印刷プロトコルをサポートしています。

## SendToPrinter Service の使用 {#using-sendtoprinter-service}

次の表にリストを示します。

* 様々なプロトコルで使用する printerName または printServer に関する情報です。
* プリンタサーバー URI とプリンタ名の様々な組み合わせに対してプリンタが返す値または例外

| プロトコル（アクセスメカニズム） | プリントサーバー URI (PrinterSpec.printServer) | プリンタ名 (PrinterSpec.printerName) | 結果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空白 | 例外：必須の引数 sPrinterName を空にすることはできません。 |
| SharedPrinter | 任意 | 無効 | プリンタが見つからないことを示す例外が発生しました。 |
| SharedPrinter | 任意 | 有効 | 印刷ジョブが正常に完了しました。 |
| LPD | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| LPD | 無効 | 空白 | 必須の引数 sPrinterName を空にすることはできないという例外があります。 |
| LPD | 無効 | 空ではない | sPrintServerUri が見つからないという例外があります。 |
| LPD | 有効 | 無効 | プリンタが見つからないことを示す例外。 |
| LPD | 有効 | 有効 | 正常な印刷ジョブです。 |
| CUPS | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| CUPS | 無効 | 任意 | プリンタが見つからないことを示す例外。 |
| CUPS | 有効 | 任意 | 印刷ジョブが正常に完了しました。 |
| DirectIP | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| DirectIP | 無効 | 任意 | プリンタが見つからないことを示す例外。 |
| DirectIP | 有効 | 任意 | 印刷ジョブが正常に完了しました。 |
| CIFS | 有効 | 空白 | 印刷ジョブが正常に完了しました。 |
| CIFS | 無効 | 任意 | CIFを使用した印刷中に不明なエラーが発生しました。 |
| CIFS | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |

## 認証サポート {#authentication-support}

認証は、CIF印刷でのみサポートされます。 認証するには、PrinterSpec にユーザー名、パスワード、ドメインを入力します。次の手順を実行することで、AEM Granite CyprtoSupport Service を使用してパスワードを暗号化することができます。

1. https://&lt;server>:&lt;port>/system/console へ移動します。

1. **[!UICONTROL メイン]**／**[!UICONTROL 暗号サポート]**&#x200B;に移動します。

1. いくつかのプレーンテキストを入力し、「**[!UICONTROL 保護]**」をクリックします。
