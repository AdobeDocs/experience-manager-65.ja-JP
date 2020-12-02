---
title: ポータブル保護ライブラリを使用して、ポリシーで保護された PDF ドキュメントを Reader 用に拡張します。
seo-title: ポータブル保護ライブラリを使用して、ポリシーで保護された PDF ドキュメントを Reader 用に拡張します。
description: Reader Extensions により Acrobat Reader を介して Adobe PDF ドキュメントでインタラクティブ機能を使用できます。DRM 保護された PDF ドキュメントを Reader 用に拡張するには、Portable Protection Library（PPL）を使用することができます。
seo-description: Reader Extensions により Acrobat Reader を介して Adobe PDF ドキュメントでインタラクティブ機能を使用できます。DRM 保護された PDF ドキュメントを Reader 用に拡張するには、Portable Protection Library（PPL）を使用することができます。
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 92%

---


# ポータブル保護ライブラリを使用して、ポリシーで保護された PDF ドキュメントを Reader 用に拡張します。{#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Document Security のポリシーによって保護された PDF ドキュメントを Reader 用に拡張するには、Document Security、Reader Extension の概念および Java プログラム言語について詳しくなければなりません。

Document Security を使用して、特定の PDF ドキュメントへのアクセスを認証済のユーザーのみに制限することができます。また、保護されたドキュメントを受信者がどのように使用できるかを指定することができます。例えば、Document Security のポリシーによって保護されたドキュメントで、受信者が印刷、コピー、またはテキスト編集を行えるかどうかを指定できます。Document Security の詳細については、「[Document Security について](/help/forms/using/admin-help/document-security.md)」を参照してください。

Reader Extensions により Acrobat Reader を介して Adobe PDF ドキュメントでインタラクティブ機能を使用できます。通常これらのインタラクティブ機能は、Adobe Acrobat Professional と Standard でのみ可能になります。Reader Extensionで有効にできるインタラクティブ機能については、[Adobe Experience Manager FormsDocAssuranceサービス&#x200B;](/help/forms/using/overview-aem-document-services.md)**を参照してください。**

Portable Protection Library を使用して、ネットワークにドキュメントを送信することなくドキュメントにポリシーを適用できます。ネットワークに送信されるのは、セキュリティ証明書と保護ポリシーの詳細のみです。 実際のドキュメントはクライアントの手元から離れることはなく、保護ポリシーはクライアント側のローカルに適用されます。

## Document Security のポリシーで保護された PDF ドキュメントの Reader 用の拡張  {#reader-extending-document-security-policy-protected-pdf-documents}

ポリシーで保護されたドキュメントは暗号化されています。通常の Reader Extension API では、ポリシーで保護された PDF ドキュメントの使用権限を適用、削除、復元することはできません。Document Security のポリシーで保護された PDF ドキュメントの使用権限を適用、削除、復元できる API を提供しているのは、Portable Protection Library の Reader Extensions サービスのみです。

### Reader Extensions サービス {#reader-extensions-service}

Reader Extension サービスでは、ポリシーで保護された PDF ドキュメントに使用権限を追加し、通常 Adobe Acrobat Reader で PDF ドキュメントを開いた場合に使用できる機能をアクティブにします。このサービスには、ポリシーで保護されたドキュメントの使用権限を削除および復元できる API も用意されています。

Reader Extensions サービスは、PDF 標準 1.6 に基づいた PDF ドキュメントを完全にサポートします。Acrobat Reader は別として、サードパーティユーザーは、ポリシーで保護された PDF ドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。

Reader Extensions サービスを使用すると、次のタスクを実行できます。

* ポリシーで保護された PDF ドキュメントに使用権限を適用。
* ポリシーで保護された PDF ドキュメントの使用権限を削除。
* ポリシーで保護された PDF ドキュメントに適用された使用権限を復元。

### Document Security のポリシーで保護された PDF ドキュメントに使用権限を提供。{#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

`applyUsageRights` Java API を使用して、ポリシーで保護された PDF ドキュメントに使用権限を適用できます。使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

**構文：** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>使用権限を付与する PDF ドキュメントを示す InputStream を指定します。LiveCycle Rights Management または AEM Forms Document Security で保護されたドキュメントを使用することができます。</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>.jks ファイルを示すファイルオブジェクトを指定します。.jks ファイルはキーストアファイルです。このファイルは、使用権限を許可する証明書を指し示します。</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>キーストアのパスワードを指定します。 </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p><a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">usageRights</a> のオブジェクトタイプを指定します。usageRights のオブジェクトは、ポリシーで保護された PDF ドキュメントに適用できる個々の権限を表します。</p> </td>
  </tr>
 </tbody>
</table>

### ポリシーで保護された PDF ドキュメントに適用された使用権限を復元。  {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

`getDocumentUsageRights` Java API を使用して、ポリシーで保護された PDF ドキュメントの Reader Extension の使用権限を復元できます。使用権限に関する情報を取得することで、ポリシーで保護されたPDFドキュメントで有効になっているReader Extensionの機能を確認できます。

**構文：** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>使用権限の復元元の PDF ドキュメントを示す InputStream を指定します。LiveCycle Rights Management または AEM Forms Document Security で保護されたドキュメントを使用することができます。</p> </td>
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

System.out.println("UsageRights applied successfully to the document. ”);
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

### ポリシーで保護された PDF ドキュメントの使用権限の削除 {#remove-usage-rights-of-a-policy-protected-pdf-document}

`removeUsageRights` Java API を使用して、ポリシーで保護されたドキュメントから使用権限を削除することができます。ドキュメントに対してその他の AEM Forms の操作を実行するには、ポリシーで保護された PDF ドキュメントから使用権限を削除する必要があります。例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、ポリシーで保護されたドキュメントに対して操作を行う場合、その PDF ドキュメントから使用権限を削除し、PDF ドキュメントへの電子署名など、その他の操作を行った後にドキュメントに対して使用権限を再び適用します。

**構文：** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>パラメーター</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>使用権限を削除する PDF ドキュメントを示す InputStream を指定します。<br />LiveCycle Rights Management または AEM Forms Document Security で保護されたドキュメントを使用することができます。</td>
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
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

