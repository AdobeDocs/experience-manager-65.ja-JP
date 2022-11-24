---
title: Reader拡張証明書の有効期限とその影響
description: Reader拡張証明書の有効期限とその影響
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: bcbfdcd305b7319506a11677909895c38f92a6cf
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 4%

---


# Reader拡張証明書の有効期限とその影響 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Experience Manager Forms(AEM Forms) をご利用のお客様は、Adobe Managed Services またはオンプレミスの Enterprise Base ライセンスをお持ちの場合、Acrobat Reader DC Extensions サービスを使用する権利が付与されます。 このサービスを使用すると、追加の使用権限でAcrobat Readerの機能を拡張し、組織がインタラクティブなPDFドキュメントを簡単に共有できます。 このサービスは、PDFドキュメントに使用権限を追加し、ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など、Adobe Acrobat Readerを使用してPDFドキュメントを開いた場合に使用できない機能をアクティブにします。 サードパーティユーザーは、使用権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。使用権限が追加された PDF ドキュメントは、「使用権限を付与されたドキュメント」と呼ばれます。Acrobat Readerで権限が付与されたPDFドキュメントを開いたユーザーは、そのドキュメントに対して有効な操作を実行できます。

Adobeでは、公開鍵基盤 (PKI) を利用して、ライセンスや機能の有効化に使用する電子証明書を発行します。 Adobeは、2023 年 1 月 7 日に期限切れに設定された認証局「Adobeルート CA」に基づいて証明書を発行しています。 新しい認証局「Adobeルート CA G2」と、新しい認証局に基づく証明書が使用できるようになりました。

