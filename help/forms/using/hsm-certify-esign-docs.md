---
title: ドキュメントのデジタル署名や証明に HSM を使用する
description: PDF ドキュメントの署名や認証に HSM サーバーまたは eToken デバイスを使用する
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
source-git-commit: 4a4a75018e960733908f40c631a24203290be55c
workflow-type: ht
source-wordcount: '655'
ht-degree: 100%

---

# ドキュメントのデジタル署名や証明に HSM を使用する {#use-hsm-to-digitally-sign-or-certify-documents}

ハードウェアセキュリティモジュール（HSM）および eToken は、デジタルキーを安全に管理、処理、保管するように設計された、改ざん耐性のあるセキュリティが強化された専用計算デバイスです。これらのデバイスは、コンピューターまたはネットワークサーバーに直接接続されます。

Adobe Experience Manager Forms は、HSM または eToken に保存された資格情報を使用して eSign を作成したり、ドキュメントにサーバーサイドのデジタル署名を適用したりできます。AEM Forms 上で HSM または eToken デバイスを使用するには：

1. [DocAssurance サービスを有効にします](#configuredocassurance)。
1. [AEM web コンソールから、HSM または eToken デバイスのエイリアスを作成します](#configuredeviceinaemconsole)。
1. [DocAssurance サービス API を使用して、デバイスに保存されたデジタルキーで文書の署名または証明を行います](#programatically)。

## AEM Forms で HSM または eToken デバイスを設定する前に {#configurehsmetoken}

* [AEM Forms アドオン](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)パッケージをインストールします。
* AEM サーバーと同じコンピューターに HSM または eToken クライアントソフトウェアをインストールして設定します。クライアントソフトウェアは、HSM および eToken デバイスと通信する必要があります。

## DocAssurance サービスを有効にする {#configuredocassurance}

デフォルトでは、DocAssurance サービスは無効になっています。このサービスを有効にするには、次の手順を実行します。

1. AEM Forms 環境のオーサーインスタンスを停止させます。

1. [AEM_root]\crx-quickstart\conf\sling.properties ファイルを開き、編集します。

   >[!NOTE]
   >
   >[AEM_root]\crx-quickstart\bin\start.bat ファイルを使用して AEM インスタンスを起動した場合は、[AEM_root]\crx-quickstart\sling.properties ファイルを開いて変更してください。

1. sling.properties ファイルに次のプロパティを追加（または書き換え）します。

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. sling.properties ファイルを保存して閉じます。
1. AEM インスタンスを再起動します。

<!--

## Set up certificates for Reader extensions {#set-up-certificates-for-reader-extensions}

Perform the following steps to setup certificates:

1. Log in to AEM Author instance as an administrator.

1. Click **Adobe Experience Manager** on Global Navigation Bar. Go to **Tools** &gt;  **Security** &gt;  **Users**.
1. Click the **name** field of the user account. The **Edit User Settings** page opens.
1. On the AEM Author instance, certificates reside in a KeyStore. If you have not created a KeyStore earlier, click **Create KeyStore** and set a new password for the KeyStore. If the server already contains a KeyStore, skip this step.

1. On the **Edit User Settings** page, click **Manage KeyStore**.

1. On KeyStore Management dialog, expand the **Add Private Key from Key Store file** option and provide an alias. The alias is used to perform the Reader Extensions operation.
1. To upload the certificate file, click **Select Key Store File** and upload a `.pfx` file.
1. Add the **Key Store Password**,**Private Key Password**, and **Private Key Alias** that is associated with the certificate to the respective fields. Click **Submit**.

   >[!NOTE]
   >
   >To determine the **Private Key Alias** of a certificate, you can use the Java keytool command: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >In the **Key Store Password** and **Private Key Password** fields, specify the password provided with the certificate file.

>[!NOTE]
>
>For AEM Forms on OSGi, to verify the signed PDF, the root certificate installed in the Trust Store.

>[!NOTE]
>
>On moving to production environment, replace your evaluation credentials with production credentials. Ensure that you delete your old Reader Extensions credentials, before updating an expired or evaluations credential.

-->


## デバイスエイリアスの作成 {#configuredeviceinaemconsole}

エイリアスには、HSM または eToken に必要なすべてのパラメーターが含まれます。eSign またはデジタル署名に必要な HSM や eToken の各資格情報に対してエイリアスを作成するには、以下の手順を実行します。

1. AEM コンソールを開きます。AEM コンソールのデフォルト URL は、https://&lt;host>:&lt;port>/system/console/configMgr です。
1. **HSM クレデンシャル設定サービス**&#x200B;を開き、次のフィールドに値を指定してください。

   * **Credential Alias**（クレデンシャルのエイリアス）：エイリアスを識別するための文字列を指定します。この値は、署名フィールドへの署名操作といった、Digital Signatures の一部の操作でプロパティとして使用されます。
   * **DLL Path**：サーバー上の HSM または eToken クライアントライブラリのパスを指定します。例えば、`C:\Program Files\LunaSA\cryptoki.dll` のようになります。クラスター環境では、クラスター内のすべてのサーバーが同じパスを使用する必要があります。
   * **HSM PIN**：デバイスキーへのアクセスに必要なパスワードを指定します。
   * **HSM Slot Id**：整数タイプのスロット識別子を指定します。スロット ID は、クライアントごとに設定されます。これは、署名または証明用の秘密鍵を含む HSM 上のスロットを識別するために使用されます。

   >[!NOTE]
   >
   >eToken を設定する際は、「HSM スロット ID」フィールドに数値を指定します。数値は、Signatures の操作を有効にするために必要です。

   * **Certificate SHA1**：使用する秘密鍵証明書の公開鍵（cer）ファイルの SHA1 値（拇印）を指定します。SHA1 値にスペースが使用されていないことを確認します。
   * **HSM デバイスタイプ**：HSM（Luna など）または eToken デバイスの発行元を選択します。

   「**保存**」をクリックします。ハードウェアセキュリティモジュールは、AEM Forms 用に設定されています。これにより、AEM Forms でハードウェアセキュリティモジュールを使用して、ドキュメントの署名や証明を行えるようになりました。

## DocAssurance サービス API を使用して、デバイスに保存されたデジタルキーでドキュメントを署名または証明 {#programatically}

次のサンプルコードでは、ドキュメントの署名や証明の際に、HSM または eToken を使用します。

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
import java.io.IOException;
import java.io.InputStream;

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
import com.adobe.fd.docassurance.client.api.SignatureOptions;
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
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
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
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
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
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
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

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

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
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
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
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

AEM 6.0 Form またはAEM 6.1 Forms からアップグレードし、以前のバージョンで DocAssurance サービスを使用していた場合は、次のようになります。

* HSM や eToken デバイスを使用せずに DocAssurance サービスを使用するには、既存のコードを引き続き使用します。
* HSM または eToken デバイスと共に DocAssurance サービスを使用するには、既存の CredentialContext オブジェクトコードを以下に示す API に置き換えます。

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

DocAssurance サービスの API とサンプルコードについて詳しくは、[AEM ドキュメントサービスをプログラムとして使用](/help/forms/using/aem-document-services-programmatically.md)を参照してください。
