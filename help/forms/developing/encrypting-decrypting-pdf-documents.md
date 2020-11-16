---
title: PDFドキュメントの暗号化と復号化
seo-title: PDFドキュメントの暗号化と復号化
description: 'null'
seo-description: 'null'
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '8118'
ht-degree: 8%

---


# PDFドキュメントの暗号化と復号化 {#encrypting-and-decrypting-pdf-documents}

**Encryptionサービスについて**

Encryptionサービスを使用すると、ドキュメントの暗号化および復号化を行うことができます。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryptionサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをパスワードで暗号化します。 (「PDFドキュメントのパスワード [による暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。
* PDFドキュメントを証明書で暗号化します。 (See [Encrypting PDF Documents with Certificates](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* PDFドキュメントからパスワードベースの暗号化を削除します。 (Removing Password Encryption [を参照](encrypting-decrypting-pdf-documents.md#removing-password-encryption))。
* PDFドキュメントから証明書ベースの暗号化を削除します。 (証明書ベースの暗号化の [削除を参照](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption))。
* 他のサービス操作を実行できるように、PDFドキュメントのロックを解除します。 例えば、パスワードで暗号化されたPDFドキュメントのロックが解除された後に、電子署名を適用できます。 (暗号化されたPDFドキュメントの [ロック解除を参照](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents))。
* 保護されたPDFドキュメントの暗号化タイプを指定します。 (Determining Encryption Type [](encrypting-decrypting-pdf-documents.md#determining-encryption-type)（暗号化タイプの決定を参照）。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Encrypting PDF Documents with a Password {#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、PDFドキュメントのデジタル署名など、別のAEM Forms操作をドキュメントで実行する前に、パスワードで暗号化されたPDFドキュメントをロック解除する必要があります。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードする場合、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、暗号化を行わないことをお勧めします。 (リソースの [書き込みを参照](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをパスワードで暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化クライアントAPIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 暗号化の実行時オプションを設定します。
1. 追加パスワード。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**暗号化クライアントAPIオブジェクトの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。

**暗号化するPDFドキュメントの取得**

パスワードを使用してドキュメントを暗号化するには、暗号化されていないPDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**暗号化の実行時オプションの設定**

PDFドキュメントをパスワードで暗号化するには、2つのパスワード値を含む4つの値を指定します。 最初のパスワード値は、PDFドキュメントの暗号化に使用され、PDFドキュメントを開くときに指定する必要があります。 2番目のパスワード値は、マスターパスワード値という名前で、PDFドキュメントから暗号化を削除するために使用されます。 パスワードの値は大文字と小文字が区別されます。また、これらの2つのパスワード値を同じ値にすることはできません。

暗号化するPDFドキュメントリソースを指定する必要があります。 PDFドキュメント全体(ドキュメントのメタデータを除くすべて)またはドキュメントの添付ファイルのみを暗号化できます。 ドキュメントの添付ファイルのみを暗号化する場合、ユーザーが添付ファイルにアクセスしようとすると、パスワードの入力が求められます。

PDFドキュメントを暗号化する場合、保護されたドキュメントに関連付けられている権限を指定できます。 権限を指定すると、パスワードで暗号化されたPDFドキュメントを開いたユーザーに対して実行を許可するアクションを制御できます。 例えば、フォームデータを正しく抽出するには、次の権限を設定する必要があります。

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>権限は、 `PasswordEncryptionPermission` 定義済みリストの値として指定します。

**追加パスワード**

保護されていないPDFドキュメントを取得し、暗号化の実行時の値を設定したら、PDFドキュメントにパスワードを追加できます。

**暗号化されたPDFドキュメントをPDFファイルとして保存します**

パスワードで暗号化されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントの証明書による暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Java APIを使用したPDFドキュメントの暗号化 {#encrypt-a-pdf-document-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化クライアントAPIの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化するPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の実行時オプションを設定します。

   * Create a `PasswordEncryptionOptionSpec` object by invoking its constructor.
   * オブジェクトのメソッドを呼び出し、暗号化するPDFドキュメントリソースを指定する `PasswordEncryptionOptionSpec``setEncryptOption``PasswordEncryptionOption` 定義済みリスト値を渡して、ドキュメントするPDFリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定し `PasswordEncryptionOption.ALL`ます。
   * コンストラクターを使用して、暗号化権限を格納する `java.util.List` オブジェクトを作成し `ArrayList` ます。
   * オブジェクト「s」 `java.util.List``add` メソッドを呼び出し、設定する権限に対応する定義済みリスト値を渡して、権限を指定します。 例えば、PDFドキュメント内のデータをユーザーがコピーできる権限を設定するには、を指定し `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`ます。 （設定する権限ごとに、この手順を繰り返します）。
   * オブジェクトの `PasswordEncryptionOptionSpec``setCompatability` メソッドを呼び出し、Acrobatの互換性レベルを指定する定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 例えば、を指定でき `PasswordEncryptionCompatability.ACRO_7`ます。
   * 暗号化されたPDFドキュメントをユーザーが開くために、 `PasswordEncryptionOptionSpec` オブジェクトの `setDocumentOpenPassword` メソッドを呼び出し、開くパスワードを表すstring値を渡すパスワード値を指定します。
   * マスターパスワード値を指定します。この値を指定すると、ユーザーは、 `PasswordEncryptionOptionSpec` オブジェクトの `setPermissionPassword` メソッドを呼び出し、マスターパスワードを表すstring値を渡すことで、PDFドキュメントから暗号化を削除できます。

1. 追加パスワード。

   オブジェクトの `EncryptionServiceClient` メソッドを呼び出し、次の値を渡して、PDFドキュメントを暗号化し `encryptPDFUsingPassword` ます。

   * パスワードを使用して暗号化するPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * 暗号化の実行時オプションを含む `PasswordEncryptionOptionSpec` オブジェクトです。

   パスワードで暗号化されたPDFドキュメントを含む `encryptPDFUsingPassword``com.adobe.idp.Document` オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingPassword` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの暗号化 {#encrypting-a-pdf-document-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定するには、 `PasswordEncryptionOption` オブジェクトの `PasswordEncryptionOptionSpec``encryptOption` データメンバーに定義済みリスト値を割り当てます。 メタデータと添付ファイルを含むPDF全体を暗号化するには、このデータメンバ `PasswordEncryptionOption.ALL` ーに割り当てます。
   * Acrobat互換性オプションを指定するには、オ `PasswordEncryptionCompatability` ブジェクトの `PasswordEncryptionOptionSpec``compatability` データメンバに定義済みリスト値を割り当てます。 例えば、このデータメンバ `PasswordEncryptionCompatability.ACRO_7` ーに割り当てます。
   * ユーザーが暗号化されたPDFドキュメントを開くためのpassword値を指定します。この値には、 `PasswordEncryptionOptionSpec` オブジェクトの `documentOpenPassword` データメンバーに開いているパスワードを表すstring値を割り当てます。
   * ユーザーがPDFドキュメントから暗号化を削除できるように、マスターパスワードを表すstring値を `PasswordEncryptionOptionSpec` オブジェクトの `permissionPassword` データメンバーに割り当てるためのpassword値を指定します。

1. 追加パスワード。

   オブジェクトの `EncryptionServiceClient` メソッドを呼び出し、次の値を渡して、PDFドキュメントを暗号化し `encryptPDFUsingPassword` ます。

   * パスワードを使用して暗号化するPDFドキュメントを含む `BLOB` オブジェクトです。
   * 暗号化の実行時オプションを含む `PasswordEncryptionOptionSpec` オブジェクトです。

   パスワードで暗号化されたPDFドキュメントを含む `encryptPDFUsingPassword``BLOB` オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、保護されたPDF `System.IO.FileStream` ドキュメントーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `encryptPDFUsingPassword` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Encrypting PDF Documents with Certificates {#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化を使用すると、公開鍵による暗号化を使用して、特定の受信者用のドキュメントを暗号化できます。 それぞれの受信者に、異なる権限を与えることができます。公開鍵によって、さまざまな暗号化を行うことができます。An algorithm is used to generate two large numbers, known as *keys*, that have the following properties:

* 鍵のうち 1 つは、一連のデータを暗号化するために使用されます。その後、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう片方の鍵と区別することは不可能です。

鍵の1つは、ユーザーの秘密鍵として機能します。 そのユーザーのみがこの鍵にアクセスできることが重要です。もう1つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードする場合、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、暗号化を行わないことをお勧めします。 (リソースの [書き込みを参照](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>PDFドキュメントを証明書で暗号化する前に、証明書をAEM Formsに追加しておく必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 (Trust Manager APIを使用した秘密鍵証明書の [読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFドキュメントを証明書で暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化クライアントAPIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 証明書を参照します。
1. 暗号化の実行時オプションを設定します。
1. 証明書で暗号化されたPDFドキュメントを作成します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

**暗号化クライアントAPIオブジェクトの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、 `EncrytionServiceClient` オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、 `EncryptionServiceService` オブジェクトを作成します。

**暗号化するPDFドキュメントの取得**

暗号化する非暗号化のPDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**証明書の参照**

PDFドキュメントを証明書で暗号化するには、PDFドキュメントの暗号化に使用される証明書を参照します。 証明書は.cerファイル、.crtファイル、または.pemファイルです。 PKCS#12ファイルは、対応する証明書を持つ秘密鍵を保存するために使用されます。

PDFドキュメントを証明書で暗号化する場合は、保護されたドキュメントに関連付けられている権限を指定します。 権限を指定すると、証明書で暗号化されたPDFドキュメントを開いたユーザーが実行できるアクションを制御できます。

**暗号化の実行時オプションの設定**

暗号化するPDFドキュメントリソースを指定します。 PDFドキュメント全体(ドキュメントのメタデータを除くすべて)またはドキュメントの添付ファイルのみを暗号化できます。

**証明書で暗号化されたPDFドキュメントの作成**

保護されていないPDFドキュメントを取得し、証明書を参照し、実行時のオプションを設定したら、証明書で暗号化されたPDFドキュメントを作成できます。 PDFドキュメントが暗号化された後、対応する公開鍵を使用して復号化する必要があります。

**暗号化されたPDFドキュメントをPDFファイルとして保存します**

暗号化されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用した証明書によるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[WebサービスAPIを使用して、PDFドキュメントを証明書で暗号化する](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用した証明書によるPDFドキュメントの暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化するPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 証明書を参照します。

   * コンストラクタを使用して、権限情報を格納する `java.util.List` オブジェクトを作成します。
   * 暗号化されたドキュメントに関連付けられている権限を指定します。そのためには、 `java.util.List` オブジェクトの `add` メソッドを呼び出し、保護されたPDFドキュメントを開くユーザーに許可されている権限を表す `CertificateEncryptionPermissions` 定義済みリスト値を渡します。 例えば、すべての権限を指定するには、を渡し `CertificateEncryptionPermissions.PKI_ALL_PERM`ます。
   * コンストラクタを使用して `Recipient` オブジェクトを作成します。
   * PDFドキュメントのコンストラクターを使用し、証明書の場所を指定するstring値を渡して、PDFの暗号化に使用される証明書を表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し、証明書を表すオブジェクトを渡して、 `com.adobe.idp.Document``java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクトの `Recipient` メソッドを呼び出し、証明書を含む `setX509Cert``com.adobe.idp.Document` オブジェクトを渡します。 (さらに、 `Recipient`オブジェクトには、証明書ソースとしてTruststore証明書エイリアスまたはLDAP URLを設定できます)。
   * 権限と証明書の情報を格納する `CertificateEncryptionIdentity` オブジェクトを作成するには、コンストラクターを使用します。
   * オブジェクトの `CertificateEncryptionIdentity` メソッドを呼び出し、権限情報を格納する `setPerms``java.util.List` オブジェクトを渡します。
   * オブジェクトの `CertificateEncryptionIdentity` メソッドを呼び出し、証明書情報を格納する `setRecipient``Recipient` オブジェクトを渡します。
   * コンストラクターを使用して、証明書情報を格納する `java.util.List` オブジェクトを作成します。
   * Invoke the `java.util.List` object’s add method and pass the `CertificateEncryptionIdentity` object. (この `java.util.List` オブジェクトは、メソッドにパラメーターとして渡され `encryptPDFUsingCertificates` ます)。

1. 暗号化の実行時オプションを設定します。

   * Create a `CertificateEncryptionOptionSpec` object by invoking its constructor.
   * オブジェクトのメソッドを呼び出し、暗号化するPDFドキュメントリソースを指定する `CertificateEncryptionOptionSpec``setOption``CertificateEncryptionOption` 定義済みリスト値を渡して、ドキュメントするPDFリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定し `CertificateEncryptionOption.ALL`ます。
   * オブジェクトのメソッドを呼び出し、Acrobatの互換性レベルを指定する `CertificateEncryptionOptionSpec``setCompat``CertificateEncryptionCompatibility` 定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 例えば、を指定でき `CertificateEncryptionCompatibility.ACRO_7`ます。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュメントを証明書 `EncryptionServiceClient` で暗号化し `encryptPDFUsingCertificates` ます。

   * 暗号化するPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * 証明書情報を格納する `java.util.List` オブジェクトです。
   * 暗号化の実行時オプションを含む `CertificateEncryptionOptionSpec` オブジェクトです。

   証明書で暗号化されたPDFドキュメントを含む `encryptPDFUsingCertificates``com.adobe.idp.Document` オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingCertificates` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した証明書によるPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用して、PDFドキュメントを証明書で暗号化する {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、証明書で暗号化されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. 証明書を参照します。

   * コンストラクタを使用して `Recipient` オブジェクトを作成します。このオブジェクトは、証明書情報を格納します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトには、PDFドキュメントを暗号化する証明書が格納されます。
   * コンストラクターを呼び出し、証明書のファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。
   * 証明書を保存する `BLOB` オブジェクトを `Recipient` オブジェクトの `x509Cert` データメンバーに割り当てます。
   * コンストラクターを使用して、証明書情報を格納する `CertificateEncryptionIdentity` オブジェクトを作成します。
   * 証明書を保存する `Recipient` オブジェクトを、 `CertificateEncryptionIdentity`オブジェクトの受信者データメンバに割り当てます。
   * 配列を作成し、 `Object` オブジェクトを配列の最初の要素に割り当て `CertificateEncryptionIdentity``Object` ます。 この `Object` 配列は、メソッドにパラメーターとして渡され `encryptPDFUsingCertificates` ます。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定するには、 `CertificateEncryptionOption` オブジェクトの `CertificateEncryptionOptionSpec``option` データメンバーに定義済みリスト値を割り当てます。 メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、このデータメンバー `CertificateEncryptionOption.ALL` に割り当てます。
   * Acrobat互換性オプションを指定するには、オ `CertificateEncryptionCompatibility` ブジェクトの `CertificateEncryptionOptionSpec``compat` データメンバに定義済みリスト値を割り当てます。 例えば、このデータメンバ `CertificateEncryptionCompatibility.ACRO_7` ーに割り当てます。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュメントを証明書 `EncryptionServiceService` で暗号化し `encryptPDFUsingCertificates` ます。

   * 暗号化するPDFドキュメントを含む `BLOB` オブジェクトです。
   * 証明書情報を格納する `Object` 配列。
   * 暗号化の実行時オプションを含む `CertificateEncryptionOptionSpec` オブジェクトです。

   証明書で暗号化されたPDFドキュメントを含む `encryptPDFUsingCertificates``BLOB` オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、保護されたPDF `System.IO.FileStream` ドキュメントーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `encryptPDFUsingCertificates` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除 {#removing-certificate-based-encryption}

証明書で暗号化されたPDFドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。 暗号化がPDFドキュメントから削除されると、その暗号化は保護されなくなります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントから証明書ベースの暗号化を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryptionサービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. 暗号化を削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

**Encryptionサービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、 `EncrytionServiceClient` オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、 `EncryptionServiceService` オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外が発生します。 同様に、パスワードで暗号化されたドキュメントから証明書ベースの暗号化を削除しようとすると、例外が発生します。

**暗号化の削除**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。 秘密鍵のエイリアス値は、暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するときに指定します。 公開鍵について詳しくは、「証明書によるPDFドキュメントの [暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)」を参照してください。

>[!NOTE]
>
>秘密鍵はAEM FormsTrust Storeに保存されます。 証明書がそこに配置されると、エイリアス値が指定されます。

**PDFドキュメントの保存**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 PDFドキュメントは、Adobe ReaderまたはAcrobatで開くことができます。

**関連トピック**

[Java APIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[WebサービスAPIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化を削除します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、PDFドキュメントから証明書ベースの暗号化 `EncryptionServiceClient` を削除し `removePDFCertificateSecurity` ます。

   * 暗号化されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * PDfドキュメントの暗号化に使用されるキーに対応する秘密鍵のエイリアス名を指定するstring値。

   この `removePDFCertificateSecurity` メソッドは、保護されていないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. `com.adobe.idp.Document` メソッドから返された `removePDFCredentialSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した証明書ベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-web-service-api}

Encryption API（Webサービス）を使用して、証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、暗号化されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。

1. 暗号化を削除します。

   オブジェクトの `EncryptionServiceClient``removePDFCertificateSecurity` メソッドを呼び出し、次の値を渡します。

   * 暗号化されたPDFドキュメントを表すファイルストリームデータを含む `BLOB` オブジェクトです。
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   この `removePDFCredentialSecurity` メソッドは、保護されていないPDFドキュメントを含む `BLOB` オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワード暗号化の削除 {#removing-password-encryption}

パスワードベースの暗号化をPDFドキュメントから削除して、パスワードを指定しなくても、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができるようにすることができます。 パスワードベースの暗号化をPDFドキュメントから削除すると、ドキュメントのセキュリティは保護されなくなります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントからパスワードベースの暗号化を削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Encryptionサービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. パスワードを削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**Encryptionサービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、 `EncrytionServiceClient` オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、 `EncryptionServiceService` オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

パスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外が発生します。

**パスワードの削除**

暗号化されたPDFドキュメントからパスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントから暗号化を削除するために使用するマスターパスワードの両方を指定する必要があります。 パスワードで暗号化されたPDFドキュメントを開く際に使用するパスワードは、暗号化の削除には使用できません。 マスターパスワードは、PDFドキュメントがパスワードを使用して暗号化される場合に指定します。 (「PDFドキュメントのパスワード [による暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。

**PDFドキュメントの保存**

EncryptionサービスでPDFドキュメントからパスワードベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、パスワードを指定せずに、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. パスワードを削除します。

   オブジェクトの `EncryptionServiceClient` メソッドを呼び出し、次の値を渡すことで、PDFドキュメントからパスワードベースの暗号化を削除し `removePDFPasswordSecurity` ます。

   * 暗号化されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるマスターパスワード値を指定するstring値です。

   この `removePDFPasswordSecurity` メソッドは、保護されていないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. `Document` メソッドから返された `removePDFPasswordSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したパスワードベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### WebサービスAPIを使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-web-service-api}

Encryption API（Webサービス）を使用して、パスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。

1. パスワードを削除します。

   オブジェクトの `EncryptionServiceService``removePDFPasswordSecurity` メソッドを呼び出し、次の値を渡します。

   * 暗号化されたPDFドキュメントを表すファイルストリームデータを含む `BLOB` オブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   この `removePDFPasswordSecurity` メソッドは、保護されていないPDFドキュメントを含む `BLOB` オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化されたPDFドキュメントのロック解除 {#unlocking-encrypted-pdf-documents}

パスワードで暗号化または証明書で暗号化されたPDFドキュメントは、ロックを解除しないと、別のAEM Forms操作を実行できません。 暗号化されたPDFドキュメントに対して操作を実行しようとすると、例外が生成されます。 暗号化されたPDFドキュメントのロックを解除した後、暗号化されたPDF画像に対して1つ以上の操作を実行できます。 これらの操作は、Acrobat Reader DC拡張サービスなど、他のサービスに属することができます。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

暗号化されたPDFドキュメントのロックを解除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryptionサービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. ドキュメントのロックを解除します。
1. AEM Forms操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

**Encryptionサービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、 `EncrytionServiceClient` オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、 `EncryptionServiceService` オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

ロックを解除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントのロックを解除しようとすると、例外が発生します。

**ドキュメントのロック解除**

パスワードで暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、パスワードで暗号化されたPDFドキュメントを開くために使用するパスワード値の両方が必要です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。 (「PDFドキュメントのパスワード [による暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。

証明書で暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM Forms操作の実行**

暗号化されたPDFドキュメントのロックが解除された後、その画像に対して別のサービス操作（使用権限の適用など）を実行できます。 この操作は、Acrobat Reader DC拡張サービスに属します。

**関連トピック**

[Java APIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-java-api}

暗号化API(Java)を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントのロックを解除します。

   オブジェクトまたは `EncryptionServiceClient` メソッドを呼び出して、暗号化されたPDFドキュメントのロックを解除し `unlockPDFUsingPassword` ま `unlockPDFUsingCredential` す。

   パスワードを使用して暗号化されたPDFドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを呼び出し、次の値を渡します。

   * パスワードで暗号化されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   証明書で暗号化されているPDFドキュメントのロックを解除するには、 `unlockPDFUsingCredential` メソッドを呼び出し、次の値を渡します。

   * A `com.adobe.idp.Document` object that contains the certificate-encrypted PDF document.
   * PDFドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   メソッド `unlockPDFUsingPassword` と `unlockPDFUsingCredential` メソッドは共に、別のAEM FormsJavaメソッドに渡した `com.adobe.idp.Document` オブジェクトを返し、操作を実行します。

1. AEM Forms操作を実行します。

   ロック解除されたPDFドキュメントに対して、ビジネス要件に合わせてAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合は、またはのメソッドによって返された `com.adobe.idp.Document` オブジェクトをその `unlockPDFUsingPassword` オブジェクトの `unlockPDFUsingCredential``ReaderExtensionsServiceClient``applyUsageRights` メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAPモード）を使用した暗号化されたPDFドキュメントのロック解除

[PDFドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Encryption API（Webサービス）を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。

1. ドキュメントのロックを解除します。

   オブジェクトまたは `EncryptionServiceClient` メソッドを呼び出して、暗号化されたPDFドキュメントのロックを解除し `unlockPDFUsingPassword` ま `unlockPDFUsingCredential` す。

   パスワードを使用して暗号化されたPDFドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを呼び出し、次の値を渡します。

   * パスワードで暗号化されたPDFドキュメントを含む `BLOB` オブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   証明書で暗号化されているPDFドキュメントのロックを解除するには、 `unlockPDFUsingCredential` メソッドを呼び出し、次の値を渡します。

   * A `BLOB` object that contains the certificate-encrypted PDF document.
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   メソッド `unlockPDFUsingPassword` と `unlockPDFUsingCredential` メソッドは共に、別のAEM Formsメソッドに渡した `com.adobe.idp.Document` オブジェクトを返し、操作を実行します。

1. AEM Forms操作を実行します。

   ロック解除されたPDFドキュメントに対して、ビジネス要件に合わせてAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合は、またはのメソッドによって返された `BLOB` オブジェクトをその `unlockPDFUsingPassword` オブジェクトの `unlockPDFUsingCredential``ReaderExtensionsServiceClient``applyUsageRights` メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化タイプの決定 {#determining-encryption-type}

Java Encryption Service APIまたはWebサービスのEncryption Service APIを使用して、PDFドキュメントを保護する暗号化の種類をプログラムで判断できます。 PDFドキュメントが暗号化されているかどうか、および暗号化されている場合は暗号化の種類を動的に判断する必要がある場合があります。 例えば、PDFドキュメントをパスワードベースの暗号化またはRights Managementポリシーで保護するかどうかを指定できます。

PDFドキュメントは、次の暗号化タイプで保護できます。

* パスワードベースの暗号化
* 証明書ベースの暗号化
* Rights Managementサービスによって作成されるポリシーです
* 別の種類の暗号化

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

PDFドキュメントを保護する暗号化の種類を決定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryptionサービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. 暗号化タイプを決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

**サービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、 `EncrytionServiceClient` オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、 `EncryptionServiceService` オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

PDFドキュメントを取得して、保護する暗号化の種類を判断する必要があります。

**暗号化タイプの決定**

PDFドキュメントを保護する暗号化の種類を指定できます。 PDFドキュメントが保護されていない場合は、PDFドキュメントが保護されていないことを通知するEncryptionサービスが提供されます。

**関連トピック**

[Java APIを使用した暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[WebサービスAPIを使用した暗号化の種類の決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[ポリシーによるドキュメントの保護](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java APIを使用した暗号化タイプの決定 {#determine-the-encryption-type-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、PDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化タイプを決定します。

   * オブジェクトの `EncryptionServiceClient` メソッドを呼び出し、PDFドキュメントを含むオブジェクトを渡すことで、暗号化タイプを決定し `getPDFEncryption``com.adobe.idp.Document` ます。 このメソッドは、 `EncryptionTypeResult` オブジェクトを返します。
   * オブジェクトの `EncryptionTypeResult` メソッドを呼び出し `getEncryptionType` ます。 このメソッドは、暗号化の種類を指定する `EncryptionType` 列挙値を返します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このメソッドはを返し `EncryptionType.PASSWORD`ます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した暗号化の種類の決定 {#determine-the-encryption-type-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. サービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `EncryptionServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/EncryptionService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptionServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `EncryptionServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `EncryptionServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `BLOB``MTOM` データメンバーに割り当てて、オブジェクトを設定します。

1. 暗号化タイプを決定します。

   * オブジェクトの `EncryptionServiceClient` メソッドを呼び出し、PDFドキュメントを含む `getPDFEncryption``BLOB` オブジェクトを渡します。 このメソッドは、 `EncryptionTypeResult` オブジェクトを返します。
   * オブジェクトの `EncryptionTypeResult` データメソッドの値を取得し `encryptionType` ます。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このデータメンバーの値はで `EncryptionType.PASSWORD`す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)