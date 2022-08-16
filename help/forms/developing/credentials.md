---
title: 資格情報の操作
seo-title: Working with Credentials
description: Trust Manager API と Java API を使用して、秘密鍵証明書を AEM Forms に読み込みます。さらに、Trust Manager API と Java API を使用して秘密鍵証明書を削除する方法についても説明します。
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 100%

---

# 資格情報の操作 {#working-with-credentials}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**認証情報サービスについて**

秘密鍵証明書には、ドキュメントへの署名や識別に必要な秘密鍵情報が格納されています。証明書は、信頼のために設定する公開鍵情報です。AEM Forms が証明書と秘密鍵証明書を使用する目的はいくつかあります。

* Acrobat Reader DC Extensions では、秘密鍵証明書を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。（[PDF ドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照。）
* Signature サービスは、PDF ドキュメントへのデジタル署名などの操作を実行しながら、証明書および秘密鍵証明書にアクセスします。（[PDF ドキュメントへのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照。）

Trust Manager Java API を使用して、Credential サービスとプログラム経由で対話を行うことができます。次のタスクを実行できます。

* [Trust Manager API を使用した認証情報の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>管理コンソールを使用して証明書の読み込みおよび削除を行うこともできます。（[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63_jp)を参照。）

## Trust Manager API を使用した認証情報の読み込み {#importing-credentials-by-using-the-trust-manager-api}

Trust Manager API を使用して、プログラム経由で秘密鍵証明書を AEM Forms に読み込むことができます。例えば、PDF ドキュメントへの署名に使用する秘密鍵証明書を読み込むことができます。（[PDF ドキュメントへのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照。）

秘密鍵証明書を読み込む際は、秘密鍵証明書のエイリアスを指定します。エイリアスは、秘密鍵証明書を必要とする Forms 操作を実行する際に使用されます。次の図に示すように、読み込んだ秘密鍵証明書は管理コンソールで表示できます。秘密鍵証明書のエイリアスは「*Secure*」です。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Web サービスを使用して AEM Forms に秘密鍵証明書を読み込むことはできません。

### 手順の概要 {#summary-of-steps}

秘密鍵証明書を AEM Forms に読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 資格情報サービスクライアントを作成します。
1. 秘密鍵証明書を参照します。
1. 読み込み操作を実行します。

**プロジェクトファイルのインクルード**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**認証情報サービスクライアントの作成**

プログラム経由で秘密鍵証明書を AEM Forms に読み込む前に、認証情報サービスクライアントを作成します。詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**秘密鍵証明書の参照**

AEM Forms に読み込む秘密鍵証明書を参照します。このセクションに関連するクイックスタートは、ファイルシステム内の P12 ファイルを参照します。

**読み込み操作の実行**

認証情報を参照した後、その認証情報を AEM Forms に読み込みます。認証情報が正常に読み込まれない場合は、例外がスローされます。認証情報を読み込む際は、認証情報のエイリアスを指定します。

**関連トピック**

[Java API を使用した認証情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Credential Service API のクイックスタート](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Java API を使用した認証情報の読み込み {#import-credentials-using-the-java-api}

Trust Manager API（Java）を使用して、認証情報を AEM Forms に読み込みます。

1. プロジェクトファイルを含める

   adobe-truststore-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. 認証情報サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 認証情報の参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。認証情報の場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document` コンストラクターを使用して、認証情報を保存する `com.adobe.idp.Document` オブジェクトを作成します。コンストラクターの認証情報が格納された `java.io.FileInputStream` オブジェクトを渡します。

1. 読み込み操作の実行

   * 1 つの要素を持つ文字列配列を作成します。値 `truststore.usage.type.sign` を要素に割り当てます。
   * `CredentialServiceClient` オブジェクトの `importCredential` メソッドを呼び出して、次の値を渡します。

      * 認証情報のエイリアス値を指定する文字列値です。
      * 認証情報を保存する `com.adobe.idp.Document` インスタンス。
      * 資格情報に関連付けられるパスワードを指定する文字列値です。
      * 使用量値を含む文字列配列です。例えば、この値として `truststore.usage.type.sign` を指定します。Reader Extension 資格情報をインポートするには、`truststore.usage.type.lcre` を指定します。

**関連トピック**

[Trust Manager API を使用した認証情報の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAP モード）：Java API を使用した資格情報のインポート](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trust Manager API を使用した資格情報の削除 {#deleting-credentials-by-using-the-trust-manager-api}

Trust Manager API を使用すると、プログラムにより資格情報を削除できます。資格情報を削除する際には、資格情報に対応するエイリアスを指定します。削除した後は、資格情報を使用して操作を実行できません。

>[!NOTE]
>
>Web サービスを使用して AEM Forms の資格情報を削除することはできません。

### 手順の概要 {#summary_of_steps-1}

資格情報を削除するには、以下の手順を実行します。

1. プロジェクトファイルを含めます。
1. 資格情報サービスクライアントを作成します。
1. 削除操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**資格情報サービスクライアントの作成**

プログラムによって資格情報を削除する前に、Data Integration サービスクライアントを作成します。サービスクライアントを作成する際は、サービスを呼び出すために必要な接続設定を定義します。詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**削除操作の実行**

資格情報を削除するには、資格情報に対応するエイリアスを指定します。存在しないエイリアスを指定すると、例外が発生します。

**関連トピック**

[Java API を使用した認証情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API を使用した認証情報の読み込み](credentials.md#import-credentials-using-the-java-api)

### Java API を使用した資格情報の削除 {#deleting-credentials-using-the-java-api}

Trust Manager API（Java）を使用して、AEM Forms から資格情報を削除します。

1. プロジェクトファイルを含める

   adobe-truststore-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. 認証情報サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除操作の実行

   `CredentialServiceClient` オブジェクトの `deleteCredential` メソッドを呼び出して、エイリアス値を指定する文字列値を渡します。

**関連トピック**

[Trust Manager API を使用した資格情報の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[クイックスタート（SOAP モード）：Java API を使用した資格情報の削除](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
