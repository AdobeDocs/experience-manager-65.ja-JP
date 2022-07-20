---
title: PDF ドキュメントの暗号化および復号化
seo-title: Encrypting and Decrypting PDF Documents
description: 暗号化サービスを使用して、ドキュメントを暗号化および復号化します。暗号化サービスタスクには、次の内容が含まれます。PDF ドキュメントのパスワードによる暗号化、PDF ドキュメントの証明書による暗号化、PDF ドキュメントからのパスワードによる暗号化の削除、PDF ドキュメントからの証明書による暗号化の削除、他のサービス操作を可能にする PDF ドキュメントのロック解除、保護された PDF ドキュメントの暗号化の種類の決定。
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '8189'
ht-degree: 100%

---

# PDF ドキュメントの暗号化および復号化 {#encrypting-and-decrypting-pdf-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**暗号化サービスについて**

暗号化サービスを使用すると、ドキュメントの暗号化および復号化が可能になります。ドキュメントを暗号化すると、その内容は判読できなくなります。許可されたユーザーはドキュメントを復号化して、コンテンツにアクセスできます。PDF ドキュメントがパスワードで暗号化されている場合、ユーザーは開くためのパスワードを指定しないと、Adobe Reader または Adobe Acrobat でドキュメントを表示できません。同じように、PDF ドキュメントが証明書で暗号化されている場合も、ユーザーが PDF ドキュメントを復号化するには、その PDF ドキュメントの暗号化に使用された証明書（秘密鍵）に対応した公開鍵が必要です。

暗号化サービスを使用して、次のタスクを実行できます。

