---
title: sendToPrinter API の使用
seo-title: Using the sendToPrinter API
description: SendToPrinter サービスを使用して、プリンタにドキュメントを送信します。
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 100%

---

# sendToPrinter API の使用 {#using-the-sendtoprinter-api}

## 概要 {#overview}

AEM Forms では、SendToPrinter サービスを使用することで、プリンタにドキュメントを送信できます。SendToPrinter サービスは、次の印刷アクセスメカニズムをサポートしています。

* **直接アクセス型プリンター** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **間接アクセス型プリンター** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   ドキュメントをプリンターに送信する場合は、次のいずれかの印刷プロトコルを指定します。 

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * ``**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * ``**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**：Output サービスは、Common Internet File System（CIFS）印刷プロトコルをサポートしています。

## SendToPrinter Service の使用 {#using-sendtoprinter-service}

テーブルには、以下の項目が表示されます。

* さまざまなプロトコルで使用する printerName または PRINTSERVER に関する情報。
* プリンタサーバー URI とプリンタ名の様々な組み合わせに対してプリンタが返す値または例外

| プロトコル（アクセスメカニズム） | プリントサーバー URI（PrinterSpec.printServer） | プリンタ名（PrinterSpec.printerName） | 結果 |
|--- |--- |--- |--- |
| SharedPrinter | 任意 | 空白 | 例外：必須の引数 sPrinterName を空にすることはできません。 |
| SharedPrinter | 任意 | 無効 | プリンターが見つからないという内容の例外がスローされます。 |
| SharedPrinter | 任意 | 有効 | 印刷ジョブが正常に作成されます。 |
| LPD | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| LPD | 無効 | 空白 | 必須の引数 sPrinterName を空にすることはできないという例外があります。 |
| LPD | 無効 | 空ではない | sPrintServerUri が見つからないという例外があります。 |
| LPD | 有効 | 無効 | プリンターが見つからないという内容の例外がスローされます。 |
| LPD | 有効 | 有効 | 印刷ジョブが正常に作成されます。 |
| CUPS | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| CUPS | 無効 | 任意 | プリンターが見つからないという内容の例外がスローされます。 |
| CUPS | 有効 | 任意 | 印刷ジョブが正常に作成されます。 |
| DirectIP | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |
| DirectIP | 無効 | 任意 | プリンターが見つからないという内容の例外がスローされます。 |
| DirectIP | 有効 | 任意 | 印刷ジョブが正常に作成されます。 |
| CIFS | 有効 | 空白 | 印刷ジョブが正常に作成されます。 |
| CIFS | 無効 | 任意 | CIFS を使用した印刷中に不明なエラーがスローされます。 |
| CIFS | 空白 | 任意 | 必須の引数 sPrintServerUri を空にすることはできないことを示す例外。 |

## 認証サポート {#authentication-support}

認証は、CIFS 印刷に対してのみサポートされます。認証するには、PrinterSpec にユーザー名、パスワード、ドメインを入力します。次の手順を実行することで、AEM Granite CyprtoSupport Service を使用してパスワードを暗号化することができます。

1. https://&lt;server>:&lt;port>/system/console へ移動します。

1. **[!UICONTROL メイン]**／**[!UICONTROL 暗号サポート]**&#x200B;に移動します。

1. いくつかのプレーンテキストを入力し、「**[!UICONTROL 保護]**」をクリックします。
