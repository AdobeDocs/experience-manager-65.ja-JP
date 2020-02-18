---
title: Java API quickStartの概要
seo-title: Java API quickStartの概要
description: 'null'
seo-description: 'null'
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Java APIの概要クイックスタート {#introducing-java-api-quickstart}

Adobe AEM Forms APIクイックスタートは、AEM Formsサービスとやり取りするプログラムの開発に向けての取り組みを加速するお手伝いをします。 *クイッ*&#x200B;クスタートは、独自のプロジェクトにコピーして貼り付け、開始点として使用できる完全なプログラムです。 クイックスタートを実行して、その動作を確認し、独自のニーズに合わせて変更することができます。

AEM Formsの操作は、AEM Formsの厳密に型指定されたAPIを使用して実行でき、接続モードをSOAPに設定する必要があります。

Javaで厳密に型指定されたAPIクイックスタートでは、Javaアプリケーションの実行に必要なJARファイルのリストが提供されます。 ほとんどのJavaクイックスタートは、内で実行するコンソールアプリケーションで `main`す。 ただし、Forms javaの厳密に型指定されたAPIクイックスタートは、Webアプリケーション内で実行するJavaサーブレットとして実装されます。

JARファイルのリストは、クイックスタートの先頭にあるコメントセクションにあります。 例えば、次のコメントはOutputクイックスタートにあり、各Javaクイックスタートに含まれる一般的なJARファイルのリストです。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 複数のサービスのクイックスタート {#multiple-services-quick-start}

ほとんどのクイックスタートは、「JEE上のAEM Forms *によるプログラミング」にあり* 、操作を実行するために特定のサービスを呼び出します。 ただし、一部のクイックスタートでは、特定のワークフローを実行するために複数のAEM Formsサービスを呼び出します。 複数のAEM Formsサービスを呼び出すJavaクイックスタートを次に示します。

[クイックスタート（SOAPモード）:Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （RepositoryとOutputサービスを呼び出す）

[クイックスタート（SOAPモード）:Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （AssemblerおよびOutputサービスを呼び出す）

[クイックスタート（SOAPモード）:Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) （Forms、OutputおよびDocument Managementサービスを呼び出す）を使用した送信済みXMLデータを使用したPDFドキュメントの作成

[クイックスタート（SOAPモード）:Java APIを使用してFormsサービスにドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) （FormsとDocument Managementサービスを呼び出す）

[クイックスタート（SOAPモード）:Java APIを使用したXFAベースのフォームへの電子署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) （Forms and Signatureサービスを呼び出す）

[クイックスタート（SOAPモード）:Java APIを使用したロールと権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （DirectoryManagerおよびAuthorizationManagerサービスを呼び出す）

[クイックスタート（SOAPモード）:Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （OutputおよびDocument Managementサービスを呼び出す）

>[!NOTE]
>
>「AEM formsによるプログラミング」にあるクイックスタートは、JBoss® Application serverおよびMicrosoft® Windows®オペレーティングシステムにデプロイされるAEM Formsに基づいています。 ただし、UNIX®など別のオペレーティングシステムを使用している場合は、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを必ず指定してください。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>WebサービスのクイックスタートのほとんどはC#で記述され、.NET Frameworkを使用します。 ただし、SOAP標準をサポートする任意の開発環境でAEM Formsサービスを呼び出すことができるクライアントアプリケーションロジックを作成できます。 (See [Invoking AEM Forms Using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

