---
title: Postscript から PDF ドキュメントへの変換
seo-title: Converting Postscript to PDF Documents
description: Distiller サービスを使用して、PostScript®、Encapsulated PostScript（EPS）および PRN ファイルを、ネットワーク上でコンパクトで信頼性の高い、より安全な PDF ファイルに変換します。Distiller サービスは、Java API および web サービス API を使用して、大量の印刷ドキュメントを請求書や明細書などの電子ドキュメントに変換します。
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 100%

---

# Postscript から PDF ドキュメントへの変換 {#converting-postscript-to-pdf-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Distiller サービスについて {#about-the-distiller-service}

Distiller® サービスは、PostScript®、Encapsulated PostScript（EPS）および PRN ファイルを、ネットワーク上でコンパクトで信頼の高い、より安全な PDF ファイルに変換します。Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。

>[!NOTE]
>
>Distiller サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## PostScript を PDF ドキュメントに変換する {#converting-postscript-to-pdf-documents-inner}

このトピックでは、Distiller Service API（Java および web サービス）を使用して、PostScript（PS）、Encapsulated PostScript（EPS）および PRN ファイルをプログラムで PDF ドキュメントに変換する方法について説明します。

>[!NOTE]
>
>Distiller サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>PostScript ファイルを PDF ドキュメントに変換するには、AEM Forms をホストするサーバーに Acrobat 9 または Microsoft Visual C++ 2005 の再頒布可能パッケージ次のいずれかをインストールする必要があります。

### 手順の概要 {#summary-of-steps}

サポートされているタイプのいずれかを PDF ドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Distiller サービスクライアントを作成します。
1. 変換するファイルを取得します。
1. PDF 作成の操作を呼び出します。
1. PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**Distiller サービスクライアントの作成**

プログラムで Distiller サービス操作を実行する前に、Distiller サービスクライアントを作成する必要があります。Java API を使用している場合は、`DistillerServiceClient` オブジェクトを作成します。Web サービス API を使用している場合、`DistillerServiceService` オブジェクトを作成します。

**変換するファイルの取得**

変換するファイルを取得する必要があります。例えば、PS ファイルを PDF ドキュメントに変換するには、PS ファイルを取得する必要があります。

**PDF 作成操作の呼び出し**

サービスクライアントを作成した後で、PDF 作成の操作を呼び出すことができます。この操作を行うには、変換するドキュメントに関する情報（変換先のドキュメントのパスを含む）が必要です。

**PDF ドキュメントの保存**

PDF ドキュメントは、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用して PostScript ファイルを PDF に変換する](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Web サービス API を使用した PostScript ファイルの PDF への変換](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用して PostScript ファイルを PDF に変換する {#convert-a-postscript-file-to-pdf-using-the-java-api}

Distiller Service API（Java）を使用して、PostScript ファイルを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   adobe-distiller-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Distiller サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し `ServiceClientFactory` オブジェクトを渡すことによって、`DistillerServiceClient` オブジェクトを作成します。

1. 変換するファイルを取得します。

   * コンストラクターを使用してファイルの場所を指定する文字列値を渡すことで、変換するファイルを表す `java.io.FileInputStream` オブジェクトを作成します
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF 作成の操作を呼び出します。

   `DistillerServiceClient` オブジェクトの `createPDF` メソッドをを呼び出して、以下の値を渡します。

   * 変換する PS、EPS、または PRN ファイルを表す `com.adobe.idp.Document` オブジェクト
   * 変換するファイルの名前を含む `java.lang.String` オブジェクト
   * 使用する Adobe PDF 設定の名前を含む `java.lang.String` オブジェクト
   * 使用するセキュリティ設定の名前を含む `java.lang.String` オブジェクト
   * PDF ドキュメントの生成時に適用される設定を含むオプションの `com.adobe.idp.Document` オブジェクト
   * PDF ドキュメントに適用されるメタデータ情報を含むオプションの `com.adobe.idp.Document` オブジェクト

   この `createPDF` メソッドは、新しい PDF ドキュメントとログファイル（生成された場合）を含む `CreatePDFResult` オブジェクトを返します。通常、ログファイルには、変換リクエストによって生成されるエラーメッセージや警告メッセージが含まれます。

1. PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `CreatePDFResult` オブジェクトの `getCreatedDocument` メソッドを呼び出します。これにより、`com.adobe.idp.Document` オブジェクトが返されます。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ドキュメントを抽出します。

   同様に、ログドキュメントを取得するには、次の操作を実行します。

   * `CreatePDFResult` オブジェクトの `getLogDocument` メソッドを呼び出します。これは `com.adobe.idp.Document` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出してログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用して PostScript ファイルから PDF ドキュメントに変換](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PostScript ファイルを PDF に変換する {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Distiller Service API（Web サービス）を使用して、PostScript ファイルを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Distiller サービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `DistillerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `DistillerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `DistillerServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `DistillerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `DistillerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトを使用して、PDF ドキュメントに変換するファイルを保存します。
   * コンストラクターを呼び出し、ファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   *  `MTOM` プロパティにバイト配列の内容を割り当てて、`BLOB` オブジェクトに入力します。

1. PDF 作成の操作を呼び出します。

   `DistillerServiceService` オブジェクトの `CreatePDF2` メソッドを呼び出して、次の必須値を渡します。

   * 変換する PS ファイルを表す `BLOB` オブジェクト
   * 変換するファイルのパス名を含む文字列
   * 使用する Adobe PDF 設定を含む文字列オブジェクト（例えば `Standard`）
   * 使用するセキュリティ設定を含む文字列オブジェクト（例えば `No Securit`y）
   * PDF ドキュメントの生成時に適用される設定を含む オプションの `BLOB` オブジェクト
   * PDF ドキュメントに適用するメタデータ情報を含むオプションの `BLOB` オブジェクト
   * PDF ドキュメントの保存に使用する `BLOB` 出力パラメータ
   * ログの保存に使用する `BLOB` 出力パラメーター

1. PDF ドキュメントを保存します。

   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。署名済み PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `CreatePDF2` メソッド（出力パラメーター）によって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列に入力します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