2023 年 1 月 7 日以降、古い証明書 (「Adobeルート CA」に基づく証明書 ) は機能しなくなります。 Adobeでは、2023 年 1 月 7 日以前にPDFドキュメントをReaderするために、「Adobeルート CA G2」に基づく新しい証明書の使用を開始することをお勧めします。  以下が可能です。 [Adobeライセンス Web サイトから新しい証明書を取得する](https://licensing.adobe.com/) またはAdobeのサポート。

PDFドキュメント (2023 年 1 月 7 日より前の古い証明書を使用して拡張されたReader) は、お客様がダウンロードしたものも含め、引き続き、それらに適用されるすべての使用権限で使用され、更新は必要ありません。

## よくある質問

**Q.Adobeルート証明書とAcrobat Reader Extensions 証明書の違いは何ですか？ Adobeルート証明書はAcrobat Reader Extensions 証明書に依存していますか？ これらの証明書の有効期限は 2023 年 1 月ですか？**

A.Adobeルート CA は、Acrobat Reader Extensions 証明書の発行元の認証局です。 2023 年 1 月 7 日に、「Adobeルート CA」と、そこから発行されたすべての証明書の有効期限が切れます。

**証明書の失効や、PDF文書の使用・開封に対する影響に関して、Adobeからの以前の連絡があった。 そのコミュニケーションは無視すべきですか？**

A.状況の再評価に基づき、2023 年 1 月 7 日より前の「Adobeルート CA」から発行された生産証明書を用いて延長されたすべてのPDF文書は、2023 年 1 月 7 日以降、変更なしで引き続き機能します。 既にPDFを更新している場合、エクスペリエンスに変更はありません。


**Q.他に質問がある場合は誰に問い合わせればよいですか？**

A.連絡先は [Adobeサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support) またはサポートチケットを発行します。

**Q. 2023 年 1 月 7 日より前に証明書を更新しない場合はどうなりますか。**

A. 2023 年 1 月 7 日より前に発行された古い「Adobeルート CA」からの実稼動証明書を使用して拡張されたすべてのPDFドキュメントは、2023 年 1 月 7 日以降も引き続き機能します。 評価証明書で拡張されたPDFは、有効期限の後は機能しません。

**Q.新しい証明書の説明は古い証明書とは異なりますか。**

A.新しいAcrobat Reader Extensions 証明書の説明 **G3-P24** をプログラム名として使用します。 古い証明書（「証明書ルート CA」に基づく証明書）の説明で、次のことを行います。 **P24** は、プログラム名として言及されます。

**Q.最新の証明書を取得するにはどうすればよいですか？**

A.権利を付与されているFormsのすべてのお客様（アクティブライセンスを持つ）は、新しい証明書 (「Adobeルート CA G2」に基づく証明書 ) を [Adobeライセンス Web サイト](https://licensing.adobe.com/). Adobeライセンス Web サイトで証明書が見つからない場合は、 [Adobeサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) またはサポートチケットを発行します。

**Q. 「Adobeルート CA」（古い認証局）から発行された証明書を使用して拡張されたPDFドキュメントは、2023 年 1 月 7 日以降も引き続き機能しますか。**

A.はい。2023 年 1 月 7 日より前に「Adobeルート CA」（旧証明機関）から発行された実稼働版証明書を使用して拡張されたすべてのPDFドキュメントは、2023 年 1 月 7 日以降、変更なしで引き続き機能します。 PDF証明書を使用して拡張された評価ドキュメントは、有効期限を過ぎると機能しなくなります。

**Q. 「Adobeルート CA」（古い証明機関）から発行された証明書で拡張されたPDFドキュメントを引き続き使用するには、どのバージョンのAdobe Acrobat Readerが必要ですか？**

A. Adobe Acrobat Reader 2020 以降では、「Adobeルート CA」（古い証明機関）で拡張されたPDFドキュメントを使用する必要があります。 このドキュメントの公開時にサポートされているAcrobat Readerのバージョンです。 を使用している場合、 [Adobe Acrobatの非サポートバージョン](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)を使用する場合、Adobeは、 [最新バージョンのAdobe Acrobat Readerをダウンロードしてインストールする](https://get.adobe.com/jp/reader/).

**Q. 「Adobeルート CA 2」（新しい証明機関）から発行された証明書で拡張されたPDFドキュメントを引き続き使用するには、どのバージョンのAdobe Acrobat Readerが必要ですか？**

A. Adobe Acrobat Reader 2020 以降では、「Adobeルート CA 2」（新しい証明機関）で拡張されたPDFドキュメントを使用する必要があります。 を使用している場合、 [Adobe Acrobat Readerの非サポートバージョン](https://helpx.adobe.com/support/programs/eol-matrix.html)を使用する場合、Adobeは、 [最新バージョンのAdobe Acrobat Readerをダウンロードしてインストールする](https://get.adobe.com/reader/).

**Q.既存のエイリアスを引き続き使用しながら、古いAcrobat Reader Extensions 証明書を削除して、Adobe Experience Manager Formsサーバーに新しい証明書を追加できますか？**

A.はい。古いAcrobat Reader Extensions 証明書を削除して、既存のエイリアスを持つ新しい証明書をAdobe Experience Manager Forms Server に追加できます。

**Q.新しい証明書と古いAcrobat Reader Extensions 証明書の両方をAdobe Experience Manager Forms Server に保持できますか？**

A.はい。Adobe Experience Manager Forms Server 上では、両方の証明書を保持できますが、異なるエイリアスを使用できます。 2023 年 1 月 8 日以降は、新しい証明書のみを使用して、PDFドキュメントをReader拡張できます。

**Q.同じAcrobat Reader Extensions 証明書をすべてのAdobe Experience Manager Forms環境に読み込むことはできますか？**

A.はい。同じAcrobat Reader Extensions 証明書を複数の環境で使用できます。

**Q.PDF文書に適用される使用権限を確認する方法を教えてください。**

A. [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) PDFドキュメントに適用された使用権限に関する情報を取得する API。

**Q. Acrobat Reader Extensions 証明書ファイルのパスワードを変更する方法を教えてください。**

A. Microsoft Windows で証明書のパスワードを変更するには、Microsoft管理コンソール (MMC) を使用して証明書をインストールし、「 」を選択します **キーを書き出し可能にする**. インストールが完了したら、証明書を秘密鍵で書き出し、PFX ファイルに別のパスワードを使用します。


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