* パスワードで PDF ドキュメントを暗号化します。（[PDF ドキュメントのパスワードによる暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)を参照してください）。
* 証明書で PDF ドキュメントを暗号化します。（[証明書による PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)を参照してください）。
* PDF ドキュメントからパスワードベースの暗号化を削除します。（[パスワード暗号化を削除](encrypting-decrypting-pdf-documents.md#removing-password-encryption)を参照してください）。
* PDF ドキュメントから証明書ベースの暗号化を削除します。（[証明書ベースの暗号化の削除](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)を参照してください）。
* 他のサービス操作を実行できるように、PDF ドキュメントのロックを解除します。例えば、パスワードで暗号化された PDF ドキュメントのロックが解除された後に、デジタル署名を適用できます。（[暗号化された PDF ドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)を参照してください）。
* 保護された PDF ドキュメントの暗号化のタイプを決定します。（[暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determining-encryption-type)を参照してください）。

>[!NOTE]
>
>暗号化サービスについての詳細情報は、『[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## パスワードを使用した PDF ドキュメントの暗号化 {#encrypting-pdf-documents-with-a-password}

PDF ドキュメントをパスワードで暗号化する場合、ユーザーは Adobe Reader または Acrobat で PDF ドキュメントを開くためのパスワードを指定する必要があります。また、ドキュメントにデジタル署名を行うなど、別の AEM Forms 操作を行う前に、パスワードで暗号化された PDF ドキュメントのロックを解除しておく必要があります。

>[!NOTE]
>
>暗号化された PDF ドキュメントを AEM Forms リポジトリにアップロードすると、PDF ドキュメントを復号化して XDP コンテンツをエクストラクトすることはできません。ドキュメントを AEM Forms リポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。（[リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources) を参照してください）。

>[!NOTE]
>
>暗号化サービスについての詳細情報に関しては、『[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary-of-steps}

パスワードを使用して PDF ドキュメントを暗号化するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化クライアント API オブジェクトを作成します。
1. 暗号化する PDF ドキュメントを取得します。
1. 暗号化の実行時オプションを設定します。
1. パスワードを追加します。
1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**暗号化クライアント API オブジェクトを作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。

**暗号化する PDF ドキュメントを取得**

パスワードを使用してドキュメントを暗号化するには、暗号化されていない PDF ドキュメントを取得する必要があります。既に暗号化されている PDF ドキュメントを保護しようとすると、例外が発生します。

**暗号化の実行時オプションを設定**

パスワードを使用して PDF ドキュメントを暗号化するには、2 つのパスワード値を含む 4 つの値を指定します。最初のパスワード値は、PDF ドキュメントの暗号化に使用され、PDF ドキュメントを開く際に指定する必要があります。2 つ目のパスワード値は、プライマリパスワード値と呼ばれ、PDF ドキュメントから暗号化を削除するために使用されます。パスワード値では大文字と小文字が区別され、これら 2 つのパスワード値を同じ値にすることはできません。

暗号化する PDF ドキュメントリソースを指定する必要があります。PDF ドキュメント全体、ドキュメントのメタデータ以外のすべて、またはドキュメントの添付ファイルのみを暗号化できます。ドキュメントの添付ファイルのみを暗号化する場合、添付ファイルにアクセスしようとすると、ユーザーにパスワードの入力が求められます。

PDF ドキュメントを暗号化する際に、保護されたドキュメントに関連付けられた権限を指定できます。権限を指定すると、パスワードで暗号化されたPDF ドキュメントを開いたユーザーが実行できるアクションを制御できます。例えば、フォームデータを正常にエクストラクトするには、以下の権限を設定する必要があります。

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>権限は `PasswordEncryptionPermission` 列挙値として指定します。

**パスワードを追加**

保護されていない PDF ドキュメントを取得し、暗号化の実行時の値を設定した後、パスワードを PDF ドキュメントに追加できます。

**暗号化された PDF ドキュメントを PDF ファイルとして保存**

パスワードで暗号化された PDF ドキュメントは、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用して PDFドキュメントを暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Web サービス API を使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[証明書による PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Java API を使用して PDFドキュメントを暗号化 {#encrypt-a-pdf-document-using-the-java-api}

暗号化 API（Java）を使用して、PDF ドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスにクライアントの JAR ファイル（adobe-livecycle-client.jar など）を含めます。

1. 暗号化クライアント API を作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化する PDF ドキュメントを取得します。

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクト作成するには、そのオブジェクトのコンストラクターを使用して、`java.io.FileInputStream` オブジェクトを渡します。

1. 暗号化の実行時オプションを設定します。

   * コンストラクターを使用して `PasswordEncryptionOptionSpec` オブジェクトを作成します。
   * `PasswordEncryptionOptionSpec` オブジェクトの `setEncryptOption` メソッドを呼び出し、暗号化するドキュメントリソースを指定する `PasswordEncryptionOption` 列挙値を渡すことによって、暗号化する PDF ドキュメントリソースを指定します。例えば、メタデータと添付ファイルを含む PDF ドキュメント全体を暗号化するには、`PasswordEncryptionOption.ALL` と指定します。
   * `ArrayList` コンストラクターを使用して、暗号化の権限を保存する `java.util.List` オブジェクトを作成します。
   * `java.util.List` オブジェクトの `add` メソッドを呼び出し、設定する権限に対応する列挙値を渡すことにより、権限を指定してください。例えば、ユーザーが PDF ドキュメント内のデータをコピーできる権限を設定するには、`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`と指定してください。（設定する権限ごとに、このステップを繰り返します）。
   * `PasswordEncryptionOptionSpec` オブジェクトの `setCompatability` メソッドを呼び出し、Acrobat の互換性レベルを指定する列挙値を渡して、Acrobat の互換性オプションを指定します。例えば、`PasswordEncryptionCompatability.ACRO_7` と指定できます。
   * パスワードの値を指定します。この値を使用すると、`PasswordEncryptionOptionSpec` オブジェクトの `setDocumentOpenPassword` メソッドを呼び出し、開くパスワードを表す文字列値を渡すことによって、ユーザーが暗号化された PDF ドキュメントを開くことができます。
   * プライマリパスワードの値を指定します。この値を使用すると、`PasswordEncryptionOptionSpec` オブジェクトの `setPermissionPassword` メソッドを呼び出し、プライマリパスワードを表す文字列値を渡すことによって、ユーザーが暗号化された PDF ドキュメントから暗号化を削除することができます。

1. パスワードを追加します。

   `EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッドを呼び出して、以下の値を渡すことにより、PDF ドキュメントを暗号化します。

   * パスワードで暗号化する PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * 暗号化の実行時オプションを含む `PasswordEncryptionOptionSpec` オブジェクト。

   この `encryptPDFUsingPassword` メソッドは、パスワードで暗号化されたPDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツをファイルにコピーします。`encryptPDFUsingPassword` メソッドから返された `com.adobe.idp.Document` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF ドキュメントの暗号化 {#encrypting-a-pdf-document-using-the-web-service-api}

暗号化 API（web サービス）を使用して、PDF ドキュメントをパスワードで暗号化します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. 暗号化クライアント API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`EncryptionServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. 暗号化する PDF ドキュメントを取得します。

   * `BLOB` オブジェクトのコンストラクタを使用して、このオブジェクトを作成します。`BLOB` オブジェクトを使用して、証明書で暗号化された PDF ドキュメントを保存します。
   * コンストラクターを呼び出して、暗号化する PDF ドキュメントファイルの場所とファイルを開くモードを表す文字列の値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバーに割り当てることにより、`BLOB` オブジェクトを入力します。

1. 暗号化の実行時オプションを設定します。

   * `PasswordEncryptionOptionSpec` オブジェクトのコンストラクタを使用して、このオブジェクトを作成します。
   * `PasswordEncryptionOption` 列挙値を `PasswordEncryptionOptionSpec` オブジェクトの `encryptOption` データメンバーに割り当てることにより、暗号化する PDF ドキュメントリソースを指定します。メタデータと添付ファイルを含む PDF 全体を暗号化するには、 `PasswordEncryptionOption.ALL` をこのデータメンバーに割り当てます。
   * `PasswordEncryptionCompatability` 列挙値を `PasswordEncryptionOptionSpec` オブジェクトの `compatability` データメンバーに割り当てることにより、Acrobat の互換性オプションを指定します。例えば、`PasswordEncryptionCompatability.ACRO_7` をこのデータメンバーに割り当てます。
   * ユーザーが暗号化された PDF ドキュメントを開くためのパスワード値を指定します。この値を指定するには、開封パスワードを表す文字列値を `PasswordEncryptionOptionSpec` オブジェクトの `documentOpenPassword` データメンバーに割り当てます。
   * ユーザーが PDF ドキュメントの暗号化を削除するためのパスワード値を指定します。この値を指定するには、プライマリパスワードを表す文字列値を `PasswordEncryptionOptionSpec` オブジェクトの `permissionPassword` データメンバーに割り当てます。

1. パスワードを追加します。

   `EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッドを呼び出して、以下の値を渡すことにより、PDF ドキュメントを暗号化します。

   * パスワードで暗号化する PDF ドキュメントを含む `BLOB` オブジェクト。
   * 暗号化の実行時オプションを含む `PasswordEncryptionOptionSpec` オブジェクト。

   この `encryptPDFUsingPassword` メソッドは、パスワードで暗号化されたPDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、このオブジェクトのコンストラクターを呼び出し、保護された PDF ドキュメントのファイルの場所を表す文字列の値を渡します。
   * `encryptPDFUsingPassword` メソッドが返した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書による PDF ドキュメントの暗号化 {#encrypting-pdf-documents-with-certificates}

証明書ベースの暗号化では、公開鍵によるテクノロジーを使用して、特定の受信者用にドキュメントを暗号化できます。様々な受信者に、ドキュメントに対する異なる権限を与えることができます。公開鍵のテクノロジーによって、暗号化の様々な側面が可能になります。アルゴリズムによって、大きい数字が 2 つ生成されます。この数字は以下のような特性を持つ&#x200B;*鍵*&#x200B;として知られています。

* 鍵のうち 1 つは、1 組のデータを暗号化するために使用されます。その後、もう一方の鍵のみがデータの復号に使用できます。
* 1 つの鍵を、もう一方の鍵と区別することは不可能です。

鍵のうち 1 つは、ユーザーの秘密鍵として機能します。当該のユーザーのみがこの鍵にアクセスできることが重要です。もう 1 つの鍵はユーザーの公開鍵です。これは、他のユーザーと共有できます。

公開鍵証明書には、ユーザーの公開鍵と識別情報が含まれます。証明書の保存には、X.509 形式が使用されます。通常、証明書は認証局（CA）で発行および電子署名されます。CA は、証明書の有効性における信頼度を提供する、承認されたエンティティです。証明書には有効期限があり、この期限を過ぎると無効になります。また、証明書の失効リスト（CRL）には、有効期限よりも前に失効した証明書に関する情報が示されます。CRL は認証局によって定期的に発行されます。証明書の失効ステータスは、ネットワークを通じてオンライン証明書ステータスプロトコル（OCSP）から取得することもできます。

>[!NOTE]
>
>暗号化された PDF ドキュメントを AEM Forms リポジトリにアップロードすると、PDF ドキュメントを復号化して XDP コンテンツをエクストラクトすることはできません。ドキュメントを AEM Forms リポジトリにアップロードする前に、ドキュメントを暗号化しないことをお勧めします。（[リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources) を参照。）

>[!NOTE]
>
>PDF ドキュメントを証明書で暗号化する前に、AEM Forms に証明書が追加されていることを確認する必要があります。証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。（[Trust Manager API を使用した資格情報のインポート](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api) を参照。）

>[!NOTE]
>
>暗号化サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

証明書を使用して PDF ドキュメントを暗号化するには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化クライアント API オブジェクトを作成します。
1. 暗号化する PDF ドキュメントを取得します。
1. 証明書を参照します。
1. 暗号化の実行時オプションを設定します。
1. 証明書で暗号化された PDF ドキュメントを作成します。
1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

**暗号化クライアント API オブジェクトを作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。Java Encryption Service API を使用している場合は、`EncrytionServiceClient` オブジェクトを作成します。Web サービス暗号化サービス API を使用している場合は、`EncryptionServiceService` オブジェクトを作成します。

**暗号化する PDF ドキュメントを取得**

暗号化するためには、暗号化されていない PDF ドキュメントを取得する必要があります。既に暗号化されている PDF ドキュメントを保護しようとすると、例外が発生します。

**証明書を参照**

PDF ドキュメントを証明書で暗号化するには、PDF ドキュメントの暗号化に使用する証明書を参照します。証明書は .cer ファイル、.crt ファイル、.pem ファイルのいずれかです。PKCS#12 ファイルは、対応する証明書とともに秘密鍵を保存するために使用します。

証明書を使用して PDF ドキュメントを暗号化する場合は、保護されたドキュメントに関連付けられている権限を指定します。権限を指定すると、証明書で暗号化された PDF ドキュメントを開いたユーザーが実行できるアクションを制御できます。

**暗号化実行時オプションの設定**

暗号化する PDF ドキュメントリソースを指定します。PDFドキュメント全体、ドキュメントのメタデータを除くすべて、またはドキュメントの添付ファイルのみを暗号化できます。

**証明書で暗号化された PDF ドキュメントの作成**

セキュリティで保護されていない PDF ドキュメントを取得し、証明書を参照しながら、実行時オプションを設定したら、証明書で暗号化された PDF ドキュメントを作成できます。暗号化された PDF ドキュメントを復号化するには、対応する公開鍵が必要になります。

**暗号化された PDF ドキュメントを PDF ファイルとして保存**

暗号化された PDF ドキュメントは、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用して証明書で PDF ドキュメントを暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Web サービス API を使用して 証明書により PDF ドキュメントを暗号化](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードを使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用して証明書で PDF ドキュメントを暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

暗号化 API（Java）を使用して、証明書により PDF ドキュメントを暗号化します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスにクライアントの JAR ファイル（adobe-livecycle-client.jar など）を含めます。

1. Encryption Client API オブジェクトを作成する。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化する PDF ドキュメントを取得します。

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 証明書を参照する。

   * コンストラクターを使用して権限情報を格納する `java.util.List` オブジェクトを作成します。
   * `java.util.List` オブジェクトの `add` メソッドを呼び出して、セキュリティで保護された PDF ドキュメントを開くユーザーに付与する権限を表す列挙値（`CertificateEncryptionPermissions`）を渡すことにより、暗号化されたドキュメントに関連する権限を指定します。例えば、すべての権限を指定する場合は、 `CertificateEncryptionPermissions.PKI_ALL_PERM` を指定します。
   * コンストラクターを使用して `Recipient` を作成します。
   * コンストラクターを使用して、証明書の場所を指定する文字列値を渡すことにより、PDF ドキュメントの暗号化に使用する証明書を表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し、証明書を表す `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。
   * `Recipient` オブジェクトの `setX509Cert` メソッドを呼び出し、証明書が含まれる `com.adobe.idp.Document` オブジェクトを渡します（`Recipient` オブジェクトには、証明書のソースとして TrustStore 証明書のエイリアス、または LDAP URL を指定することもできます。）
   * コンストラクターを使用して、権限と証明書の情報を格納する `CertificateEncryptionIdentity` オブジェクトを作成します。
   * `CertificateEncryptionIdentity` オブジェクトの `setPerms` メソッドを呼び出して、権限情報を格納する `java.util.List` オブジェクトを渡します。
   * `CertificateEncryptionIdentity` オブジェクトの `setRecipient` メソッドを呼び出して、証明書情報を格納する `Recipient` オブジェクトを渡します。
   * コンストラクターを使用して証明書情報を格納する `java.util.List` を作成します。
   * `java.util.List` オブジェクトの add メソッドを呼び出して `CertificateEncryptionIdentity` オブジェクトを渡します。（この `java.util.List` オブジェクトは、パラメーターとして `encryptPDFUsingCertificates` メソッドに渡されます）

1. 暗号化の実行時オプションを設定する。

   * コンストラクターを使用して `CertificateEncryptionOptionSpec` オブジェクトを作成します。
   * `CertificateEncryptionOptionSpec` オブジェクトの `setOption` メソッドを呼び出し、暗号化するドキュメントリソースを指定する `CertificateEncryptionOption` 列挙値を渡すことによって、暗号化する PDF ドキュメントリソースを指定します。例えば、メタデータと添付ファイルを含む PDF ドキュメント全体を暗号化する場合は、`CertificateEncryptionOption.ALL` と指定します。
   * `CertificateEncryptionOptionSpec` オブジェクトの `setCompat` メソッドを呼び出して、Acrobat の互換性レベルを指定する列挙値（`CertificateEncryptionCompatibility`）を渡して、Acrobat の互換性オプションを指定します。例えば、`CertificateEncryptionCompatibility.ACRO_7` と指定できます。

1. 証明書で暗号化された PDF ドキュメントを作成する。

   `EncryptionServiceClient` オブジェクトの `encryptPDFUsingCertificates` メソッドを呼び出し、次の値を渡すことにより、PDF ドキュメントを証明書で暗号化します。

   * 暗号化する PDF ドキュメントが含まれる `com.adobe.idp.Document` オブジェクト
   * 証明書情報を格納する `java.util.List` オブジェクト
   * 暗号化の実行時オプションが含まれる `CertificateEncryptionOptionSpec` オブジェクト

   `encryptPDFUsingCertificates` メソッドにより、証明書で暗号化された PDF ドキュメントが含まれる `com.adobe.idp.Document` オブジェクトが返されます。

1. 暗号化された PDF ドキュメントを PDF ファイルとして保存する。

   * `java.io.File` オブジェクトを作成し、ファイルの拡張子が .pdf になっていることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツをファイルにコピーします。`encryptPDFUsingCertificates` メソッドから返された `com.adobe.idp.Document` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの証明書での暗号化](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して 証明書により PDF ドキュメントを暗号化 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Encryption API（Web サービス）を使用して、PDF ドキュメントを証明書で暗号化します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. 暗号化クライアント API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`EncryptionServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. 暗号化する PDF ドキュメントを取得します。

   * コンストラクターを呼び出すことにより、`BLOB` オブジェクトを作成します。`BLOB` オブジェクトを使用して、証明書で暗号化された PDF ドキュメントを保存します。
   * コンストラクターを呼び出して、暗号化する PDF ドキュメントファイルの場所とファイルを開くモードを表す文字列の値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることにより、`BLOB` オブジェクトに格納します。

1. 証明書を参照します。

   * コンストラクターを使用して `Recipient` オブジェクトを作成します。このオブジェクトは、証明書情報を格納します。
   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトには、PDF ドキュメントを暗号化する証明書が格納されます。
   * コンストラクターを呼び出して、証明書ファイルの場所とファイルを開くモードを表す文字列の値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバーに割り当てることにより、`BLOB` オブジェクトに格納します。
   * 証明書を格納する `BLOB` オブジェクトを、`Recipient` オブジェクトの `x509Cert` データメンバーに割り当てます。
   * コンストラクターを使用して、証明書情報を格納する `CertificateEncryptionIdentity` オブジェクトを作成します。
   * 証明書を格納する `Recipient` オブジェクトを、`CertificateEncryptionIdentity` オブジェクトの受信者データメンバーに割り当てます。
   * `Object` 配列を作成して、`CertificateEncryptionIdentity` オブジェクトを `Object` 配列の最初の要素に割り当てます。この `Object` 配列が、`encryptPDFUsingCertificates` メソッドへパラメーターとして渡されます。

1. 暗号化の実行時オプションを設定します。

   * `CertificateEncryptionOptionSpec` オブジェクトのコンストラクタを使用して、このオブジェクトを作成します。
   * `CertificateEncryptionOption` 列挙値を `CertificateEncryptionOptionSpec` オブジェクトの `option` データメンバーに割り当てることにより、暗号化する PDF ドキュメントリソースを指定します。メタデータと添付ファイルを含む、PDFドキュメント全体を暗号化するには、`CertificateEncryptionOption.ALL` をこのデータメンバーに割り当てます。
   * `CertificateEncryptionCompatibility` 列挙値を `CertificateEncryptionOptionSpec` オブジェクトの `compat` データメンバーに割り当てることにより、Acrobat の互換性オプションを指定します。例えば、`CertificateEncryptionCompatibility.ACRO_7` をこのデータメンバーに割り当てます。

1. 証明書で暗号化された PDF ドキュメントを作成します。

   `EncryptionServiceService` オブジェクトの `encryptPDFUsingCertificates` メソッドを呼び出し、次の値を渡すことにより、PDF ドキュメントを証明書で暗号化します。

   * 暗号化する PDF ドキュメントを含む `BLOB` オブジェクト。
   * 証明書情報を格納する `Object` 配列。
   * 暗号化の実行時オプションを含む `CertificateEncryptionOptionSpec` オブジェクト。

   `encryptPDFUsingCertificates` メソッドにより、証明書で暗号化された PDF ドキュメントが含まれる `BLOB` オブジェクトが返されます。

1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、このオブジェクトのコンストラクターを呼び出し、保護された PDF ドキュメントのファイルの場所を表す文字列の値を渡します。
   * `encryptPDFUsingCertificates` メソッドが返した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `binaryData` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 証明書ベースの暗号化の削除 {#removing-certificate-based-encryption}

証明書ベースの暗号化は PDF ドキュメントから削除することができ、これにより、Adobe Reader または Acrobat で PDF ドキュメントを開くことができます。証明書で暗号化されている PDF ドキュメントから暗号化を削除するには、公開鍵を参照する必要があります。PDF ドキュメントから暗号化を削除すると、そのドキュメントは保護されなくなります。

>[!NOTE]
>
>暗号化サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

証明書ベースの暗号化を PDF ドキュメントから削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化された PDF ドキュメントを取得します。
1. 暗号化を削除します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。Java Encryption Service API を使用している場合は、`EncrytionServiceClient` オブジェクトを作成します。Web サービス Encryption Service API を使用している場合は、`EncryptionServiceService` オブジェクトを作成します。

**暗号化された PDF ドキュメントを取得**

証明書ベースの暗号化を削除するには、暗号化された PDF ドキュメントを取得する必要があります。暗号化されていない PDF ドキュメントから暗号化を削除しようとすると、例外がスローされます。同様に、パスワードで暗号化されたドキュメントから証明書ベースの暗号化を削除しようとすると、例外がスローされます。

**暗号化を削除**

暗号化された PDF ドキュメントから証明書ベースの暗号化を削除するには、暗号化された PDF ドキュメントと、PDF ドキュメントの暗号化に使用されたキーに対応する秘密鍵の両方が必要です。暗号化された PDF ドキュメントから証明書ベースの暗号化を削除する際に、秘密鍵のエイリアス値が指定されます。公開鍵についての詳細情報に関しては、[証明書を使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)を参照してください。

>[!NOTE]
>
>秘密鍵は AEM Forms Trust Store に保存されます。証明書が配置されると、エイリアス値が指定されます。

**PDF ドキュメントを保存**

暗号化された PDF ドキュメントから証明書ベースの暗号化を削除した後、PDF ドキュメントを PDF ファイルとして保存できます。ユーザーは、Adobe Reader または Acrobat で PDF ドキュメントを開くことができます。

**関連トピック**

[Java API を使用して証明書ベースの暗号化を削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Web サービス API を使用して証明書ベースの暗号化を削除](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API を使用して証明書ベースの暗号化を削除 {#remove-certificate-based-encryption-using-the-java-api}

暗号化 API（Java）を使用して、PDF ドキュメントから証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスにクライアントの JAR ファイル（adobe-livecycle-client.jar など）を含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化された PDF ドキュメントを取得します。

   * 暗号化された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、このオブジェクトのコンストラクターを使用し、暗号化された PDF ドキュメントの場所を表す文字列値を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成するには、このオブジェクトのコンストラクターを使用し、`java.io.FileInputStream` オブジェクトをを渡します。

1. 暗号化を削除します。

   `EncryptionServiceClient` オブジェクトの `removePDFCertificateSecurity` メソッドを呼び出し、次の値を渡すことによって、証明書ベースの暗号化を PDF ドキュメントから削除します。

   * 暗号化された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * PDF ドキュメントの暗号化に使用されたキーに対応する秘密鍵のエイリアス名を指定する文字列値です。

   `removePDFCertificateSecurity` メソッドは、保護されていない PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトのコンテンツをファイルにコピーします。`removePDFCredentialSecurity` メソッドから返された `com.adobe.idp.Document` オブジェクトを必ず使用してください。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した証明書ベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して証明書ベースの暗号化を削除 {#remove-certificate-based-encryption-using-the-web-service-api}

暗号化 API（web サービス）を使用して、証明書ベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストしているサーバーの IP アドレスに置換します。

1. 暗号化サービスクライアントを作成します。

   * `EncryptionServiceClient` オブジェクトを作成するには、このオブジェクトのデフォルトのコンストラクターを使用します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 暗号化された PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、暗号化された PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、暗号化された PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバーに割り当てることにより、`BLOB` オブジェクトにデータを入力します。

1. 暗号化を削除します。

   `EncryptionServiceClient` オブジェクトの `removePDFCertificateSecurity` メソッドを呼び出して、次の値を渡します。

   * 暗号化された PDF ドキュメントを表すファイルストリームデータを含む `BLOB` オブジェクト。
   * PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス名を指定する文字列値。

   `removePDFCredentialSecurity` メソッドは、保護されていない PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. PDF ドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていない PDF ドキュメントのファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `removePDFPasswordSecurity` メソッドによって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得し、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## パスワード暗号化の削除 {#removing-password-encryption}

パスワードベースの暗号化を PDF ドキュメントから削除できるため、ユーザーはパスワードを指定しなくても Adobe Reader または Acrobat で PDF ドキュメントを開くことができます。パスワードによる暗号化を PDF ドキュメントから削除すると、そのドキュメントは保護されなくなります。

>[!NOTE]
>
>暗号化サービスについて詳しくは、『[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-3}

PDF ドキュメントからパスワードベースの暗号化を削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. 暗号化サービスクライアントを作成します。
1. 暗号化された PDF ドキュメントを取得します。
1. パスワードを削除します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。Java Encryption Service API を使用している場合は、`EncrytionServiceClient` オブジェクトを作成します。Web サービス Encryption Service API を使用している場合は、`EncryptionServiceService` オブジェクトを作成します。

**暗号化された PDF ドキュメントを取得**

パスワードベースの暗号化を削除するには、暗号化された PDF ドキュメントを取得する必要があります。暗号化されていない PDF ドキュメントから暗号化を削除しようとすると、例外がスローされます。

**パスワードを削除**

暗号化された PDF ドキュメントからパスワードベースの暗号化を削除するには、暗号化された PDF ドキュメントと、PDF ドキュメントから暗号化を削除するために使用されるマスターパスワード値の両方が必要です。パスワードで暗号化された PDF ドキュメントを開くために使用されるパスワードは、暗号化を削除するために使用することはできません。マスターパスワードは、PDF ドキュメントがパスワードで暗号化されるときに指定します。（[パスワードを使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)を参照。）

**PDF ドキュメントの保存**

暗号化サービスが PDF ドキュメントからパスワードベースの暗号化を削除したら、PDF ドキュメントを PDF ファイルとして保存できます。ユーザーは、パスワードを指定せずに Adobe Reader または Acrobat で PDF ドキュメントを開くことができます。

**関連項目**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[パスワードを使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API を使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-java-api}

暗号化 API（Java）を使用して、PDF ドキュメントからパスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   クライアント JAR ファイル（adobe-encryption-client.jar など）を Java プロジェクトのクラスパスに含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化された PDF ドキュメントを取得します。

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡すことにより、暗号化された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. パスワードを削除します。

   `EncryptionServiceClient` オブジェクトの `removePDFPasswordSecurity` メソッドを呼び出して次の値を渡すことによって、PDF ドキュメントからパスワードベースの暗号化を削除します。

   * 暗号化された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * PDF ドキュメントから暗号化を削除するために使用するマスターパスワード値を指定する文字列の値。

   `removePDFPasswordSecurity` メソッドは、保護されていない PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトのコンテンツをファイルにコピーします。`removePDFPasswordSecurity` メソッドから返された `Document` オブジェクトを必ず使用してください。

**関連項目**

[クイックスタート（SOAP モード）：Java API を使用したパスワードベースの暗号化の削除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Web サービス API を使用したパスワードベースの暗号化の削除 {#remove-password-based-encryption-using-the-web-service-api}

Encryption API（web サービス）を使用して、パスワードベースの暗号化を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストしているサーバーの IP アドレスに置換します。

1. 暗号化サービスクライアントを作成します。

   * `EncryptionServiceClient` オブジェクトを作成するには、このオブジェクトのデフォルトのコンストラクターを使用します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 暗号化された PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトを使用して、パスワードで暗号化された PDF ドキュメントを格納します。
   * コンストラクターを呼び出し、暗号化された PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列のコンテンツを `BLOB` オブジェクトの `MTOM` データメンバーに割り当てることにより、`BLOB` オブジェクトを設定します。

1. パスワードを削除します。

   `EncryptionServiceService` オブジェクトの `removePDFPasswordSecurity` メソッドを呼び出して、以下の値を渡します。

   * 暗号化された PDF ドキュメントを表すファイルストリームデータを格納する `BLOB` オブジェクト。
   * PDF ドキュメントから暗号化を削除するために使用するパスワード値を指定する文字列値。この値は、パスワードで PDF ドキュメントを暗号化する際に指定します。

   `removePDFPasswordSecurity` メソッドは、保護されていない PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. PDF ドキュメントを保存します。

   * コンストラクターを呼び出し、保護されていない PDF ドキュメントのファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `removePDFPasswordSecurity` メソッドによって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得し、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化された PDF 文書のロック解除 {#unlocking-encrypted-pdf-documents}

パスワードまたは証明書で暗号化された PDF ドキュメントは、別の AEM Forms で操作する前に、ロックを解除する必要があります。暗号化された PDF ドキュメントに対して操作を実行しようとすると、例外が発生します。暗号化された PDF ドキュメントのロックを解除すると、そのドキュメントに対する操作を実行できるようになります。Acrobat Reader DC 拡張機能サービスなど、別のサービスがそのような操作を行う可能性があります。

>[!NOTE]
>
>暗号化サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-4}

暗号化された PDF ドキュメントのロックを解除するには、次の手順を実施します。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化された PDF 文書を取得します。
1. ドキュメントのロックを解除します。
1. AEM Forms の操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

**暗号化サービスクライアントの作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。Java Encryption Service API を使用している場合は、`EncrytionServiceClient` オブジェクトを作成します。Web サービス Encryption Service API を使用している場合は、`EncryptionServiceService` オブジェクトを作成します。

**暗号化された PDF 文書の取得**

ロックを解除するには、暗号化された PDF ドキュメントを取得する必要があります。暗号化されていない PDF ドキュメントのロックを解除しようとすると、例外が発生します。

**ドキュメントのロックを解除**

パスワードで暗号化された PDF ドキュメントのロックを解除するには、暗号化されたPDF ドキュメントと、パスワードで暗号化された PDF ドキュメントを開くために使用するパスワード値の両方が必要です。この値は、パスワードで PDF ドキュメントを暗号化する際に指定します。（[パスワードを使用した PDF ドキュメントの暗号化](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)を参照。）

証明書で暗号化された PDF ドキュメントのロックを解除するには、暗号化された PDF ドキュメントと、PDF ドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス値の両方が必要です。

**AEM Forms 操作の実行**

暗号化された PDF ドキュメントのロックが解除された後は、そのドキュメントに対して別のサービス操作（使用権限の適用など）を実行できます。この操作は、Acrobat Reader DC Extensions サービスに属しています。

**関連項目**

[Java API での暗号化された PDF ドキュメントのロック解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Web サービス API を使用して暗号化された PDF ドキュメントのロックを解除](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Java API での暗号化された PDF ドキュメントのロック解除 {#unlock-an-encrypted-pdf-document-using-the-java-api}

Encryption API（Java）を使用して、暗号化された PDF ドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスにクライアントの JAR ファイル（adobe-livecycle-client.jar など）を含めます。

1. 暗号化サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化された PDF ドキュメントを取得します。

   * 暗号化された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、このオブジェクトのコンストラクターを使用し、暗号化された PDF ドキュメントの場所を表す文字列値を渡します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. ドキュメントのロックを解除します。

   `EncryptionServiceClient` オブジェクトの `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドを呼び出して、暗号化された PDFドキュメントをロック解除します。

   パスワードで暗号化された PDF ドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを呼び出して、次の値を渡します。

   * パスワードで暗号化された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * パスワードで暗号化された PDF ドキュメントを開くために使用されるパスワード値を指定する文字列値です。この値は、パスワードで PDF ドキュメントを暗号化する際に指定します。

   証明書で暗号化されている PDF ドキュメントのロックを解除するには、`unlockPDFUsingCredential` メソッドを呼び出して、次の値を渡します。

   * 証明書で暗号化された PDF ドキュメントのコンテンツを表す `com.adobe.idp.Document` オブジェクト。
   * PDF ドキュメントの暗号化に使用される秘密鍵に対応する公開鍵のエイリアス名を指定する文字列値。

   `unlockPDFUsingPassword` および `unlockPDFUsingCredential` メソッドは両方とも、別の AEM Forms Java メソッドに渡して操作を実行する `com.adobe.idp.Document` オブジェクトを返します。

1. AEM Forms 操作を実行します。

   ロックが解除された PDF ドキュメントに対して AEM Forms 操作を実行し、ビジネス要件を満たします。例えば、ロック解除された PDF ドキュメントに使用権限を適用する場合、`unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドによって返された `com.adobe.idp.Document` オブジェクトを `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した暗号化された PDF ドキュメントのロック解除](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP モード）

[PDF ドキュメントへの使用権限を適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して暗号化された PDF ドキュメントのロックを解除 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

暗号化 API（web サービス）を使用して、暗号化された PDF ドキュメントのロックを解除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストしているサーバーの IP アドレスに置換します。

1. 暗号化サービスクライアントを作成します。

   * `EncryptionServiceClient` オブジェクトを作成するには、このオブジェクトのデフォルトのコンストラクターを使用します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 暗号化された PDF ドキュメントを取得します。

   * `BLOB` オブジェクトのコンストラクタを使用して、このオブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化された PDF ドキュメントのファイルの場所と、そのファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列のコンテンツを `BLOB` オブジェクトの `MTOM` データメンバーに割り当てて、`BLOB` オブジェクトを入力します。

1. ドキュメントのロックを解除します。

   `EncryptionServiceClient` オブジェクトの `unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドを呼び出して、暗号化された PDFドキュメントをロック解除します。

   パスワードで暗号化された PDF ドキュメントのロックを解除するには、 `unlockPDFUsingPassword` メソッドを呼び出して、次の値を渡します。

   * パスワードで暗号化された PDF ドキュメントを含む `BLOB` オブジェクト。
   * パスワードで暗号化された PDF ドキュメントを開くために使用されるパスワード値を指定する文字列値です。この値は、パスワードで PDF ドキュメントを暗号化する際に指定します。

   証明書で暗号化されている PDF ドキュメントのロックを解除するには、`unlockPDFUsingCredential` メソッドを呼び出して、次の値を渡します。

   * 証明書で暗号化された PDF ドキュメントを表す `BLOB` オブジェクト。
   * PDFドキュメントの暗号化に使用された秘密鍵に対応する公開鍵のエイリアス名を指定する文字列値。

   `unlockPDFUsingPassword` および `unlockPDFUsingCredential` メソッドは両方とも、別の AEM Forms メソッドに渡して操作を実行する `com.adobe.idp.Document` オブジェクトを返します。

1. AEM Forms 操作を実行します。

   ロックが解除された PDF ドキュメントに対して AEM Forms 操作を実行し、ビジネス要件を満たします。例えば、ロック解除された PDF ドキュメントに使用権限を適用する場合、`unlockPDFUsingPassword` または `unlockPDFUsingCredential` メソッドによって返された `BLOB` オブジェクトを `ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドに渡します。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 暗号化タイプの決定 {#determining-encryption-type}

Java 暗号化サービス API または web サービス 暗号化サービス API を使用して、PDF ドキュメントを保護する暗号化の種類をプログラムで判断できます。PDF ドキュメントが暗号化されているかどうか、また暗号化されている場合は、暗号化タイプを動的に判断する必要が生じる場合があります。例えば、PDF ドキュメントをパスワードベースの暗号化で保護するか、Rights Management ポリシーで保護するかを指定できます。

PDF ドキュメントは、次のタイプの暗号化で保護できます。

* パスワードベースの暗号化
* 証明書ベースの暗号化
* Rights Management サービスによって作成されるポリシー
* それ以外のタイプの暗号化

>[!NOTE]
>
>Encryption サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-5}

PDF ドキュメントを保護する暗号化のタイプを判断するには、以下の手順に従います。

1. プロジェクトファイルを含めます。
1. 暗号化サービスクライアントを作成します。
1. 暗号化された PDF ドキュメントを取得します。
1. 暗号化の種類を決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

**サービスクライアントの作成**

プログラムによって暗号化サービスの操作を実行するには、暗号化サービスクライアントを作成する必要があります。Java Encryption Service API を使用している場合は、`EncrytionServiceClient` オブジェクトを作成します。Web サービス Encryption Service API を使用している場合は、`EncryptionServiceService` オブジェクトを作成します。

**暗号化された PDF ドキュメントを取得**

保護する暗号化のタイプを判断するには、PDF ドキュメントを入手する必要があります。

**暗号化タイプの決定**

PDF ドキュメントを保護している暗号化のタイプを判別できます。PDF ドキュメントが保護されていない場合、暗号化サービスは、PDF ドキュメントが保護されていないことを通知します。

**関連項目**

[Java API を使用した暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Web サービス API を使用した暗号化タイプの決定](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption サービス API のクイックスタート](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[ポリシーを使用したドキュメントの保護](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Java API を使用した暗号化タイプの決定 {#determine-the-encryption-type-using-the-java-api}

Encryption API（Java）を使用して、PDF ドキュメントを保護する暗号化タイプを決定します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスにクライアントの JAR ファイル（adobe-livecycle-client.jar など）を含めます。

1. サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`EncryptionServiceClient` オブジェクトを作成します。

1. 暗号化された PDF ドキュメントを取得します。

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列の値を渡すことにより、PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. 暗号化タイプを決定します。

   * `EncryptionServiceClient` オブジェクトの `getPDFEncryption` メソッドを呼び出して、PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡すことにより、暗号化タイプを決定します。このメソッドは、`EncryptionTypeResult` オブジェクトを返します。
   * `EncryptionTypeResult` オブジェクトの `getEncryptionType` メソッドを呼び出します。このメソッドは、暗号化タイプを指定する `EncryptionType` 列挙値を返します。例えば、パスワードベースの暗号化で PDF ドキュメントが保護されている場合、このメソッドは `EncryptionType.PASSWORD` を返します。

**関連項目**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した暗号化タイプの決定](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した暗号化タイプの決定 {#determine-the-encryption-type-using-the-web-service-api}

Encryption API（web サービス）を使用して、PDF ドキュメントを保護する暗号化の種類を決定します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホスティングしているサーバーの IP アドレスに置き換えます。

1. サービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `EncryptionServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`EncryptionServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/EncryptionService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `EncryptionServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `EncryptionServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `EncryptionServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 暗号化された PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出し、暗号化された PDF ドキュメントのファイルの場所と、そのファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `BLOB` オブジェクトの `MTOM` データメンバーに割り当てることにより、`BLOB` オブジェクトに入力します。

1. 暗号化タイプを決定します。

   * `EncryptionServiceClient` オブジェクトの `getPDFEncryption` メソッドを呼び出して、PDF ドキュメントが格納されている `BLOB` オブジェクトを渡します。このメソッドは、 `EncryptionTypeResult` オブジェクトを返します。
   * `EncryptionTypeResult` オブジェクトの `encryptionType` データメソッドの値を取得します。例えば、PDF ドキュメントがパスワードベースの暗号化で保護されている場合、このデータメンバーの値は `EncryptionType.PASSWORD` です。

**関連トピック**

[手順の概要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
