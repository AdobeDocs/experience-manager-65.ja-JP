---
title: Reader 拡張証明書の有効期限とその影響
description: Reader 拡張証明書の有効期限とその影響
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---


# Reader 拡張証明書の有効期限とその影響 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Experience Manager Forms（AEM Forms）をご利用のお客様で、Adobe Managed Services またはオンプレミスの Enterprise Base ライセンスをお持ちの場合、Acrobat Reader DC Extensions サービスを使用する資格があります。サービスを使用すると、追加の使用権限を付与して Acrobat Reader の機能を拡張することで、組織内でインタラクティブ PDF ドキュメントを簡単に共有できます。このサービスは、PDF ドキュメントに使用権限を追加し、ドキュメントへのコメントの追加、フォームへの入力、ドキュメントの保存など、Adobe Acrobat Reader を使用して PDF ドキュメントを開いた場合には使用できない機能をアクティブにします。サードパーティユーザーは、使用権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。使用権限が追加された PDF ドキュメントは、「使用権限を付与されたドキュメント」と呼ばれます。使用権限を付与された PDF ドキュメントを Acrobat Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

アドビは公開鍵インフラストラクチャ（PKI）を使用して、ライセンスやイネーブルメント機能に使用する電子証明書を発行します。アドビは、認証局 **Adobe ルート CA** によって証明書を発行していますが、この証明書は 2023年1月7日（PT）に期限が切れる予定です。証明書の有効期限が切れても、**Adobe ルート CA** ベースの証明書（古い証明書）から発行された実稼働用の証明書を使用して拡張された PDF ドキュメントには影響しません。すべての PDF ドキュメント（2023年1月7日（PT）より前の古い証明書を使用して拡張された Reader）は、顧客がダウンロードしたものも含め、適用されているすべての使用権限で引き続き機能し、更新する必要はありません。

新しい認証局 **Adobe ルート CA G2**&#x200B;と、新しい認証局に基づく証明書が使用できるようになりました。2023年1月7日（PT）までに、Reader で **Adobe ルート CA G2** に基づく新しい証明書の使用を開始して、新しい PDF ドキュメントを拡張してください。[新しい証明書の取得は、アドビのライセンス web サイトから](https://licensing.adobe.com/)、またはアドビのサポートから可能です。

## よくある質問

**質問：Adobe ルート証明書と Acrobat Reader Extensions 証明書の違いは何ですか？ Adobe ルート証明書は Acrobat Reader Extensions 証明書に依存していますか。両方の証明書の有効期限は 2023年1月ですか。**

回答：Adobe ルート CA は、Acrobat Reader Extensions 証明書の発行元の認証局です。 2023年1月7日（PT）に「Adobeルート CA」と、そこから発行されたすべての証明書の有効期限が切れます。

**質問：証明書の失効や、PDF ドキュメントの使用や開封に対する影響に関して、アドビから以前連絡がありました。 その通信は無視すべきですか。**

回答：状況の再評価に基づき、2023年1月7日（PT）以前に「Adobeルート CA」から発行された実稼働環境用の証明書を用いて延長されたすべての PDF ドキュメントは、2023年1月7日（PT）以降も変更なしで引き続き機能します。既に PDF ドキュメントを更新している場合、エクスペリエンスに変更はありません。

**質問：他に質問がある場合、誰に問い合わせればよいですか？**

回答：[アドビサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support)に連絡するか、またはサポートチケットを発行してください。

**質問：2023年1月7日（PT）より前に証明書をアップデートしない場合はどうなりますか？**

回答：2023年1月7日（PT）より前に発行された古い「Adobeルート CA」からの実稼働環境用の証明書を使用して拡張されたすべての PDF ドキュメントは、2023年1月7日（PT）以降も引き続き機能します。評価用証明書で拡張された PDF は、有効期限が切れた後は機能しません。

**質問：新しい証明書の説明は古い証明書とは異なりますか？**

回答：新しい Acrobat Reader Extensions 証明書の説明には、プログラム名として **G3-P24** が記載されています。古い証明書（「証明書ルート CA」に基づく証明書）の説明では、**P24** がプログラム名として記載されています。

