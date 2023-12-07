---
title: ポータブル保護ライブラリを使用して、ポリシーで保護された PDF ドキュメントを Reader 用に拡張します。
description: Reader拡張機能を使用すると、Acrobat Readerを介してAdobe PDFドキュメントのインタラクティブ機能を有効にできます。 DRM で保護されたライブラリドキュメントを Reader 用に拡張するには、Portable Protection Library (PPL) を使用します。PDF
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 32%

---

# ポータブル保護ライブラリを使用して、ポリシーで保護された PDF ドキュメントを Reader 用に拡張します。 {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

ドキュメントセキュリティポリシーで保護されたPDFドキュメントを Reader-Extend するには、ドキュメントセキュリティ、Reader Extension、および Java プログラミング言語の概念を理解しておく必要があります。

Document Security を使用して、特定のユーザードキュメントへのアクセスを、許可されたPDFに対してのみ制限できます。 また、受信者が保護されたドキュメントをどのように使用できるかを指定することもできます。 例えば、Document Security のポリシーで保護されたドキュメントの受信者がテキストの印刷、コピー、編集を行えるかどうかを指定できます。 Document Security の詳細については、 [document security について](/help/forms/using/admin-help/document-security.md).

Reader Extensions を使用すると、Acrobat Readerを通じてAdobe PDFドキュメントのインタラクティブ機能を有効にすることができます。 これらのインタラクティブ機能は、通常、Adobe Acrobat Professional および Standard でのみ利用できます。 Reader 拡張機能により有効にできるインタラクティブ機能については、「[Adobe Experience Manager Forms DocAssurance サービス&#x200B;](/help/forms/using/overview-aem-document-services.md)**」を参照してください。**

ポータブル保護ライブラリ（PPL）を使用して、ネットワークにドキュメントを送信することなくドキュメントにポリシーを適用できます。ネットワークに送信されるのは、セキュリティの資格情報と保護ポリシーの詳細のみです。実際のドキュメントはクライアントから離れることはなく、保護ポリシーはクライアント上でローカルに適用されます。

## ReaderDocument Security のポリシーで保護されたPDFドキュメントの拡張 {#reader-extending-document-security-policy-protected-pdf-documents}

ポリシーで保護されたドキュメントは、暗号化されたドキュメントです。 ポリシーで保護されたPDFドキュメントの使用権限の適用、削除、取得に、標準の Reader Extension API を使用することはできません。 Document Security のポリシーで保護された PDF ドキュメントの使用権限を適用、削除、復元できる API を提供しているのは、ポータブル保護ライブラリ（PPL）の Reader エクステンションサービスのみです。

### Reader拡張サービス {#reader-extensions-service}

Reader Extension サービスは、ポリシーで保護されたPDFドキュメントに使用権限を追加し、Adobe Acrobat Readerを使用してPDFドキュメントを開いた場合に通常使用できない機能をアクティベートします。 また、ポリシーで保護されたドキュメントの使用権限を削除および取得する API も用意されています。

Reader拡張サービスは、PDF標準 1.6 以降に基づくPDFドキュメントを完全にサポートします。 Acrobat Reader以外のサードパーティユーザーは、ポリシーで保護されたPDFドキュメントを使用するために、追加のソフトウェアやプラグインを必要としません。

拡張機能サービスを使用して、次のタスクをReaderできます。

* ポリシーで保護されたPDF・ドキュメントに使用権限を適用する。
* ポリシーで保護されたポリシードキュメントの使用権限をPDFします。
* ポリシーで保護された PDF ドキュメントに適用された使用権限を取得します。

### Document Security のポリシーで保護された PDF ドキュメントに使用権限を適用します。 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

`applyUsageRights` Java API を使用して、ポリシーで保護された PDF ドキュメントに使用権限を適用できます。使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。PDFに使用権限が適用されているドキュメントは、「権限付きドキュメント」と呼ばれます。 Adobe Readerで権限を付与されたドキュメントを開いたユーザーは、そのドキュメントに対して有効になっている操作を実行できます。

**構文：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>使用権限を適用するPDFドキュメントを表す InputStream を指定します。 LiveCycleRights ManagementまたはAEM Forms Document Security で保護されたドキュメントを使用できます。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>.jks ファイルを表す File オブジェクトを指定します。 .jks ファイルはキーストアファイルです。 使用権限を付与する証明書を指しています。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>キーストアのパスワードを指定します。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>タイプのオブジェクトを指定します <a href="https://help.adobe.com/ja_jp/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. usageRights オブジェクトは、ポリシーで保護されたPDF・ドキュメントに適用できる個々の権限を表します。</p> </td>
  </tr>
 </tbody>
</table>

### ポリシーで保護された PDF ドキュメントに適用された使用権限を取得します。  {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

`getDocumentUsageRights` Java API を使用して、ポリシーで保護された PDF ドキュメントの Reader 拡張機能の使用権限を取得できます。使用権限に関する情報を取得することで、ポリシーで保護された PDF ドキュメントで有効にされている Reader 拡張機能の機能を知ることができます。

**構文：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>使用権限を取得するPDFドキュメントを表す InputStream を指定します。 LiveCycleRights ManagementまたはAEM Forms Document Security で保護されたドキュメントを使用できます。</p> </td>
  </tr>
 </tbody>
</table>

#### コードサンプル {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ");
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### ポリシーで保護されたPDFドキュメントの使用権限を削除 {#remove-usage-rights-of-a-policy-protected-pdf-document}

`removeUsageRights` Java API を使用して、ポリシーで保護されたドキュメントから使用権限を削除することができます。ドキュメントに対するその他のAEM Forms操作を実行するには、PDFで保護されたポリシードキュメントから使用権限を削除する必要があります。 例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、PDFで保護されたドキュメントに対して操作を実行する場合は、ポリシードキュメントから使用権限を削除し、ドキュメントの電子署名など他の操作を実行してから、ドキュメントに使用権限を再適用する必要があります。

**構文：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>使用するPDFドキュメントを表す InputStream を指定<br /> 権限を削除します。 LiveCycleRights ManagementまたはAEM Forms Document Security で保護されたドキュメントを使用できます。</td>
  </tr>
 </tbody>
</table>

#### コードサンプル {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
