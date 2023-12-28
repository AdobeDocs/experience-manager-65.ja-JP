---
title: AEM Document Services をプログラムとして使用する
description: Document Services API を使用して、デジタル署名、暗号化、およびPDFドキュメントを生成する方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
source-git-commit: 744cfcee691ea71f33cd56509f65d4f640d4c6e3
workflow-type: tm+mt
source-wordcount: '6348'
ht-degree: 44%

---

# AEM Document Services をプログラムとして使用する  {#using-aem-document-services-programmatically}

このドキュメントのサンプルと例は、OSGi 環境の AEM Forms で AEM ドキュメントサービスを理解し、使用する際に役立ちます。JEE 上の AEM Forms 環境のサンプルと例については、以下を参照してください。

* [Signature Service Java API クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/signature-service-java-api-quick.html?lang=ja#programming-aem-forms-jee)

* [暗号化サービス Java API クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/encryption-service-java-api-quick.html?lang=ja#developer-reference)

* [Acrobat Reader Extensions Service Java API クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=ja#developer-reference)

## 前提条件 {#prerequisite}

* DocAssurance サービスの API を使用する前に、[DocAssurance サービスを設定](/help/forms/using/install-configure-document-services.md)してください。

* [AEM Forms Client SDK](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)をダウンロードして AEM maven プロジェクトと併せて設定してください。AEM ドキュメントサービスを使用して Maven プロジェクトを構築するために必要なクライアントクラスは、[AEM Forms Client SDK](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) から取得することができます。

* [Maven を使用したAEM プロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md)について学ぶ

## DocAssurance サービス {#docassurance-service}

DocAssurance サービスには、次のサービスが含まれます。

* Signature サービス
* Encryption サービス
* Reader拡張サービス

DocAssurance サービスを使用して、次の操作を実行できます。

* [非表示署名の追加](/help/forms/using/aem-document-services-programmatically.md#p-adding-an-invisible-signature-field-p)

* [署名フィールドの追加](/help/forms/using/aem-document-services-programmatically.md#p-adding-a-signature-field-nbsp-p)
* [ドキュメントのタイムスタンプを適用](/help/forms/using/aem-document-services-programmatically.md#apply-document-timestamp)

* [署名の取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-p)
* [署名フィールドリストの取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-signature-field-list-nbsp-p)
* [署名フィールドの変更](/help/forms/using/aem-document-services-programmatically.md#p-modifying-signature-fields-nbsp-p)

* [ドキュメントを保護](/help/forms/using/aem-document-services-programmatically.md#p-securing-documents-p)

* [資格情報の使用権限の取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-credential-usage-rights-p)

* [ドキュメントの使用権限の取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-document-usage-rights-p)

* [使用権限の削除](/help/forms/using/aem-document-services-programmatically.md#p-removing-usage-rights-p)
* [デジタル署名の検証](/help/forms/using/aem-document-services-programmatically.md#p-verifying-digital-signatures-p)
* [複数のデジタル署名の検証](/help/forms/using/aem-document-services-programmatically.md#p-verifying-multiple-digital-signatures-p)
* [デジタル署名の削除](/help/forms/using/aem-document-services-programmatically.md#p-removing-digital-signatures-p)

* [認証署名フィールドの取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-certifying-signature-field-p)
* [PDF の暗号化タイプの取得](/help/forms/using/aem-document-services-programmatically.md#p-getting-pdf-encryption-type-p)
* [パスワード暗号化の削除](/help/forms/using/aem-document-services-programmatically.md#p-removing-password-encryption-from-pdf-p)

* [証明書暗号化の削除](/help/forms/using/aem-document-services-programmatically.md#p-removing-certificate-encryption-p)

>[!NOTE]
>
>Document オブジェクトを Javadoc の入力パラメーターとして使用しているこれらすべてのサービスは、[https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/index.html](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/index.html) で確認することができます。

### 非表示の署名フィールドの追加 {#adding-an-invisible-signature-field}

電子署名は、署名をグラフィカルに表現するフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用することも、プログラムによって署名フィールドを追加することもできます。 どちらの場合においても、PDF ドキュメントに署名するには、署名フィールドが存在している必要があります。プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。PDF ドキュメントに複数の署名フィールドを追加できます。ただし、各署名フィールド名は一意である必要があります。

**構文**：`addInvisibleSignatureField(Document inDoc, String signatureFieldName, FieldMDPOptionSpec fieldMDPOptionsSpec, PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>PDF を含む document オブジェクトです。<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code><br /> </td>
   <td>署名フィールドの名前です。このパラメーターは必須で、値に null を含めることはできません。<br /> </td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>署名フィールドへの署名するとロックされる PDF ドキュメントフィールドを指定する <code>FieldMDPOptionSpec</code> オブジェクトです。このパラメーターはオプションであり、Null 値を取ることができます。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>フィールドのさまざまなシード値を指定する <code>SeedValueOptions</code> オブジェクトです。このパラメーターはオプションであり、Null 値を取ることができます。<span class="acrolinxCursorMarker"></span></td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>暗号化ファイルのロックを解除するために必要なパラメーターが含まれます。このパラメーターは、暗号化ファイルにのみ必要です。</td>
  </tr>
 </tbody>
</table>

PDF ドキュメントに非表示の署名フィールドを追加する Java コードのサンプルを以下に示します。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds an invisible signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddInvisibleSignatureField.class)
public class AddInvisibleSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addInvisibleSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addInvisibleSignatureField(
       inDoc,
       fieldName,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

ドキュメントの署名には [CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29) 仕様も使用できます。次のサンプルコードを使用して、に対する署名形式を設定します。 [CAdES。](https://en.wikipedia.org/wiki/CAdES_%28computing%29)

```java
SigningFormat signingFormat = SigningFormat.CAdES;
sigAppearence.setSigningFormat(signingFormat);
signOptions.setSigAppearence(sigAppearence);
```

### 署名フィールドの追加  {#adding-a-signature-field-nbsp}

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。1 つの署名ドキュメントに複数の署名フィールドをPDFできます。 ただし、各署名フィールド名は一意である必要があります。

**構文**：

```java
public Document addSignatureField(Document inDoc,
 String signatureFieldName,
 Integer pageNo,
 PositionRectangle positionRectangle,
 FieldMDPOptionSpec fieldMDPOptionsSpec,
 PDFSeedValueOptionSpec seedValueOptionsSpec, UnlockOptions unlockOptions)
```

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>PDF を含む document オブジェクトです。</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>署名フィールドの名前。 このパラメーターは必須であり、Null 値は取れません。</td>
  </tr>
  <tr>
   <td><code>pageNumber</code></td>
   <td>署名フィールドを追加するページ番号です。 有効な値は、1 からドキュメントに含まれるページ数までです。 このパラメーターは必須で、null 値を受け入れることはできません。<br /> </td>
  </tr>
  <tr>
   <td><code>positionRectangle</code></td>
   <td>署名フィールドの位置を指定する <code>PositionRectangle object</code> です。このパラメーターは必須であり、Null 値は取れません。指定した長方形が指定したページの切り抜きボックス上に一部でも重なっていない場合は、<code>InvalidArgumentException</code> が発生します。また、指定した長方形の高さと幅は、どちらにも 0 または負の値を指定できません。 左下の X 座標または左下の Y 座標は、0 以上、負ではなく、ページの切り抜きボックスを基準とした相対座標にすることができます。</td>
  </tr>
  <tr>
   <td><code>fieldMDPOptionsSpec</code></td>
   <td>署名フィールドに署名したらロックされる PDF ドキュメントのフィールドを指定する <code>FieldMDPOptionSpec</code> オブジェクトです。このパラメーターはオプションであり、Null を指定することもできます。</td>
  </tr>
  <tr>
   <td><code>seedValueOptionsSpec</code></td>
   <td>フィールドのさまざまなシード値を指定する <code>SeedValueOptions</code> オブジェクトです。このパラメーターはオプションであり、Null を指定することもできます。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 このパラメーターは、暗号化されたファイルに対してのみ必要です。</td>
  </tr>
 </tbody>
</table>

署名ドキュメントに署名フィールドを追加する Java コードのサンプルを以下にPDFします。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures appear in signature fields, which are form fields that contain a graphic representation of the signature.
 * Signature fields can be visible or invisible. Signers can use a pre existing signature field, or a signature field can be
 * programmatically added. In either case, the signature field must exist before a PDF document can be signed.
 * You can programmatically add a signature field by using the Signature service Java API or Signature web service API.
 * You can add more than one signature field to a PDF document; however, each signature field name must be unique.
 *
 * The following Java code example adds a signature field named SignatureField1 to a PDF document.
 */

@Component
@Service(value=AddSignatureField.class)
public class AddSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to an pdf document stored at disk
  * @param outputFile - path where the output file has to be saved
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  *
  */
 public void addSignatureField(String inputFile, String outputFile) throws InvalidArgumentException, PDFOperationException, PermissionsException, DuplicateSignatureFieldException, SignaturesBaseException, DocAssuranceException {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a  PositionRectangle object that specifies
        //the signature fields location
        PositionRectangle post = new  PositionRectangle(193,47,133,12);

        //Specify the page number that will contain the signature field
        java.lang.Integer pageNum = new java.lang.Integer(1);

        //Add a signature field to the PDF document
        try {
   outDoc = docAssuranceService.addSignatureField(
       inDoc,
       fieldName,
       pageNum,
       post,
       null,
       null,
       null);
  } catch (Exception e1) {
   // TODO Auto-generated catch block
   e1.printStackTrace();
  } // for an encrypted PDF input, pass unlock options

        //save the outDoc
        try {
   outDoc.copyToFile(outFile);
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
 }

 /**
  *
  * UnlockOptions to be passed to addSignatureField() API to add a signature field in an encrypted pdf document.
  */
 private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### ドキュメントのタイムスタンプを適用 {#apply-document-timestamp}

[PAdES 4](https://en.wikipedia.org/wiki/PAdES) 仕様に従って、プログラムでドキュメントにタイムスタンプを押すことができます。トランザクション関連のドキュメントには、[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29) 仕様も使用できます。

**構文**：`applyDocumentTimeStamp(Document doc, VerificationTime verificationTime, ValidationPreferences dssPrefs, ResourceResolver resourceResolver, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>PDF を含む document オブジェクトです。<br /> </td>
  </tr>
  <tr>
   <td><code>VerificationTime</code></td>
   <td>署名が検証される時間です。<br /> </td>
  </tr>
  <tr>
   <td><code>ValidationPreferences</code> </td>
   <td>検証の設定を管理する環境設定です。</td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>Granite Trust Store に対するリソースリゾルバーです。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 これは、ファイルが暗号化されている場合にのみ必要です。</td>
  </tr>
 </tbody>
</table>

以下のコードサンプルでは、 [PAdES 4](https://en.wikipedia.org/wiki/PAdES).

```java
package com.adobe.signatures.test;

import java.io.File;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

 @Component
 @Service(value=Test.class)
 public class Test {

     @Reference
     private DocAssuranceService docAssuranceService;

     @Reference
     private SlingRepository slingRepository;

     @Reference
     private JcrResourceResolverFactory jcrResourceResolverFactory ;

     /**
      *
      * @param inputFile - path to the pdf document stored at disk
      * @param outputFile - path to the pdf document where the output needs to be stored
      * @throws Exception
      */
     public void TimeStamp(String inputFile, String outputFile) throws Exception{

         File inFile = new File(inputFile);
         Document inDoc = new Document(inFile);

         File outFile = new File(outputFile);
         Document outDoc = null;

         Session adminSession = null;
         ResourceResolver resourceResolver = null;
         try {

              /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
              the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
              the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
              here we are using the same resource resolver
              */
              adminSession = slingRepository.loginAdministrative(null);
              resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

              VerificationTime verificationTime = getVerificationTimeForPades();
              ValidationPreferences dssPrefs = getValidationPreferences();

              //retrieve specifications for each of the services, you may pass null if you don't want to use that service
              //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
               outDoc = docAssuranceService.applyDocumentTimeStamp(inDoc, verificationTime, dssPrefs, resourceResolver, null);
         }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

         outDoc.copyToFile(outFile);

     }

  public  VerificationTime getVerificationTimeForPades(){

         return VerificationTime.SECURE_TIME_ELSE_CURRENT_TIME;

     }

 /**
       * sets ValidationPreferences
       */
      private static ValidationPreferences getValidationPreferences(){

         ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
         prefs.setPKIPreferences(getPKIPreferences());

         //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected

         return prefs;

     }

   /**
       * sets PKIPreferences
       */
     private static PKIPreferences getPKIPreferences(){
         PKIPreferences pkiPref = new PKIPreferencesImpl();
         pkiPref.setCRLPreferences(getCRLPreferences());
         pkiPref.setPathPreferences(getPathValidationPreferences());
         pkiPref.setOCSPPreferences(getOCSPPref());
         pkiPref.setTSPPreferences(getTspPref());
         return pkiPref;
     }

   /**
      * sets CRL Preferences
      */
     private static CRLPreferences getCRLPreferences(){

         CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
         crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
         crlPrefs.setGoOnline(true);
         return crlPrefs;
     }

     /**
      *
      * sets PathValidationPreferences
      */
     private static PathValidationPreferences getPathValidationPreferences(){
         PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
         pathPref.setDoValidation(true);
         return pathPref;

     }

   public static TSPPreferences getTspPref(){
   TSPPreferencesImpl tspPrefs=new TSPPreferencesImpl();
   char pass[]=new char[9];

   tspPrefs.setTspServerURL("TSPPrefs_ServerURL");
   tspPrefs.setUsername("TSPPrefs_Username");
   tspPrefs.setPassword(pass);
   tspPrefs.setSize(10240);
   return tspPrefs;
   }

     private static OCSPPreferencesImpl getOCSPPref(){
         OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
         ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
         return ocsp;
     }

}
```

### 署名を取得しています {#getting-signature}

署名または認証する署名ドキュメント内のすべてのPDFフィールドの名前を取得できます。 PDFドキュメント内の署名フィールド名が不明な場合や、名前を検証する場合は、プログラムを使用して名前を取得します。 Signature サービスは、`form1[0].grantApplication[0].page1[0].SignatureField1[0]` のような署名フィールドの完全修飾名を返します。

**構文**：`getSignature(Document doc, String signatureFieldName, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>doc</code><br /> </td>
   <td>PDF を含む document オブジェクトです。<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>署名が含まれている署名フィールドの名前です。 署名フィールドの完全修飾名を指定します。 XFA フォームに基づくPDFドキュメントを使用する場合、署名フィールドの名前の一部を使用できます。 例えば、<code>form1[0].#subform[1].SignatureField3[3]</code> は <code>SignatureField3[3]</code> として指定できます。</td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 これは、ファイルが暗号化されている場合にのみ必要です。</td>
  </tr>
 </tbody>
</table>

次の Java コードの例では、署名ドキュメント内の指定された署名フィールドの署名情報をPDFします。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.client.types.PDFSignature;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetSignature.class)
public class GetSignature {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void GetSignature(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignature pdfSignature = docAssuranceService.getSignature(inDoc,"fieldName",null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 署名フィールドリストを取得しています  {#getting-signature-field-list-nbsp}

署名または認証する署名ドキュメント内のすべてのPDFフィールドの名前を取得できます。 署名ドキュメント内の署名フィールド名が不明な場合は、プログラムによってPDFを取得し、検証することができます。 Signature サービスは、`form1[0].grantApplication[0].page1[0].SignatureField1[0]` のような署名フィールドの完全修飾名を返します。

**構文**：`public List <PDFSignatureField> getSignatureFieldList (Document inDoc, UnlockOptions unlockOptions)`

**入力パラメーター**

| パラメーター | 説明 |
|---|---|
| `inDoc` | PDF を含む document オブジェクトです |
| `unlockOptions` | 暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 これは、ファイルが暗号化されている場合にのみ必要です。 |

次の Java コードの例では、署名ドキュメント内の署名フィールドの名前をPDFします。

```java
/*************************************************************************
 *
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------
**************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the names of signature fields in a PDF document.
 */

@Component
@Service(value=GetSignatureFields.class)
public class GetSignatureFields {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getSignatureFields(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve the name of the document's signature fields
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        List fieldNames = docAssuranceService.getSignatureFieldList(inDoc,null);

        //Obtain the name of each signature field by iterating through the
        //List object
        Iterator iter = fieldNames.iterator();
        int i = 0 ;
        String fieldName="";
        while (iter.hasNext()) {
            PDFSignatureField signatureField = (PDFSignatureField)iter.next();
            fieldName = signatureField.getName();
            System.out.println("The name of the signature field is " +fieldName);
            i++;
        }
   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 署名フィールドの変更  {#modifying-signature-fields-nbsp}

署名ドキュメント内の署名フィールドを変更することがPDFできます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

フィールドロックディクショナリは、署名フィールドへの署名時にロックするフィールドのリストを指定します。フィールドがロックされると、ユーザーはそのフィールドを編集できません。シード値ディクショナリには、署名の適用時に使用される制約情報が含まれます。例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更することで、PDF を編集し、ビジネス要件の変更を反映させることができます。例えば、新しいビジネス要件ではドキュメントに署名が行われたあと、すべてのドキュメントフィールドをロックしなければいけない場合などです。

**構文**：`public Document modifySignatureField(Document inDoc, String signatureFieldName, PDFSignatureFieldProperties pdfSignatureFieldProperties, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code></td>
   <td>PDF を含む document オブジェクトです。</td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>署名フィールドの名前です。このパラメーターは必須で、null 値を受け入れることはできません。<br /> </td>
  </tr>
  <tr>
   <td><code>pdfSignatureFieldProperties</code></td>
   <td>署名フィールドの <code>PDFSeedValueOptionSpec</code> と <code>FieldMDPOptionSpec</code> の値に関する情報を指定するオブジェクトです。</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 これは、ファイルが暗号化されている場合にのみ必要です。</td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、署名フィールドに署名が適用された際に、フォーム内のすべてのフィールドをロックして署名フィールドを修正することができます。

```java
/*************************************************************************
 *

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.FieldMDPAction;
import com.adobe.fd.signatures.client.types.FieldMDPOptionSpec;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.PDFSeedValueOptionSpec;
import com.adobe.fd.signatures.client.types.PDFSignatureFieldProperties;
import com.adobe.fd.signatures.client.types.PositionRectangle;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.MissingSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignatureFieldSignedException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can modify signature fields that are in a PDF document by using the Java API and web service API. Modifying a signature field involves
 * manipulating its signature field lock dictionary values or seed value dictionary values.
 * A field lock dictionary specifies a list of fields that are locked when the signature field is signed. A locked field prevents users from making
 * changes to the field. A seed value dictionary contains constraining information that is used at the time the signature is applied.
 * For example, you can change permissions that control the actions that can occur without invalidating a signature.
 * By modifying an existing signature field, you can change the PDF document to reflect changing business requirements. For example,
 * a new business requirement may require locking all document fields after the document is signed.
 * This section explains how to modify a signature field by amending both field lock dictionary and seed value dictionary values.
 * Changes made to the signature field lock dictionary result in all fields in the PDF document being locked when a signature field is signed.
 * Changes made to the seed value dictionary prohibit specific types of changes to the document.
 *
 * The following Java code example modifies a signature field named SignatureField1 by locking all fields in the form when a signature is applied to the signature field and ensuring that no changes are allowed.
 * After the Signature service returns the PDF document that contains the modified signature field
 */

@Component
@Service(value=ModifySignatureField.class)
public class ModifySignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  *
  *
  */
 public void modifySignatureField(String inputFile, String outFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Create a PDFSignatureFieldProperties
        PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();

         //Create a PDFSeedValueOptionSpec object that stores
         //seed value dictionary information.
         PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();

         //Disallow changes to the PDF document. Any change to the document invalidates
         //the signature
         seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);

         //Create a FieldMDPOptionSpec object that stores
         //signature field lock dictionary information.
         FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();

         //Lock all fields in the PDF document
         fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);

         //Set dictionary information
         fieldProperties.setSeedValue(seedOptionsSpec);
         fieldProperties.setFieldMDP(fieldMDPOptionsSpec);

         //Modify the signature field
         //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
         Document modSignatureField =  docAssuranceService.modifySignatureField(inDoc,fieldName,fieldProperties,null);

        //save the modSignatureField
         modSignatureField.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 認証PDF書  {#certifying-pdf-documents-nbsp}

認証済みPDFと呼ばれる特定の種類の署名を使用して認証することで、署名ドキュメントを保護できます。 認証済みの署名は、次の点でデジタル署名と区別されます。

* PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。署名ドキュメントの署名とPDFを行うには、署名前に認証を行ってください。 署名ドキュメントを認証した後、PDFフィールドに電子署名を行うことができます。
* ドキュメントの作成者または作成者は、認証された署名を無効にすることなく、特定の方法でドキュメントを変更できるように指定できます。 例えば、ドキュメントでは、フォームへの入力やコメントを許可することができます。作成者が特定の変更を許可しない設定を行った場合は、その方法でのドキュメントの変更は Acrobat によって制限されます。そのような変更が行われた場合は、認証署名は無効となります。さらに、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名の場合、変更は防止されず、通常の編集操作で元の署名が無効になることはありません）。
* 署名時に、文書の内容をあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツを文書にスキャンします。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。このようなコンテンツに関する説明（法的証明）を提供できます。

**構文**:

```java
secureDocument(Document inDoc, EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions, ReaderExtensionOptions readerExtensionOptions, UnlockOptions unlockOptions)
```

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>PDF ドキュメントを入力するドキュメント<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>PDF ドキュメントの暗号化に必要な引数が含まれます<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>PDF ドキュメントへの署名や認証に必要なオプションが含まれます</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>PDF ドキュメントの Reader 用の拡張に必要なオプションが含まれます</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。これは、ファイルが暗号化されている場合にのみ必要です。<br /> </td>
  </tr>
 </tbody>
</table>

次のコードのサンプルは、PDFファイルに基づくPDFドキュメントを認証します。

```java
/*************************************************************************

-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * You can secure a PDF document by certifying it with a particular type of signature called a certified signature.
 * A certified signature is distinguished from a digital signature in these ways:
 *
 * It must be the first signature applied to the PDF document; that is, at the time the certified signature is applied, any other signature fields in the document must be unsigned.
 * Only one certified signature is permitted in a PDF document. If you want to sign and certify a PDF document, you must certify it before signing it.
 * After you certify a PDF document, you can digitally sign additional signature fields.
 *
 * The author or originator of the document can specify that the document can be modified in certain ways without invalidating the certified signature. For example,
 * the document may permit filling in forms or commenting. If the author specifies that a certain modification is not permitted, Acrobat restricts users from modifying the document
 * in that way. If such modifications are made, such as by using another application, the certified signature is invalid and Acrobat issues a warning when a user opens the document.
 * (With non-certified signatures, modifications are not prevented, and normal editing operations do not invalidate the original signature.)
 *
 * At the time of signing, the document is scanned for specific types of content that could make the contents of a document ambiguous or misleading. For example, an annotation could
 * obscure some text on a page that is important for understanding what is being certified. An explanation (legal attestation) can be provided about such content.
 * You can programmatically certify PDF documents by using the Signature service Java API or the Signature web service API. When certifying a PDF document, you must reference a security
 * credential that exists in the Credential service.
 *
 * Note: When certifying and signing the same PDF document, if the certify signature is not trusted, a yellow triangle appears next to the first sign signature when you open the PDF document in Acrobat or Adobe Reader.
 * The certifying signature must be trusted to avoid this situation.
 *
 * The following Java code example certifies a PDF document that is based on a PDF file.
 *
 * PreRequisites - Digital certificate for certifying the document has to be uploaded on AEM Key Store.
 *
 */

@Component
@Service(value=Certify.class)
public class Certify {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void certify(String inputFile, String outputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //we are not extending the reader in this case, so passing null
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    try {
    outDoc = docAssuranceService.secureDocument(inDoc, null, getCertificationOptions(resourceResolver), null,null);
   } catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
   }

        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA256;

        //Reason for signing/certifying
        String reason = "Reason";

        //location of the signer
        String location = "Location";

        //contact info of the signer
        String contactInfo = "Contact Info";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, false, true, true, TextDirection.AUTO);
        signatureOptions.setLockCertifyingField(true);
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### ドキュメントの保護 {#securing-documents}

secureDocument を使用すると、PDF ドキュメントの暗号化、署名および認証、Reader 用の拡張を、個別に、または任意の順序で組み合わせて行うことができます。この機能にアクセスするには、対応する引数を渡します。 null の場合は、特定の処理が必要ないと見なされます。

**パスワードを使用したPDFドキュメントの暗号化**

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、別のAEM Forms Document Services の操作がドキュメントを使用する前に、パスワードで暗号化されたPDFドキュメントのロックを解除する必要があります。

**証明書を使用したPDFドキュメントの暗号化**

証明書ベースの暗号化では、公開鍵技術を使用して特定の受信者向けにドキュメントを暗号化できます。

様々な受信者に、ドキュメントに対する異なる権限を与えることができます。公開鍵のテクノロジーによって、暗号化の様々な側面が可能になります。

アルゴリズムは、次のプロパティを持つキーと呼ばれる大きな数値を 2 つ生成するために使用します。

* 鍵のうち 1 つは、1 組のデータを暗号化するために使用されます。後で、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう一方の鍵と区別することは不可能です。
* キーの 1 つが、ユーザーの秘密鍵として機能します。 当該のユーザーのみがこの鍵にアクセスできることが重要です。
* もう 1 つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 X.509 形式は、証明書の保存に使用されます。 証明書は、通常、認証局 (CA) によって発行され、デジタル署名されます。CA は、証明書の有効性に対する信頼性の尺度を提供する認識済みのエンティティです。 証明書には有効期限があり、この期限を過ぎると無効になります。

また、証明書失効リスト (CRL) は、有効期限より前に失効した証明書に関する情報を提供します。 CRL は、認証局によって定期的に公開されます。 証明書の失効ステータスは、ネットワーク上のオンライン証明書ステータスプロトコル (OCSP) を通じて取得することもできます。

>[!NOTE]
>
>PDF ドキュメントを証明書で暗号化できるようにするには、まず AEM Trust Store に証明書が追加されていることを確認する必要があります。

**使用権限のPDFドキュメントへの適用**

拡張機能 Java クライアント API と Web サービスを使用して、PDFドキュメントにReader権限を適用できます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。PDFに使用権限が適用されているドキュメントは、「権限付きドキュメント」と呼ばれます。 Adobe Readerで権限を付与されたドキュメントを開いたユーザーは、そのドキュメントに対して有効になっている操作を実行できます。

証明書を使用してPDFドキュメントのReaderを設定する前に、証明書をAEMキーストアに追加する必要があります。

**デジタル署名PDF文書**

デジタル署名を PDF ドキュメントに適用して、一定レベルのセキュリティを提供できます。デジタル署名は、手書きの署名と同様に、署名者が自分自身を識別し、ドキュメントに関するステートメントを作成する手段を提供します。

ドキュメントに電子署名を行う技術は、署名者と受信者の両方が、何が署名されたかを明確にし、ドキュメントが署名後に変更されなかったことを確実に示すのに役立ちます。

PDFドキュメントは、公開鍵技術によって署名されます。 署名者には、公開鍵と秘密鍵の 2 つの鍵があります。 秘密鍵は、署名時に使用可能である必要があるユーザーの資格情報に保存されます。

公開鍵はユーザーの証明書に保存されます。この証明書は、受信者が署名を検証するために使用できる必要があります。 失効した証明書に関する情報は、証明機関 (CA) から配布された証明書失効リスト (CRL) およびオンライン証明書ステータスプロトコル (OCSP) 応答に含まれています。 署名時刻は、タイムスタンプ機関と呼ばれる、信頼できるソースから取得できます。

>[!NOTE]
>
>PDF ドキュメントにデジタル署名を行うには、まず AEM キーストアに資格情報が追加されていることを確認する必要があります。資格情報は、署名に使用する秘密鍵です。

>[!NOTE]
>
>AEM Forms では、PDF ドキュメントのデジタル署名で *[CAdES](https://en.wikipedia.org/wiki/CAdES_%28computing%29)* 仕様もサポートしています。

**PDF ドキュメントの認証**

認証済みPDFと呼ばれる特定の種類の署名を使用して認証することで、署名ドキュメントを保護できます。 認証済みの署名は、次の点でデジタル署名と区別されます。

認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。

認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。

署名ドキュメントを認証した後、PDFフィールドに電子署名を行うことができます。

ドキュメントの作成者または作成者は、認証された署名を無効にすることなく、特定の方法でドキュメントを変更できるように指定できます。

例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が、特定の変更を許可しないと指定した場合、

Acrobat はユーザーがその方法でドキュメントを変更することを制限します。別のアプリケーションの使用などによる変更がおこなわれた場合、認証署名は無効になり、Acrobatはユーザーがドキュメントを開いたときに警告を発します。 （未認証の署名の場合、変更は防止されず、通常の編集操作で元の署名が無効になることはありません）。

署名時に、文書の内容をあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツを文書にスキャンします。

例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。このようなコンテンツに関する説明（法的証明）を提供できます。

>[!NOTE]
>
>PDF ドキュメントにデジタル署名を行うには、まず AEM キーストアに資格情報が追加されていることを確認する必要があります。資格情報は、署名に使用する秘密鍵です。

**構文**：

```java
secureDocument(Document inDoc,
 EncryptionOptions encryptionOptions,
 SignatureOptions signatureOptions,
 ReaderExtensionOptions readerExtensionOptions,
 UnlockOptions unlockOptions)
```

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>入力する PDF ドキュメント<br /> </td>
  </tr>
  <tr>
   <td><code>encryptionOptions</code><br /> </td>
   <td>PDF ドキュメントの暗号化に必要な引数が含まれます<br /> </td>
  </tr>
  <tr>
   <td><code>signatureOptions</code></td>
   <td>PDF ドキュメントの署名や認証に必要なオプションが含まれます</td>
  </tr>
  <tr>
   <td><code>readerExtensionOptions</code></td>
   <td>PDF ドキュメントの Reader 用の拡張に必要なオプションが含まれます</td>
  </tr>
  <tr>
   <td><code>unlockOptions</code></td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。これは、ファイルが暗号化されている場合にのみ必要です。<br /> </td>
  </tr>
 </tbody>
</table>

**サンプル 1**：このサンプルは、パスワードの暗号化、署名フィールドの認証、Readerドキュメントの拡張の実行に使用されます。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.PasswordEncryptionCompatability;
import com.adobe.fd.encryption.client.PasswordEncryptionOption;
import com.adobe.fd.encryption.client.PasswordEncryptionOptionSpec;
import com.adobe.fd.encryption.client.PasswordEncryptionPermission;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.MDPPermissions;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * password encryption, certifying a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptCertifyExtend.class)
public class PassEncryptCertifyExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void SecureDocument(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getPassEncryptionOptions(), getCertificationOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getPassEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

  //Create a PasswordEncryptionOptionSpec object that stores encryption run-time values
        PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();

        //Specify the PDF document resource to encrypt
        passSpec.setEncryptOption(PasswordEncryptionOption.ALL);

        //Specify the permission associated with the password
        //These permissions enable data to be extracted from a password
        //protected PDF form
        List<PasswordEncryptionPermission> encrypPermissions = new ArrayList<PasswordEncryptionPermission>();
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_ADD);
        encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_MODIFY);
        passSpec.setPermissionsRequested(encrypPermissions);

        //Specify the Acrobat version
        passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);

        //Specify the password values
        passSpec.setDocumentOpenPassword("OpenPassword");
        passSpec.setPermissionPassword("PermissionPassword");

        //Set the encryption type to Password Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_PASSWORD);
        encryptionOptions.setPasswordEncryptionOptionSpec(passSpec);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getCertificationOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.CERTIFY);

  //signature field to certify, pass null if invisible signature field
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //DocMDP Permissions associated with certification
        MDPPermissions mdpPermissions = MDPPermissions.valueOf("FormChanges");

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
        signatureOptions.setMdpPermissions(mdpPermissions);
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

**サンプル 2**：このサンプルは、PKI 暗号化の実行、署名フィールドへの署名、Readerドキュメントの拡張に使用されます。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.EncryptionOptions;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.encryption.client.CertificateEncryptionCompatibility;
import com.adobe.fd.encryption.client.CertificateEncryptionIdentity;
import com.adobe.fd.encryption.client.CertificateEncryptionOption;
import com.adobe.fd.encryption.client.CertificateEncryptionOptionSpec;
import com.adobe.fd.encryption.client.CertificateEncryptionPermissions;
import com.adobe.fd.encryption.client.Recipient;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * certificate encryption, signing a signature field and reader extending the pdf document.
 *
 * PreRequisites - Digital certificate for encrypting the document has to be uploaded on Granite Trust Store
       Digital certificate for signing the document has to be uploaded on Granite Key Store
 * Digital certificate for reader extending the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=PassEncryptSignExtend.class)
public class PassEncryptSignExtend {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws Exception
  */
 public void CertEncryptSignReaderExtend(String inputFile, String outputFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  File outFile = new File(outputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, getCertEncryptionOptions(), getSignatureOptions(resourceResolver), getReaderExtensionOptions(resourceResolver),null);
        }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        outDoc.copyToFile(outFile);

 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

 /**
  * @return EncryptionOptions for password encrypting the document.
  *
  */
 private EncryptionOptions getCertEncryptionOptions(){

  //Create an instance of EncryptionOptions
  EncryptionOptions encryptionOptions = EncryptionOptions.getInstance();

        //Set the encryption type to Certificate Encryption
  encryptionOptions.setEncryptionType(DocAssuranceServiceOperationTypes.ENCRYPT_WITH_CERTIFCATE);

  //Set the List that stores PKI information
  List<CertificateEncryptionIdentity> pkiIdentities = new ArrayList<CertificateEncryptionIdentity>();

  //Set the Permission List
  List<CertificateEncryptionPermissions> permList = new ArrayList<CertificateEncryptionPermissions>();
  permList.add(CertificateEncryptionPermissions.PKI_ALL_PERM) ;

  //Create a Recipient object to store certificate information
  Recipient recipient = new Recipient();

  //Specify the alias of the public certificate present in the trust store that is used to encrypt the document
  recipient.setX509Cert("alias");
  /*
   * An alternative to add a certificate is by providing the alias
   * of the certificate stored in AEM trust store.
   * recipient.setAlias(alias);
   */

  //Create an EncryptionIdentity object
  CertificateEncryptionIdentity encryptionId = new CertificateEncryptionIdentity();
  encryptionId.setPerms(permList);
  encryptionId.setRecipient(recipient);

  //Add the EncryptionIdentity to the list
  pkiIdentities.add(encryptionId);

  //Set encryption run-time options
  CertificateEncryptionOptionSpec certOptionsSpec = new CertificateEncryptionOptionSpec();
  certOptionsSpec.setOption(CertificateEncryptionOption.ALL);
  certOptionsSpec.setCompat(CertificateEncryptionCompatibility.ACRO_9);

  //Set the certificate encryption option
  encryptionOptions.setCertOptionSpec(certOptionsSpec)

  //Set the PKI Identities in encryption Options
        encryptionOptions.setPkiIdentities(pkiIdentities);

     return encryptionOptions;
 }

 /**
  *
  * @param resourceResolver corresponding to the user with the access to Reader Extension credential
  * for the given alias -"production" in this case
  * @return
  */
 private ReaderExtensionOptions getReaderExtensionOptions(ResourceResolver resourceResolver){

  //Create an instance of ReaderExtensionOptions
  ReaderExtensionOptions reOptions = ReaderExtensionOptions.getInstance();

  //Create instance for UsageRights to be enabled in the reader
  UsageRights uRights = new UsageRights();
  //enabling comments in the PDF Reader
  uRights.setEnabledComments(true);
  //setting ReaderExtensionsOptionSpec in the reOptions
  reOptions.setReOptions(new ReaderExtensionsOptionSpec(uRights, "Enable commenting in PDF"));
  //alias of the credential to be used for extending the PDF Reader
  reOptions.setCredentialAlias("production");
  //corresponding to the user with the access to Reader Extension credential
  reOptions.setResourceResolver(resourceResolver);

  return reOptions;
 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

  //alias of the private credential uploaded on the Key Store
        String alias = "allcertificatesanypolicytest11ee_new";

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

}
```

Reader が PDF ドキュメントの拡張中に、次のエラーメッセージが表示される場合：

```javascript
org.apache.sling.engine.impl.SlingRequestProcessorImpl service: Uncaught Throwable java.lang.ThreadDeath: null at com.adobe.internal.pdftoolkit.services.javascript.GibsonContextFactory.observeInstructionCount(GibsonContextFactory.java:138)
```

Reader 拡張サービスが、ドキュメントで使用されている JavaScript を所定のタイムアウト間隔内に実行できなかったことを示しています。

次を使用して、PDF ドキュメント内の JavaScripts に定義されたタイムアウト間隔を管理します。

```javascript
ReaderExtensionsOptionSpec optionSpec = new ReaderExtensionsOptionSpec(usageRights, message);
optionSpec.setJsScriptExecutionTimeoutInterval(100);
```

ここで、100 は、JavaScripts の実行のために定義したタイムアウト間隔（秒）です。タイムアウト間隔に適切な値を設定します。

### 資格情報の使用権限の取得 {#getting-credential-usage-rights}

特定の `credentialAlias` で指定された資格情報の使用権限に関する情報を取得するには、この API を `SecureDocument` API 内から呼び出します。

**構文**：`getCredentialUsageRights(String credentialAlias, ResourceResolver resourceResolver)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>credentialAlias</code><br /> </td>
   <td>資格情報を指定する <code>credentialAlias</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>credentialPassword</code><br /> </td>
   <td>秘密鍵証明書が暗号化されている場合は、秘密鍵証明書のパスワードを使用し、秘密鍵証明書が暗号化されていない場合は null を使用する必要があります。<br /> </td>
  </tr>
 </tbody>
</table>

以下のサンプルは、指定した秘密鍵証明書の使用権限情報を取得します。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 *
 */
@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
 private ResourceResolverFactory resourceResolverFactory;
public void getCredentialUsageRights() {
  try {

   GetUsageRightsResult usageRightsResult = docAssuranceService.getCredentialUsageRights("production",
     resourceResolverFactory.getAdministrativeResourceResolver(null));

   System.out.println("Credential usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  }
 }
}
```

### ドキュメント使用権限の取得 {#getting-document-usage-rights}

特定のドキュメントの使用権限情報を取得するには、この API を `docAssuranceService` API から呼び出します。

**構文**：`getDocumentUsageRights(Document inDocument, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>使用権限情報を取得するドキュメント<br /> </td>
  </tr>
 </tbody>
</table>

次のサンプルコードは、ドキュメントの使用権限情報を返します。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void getDocumentUsageRights() {
  Document inputDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/GetUsageRightsInfo/02_fromAcrobat7.0.8_Acro700_UB8_BS_signed_commenting.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   GetUsageRightsResult usageRightsResult = docAssuranceService.getDocumentUsageRights(inputDocument, unlockOptions);

   System.out.println("Document usage Rights are as follows");
   System.out.println(usageRightsResult.toString());

  } catch (Exception e) {
   e.printStackTrace();
  } finally {
//   if (inputDocument != null) {
//    inputDocument.dispose(); //dispose off the document.
//   }
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

### 使用権限の削除 {#removing-usage-rights}

`docAssuranceService` API から `removeUsageRights` API を呼び出すことによって、ドキュメントの使用権限を削除できます。

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDocument</code><br /> </td>
   <td>使用権限を削除するドキュメントです。<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。 これは、ファイルが暗号化されている場合にのみ必要です。<br /> </td>
  </tr>
 </tbody>
</table>

以下のサンプルでは、特定のドキュメントの使用権限を削除します。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.fd.readerextensions.samples;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.jcr.SimpleCredentials;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.LoginException;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.jcr.resource.JcrResourceConstants;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.ReaderExtensionOptions;
import com.adobe.fd.readerextensions.client.GetUsageRightsResult;
import com.adobe.fd.readerextensions.client.ReaderExtensionsOptionSpec;
import com.adobe.fd.readerextensions.client.UsageRights;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

@Component(metatype = true, immediate = true, label = "ReaderExtensionsSampleService")
@Service(value = ReaderExtensionsSampleService.class)
public class ReaderExtensionsSampleService {

 @Reference(referenceInterface=DocAssuranceService.class)
 private DocAssuranceService docAssuranceService;

 @Reference(referenceInterface=ResourceResolverFactory.class)
private ResourceResolverFactory resourceResolverFactory;

public void removeDocumentUsageRights() {
  Document inputDocument = null;
  Document outDocument = null;
  try {
   //Name of the input file on which usage rights is to be applied.
   String inputFileName = "C:/RETest/input/RemoveUsageRights/01_Ubiquitized_50-267_PDF1.5_UB2_Rights.pdf";

   //Name of the output file where result will be saved.
   String outputFileName = "C:/RETest/output/samples/removeUsageRightsOutput.pdf";

   //Document to be input to Doc Assurance Service
   inputDocument = new Document(new File(inputFileName));

   //Unlock options to unlock the document if some kind of security is set on it.
   //Currently set to null because input document has no security.
   UnlockOptions unlockOptions = null;

   //Specify null encryption options and signatures options.
   //If requirement is also to encrypt and sign the document then, corresponding options can also be specified.
   outDocument = docAssuranceService.removeUsageRights(inputDocument, unlockOptions);

   File outputdir = new File("C:/RETest/output/samples");
   outputdir.mkdirs();

   outDocument.copyToFile(new File(outputFileName));
  } catch (Exception e) {
   e.printStackTrace();
  }
}

/**
  * Resource resolver of the user in whose keystore Reader Extensions Certificate is installed.
  * @param resourceResolverFactory
  * @return
  * @throws LoginException
  */
 public ResourceResolver getResourceResolver() throws LoginException{
  Map<String,Object> authInfo = new HashMap<String,Object>();
  //Username and password of the user in whose keystore Reader Extensions Certificate is installed
  SimpleCredentials credentials = new SimpleCredentials("username"/*UserName*/, "password"/*Password*/.toCharArray());
  authInfo.put(JcrResourceConstants.AUTHENTICATION_INFO_CREDENTIALS,credentials);
  return resourceResolverFactory.getResourceResolver(authInfo);
}

}
```

#### 電子署名の検証 {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者の ID などの署名のプロパティを確認できます。 デジタル署名を信頼する前に、検証することをお勧めします。 デジタル署名を検証する場合は、デジタルPDFを含む署名ドキュメントを参照します。

**構文**：`verify( inDoc, signatureFieldName, revocationCheckStyle, verificationTime, dssPrefs, ResourceResolver resourceResolver)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>PDF を含む document オブジェクトです<br /> </td>
  </tr>
  <tr>
   <td><code class="code">signatureField
      Name</code><br /> </td>
   <td>検証する署名フィールドの名前。 完全修飾名または名前の一部を指定できます<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>検証中に発生した証明書の失効確認を管理するオプションです</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>署名が検証される時間です</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>さまざまな検証の設定を管理する環境設定です。暗号化されたドキュメントの場合、ロック解除オプションを設定するには次を使用します。 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Granite Trust Store に対するリソースリゾルバーです</td>
  </tr>
 </tbody>
</table>

以下のサンプルコードでは、暗号化された PDF ドキュメントの署名フィールドを検証するため、`DocAssuranceService` を使用しています。

```java
/*************************************************************************
 *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.IdentityInformation;
import com.adobe.fd.signatures.client.types.IdentityStatus;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.OCSPPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.TSPPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of a signature field in an already Encrypted PDF Document
 *
 * Digital signatures can be verified to ensure that a signed PDF document was not modified and that the digital signature is valid.
 * When verifying a digital signature, you can check the signature's status and the signature's properties, such as the signer's identity.
 * Before trusting a digital signature, it is recommended that you verify it. When verifying a digital signature, reference a PDF document
 * that contains a digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyFieldEncryptedPDF.class)
public class VerifyFieldEncryptedPDF {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyFieldEncryptedPDF(String inputFile,String fieldName) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

         //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

           //Specify the name of the signature field

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.AlwaysCheck;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFSignatureVerificationInfo  signInfo = docAssuranceService.verify(
                 inDoc,
                 fieldName,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get the Signature Status
             SignatureStatus sigStatus = signInfo.getStatus();
             String myStatus="";

             //Determine the status of the signature
             if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                 myStatus = "The signatures in the dynamic PDF form are unknown";
             else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                 myStatus = "The signatures in the PDF document are unknown";
             else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a certified PDF form are valid";
             else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                 myStatus = "The signatures in a signed dynamic PDF form are valid";
             else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                 myStatus = "The signatures in a certified PDF document are valid";
             else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                 myStatus = "The signatures in a signed PDF document are valid";
             else if (sigStatus == SignatureStatus.SignatureFormatError)
                 myStatus = "The format of a signature in a signed document is invalid";
             else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                 myStatus = "No changes were made to the signed dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                 myStatus = "No changes were made to the signed PDF document";
             else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified dynamic PDF form";
             else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                 myStatus = "No changes were made to the certified PDF document";
             else if (sigStatus == SignatureStatus.DocSigWithChanges)
                 myStatus = "There were changes to a signed PDF document";
            else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                 myStatus = "There were changes made to the PDF document.";

             //Get the signature type
             SignatureType sigType = signInfo.getSignatureType();
             String myType = "";

             if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                    myType="Certification";
             else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                    myType="Recipient";

             //Get the identity of the signer
             IdentityInformation signerId = signInfo.getSigner();
             String signerMsg = "";

            if (signerId.getStatus() == IdentityStatus.UNKNOWN)
                signerMsg = "Identity Unknown";
            else if (signerId.getStatus() == IdentityStatus.TRUSTED)
                signerMsg = "Identity Trusted";
            else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
                signerMsg = "Identity Not Trusted";

            //Get the Signature properties returned by the Signature service
            SignatureProperties sigProps = signInfo.getSignatureProps();
            String signerName =  sigProps.getSignerName();

           System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the input doc is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        pkiPref.setOCSPPreferences(getOCSPPref());
        pkiPref.setTSPPreferences(getTspPref());
        return pkiPref;
    }

    private static TSPPreferences getTspPref(){
     TSPPreferencesImpl tsp = new TSPPreferencesImpl();
     tsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return tsp;
    }
    private static OCSPPreferencesImpl getOCSPPref(){
     OCSPPreferencesImpl ocsp = new OCSPPreferencesImpl();
     ocsp.setRevocationCheck(RevocationCheckStyle.BestEffort);
     return ocsp;
    }
    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.BestEffort);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(true);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 複数の電子署名の検証 {#verifying-multiple-digital-signatures}

AEMを使用すると、PDFドキュメント内の電子署名を検証できます。 複数の署名者による署名が必要なビジネスプロセスで使用する場合、1 つの PDF ドキュメントに複数のデジタル署名を含めることができます。例えば、金融取引では、ローン担当者と管理者の両方の署名が必要です。 Signature service API を使用して、署名ドキュメント内のすべての署名をPDFできます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、Adobeは、電子署名を検証することをお勧めします。

**構文**：`verifyDocument(Document doc, RevocationCheckStyle revocationCheckStyle, VerificationTime verificationTime, ValidationPreferences prefStore, ResourceResolver resourceResolver)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>PDF を含む document オブジェクトです<br /> </td>
  </tr>
  <tr>
   <td><code>revocationCheckStyle</code></td>
   <td>検証中に発生した証明書の失効確認を管理するオプションです</td>
  </tr>
  <tr>
   <td><code>verificationTime</code></td>
   <td>署名が検証される時間です</td>
  </tr>
  <tr>
   <td><code>dssPrefs</code></td>
   <td>さまざまな検証の設定を管理する環境設定です。暗号化されたドキュメントの場合、ロック解除オプションを設定するには次を使用します。 <code>setUnlockOptions()</code></td>
  </tr>
  <tr>
   <td><code>resourceResolver</code></td>
   <td>Granite Trust Store に対するリソースリゾルバーです</td>
  </tr>
 </tbody>
</table>

以下のサンプルコードでは、 DocAssuranceService を使用して、既に暗号化されている署名ドキュメント内のPDFフィールドを検証します。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file from a
*source other than Adobe, then your use, modification, or distribution of it requires the prior
*written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;
import java.util.Iterator;
import java.util.List;

import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFDocumentVerificationInfo;
import com.adobe.fd.signatures.client.types.PDFSignatureType;
import com.adobe.fd.signatures.client.types.PDFSignatureVerificationInfo;
import com.adobe.fd.signatures.client.types.SignatureProperties;
import com.adobe.fd.signatures.client.types.SignatureStatus;
import com.adobe.fd.signatures.client.types.SignatureType;
import com.adobe.fd.signatures.client.types.VerificationTime;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferences;
import com.adobe.fd.signatures.pdf.inputs.ValidationPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 *
 * This class provides a sample code to use {@code DocAssuranceService} to carry out
 * verification of all the signature fields in an already Encrypted PDF Document
 *
 * Assume that a PDF document contains multiple digital signatures as a result of a business process that requires signatures from multiple
 * signers. For example, consider a financial transaction that requires both a loan officer's and a manager's signature. You can use the
 * Signature service Java API or web service API to verify all signatures within the PDF document. When verifying multiple digital signatures,
 * you can check the status and properties of each signature. Before you trust a digital signature, it is recommended that you verify it. It
 * is recommended that you are familiar with verifying a single digital signature.
 *
 * For unprotected document, you are not required to set UnlockOptions in ValidationPreferences
 * PreRequisites - The certificate chain upto the Root Certificate should be uploaded on CQ trust Store
 */

@Component
@Service(value=VerifyEncryptedPDFDoc.class)
public class VerifyEncryptedPDFDoc {

 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at JCR node
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void verifyEncryptedPDFDoc(String inputFile) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          //the resource resolver has to be corresponding to the user who has access to CQ Trust Store
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             RevocationCheckStyle revocationCheckStyle = RevocationCheckStyle.CheckIfAvailable;
             VerificationTime verificationTime = VerificationTime.CURRENT_TIME;
             ValidationPreferences dssPrefs = getValidationPreferences();

             //Verify the digital signature
             PDFDocumentVerificationInfo  docInfo = docAssuranceService.verifyDocument(
                 inDoc,
                 revocationCheckStyle,
                 verificationTime,
                 dssPrefs,
                 resourceResolver);

             //Get a list of all signatures that are in the PDF document
             List allSignatures = docInfo.getVerificationInfos();

           //Create an Iterator object and iterate through
           //the List object
           Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();

           while (iter.hasNext()) {
                  PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();

                  //Get the Signature Status
                     SignatureStatus sigStatus = signInfo.getStatus();
                     String myStatus="";

                   //Determine the status of the signature
                     if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                         myStatus = "The signatures in the dynamic PDF form are unknown";
                     else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                         myStatus = "The signatures in the PDF document are unknown";
                     else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a certified PDF form are valid";
                     else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                         myStatus = "The signatures in a signed dynamic PDF form are valid";
                     else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                         myStatus = "The signatures in a certified PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                         myStatus = "The signatures in a signed PDF document are valid";
                     else if (sigStatus == SignatureStatus.SignatureFormatError)
                         myStatus = "The format of a signature in a signed document is invalid";
                     else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                         myStatus = "No changes were made to the signed dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                         myStatus = "No changes were made to the signed PDF document";
                     else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified dynamic PDF form";
                     else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                         myStatus = "No changes were made to the certified PDF document";
                     else if (sigStatus == SignatureStatus.DocSigWithChanges)
                         myStatus = "There were changes to a signed PDF document";
                    else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                         myStatus = "There were changes made to the PDF document.";

                     //Get the signature type
                    SignatureType sigType = signInfo.getSignatureType();
                    String myType = "";

                    if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                        myType="Certification";
                    else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                        myType="Recipient";

                    //Get the Signature properties returned by the Signature service
                    SignatureProperties sigProps = signInfo.getSignatureProps();
                    String signerName =  sigProps.getSignerName();

                   System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
               }
           }
           catch (Exception ee)
           {
               ee.printStackTrace();
           }
         finally{
             /**
              * always close the PDFDocument object after your processing is done.
              */
             if(inDoc != null){
                 inDoc.close();
             }
             if(adminSession != null && adminSession.isLive()){
                 if(resourceResolver != null){
                     resourceResolver.close();
                 }
                 adminSession.logout();
             }
         }

 }

 /**
   * sets ValidationPreferences
   */
  private static ValidationPreferences getValidationPreferences(){

        ValidationPreferencesImpl prefs = new ValidationPreferencesImpl();
        prefs.setPKIPreferences(getPKIPreferences());

        //set the unlock options for processing an encrypted pdf document, do not set if the document is unprotected
        prefs.setUnlockOptions(getUnlockOptions());
        return prefs;

    }

  /**
   * sets PKIPreferences
   */
    private static PKIPreferences getPKIPreferences(){
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    /**
     * sets CRL Preferences
     */
    private static CRLPreferences getCRLPreferences(){

        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    /**
     *
     * sets PathValidationPreferences
     */
    private static PathValidationPreferences getPathValidationPreferences(){
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private static UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }

}
```

### 電子署名の削除 {#removing-digital-signatures}

以前の電子署名を削除した後でのみ、署名フィールドに新しい電子署名を適用できます。 電子署名を上書きすることはできません。 既に署名が含まれている署名フィールドに電子署名を適用しようとすると、例外が発生します。

**構文**：`clearSignatureField(Document inDoc, String signatureFieldName, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>PDF を含む document オブジェクトです<br /> </td>
  </tr>
  <tr>
   <td><code>signatureFieldName</code></td>
   <td>署名フィールドの名前です<br /> </td>
  </tr>
  <tr>
   <td><code>unlockOptions</code><br /> </td>
   <td>暗号化されたファイルのロックを解除するために必要なパラメーターが含まれます。ファイルが暗号化されている場合にのみ必要です<br /> </td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、署名フィールドから電子署名を削除することができます。

```java
/*************************************************************************
 *
  *
-------------------------------------------------------------
*ADOBE SYSTEMS INCORPORATED
*Copyright 2014 Adobe Systems Incorporated
*All Rights Reserved.

*NOTICE:  Adobe permits you to use, modify, and distribute this file in accordance with the
*terms of the Adobe license agreement accompanying it.  If you have received this file
*from a source other than Adobe, then your use, modification, or distribution of it requires
*the prior written permission of Adobe.
-------------------------------------------------------------------------------------------------

 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.io.IOException;

import javax.jcr.RepositoryException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesOtherException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * Digital signatures must be removed from a signature field before a newer digital signature can be applied.
 * A digital signature cannot be overwritten.
 * If you attempt to apply a digital signature to a signature field that contains a signature, an exception occurs
 *
 *The following Java code example removes a digital signature from a signature field named SignatureField1.
 *The name of the PDF file that contain the signature field is LoanSigned.pdf
 */

@Component
@Service(value=ClearSignatureField.class)
public class ClearSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;
 /**
  *
  * @param inputFile - path to an encrypted pdf document stored at disk
  * @param outFile - path where the output file has to be saved
  * @throws Exception
  */
 public void clearSignatureField(String inputFile, String outFile) throws Exception{

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

        //Specify the name of the signature field
        String fieldName = "SignatureField1";

        //Clear the signature field
        //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        Document outPDF = docAssuranceService.clearSignatureField(inDoc,fieldName,null);

        //save the outPDF
        outPDF.copyToFile(new File(outFile));
 }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### 認証署名フィールドを取得しています {#getting-certifying-signature-field}

署名または認証する署名ドキュメント内のすべてのPDFフィールドの名前を取得できます。 PDFドキュメント内の署名フィールド名が不明な場合や、名前を検証する場合は、プログラムを使用して名前を取得できます。 Signature サービスは、`form1[0].grantApplication[0].page1[0].SignatureField1[0]` のような署名フィールドの完全修飾名を返します。

**構文**：`getCertifyingSignatureField(Document inDoc, UnlockOptions unlockOptions)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>PDF を含む document オブジェクトです。<br /> </td>
  </tr>
  <tr>
   <td><code>UnlockOptions</code></td>
   <td>UnlockOptions は、暗号化されたファイルのロックを解除するために必要なパラメータを含みます。 これは、ファイルが暗号化されている場合にのみ必要です。</td>
  </tr>
 </tbody>
</table>

以下の Java コードの例では、ドキュメントの認証に使用された署名フィールドを取得します。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the ignature field that was used to certify the document.
 */

@Component
@Service(value=GetCertifyingSignatureField.class)
public class GetCertifyingSignatureField {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getCertifyingSignatureField(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        PDFSignatureField pdfSignature = docAssuranceService.getCertifyingSignatureField(inDoc,null);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### PDF暗号化タイプを取得中 {#getting-pdf-encryption-type}

署名または認証する署名ドキュメント内のすべてのPDFフィールドの名前を取得できます。 PDFドキュメント内の署名フィールド名が不明な場合や、名前を検証する場合は、プログラムを使用して名前を取得できます。 Signature サービスは、`asform1[0].grantApplication[0].page1[0].SignatureField1[0]` のような署名フィールドの完全修飾名を返します。

**構文**：`void getPDFEncryption(Document inDoc)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>入力として指定されたドキュメントです。 暗号化する場合としない場合があります。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードの例では、署名ドキュメント内の指定された署名フィールドの署名情報をPDFします。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.File;
import java.util.Iterator;
import java.util.List;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.signatures.client.types.PDFSignatureField;
import com.adobe.fd.signatures.client.types.exceptions.DuplicateSignatureFieldException;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.client.types.exceptions.PDFOperationException;
import com.adobe.fd.signatures.client.types.exceptions.PermissionsException;
import com.adobe.fd.signatures.client.types.exceptions.SignaturesBaseException;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.encryption.client.EncryptionTypeResult;

/**
 * You can retrieve the names of all signature fields that are in a PDF document that you want to sign or certify.
 * If you are unsure of the signature field names that are in a PDF document or you want to verify the names, you can
 * programmatically retrieve them. The Signature service returns the fully qualified name of the signature field, such as
 * form1[0].grantApplication[0].page1[0].SignatureField1[0].
 *
 * The following Java code example retrieves the Signature Info for the given signature field in a PDF document.
 */

@Component
@Service(value=GetPDFEncryption.class)
public class GetPDFEncryption {

 @Reference
 private DocAssuranceService docAssuranceService;

 /**
  *
  * @param inputFile - path to the pdf document stored at disk
  * @throws SignaturesBaseException
  * @throws DuplicateSignatureFieldException
  * @throws PermissionsException
  * @throws PDFOperationException
  * @throws InvalidArgumentException
  *
  */
 public void getPDFEncryption(String inputFile) throws Exception {

  File inFile = new File(inputFile);
  Document inDoc = new Document(inFile);

  //Retrieve signature data for a given signature field.
  //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
        EncryptionTypeResult encryptionTypeResult = docAssuranceService.getPDFEncryption(inDoc);

   }

  /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
}
```

### PDF のパスワード暗号化の削除 {#removing-password-encryption-from-pdf}

PDF ドキュメントからパスワードベースの暗号化を削除すると、ユーザーはパスワードを指定することなく、Adobe Reader または Acrobat で PDF ドキュメントを開くことができるようになります。パスワードベースの暗号化を PDF ドキュメントから削除すると、そのドキュメントは保護されなくなります。

**構文**：`Document removePDFPasswordSecurity (Document inDoc,String password)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>入力として指定されたドキュメント。 パスワードで保護する必要があります。<br /> </td>
  </tr>
  <tr>
   <td><code>password</code><br /> </td>
   <td>ドキュメントからセキュリティを削除するために使用するドキュメントを開くか、権限パスワードを指定します。<br /> </td>
  </tr>
 </tbody>
</table>

次のコードのサンプルを使用すると、パスワードベースの暗号化をPDFドキュメントから削除できます。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;
    import java.io.FileNotFoundException;
    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.jcr.api.SlingRepository;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes password-based encryption from a PDF document.
    * The master password value used to remove password-based encryption is PermissionPassword
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePasswordEncryption.class)
    public class RemovePasswordEncryption {

    // Create reference for DocAssuranceService
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    /**
    * The below sample code demonstrates removing password encryption from a PDF using AEM EncryptionService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_out.pdf"
    * @throws Exception
    */
    public void removePasswordEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

        try{

        String password = "PermissionPassword"; //master password with which the pdf was encrypted
                    //in case if the pdf is encrypted only with user password, specify the
                    //user password
        //Remove password-based encryption from the PDF document
        outDoc = docAssuranceService.removePDFPasswordSecurity(inDoc,password);

        }finally{
                    /**
                    * always close the PDFDocument object after your processing is done.
                    */
                    if(inDoc != null){
                        inDoc.close();
                    }

            }

            outDoc.copyToFile(outFile);

    }

    }
```

### 証明書の暗号化の削除 {#removing-certificate-encryption}

証明書ベースの暗号化をPDFドキュメントから削除して、ユーザーがAdobe ReaderまたはAcrobatでPDFドキュメントを開けるようにできます。 証明書で暗号化されたPDFドキュメントから暗号化を削除するには、秘密鍵を参照します。 暗号化を削除すると、そのPDFは保護されなくなります。

**構文**：`removePDFCertificateSecurity(Document inDoc, String alias, ResourceResolver resourceResolver)`

**入力パラメーター**

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>inDoc</code><br /> </td>
   <td>証明書で暗号化された PDF ドキュメントを表す document オブジェクトです。<br /> </td>
  </tr>
  <tr>
   <td><code>alias</code><br /> </td>
   <td>PDF ドキュメントから証明書ベースの暗号化を削除するために使用される、Granite Trust Store 内の鍵に対応するエイリアスです。<br /> </td>
  </tr>
  <tr>
   <td><code>ResourceResolver</code></td>
   <td>ResourceResolver ：特定のユーザーのキーストアにアクセスして秘密鍵証明書を取得します。</td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用すると、証明書ベースの暗号化をPDFドキュメントから削除できます。

```java
    package com.adobe.docassurance.samples;

    import java.io.File;

    import javax.jcr.Session;

    import org.apache.felix.scr.annotations.Component;
    import org.apache.felix.scr.annotations.Reference;
    import org.apache.felix.scr.annotations.Service;
    import org.apache.sling.api.resource.ResourceResolver;
    import org.apache.sling.jcr.api.SlingRepository;
    import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

    import com.adobe.aemfd.docmanager.Document;
    import com.adobe.fd.docassurance.client.api.DocAssuranceService;

    /**
    * The following Java code example removes certificate-based encryption from a PDF document
    *
    */
    @Component(enabled=true,immediate=true)
    @Service(value=RemovePKIEncryption.class)
    public class RemovePKIEncryption {

    // Create reference for docAssuranceServiceInterface
    @Reference
    private DocAssuranceService docAssuranceService;

    @Reference
        private SlingRepository slingRepository;

    @Reference
        private JcrResourceResolverFactory jcrResourceResolverFactory ;

    /**
    * The below sample code demonstrates encrypting PDF with Password using AEM docAssuranceService.
    *
    * @param inFilePath  path of the input PDF File
    * Path Example for Files stored at hardDisk = "C:/temp/test.pdf"
    *
    * @param outFilePath path where the output PDF File needs to be saved
    * Path Example for Files stored at hardDisk = "C:/temp/test_Encrypted.pdf"
    *
    * @throws Exception
    */
    public void removePKIEncryption(String inputFile, String outputFile) throws Exception {

    File inFile = new File(inputFile);
    Document inDoc = new Document(inFile);

    File outFile = new File(outputFile);
    Document outDoc = null;

            Session adminSession = null;
            ResourceResolver resourceResolver = null;
            try{
        adminSession = slingRepository.loginAdministrative(null);
        resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

        //Remove certificate-based encryption from the PDF document
        /**
        * Here the alias("encryption") of the private credential stored in the keystore of the
        * user has been provided with the user's resource resolver
        */
        outDoc = docAssuranceService.removePDFCertificateSecurity(inDoc, "encryption",resourceResolver);

            }catch(Exception e){

            // TODO Auto-generated catch block
            }finally{
                /**
                * always close the PDFDocument object after your processing is done.
                */
                if(inDoc != null){
                    inDoc.close();
                }
                if(adminSession != null && adminSession.isLive()){
                    if(resourceResolver != null){
                        resourceResolver.close();
                    }
                    adminSession.logout();
                }
            }

            outDoc.copyToFile(outFile);
    }

    }
```

## Output サービス {#output-service}

Output サービスは、XDP ファイルをレンダリングする APIを.pdf、.pcl、.zpl、.ps 形式で提供します。 このサービスは、以下の API をサポートしています。

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p)：**&#x200B;フォームデザインと、ネットワーク、ローカルファイルシステム、または HTTP 上の場所にリテラル値で保存されたデータをマージして PDF ドキュメントを生成します。

* **[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p)：**&#x200B;フォームデザインとアプリケーションに保存されたデータをマージして PDF ドキュメントを生成します。
* **[generatePDFOutputBatch](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutputbatch-p)：**&#x200B;フォームデザインとデータをマージして PDF ドキュメントを生成します。オプションで、レコードごとのメタデータファイルを生成したり、出力を PDF ファイルに保存したりできます。
* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p)：**&#x200B;フォームデザインと、ネットワーク、ローカルファイルシステム、または HTTP 上の場所にリテラル値で保存されたデータをマージして、PCL、PostScript、および ZPL 出力を生成します。

* **[generatePrintedOutput](/help/forms/using/aem-document-services-programmatically.md#p-generateprintedoutput-p)：**&#x200B;フォームデザインと、アプリケーションに保存されたデータをマージして PCL、PostScript、および ZPL 出力を生成します。

### generatePDFOutput {#generatepdfoutput}

generatePDFOutput API は、フォームデザインとPDFを結合してデータドキュメントを生成します。 オプションで、レコードごとのメタデータファイルを生成したり、出力を PDF ファイルに保存したりできます。フォームデザイン、またはネットワーク、ローカルファイルシステム、HTTP の場所にリテラル値で保存されているデータの場合は、generatePDFOutput API を使用します。フォームデザインと XML データがアプリケーションに保存されている場合は、[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API を使用します。

**構文**：`Document generatePDFOutput(String uriOrFileName, Document data, PDFOutputOptions options);`

#### 入力パラメーター {#input-parameters}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>uriOrFileName</td>
   <td>入力ファイルのパスと名前を指定します。 ファイルのタイプは、PDFまたは XDP です。 ファイル名のみを指定した場合、ファイルは options で指定された contentRoot に対して読み込まれます。</td>
  </tr>
  <tr>
   <td>data</td>
   <td>PDF ドキュメントにマージされるデータを含む XML ファイルです。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>contentRoot、locale、AcrobatVersion、linearizedPDF、taggedPDF の各変数の値を指定します。 options パラメーターは、PDFOutputOptions タイプのオブジェクトを受け付けます。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、フォームデザインと XML ファイルにPDFされたデータをマージして、保存ドキュメントが生成されます。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput(String contentRoot,File inputXML,String templateStr,String acrobatVersion,String tagged,String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

    try {

            PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);         if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

            {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {

                option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

            } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {             option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

            }

            if (tagged.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if (linearized.equalsIgnoreCase("true") ) {

                option.setTaggedPDF(true );

            }

            if(locale!=null)

            {

                option.setLocale(locale);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePDFOutput(templateStr,new Document(in),option);         File toSave = new File(outputFolder+"Output.pdf");

            doc.copyToFile(toSave);

            return toSave;

        } catch (OutputServiceException e) {

            e.printStackTrace();

        }catch (FileNotFoundException e) {

            e.printStackTrace();

        } catch (IOException e) {

            e.printStackTrace();

        }finally{

                    doc.dispose();

        }

        return null;

    }
```

### generatePDFOutput {#generatepdfoutput-1}

generatePDFOutput API は、フォームデザインとPDFを結合してデータドキュメントを生成します。 オプションで、レコードごとのメタデータファイルを生成したり、出力を PDF ファイルに保存したりできます。フォームデザインまたはアプリケーションに保存されているデータの場合は、generatePrintedOutput API を使用します。フォームデザインと XML データが、ネットワーク上の場所、ローカル、または HTTP 上の場所にリテラル値で保存されている場合は、[generatePDFOutput](/help/forms/using/aem-document-services-programmatically.md#p-generatepdfoutput-p) API を使用します。

**構文**：`Document generatePDFOutput(Document inputdocument, Document data, PDFOutputOptions options)`

#### 入力パラメーター {#input-parameter}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>入力ファイルのパスと名前を指定します。 ファイルのタイプは、PDFまたは XDP です。 ファイル名のみを指定した場合、ファイルは options で指定された contentRoot に対して読み込まれます。 <br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>PDF ドキュメントにマージされるデータを含む XML ファイルです。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>contentRoot、locale、AcrobatVersion、linearizedPDF、taggedPDF の各変数の値を指定します。 options パラメーターは、PDFOutputOptions 型のオブジェクトを受け付けます。</td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、フォームデザインと XML ファイルにPDFされたデータをマージして、保存ドキュメントが生成されます。

```java
    @Reference private OutputService outputService;

    private File generatePDFOutput2(String contentRoot, File inputXML, File templateStr, String acrobatVersion, String tagged, String linearized, String locale) {

    String outputFolder="C:/Output";

    Document doc=null;

        try {

                PDFOutputOptions option = new PDFOutputOptions();             option.setContentRoot(contentRoot);
                if(locale!=null)

                {

                    option.setLocale(locale);

                }

                if(acrobatVersion.equalsIgnoreCase("Acrobat_10"))

                {

                    option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_10_1")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_10_1);

                } else if(acrobatVersion.equalsIgnoreCase("Acrobat_11")) {                 option.setAcrobatVersion(com.adobe.fd.output.api.AcrobatVersion.Acrobat_11);

                }

                if (tagged.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                if (linearized.equalsIgnoreCase("true") ) {

                    option.setTaggedPDF(true );

                }

                InputStream inputXMLStream = new FileInputStream(inputXML);

                InputStream templateStream = new FileInputStream(templateStr);;

                doc = outputService.generatePDFOutput(new Document(templateStream),new             Document(inputXMLStream),option);

                        File toSave = new File(outputFolder,"Output.pdf");

                        doc.copyToFile(toSave);

                        return toSave;

                    } catch (OutputServiceException e) {

                            e.printStackTrace();

                }catch (FileNotFoundException e) {

                            e.printStackTrace();

                } catch (IOException e) {

                            e.printStackTrace();

                }finally{

                                doc.dispose();

                }

                    return null;

    }
```

### generatePDFOutputBatch {#generatepdfoutputbatch}

フォームデザインをデータとマージして、PDFドキュメントを作成します。 オプションで、レコードごとのメタデータファイルを生成したり、出力を PDF ファイルに保存したりできます。generatePDFOutputBatch API は、フォームデザイン、またはネットワーク、ローカルファイルシステム、または HTTP 上の場所にリテラル値で保存されているデータに使用します。

**構文**：`BatchResult generatePDFOutputBatch(Map templates, Map data, PDFOutputOptions options, BatchOptions batchOptions);`

#### 入力パラメーター {#input-parameters-1}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>templates<br /> </td>
   <td>キーのマップとテンプレートのファイル名を指定します。<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>キーとデータドキュメントのマップを指定します。 キーが Null でない場合、データドキュメントは templates マップで指定されたキーに対応するテンプレートでレンダリングされます。 </td>
  </tr>
  <tr>
   <td>options</td>
   <td>contentRoot、locale、AcrobatVersion、linearizedPDF、taggedPDF の各変数の値を指定します。 options パラメーターは、PDFOutputOptions 型のオブジェクトを受け付けます。</td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>変数 <code>generateManyFiles</code> の値を指定します。generateManyFiles フラグを設定して、複数のファイルを生成します。 options パラメーターは、BatchOptions 型のオブジェクトを受け付けます。</td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用すると、フォームデザインと XML ファイルに格納されたPDFを結合して、データドキュメントを生成することができます。

```java
private ArrayList generatePDFBatch(String contentRoot,String multipleFiles) {

String outputFolder="C:/Output";

    try {

        PDFOutputOptions option = new PDFOutputOptions();         option.setContentRoot(contentRoot);

        Map templates = new LinkedHashMap();

        Map data = new LinkedHashMap();

        String template1 = "PurchaseOrder.xdp"; String template2 = "CardApp.xdp";         templates.put(template1.substring(0, template1.indexOf(".xdp")),template1);         templates.put(template1.substring(0, template2.indexOf(".xdp")),template2);

        File inputXML1 = new File("c:/InputFolder/PurchaseOrder.xml");

        File inputXML2 = new File("c:/InputFolder/CardApp.xml");

        InputStream in1 = new FileInputStream(inputXML1);

        InputStream in2 = new FileInputStream(inputXML2);

        data.put(template1.substring(0, template1.indexOf(".xdp")),new         Document((in1))); data.put(template1.substring(0,         template1.indexOf(".xdp")),new Document((in2))); BatchOptions bo = new         BatchOptions(); BatchResult ret=null;         if(multipleFiles.equalsIgnoreCase("true"))

        {

            bo.setGenerateManyFiles(true);

            ret = outputService.generatePDFOutputBatch(templates, data, option, bo);

        } else {

            ret = outputService.generatePDFOutputBatch(templates, data, option, new             BatchOptions());

        }

        ArrayList outputs = new ArrayList();

        int counter=0;

        if(ret.getMetaDataDoc() !=null ){

        File toSave = new File(outputFolder+"Output.xml");

        ret.getMetaDataDoc().copyToFile(toSave);

        outputs.add(toSave);

        List<Document> list = ret.getGeneratedDocs();

        for(Document doc:list){

        File toSave = new File(outputFolder,"Output"+"_"+counter+".pdf");         doc.copyToFile(toSave);                    outputs.add(toSave);

        counter++;

        doc.dispose();

        }

        return outputs;

       } catch (OutputServiceException e) {

            e.printStackTrace();

       }catch (FileNotFoundException e) {

            e.printStackTrace();

       }catch (IOException e) {

            e.printStackTrace();

       }

       return null;

}
```

### generatePrintedOutput {#generateprintedoutput}

フォームデザインとデータファイルから PCL、PostScript、および ZPL 出力を生成します。 データファイルはフォームデザインとマージされ、印刷用にフォーマットされます。出力をプリンターに直接送信したり、ファイルとして保存したりできます。 フォームデザインまたはアプリケーションに保存されているデータの場合は、generatePrintedOutput API を使用します。

**構文**：`Document generatePrintedOutput(String uriOrFileName, Document data, PrintedOutputOptions);`

#### 入力パラメーター {#input-parameters-2}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>uriOrFileName<br /> </td>
   <td>入力ファイルのパスと名前を指定します。 ファイル名のみを指定した場合、ファイルは options で指定された contentRoot に対して読み込まれます。 ファイルのタイプは、PDFまたは XDP です。<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>PDF ドキュメントにマージされるデータを含む XML ファイルです。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>contentRoot、locale、AcrobatVersion、linearizedPDF、taggedPDF の各変数の値を指定します。 この options パラメーターは、 PrintedOutputOptions タイプのオブジェクトを受け付けます。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、フォームデザインとデータから、PCL、PostScript、および ZPL 出力を生成できます。出力タイプは、`printConfig` パラメーターに渡された値によって異なります。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput(String contentRoot,File inputXML,String templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

    try {

            PrintedOutputOptions options = new PrintedOutputOptions();                           options.setContentRoot(contentRoot);

            if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {

                            options.setPrintConfig(PrintConfig.HP_PCL_5e);

                     }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

            }

            InputStream in = new FileInputStream(inputXML);

            doc = outputService.generatePrintedOutput(templateStr,new             Document(in),options);

            in.close();

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return  toSave;

        } catch (OutputServiceException e) {

             e.printStackTrace();

        }catch (FileNotFoundException e) {

             e.printStackTrace();

        }catch (IOException e) {

             e.printStackTrace();

        }finally{

             doc.dispose();

        }

        return null;

}
```

### generatePrintedOutput {#generateprintedoutput-1}

指定されたフォームデザインとデータファイルに対して、PCL、PostScript、および ZPL 出力を生成します。 データファイルはフォームデザインとマージされ、印刷用にフォーマットされます。出力は、プリンターに直接送信することも、ファイルとして保存することもできます。 フォームデザインまたはアプリケーションに保存されたデータに対しては、 generatePrintedOutput API を使用します。

**構文**：`Document generatePrintedOutput(Document inputdocument, Document data, PrintedOutputOptions);`

#### 入力パラメーター {#input-parameters-3}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>Inputdocument<br /> </td>
   <td>入力ファイルのパスと名前を指定します。 ファイル名のみを指定した場合、ファイルは options で指定された contentRoot に対して読み込まれます。 XDP のファイル形式に対応しています。 </td>
  </tr>
  <tr>
   <td>data</td>
   <td>PDF ドキュメントにマージされるデータを含む XML ファイルです。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>このオブジェクトは、contentRoot、locale、printConfig、copies、および paginationOverride の値を設定するために使用されます。 この options パラメーターは、 PrintedOutputOptions タイプのオブジェクトを受け付けます。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、フォームデザインとデータから、PCL、PostScript、および ZPL 出力を生成できます。出力タイプは、`printConfig` パラメーターに渡された値によって異なります。

```java
@Reference private OutputService outputService;

private File generatePrintedOutput2(File  inputXML,File templateStr,String printConfig) {

String outputFolder="C:/Output";

Document doc=null;

       try {

            PrintedOutputOptions options = new PrintedOutputOptions();             if(printConfig.equalsIgnoreCase("ps"))

            {

                options.setPrintConfig(PrintConfig.PS_PLAIN);

            }else if(printConfig.equalsIgnoreCase("pcl")) {                                   options.setPrintConfig(PrintConfig.HP_PCL_5e);

            }else if(printConfig.equalsIgnoreCase("zpl")) {                                                                       options.setPrintConfig(PrintConfig.ZPL300);

                             }

            InputStream inputXMlStream = new FileInputStream(inputXML);

            InputStream templateStream = new FileInputStream(templateStr); doc =             outputService.generatePrintedOutput(new Document(templateStream),new             Document(inputXMlStream),options);

            File toSave = new File(outputFolder,"Output"+"."+printConfig);             doc.copyToFile(toSave);

            return toSave;

            } catch (OutputServiceException e) {

                e.printStackTrace();

            }catch (FileNotFoundException e) {

                e.printStackTrace();

            } catch (IOException e) {

                e.printStackTrace();

            }finally{

                doc.dispose();

            }

            return null;

}
```

### generatePrintedOutputBatch {#generateprintedoutputbatch}

フォームデザインとデータをマージして、PS 形式、PCL 形式、ZPL 形式のドキュメントを生成します。オプションで、レコードごとのメタデータファイルを生成したり、出力を PDF ファイルに保存したりできます。generatePrintedOutputBatch API は、ネットワーク上の場所、ローカルファイルシステム、または HTTP 上の場所にリテラル値で保存されているフォームデザインまたはデータに使用します。

**構文`:`** `BatchResult generatePrintedOutputBatch(Map templates, Map data, PrintedOutputOptions options, BatchOptions batchOptions);`

#### 入力パラメーター {#input-parameters-4}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>テンプレート<br /> </td>
   <td>キーのマップとテンプレートのファイル名を指定します。<br /> </td>
  </tr>
  <tr>
   <td>data</td>
   <td>キーとデータドキュメントのマップを指定します。 キーが null でない場合、データドキュメントはテンプレート Map で対応するキーのテンプレートと共にレンダリングされます。<br /> </td>
  </tr>
  <tr>
   <td>options</td>
   <td>PrintedOutputOptions 型のオブジェクトを指定します。 このオブジェクトは、contentRoot、locale、printConfig、copies、paginationOverride の値を設定するために使用されます。<br /> </td>
  </tr>
  <tr>
   <td>batchOptions</td>
   <td>変数 generateManyFiles の値を指定します。 generateManyFiles フラグを設定して、複数のファイルを生成します。 options パラメーターは、BatchOptions 型のオブジェクトを受け付けます。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、複数のフォームデザインテンプレートとデータファイルから、PCL、PostScript、および ZPL の出力をバッチで生成できます。 出力タイプは、`printConfig` パラメーターに渡された値によって異なります。

```java
@Reference private OutputService outputService;

private ArrayList generatePrintedOutputBatch(String contentRoot,String multipleFiles,String printConfig) {

String outputFolder="C:/Output";

        try {

                PrintedOutputOptions option = new PrintedOutputOptions();                 option.setContentRoot(contentRoot);

                Map templates = new LinkedHashMap();

                Map data = new LinkedHashMap();

                String template1 = "PurchaseOrder.xdp";

                String template2 = "CardApp.xdp";

                templates.put(template1.substring(0,                 template1.indexOf(".xdp")),template1);                 templates.put(template1.substring(0,                 template2.indexOf(".xdp")),template2);

                File inputXML1 = new                                   File("c:/InputFolder/PurchaseOrder.xml");

                File inputXML2 = new File("c:/InputFolder/CardApp.xml");

                InputStream in1 = new FileInputStream(inputXML1);

                InputStream in2 = new FileInputStream(inputXML2);                  data.put(template1.substring(0,                     template1.indexOf(".xdp")),new Document((in1)));

                 data.put(template2.substring(0,                     template2.indexOf(".xdp")),new Document((in2)));

                 if(printConfig.equalsIgnoreCase("ps"))

                 {

                    option.setPrintConfig(PrintConfig.PS_PLAIN);

                 } else if(printConfig.equalsIgnoreCase("pcl"))

                 {

                    option.setPrintConfig(PrintConfig.HP_PCL_5e);

                 } else if(printConfig.equalsIgnoreCase("zpl")){

                                         option.setPrintConfig(PrintConfig.ZPL300);

                 }

                 option.setContentRoot(contentRoot);

                 BatchOptions bo = new BatchOptions();

                 BatchResult ret =                             outputService.generatePrintedOutputBatch(temp                                    lates, data, option, new                                                     BatchOptions());

                 ArrayList outputs = new ArrayList();

                 int counter=0;

                 if(ret.getMetaDataDoc() !=null ){

                 File toSave = new File(outputFolder,"Output"+".xml");                    ret.getMetaDataDoc().copyToFile(toSave);

                 outputs.add(toSave);

                 List<Document> list = ret.getGeneratedDocs();

                 for(Document doc:list){

                 File toSave = new                                                               File(outputFolder,"Output"+"_"+counter+".                                        "+printConfig);                                    doc.copyToFile(toSave);

                 outputs.add(toSave);

                 counter++;

                 doc.dispose();

                 }

                 return outputs;

          }

            catch (OutputServiceException e) {

                e.printStackTrace();

          }catch (FileNotFoundException e) {

                e.printStackTrace();

          } catch (IOException e) {

                e.printStackTrace();

          }

            return null;

  }
```

## Forms サービス {#forms-service}

Formsサービスは、インタラクティブなPDFフォームとの間でデータの読み込みと書き出しをおこなう API を提供します。 インタラクティブPDFフォームは、PDFから情報を表示および収集するために使用される 1 つ以上のフィールドを含むユーザードキュメントです。 このサービスは、以下の API をサポートしています。

* **[exportData](/help/forms/using/aem-document-services-programmatically.md#p-exportdata-p)：** PDF フォームからデータをエクスポートします。
* **[importData](/help/forms/using/aem-document-services-programmatically.md#p-importdata-p)：**&#x200B;インタラクティブ PDF フォームにデータをインポートします。

### exportData {#exportdata}

XML および XDP 形式でインタラクティブPDFフォームからフォームデータを書き出します。

**構文**：`Document exportData(Document xdpOrPdf, DataFormat dataFormat)`

#### 入力パラメーター {#input-parameters-5}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>xdpOrPdf<br /> </td>
   <td>XDP ファイルまたは PDF ファイルを含む document オブジェクトを指定します。 </td>
  </tr>
  <tr>
   <td>dataFormat<br /> </td>
   <td>データを書き出す形式を指定します。 列挙型 (XDP、XmlData、Auto) の変数を受け入れます。<br /> </td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、XML および XDP 形式でインタラクティブPDFフォームからフォームデータを書き出すことができます。

#### サンプル {#sample}

```java
@Reference private FormsService formsService;
private File exportData(String  dataFormat, File  inDoc) {

String outputFolder="C:/Output";

InputStream in; Document doc=null;

try {

        in = new FileInputStream(inDoc);

        if(dataFormat.equalsIgnoreCase("xml"))

        {

          doc=formsService.exportData(new Document(in),                                       DataFormat.XmlData);

        }

        else if(dataFormat.equalsIgnoreCase("xdp")) {

        doc =formsService.exportData(new Document(in),                       DataFormat.XDP);

        }

        File toSave = new File(outputFolder,"Output"+"."+dataFormat);

        doc.copyToFile(toSave);

        return toSave;

    } catch (FormsServiceException e) {

       e.printStackTrace();

    }catch (FileNotFoundException e) {

       e.printStackTrace();

    } catch (IOException e) {

       e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

 }
```

### importData {#importdata}

インタラクティブ PDF フォームにフォームデータをインポートします。

**構文**：`Document importData(Document PDF, Document data)`

#### 入力パラメーター {#input-parameters-6}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>PDF<br /> </td>
   <td>PDF ファイルを含む document オブジェクトを指定します。 </td>
  </tr>
  <tr>
   <td>データ<br /> </td>
   <td>XML 形式のデータを含む XML ファイル。</td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、インタラクティブ PDF フォームにフォームデータをインポートできます。

#### サンプル {#sample-1}

```java
@Reference private FormsService formsService

private File importData(File inDoc, File inXML)

{

 String outputFolder="C:/Output";

 Document doc=null;

 try {

        InputStream in = new FileInputStream(inDoc);

        InputStream in2 = new FileInputStream(inXML);

        doc=formsService.importData(new Document(in), new Document(in2));

        File toSave = new File(outputFolder,"Output.pdf");

        doc.copyToFile(toSave);

    } catch (FormsServiceException e) {

         e.printStackTrace();

    }catch (FileNotFoundException e) {

         e.printStackTrace();

    } catch (IOException e) {

         e.printStackTrace();

    }finally{

        doc.dispose();

    }

    return null;

}
```

## PDF Generator サービス {#pdfgeneratorservice}

PDF Generator サービスは、ネイティブファイル形式を PDF に変換する API を提供します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

### GeneratePDFService {#generatepdfservice}

GeneratePDFService には、.doc、.docx、.ppt、.pptx、.xls、.xlsx、.odp、.odt、.ods、.swf（非推奨）、.jpg、.bmp、.tif、.png、.html など、様々なファイル形式をPDFに変換する API が用意されています。 また、様々なファイル形式にPDFを書き出し、PDFを最適化する API も提供します。 このサービスは、次の API をサポートしています。

* **createPDF**：サポートされているファイルタイプをPDFドキュメントに変換します。 Microsoft Word、Microsoft PowerPoint、Microsoft Excel、Microsoft Project などのファイル形式をサポートしています。 これらのアプリケーションに加えて、サードパーティ製の汎用的な種類の PDF 生成アプリケーションも API にプラグインすることができます。
* **exportPDF**：サポートされるファイルPDFに変換ドキュメントを変換します。 メソッドは、PDFを入力として受け入れ、PDFのコンテンツを指定したファイルタイプ形式で書き出します。 PDF ドキュメントは、次の形式でエクスポートすることができます。Encapsulated PostScript（eps）、HTML 3.2（htm、html）、CSS 1.0 を使用した HTML 4.01（htm、html）、JPEG（jpg、jpeg、jpe）、JPEG2000（jpf、jpx、jp2、j2k、j2c、jpc）、Microsoft Word 文書（doc、 docx） Microsoft Excel ブック（xlsx）、Microsoft PowerPoint プレゼンテーション（pptx）、PNG（png）、PostScript（ps）、リッチテキスト形式（rtf）、テキスト（Accessible）（txt）、テキスト（Plain）（txt）、TIFF（tif、tiff）、XML 1.0（xml）、PDF/A-1a（sRGB）、PDF/A-1b、PDF/A-2a（sRGB）、PDF/A-2b（sRGB）、PDF/A-3a（sRGB）、PDF/A-3b（sRGB）。PDF の出力用として[カスタムの Preflight プロファイル](https://helpx.adobe.com/jp/acrobat/using/overview-pdf-portfolios.html)を指定することもできます。

* **optimizePDF**:PDFドキュメントを最適化し、PDFドキュメントを別のタイプに変換します。 メソッドは、入力としてPDFドキュメントを受け付けます。
* **htmlToPdf2**：HTML ページを PDF ドキュメントに変換します。入力としてHTMLページの URL を受け付けます。

>[!NOTE]
>
>AIX オペレーティングシステムで実行されているAEM Formsサーバーでは、HTMLtoPDF API は非推奨（廃止予定）となりました。

#### Microsoft Windows および Linux で使用可能なPDF GeneratorAPI {#pdf-generator-api-available-on-microsoft-windows-and-linux}

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><p><strong>Microsoft Windows </strong></p> </td>
   <td><strong>Linux </strong></td>
  </tr>
  <tr>
   <td>createPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
  <tr>
   <td>htmlToPDF</td>
   <td><strong>✓</strong></td>
   <td><strong>✓</strong></td>
  </tr>
   <td>optimizePDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>exportPDF</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
  <tr>
   <td>OCRPDF( 検索可能なPDF)</td>
   <td><strong>✓</strong></td>
   <td>✖</td>
  </tr>
 </tbody>
</table>

#### createPDF {#createpdf}

createPDF API は、サポートされているファイルタイプをPDFドキュメントに変換します。 Microsoft Word、Microsoft PowerPoint、Microsoft Excel、Microsoft Project など、様々なファイル形式をサポートしています。 これらのアプリケーションに加えて、サードパーティ製の汎用的な種類の PDF 生成アプリケーションも API にプラグインすることができます。

変換の場合は、一部のパラメーターのみが必須です。 入力ドキュメントは必須のパラメータです。 後で、セキュリティ権限、PDF出力設定およびメタデータ情報を出力PDFドキュメントに適用できます。

createPDF サービスは結果を java.util.Map で返します。 マップのキーは次のとおりです。

* ConvertedDoc：新しく作成されたPDF文書が含まれます。
* LogDoc：ログファイルが含まれます。

createPDF サービスは次の例外をスローします。

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**構文**：`Map createPDF(Document inputDoc, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws InvalidParameterException, ConversionException, FileFormatNotSupportedException;`

#### 入力パラメーター {#input-parameters-7}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>ドキュメントオブジェクトを指定します。 document オブジェクトには、入力ファイルが含まれています。 入力ドキュメントの上に com.adobe.aemfd.docmanager.Document オブジェクトを作成します。 必須のパラメーターです。</td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>入力ファイルの名前と拡張子。 必須のパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td>fileTypeSettings</td>
   <td>これはオプションのパラメーターです。</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>PDFされたドキュメントの変換出力。 次の設定のみを適用できます。</p>
    <ul>
     <li>High_Quality_Print<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>プレス品質<br /> </li>
     <li>Smallest_File_Size</li>
    </ul> <p>これはオプションのパラメーターです。<br /> </p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>変換後のドキュメントのセキュリティ設定です。 次の設定を適用できます。</p>
    <ul>
     <li>セキュリティなし</li>
     <li>パスワードセキュリティ<br /> </li>
     <li>証明書セキュリティ<br /> </li>
     <li>Adobeポリシーサーバー</li>
    </ul> <p>これはオプションのパラメーターです。</p> </td>
  </tr>
  <tr>
   <td>settingsDoc</td>
   <td>このファイルには、PDFドキュメントの生成時に適用される設定 (Web ビュー用のPDFドキュメントの最適化など ) と、PDFドキュメントの作成後に適用される設定（初期ビューやセキュリティなど）が含まれます。 これはオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>生成した PDF ドキュメントに適用されるメタ情報を含むファイルです。このパラメーターはオプションです。<br /> </td>
  </tr>
 </tbody>
</table>

次の Java コードは、サポートされているファイルタイプのドキュメントをPDFドキュメントに変換します。

```java
@Reference GeneratePDFService generatePdfService;
File createPDF(File inputFile, String inputFilename, String fileTypeSettings, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = generatePdfService.createPDF(inDoc, inputFilename, fileTypeSettings, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```

#### exportPDF {#exportpdf}

PDFドキュメントをサポートされるファイルタイプに変換します。 メソッドは、PDFを入力として受け入れ、PDFのコンテンツを指定したファイルタイプ形式で書き出します。

createPDF サービスは結果を java.util.Map で返します。 マップのキーは次のとおりです。

* ConvertedDoc：出力ドキュメントが含まれます。

createPDF サービスは次の例外をスローします。

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**構文：**

```java
Map exportPDF(Document inputDoc, String inputFileName, String formatType, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 入力パラメーター {#input-parameters-8}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>変換するドキュメントを指定します。 </td>
  </tr>
  <tr>
   <td>inputFileName<br /> </td>
   <td>ファイル名と拡張子。<br /> </td>
  </tr>
  <tr>
   <td>formatType</td>
   <td>exportPDF API の出力ファイル形式です。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>ファイルには、出力ドキュメントの生成時に適用される設定が含まれています。 一般に、XML ファイルです。</td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、PDF ドキュメントを特定のファイル形式に変換することができます。

```java
(tx == null)
OSGiUtils.getTransactionManager().begin();
String outputFolder="C:/Output"
Document convertedDoc = null;
Document inDoc = null;
Document settingsDoc = null;
try
{
 inDoc = new Document(inputFile);
 if(inputFileName == null || inputFileName.trim().equals("")) {
  throw new Exception("Input file name cannot be null");
 }
 if(inputFileExtension.lastIndexOf('.') == -1) {
  throw new Exception("Input file should have an extension");
 }
 if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
 settingsDoc = new Document(settingsFile);
 Map result = generatePdfService.exportPDF(inDoc, inputFileName, formatType, settingsDoc);
 convertedDoc = (Document)result.get("ConvertedDoc");
 OSGiUtils.getTransactionManager().commit();
 File outputFile = new File(outputFolder,"OutputFile");
 doc.copyToFile(outputFile);
 return outputFile;
}
catch (Exception e)
{
 if (OSGiUtils.getTransactionManager().getTransaction() != null)
 OSGiUtils.getTransactionManager().rollback();
 throw e;
}
finally {
 if (convertedDoc != null) {
  convertedDoc.dispose();
  convertedDoc = null;
 }
 if (inDoc != null) {
  inDoc.dispose();
  inDoc = null;
 }
 if (settingsDoc != null) {
  settingsDoc.dispose();
  settingsDoc = null;
 }
}
}
```

#### optimizePDF {#optimizepdf}

OptimizePDF API は、サイズを縮小してPDFファイルを最適化します。 この変換の結果、PDFファイルは元のバージョンよりも小さくなる可能性があります。 また、この操作では、PDF ドキュメントが最適化パラメーターで指定された PDF バージョンに変換されます。最適化されたPDFを含む OptimizePDFResult オブジェクトを返します。

createPDF サービスは次の例外をスローします。

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**構文：**

```java
OptimizePDFResult optimizePDF(Document inputDoc, String fileTypeSettings, Document settingsDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 入力パラメーター {#input-parameters-9}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>入力ドキュメントを指定します。 必須パラメーターです。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>これはオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>このファイルには、PDFドキュメントの生成時に適用される設定 (Web ビュー用のPDFドキュメントの最適化など ) と、PDFドキュメントの作成後に適用される設定（初期ビューやセキュリティなど）が含まれます。 これはオプションのパラメーターです。<br /> </td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、入力 PDF ファイルのサイズを小さくし、最適化することができます。

```java
@Reference GeneratePDFService generatePdfService;
File optimizePDF(File inputFile, String fileTypeSettings, File settingsFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  OptimizePDFResult result = generatePdfService.optimizePDF(inDoc, fileTypeSettings, settingsDoc);
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

#### htmlToPdf2 {#htmltopdf}

HTMLページを変換ドキュメントにPDFします。 入力としてHTMLページの URL を受け付けます。

htmlToPdf2 サービスは HtmlToPdfResult オブジェクトを返します。 result.getConvertedDocument() を使用して変換されたPDFを取得できます。

htmlToPdf2 サービスは次の例外をスローします。

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

**構文：**

```java
HtmlToPdfResult htmlToPdf2(String inputUrl, String fileTypeSettingsName, String securitySettingsName, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 入力パラメーター {#input-parameters-10}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>入力ドキュメントを指定します。 必須パラメーターです。</td>
  </tr>
  <tr>
   <td>fileTypeSettings<br /> </td>
   <td>これはオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>このファイルには、PDFドキュメントの生成時に適用される設定 (Web ビュー用のPDFドキュメントの最適化など ) と、PDFドキュメントの作成後に適用される設定（初期ビューやセキュリティなど）が含まれます。 これはオプションのパラメーターです。<br /> </td>
  </tr>
 </tbody>
</table>

以下の Java コードのサンプルを使用することで、HTML ページを PDF ドキュメントに変換することができます。

```java
Reference GeneratePDFService generatePdfService;
File htmlToPdf(String inputUrl, String fileTypeSettingsName, String securitySettingsName, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  HtmlToPdfResult result = generatePdfService.htmlToPdf2(inputURL, fileTypeSettingsName, securitySettingsName, settingsDoc, xmpDoc);;
  convertedDoc = result.getConvertedDocument();
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
 }
}
```

### DistillerService {#distillerservice}

Distillerサービスは、PostScript、Encapsulated PostScript(EPS) およびプリンターテキストファイル (PRN) をPDFファイルに変換します。 Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。サポートされるファイル形式は、.ps、.eps、.prn です。 このサービスは、次の API をサポートしています。

createPDF サービスは結果を java.util.Map で返します。 マップのキーは次のとおりです。

* ConvertedDoc ：新しく作成された変換ドキュメントがPDFされます。
* LogDoc ：ログファイルが含まれます。

createPDF サービスは次の例外をスローします。

* ConversionException
* InvalidParameterException
* FileFormatNotSupportedException

#### createPDF {#createpdf-1}

サポートされる形式をPDF文書に変換します。 このメソッドは、.ps、.eps、.prn 形式のファイルを入力として受け付けます。 出力 PDF ドキュメントには特定のセキュリティ権限、PDF 出力設定およびメタデータ情報を適用することができます。

**構文：**

```java
Map createPDF(Document inputDoc, String inputFileName, String pdfSettings, String securitySettings, Document settingsDoc, Document xmpDoc) throws ConversionException, InvalidParameterException, FileFormatNotSupportedException;
```

#### 入力パラメーター {#input-parameters-11}

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>inputDoc<br /> </td>
   <td>入力ドキュメントを指定します。 必須パラメーターです。</td>
  </tr>
  <tr>
   <td>inputFileName</td>
   <td>入力ファイルの完全な名前と、ファイルの拡張子を指定します。 必須パラメーターです。</td>
  </tr>
  <tr>
   <td>pdfSettings</td>
   <td><p>PDFされたドキュメントの変換出力設定。 次の設定のみを適用できます。</p>
    <ul>
     <li>High_Quality_Print<br /> </li>
     <li>PDFA1b_2005_RGB<br /> </li>
     <li>PDFA1b_2005_CMYK<br /> </li>
     <li>PDFX1a_2001<br /> </li>
     <li>PDFX3_2002<br /> </li>
     <li>プレス品質<br /> </li>
     <li>Smallest_File_Size</li>
    </ul> <p>これはオプションのパラメーターです。</p> </td>
  </tr>
  <tr>
   <td>securitySettings</td>
   <td><p>変換後のドキュメントのセキュリティ設定です。 次の設定を適用できます。</p>
    <ul>
     <li>セキュリティなし</li>
     <li>パスワードセキュリティ<br /> </li>
     <li>証明書セキュリティ<br /> </li>
     <li>Adobeポリシーサーバー</li>
    </ul> <p>これはオプションのパラメーターです。</p> </td>
  </tr>
  <tr>
   <td>settingsDoc </td>
   <td>このファイルには、PDFドキュメントの生成時に適用される設定 (Web ビュー用のPDFドキュメントの最適化など ) と、PDFドキュメントの作成後に適用される設定（初期ビューやセキュリティなど）が含まれます。 これはオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td>xmpDoc </td>
   <td>ファイルには、生成されたPDFドキュメントのメタデータ情報が含まれます。 これはオプションのパラメーターです。</td>
  </tr>
 </tbody>
</table>

次の Java コードのサンプルを使用すると、PostScript（PS）、Encapsulated PostScript（EPS）およびプリンタテキストファイル（PRN）の入力ファイルを PDF ファイルに変換できます。

```java
@Reference DistillerService distillerService;
File createPDF(File inputFile, String inputFilename, String pdfSettings, String securitySettings, File settingsFile, File xmpFile) throws Exception
{
 Transaction tx = OSGiUtils.getTransactionManager().getTransaction();
 // Begin transaction
 if (tx == null)
 OSGiUtils.getTransactionManager().begin();
 String outputFolder="C:/Output"
 Document convertedDoc = null;
 Document inDoc = null;
 Document settingsDoc = null;
 Document xmpDoc = null;
 try
 {
  inDoc = new Document(inputFile);
  if(inputFilename == null || inputFilename.trim().equals("")) {
   throw new Exception("Input file name cannot be null");
  }
  if(inputFileExtension.lastIndexOf('.') == -1) {
   throw new Exception("Input file should have an extension");
  }
  if(settingsFile != null && settingsFile.exists() && settingsFile.isFile())
  settingsDoc = new Document(settingsFile);
  if(xmpFile != null && xmpFile.exists() && xmpFile.isFile())
  xmpDoc = new Document(xmpFile);
  Map result = distillerService.createPDF(inDoc, inputFilename, pdfSettings, securitySettings, settingsDoc, xmpDoc);
  convertedDoc = (Document)result.get("ConvertedDoc");
  OSGiUtils.getTransactionManager().commit();
  File outputFile = new File(outputFolder,"Output.pdf");
  doc.copyToFile(outputFile);
  return outputFile;
 }
 catch (Exception e)
 {
  if (OSGiUtils.getTransactionManager().getTransaction() != null)
  OSGiUtils.getTransactionManager().rollback();
  throw e;
 }
 finally {
  if (convertedDoc != null) {
   convertedDoc.dispose();
   convertedDoc = null;
  }
  if (inDoc != null) {
   inDoc.dispose();
   inDoc = null;
  }
  if (settingsDoc != null) {
   settingsDoc.dispose();
   settingsDoc = null;
  }
  if (xmpDoc != null) {
   xmpDoc.dispose();
   xmpDoc = null;
  }
 }
}
```
