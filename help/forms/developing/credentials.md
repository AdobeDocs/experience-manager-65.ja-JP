---
title: 秘密鍵証明書の操作
seo-title: 秘密鍵証明書の操作
description: 'null'
seo-description: 'null'
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 秘密鍵証明書の操作 {#working-with-credentials}

**秘密鍵証明書サービスについて**

秘密鍵証明書には、ドキュメントへの署名や識別に必要な秘密鍵情報が格納されています。証明書は、信頼のために設定する公開鍵情報です。AEM Formsは、次のような目的で証明書と秘密鍵証明書を使用します。

* Acrobat Reader DC Extensions では、秘密鍵証明書を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。(See [Applying Usage Rights to PDF Documents](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* Signatureサービスは、PDFドキュメントへの電子署名などの操作を実行中に証明書と秘密鍵証明書にアクセスします。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

Trust Manager Java APIを使用して、プログラムによってCredentialサービスとやり取りできます。 次のタスクを実行できます。

* [Trust Manager APIを使用した秘密鍵証明書の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>管理コンソールを使用して、証明書の読み込みと削除を行うこともできます。 (See [administration help.](https://www.adobe.com/go/learn_aemforms_admin_63))

## Trust Manager APIを使用した秘密鍵証明書の読み込み {#importing-credentials-by-using-the-trust-manager-api}

Trust Manager APIを使用して、プログラムによって秘密鍵証明書をAEM Formsに読み込むことができます。 例えば、PDFドキュメントへの署名に使用する秘密鍵証明書を読み込むことができます。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)).

秘密鍵証明書を読み込む場合は、秘密鍵証明書のエイリアスを指定します。 エイリアスは、秘密鍵証明書が必要なForms操作の実行に使用されます。 次の図に示すように、秘密鍵証明書は読み込むと管理コンソールで表示できます。 秘密鍵証明書のエイリアスは *Secureです*。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Webサービスを使用して秘密鍵証明書をAEM Formsに読み込むことはできません。

### 手順の概要 {#summary-of-steps}

秘密鍵証明書をAEM Formsに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 秘密鍵証明書サービスクライアントを作成します。
1. 秘密鍵証明書を参照します。
1. インポート操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**秘密鍵証明書サービスクライアントの作成**

プログラムで秘密鍵証明書をAEM Formsに読み込むには、事前に秘密鍵証明書サービスクライアントを作成する必要があります。 詳しくは、接続プロパティ [の設定を参照してくださ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)い。

**秘密鍵証明書の参照**

AEM Formsに読み込む秘密鍵証明書を参照します。 このセクションに関連するクイックスタートは、ファイルシステム内のP12ファイルを参照します。

**インポート操作の実行**

秘密鍵証明書を参照した後、秘密鍵証明書をAEM Formsに読み込みます。 秘密鍵証明書が正常に読み込まれなかった場合は、例外がスローされます。 秘密鍵証明書を読み込む場合は、秘密鍵証明書のエイリアスを指定します。

**関連トピック**

[Java APIを使用した秘密鍵証明書の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Credential Service APIのクイックスタート](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Java APIを使用した秘密鍵証明書の読み込み {#import-credentials-using-the-java-api}

Trust Manager API(Java)を使用して、秘密鍵証明書をAEM Formsに読み込みます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-truststore-client.jarなどのクライアントJARファイルを含めます。

1. 秘密鍵証明書サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 秘密鍵証明書の参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。秘密鍵証明書の場所を指定するstring値を渡します。
   * コンストラク `com.adobe.idp.Document` ターを使用して、秘密鍵証明書を保存するオブジェクトを作成 `com.adobe.idp.Document` します。 秘密鍵証明書 `java.io.FileInputStream` を含むオブジェクトをコンストラクターに渡します。

1. インポート操作の実行

   * 1つの要素を保持する文字列配列を作成します。 要素に値を割 `truststore.usage.type.sign` り当てます。
   * オブジェクト `CredentialServiceClient` のメソッドを `importCredential` 呼び出し、次の値を渡します。

      * 秘密鍵証明書のエイリアス値を指定するstring値です。
      * 秘密鍵証 `com.adobe.idp.Document` 明書を保存するインスタンスです。
      * 秘密鍵証明書に関連付けられているパスワードを指定するstring値です。
      * 使用状況の値を含む文字列配列。 例えば、この値を指定できます `truststore.usage.type.sign`。 Reader Extension証明書を読み込むには、を指定しま `truststore.usage.type.lcre`す。

**関連トピック**

[Trust Manager APIを使用した秘密鍵証明書の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAPモード）:Java APIを使用した秘密鍵証明書の読み込み](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trust Manager APIを使用した秘密鍵証明書の削除 {#deleting-credentials-by-using-the-trust-manager-api}

Trust Manager APIを使用して、プログラムで秘密鍵証明書を削除できます。 秘密鍵証明書を削除する場合は、秘密鍵証明書に対応するエイリアスを指定します。 一度削除すると、秘密鍵証明書を使用して操作を実行できなくなります。

>[!NOTE]
>
>Webサービスを使用してAEM Formsに秘密鍵証明書を削除することはできません。

### 手順の概要 {#summary_of_steps-1}

秘密鍵証明書を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 秘密鍵証明書サービスクライアントを作成します。
1. 削除操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**秘密鍵証明書サービスクライアントの作成**

プログラムで秘密鍵証明書を削除する前に、Data Integrationサービスクライアントを作成します。 サービスクライアントを作成する場合は、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、接続プロパティ [の設定を参照してくださ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)い。

**削除操作の実行**

秘密鍵証明書を削除するには、秘密鍵証明書に対応するエイリアスを指定します。 存在しないエイリアスを指定した場合は、例外が発生します。

**関連トピック**

[Java APIを使用した秘密鍵証明書の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Java APIを使用した秘密鍵証明書の読み込み](credentials.md#import-credentials-using-the-java-api)

### Java APIを使用した秘密鍵証明書の削除 {#deleting-credentials-using-the-java-api}

Trust Manager API(Java)を使用して、AEM Formsから秘密鍵証明書を削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-truststore-client.jarなどのクライアントJARファイルを含めます。

1. 秘密鍵証明書サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除操作の実行

   オブジェクト `CredentialServiceClient` のメソッドを `deleteCredential` 呼び出し、エイリアス値を指定するstring値を渡します。

**関連トピック**

[Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAPモード）:Java APIを使用した秘密鍵証明書の削除](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
