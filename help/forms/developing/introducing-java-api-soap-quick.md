---
title: Java API QuickStartの概要
seo-title: Java API QuickStartの概要
description: 'null'
seo-description: 'null'
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---


# Java APIクイック開始の概要 {#introducing-java-api-quickstart}

AdobeAEM FormsAPIクイック開始は、AEM Formsサービスとやり取りするプログラムの開発に向けた取り組みを迅速化するのに役立ちます。 *クイック*&#x200B;開始は完全なプログラムで、独自のプロジェクトにコピーして貼り付け、開始点として使用できます。 クイック開始を実行して、動作を確認し、必要に応じて変更することができます。

AEM Forms操作は、厳密に型指定されたAPIをAEM Formsを使用して実行できます。接続モードはSOAPに設定する必要があります。

Java厳密に型指定されたAPIクイック開始は、Javaアプリケーションの実行に必要なJARファイルのリストを提供します。 ほとんどのJavaクイック開始は、内で実行されるコンソールアプリケーションで `main`す。 ただし、Forms Javaの厳密に型指定されたAPIクイック開始は、Webアプリケーション内で実行されるJavaサーブレットとして実装されます。

JARファイルのリストは、クイック開始の先頭にあるコメントセクションにあります。 例えば、次のコメントはOutputクイック開始にあり、各Javaクイック開始に含まれる一般的なJARファイルリストです。

```java
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

## 複数のサービスのクイック開始 {#multiple-services-quick-start}

「JEE上のAEM Formsの *プログラミング」にあるほとんどのクイック開始は、操作を実行するために特定のサービスを呼び出します* 。 ただし、一部のクイック開始は、特定のワークフローを実行するために複数のAEM Formsサービスを呼び出します。 次のリストは、複数のAEM Formsサービスを呼び出すJavaクイック開始を提供します。

[クイック開始（SOAPモード）: Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （RepositoryとOutputサービスを呼び出す）

[クイック開始（SOAPモード）: Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （AssemblerとOutputサービスを呼び出す）

[クイック開始（SOAPモード）: Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (Forms、Output、およびドキュメント管理サービスを呼び出す)を使用して、送信済みのXMLデータを使用してPDFドキュメントを作成する

[クイック開始（SOAPモード）: Java APIを使用してFormsサービスにドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (Formsおよびドキュメント管理サービスを呼び出す)

[クイック開始（SOAPモード）: Java API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) （FormsとSignatureサービスを呼び出す）を使用したXFAベースのフォームの電子署名

[クイック開始（SOAPモード）: Java APIを使用したロールと権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （DirectoryManagerおよびAuthorizationManagerサービスを呼び出す）

[クイック開始（SOAPモード）: Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (Outputおよびドキュメント管理サービスを呼び出す)を使用してOutputサービスにドキュメントを渡す

>[!NOTE]
>
>「AEM Formsを使用したプログラミング」にあるクイック開始は、JBoss® Application ServerおよびMicrosoft® Windows®オペレーティングシステムにデプロイされているAEM Formsに基づいています。 ただし、UNIX®など別のオペレーティングシステムを使用している場合は、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを指定していることを確認してください。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>ほとんどのWebサービスクイック開始はC#で記述され、.NET Frameworkを使用します。 ただし、SOAP標準をサポートする任意の開発環境でAEM Formsサービスを呼び出すことができるクライアントアプリケーションロジックを作成できます。 (See [Invoking AEM Forms Using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

