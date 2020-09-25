---
title: ドキュメントのデジタル署名や証明に HSM を使用する
seo-title: 電子署名付きドキュメントの証明に HSM を使用する
description: 電子署名付きドキュメントの証明に、HSM または eToken デバイスを使用する
seo-description: 電子署名付きドキュメントの証明に、HSM または eToken デバイスを使用する
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 81%

---


# ドキュメントのデジタル署名や証明に HSM を使用する {#use-hsm-to-digitally-sign-or-certify-documents}

ハードウェアセキュリティモジュール（HSM）や eToken は、改ざん耐性を備え、セキュリティが強化された専用の計算デバイスです。これらは、デジタルキーを安全に管理、処理、そして保管できるように設計されています。これらのデバイスは、コンピュータやネットワークサーバーに直接保存されます。

Adobe Experience Manager Forms では、HSM や eToken に保存された資格情報を使用したり、ドキュメントにサーバーサイドのデジタル署名を適用したりすることができます。AEM フォーム上で HSM または eToken デバイスを使用するには：

1. DocAssurance サービスを有効にします。
1. Reader 拡張機能用の証明書を設定します。
1. AEM Web コンソールから、HSM または eToken デバイスのエイリアスを作成します。
1. DocAssurance サービスの API により、デバイスに保存されたデジタルキーと共に文書を証明または署名します。

## AEM Forms で HSM または eToken デバイスを設定する前に {#configurehsmetoken}

* [AEM Forms アドオン](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)パッケージをインストールします。
* AEM サーバーがインストールされているコンピュータに HSM または eToken クライアントソフトウェアをインストールし、セットアップします。クライアントソフトウェアは、HSM や etoken デバイスと通信する必要があります。
* （Microsoft Windows の場合のみ）JAVA_HOME_32 環境変数を設定し、32 ビット版の Java 8 Development Kit（JDK 8）のインストール先を参照します。ディレクトリのデフォルトパスは、C:\Program Files(x86)\Java\jdk&lt;version> です。
* トラストストアにルート証明書をインストールします（OSGi 上の AEM Forms のみ）これは、署名済み PDF の検証に必要です。

>[!NOTE]
>
>Microsoft Windows の場合、32 ビットの LunaSA または EToken クライアントのみに対応しています。

## DocAssurance サービスを有効にする {#configuredocassurance}

デフォルトでは、DocAssurance サービスは無効になっています。次の手順を実行して、サービスを有効にします。

1. AEM Forms 環境のオーサーインスタンスを停止させます。

1. Open the [AEM_root]\crx-quickstart\conf\sling.properties file for editing.

   >[!NOTE]
   >
   >If you have used the [AEM_root]\crx-quickstart\bin\start.bat file to start the AEM instance, then open the [AEM_root]\crx-quickstart\sling.properties file for editing.

1. sling.properties ファイルに次のプロパティを追加（または書き換え）します。

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. sling.properties ファイルを保存して閉じます。
1. AEM インスタンスを再起動します。

## Reader Extensions 用の証明書を設定します。{#set-up-certificates-for-reader-extensions}

次の手順を実行して証明書をセットアップします。

1. AEM オーサーインスタンスに管理者としてログインします。

1. グローバルナビゲーションバーで「**Adobe Experience Manager**」をクリックします。**ツール**／**セキュリティ**／**ユーザー**&#x200B;に移動します。
1. ユーザーアカウントの「**名前**」フィールドをクリックします。「**ユーザー設定を編集**」ページが開きます。
1. AEM オーサーインスタンスでは証明書がキーストアに存在します。キーストアをまだ作成していない場合は、「**キーストアを作成**」をクリックし、キーストアの新しいパスワードを設定します。サーバーに既にキーストアが含まれている場合は、この手順をスキップします。

1. **ユーザー設定を編集**&#x200B;ページで、「**キーストアを管理**」をクリックします。 

