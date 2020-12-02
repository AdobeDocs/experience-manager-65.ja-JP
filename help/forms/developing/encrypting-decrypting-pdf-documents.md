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


# PDFドキュメントの暗号化と復号化{#encrypting-and-decrypting-pdf-documents}

**Encryptionサービスについて**

Encryptionサービスを使用すると、ドキュメントの暗号化および復号化を行うことができます。 ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

Encryptionサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをパスワードで暗号化します。 (「[パスワードによるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。
* PDFドキュメントを証明書で暗号化します。 (「[証明書によるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)」を参照)。
* PDFドキュメントからパスワードベースの暗号化を削除します。 （「[パスワード暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-password-encryption)」を参照）。
* PDFドキュメントから証明書ベースの暗号化を削除します。 （「[証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)」を参照）。
* 他のサービス操作を実行できるように、PDFドキュメントのロックを解除します。 例えば、パスワードで暗号化されたPDFドキュメントのロックが解除された後に、電子署名を適用できます。 ([暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)を参照)。
* 保護されたPDFドキュメントの暗号化タイプを指定します。 （「[暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determining-encryption-type)」を参照）。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## PDFドキュメントのパスワードによる暗号化{#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、PDFドキュメントのデジタル署名など、別のAEM Forms操作をドキュメントで実行する前に、パスワードで暗号化されたPDFドキュメントをロック解除する必要があります。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードする場合、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、暗号化を行わないことをお勧めします。 （[リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources)を参照）。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

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
>権限は`PasswordEncryptionPermission`定義済みリスト値として指定します。

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

### Java API {#encrypt-a-pdf-document-using-the-java-api}を使用してPDFドキュメントを暗号化する

Encryption API(Java)を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化クライアントAPIの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクターを呼び出して、`PasswordEncryptionOptionSpec`オブジェクトを作成します。
   * `PasswordEncryptionOptionSpec`オブジェクトの`setEncryptOption`メソッドを呼び出し、暗号化するドキュメントリソースを指定する`PasswordEncryptionOption`定義済みリスト値を渡して、暗号化するPDFドキュメントリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、`PasswordEncryptionOption.ALL`を指定します。
   * `ArrayList`コンストラクターを使用して、暗号化の権限を格納する`java.util.List`オブジェクトを作成します。
   * `java.util.List`オブジェクト&#39;s `add`メソッドを呼び出し、設定する権限に対応する定義済みリスト値を渡して、権限を指定します。 例えば、PDFドキュメント内のデータをユーザーがコピーできる権限を設定するには、`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`を指定します。 （設定する権限ごとに、この手順を繰り返します）。
   * `PasswordEncryptionOptionSpec`オブジェクトの`setCompatability`メソッドを呼び出し、Acrobatの互換性レベルを指定する定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 例えば、`PasswordEncryptionCompatability.ACRO_7`を指定できます。
   * ユーザーが暗号化されたPDFドキュメントを開くために、`PasswordEncryptionOptionSpec`オブジェクトの`setDocumentOpenPassword`メソッドを呼び出し、開くパスワードを表すstring値を渡すパスワード値を指定します。
   * マスターパスワード値を指定します。この値を指定すると、ユーザーが`PasswordEncryptionOptionSpec`オブジェクトの`setPermissionPassword`メソッドを呼び出し、マスターパスワードを表す文字列値を渡すことで、PDFドキュメントから暗号化を削除できます。

1. 追加パスワード。

   `EncryptionServiceClient`オブジェクトの`encryptPDFUsingPassword`メソッドを呼び出し、次の値を渡して、PDFドキュメントを暗号化します。

   * パスワードを使用して暗号化するPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
   * 暗号化の実行時オプションを含む`PasswordEncryptionOptionSpec`オブジェクトです。

   `encryptPDFUsingPassword`メソッドは、パスワードで暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。 `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingPassword` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#encrypting-a-pdf-document-using-the-web-service-api}を使用したPDFドキュメントの暗号化

Encryption API（Webサービス）を使用して、PDFドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定するには、`PasswordEncryptionOption`定義済みリスト値を`PasswordEncryptionOptionSpec`オブジェクトの`encryptOption`データメンバに割り当てます。 PDF全体（メタデータと添付ファイルを含む）を暗号化するには、このデータメンバーに`PasswordEncryptionOption.ALL`を割り当てます。
   * `PasswordEncryptionCompatability`定義済みリスト値を`PasswordEncryptionOptionSpec`オブジェクトの`compatability`データメンバに割り当てて、Acrobat互換性オプションを指定します。 例えば、`PasswordEncryptionCompatability.ACRO_7`をこのデータメンバーに割り当てます。
   * 暗号化されたPDFドキュメントをユーザーが開くためのpassword値を指定します。この値は、開いたパスワードを表すstring値を`PasswordEncryptionOptionSpec`オブジェクトの`documentOpenPassword`データメンバーに割り当てることによって指定します。
   * ユーザーがマスターパスワードを表す文字列値を`PasswordEncryptionOptionSpec`オブジェクトの`permissionPassword`データメンバーに割り当てることで、PDFドキュメントから暗号化を削除できるように、password値を指定します。

1. 追加パスワード。

   `EncryptionServiceClient`オブジェクトの`encryptPDFUsingPassword`メソッドを呼び出し、次の値を渡して、PDFドキュメントを暗号化します。

   * パスワードを使用して暗号化するPDFドキュメントが含まれる`BLOB`オブジェクトです。
   * 暗号化の実行時オプションを含む`PasswordEncryptionOptionSpec`オブジェクトです。

   `encryptPDFUsingPassword`メソッドは、パスワードで暗号化されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、保護されたPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `encryptPDFUsingPassword`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの証明書による暗号化{#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化を使用すると、公開鍵による暗号化を使用して、特定の受信者用のドキュメントを暗号化できます。 それぞれの受信者に、異なる権限を与えることができます。公開鍵によって、さまざまな暗号化を行うことができます。アルゴリズムは、*keys*&#x200B;と呼ばれる、次のプロパティを持つ2つの大きな数値を生成するために使用します。

* 鍵のうち 1 つは、一連のデータを暗号化するために使用されます。その後、他のキーのみを使用してデータを復号化できます。
* 1 つの鍵を、もう片方の鍵と区別することは不可能です。

鍵の1つは、ユーザーの秘密鍵として機能します。 そのユーザーのみがこの鍵にアクセスできることが重要です。もう1つのキーはユーザーの公開鍵で、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。 証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化されたPDFドキュメントをAEM Formsリポジトリにアップロードする場合、PDFドキュメントを復号化してXDPコンテンツを抽出することはできません。 ドキュメントをAEM Formsリポジトリにアップロードする前に、暗号化を行わないことをお勧めします。 （[リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources)を参照）。

>[!NOTE]
>
>PDFドキュメントを証明書で暗号化する前に、証明書をAEM Formsに追加しておく必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 （「[Trust Manager APIを使用した秘密鍵証明書の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)」を参照）。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

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

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、`EncrytionServiceClient`オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、`EncryptionServiceService`オブジェクトを作成します。

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

### Java API {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}を使用して、PDFドキュメントを証明書で暗号化します。

Encryption API(Java)を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 証明書を参照します。

   * コンストラクタを使用して、権限情報を格納する`java.util.List`オブジェクトを作成します。
   * `java.util.List`オブジェクトの`add`メソッドを呼び出し、保護されたPDFドキュメントを開くユーザーに許可する権限を表す`CertificateEncryptionPermissions`定義済みリスト値を渡して、暗号化されたドキュメントに関連付けられた権限を指定します。 例えば、すべての権限を指定するには、`CertificateEncryptionPermissions.PKI_ALL_PERM`を渡します。
   * コンストラクタを使用して `Recipient` オブジェクトを作成します。
   * PDFドキュメントのコンストラクターを使用し、証明書の場所を指定する文字列値を渡して、PDFの暗号化に使用される証明書を表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクターを使用し、証明書を表す`java.io.FileInputStream`オブジェクトを渡して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `Recipient`オブジェクトの`setX509Cert`メソッドを呼び出し、証明書を含む`com.adobe.idp.Document`オブジェクトを渡します。 （さらに、`Recipient`オブジェクトには、Truststore証明書エイリアスまたはLDAP URLを証明書ソースとして指定できます）。
   * コンストラクターを使用して、権限と証明書情報を格納する`CertificateEncryptionIdentity`オブジェクトを作成します。
   * `CertificateEncryptionIdentity`オブジェクトの`setPerms`メソッドを呼び出し、権限情報を格納する`java.util.List`オブジェクトを渡します。
   * `CertificateEncryptionIdentity`オブジェクトの`setRecipient`メソッドを呼び出し、証明書情報を格納する`Recipient`オブジェクトを渡します。
   * 証明書情報を格納する`java.util.List`オブジェクトを作成します。このオブジェクトは、コンストラクターを使用して作成します。
   * `java.util.List`オブジェクトのaddメソッドを呼び出し、`CertificateEncryptionIdentity`オブジェクトを渡します。 （この`java.util.List`オブジェクトは、`encryptPDFUsingCertificates`メソッドにパラメーターとして渡されます）。

1. 暗号化の実行時オプションを設定します。

   * コンストラクターを呼び出して、`CertificateEncryptionOptionSpec`オブジェクトを作成します。
   * `CertificateEncryptionOptionSpec`オブジェクトの`setOption`メソッドを呼び出し、暗号化するドキュメントリソースを指定する`CertificateEncryptionOption`定義済みリスト値を渡して、暗号化するPDFドキュメントリソースを指定します。 例えば、メタデータと添付ファイルを含むPDFドキュメント全体を暗号化するには、`CertificateEncryptionOption.ALL`を指定します。
   * `CertificateEncryptionOptionSpec`オブジェクトの`setCompat`メソッドを呼び出し、Acrobatの互換性レベルを指定する`CertificateEncryptionCompatibility`定義済みリスト値を渡して、Acrobatの互換性オプションを指定します。 例えば、`CertificateEncryptionCompatibility.ACRO_7`を指定できます。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   `EncryptionServiceClient`オブジェクトの`encryptPDFUsingCertificates`メソッドを呼び出し、次の値を渡して、PDFドキュメントを証明書で暗号化します。

   * 暗号化するPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
   * 証明書情報を格納する`java.util.List`オブジェクトです。
   * 暗号化の実行時オプションを含む`CertificateEncryptionOptionSpec`オブジェクトです。

   `encryptPDFUsingCertificates`メソッドは、証明書で暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。 `com.adobe.idp.Document` メソッドから返された `encryptPDFUsingCertificates` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した証明書によるPDFドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}を使用して、PDFドキュメントを証明書で暗号化します

Encryption API（Webサービス）を使用して、PDFドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 暗号化クライアントAPIオブジェクトを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、証明書で暗号化されたPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. 証明書を参照します。

   * コンストラクタを使用して `Recipient` オブジェクトを作成します。このオブジェクトは、証明書情報を格納します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトには、PDFドキュメントを暗号化する証明書が格納されます。
   * コンストラクターを呼び出し、証明書のファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。
   * 証明書を保存する`BLOB`オブジェクトを`Recipient`オブジェクトの`x509Cert`データメンバに割り当てます。
   * 証明書情報を格納する`CertificateEncryptionIdentity`オブジェクトを作成します。このオブジェクトは、コンストラクターを使用して作成します。
   * 証明書を保存する`Recipient`オブジェクトを`CertificateEncryptionIdentity`オブジェクトの受信者データメンバに割り当てます。
   * `Object`配列を作成し、`CertificateEncryptionIdentity`オブジェクトを`Object`配列の最初の要素に割り当てます。 この`Object`配列は、`encryptPDFUsingCertificates`メソッドにパラメーターとして渡されます。

1. 暗号化の実行時オプションを設定します。

   * コンストラクタを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * 暗号化するPDFドキュメントリソースを指定するには、`CertificateEncryptionOption`定義済みリスト値を`CertificateEncryptionOptionSpec`オブジェクトの`option`データメンバに割り当てます。 PDFドキュメント全体（メタデータと添付ファイルを含む）を暗号化するには、`CertificateEncryptionOption.ALL`をこのデータメンバーに割り当てます。
   * `CertificateEncryptionCompatibility`定義済みリスト値を`CertificateEncryptionOptionSpec`オブジェクトの`compat`データメンバに割り当てて、Acrobat互換性オプションを指定します。 例えば、`CertificateEncryptionCompatibility.ACRO_7`をこのデータメンバーに割り当てます。

1. 証明書で暗号化されたPDFドキュメントを作成します。

   `EncryptionServiceService`オブジェクトの`encryptPDFUsingCertificates`メソッドを呼び出し、次の値を渡して、PDFドキュメントを証明書で暗号化します。

   * 暗号化するPDFドキュメントが含まれる`BLOB`オブジェクトです。
   * 証明書情報を格納する`Object`配列。
   * 暗号化の実行時オプションを含む`CertificateEncryptionOptionSpec`オブジェクトです。

   `encryptPDFUsingCertificates`メソッドは、証明書で暗号化されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、保護されたPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `encryptPDFUsingCertificates`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除{#removing-certificate-based-encryption}

証明書ベースの暗号化をPDFドキュメントから削除して、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができるようにすることができます。 証明書で暗号化されたPDFドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。 暗号化がPDFドキュメントから削除されると、その暗号化は保護されなくなります。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-2}の概要

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

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、`EncrytionServiceClient`オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、`EncryptionServiceService`オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外が発生します。 同様に、パスワードで暗号化されたドキュメントから証明書ベースの暗号化を削除しようとすると、例外が発生します。

**暗号化の削除**

暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。 秘密鍵のエイリアス値は、暗号化されたPDFドキュメントから証明書ベースの暗号化を削除するときに指定します。 公開鍵について詳しくは、[証明書でのPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)を参照してください。

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

### Java API {#remove-certificate-based-encryption-using-the-java-api}を使用した証明書ベースの暗号化の削除

Encryption API(Java)を使用して、PDFドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化を削除します。

   `EncryptionServiceClient`オブジェクトの`removePDFCertificateSecurity`メソッドを呼び出し、次の値を渡すことで、証明書ベースの暗号化をPDFドキュメントから削除します。

   * 暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * PDfドキュメントの暗号化に使用されるキーに対応する秘密鍵のエイリアス名を指定するstring値。

   `removePDFCertificateSecurity`メソッドは、保護されていないPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `com.adobe.idp.Document` メソッドから返された `removePDFCredentialSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した証明書ベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#remove-certificate-based-encryption-using-the-web-service-api}を使用して証明書ベースの暗号化を削除する

Encryption API（Webサービス）を使用して、証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、暗号化されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。

1. 暗号化を削除します。

   `EncryptionServiceClient`オブジェクトの`removePDFCertificateSecurity`メソッドを呼び出し、次の値を渡します。

   * 暗号化されたPDFドキュメントを表すファイルストリームデータを含む`BLOB`オブジェクトです。
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   `removePDFCredentialSecurity`メソッドは、保護されていないPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `removePDFPasswordSecurity`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワード暗号化の削除{#removing-password-encryption}

パスワードベースの暗号化をPDFドキュメントから削除して、パスワードを指定しなくても、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができるようにすることができます。 パスワードベースの暗号化をPDFドキュメントから削除すると、ドキュメントのセキュリティは保護されなくなります。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-3}の概要

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

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、`EncrytionServiceClient`オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、`EncryptionServiceService`オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

パスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントから暗号化を削除しようとすると、例外が発生します。

**パスワードの削除**

暗号化されたPDFドキュメントからパスワードベースの暗号化を削除するには、暗号化されたPDFドキュメントと、PDFドキュメントから暗号化を削除するために使用するマスターパスワードの両方を指定する必要があります。 パスワードで暗号化されたPDFドキュメントを開く際に使用するパスワードは、暗号化の削除には使用できません。 マスターパスワードは、PDFドキュメントがパスワードを使用して暗号化される場合に指定します。 (「[パスワードによるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。

**PDFドキュメントの保存**

EncryptionサービスでPDFドキュメントからパスワードベースの暗号化を削除した後、PDFドキュメントをPDFファイルとして保存できます。 ユーザーは、パスワードを指定せずに、Adobe ReaderまたはAcrobatでPDFドキュメントを開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[PDFドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#remove-password-based-encryption-using-the-java-api}を使用したパスワードベースの暗号化の削除

Encryption API(Java)を使用して、PDFドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. パスワードを削除します。

   `EncryptionServiceClient`オブジェクトの`removePDFPasswordSecurity`メソッドを呼び出し、次の値を渡すことで、PDFドキュメントからパスワードベースの暗号化を削除します。

   * 暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるマスターパスワード値を指定するstring値です。

   `removePDFPasswordSecurity`メソッドは、保護されていないPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `Document` メソッドから返された `removePDFPasswordSecurity` オブジェクトを必ず使用してください。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したパスワードベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### WebサービスAPI {#remove-password-based-encryption-using-the-web-service-api}を使用してパスワードベースの暗号化を削除

Encryption API（Webサービス）を使用して、パスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。

1. パスワードを削除します。

   `EncryptionServiceService`オブジェクトの`removePDFPasswordSecurity`メソッドを呼び出し、次の値を渡します。

   * 暗号化されたPDFドキュメントを表すファイルストリームデータを含む`BLOB`オブジェクトです。
   * PDFドキュメントから暗号化を削除するために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   `removePDFPasswordSecurity`メソッドは、保護されていないPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていないPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `removePDFPasswordSecurity`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化されたPDFドキュメントのロックを解除{#unlocking-encrypted-pdf-documents}

パスワードで暗号化または証明書で暗号化されたPDFドキュメントは、ロックを解除しないと、別のAEM Forms操作を実行できません。 暗号化されたPDFドキュメントに対して操作を実行しようとすると、例外が生成されます。 暗号化されたPDFドキュメントのロックを解除した後、暗号化されたPDF画像に対して1つ以上の操作を実行できます。 これらの操作は、Acrobat Reader DC拡張サービスなど、他のサービスに属することができます。

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-4}の概要

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

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、`EncrytionServiceClient`オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、`EncryptionServiceService`オブジェクトを作成します。

**暗号化されたPDFドキュメントの取得**

ロックを解除するには、暗号化されたPDFドキュメントを取得する必要があります。 暗号化されていないPDFドキュメントのロックを解除しようとすると、例外が発生します。

**ドキュメントのロック解除**

パスワードで暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、パスワードで暗号化されたPDFドキュメントを開くために使用するパスワード値の両方が必要です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。 (「[パスワードによるPDFドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)」を参照)。

証明書で暗号化されたPDFドキュメントのロックを解除するには、暗号化されたPDFドキュメントと、PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM Forms操作の実行**

暗号化されたPDFドキュメントのロックが解除された後、その画像に対して別のサービス操作（使用権限の適用など）を実行できます。 この操作は、Acrobat Reader DC拡張サービスに属します。

**関連トピック**

[Java APIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[WebサービスAPIを使用した暗号化されたPDFドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[EncryptionサービスAPIのクイック開始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API {#unlock-an-encrypted-pdf-document-using-the-java-api}を使用した暗号化されたPDFドキュメントのロック解除

暗号化API(Java)を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. Encryptionサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、暗号化されたPDFドキュメントの場所を指定するstring値を渡して、暗号化されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ドキュメントのロックを解除します。

   `EncryptionServiceClient`オブジェクトの`unlockPDFUsingPassword`メソッドまたは`unlockPDFUsingCredential`メソッドを呼び出して、暗号化されたPDFドキュメントのロックを解除します。

   パスワードを使用して暗号化されたPDFドキュメントのロックを解除するには、`unlockPDFUsingPassword`メソッドを呼び出し、次の値を渡します。

   * パスワードで暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   証明書で暗号化されたPDFドキュメントのロックを解除するには、`unlockPDFUsingCredential`メソッドを呼び出し、次の値を渡します。

   * 証明書で暗号化されたPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
   * PDFドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   `unlockPDFUsingPassword`メソッドと`unlockPDFUsingCredential`メソッドは共に`com.adobe.idp.Document`オブジェクトを返します。このオブジェクトは、別のAEM FormsJavaメソッドに渡して操作を実行します。

1. AEM Forms操作を実行します。

   ロック解除されたPDFドキュメントに対して、ビジネス要件に合わせてAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合、`unlockPDFUsingPassword`メソッドまたは`unlockPDFUsingCredential`メソッドから返された`com.adobe.idp.Document`オブジェクトを`ReaderExtensionsServiceClient`オブジェクトの`applyUsageRights`メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAPモード）を使用した暗号化されたPDFドキュメントのロック解除

[PDFドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#unlock-an-encrypted-pdf-document-using-the-web-service-api}を使用して暗号化されたPDFドキュメントのロックを解除する

Encryption API（Webサービス）を使用して暗号化されたPDFドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Encryptionサービスクライアントを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。

1. ドキュメントのロックを解除します。

   `EncryptionServiceClient`オブジェクトの`unlockPDFUsingPassword`メソッドまたは`unlockPDFUsingCredential`メソッドを呼び出して、暗号化されたPDFドキュメントのロックを解除します。

   パスワードを使用して暗号化されたPDFドキュメントのロックを解除するには、`unlockPDFUsingPassword`メソッドを呼び出し、次の値を渡します。

   * パスワードで暗号化されたPDFドキュメントを含む`BLOB`オブジェクトです。
   * パスワードで暗号化されたPDFドキュメントを開くために使用されるパスワード値を指定するstring値です。 この値は、PDFドキュメントをパスワードで暗号化する場合に指定します。

   証明書で暗号化されたPDFドキュメントのロックを解除するには、`unlockPDFUsingCredential`メソッドを呼び出し、次の値を渡します。

   * 証明書で暗号化されたPDFドキュメントが含まれる`BLOB`オブジェクトです。
   * PDfドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定するstring値。

   `unlockPDFUsingPassword`メソッドと`unlockPDFUsingCredential`メソッドは共に、別のAEM Formsメソッドに渡す`com.adobe.idp.Document`オブジェクトを返します。

1. AEM Forms操作を実行します。

   ロック解除されたPDFドキュメントに対して、ビジネス要件に合わせてAEM Forms操作を実行します。 例えば、ロック解除されたPDFドキュメントに使用権限を適用する場合、`unlockPDFUsingPassword`メソッドまたは`unlockPDFUsingCredential`メソッドから返された`BLOB`オブジェクトを`ReaderExtensionsServiceClient`オブジェクトの`applyUsageRights`メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化タイプの決定{#determining-encryption-type}

Java Encryption Service APIまたはWebサービスのEncryption Service APIを使用して、PDFドキュメントを保護する暗号化の種類をプログラムで判断できます。 PDFドキュメントが暗号化されているかどうか、および暗号化されている場合は暗号化の種類を動的に判断する必要がある場合があります。 例えば、PDFドキュメントをパスワードベースの暗号化またはRights Managementポリシーで保護するかどうかを指定できます。

PDFドキュメントは、次の暗号化タイプで保護できます。

* パスワードベースの暗号化
* 証明書ベースの暗号化
* Rights Managementサービスによって作成されるポリシーです
* 別の種類の暗号化

>[!NOTE]
>
>Encryptionサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-5}の概要

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

プログラムによってEncryptionサービスの操作を実行するには、Encryptionサービスクライアントを作成する必要があります。 Java Encryption Service APIを使用している場合は、`EncrytionServiceClient`オブジェクトを作成します。 WebサービスのEncryption Service APIを使用している場合は、`EncryptionServiceService`オブジェクトを作成します。

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

### Java API {#determine-the-encryption-type-using-the-java-api}を使用して暗号化タイプを決定する

Encryption API(Java)を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-encryption-client.jarなどのクライアントJARファイルを含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`EncryptionServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、PDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 暗号化タイプを決定します。

   * `EncryptionServiceClient`オブジェクトの`getPDFEncryption`メソッドを呼び出し、PDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡して、暗号化の種類を決定します。 このメソッドは、`EncryptionTypeResult`オブジェクトを返します。
   * `EncryptionTypeResult`オブジェクトの`getEncryptionType`メソッドを呼び出します。 このメソッドは、暗号化の種類を指定する`EncryptionType`列挙値を返します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、`EncryptionType.PASSWORD`を返します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#determine-the-encryption-type-using-the-web-service-api}を使用して暗号化の種類を決定する

Encryption API（Webサービス）を使用して、PDFドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. サービスクライアントを作成します。

   * `EncryptionServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`EncryptionServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `EncryptionServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`EncryptionServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`EncryptionServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 暗号化されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の内容を`BLOB`オブジェクトの`MTOM`データメンバーに割り当てて、`BLOB`オブジェクトを入力します。

1. 暗号化タイプを決定します。

   * `EncryptionServiceClient`オブジェクトの`getPDFEncryption`メソッドを呼び出し、PDFドキュメントを含む`BLOB`オブジェクトを渡します。 このメソッドは、`EncryptionTypeResult`オブジェクトを返します。
   * `EncryptionTypeResult`オブジェクトの`encryptionType`データメソッドの値を取得します。 例えば、PDFドキュメントがパスワードベースの暗号化で保護されている場合、このデータメンバーの値は`EncryptionType.PASSWORD`です。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)