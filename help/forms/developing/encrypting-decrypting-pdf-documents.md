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
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# PDFドキュメントの暗号化と復号化 {#encrypting-and-decrypting-pdf-documents}

**Encryptionサービスについて**

Encryptionサービスを使用すると、ドキュメントの暗号化と復号化を行うことができます。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryptionサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをパスワードで暗号化します。 (PDFドキュメ [ントのパスワードによる暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。
* PDFドキュメントを証明書で暗号化します。 (See [Encrypting PDF Documents with Certificates](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* PDFドキュメントからパスワードベースの暗号化を削除します。 (「パスワー [ド暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-password-encryption)」を参照)。
* PDFドキュメントから証明書ベースの暗号化を削除します。 (証明書ベ [ースの暗号化の削除を参照](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption))。
* PDFドキュメントのロックを解除して、他のサービス操作を実行できるようにします。 例えば、パスワードで暗号化されたPDFドキュメントのロックが解除された後に、ドキュメントに電子署名を適用できます。 (暗号化されたPDF [ドキュメントのロック解除を参照](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents))。
* 保護されたPDFドキュメントの暗号化タイプを決定します。 (Determining [Encryption typeを参照](encrypting-decrypting-pdf-documents.md#determining-encryption-type))。

   ***注意&#x200B;**:Encryptionサービスについて詳しくは、『AEM Formsサービスリファレ[ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。*

## Encrypting PDF Documents with a Password {#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、PDFドキュメントへの電子署名など、別のAEM Forms操作をドキュメントで実行する前に、パスワードで暗号化されたPDFドキュメントのロックを解除する必要があります。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、そのPDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントは、AEM Formsリポジトリにアップロードする前に暗号化しないことをお勧めします。 ( [Writing Resources](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをパスワードで暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryption Client APIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 暗号化の実行時オプションを設定します。
1. パスワードを追加します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**Encryption Client APIオブジェクトの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。

**暗号化するPDFドキュメントの取得**

ドキュメントをパスワードで暗号化するには、暗号化されていないPDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**暗号化の実行時オプションの設定**

PDFドキュメントをパスワードで暗号化するには、2つのパスワード値を含む4つの値を指定します。 最初のパスワード値はPDFドキュメントの暗号化に使用され、PDFドキュメントを開くときに指定する必要があります。 マスターパスワード値という2番目のパスワード値は、PDFドキュメントの暗号化を削除するために使用されます。 パスワードの値は大文字と小文字が区別され、これら2つのパスワードの値を同じにすることはできません。

暗号化するPDFドキュメントリソースを指定する必要があります。 PDFドキュメント全体、ドキュメントのメタデータを除くすべてのデータ、またはドキュメントの添付ファイルのみを暗号化できます。 ドキュメントの添付ファイルのみを暗号化する場合、ユーザーが添付ファイルにアクセスしようとすると、パスワードの入力を求められます。

PDFドキュメントを暗号化する場合は、保護されたドキュメントに関連付けられている権限を指定できます。 権限を指定すると、パスワードで暗号化されたPDFドキュメントを開くユーザーが実行できるアクションを制御できます。 例えば、フォームデータを正常に抽出するには、次の権限を設定する必要があります。

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>権限は列挙値として指 `PasswordEncryptionPermission` 定されます。

**パスワードの追加**

保護されていないPDFドキュメントを取得し、暗号化の実行時の値を設定した後、PDFドキュメントにパスワードを追加できます。

**暗号化されたPDFドキュメントをPDFファイルとして保存**

パスワードで暗号化されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントの証明書による暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Java APIを使用したPDFドキュメントの暗号化 {#encrypt-a-pdf-document-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化クライアントAPIの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、暗号化するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の実行時オプションを設定します。

   * Create a `PasswordEncryptionOptionSpec` object by invoking its constructor.
   * オブジェクトのメソッドを呼び出し、暗号化するドキュメ `PasswordEncryptionOptionSpec` ントリソースを指 `setEncryptOption` 定する列 `PasswordEncryptionOption` 挙値を渡して、暗号化するPDFドキュメントリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定しま `PasswordEncryptionOption.ALL`す。
   * コンストラク `java.util.List` ターを使用して、暗号化権限を格納するオブジェクトを作成 `ArrayList` します。
   * オブジェクトのメソッドを呼び出 `java.util.List` し、設定す `add` る権限に対応する列挙値を渡して、権限を指定します。 例えば、PDFドキュメント内のデータをユーザーがコピーできる権限を設定するには、を指定しま `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`す。 （設定する権限ごとに、この手順を繰り返します）。
   * オブジェクトのメソッドを呼び出し、Acrobatの互換性 `PasswordEncryptionOptionSpec` レベルを指 `setCompatability` 定する列挙値を渡して、Acrobatの互換性オプションを指定します。 例えば、を指定できます `PasswordEncryptionCompatability.ACRO_7`。
   * ユーザーがオブジェクトのメソッドを呼び出し、開くパスワードを表すstring値を渡すことで、暗号化さ `PasswordEncryptionOptionSpec` れたPDFドキ `setDocumentOpenPassword` ュメントを開くためのパスワード値を指定します。
   * マスターパスワード値を指定します。この値を使用すると、ユーザーはオブジェクトのメソッドを呼び出し、マスターパスワ `PasswordEncryptionOptionSpec` ードを表す `setPermissionPassword` string値を渡すことで、PDFドキュメントの暗号化を解除できます。

1. パスワードを追加します。

   オブジェクトのメソッドを呼び出し、次 `EncryptionServiceClient` の値を渡すこ `encryptPDFUsingPassword` とで、PDFドキュメントを暗号化します。

   * パスワード `com.adobe.idp.Document` を使用して暗号化するPDFドキュメントを含むオブジェクトです。
   * 暗号化の `PasswordEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingPassword` ッドは、パスワードで `com.adobe.idp.Document` 暗号化されたPDFドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingPassword` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの暗号化 {#encrypting-a-pdf-document-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Encryption Client APIオブジェクトを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * オブジェクトのデータメンバーに列挙値を割り当てるこ `PasswordEncryptionOption` とで、暗号化するPDFドキュ `PasswordEncryptionOptionSpec` メントリソース `encryptOption` を指定します。 PDF全体（メタデータと添付ファイルを含む）を暗号化するには、このデータメンバ `PasswordEncryptionOption.ALL` ーに割り当てます。
   * オブジェクトのデータメンバに列挙値を割り当て `PasswordEncryptionCompatability` て、Acrobatの互換性オ `PasswordEncryptionOptionSpec` プションを `compatability` 指定します。 例えば、このデータメ `PasswordEncryptionCompatability.ACRO_7` ンバーに割り当てます。
   * 暗号化されたPDFドキュメントをユーザーが開くためのパスワード値を指定します。この値は、オブジェクトのデータメンバーに開くパスワードを表すstring値 `PasswordEncryptionOptionSpec` を割り当てるこ `documentOpenPassword` とで指定します。
   * ユーザーがマスターパスワードを表すstring値をオブジェクトのデータメンバーに割り当てることで、PDFドキュメントから暗号化を削除できるパスワー `PasswordEncryptionOptionSpec` ド値を指 `permissionPassword` 定します。

1. パスワードを追加します。

   オブジェクトのメソッドを呼び出し、次 `EncryptionServiceClient` の値を渡すこ `encryptPDFUsingPassword` とで、PDFドキュメントを暗号化します。

   * パスワード `BLOB` を使用して暗号化するPDFドキュメントを含むオブジェクトです。
   * 暗号化の `PasswordEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingPassword` ッドは、パスワードで `BLOB` 暗号化されたPDFドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `encryptPDFUsingPassword` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Encrypting PDF Documents with Certificates {#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化を使用すると、公開鍵技術を使用して特定の受信者向けにドキュメントを暗号化できます。 それぞれの受信者に、異なる権限を与えることができます。公開鍵によって、さまざまな暗号化を行うことができます。An algorithm is used to generate two large numbers, known as *keys*, that have the following properties:

* 鍵のうち 1 つは、一連のデータを暗号化するために使用されます。その後、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう片方の鍵と区別することは不可能です。

キーの1つは、ユーザーの秘密鍵として機能します。 そのユーザーのみがこの鍵にアクセスできることが重要です。もう1つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、そのPDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントは、AEM Formsリポジトリにアップロードする前に暗号化しないことをお勧めします。 ( [Writing Resources](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>PDFドキュメントを証明書で暗号化する前に、証明書をAEM Formsに追加する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムで追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFドキュメントを証明書で暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryption Client APIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 証明書を参照します。
1. 暗号化の実行時オプションを設定します。
1. 証明書で暗号化されたPDFドキュメントを作成します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**Encryption Client APIオブジェクトの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化するPDFドキュメントの取得**

暗号化する非暗号化PDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**証明書の参照**

PDFドキュメントを証明書で暗号化するには、PDFドキュメントの暗号化に使用する証明書を参照します。 証明書は.cerファイル、.crtファイル、または.pemファイルです。 PKCS#12ファイルは、対応する証明書と共に秘密鍵を保存するために使用されます。

PDFドキュメントを証明書で暗号化する場合は、保護されたドキュメントに関連付けられている権限を指定します。 権限を指定すると、証明書で暗号化されたPDFドキュメントを開くユーザーが実行できるアクションを制御できます。

**暗号化の実行時オプションの設定**

暗号化するPDFドキュメントリソースを指定します。 PDFドキュメント全体、ドキュメントのメタデータを除くすべて、またはドキュメントの添付ファイルのみを暗号化できます。

**証明書で暗号化されたPDFドキュメントの作成**

保護されていないPDFドキュメントを取得し、証明書を参照し、実行時のオプションを設定した後で、証明書で暗号化されたPDFドキュメントを作成できます。 PDFドキュメントが暗号化された後、そのドキュメントを復号化するには、対応する公開鍵が必要です。

**暗号化されたPDFドキュメントをPDFファイルとして保存**

暗号化されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用した証明書によるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[WebサービスAPIを使用した証明書によるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用した証明書によるPDFドキュメントの暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryption Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化するPDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、暗号化するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 証明書を参照します。

   * コンストラクタ `java.util.List` ーを使用して、権限情報を格納するオブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、保護されたPDFドキュメントを開くユーザーに付与された権限を表す列挙値を渡して、暗号化されたドキュメ `java.util.List``add``CertificateEncryptionPermissions` ントに関連付けられた権限を指定します。 例えば、すべての権限を指定するには、を渡しま `CertificateEncryptionPermissions.PKI_ALL_PERM`す。
   * コンストラクタを使用して `Recipient` オブジェクトを作成します。
   * PDFドキュメ `java.io.FileInputStream` ントのコンストラクターを使用し、証明書の場所を指定するstring値を渡して、PDFドキュメントの暗号化に使用される証明書を表すオブジェクトを作成します。
   * コンストラク `com.adobe.idp.Document` ターを使用し、証明書を表すオブジェクトを渡して、オ `java.io.FileInputStream` ブジェクトを作成します。
   * オブジェクト `Recipient` のメソッドを呼び `setX509Cert` 出し、証明書を含 `com.adobe.idp.Document` むオブジェクトを渡します。 (さらに、オブジェクトに証 `Recipient`明書ソースとしてTruststore証明書エイリアスまたはLDAP URLを設定できます)。
   * コンストラクタ `CertificateEncryptionIdentity` ーを使用して、権限と証明書の情報を格納するオブジェクトを作成します。
   * オブジェクト `CertificateEncryptionIdentity` のメソッドを呼び `setPerms` 出し、権限情報を格納 `java.util.List` するオブジェクトを渡します。
   * オブジェクト `CertificateEncryptionIdentity` のメソッドを呼び `setRecipient` 出し、証明書情報を格納 `Recipient` するオブジェクトを渡します。
   * コンストラク `java.util.List` ターを使用して、証明書情報を格納するオブジェクトを作成します。
   * Invoke the `java.util.List` object’s add method and pass the `CertificateEncryptionIdentity` object. (このオ `java.util.List` ブジェクトは、メソッドにパラメーターとして渡 `encryptPDFUsingCertificates` されます)。

1. 暗号化の実行時オプションを設定します。

   * Create a `CertificateEncryptionOptionSpec` object by invoking its constructor.
   * オブジェクトのメソッドを呼び出し、暗号化するドキュメ `CertificateEncryptionOptionSpec` ントリソースを指 `setOption` 定する列 `CertificateEncryptionOption` 挙値を渡して、暗号化するPDFドキュメントリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定しま `CertificateEncryptionOption.ALL`す。
   * オブジェクトのメソッドを呼び出し、Acrobatの互換 `CertificateEncryptionOptionSpec` 性レベルを指 `setCompat` 定する列 `CertificateEncryptionCompatibility` 挙値を渡して、Acrobatの互換性オプションを指定します。 例えば、を指定できます `CertificateEncryptionCompatibility.ACRO_7`。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキ `EncryptionServiceClient` ュメントを証 `encryptPDFUsingCertificates` 明書で暗号化します。

   * 暗号化 `com.adobe.idp.Document` するPDFドキュメントを含むオブジェクトです。
   * 証明書 `java.util.List` 情報を格納するオブジェクトです。
   * 暗号化の `CertificateEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingCertificates` ッドは、証明書で暗 `com.adobe.idp.Document` 号化されたPDFドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingCertificates` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用した証明書によるPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した証明書によるPDFドキュメントの暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Encryption Client APIオブジェクトを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、証明書で暗号化されたPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 証明書を参照します。

   * コンストラクタを使用して `Recipient` オブジェクトを作成します。このオブジェクトには証明書情報が格納されます。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトには、PDFドキュメントを暗号化する証明書が格納されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、証明書のファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。
   * 証明書を保 `BLOB` 存するオブジェクトをオブジェクトのデー `Recipient` タメンバーに `x509Cert` 割り当てます。
   * コンストラク `CertificateEncryptionIdentity` ターを使用して、証明書情報を格納するオブジェクトを作成します。
   * 証明書を保 `Recipient` 存するオブジェクトを、オブジェクトの受 `CertificateEncryptionIdentity`信者データメンバーに割り当てます。
   * 配列を作 `Object` 成し、その配列の最 `CertificateEncryptionIdentity` 初の要素にオブジェクトを割り当て `Object` ます。 この配 `Object` 列は、メソッドにパラメーターとして渡さ `encryptPDFUsingCertificates` れます。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * オブジェクトのデータメンバーに列挙値を割り当てるこ `CertificateEncryptionOption` とで、暗号化するPDFドキュ `CertificateEncryptionOptionSpec` メントリソース `option` を指定します。 PDFドキュメント全体（メタデータと添付ファイルを含む）を暗号化するには、このデータメン `CertificateEncryptionOption.ALL` バーに割り当てます。
   * オブジェクトのデータメンバに列挙値を割り当て `CertificateEncryptionCompatibility` て、Acrobatの互換性オ `CertificateEncryptionOptionSpec` プションを `compat` 指定します。 例えば、このデータメ `CertificateEncryptionCompatibility.ACRO_7` ンバーに割り当てます。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキ `EncryptionServiceService` ュメントを証 `encryptPDFUsingCertificates` 明書で暗号化します。

   * 暗号化 `BLOB` するPDFドキュメントを含むオブジェクトです。
   * 証明書 `Object` 情報を格納する配列です。
   * 暗号化の `CertificateEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingCertificates` ッドは、証明書で暗 `BLOB` 号化されたPDFドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `encryptPDFUsingCertificates` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除 {#removing-certificate-based-encryption}

証明書ベースの暗号化をPDFドキュメントから削除して、ユーザーがAdobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。 証明書で暗号化されたPDFドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。 暗号化がPDFドキュメントから削除されると、そのドキュメントのセキュリティは失われます。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントから証明書ベースの暗号化を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. 暗号化を削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化されたPDFドキュメントの取得**

証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外がスローされます。 同様に、パスワードで暗号化されたドキュメントから証明書ベースの暗号化を削除しようとすると、例外が発生します。

**暗号化の削除**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。 暗号化されたPDFドキュメントから証明書ベースの暗号化を削除する場合、秘密鍵のエイリアス値が指定されます。 公開鍵について詳しくは、「PDFドキュメントの証明 [書による暗号化」を参照してください](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>秘密鍵はAEM Forms Trust storeに保存されます。 証明書をそこに配置すると、エイリアス値が指定されます。

**PDFドキュメントの保存**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 PDFドキュメントはAdobe readerまたはAcrobatで開くことができます。

**関連トピック**

[Java APIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[WebサービスAPIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラク `java.io.FileInputStream` ターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化を削除します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、PDFドキュメ `EncryptionServiceClient` ントから証明書ベ `removePDFCertificateSecurity` ースの暗号化を削除します。

   * 暗号化 `com.adobe.idp.Document` されたPDFドキュメントを含むオブジェクトです。
   * PDfドキュメントの暗号化に使用されるキーに対応する秘密鍵のエイリアス名を指定するstring値。
   このメソ `removePDFCertificateSecurity` ッドは、保護されてい `com.adobe.idp.Document` ないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. `com.adobe.idp.Document` メソッドから返された `removePDFCredentialSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用した証明書ベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-web-service-api}

Encryption API（Webサービス）を使用して証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。オブジェクト `BLOB` は、暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。

1. 暗号化を削除します。

   オブジェクト `EncryptionServiceClient` のメソッドを `removePDFCertificateSecurity` 呼び出し、次の値を渡します。

   * 暗号化 `BLOB` されたPDFドキュメントを表すファイルストリームデータを含むオブジェクトです。
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。
   このメソ `removePDFCredentialSecurity` ッドは、保護されてい `BLOB` ないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントを保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワードの暗号化の削除 {#removing-password-encryption}

パスワードベースの暗号化をPDFドキュメントから削除して、ユーザーがパスワードを指定しなくてもAdobe readerまたはAcrobatでPDFドキュメントを開くことができるようにすることができます。 パスワードベースの暗号化をPDFドキュメントから削除すると、ドキュメントのセキュリティは保護されなくなります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントからパスワードベースの暗号化を削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. パスワードを削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化されたPDFドキュメントの取得**

パスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外がスローされます。

**パスワードの削除**

暗号化されたPDFドキュメントからパスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントから暗号化を削除するために使用するマスターパスワードの両方が必要です。 パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワードは、暗号化の削除には使用できません。 PDFドキュメントがパスワードで暗号化されている場合、マスターパスワードが指定されます。 (PDFドキュメ [ントのパスワードによる暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。

**PDFドキュメントの保存**

EncryptionサービスでPDFドキュメントからパスワードベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、パスワードを指定せずに、Adobe readerまたはAcrobatでPDFドキュメントを開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. パスワードを削除します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、PDFドキュメ `EncryptionServiceClient` ントからパスワ `removePDFPasswordSecurity` ードベースの暗号化を削除します。

   * 暗号化 `com.adobe.idp.Document` されたPDFドキュメントを含むオブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるマスターパスワード値を指定するstring値です。
   このメソ `removePDFPasswordSecurity` ッドは、保護されてい `com.adobe.idp.Document` ないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. `Document` メソッドから返された `removePDFPasswordSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したパスワードベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### WebサービスAPIを使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-web-service-api}

Encryption API（Webサービス）を使用して、パスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。

1. パスワードを削除します。

   オブジェクト `EncryptionServiceService` のメソッドを `removePDFPasswordSecurity` 呼び出し、次の値を渡します。

   * 暗号化 `BLOB` されたPDFドキュメントを表すファイルストリームデータを含むオブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。
   このメソ `removePDFPasswordSecurity` ッドは、保護されてい `BLOB` ないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントを保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されていないPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化されたPDFドキュメントのロック解除 {#unlocking-encrypted-pdf-documents}

パスワードで暗号化されたPDFドキュメントまたは証明書で暗号化されたPDFドキュメントに対して別のAEM Forms操作を実行する前に、ロックを解除する必要があります。 暗号化されたPDFドキュメントに対して操作を実行しようとすると、例外が生成されます。 暗号化されたPDFドキュメントのロックを解除した後、そのドキュメントに対して1つ以上の操作を実行できます。 これらの操作は、Acrobat Reader DCエクステンションサービスなど、他のサービスに属する場合があります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

暗号化されたPDFドキュメントのロックを解除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. ドキュメントのロックを解除します。
1. AEM forms操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化されたPDFドキュメントの取得**

ロックを解除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントのロックを解除しようとすると、例外がスローされます。

**ドキュメントのロック解除**

パスワードで暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、パスワードで暗号化されたPDFドキュメントを開くために使用するパスワードの値の両方が必要です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。 (PDFドキュメ [ントのパスワードによる暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。

証明書で暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM forms操作の実行**

暗号化されたPDFドキュメントのロックが解除された後、そのドキュメントに対して別のサービス操作（使用権限の適用など）を実行できます。 この操作は、Acrobat Reader DC Extensionsサービスに属しています。

**関連トピック**

[Java APIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-java-api}

暗号化API(Java)を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラク `java.io.FileInputStream` ターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントのロックを解除します。

   オブジェクトまたはメソッドを呼び出して、暗号化されたPDF `EncryptionServiceClient` ドキュメントのロッ `unlockPDFUsingPassword` クを解除 `unlockPDFUsingCredential` します。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingPassword` し、次の値を渡します。

   * パスワ `com.adobe.idp.Document` ードで暗号化されたPDFドキュメントを含むオブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。
   証明書で暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingCredential` し、次の値を渡します。

   * A `com.adobe.idp.Document` object that contains the certificate-encrypted PDF document.
   * PDFドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値です。
   メソッド `unlockPDFUsingPassword` とメソ `unlockPDFUsingCredential` ッドは、両方とも、操作を実 `com.adobe.idp.Document` 行するために別のAEM Forms javaメソッドに渡すオブジェクトを返します。

1. AEM forms操作を実行します。

   ビジネス要件に合わせて、ロック解除されたPDFドキュメントに対してAEM forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合は、またはメソッドによって返されたオブジェクトをオ `com.adobe.idp.Document` ブジ `unlockPDFUsingPassword` ェクトのメ `unlockPDFUsingCredential` ソッドに渡 `ReaderExtensionsServiceClient``applyUsageRights` します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAPモード）を使用した暗号化されたPDFドキュメントのロック解除

[PDFドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

暗号化API（Webサービス）を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。

1. ドキュメントのロックを解除します。

   オブジェクトまたはメソッドを呼び出して、暗号化されたPDF `EncryptionServiceClient` ドキュメントのロッ `unlockPDFUsingPassword` クを解除 `unlockPDFUsingCredential` します。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingPassword` し、次の値を渡します。

   * パスワ `BLOB` ードで暗号化されたPDFドキュメントを含むオブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。
   証明書で暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingCredential` し、次の値を渡します。

   * A `BLOB` object that contains the certificate-encrypted PDF document.
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。
   メソッド `unlockPDFUsingPassword` とメ `unlockPDFUsingCredential` ソッドは、操作を実行する `com.adobe.idp.Document` ために別のAEM Formsメソッドに渡すオブジェクトを返します。

1. AEM forms操作を実行します。

   ビジネス要件に合わせて、ロック解除されたPDFドキュメントに対してAEM forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合、またはメソッドによって返されたオブジェクトをオブジェクトのメソッドに `BLOB``unlockPDFUsingPassword` 渡す必要 `unlockPDFUsingCredential` があ `ReaderExtensionsServiceClient``applyUsageRights` ります。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化の種類の決定 {#determining-encryption-type}

Java Encryption Service APIまたはWebサービスのEncryption Service APIを使用して、PDFドキュメントを保護する暗号化の種類をプログラムで判断できます。 PDFドキュメントが暗号化されているかどうか、および暗号化タイプが動的に判断する必要がある場合は、暗号化の種類を決定します。 例えば、PDFドキュメントをパスワードベースの暗号化またはRights Managementポリシーで保護するかどうかを指定できます。

PDFドキュメントは、次の暗号化タイプで保護できます。

* パスワードベースの暗号化
* 証明書ベースの暗号化
* Rights Managementサービスによって作成されるポリシー
* 別の種類の暗号化

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

PDFドキュメントを保護する暗号化の種類を決定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFドキュメントを取得します。
1. 暗号化タイプを決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**サービスクライアントの作成**

プログラムによってEncryptionサービス操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化されたPDFドキュメントの取得**

保護する暗号化の種類を判断するには、PDFドキュメントを取得する必要があります。

**暗号化の種類の決定**

PDFドキュメントを保護する暗号化の種類を指定できます。 PDFドキュメントが保護されていない場合、EncryptionサービスはPDFドキュメントが保護されていないことを通知します。

**関連トピック**

[Java APIを使用した暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[WebサービスAPIを使用した暗号化の種類の決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[ポリシーを使用したドキュメントの保護](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java APIを使用した暗号化タイプの決定 {#determine-the-encryption-type-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFドキュメントを取得します。

   * PDFドキュメ `java.io.FileInputStream` ントを表すオブジェクトを作成します。このオブジェクトは、コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことによって作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化タイプを決定します。

   * オブジェクトのメソッドを呼び出し、PDFドキュ `EncryptionServiceClient` メントを含むオ `getPDFEncryption` ブジェクトを渡すこ `com.adobe.idp.Document` とで、暗号化の種類を決定します。 このメソッドは、オブジェクトを `EncryptionTypeResult` 返します。
   * オブジェクト `EncryptionTypeResult` のメソッドを呼び出 `getEncryptionType` します。 このメソッドは、暗 `EncryptionType` 号化の種類を指定するenum値を返します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このメソッドはを返しま `EncryptionType.PASSWORD`す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した暗号化の種類の決定 {#determine-the-encryption-type-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/EncryptionService?WSDL`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てて、オ `BLOB` ブジェクトを `MTOM` 設定します。

1. 暗号化タイプを決定します。

   * オブジェクト `EncryptionServiceClient` のメソッドを呼び `getPDFEncryption` 出し、PDFドキュメ `BLOB` ントを含むオブジェクトを渡します。 このメソッドは、オブジェクトを `EncryptionTypeResult` 返します。
   * オブジェクトのデー `EncryptionTypeResult` タメソッドの値 `encryptionType` を取得します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このデータメンバーの値はです `EncryptionType.PASSWORD`。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)