1. On KeyStore Management dialog, expand the **Add Private Key from Key Store file** option and provide an alias. エイリアスは Reader Extensions の操作を実行する際に使用されます。
1. To upload the certificate file, click **Select Key Store File** and upload a `.pfx` file.
1. **キーストアのパスワード**、**秘密鍵のパスワード**、および証明書に関連付けられている&#x200B;**秘密鍵エイリアス**&#x200B;を、各フィールドに追加します。「**送信**」をクリックします。

   >[!NOTE]
   >
   >To determine the P **rivate Key Alias** of a certificate, you can use the Java keytool command: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >「**キーストアのパスワード**」および「**秘密鍵のパスワード**」フィールドに、証明書ファイルとともに提供するパスワードを指定します。

>[!NOTE]
>
>OSGi 上の AEM Forms の場合は、署名済み PDF を検証するため、トラストストアにルート証明書がインストールされます。

>[!NOTE]
>
>実稼働環境に移行する際は、評価用の資格情報を実稼働用の資格情報に置き換えます。期限切れの資格情報または評価用の資格情報を更新する前に、古いReader拡張機能の資格情報を削除してください。

## デバイスエイリアスの作成 {#configuredeviceinaemconsole}

エイリアスには、HSM や eToken に必要なパラメータがすべて含まれます。eSign やデジタル署名に必要な HSM や eToken の各資格情報に対してエイリアスを作成するには、以下の手順を実行します。

1. AEM コンソールを開きます。AEMコンソールのデフォルトのURLは、https://&lt;host>:&lt;port>/system/console/configMgrです。
1. 「**HSM クレデンシャル設定サービス**」を開き、次のフィールドに値を入力します。

   * **Credential Alias**（クレデンシャルのエイリアス）：エイリアスを識別するための文字列を指定します。この値は、署名フィールドへの署名操作など、Digital Signaturesの一部の操作でプロパティとして使用されます。
   * **DLL Path**（DLL のパス）：サーバーの HSM クライアントライブラリの完全修飾パスを指定します。例えば、「c:\Program Files\LunaSA\cryptoki.dll」のように入力します。クラスター環境では、クラスター内のすべてのサーバーでこのパスが同じである必要があります。
   * **HSM Pin**:デバイスキーにアクセスするために必要なパスワードを指定します。
   * **HSM Slot Id**（HSM スロットの ID）：データタイプが integer のスロットに対して、識別子を指定します。スロット ID はクライアントごとに設定します。2 番目のマシンを別のパーティション（同じ HSM デバイスの HSMPART2 など）に登録すると、スロット 1 はこのクライアントの HSMPART2 パーティションに関連付けられます。

   >[!NOTE]
   >
   >HSM Slot Idフィールドには、eTokenの設定時に数値を指定します。 数値は、Signatures の操作を有効にするために必要です。

   * **Certificate SHA1**（証明書 SHA1）：使用する秘密鍵証明書について、公開鍵（.cer）ファイルの SHA1 値（拇印）を指定します。SHA1 値にスペースが使用されていないことを確認します。物理証明書を使用している場合は、必要ありません。
   * **HSM Device Type**:HSM（Lunaなど）またはeTokenデバイスの製造元を選択します。

   「**保存**」をクリックします。ハードウェアセキュリティモジュールは、AEM Forms 用に構成されています。これにより、ドキュメントの署名や証明を行う際に、AEM Forms 上でハードウェアセキュリティモジュールを使用できるようになります。

## DocAssurance サービス API を使用して、デバイスに保存されたデジタルキーで文書を署名または証明する {#programatically}

次のサンプルコードでは、ドキュメントの署名や証明の際に、HSM または eToken を使用しています。

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

AEM 6.0 Form または AEM 6.1 Form からアップグレードした場合で、かつ以前のバージョンで DocAssurance サービスを使用していた場合：

* HSM または eToken デバイスを使用せず DocAssurance サービスを利用するには、既存のコードを使用し続けてください。
* HSM または eToken デバイスと共に DocAssurance サービスを利用するには、既存の CredentialContext オブジェクトコードを、以下に記載されている API に置き換えてください。

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

DocAssurance サービスの API やサンプルコードの詳細については、「[AEM Document Services をプログラムとして使用する](/help/forms/using/aem-document-services-programmatically.md)」を参照してください。
