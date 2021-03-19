---
title: 秘密鍵証明書の操作
seo-title: 秘密鍵証明書の操作
description: Trust Manager APIとJava APIを使用して秘密鍵証明書をAEM Formsに読み込みます。 さらに、Trust Manager APIとJava APIを使用して秘密鍵証明書を削除する方法を説明します。
seo-description: Trust Manager APIとJava APIを使用して秘密鍵証明書をAEM Formsに読み込みます。 さらに、Trust Manager APIとJava APIを使用して秘密鍵証明書を削除する方法を説明します。
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: デベロッパー
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 11%

---


# 資格情報の操作{#working-with-credentials}

**このドキュメントのサンプルと例は、JEE環境上のAEM Formsに対してのみ提供されています。**

**秘密鍵証明書サービスについて**

秘密鍵証明書には、ドキュメントへの署名や識別に必要な秘密鍵情報が格納されています。証明書は、信頼のために設定する公開鍵情報です。AEM Formsは、次のような目的で証明書と秘密鍵証明書を使用します。

* Acrobat Reader DC Extensions では、秘密鍵証明書を使用して、PDF ドキュメントで Adobe Reader の使用権限を有効にします。(「[PDFドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)」を参照)。
* Signatureサービスは、PDFドキュメントのデジタル署名などの操作を実行する際に、証明書と秘密鍵証明書にアクセスします。 (「[PDFドキュメントのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)」を参照)。

Trust Manager Java APIを使用して、プログラムによって秘密鍵証明書サービスを操作できます。 次のタスクを実行できます。

* [Trust Manager APIを使用した秘密鍵証明書の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>管理コンソールを使用して、証明書の読み込みと削除を行うこともできます。 （[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63)を参照）。

## Trust Manager API {#importing-credentials-by-using-the-trust-manager-api}を使用した秘密鍵証明書の読み込み

Trust Manager APIを使用すると、プログラムによって秘密鍵証明書をAEM Formsに読み込むことができます。 例えば、PDFドキュメントへの署名に使用する秘密鍵証明書を読み込むことができます。 (「[PDFドキュメントのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)」を参照)。

秘密鍵証明書を読み込む場合は、秘密鍵証明書のエイリアスを指定します。 エイリアスは、秘密鍵証明書を必要とするForms操作の実行に使用されます。 次の図に示すように、読み込んだ秘密鍵証明書は、管理コンソールで表示できます。 秘密鍵証明書のエイリアスは&#x200B;*Secure*&#x200B;です。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>Webサービスを使用して秘密鍵証明書をAEM Formsに読み込むことはできません。

### 手順{#summary-of-steps}の概要

秘密鍵証明書をAEM Formsに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 秘密鍵証明書サービスクライアントを作成します。
1. 秘密鍵証明書を参照します。
1. インポート操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**秘密鍵証明書サービスクライアントの作成**

プログラムで秘密鍵証明書をAEM Formsに読み込む前に、秘密鍵証明書サービスクライアントを作成します。 詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**秘密鍵証明書の参照**

AEM Formsに読み込む秘密鍵証明書を参照します。 このセクションに関連付けられたクイック開始は、ファイルシステム内のP12ファイルを参照します。

**インポート操作の実行**

秘密鍵証明書を参照した後、秘密鍵証明書をAEM Formsに読み込みます。 秘密鍵証明書が正常に読み込まれない場合は、例外が発生します。 秘密鍵証明書を読み込む場合は、秘密鍵証明書のエイリアスを指定します。

**関連トピック**

[Java APIを使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Credential Service APIのクイック開始](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### Java API {#import-credentials-using-the-java-api}を使用した秘密鍵証明書の読み込み

Trust Manager API(Java)を使用して秘密鍵証明書をAEM Formsに読み込みます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-truststore-client.jarなどのクライアントJARファイルを含めます。

1. 秘密鍵証明書サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 秘密鍵証明書の参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。秘密鍵証明書の場所を指定するstring値を渡します。
   * `com.adobe.idp.Document`コンストラクターを使用して、秘密鍵証明書を保存する`com.adobe.idp.Document`オブジェクトを作成します。 秘密鍵証明書を含む`java.io.FileInputStream`オブジェクトをコンストラクターに渡します。

1. インポート操作の実行

   * 1つの要素を格納する文字列配列を作成します。 要素に値`truststore.usage.type.sign`を割り当てます。
   * `CredentialServiceClient`オブジェクトの`importCredential`メソッドを呼び出し、次の値を渡します。

      * 秘密鍵証明書のエイリアス値を指定するstring値です。
      * 秘密鍵証明書を保存する`com.adobe.idp.Document`インスタンスです。
      * 秘密鍵証明書に関連付けられているパスワードを指定するstring値です。
      * 使用状況の値を格納する文字列配列。 例えば、`truststore.usage.type.sign`という値を指定できます。 Reader拡張機能の証明書を読み込むには、`truststore.usage.type.lcre`を指定します。

**関連トピック**

[Trust Manager APIを使用した秘密鍵証明書の読み込み](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[クイック開始（SOAPモード）:Java APIを使用した秘密鍵証明書の読み込み](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Trust Manager API {#deleting-credentials-by-using-the-trust-manager-api}を使用した秘密鍵証明書の削除

Trust Manager APIを使用すると、プログラムによって秘密鍵証明書を削除できます。 秘密鍵証明書を削除する場合は、秘密鍵証明書に対応するエイリアスを指定します。 一度削除すると、秘密鍵証明書を使用して操作を実行できなくなります。

>[!NOTE]
>
>Webサービスを使用して、秘密鍵証明書をAEM Formsに削除することはできません。

### 手順{#summary_of_steps-1}の概要

秘密鍵証明書を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. 秘密鍵証明書サービスクライアントを作成します。
1. 削除操作を実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**秘密鍵証明書サービスクライアントの作成**

プログラムで秘密鍵証明書を削除する前に、Data Integration Serviceクライアントを作成します。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**削除操作の実行**

秘密鍵証明書を削除するには、秘密鍵証明書に対応するエイリアスを指定します。 存在しないエイリアスを指定すると、例外が発生します。

**関連トピック**

[Java APIを使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Java APIを使用した資格情報の読み込み](credentials.md#import-credentials-using-the-java-api)

### Java API {#deleting-credentials-using-the-java-api}を使用した秘密鍵証明書の削除

Trust Manager API(Java)を使用して、AEM Formsから秘密鍵証明書を削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-truststore-client.jarなどのクライアントJARファイルを含めます。

1. 秘密鍵証明書サービスクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `CredentialServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除操作の実行

   `CredentialServiceClient`オブジェクトの`deleteCredential`メソッドを呼び出し、エイリアス値を指定する文字列値を渡します。

**関連トピック**

[Trust Manager APIを使用した秘密鍵証明書の削除](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[クイック開始（SOAPモード）:Java APIを使用した秘密鍵証明書の削除](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
