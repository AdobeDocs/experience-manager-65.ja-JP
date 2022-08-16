---
title: Java API クイックスタートの概要
seo-title: Introducing Java API QuickStart
description: Java API クイックスタートの概要
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 100%

---

# Java API クイックスタートの概要 {#introducing-java-api-quickstart}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Adobe AEM Forms API クイックスタートは、AEM Forms サービスとやり取りするプログラムの開発に向けた取り組みを加速するのに役立ちます。*クイックスタート*&#x200B;は、独自のプロジェクトにコピーして貼り付け、出発点として使用できる完全なプログラムです。クイックスタートを実行して、動作を確認し、独自のニーズに合わせて変更できます。

AEM Forms の操作は、AEM Forms の厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

Java の厳密に型指定された API クイックスタートには、Java アプリケーションの実行に必要な JAR ファイルのリストが表示されます。ほとんどの Java クイックスタートは、`main` 内で実行されるコンソールアプリケーションです。ただし、Forms Java の厳密に型指定された API クイックスタートは、web アプリケーション内で実行する Java サーブレットとして実装されます。

JAR ファイルのリストは、クイックスタートの先頭にあるコメントセクションにあります。例えば、次のコメントは Output クイックスタートにあり、各 Java クイックスタートにある一般的な JAR ファイルリストです。

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

## 複数のサービスのクイックスタート {#multiple-services-quick-start}

*AEM Forms on JEE を使用したプログラミング*&#x200B;にあるほとんどのクイックスタートは、ある1 つのサービスを呼び出すことで操作を実行します。ただし、一部のクイックスタートでは、複数の AEM Forms サービスを呼び出すことで特定のワークフローを実行します。次のリストは、複数の AEM Forms サービスを呼び出す Java クイックスタートを示しています。

[クイックスタート（SOAP モード）：Java API を使用して、AEM Forms リポジトリ内のドキュメントを Output サービスに渡します](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （Repository サービスと Output サービスを呼び出します）

[クイックスタート（SOAP モード）：Java API を使用して、フラグメントに基づく PDF ドキュメントを作成します](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （Assembler サービスと Output サービスを呼び出します）

[クイックスタート（SOAP モード）：Java API を使用して、送信済み XML データで PDFドキュメントを作成します](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)（Forms サービス、Output サービス、Document Management サービスを呼び出します）

[クイックスタート（SOAP モード）：Java API を使用して、Forms サービスにドキュメントを渡します](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)（Forms サービスと Document Management サービスを呼び出します）

[クイックスタート（SOAP モード）：Java API を使用して、XFA ベースのフォームにデジタル署名をします](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)（Forms サービスと Signature サービスを呼び出します）

[クイックスタート（SOAP モード）：Java API を使用して、役割と権限を管理します](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （DirectoryManager サービスと AuthorizationManager サービスを呼び出します）。

[クイックスタート（SOAP モード）：Java API を使用して、Output サービスにドキュメントを渡します](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （Output サービスと Document Management サービスを呼び出します）

>[!NOTE]
>
>「AEM Forms のプログラミング」にあるクイックスタートは、JBoss® Application Server と Microsoft® Windows® オペレーティングシステムにデプロイされる AEM Forms に基づいています。ただし、UNIX® などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを該当するオペレーティングシステムでサポートされているパスに置き換えます。同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>ほとんどの web サービスのクイックスタートは、C# で記述され、.NET フレームワークを使用します。ただし、SOAP 標準をサポートする任意の開発環境で、AEM Forms サービスを呼び出せるクライアントアプリケーションロジックを作成できます。（[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)を参照。）