**質問：最新の証明書を取得するにはどうすればよいですか？**

回答：資格のある（有効なライセンスを持つ）Forms 顧客は、新しい証明書（「Adobe Root CA G2」に基づく証明書）を[アドビライセンス web サイト](https://licensing.adobe.com/)からダウンロードできます。アドビライセンス web サイトで証明書が見つからない場合は、[アドビサポート](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja&amp;s#support)に連絡するか、またはサポートチケットを発行します。

**質問：「Adobeルート CA」（古い認証局）から発行された証明書を使用して拡張された PDF ドキュメントは、2023年1月7日（PT）以降も引き続き機能しますか？**

回答：はい。2023年1月7日（PT）より前に「Adobeルート CA」（旧証明機関）から発行された実稼働環境用の証明書を使用して拡張されたすべての PDF ドキュメントは、2023年1月7日（PT）以降も変更なしで引き続き機能します。 評価用証明書を使用して拡張された PDF ドキュメントは、有効期限を過ぎると機能しなくなります。

**質問：「Adobeルート CA」（古い認証局）から発行された証明書で拡張された PDF ドキュメントを引き続き使用するには、どのバージョンの Adobe Acrobat Reader が必要ですか？**

回答：Adobe Acrobat Reader 2020 以降では、「Adobeルート CA」（古い認証局）で拡張された PDF ドキュメントを使用する必要があります。 このドキュメントの公開時点でサポートされている Acrobat Reader のバージョンです。[サポートされていないバージョンの Adobe Acrobat](https://helpx.adobe.com/jp/support/programs/eol-matrix.html) を使用している場合、アドビは[最新バージョンの Adobe Acrobat Reader](https://get.adobe.com/jp/reader/) をダウンロードしてインストールすることをお勧めします。

**質問：「Adobeルート CA 2」（新しい認証局）から発行された証明書で拡張された PDF ドキュメントを引き続き使用するには、どのバージョンの Adobe Acrobat Reader が必要ですか？**

回答：「Adobe Root CA 2」（新しい認証局）で拡張された PDF ドキュメントを利用するには、Adobe Acrobat Reader 2020 以降が必要です。[サポートされていないバージョンの Adobe Acrobat Reader](https://helpx.adobe.com/jp/support/programs/eol-matrix.html) を使用している場合、アドビは[最新バージョンの Adobe Acrobat Reader をダウンロードしてインストールする](https://get.adobe.com/jp/reader/)ことをお勧めします。

**質問：既存のエイリアスを引き続き使用しながら、古い Acrobat Reader Extensions 証明書を削除し、Adobe Experience Manager Forms サーバーに新しい証明書を追加できますか？**

回答：はい。古い Acrobat Reader Extensions 証明書を削除して、既存のエイリアスを持つ新しい証明書を Adobe Experience Manager Forms サーバーに追加できます。

**質問：新しい証明書と古い Acrobat Reader Extensions 証明書の両方を Adobe Experience Manager Forms サーバーに保持できますか？**

回答：はい。Adobe Experience Manager Forms サーバー上では、両方の証明書を保持できますが、異なるエイリアスを使用します。 2023年1月7日（PT）以降は、新しい証明書のみを使用して、PDF ドキュメントを Reader 拡張することができます。

**質問：同じ Acrobat Reader Extensions 証明書をすべての Adobe Experience Manager Forms 環境に読み込むことができますか？**

回答：はい。同じ Acrobat Reader Extensions 証明書を複数の環境で使用することができます。

**質問：PDF ドキュメントに適用される使用権限を確認する方法を教えてください。**

回答：[getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=ja#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API を使用して、PDF ドキュメントに適用される使用権限に関する情報を取得することができます。

**質問：Acrobat Reader Extensions 証明書ファイルのパスワードを変更する方法を教えてください。**

回答：Microsoft Windows で証明書のパスワードを変更するには、Microsoft 管理コンソール（MMC）を使用して証明書をインストールし、「**キーをエクスポート可能としてマークする**」を選択します。インストールが完了したら、証明書を秘密鍵を使用して書き出し、PFX ファイルに別のパスワードを使用します。


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

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

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

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
