---
title: PDFの暗号化と復号化のドキュメント
seo-title: PDFの暗号化と復号化のドキュメント
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

---


# PDFの暗号化と復号化のドキュメント {#encrypting-and-decrypting-pdf-documents}

**Encryption Serviceについて**

Encryptionサービスを使用すると、暗号化の暗号化と復号化をドキュメントできます。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryptionサービスを使用して、次のタスクを実行できます。

* PDFパスワードをドキュメントで暗号化します。 (PDFパスワ [ードのドキュメントの暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。
* 証明書を使用してPDFドキュメントを暗号化します。 (See [Encrypting PDF Documents with Certificates](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* PDFパスワードベースの暗号化を削除します。ドキュメント (Removing [Password Encryptionを参照](encrypting-decrypting-pdf-documents.md#removing-password-encryption))。
* 証明書ベースの暗号化をPDFドキュメントから削除 (証明書ベ [ースの暗号化の削除を参照](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption))。
* 他のサービス操作を実行できるようにPDFドキュメントのロックを解除します。 例えば、パスワードで暗号化されたPDFドキュメントのロックが解除された後、電子署名を適用できます。 (暗号化されたPDF [ドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)を参照)。
* 保護されたPDF暗号化の種類を指定します。ドキュメント (Determining [Encryption Typeを参照](encrypting-decrypting-pdf-documents.md#determining-encryption-type))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Encrypting PDF Documents with a Password {#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、PDFドキュメントへの電子署名など、別のAEM Forms操作をドキュメントで実行する前に、パスワードで暗号化されたPDFドキュメントのロックを解除する必要があります。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 AEM Formsリポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。 ( [Writing Resources](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFパスワードをドキュメントで暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryption Client APIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 暗号化の実行時オプションを設定します。
1. パ追加スワード。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

**Encryption Client APIオブジェクトの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。

**暗号化するPDFドキュメントの取得**

パスワードを使用して暗号化を行うには、ドキュメントが暗号化されていないPDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**暗号化の実行時オプションの設定**

PDFパスワードをドキュメントで暗号化するには、2つのパスワード値を含む4つの値を指定します。 最初のパスワード値はPDFドキュメントの暗号化に使用され、PDFパスワードを開くときに指定する必要があります。ドキュメント マスターパスワード値という2番目のパスワード値は、PDFパスワードの暗号化を削除するために使用されます。ドキュメント パスワードの値は大文字と小文字が区別され、これら2つのパスワード値を同じ値にすることはできません。

暗号化するPDFドキュメントリソースを指定する必要があります。 PDFドキュメント全体(ドキュメントのメタデータを除くすべて)またはドキュメントの添付ファイルのみを暗号化できます。 ドキュメントの添付ファイルのみを暗号化する場合、ユーザーが添付ファイルにアクセスしようとすると、パスワードの入力を求められます。

PDF暗号化を行う場合、ドキュメントが保護されているユーザーに関連付けられている権限をドキュメントできます。 権限を指定することで、パスワードで暗号化されたPDFユーザーが実行できるドキュメントを制御できます。 例えば、フォームデータを正しく抽出するには、次の権限を設定する必要があります。

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>権限は、 `PasswordEncryptionPermission` 定義済みリスト値です。

**追加パスワード**

保護されていないPDFドキュメントを取得し、暗号化の実行時の値を設定した後、PDFパスワードにパスワードを追加できます。ドキュメント

**暗号化されたPDFドキュメントをPDFファイルとして保存**

パスワードで暗号化されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[証明書によるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

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
   * オブジェクトのメソッドを呼び出し、暗号化する `PasswordEncryptionOptionSpec` ドキュメントリソー `setEncryptOption` スを指定する `PasswordEncryptionOption` 定義済みリスト値を渡して、ドキュメントするPDFリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定しま `PasswordEncryptionOption.ALL`す。
   * コンストラクター `java.util.List` を使用して、暗号化権限を格納するオブジェクトを作成 `ArrayList` します。
   * オブジェクトのメソッドを呼 `java.util.List` び出し、設 `add` 定する権限に対応する定義済みリスト値を渡して、権限を指定します。 例えば、PDFユーザーがPDFユーザー内のデータをコピーできる権限を設定するには、をドキュメントしま `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`す。 （設定する権限ごとに、この手順を繰り返します）。
   * オブジェクトのメソッドを呼び出し、Acrobat `PasswordEncryptionOptionSpec` の互換性レベ `setCompatability` ルを指定する定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 For example, you can specify `PasswordEncryptionCompatability.ACRO_7`.
   * オブジェクトのメソッドを呼び出し、オープンパスワードを表すstring値を渡すことで、暗号化さ `PasswordEncryptionOptionSpec` れたPDF `setDocumentOpenPassword` ドキュメントをユーザーが開くためのパスワード値を指定します。
   * マスターパスワード値を指定します。この値を使用すると、オブジェクトのメソッドを呼び出し、マスターパスワ `PasswordEncryptionOptionSpec` ードを表すstring値を `setPermissionPassword` 渡すことで、PDFドキュメントの暗号化を削除できます。

1. パ追加スワード。

   オブジェクトのドキュメントを呼び出し、次 `EncryptionServiceClient` の値を渡すこ `encryptPDFUsingPassword` とで、PDFメソッドを暗号化します。

   * パスワード `com.adobe.idp.Document` で暗号化するPDFドキュメントを含むオブジェクトです。
   * 暗号化の `PasswordEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingPassword` ッドは、パスワードで `com.adobe.idp.Document` 暗号化されたPDFメソッドを含むオブジェクトを返しますドキュメント。

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
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Encryption Client APIオブジェクトを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、パスワードで暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定します。こ `PasswordEncryptionOption` の場合、定義済みリスト値をオブジェクトのデ `PasswordEncryptionOptionSpec` ータメンバに割 `encryptOption` り当てます。 PDF全体（メタデータと添付ファイルを含む）を暗号化するには、このデータメン `PasswordEncryptionOption.ALL` バーに割り当てます。
   * オブジェクトのデータメンバーに `PasswordEncryptionCompatability` 定義済みリスト値を割り当てて、Acrobat `PasswordEncryptionOptionSpec` の互換性オプシ `compatability` ョンを指定します。 例えば、このデータメ `PasswordEncryptionCompatability.ACRO_7` ンバーに割り当てます。
   * オブジェクトのデータメンバーに開くドキュメントを表すstring値を割り当てて、暗号化されたPDFパスワードをユーザーが開くことができ `PasswordEncryptionOptionSpec` るパスワード値を指 `documentOpenPassword` 定します。
   * オブジェクトのデータメンバーにマスターパスワードを表すstring値を割り当てることで、PDFドキュメントの暗号化を削除できるようにする `PasswordEncryptionOptionSpec` パスワード値を指 `permissionPassword` 定します。

1. パ追加スワード。

   オブジェクトのドキュメントを呼び出し、次 `EncryptionServiceClient` の値を渡すこ `encryptPDFUsingPassword` とで、PDFメソッドを暗号化します。

   * パスワード `BLOB` で暗号化するPDFドキュメントを含むオブジェクトです。
   * 暗号化の `PasswordEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingPassword` ッドは、パスワードで `BLOB` 暗号化されたPDFメソッドを含むオブジェクトを返しますドキュメント。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクタ `System.IO.FileStream` ーを呼び出し、保護されたPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * メソッドによって返されたオブジェクトのデータ内容を `BLOB` 格納するバイト配列を作成 `encryptPDFUsingPassword` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Encrypting PDF Documents with Certificates {#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化を使用すると、公開鍵ドキュメントを使用して、特定の受信者の暗号化を行うことができます。 それぞれの受信者に、異なる権限を与えることができます。公開鍵によって、さまざまな暗号化を行うことができます。An algorithm is used to generate two large numbers, known as *keys*, that have the following properties:

* 鍵のうち 1 つは、一連のデータを暗号化するために使用されます。その後、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう片方の鍵と区別することは不可能です。

キーの1つは、ユーザーの秘密鍵として機能します。 そのユーザーのみがこの鍵にアクセスできることが重要です。もう1つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードすると、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 AEM Formsリポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。 ( [Writing Resources](/help/forms/developing/aem-forms-repository.md#writing-resources))。

>[!NOTE]
>
>PDF証明書を証明書で暗号化する前に、ドキュメントをAEM Formsに追加する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムによって追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDF証明書を暗号化するドキュメントを証明書で暗号化するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Encryption Client APIオブジェクトを作成します。
1. 暗号化するPDFドキュメントを取得します。
1. 証明書を参照します。
1. 暗号化の実行時オプションを設定します。
1. 証明書で暗号化されたPDFドキュメントの作成
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**Encryption Client APIオブジェクトの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用する場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**暗号化するPDFドキュメントの取得**

暗号化する非暗号化PDFドキュメントを取得する必要があります。 既に暗号化されているPDFドキュメントを保護しようとすると、例外が発生します。

**証明書の参照**

PDFドキュメントを証明書で暗号化するには、PDF暗号化の暗号化に使用される証明書を参照します。ドキュメント 証明書は.cerファイル、.crtファイル、または.pemファイルです。 PKCS#12ファイルは、対応する証明書と共に秘密鍵を保存するために使用されます。

証明書を使用してPDFドキュメントを暗号化する場合は、保護された認証に関連付けられている権限をドキュメントします。 権限を指定することで、証明書で暗号化されたPDFユーザーが実行できるアクションをドキュメントできます。

**暗号化の実行時オプションの設定**

暗号化するPDFドキュメントリソースを指定します。 PDFドキュメント全体(ドキュメントのメタデータを除くすべて)またはドキュメントの添付ファイルのみを暗号化できます。

**証明書で暗号化されたPDFの作成ドキュメント**

セキュリティで保護されていないPDFドキュメントを取得し、証明書を参照し、実行時のオプションを設定したら、証明書で暗号化されたPDFドキュメントを作成できます。 PDFドキュメントが暗号化されたら、対応する公開鍵を使用して復号化する必要があります。

**暗号化されたPDFドキュメントをPDFファイルとして保存**

暗号化されたPDFファイルをPDFドキュメントとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの証明書による暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントを証明書で暗号化する](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードによるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したPDFドキュメントの証明書による暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

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
   * オブジェクトのメソッドを呼び出し、保護されたPDFドキュメントを開く定義済みリストに付与された権限を表す `java.util.List``add``CertificateEncryptionPermissions` ドキュメント値を渡して、暗号化されたユーザーに関連付けられた権限を指定します。 例えば、すべての権限を指定するには、を渡しま `CertificateEncryptionPermissions.PKI_ALL_PERM`す。
   * コンストラクタを使用して `Recipient` オブジェクトを作成します。
   * PDFドキュメントの `java.io.FileInputStream` コンストラクターを使用し、証明書の場所を指定するstring値を渡すことで、PDFの暗号化に使用される証明書を表すオブジェクトを作成します。
   * コンストラク `com.adobe.idp.Document` ターを使用し、証明書を表すオブジェクトを渡 `java.io.FileInputStream` して、オブジェクトを作成します。
   * オブジェクト `Recipient` のメソッドを呼 `setX509Cert` び出し、証明書を含 `com.adobe.idp.Document` むオブジェクトを渡します。 (また、オブジェクトには、証 `Recipient`明書ソースとしてTruststore証明書エイリアスまたはLDAP URLを含めることができます)。
   * コンストラクタ `CertificateEncryptionIdentity` ーを使用して、権限と証明書の情報を格納するオブジェクトを作成します。
   * オブジェクト `CertificateEncryptionIdentity` のメソッドを呼 `setPerms` び出し、権限情報を格納 `java.util.List` するオブジェクトを渡します。
   * オブジェクト `CertificateEncryptionIdentity` のメソッドを呼 `setRecipient` び出し、証明書情報を格納 `Recipient` するオブジェクトを渡します。
   * コンストラクタ `java.util.List` ーを使用して、証明書情報を格納するオブジェクトを作成します。
   * Invoke the `java.util.List` object’s add method and pass the `CertificateEncryptionIdentity` object. (このオ `java.util.List` ブジェクトは、メソッドにパラメーターとして渡 `encryptPDFUsingCertificates` されます)。

1. 暗号化の実行時オプションを設定します。

   * Create a `CertificateEncryptionOptionSpec` object by invoking its constructor.
   * オブジェクトのメソッドを呼び出し、暗号化する `CertificateEncryptionOptionSpec` ドキュメントリソー `setOption` スを指定する `CertificateEncryptionOption` 定義済みリスト値を渡して、ドキュメントするPDFリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化する場合は、を指定しま `CertificateEncryptionOption.ALL`す。
   * オブジェクトのメソッドを呼び出し、Acrobat `CertificateEncryptionOptionSpec` の互換性レベ `setCompat` ルを指定する `CertificateEncryptionCompatibility` 定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 For example, you can specify `CertificateEncryptionCompatibility.ACRO_7`.

1. 証明書で暗号化されたPDFドキュメントの作成

   オブジェクトのドキュメントを呼び出し、次の `EncryptionServiceClient` 値を渡すことで、PDF `encryptPDFUsingCertificates` メソッドを証明書で暗号化します。

   * 暗号化 `com.adobe.idp.Document` するPDFドキュメントを含むオブジェクト。
   * 証明書 `java.util.List` 情報を格納するオブジェクトです。
   * 暗号化の `CertificateEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingCertificates` ッドは、証明書で暗 `com.adobe.idp.Document` 号化されたPDFメソッドを含むオブジェクトを返します。ドキュメント

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingCertificates` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの証明書による暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してPDFドキュメントを証明書で暗号化する {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Encryption Client APIオブジェクトを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、証明書で暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` にバイト配列の内容を割り `MTOM` 当てて、オブジェクトを設定します。

1. 証明書を参照します。

   * コンストラクタを使用して `Recipient` オブジェクトを作成します。このオブジェクトには、証明書情報が格納されます。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトには、PDF暗号化を暗号化する証明書が格納されます。ドキュメント
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、証明書のファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。
   * 証明書を保 `BLOB` 存するオブジェクトをオブジェクトのデ `Recipient` ータメンバーに割 `x509Cert` り当てます。
   * コンストラクタ `CertificateEncryptionIdentity` ーを使用して、証明書情報を格納するオブジェクトを作成します。
   * 証明書を保 `Recipient` 存するオブジェクトをオブジェクトの `CertificateEncryptionIdentity`受信者データメンバに割り当てます。
   * 配列を作成 `Object` し、その配列の最 `CertificateEncryptionIdentity` 初の要素にオブジェクトを割り当て `Object` ます。 この配 `Object` 列は、メソッドにパラメーターとして渡さ `encryptPDFUsingCertificates` れます。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定します。こ `CertificateEncryptionOption` の場合、定義済みリスト値をオブジェクトのデ `CertificateEncryptionOptionSpec` ータメンバに割 `option` り当てます。 メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、このデータメン `CertificateEncryptionOption.ALL` バーに割り当てます。
   * オブジェクトのデータメンバーに `CertificateEncryptionCompatibility` 定義済みリスト値を割り当てて、Acrobat `CertificateEncryptionOptionSpec` の互換性オプシ `compat` ョンを指定します。 例えば、このデータメ `CertificateEncryptionCompatibility.ACRO_7` ンバーに割り当てます。

1. 証明書で暗号化されたPDFドキュメントの作成

   オブジェクトのドキュメントを呼び出し、次の `EncryptionServiceService` 値を渡すことで、PDF `encryptPDFUsingCertificates` メソッドを証明書で暗号化します。

   * 暗号化 `BLOB` するPDFドキュメントを含むオブジェクト。
   * 証明書 `Object` 情報を格納する配列です。
   * 暗号化の `CertificateEncryptionOptionSpec` 実行時オプションを含むオブジェクトです。
   このメソ `encryptPDFUsingCertificates` ッドは、証明書で暗 `BLOB` 号化されたPDFメソッドを含むオブジェクトを返します。ドキュメント

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクタ `System.IO.FileStream` ーを呼び出し、保護されたPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * メソッドによって返されたオブジェクトのデータ内容を `BLOB` 格納するバイト配列を作成 `encryptPDFUsingCertificates` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `binaryData` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除 {#removing-certificate-based-encryption}

証明書ベースの暗号化をPDFドキュメントから削除して、ユーザーがAdobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。 証明書で暗号化されたPDFドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。 暗号化がPDF暗号化から削除されると、ドキュメントは保護されなくなります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

証明書ベースの暗号化をPDFドキュメントから削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFの取得ドキュメント。
1. 暗号化を削除します。
1. PDFファイルとしてPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用する場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**「Get the encrypted PDF」ドキュメント**

証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDF暗号化を削除しようとすると、ドキュメントが発生します。 同様に、パスワードで暗号化されたパスワードから証明書ベースの暗号化を削除しようとすると、ドキュメントが発生します。

**暗号化の削除**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。 秘密鍵のエイリアス値は、暗号化されたPDF暗号化から証明書ベースの暗号化を削除するときに指定されます。ドキュメント 公開鍵について詳しくは、証明書を使用したPDF [ドキュメントの暗号化を参照してください](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>秘密鍵はAEM Forms Trust Storeに保存されます。 証明書が配置されると、エイリアス値が指定されます。

**「Save the PDF」ドキュメント**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。

**関連トピック**

[Java APIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[WebサービスAPIを使用した証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した証明書ベースの暗号化の削除 {#remove-certificate-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクター `java.io.FileInputStream` を使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化を削除します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、PDFドキュメント `EncryptionServiceClient` から証明書ベ `removePDFCertificateSecurity` ースの暗号化を削除します。

   * 暗号化さ `com.adobe.idp.Document` れたPDFドキュメントを含むオブジェクト。
   * PDf暗号化に使用されるキーに対応する秘密鍵のエイリアス名を指定するstring値です。ドキュメント
   このメソッ `removePDFCertificateSecurity` ドは、保護されて `com.adobe.idp.Document` いないPDFオブジェクトを含むドキュメントを返します。

1. 「PDF」ドキュメントを保存

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
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。オブジェクト `BLOB` は、暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。

1. 暗号化を削除します。

   オブジェクト `EncryptionServiceClient` のメソッドを `removePDFCertificateSecurity` 呼び出し、次の値を渡します。

   * 暗号化 `BLOB` されたPDFデータを表すファイルストリームデータを含むオブジェクトです。ドキュメント。
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値です。
   このメソッ `removePDFCredentialSecurity` ドは、保護されて `BLOB` いないPDFオブジェクトを含むドキュメントを返します。

1. 「PDF」ドキュメントを保存

   * コンストラクタ `System.IO.FileStream` ーを呼び出し、保護されていないPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワードの暗号化の削除 {#removing-password-encryption}

パスワードベースの暗号化をPDFドキュメントから削除して、パスワードを指定しなくてもAdobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。 パスワードベースの暗号化をPDFドキュメントから削除すると、ドキュメントのセキュリティが低下します。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

パスワードベースの暗号化をPDFドキュメントから削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFの取得ドキュメント。
1. パスワードを削除します。
1. PDFファイルとしてPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用する場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**「Get the encrypted PDF」ドキュメント**

パスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDF暗号化を削除しようとすると、ドキュメントが発生します。

**パスワードの削除**

暗号化されたPDFドキュメントからパスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントから暗号化を削除するために使用されるマスターパスワードの両方が必要です。 パスワードで暗号化されたPDFパスワードを開くために使用されるドキュメントは、暗号化の削除には使用できません。 PDFパスワードがパスワードで暗号化されている場合、マスタードキュメントが指定されます。 (PDFパスワ [ードのドキュメントの暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。

**「Save the PDF」ドキュメント**

EncryptionサービスでPDFドキュメントからパスワードベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、パスワードを指定しなくても、PDFドキュメントをAdobe ReaderまたはAcrobatで開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードによるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクター `java.io.FileInputStream` を使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. パスワードを削除します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、PDFドキュメント `EncryptionServiceClient` からパスワードベ `removePDFPasswordSecurity` ースの暗号化を削除します。

   * 暗号化さ `com.adobe.idp.Document` れたPDFドキュメントを含むオブジェクト。
   * PDFパスワードから暗号化を削除するために使用されるマスターパスワード値を指定するstringドキュメント。
   このメソッ `removePDFPasswordSecurity` ドは、保護されて `com.adobe.idp.Document` いないPDFオブジェクトを含むドキュメントを返します。

1. 「PDF」ドキュメントを保存

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
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、パスワードで暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。

1. パスワードを削除します。

   オブジェクト `EncryptionServiceService` のメソッドを `removePDFPasswordSecurity` 呼び出し、次の値を渡します。

   * 暗号化 `BLOB` されたPDFデータを表すファイルストリームデータを含むオブジェクトです。ドキュメント。
   * PDFパスワードから暗号化を削除するために使用されるパスワード値を指定するstringドキュメント。 この値は、PDFパスワードを暗号化する際にドキュメントを指定します。
   このメソッ `removePDFPasswordSecurity` ドは、保護されて `BLOB` いないPDFオブジェクトを含むドキュメントを返します。

1. 「PDF」ドキュメントを保存

   * コンストラクタ `System.IO.FileStream` ーを呼び出し、保護されていないPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `removePDFPasswordSecurity` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化されたPDFのロック解除ドキュメント {#unlocking-encrypted-pdf-documents}

パスワードで暗号化されたPDFドキュメントまたは証明書で暗号化されたPDFパスワードは、ロック解除してから、別のAEM Forms操作を実行する必要があります。 暗号化されたPDFドキュメントに対して操作を実行しようとすると、例外が生成されます。 暗号化されたPDFドキュメントのロックを解除した後、1つ以上の操作を実行できます。 これらの操作は、Acrobat Reader DCエクステンションサービスなど、他のサービスに属する場合があります。

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

暗号化されたPDFのロックを解除するには、ドキュメントを次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFの取得ドキュメント。
1. ロックを解除します。ドキュメント
1. AEM Forms操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用する場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**「Get the encrypted PDF」ドキュメント**

ロックを解除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントのロックを解除しようとすると、例外が発生します。

**ロック解除のドキュメント**

パスワードで暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、パスワードで暗号化されたPDFドキュメントを開くために使用するパスワードの両方が必要です。 この値は、PDFパスワードを暗号化する際にドキュメントを指定します。 (PDFパスワ [ードのドキュメントの暗号化を参照](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password))。

証明書で暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM Forms操作の実行**

暗号化されたPDFドキュメントのロックが解除されたら、別のサービス操作（使用権限の適用など）を実行できます。 この操作は、Acrobat Reader DC Extensionsサービスに属しています。

**関連トピック**

[Java APIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java APIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-java-api}

暗号化API(Java)を使用して、暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクター `java.io.FileInputStream` を使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ロックを解除します。ドキュメント

   オブジェクトまたはドキュメントを呼び出して、暗号 `EncryptionServiceClient` 化されたPDFメソッドをロ `unlockPDFUsingPassword` ック解除 `unlockPDFUsingCredential` します。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingPassword` し、次の値を渡します。

   * パスワ `com.adobe.idp.Document` ードで暗号化されたPDFパスワードを含むドキュメント。
   * パスワードで暗号化されたPDFパスワードを開くために使用されるパスワード値を指定するstring値ドキュメント。 この値は、PDFパスワードを暗号化する際にドキュメントを指定します。
   証明書で暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingCredential` し、次の値を渡します。

   * A `com.adobe.idp.Document` object that contains the certificate-encrypted PDF document.
   * PDF暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値です。ドキュメント
   メソッド `unlockPDFUsingPassword` とメ `unlockPDFUsingCredential` ソッドはどちらも、操 `com.adobe.idp.Document` 作を実行するために別のAEM Forms Javaメソッドに渡すオブジェクトを返します。

1. AEM Forms操作を実行します。

   ビジネス要件に合わせて、ロック解除されたPDFドキュメントでAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合、またはメソッドによって返されたオ `com.adobe.idp.Document` ブジェクトをオ `unlockPDFUsingPassword` ブジェ `unlockPDFUsingCredential` クトのメ `ReaderExtensionsServiceClient` ソッ `applyUsageRights` ドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAPモード）を使用した暗号化されたPDFドキュメントのロック解除

[使用権限のPDFドキュメント](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Encryption API（Webサービス）を使用して、暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 暗号化サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。

1. ロックを解除します。ドキュメント

   オブジェクトまたはドキュメントを呼び出して、暗号 `EncryptionServiceClient` 化されたPDFメソッドをロ `unlockPDFUsingPassword` ック解除 `unlockPDFUsingCredential` します。

   パスワードで暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingPassword` し、次の値を渡します。

   * パスワ `BLOB` ードで暗号化されたPDFパスワードを含むドキュメント。
   * パスワードで暗号化されたPDFパスワードを開くために使用されるパスワード値を指定するstring値ドキュメント。 この値は、PDFパスワードを暗号化する際にドキュメントを指定します。
   証明書で暗号化されたPDFドキュメントのロックを解除するには、このメソッドを呼び出 `unlockPDFUsingCredential` し、次の値を渡します。

   * A `BLOB` object that contains the certificate-encrypted PDF document.
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値です。
   メソッド `unlockPDFUsingPassword` とメ `unlockPDFUsingCredential` ソッドはどちらも、操 `com.adobe.idp.Document` 作を実行するために別のAEM Formsメソッドに渡すオブジェクトを返します。

1. AEM Forms操作を実行します。

   ビジネス要件に合わせて、ロック解除されたPDFドキュメントでAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合、またはメソッドによって返されたオブジェクトをオブジ `BLOB` ェ `unlockPDFUsingPassword` クトのメ `unlockPDFUsingCredential` ソッドに渡し `ReaderExtensionsServiceClient``applyUsageRights` ます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化の種類の決定 {#determining-encryption-type}

Java Encryption Service APIまたはWebサービスのEncryption Service APIを使用して、PDFドキュメントを保護する暗号化の種類をプログラムで判断できます。 PDF暗号化が暗号化されているかどうか、および暗号化タイプがドキュメントされている場合は、動的に判断する必要がある場合があります。 例えば、PDFドキュメントをパスワードベースの暗号化またはRights Managementポリシーで保護するかどうかを指定できます。

A PDF document can be protected by the following encryption types:

* Password-based encryption
* Certificate-based encryption
* Rights Managementサービスによって作成されるポリシー
* 別の種類の暗号化

>[!NOTE]
>
>For more information about the Encryption service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

PDF暗号化を保護する暗号化の種類を決定するには、次のドキュメントを実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化されたPDFの取得ドキュメント。
1. 暗号化の種類を決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

**サービスクライアントの作成**

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用する場合は、オブジェクトを作成し `EncrytionServiceClient` ます。 WebサービスのEncryption Service APIを使用している場合は、オブジェクトを作成 `EncryptionServiceService` します。

**「Get the encrypted PDF」ドキュメント**

保護する暗号化の種類を判断するには、PDFドキュメントを取得する必要があります。

**暗号化の種類の決定**

PDF暗号化を保護する暗号化の種類を指定できます。ドキュメント If the PDF document is not protected, then the Encryption service informs you that the PDF document is not secured.

**関連トピック**

[Java APIを使用した暗号化の種類の決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[WebサービスAPIを使用して暗号化の種類を判断する](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service APIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[ポリシーでドキュメントを保護する](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java APIを使用した暗号化の種類の決定 {#determine-the-encryption-type-using-the-java-api}

Encryption API(Java)を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `EncryptionServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントーの場所を指定するstring値を渡して、PDFドキュメントーを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の種類を決定します。

   * オブジェクトのメソッドを呼び出し、PDF `EncryptionServiceClient` メソッドを `getPDFEncryption` 含むオブジェクトを渡すこ `com.adobe.idp.Document` とで、暗号化の種類をドキュメントします。 このメソッドは、オブジェクトを `EncryptionTypeResult` 返します。
   * オブジェクトの `EncryptionTypeResult` メソッドを呼び出 `getEncryptionType` します。 このメソッドは、暗号 `EncryptionType` 化の種類を指定する列挙値を返します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このメソッドはを返しま `EncryptionType.PASSWORD`す。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用して暗号化の種類を判断する {#determine-the-encryption-type-using-the-web-service-api}

Encryption API（Webサービス）を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. サービスクライアントを作成します。

   * デフォルトのコンス `EncryptionServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `EncryptionServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/EncryptionService?WSDL`.)に渡します。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `EncryptionServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `EncryptionServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 暗号化されたPDFの取得ドキュメント。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` のデータメンバーにバイト配列の内容を割り当てること `BLOB` で、オブジェクトを `MTOM` 設定します。

1. 暗号化の種類を決定します。

   * Invoke the `EncryptionServiceClient` object’s `getPDFEncryption` method and pass the `BLOB` object that contains the PDF document. このメソッドは、オブジェクトを `EncryptionTypeResult` 返します。
   * Get the value of the `EncryptionTypeResult` object’s `encryptionType` data method. For example, if the PDF document is protected with password-based encryption, the value of this data member is `EncryptionType.PASSWORD`.

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)