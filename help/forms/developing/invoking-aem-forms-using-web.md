---
title: Web サービスを使用した AEM Forms の呼び出し
seo-title: Invoking AEM Forms using Web Services
description: WSDL 生成を完全にサポートする web サービスを使用して、AEM Forms プロセスを呼び出します。
seo-description: Invoke AEM Forms processes using web services with full support for WSDL generation.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '9905'
ht-degree: 100%

---

# Web サービスを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-web-services}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

サービスコンテナー内の AEM Forms サービスのほとんどは、web サービスを公開するように設定され、web サービス定義言語（WSDL）の生成が完全にサポートされています。つまり、AEM Forms サービスのネイティブ SOAP スタックを使用するプロキシオブジェクトを作成できます。その結果、AEM Forms サービスは以下の SOAP メッセージを交換して処理できます。

* **SOAP リクエスト**：アクションをリクエストするクライアントアプリケーションによって Forms サービスに送信されます。
* **SOAP 応答**：SOAP リクエストの処理後に、Forms サービスによってクライアントアプリケーションに送信されます。

Web サービスを使用すると、Java API を使用して実行できる操作と同じ AEM Forms サービス操作を実行できます。Web サービスを使用して AEM Forms サービスを呼び出す利点の 1 つは、SOAP をサポートする開発環境でクライアントアプリケーションを作成できることです。クライアントアプリケーションは、特定の開発環境やプログラミング言語にバインドされていません。例えば、Microsoft Visual Studio .NET と C# をプログラミング言語として使用して、クライアントアプリケーションを作成できます。

AEM Forms サービスは、SOAP プロトコルで公開され、WSI Basic Profile 1.1 に準拠しています。Web Services Interoperability（WSI）は、プラットフォーム間での web サービスの相互運用性を促進するオープンスタンダード組織です。詳しくは、[https://www.ws-i.org/](https://www.ws-i.org) を参照してください。

AEM Forms は、以下の web サービス標準規格をサポートしています。

* **エンコード**：ドキュメントおよびリテラルエンコーディング（WSI Basic Profile に準拠した推奨エンコーディング）のみがサポートされます（[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding)を参照）。
* **MTOM**：SOAP リクエストで添付ファイルをエンコードする方法を表します（[MTOM を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-mtom)を参照）。
* **SwaRef**：SOAP リクエストで添付ファイルをエンコードする別の方法を表します（[SwaRef を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-swaref)を参照）。
* **添付ファイル付き SOAP**：MIME と DIME（Direct Internet Message Encapsulation）の両方をサポートします。これらのプロトコルは、SOAP 経由で添付ファイルを送信する標準的な方法です。Microsoft Visual Studio .NET アプリケーションは DIME を使用します（[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding)を参照）。
* **WS-Security**：ユーザー名パスワードトークンプロファイルをサポートします。このプロファイルは、WS Security SOAP ヘッダーの一部としてユーザー名とパスワードを送信する標準的な方法です。AEM Forms は、HTTP 基本認証もサポートしています。秒

Web サービスを使用して AEM Forms サービスを呼び出すには、通常、サービス WSDL を使用するプロキシライブラリを作成します。この *Web サービスを使用した AEM Forms の呼び出し*&#x200B;節では、JAX-WS を使用して Java プロキシクラスを作成し、サービスを呼び出します（[JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)を参照）。

以下の URL 定義を指定して、サービス WDSL を取得できます（括弧で囲まれた項目は任意です）。

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

各パラメーターの意味は次のとおりです。

* *your_serverhost* は、AEM Forms をホストする J2EE アプリケーションサーバーの IP アドレスを表します。
* *your_port* は、J2EE アプリケーションサーバーが使用する HTTP ポートを表します。
* *service_name* は、サービス名を表します。
* *version* は、サービスのターゲットバージョンを表します（デフォルトでは最新のサービスバージョンが使用されます）。
* `async` は `true` 値を指定して、非同期呼び出しの追加操作を有効にします（デフォルトでは `false`）。
* *lc_version* は、呼び出す AEM Forms のバージョンを表します。

以下の表に、サービスの WSDL 定義を示します（AEM Forms がローカルホストにデプロイされ、投稿数が 8080 である場合）。

<table>
 <thead>
  <tr>
   <th><p>サービス</p></th>
   <th><p>WSDL の定義</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assembler</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Back と Restore</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>バーコードフォーム</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Convert PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>暗号化 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms のデータ統合機能</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generate PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Generate 3D PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>出力</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF Utilities </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Acrobat Reader DC エクステンション</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>リポジトリー</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>シグネチャ </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP Utilities</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms Process WSDL の定義**

Workbench で作成されたプロセスに属する WSDL にアクセスするには、WSDL 定義内でアプリケーション名とプロセス名を指定する必要があります。アプリケーション名が `MyApplication` で、プロセス名が `EncryptDocument` であると仮定します。この場合、以下の WSDL 定義を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>`MyApplication/EncryptDocument` 短時間のみ有効なプロセスの例について詳しくは、[短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md) を参照してください。

>[!NOTE]
>
>アプリケーションには、フォルダーを含めることができます。この場合、WSDL 定義内でフォルダー名を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Web サービスを使用した新しい機能へのアクセス**

新しい AEM Forms サービス機能には、web サービスを使用してアクセスできます。例えば AEM Forms には、MTOM を使用して添付ファイルをエンコードする機能が導入されました。（[MTOM を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-mtom) を参照してくださ）。

AEM Forms に導入された新機能にアクセスするには、WSDL 定義で `lc_version` フィールド名を設定します。例えば、新しいサービス機能（MTOM のサポートを含む）にアクセスするには、次の WSDL 定義を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>`lc_version` フィールド名を設定する際は、必ず 3 桁の数字を使用します。例えば 9.0.1 は、バージョン 9.0 と等しくなります。

**Web サービス BLOB データタイプ**

AEM Forms サービス WSDL は、多くのデータタイプを定義します。Web サービスで公開される最も重要なデータタイプの 1 つは、`BLOB` タイプです。このデータタイプは、AEM Forms Java API を使用する場合、`com.adobe.idp.Document` クラスにマッピングされます。（[Java API を使用した AEM Forms サービスへのデータの引き渡し](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)を参照してください）。

`BLOB` オブジェクトは、AEM Forms サービスとの間でバイナリデータ（PDF ファイル、XML データなど）を送受信します。`BLOB` タイプは、サービス WSDL で次のように定義されます。

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

`MTOM` および `swaRef` フィールドは、AEM Forms でのみサポートされます。これらの新しいフィールドは、`lc_version` プロパティを含む URL を指定した場合にのみ使用できます。

**サービスリクエストでの BLOB オブジェクトの供給**

AEM Forms サービス操作が `BLOB` タイプを入力値として要求する場合、`BLOB` タイプのインスタンスを、アプリケーションロジック内に作成します。（*AEM Forms によるプログラミング* にある多くの web サービスのクイックスタートは、 BLOB データタイプの操作方法を示します）。

`BLOB` インスタンスに属するフィールドには、次のように値を割り当てます。

* **Base64**：データを Base64 形式でエンコードされたテキストとして渡すには、`BLOB.binaryData` フィールドにデータを設定し、`BLOB.contentType` フィールドに MIME 形式でデータタイプ（例：`application/pdf`）を設定します。（[Base64 エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding) を参照してください）。
* **MTOM**：MTOM 添付ファイルにバイナリデータを渡すには、`BLOB.MTOM` フィールドにデータを設定します。この設定により、Java JAX-WS フレームワークまたは SOAP フレームワークのネイティブ API を使用して、SOAP リクエストにデータが添付されます。（[MTOM を使用した AEM Forms の呼び出し ](#invoking-aem-forms-using-mtom) を参照してください）。
* **SwaRef**：WS-I SwaRef 添付ファイルにバイナリデータを渡すには、`BLOB.swaRef` フィールドにデータを設定します。この設定により、Java JAX-WS フレームワークを使用して、SOAP リクエストにデータが添付されます。（[SwaRef を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-swaref) を参照してください）。
* **MIME または DIME 添付ファイル**：MIME または DIME 添付ファイルにデータを渡すには、SOAP フレームワークのネイティブ API を使用して、SOAP リクエストにデータを添付します。添付ファイル識別情報を `BLOB.attachmentID` フィールドに設定します。（[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding) を参照してください）。
* **リモート URL**：データが web サーバーでホストされ、HTTP URL 経由でアクセス可能な場合は、HTTP URL を `BLOB.remoteURL` フィールドに設定します。（[HTTP 経由の BLOB データを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-blob-data-over-http) を参照してください）。

**サービスから返された BLOB オブジェクト内のデータへのアクセス**

返された `BLOB` オブジェクトの送信プロトコルは、いくつかの要因に依存しますが、これは次の順序で考慮され、主な条件が満たされた場合に停止します。

1. **ターゲット URL は送信プロトコルを指定します**。SOAP 呼び出しで指定されたターゲット URL に `blob="`*BLOB_TYPE* というパラメーターでが含まれる場合、*BLOB_TYPE* は送信プロトコルを決定します。*BLOB_TYPE* は、base64、dime、mime、http、mtom や swaref のプレースホルダーです。
1. **サービス SOAP エンドポイントがスマートです**。次の条件が true の場合、出力ドキュメントは入力ドキュメントと同じ送信プロトコルを使用して返されます。

   * サービスの SOAP エンドポイントパラメーターの出力 BLOB オブジェクトのデフォルトプロトコルは、スマートに設定されています。

      SOAP エンドポイントを持つ各サービスについて、管理コンソールを使用して、返された BLOB の送信プロトコルを指定できます。（[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63_jp)を参照してください）。

   * AEM Forms サービスは、1 つ以上のドキュメントを入力として取得します。

1. **サービス SOAP エンドポイントがスマートではありません**。設定されたプロトコルがドキュメント送信プロトコルを決定し、データは対応する `BLOB` フィールドに返されます。例えば、SOAP エンドポイントが DIME に設定されている場合、返される BLOB は入力ドキュメントの送信プロトコルに関係なく、`blob.attachmentID` フィールドにあります。
1. **それ以外の場合**。サービスがドキュメントタイプを入力として取得しない場合、出力ドキュメントは HTTP プロトコル経由で `BLOB.remoteURL` のフィールドに返されます。

最初の条件で説明したように、以下のようなサフィックスを付けて SOAP エンドポイント URL を拡張することで、返されるドキュメントの送信タイプを確認できます。

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

次に、送信タイプとデータの取得元のフィールドとの相関性を示します。

* **Base64 形式**：`blob` サフィックスを `base64` に設定すると、`BLOB.binaryData` フィールドのデータが返されます。
* **MIME または DIME 添付ファイル**：`blob` サフィックスを `DIME` または `MIME` に設定すると、`BLOB.attachmentID` フィールドに返された添付ファイルの識別情報と併せて、データを対応する添付ファイルタイプとして返します。 SOAP フレームワーク独自の API を使用して、添付ファイルからデータを読み取ります。
* **リモート URL**：`blob` サフィックスを `http` に設定すると、アプリケーションサーバー上のデータを保持し、`BLOB.remoteURL` フィールドにあるデータを指す URL を返します。
* **MTOM または SwaRef**：`blob` サフィックスを `mtom` または `swaref` に設定すると、`BLOB.MTOM` または `BLOB.swaRef` フィールドに返された添付ファイルの識別情報と併せて、データを対応する添付ファイルタイプとして返します。SOAP フレームワークのネイティブ API を使用して、添付ファイルからデータを読み取ります。

>[!NOTE]
>
>`BLOB` オブジェクトの `setBinaryData` メソッドを呼び出して入力する場合、30 MB を超えないようにすることが推奨されます。超えてしまうと、`OutOfMemory` 例外が発生する可能性があります。

>[!NOTE]
>
>MTOM 送信プロトコルを使用する JAX WS ベースのアプリケーションは、送受信データが 25 MB に制限されています。 この制限は、JAX-WS のバグが原因です。 送受信ファイルの合計サイズが 25 MB を超える場合は、MTOM プロトコルの代わりに SwaRef 送信プロトコルを使用します。 そうしないと、 `OutOfMemory` 例外が発生する可能性があります。

**base64 でエンコードされたバイト配列の MTOM 送信**

さらに `BLOB` オブジェクトの場合、MTOM プロトコルは、任意の複合型の byte-array パラメーターまたは byte-array フィールドをサポートします。 つまり、MTOM をサポートするクライアント SOAP フレームワークは、任意の `xsd:base64Binary` 要素を（base64 エンコードされたテキストの代わりに）MTOM 添付ファイルとして送信します。AEM Forms SOAP エンドポイントは、この種のバイト配列エンコーディングを読み取ることができます。ただし AEM Forms サービスは常に、base64 エンコードされたテキストとしてバイト配列型を返します。 出力バイト配列パラメーターは MTOM をサポートしていません。

大量のバイナリデータを返す AEM Forms サービスでは、バイト配列タイプではなく Document/BLOB タイプを使用します。 このドキュメントタイプは、大量のデータを送信する場合に、より効率的です。

## Web サービスのデータタイプ {#web-service-data-types}

次の表に、Java データタイプと、対応する web サービスデータタイプを示します。

<table>
 <thead>
  <tr>
   <th><p>Java データタイプ</p></th>
   <th><p>Web サービスのデータタイプ</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>この <code>DATE</code> タイプは、サービス WSDL で次のように定義されています。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms サービスの操作で <code>java.util.Date</code> 値を入力として取得する場合、SOAP クライアントアプリケーションは、日付を <code>DATE.date</code> フィールドに渡す必要があります。この場合、<code>DATE.calendar</code> フィールドを設定すると、ランタイム例外が発生します。 サービスが <code>java.util.Date</code> を返す場合、日付は <code>DATE.date</code> フィールドに返されます。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>この <code>DATE</code> タイプは、サービス WSDL で次のように定義されます。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms サービスの操作で <code>java.util.Calendar</code> 値を入力として取得する場合、SOAP クライアントアプリケーションは、日付を <code>DATE.caledendar</code> フィールドに渡す必要があります。 この場合、<code>DATE.date</code> フィールドを設定すると、ランタイム例外が発生します。 サービスが <code>java.util.Calendar</code> を返す場合、日付が <code>DATE.calendar</code> フィールドに返されます。 </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>この <code>apachesoap:Map</code> サービスは、WSDL で次のように定義されます。</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>マップは、キーと値のペアのシーケンスとして表されます。</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>XML タイプは、サービス WSDL で次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms サービス操作が <code>org.w3c.dom.Document</code> の値の入力を受け入れる場合、XML データを <code>XML.document</code> フィールドに渡します。</p><p><code>XML.element</code> フィールドを設定すると、ランタイム例外が発生します。 サービスが <code>org.w3c.dom.Document</code> を返すと、XML データが <code>XML.document</code> フィールドに返されます。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML タイプは、サービス WSDL で次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms サービスの操作が <code>org.w3c.dom.Element</code> 値を入力として取得すると、XML データを <code>XML.element</code> フィールドに渡します。</p><p><code>XML.document</code> フィールドを設定すると、ランタイム例外が発生します。 サービスが <code>org.w3c.dom.Element</code> を返すと、XML データが <code>XML.element</code> フィールドに返されます。</p></td>
  </tr>
 </tbody>
</table>

## JAX-WS を使用した Java プロキシクラスの作成 {#creating-java-proxy-classes-using-jax-ws}

JAX-WS を使用して、Forms サービス WSDL を Java プロキシクラスに変換できます。 これらのクラスを使用して、AEM Forms サービス操作を呼び出すことができます。 Apache Ant を使用すると、AEM Forms サービス WSDL を参照して Java プロキシクラスを生成するビルドスクリプトを作成できます。次の手順を実行して、JAX-WS プロキシファイルを生成できます。

1. クライアントコンピューターに Apache Ant をインストールします。 （[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi) を参照。）

   * bin ディレクトリをクラスパスに追加します。
   * `ANT_HOME` 環境変数を、Ant をインストールしたディレクトリに設定します。

1. JDK 1.6 以降をインストールします。

   * JDK bin ディレクトリをクラスパスに追加します。
   * JRE bin ディレクトリをクラスパスに追加します。 この bin は、`[JDK_INSTALL_LOCATION]/jre` ディレクトリに配置されています。
   * `JAVA_HOME` 環境変数を、JDK をインストールしたディレクトリに設定します。

   JDK 1.6 には、build.xml ファイルで使用される wsimport プログラムが含まれています。 JDK 1.5 には、このプログラムは含まれていません。

1. JAX-WS をクライアントコンピューターにインストールします。 （[XML web サービス用 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html) を参照。）
1. JAX-WS と Apache Ant を使用して、Java プロキシクラスを生成します。 このタスクを実行する Ant ビルドスクリプトを作成します。 次のスクリプトは、build.xml という名前の Ant ビルドスクリプトのサンプルです。

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   この Ant ビルドスクリプト内では、 `url` プロパティは、localhost で実行されている 暗号化サービス WSDL を参照するように設定されていることにご注意ください。 この `username` および `password` プロパティは、有効な AEM forms のユーザー名とパスワードに設定する必要があります。 URL には `lc_version` フィールド名が含まれていることにご注意ください。`lc_version` オプションを指定しない場合、新しい AEM Forms サービス操作を呼び出すことはできません。

   >[!NOTE]
   >
   >`EncryptionService` を、Java プロキシクラスを使用して呼び出す AEM Forms サービス名に置換します。 例えば、Rights Management サービス用の Java プロキシクラスを作成するには、次のように指定します。

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Ant ビルドスクリプトを実行する BAT ファイルを作成します。Ant ビルドスクリプトの実行を担う BAT ファイルには、次のコマンドを配置できます。

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Ant ビルドスクリプトを C:\Program Files\Java\jaxws-ri\bin ディレクトリに配置します。このスクリプトで、JAVA ファイルを ./classes フォルダーに書き込みます。このスクリプトが生成する JAVA ファイル群で、サービスを呼び出すことができます。

1. これらの JAVA ファイルを 1 つの JAR ファイルにパッケージ化します。Eclipse で作業している場合は、次の手順に従います。

   * プロキシ JAVA ファイルを JAR ファイルにパッケージ化するために使用する、新しい Java プロジェクトを作成します。
   * プロジェクトにソースフォルダーを作成します。
   * ソースフォルダーに`com.adobe.idp.services`パッケージを作成します。
   * `com.adobe.idp.services`パッケージを選択して、JAVA ファイルを adobe/idp/services フォルダーからこのパッケージにインポートします。
   * 必要に応じて、`org/apache/xml/xmlsoap`パッケージをソースフォルダーに作成します。
   * ソースフォルダーを選択し、org/apache/xml/xmlsoap フォルダーから JAVA ファイルをインポートしてください。
   * Java コンパイラのコンプライアンスレベルを 5.0 以上に設定します。
   * プロジェクトをビルドします。
   * プロジェクトを JAR ファイルとしてエクスポートします。
   * この JAR ファイルをクライアントプロジェクトのクラスパスにインポートします。さらに、&lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty にあるすべての JAR ファイルをインポートします。

   >[!NOTE]
   >
   >「AEM Forms によるプログラミング」にあるすべての Java web サービスのクイックスタート（Forms サービスを除く）は、JAX-WS を使用して Java プロキシファイルを作成します。また、すべての Java web サービスのクイックスタートは、SwaRef を使用します。（[SwaRef を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-swaref)を参照。）

**関連項目**

[Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP で送信する BLOB データを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-blob-data-over-http)

[SwaRef を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-swaref)

## Apache Axis を使用した Java プロキシクラスの作成 {#creating-java-proxy-classes-using-apache-axis}

Apache Axis WSDL2Java ツールを使用すると、Forms サービスを Java プロキシクラスに変換できます。このクラスを使用すると、Forms サービス操作を呼び出すことができます。Apache Ant を使用すると、サービス WSDL から Axis ライブラリファイルを生成できます。Apache Axis は、URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/) でダウンロードできます。

>[!NOTE]
>
>Forms サービスに関連付けられた web サービスのクイックスタートでは、Apache Axis を使用して作成された Java プロキシクラスを使用します。Forms web サービスのクイックスタートでは、エンコーディングタイプとして Base64 も使用します（[Forms Service API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)を参照してください）。

次の手順を実行して、Axis Java ライブラリファイルを生成できます。

1. クライアントコンピューターに Apache Ant をインストールします。[https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi) で入手できます。

   * bin ディレクトリをクラスパスに追加します。
   * `ANT_HOME` 環境変数を、Ant をインストールしたディレクトリに設定します。

1. Apache Axis 1.4 をクライアントコンピューターにインストールします。[https://ws.apache.org/axis/](https://ws.apache.org/axis/) で入手できます。
1. Web サービスクライアントで Axis JAR ファイルを使用するクラスパスを設定します。詳しくは、[https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html) にある Axis インストール手順を参照してください。
1. Axis で Apache WSDL2Java ツールを使用して、Java プロキシクラスを生成します。このタスクを実行する Ant ビルドスクリプトを作成します。次のスクリプトは、build.xml という名前の Ant ビルドスクリプトのサンプルです。

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   この Ant ビルドスクリプトでは、`url` プロパティは、localhost で実行している暗号化サービス WSDL を参照するように設定されています。`username` プロパティと `password` プロパティには、AEM Forms の有効なユーザー名とパスワードを設定する必要があります。

1. Ant ビルドスクリプトを実行する BAT ファイルを作成します。Ant ビルドスクリプトの実行を担う BAT ファイルには、次のコマンドを配置できます。

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA ファイルは、`output` プロパティで指定したように、C:\JavaFiles フォルダーに書き込まれます。Forms サービスを正常に呼び出すには、これらの JAVA ファイルをクラスパスにインポートします。

   デフォルトでは、これらのファイルは、 `com.adobe.idp.services` という名前の Java パッケージに属します。これらの JAVA ファイルは、JAR ファイルに配置することをお勧めします。 次に、JAR ファイルをクライアントアプリケーションのクラスパスにインポートします。

   >[!NOTE]
   >
   >.JAVA ファイルを JAR に配置する方法は異なります。 1 つの方法は、Eclipse のような Java IDE を使用する方法です。 Java プロジェクトおよび `com.adobe.idp.services` パッケージを作成します（すべての .JAVA ファイルは、このパッケージに属しています）。次に、すべての .JAVA ファイルをパッケージにインポートします。 最後に、プロジェクトを JAR ファイルとして書き出します。

1. URL を `EncryptionServiceLocator` クラス内で修正して、エンコーディングタイプを指定します。 例えば、base64 を使用するには、`BLOB` オブジェクトが確実にバイナリデータを返すように、 `?blob=base64` を指定します。つまり、 `EncryptionServiceLocator` クラス内で、次のコード行を探します。

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   これを次のように変更します。

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 以下の Axis JAR ファイルを Java プロジェクトのクラスパスに追加します。

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   これらの JAR ファイルは、`[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` ディレクトリにあります。

**関連トピック**

[JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP で送信する BLOB データを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-blob-data-over-http)

## Base64 エンコーディングを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-base64-encoding}

Base64 エンコーディングを使用して、AEM Forms サービスを呼び出すことができます。 Base64 エンコーディングは、web サービスの呼び出し要求で送信される添付ファイルをエンコードします。 つまり `BLOB` SOAP メッセージ全体ではなく、データが Base64 でエンコードされ。

「Base64 エンコーディングを使用した AEM Forms の呼び出し」のセクションでは、Base64 エンコーディングを使用して、次の `MyApplication/EncryptDocument` という名前の AEM Forms の短時間有効なプロセスについて説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づくものではありません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数に返されます。

### Base64 エンコーディングを使用する .NET クライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NET クライアントアセンブリを作成して、Microsoft Visual Studio .NET プロジェクトから Forms サービスを呼び出すことができます。 base64 エンコーディングを使用する .NET クライアントアセンブリを作成するには、次の手順を実行します。

1. AEM Forms 呼び出し URL に基づいて、プロキシクラスを作成します。
1. .NET クライアントアセンブリを生成する Microsoft Visual Studio .NET プロジェクトを作成します。

**プロキシクラスの作成**

Microsoft Visual Studio に付属のツールを使用すると、.NET クライアントアセンブリの作成に使用するプロキシクラスを作成できます。このツールの名前は wsdl.exe で、Microsoft Visual Studio のインストールフォルダーにあります。プロキシクラスを作成するには、コマンドプロンプトを開き、wsdl.exe ファイルを含むフォルダーに移動します。wsdl.exe ツールについて詳しくは、 *MSDN ヘルプ*&#x200B;を参照してください。

コマンドプロンプトで次のコマンドを入力します。

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

デフォルトでは、このツールは WSDL と同じ名前のフォルダーに CS ファイルを作成します。この場合、*EncryptDocumentService.cs* という名前の CS ファイルが作成されます。この CS ファイルを使用すると、プロキシオブジェクトを作成して、呼び出し URL で指定したサービスを呼び出すことができます。

`?blob=base64` を含むようにプロキシクラスの URL を修正して、確実に `BLOB` オブジェクトがバイナリデータを返すようにします。プロキシクラスで、次のコード行を探します。

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

これを次のように変更します。

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

*Base64 エンコーディングを使用した AEM Forms の呼び出し* の節では、`MyApplication/EncryptDocument` を例として使用しています。別の Forms サービス用に .NET クライアントアセンブリを作成する場合は、必ず `MyApplication/EncryptDocument` をサービスの名前に置き換えてください。

**.NET クライアントアセンブリの開発**

.NET クライアントアセンブリを生成する Visual Studio クラスライブラリプロジェクトを作成します。wsdl.exe を使用して作成した CS ファイルを、このプロジェクトにインポートすることができます。このプロジェクトが生成する DLL ファイル（.NET クライアントアセンブリ）を使用すると、他の Visual Studio .NET プロジェクトでサービスを呼び出すことができます。

1. Microsoft Visual Studio .NET を起動します。
1. クラスライブラリプロジェクトを作成し、DocumentService という名前を付けます。
1. wsdl.exe を使用して作成した CS ファイルをインポートします。
1. **プロジェクト**&#x200B;メニューで、**参照を追加**&#x200B;を選択します。
1. 「参照を追加」ダイアログボックスで、**System.Web.Services.dll**&#x200B;を選択します。
1. **選択**&#x200B;をクリックしてから、**OK**&#x200B;をクリックしてください。
1. プロジェクトをコンパイルしてビルドします。

>[!NOTE]
>
>この手順では、DocumentService.dll という名前の .NET クライアントアセンブリが作成され、SOAP リクエストを `MyApplication/EncryptDocument` サービスに送信する際に使用できるようになります。

>[!NOTE]
>
>.NET クライアントアセンブリの作成に使用するプロキシクラスの URL に、`?blob=base64`を追加したことを確認します。追加されていない場合は、`BLOB` オブジェクトからバイナリデータを取得できません。

**.NET クライアントアセンブリの参照**

新しく作成した .NET クライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。.NET クライアントアセンブリをディレクトリに配置したら、プロジェクトから参照できるようになります。また、`System.Web.Services`ライブラリをプロジェクトから参照します。このライブラリを参照しない場合、.NET クライアントアセンブリを使用してサービスを呼び出すことはできません。

1. **プロジェクト**&#x200B;メニューで、**参照の追加**&#x200B;を選択します。
1. **.NET**&#x200B;タブをクリックします。
1. **参照**&#x200B;をクリックして、DocumentService.dll ファイルを見つけます。
1. **選択**&#x200B;をクリックしてから、**OK**&#x200B;をクリックしてください。

**Base64 エンコーディングを使用する .NET クライアントアセンブリを使用したサービスの呼び出し**

Base64 エンコーディングを使用する .NET クライアントアセンブリを使用して、Workbench で構築された `MyApplication/EncryptDocument` サービスを呼び出すことができます。`MyApplication/EncryptDocument`サービスを呼び出すには、次の手順を実行します。

1. `MyApplication/EncryptDocument`サービス WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
1. クライアントの Microsoft .NET プロジェクトを作成します。クライアントプロジェクトで Microsoft .NET クライアントアセンブリを参照します。また、`System.Web.Services`も参照します。
1. Microsoft .NET クライアントアセンブリを使用し、デフォルトのコンストラクターを呼び出して、`MyApplication_EncryptDocumentService`オブジェクトを作成します。
1. `System.Net.NetworkCredential` オブジェクトを使用して `MyApplication_EncryptDocumentService` オブジェクトの `Credentials` プロパティを設定します。`System.Net.NetworkCredential`コンストラクター内で、AEM Forms のユーザー名と対応するパスワードを指定します。.NET クライアントアプリケーションが AEM Forms と SOAP メッセージを正常に交換できるように、認証情報を設定します。
1. コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、`MyApplication/EncryptDocument` プロセスに渡す PDF ドキュメントを保存するために使用されます。
1. コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
1. `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
1. `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
1. `binaryData`プロパティにバイト配列の内容を割り当てて、`BLOB`オブジェクトにデータを入力します。
1. `MyApplication/EncryptDocument`プロセスを呼び出すには、`MyApplication_EncryptDocumentService`オブジェクトの`invoke`メソッドを呼び出し、PDF ドキュメントを含む`BLOB`オブジェクトを渡します。このプロセスは、暗号化された PDF ドキュメントを`BLOB`オブジェクト内に返します。
1. `System.IO.FileStream`オブジェクトを作成するには、コンストラクタを呼び出し、パスワードで暗号化されたドキュメントのファイルの場所を表す文字列値を渡します。
1. `MyApplicationEncryptDocumentService`オブジェクトの`invoke`メソッドが返した`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。バイト配列を入力するには、`BLOB` オブジェクトの `binaryData` データメンバーの値を取得します。
1. `System.IO.BinaryWriter`オブジェクトを作成するには、コンストラクタを呼び出して、`System.IO.FileStream`オブジェクトを渡します。
1. `System.IO.BinaryWriter` オブジェクトの `Write` メソッドをを呼び出し、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

### Java プロキシクラスと Base64 エンコーディングを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Java プロキシクラスと Base64 を使用して、AEM Forms サービスを呼び出すことができます。 Java プロキシクラスを使用して`MyApplication/EncryptDocument`サービスを呼び出すには、次の手順を実行します。

1. `MyApplication/EncryptDocument`サービス WSDL を使用する JAX-WS を使用して、Java プロキシクラスを作成します。 次の WSDL エンドポイントを使用します。

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >AEM Forms をホストする J2EE アプリケーションサーバーの IP アドレスに `hiro-xp` *を置換します。*

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスに配置された Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;インストールディレクトリ>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. `MyApplicationEncryptDocumentService` オブジェクトを作成するには、それ自身のコンストラクタを使用します。
1. `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッドを呼び出すことによって、`MyApplicationEncryptDocument` オブジェクトを作成します。
1. 次のデータメンバーに値を割り当てて、AEM Forms を呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングタイプを `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。Base64 エンコーディングを使用する `MyApplication/EncryptDocument` サービスを呼び出すには、次の URL 値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコード例に、このアプリケーションロジックを示します。

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. `MyApplication/EncryptDocument` プロセスに送信する PDF ドキュメントを取得するには、コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
1. バイト配列を作成し、 `java.io.FileInputStream` オブジェクトの内容を入力します。
1. それ自身のコンストラクタを使用して、`BLOB` オブジェクトを作成します。
1. `setBinaryData` メソッドを呼び出し、バイト配列を渡すことによって、`BLOB` オブジェクトを入力します。`BLOB` オブジェクトの `setBinaryData` は、Base64 エンコーディングを使用する場合に呼び出すメソッドです。サービスリクエストでの BLOB オブジェクトの供給を参照してください。
1. `MyApplicationEncryptDocument` オブジェクトの `invoke` メソッドを呼び出すことによって、`MyApplication/EncryptDocument` プロセスを呼び出します。PDF ドキュメントを含む `BLOB` オブジェクトを渡します。呼び出しメソッドは、暗号化された PDF ドキュメントを含む `BLOB` オブジェクトを返します。
1. `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して、暗号化された PDF ドキュメントを含むバイト配列を作成します。
1. 暗号化された PDF ドキュメントを PDF ファイルとして保存します。バイト配列をファイルに書き込みます。

**関連トピック**

[クイックスタート：Java プロキシファイルと Base64 エンコーディングを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOM を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-mtom}

Web サービス標準の MTOM を使用して、AEM Forms サービスを呼び出すことができます。この規格では、PDF ドキュメントなどのバイナリデータがインターネットやイントラネット経由で送信される方法を定義します。MTOM の特徴の 1 つは、`XOP:Include` 要素の使用です。この要素は、SOAP メッセージのバイナリ添付を参照する XML Binary Optimized Packaging（XOP）仕様で定義されます。

ここでは、MTOM を使用して、次の AEM Forms の短時間のみ有効な `MyApplication/EncryptDocument` という名前のプロセスを呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づくものではありません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>MTOM サポートは、AEM Forms、バージョン 9 で追加されました。

>[!NOTE]
>
>MTOM 送信プロトコルを使用する JAX WS ベースのアプリケーションは、送受信データが 25 MB に制限されています。 この制限は、JAX-WS のバグが原因です。 送受信ファイルの合計サイズが 25 MB を超える場合は、MTOM プロトコルの代わりに SwaRef 送信プロトコルを使用します。 そうでない場合、`OutOfMemory` 例外が発生する可能性があります。

ここでは、Microsoft .NET プロジェクト内で MTOM を使用して AEM Forms サービスを呼び出す方法について説明します。使用される .NET Framework は 3.5 で、開発環境は Visual Studio 2008 です。Web サービス拡張機能（WSE）が開発用コンピューターにインストールされている場合は削除します。.NET 3.5 フレームワークは、Windows Communication Foundation (WCF) という名前の SOAP フレームワークをサポートしています。MTOM を使用して AEM Forms を呼び出す場合、WCF（WSE ではない）のみがサポートされます。

### MTOM を使用してサービスを呼び出す .NET プロジェクトの作成 {#creating-a-net-project-that-invokes-a-service-using-mtom}

Web サービスを使用して AEM Forms サービスを呼び出す Microsoft .NET プロジェクトを作成できます。まず、Visual Studio 2008 を使用して Microsoft .NET プロジェクトを作成します。AEM Forms サービスを呼び出すには、プロジェクト内で呼び出す AEM Forms サービスへのサービスリファレンスを作成します。サービス参照を作成する際は、AEM Forms サービスの URL を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

`localhost` を AEM Forms をホストする J2EE アプリケーションサーバーの IP アドレスに置き換えます。呼び出す AEM Forms サービスの名前で `MyApplication/EncryptDocument` を置き換えます。例えば、Rights Management 操作を呼び出すには、次のように指定します。

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

`lc_version` オプションを使用すると、MTOM などの AEM Forms 機能が使用可能になります。`lc_version` オプションを指定しない場合、MTOM を使用して AEM Forms を呼び出すことはできません。

サービス参照を作成した後、AEM Forms サービスに関連付けられているデータタイプを .NET プロジェクト内で使用できるようになります。AEM Forms サービスを呼び出す .NET プロジェクトを作成するには、次の手順を実行します。

1. Microsoft Visual Studio 2008 を使用して .NET プロジェクトを作成します。
1. **プロジェクト**&#x200B;メニューから、「**サービス参照を追加**」を選択します。
1. **住所**&#x200B;ダイアログボックスで、AEM Forms サービスへの WSDL を指定します。例：

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 「 **移動**」をクリックし、「**OK**」をクリックします。

### .NET プロジェクトで MTOM を使用したサービスの呼び出し {#invoking-a-service-using-mtom-in-a-net-project}

保護されていない PDF ドキュメントを受け入れる `MyApplication/EncryptDocument` プロセスを考慮して、パスワードで暗号化された PDF ドキュメントを返します。MTOM を使用して `MyApplication/EncryptDocument` プロセス（Workbench に組み込まている）を呼び出すには、次の手順で実行します。

1. Microsoft .NET プロジェクトを作成します。
1. デフォルトのコンストラクタを使用して `MyApplication_EncryptDocumentClient` オブジェクトを作成します。
1. `System.ServiceModel.EndpointAddress` コンストラクタを使用して `MyApplication_EncryptDocumentClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスとエンコーディングタイプに渡します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   `lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定する必要があります。

   >[!NOTE]
   >
   >`hiro-xp` を *AEM Forms をホストする J2EE アプリケーションサービスの IP アドレス*&#x200B;で置き換えます。

1. `EncryptDocumentClient.Endpoint.Binding` データメンバーの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
1. `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` データメンバーを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
1. 次のタスクを実行して、HTTP 基本認証を有効にします。

   * AEM Forms ユーザー名をデータメンバー `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName` に割り当てます。
   * 対応するパスワード値をデータメンバー `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password` に割り当てます。
   * 定数値 `HttpClientCredentialType.Basic` をデータメンバーに `BasicHttpBindingSecurity.Transport.ClientCredentialType` に割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をデータメンバーに `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

   次のコードの例に、これらのタスクを示します。

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、`MyApplication/EncryptDocument` プロセスに渡す PDF ドキュメントを保存するために使用されます。
1. コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
1. `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
1. `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
1. `BLOB` オブジェクトを入力するには、`MTOM` データメンバーにバイト配列のコンテンツを割り当てます。
1. `MyApplication/EncryptDocument` プロセスを呼び出すには、`MyApplication_EncryptDocumentClient` オブジェクトの `invoke` メソッドを呼び出します。PDF ドキュメントを含む `BLOB` オブジェクトを渡します。このプロセスは、`BLOB` オブジェクト内で暗号化された PDF ドキュメントを返します。
1. `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出し、保護された PDF ドキュメントのファイルの場所を表す文字列値を渡します。
1. `invoke` メソッドが返した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
1. コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
1. バイト配列のコンテンツを PDF ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

>[!NOTE]
>
>ほとんどの AEM Forms サービス操作は、MTOM のクイックスタートを備えています。これらのクイックスタートは、サービスの対応するクイックスタートセクションに表示されます。例えば、Output のクイックスタートのセクションを見るには、[Output サービス API クイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)を参照してください。

**関連トピック**

[クイックスタート：.NET プロジェクトでの MTOM を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Web サービスを使用した複数のサービスへのアクセス](#accessing-multiple-services-using-web-services)

[人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRef を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-swaref}

SwaRef を使用して AEM Forms サービスを呼び出すことができます。`wsi:swaRef` XML 要素のコンテンツは、添付ファイルへの参照を保存する SOAP 本文内の添付ファイルとして送信されます。SwaRef を使用して Forms サービスを呼び出す場合、XML Web サービス用 Java API（JAX-WS）を使用して Java プロキシクラスを作成します（[XML Web サービス用 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html) を参照してください）。

ここでは、SwaRef を使用して、次の Forms の短時間有効な `MyApplication/EncryptDocument` という名前のプロセスを呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>AEM Forms で SwaRef のサポートを追加

以下では、Java クライアントアプリケーション内で SwaRef を使用して Forms サービスを呼び出す方法について説明します。 Java アプリケーションは、JAX-WS を使用して作成されたプロキシクラスを使用します。

### SwaRef を使用する JAX-WS ライブラリファイルを使用してサービスを呼び出す {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

JAX-WS と SwaRef を使用して作成された Java プロキシファイルを使用して、`MyApplication/EncryptDocument` プロセスを呼び出すには、次の手順を実行します。

1. `MyApplication/EncryptDocument` サービス WSDL を消費する JAX-WS を使用して、Java プロキシファイルを作成します。次の WSDL エンドポイントを使用します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、 [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)を参照してください。

   >[!NOTE]
   >
   >`hiro-xp` を *AEM Forms をホストする J2EE アプリケーションサーバーの IP アドレス*&#x200B;で置き換えます。

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスに配置された Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;インストールディレクトリ>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. `MyApplicationEncryptDocumentService` オブジェクトを作成するには、それ自身のコンストラクタを使用します。
1. `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッドを呼び出すことによって、`MyApplicationEncryptDocument` オブジェクトを作成します。
1. 次のデータメンバーに値を割り当てて、AEM Forms を呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングのタイプを `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。SwaRef エンコーディングを使用する`MyApplication/EncryptDocument`サービスを呼び出すには、次の URL 値を指定します。

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM Forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコード例に、このアプリケーションロジックを示します。

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. `MyApplication/EncryptDocument` プロセスに送信する PDF ドキュメントを取得するには、コンストラクターを使用して `java.io.File` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
1. `FileDataSource`コンストラクターを使用して`javax.activation.DataSource`オブジェクトを作成します。`java.io.File`オブジェクトを渡します。
1. `javax.activation.DataHandler` オブジェクトを作成するには、コンストラクタを使用して `javax.activation.DataSource` オブジェクトに渡します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. `BLOB`オブジェクトを入力するには、`setSwaRef`メソッドを呼び出して`javax.activation.DataHandler`オブジェクトを渡します。
1. `MyApplication/EncryptDocument`プロセスを呼び出すには、`MyApplicationEncryptDocument`オブジェクトの`invoke`メソッドを呼び出して、PDF ドキュメントを含む`BLOB`オブジェクトを渡します。呼び出しメソッドは、暗号化された PDF ドキュメントを含む`BLOB`オブジェクトを返します。
1. `BLOB`オブジェクトの`getSwaRef`メソッドを呼び出して`javax.activation.DataHandler`オブジェクトを入力します。
1. `javax.activation.DataHandler`オブジェクトを`java.io.InputSteam`インスタンスに変換するには、`javax.activation.DataHandler`オブジェクトの`getInputStream`メソッドを呼び出します。
1. 暗号化された PDF ドキュメントを表す PDF ファイルに`java.io.InputSteam`インスタンスを書き出します。

>[!NOTE]
>
>ほとんどの AEM Forms サービス操作には、SwaRef クイックスタートが用意されています。これらのクイックスタートは、サービスの対応するクイックスタートセクションに表示されます。例えば、Output のクイックスタートのセクションを見るには、[Output サービス API クイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)を参照してください。

**関連トピック**

[クイックスタート：Java プロジェクトでの SwaRef を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP で送信する BLOB データを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-blob-data-over-http}

Web サービスを使用し、HTTP 経由で BLOB データを渡すことで、AEM Forms サービスを呼び出すことができます。HTTP 経由で BLOB データを渡す方法は、Base64 エンコーディング、DIME、MIME を使用する代わりの、別の方法となります。例えば、DIME や MIME をサポートしていない web サービス拡張機能 3.0 を使用する Microsoft .NET プロジェクトで、HTTP 経由でデータを渡すことができます。 HTTP 経由で BLOB データを使用する場合は、AEM Forms サービスが呼び出される前に入力データがアップロードされます。

「HTTP 経由で BLOB データを使用した AEM Forms の呼び出し」では、HTTP 経由で BLOB データを渡すことで、次の AEM Forms の短期間有効な`MyApplication/EncryptDocument`という名前のプロセスの呼び出しについて説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>SOAP を使用した AEM Forms の呼び出しについて詳しく理解しておくことをお勧めします。 （[Web サービスを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-web-services)を参照。）

### HTTP 経由のデータを使用する .NET クライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-data-over-http}

HTTP 経由でデータを使用するクライアントアセンブリを作成するには、[Base64 エンコーディングを使用した AEM Forms の呼び出し](#invoking-aem-forms-using-base64-encoding)に従ってください。ただし、プロキシクラスの URL を修正して、 `?blob=base64` の代わりに `?blob=http` を含めます。このアクションにより、データが HTTP 経由で渡されます。プロキシクラスで、次のコード行を探します。

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

これを次のように変更します。

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clientMyApplication/EncryptDocument アセンブリの参照**

新しい .NET クライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。.NET クライアントアセンブリをディレクトリに配置したら、プロジェクトから参照できるようになります。プロジェクトから`System.Web.Services`ライブラリを参照します。このライブラリを参照しない場合、.NET クライアントアセンブリを使用してサービスを呼び出すことはできません。

1. **プロジェクト**&#x200B;メニューで、**参照の追加**&#x200B;を選択します。
1. **.NET**&#x200B;タブをクリックします。
1. **参照**&#x200B;をクリックして、DocumentService.dll ファイルを見つけます。
1. 「**選択**」をクリックしてから、「**OK**」をクリックしてください。

**HTTP 経由で BLOB データを使用する .NET クライアントアセンブリを使用したサービスの呼び出し**

HTTP 経由でデータを使用する .NET クライアントアセンブリを使用して `MyApplication/EncryptDocument` サービス（Workbench で構築）を呼び出すことができます。`MyApplication/EncryptDocument`サービスを呼び出すには、次の手順を実行します。

1. .NET クライアントアセンブリを作成します。
1. Microsoft .NET クライアントアセンブリを参照しますクライアントの Microsoft .NET プロジェクトを作成します。クライアントプロジェクトで Microsoft .NET クライアントアセンブリを参照します。また、`System.Web.Services`も参照します。
1. Microsoft .NET クライアントアセンブリを使用し、デフォルトのコンストラクターを呼び出して、`MyApplication_EncryptDocumentService`オブジェクトを作成します。
1. `System.Net.NetworkCredential` オブジェクトを使用して `MyApplication_EncryptDocumentService` オブジェクトの `Credentials` プロパティを設定します。`System.Net.NetworkCredential`コンストラクター内で、AEM Forms のユーザー名と対応するパスワードを指定します。.NET クライアントアプリケーションが AEM Forms と SOAP メッセージを正常に交換できるように、認証情報を設定します。
1. コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、データを `MyApplication/EncryptDocument` プロセスに渡すために使用されます。
1. `MyApplication/EncryptDocument` サービスに渡す PDF ドキュメントの URI の場所を指定する文字列値を、`BLOB` オブジェクトの `remoteURL` データメンバーに割り当てます。
1. `MyApplication_EncryptDocumentService` オブジェクトの `invoke` メソッドを呼び出し、`BLOB` オブジェクトを渡すことによって、`MyApplication/EncryptDocument` プロセスを呼び出します。このプロセスは、暗号化された PDF ドキュメントを `BLOB` オブジェクト内に返します。
1. コンストラクターを使用し、返された `BLOB` オブジェクトの `remoteURL` データメンバーの値を渡すことによって、`System.UriBuilder` オブジェクトを作成します。
1. `System.UriBuilder` オブジェクトを `System.IO.Stream` オブジェクトに変換します。（このリストの後に示す C# クイックスタートで、このタスクの実行方法を示しています）。
1. バイト配列を作成し、そのバイト配列に、`System.IO.Stream` オブジェクト内にあるデータを入力します。
1. コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
1. `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出し、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

### Java プロキシクラスおよび HTTP 経由での BLOB データを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Java プロキシクラスおよび HTTP 経由での BLOB データを使用して、AEM Forms サービスを呼び出すことができます。Java プロキシクラスを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次の手順を実行します。

1. `MyApplication/EncryptDocument`サービス WSDL を使用する JAX-WS を使用して、Java プロキシクラスを作成します。 次の WSDL エンドポイントを使用します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、 [JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)を参照してください。

   >[!NOTE]
   >
   >`hiro-xp` を *AEM Forms をホストする J2EE アプリケーションサーバーの IP アドレス*&#x200B;で置き換えます。

1. JAX-WS を使用して作成した Java プロキシクラスを JAR ファイルにパッケージ化します。
1. 次のパスに配置された Java プロキシ JAR ファイルと JAR ファイルを含めます。

   &lt;インストールディレクトリ>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   を Java クライアントプロジェクトのクラスパスに追加します。

1. `MyApplicationEncryptDocumentService` オブジェクトを作成するには、それ自身のコンストラクタを使用します。
1. `MyApplicationEncryptDocumentService` オブジェクトの `getEncryptDocument` メソッドを呼び出すことによって、`MyApplicationEncryptDocument` オブジェクトを作成します。
1. 次のデータメンバーに値を割り当てて、AEM Forms を呼び出すのに必要な接続値を設定します。

   * WSDL エンドポイントとエンコーディングタイプを `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。HTTP エンコーディング経由での BLOB を使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次の URL 値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM Forms ユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコード例に、このアプリケーションロジックを示します。

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. `setRemoteURL` メソッドを呼び出して `BLOB` オブジェクトを入力します。`MyApplication/EncryptDocument` サービスに渡す PDF ドキュメントの URI の場所を指定する文字列値を渡します。
1. `MyApplication/EncryptDocument` プロセスを呼び出すには、`MyApplicationEncryptDocument` オブジェクトの `invoke` メソッドを呼び出し、PDF ドキュメントを含む `BLOB` オブジェクトを渡します。このプロセスは、暗号化された PDF ドキュメントを `BLOB` オブジェクト内に返します。
1. 暗号化された PDF ドキュメントを表すデータストリームを格納するバイト配列を作成します。`BLOB` オブジェクトの `getRemoteURL` メソッド を呼び出します（ `invoke` メソッドで返された `BLOB` オブジェクトを使用）。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化された PDF ドキュメントを表します。
1. `java.io.FileOutputStream` オブジェクトを作成するには、コンストラクタを使用して `java.io.File` オブジェクトを渡します。
1. `java.io.FileOutputStream` オブジェクトの `write` メソッドを呼び出します。暗号化された PDF ドキュメントを表すデータストリームを含むバイト配列を渡します。

## DIME を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-dime}

添付ファイル付きの SOAP を使用して、AEM Forms サービスを呼び出すことができます。AEM Forms は、MIME と DIME の両方の web サービス標準をサポートしています。DIME を使用すると、添付ファイルをエンコードする代わりに、呼び出し要求と共に、PDF ドキュメントなどのバイナリ添付ファイルを送信できます。*DIME を使用した AEM Forms の呼び出し*&#x200B;の節では、DIME を使用した次の AEM Forms の短時間のみ有効な `MyApplication/EncryptDocument` という名前のプロセスの呼び出しについて説明します。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください）。

>[!NOTE]
>
>DIME を使用した AEM Forms サービス操作の呼び出しは推奨されません。MTOM を使用することをお勧めします。（[MTOM を使用した AEM Forms の呼び出し](#invoking-aem-forms-using-mtom)を参照してください）。

### DIME を使用する .NET プロジェクトの作成 {#creating-a-net-project-that-uses-dime}

DIME を使用して Forms サービスを呼び出すことのできる .NET プロジェクトを作成するには、次のタスクを実行します。

* 開発用コンピュータに web サービス拡張機能 2.0 をインストールします。
* .NET プロジェクト内から、AEM Forms サービスへの web 参照を作成します。

**Web サービス拡張機能 2.0 のインストール**

Web サービス拡張機能 2.0 を開発用コンピューターにインストールし、Microsoft Visual Studio .NET と統合します。Web サービス拡張機能 2.0 は、[Microsoft ダウンロードセンター](https://www.microsoft.com/downloads/search.aspx)からダウンロードできます。

この web ページから、Web サービス拡張機能 2.0 を検索し、開発用コンピューターにダウンロードします。このダウンロードにより、Microsoft WSE 2.0 SPI.msi という名前のファイルがコンピューターに配置されます。インストールプログラムを実行し、オンラインの指示に従います。

>[!NOTE]
>
>Web サービス拡張機能 2.0 は DIME をサポートしています。Web サービス拡張機能 2.0 を使用する場合、Microsoft Visual Studio のサポート対象バージョンは 2003 年版です。Web サービス拡張機能 3.0 は、DIME をサポートしていませんが、MTOM はサポートしています。

**AEM Forms サービスへの web 参照の作成**

Web サービス拡張機能 2.0 を開発コンピューターにインストールし、Microsoft .NET プロジェクトを作成したら、Forms サービスへの web 参照を作成します。例えば、`MyApplication/EncryptDocument` プロセスに web 参照を作成するには、Forms がローカルコンピューターにインストールされている場合は、次の URL を指定します。

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Web 参照を作成した後、2 つのプロキシデータタイプ（`EncryptDocumentService` および `EncryptDocumentServiceWse`）を .NET プロジェクト内で使用できます。DIME を使用して `MyApplication/EncryptDocument` プロセスを呼び出すには、`EncryptDocumentServiceWse` タイプを使用します。

>[!NOTE]
>
>Forms サービスへの web 参照を作成する前に、プロジェクトで web サービス拡張機能 2.0 を参照していることを確認してください。（Web サービス拡張機能 2.0 のインストールを参照してください）。

**WSE ライブラリの参照**

1. プロジェクトメニューで、「参照を追加」を選択します。
1. 参照を追加ダイアログボックスで、「Microsoft.Web.Services2.dll」を選択します。
1. 「System.Web.Services.dll」を選択します。
1. 「選択」をクリックして、「OK」をクリックします。

**Forms サービスへの web 参照の作成**

1. プロジェクトメニューで、「Web 参照を追加」を選択します。
1. URL ダイアログボックスで、Forms サービスの URL を指定します。
1. 「移動」をクリックし、「参照を追加」をクリックします。

>[!NOTE]
>
>.NET プロジェクトで WSE ライブラリを使用できるようにします。 Project Explorer 内で、プロジェクト名を右クリックし、「WSE 2.0 を有効にする」を選択します。表示されるダイアログボックスのチェックボックスがオンになっていることを確認します。

**.NET プロジェクトで DIME を使用したサービスの呼び出し**

DIME を使用して Forms サービスを呼び出すことができます。保護されていない PDF ドキュメントを受け入れ、パスワードで暗号化された PDF ドキュメントを返す `MyApplication/EncryptDocument` プロセスを考えます。DIME を使用して `MyApplication/EncryptDocument` プロセスを呼び出すには、次の手順を実行します。

1. DIME を使用してForms サービスの呼び出しを可能にする Microsoft .NET プロジェクトを作成します。必ず web サービス拡張機能 2.0 を含め、AEM Forms サービスへの web 参照を作成します。
1. `MyApplication/EncryptDocument` プロセスへの web 参照を設定した後、デフォルトのコンストラクターを使用して `EncryptDocumentServiceWse` オブジェクトを作成します。
1. AEM forms のユーザー名とパスワードの値を指定する `System.Net.NetworkCredential` 値で、`EncryptDocumentServiceWse` オブジェクトの `Credentials` データメンバーを設定します。
1. コンストラクターを使用して `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトを作成し、次の値を渡します。

   * GUID 値を指定する文字列値。`System.Guid.NewGuid.ToString` メソッドを呼び出すことによって、GUID 値を取得できます。
   * コンテンツタイプを指定する文字列値。このプロセスには PDF ドキュメントが必要なため、`application/pdf` を指定します。
   * `TypeFormat` 列挙値。以下のように `TypeFormat.MediaType` を指定します。
   * AEM Forms プロセスに渡す PDF ドキュメントの場所を指定する文字列値。

1. `BLOB` オブジェクトを、そのコンストラクタを使用して作成します。
1. `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトの `Id` データメンバーの値を `BLOB` オブジェクトの `attachmentID` データメンバーに割り当てて、`BLOB` オブジェクトに DIME 添付ファイルを追加します。
1. `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` メソッドをを呼び出して、`Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトを渡します。
1. `EncryptDocumentServiceWse` オブジェクトの `invoke` メソッドを呼び出し、DIME 添付ファイルを含む `BLOB` オブジェクトを渡すことによって、`MyApplication/EncryptDocument` プロセスを呼び出します。このプロセスは、`BLOB` オブジェクト内で暗号化された PDF ドキュメントを返します。
1. 返された `BLOB` オブジェクトの `attachmentID` データメンバーの値を取得することによって、添付ファイルの識別情報の値を取得します。
1. `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` に配置された添付ファイルを繰り返し処理し、添付ファイルの識別情報の値を用いて、暗号化された PDF ドキュメントを取得します。
1. `Attachment` オブジェクトの `Stream` データメンバーの値を取得することによって、`System.IO.Stream` オブジェクトを取得します。
1. バイト配列を作成し、そのバイト配列を `System.IO.Stream` オブジェクトの `Read` メソッドに渡します。このメソッドは、暗号化された PDF ドキュメントを表すデータストリームでバイト配列を入力します。
1. コンストラクターを呼び出し、PDF ファイルの場所を表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。このオブジェクトは、暗号化された PDF ドキュメントを表します。
1. `System.IO.BinaryWriter` オブジェクトを作成するには、コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡します。
1. `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出し、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

### DIME を使用する Apache Axis Java プロキシクラスの作成 {#creating-apache-axis-java-proxy-classes-that-use-dime}

Apache Axis WSDL2Java ツールを使用して、サービス WSDL を Java プロキシクラスに変換し、サービス操作を呼び出すことができます。Apache Ant を使用すると、サービスを呼び出す AEM Forms サービス WSDL から Axis ライブラリファイルを生成できます。（[Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis) を参照してください）。

Apache Axis WSDL2Java ツールは、SOAP リクエストをサービスに送信するために使用されるメソッドを含む JAVA ファイルを生成します。サービスが受け取った SOAP リクエストは、Axis が生成したライブラリによってデコードされ、メソッドと引数に戻されます。

Axis 生成のライブラリファイルと DIME を使用して、Workbench で構築された `MyApplication/EncryptDocument` サービスを呼び出すには、以下の手順を実行します。

1. Apache Axis を使用して `MyApplication/EncryptDocument` サービス WSDL を使用する、Java プロキシクラスを作成します（[Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)を参照）。
1. Java プロキシクラスをクラスパスに含めます。
1. `MyApplicationEncryptDocumentServiceLocator` オブジェクトを、それ自身のコンストラクタを使用して作成します。
1. `URL` オブジェクトを作成するには、コンストラクターを使用して、AEM Forms サービス WSDL の定義を指定する文字列値を渡します。SOAP エンドポイント URL の末尾に配置された `?blob=dime` を、必ず指定してください。例えば、

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. `EncryptDocumentSoapBindingStub` オブジェクトを作成するには、コンストラクターを呼び出し、`MyApplicationEncryptDocumentServiceLocator` オブジェクトと `URL` オブジェクトを渡します。
1. `EncryptDocumentSoapBindingStub` オブジェクトの `setUsername` および `setPassword` メソッドを呼び出して、AEM forms のユーザー名とパスワードの値を設定します。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. `MyApplication/EncryptDocument` サービスに送信する PDF ドキュメントを取得するには、`java.io.File` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
1. `javax.activation.DataHandler` オブジェクトを作成するには、コンストラクターを使用して、`javax.activation.FileDataSource` オブジェクトを渡します。`javax.activation.FileDataSource` オブジェクトを作成するには、コンストラクターを使用して、PDF ドキュメントを表す `java.io.File` オブジェクトを渡します。
1. `org.apache.axis.attachments.AttachmentPart` オブジェクトを作成するには、コンストラクターを使用して、`javax.activation.DataHandler` オブジェクトを渡します。
1. 添付ファイルを添付するには、`EncryptDocumentSoapBindingStub` オブジェクトの `addAttachment` メソッドを呼び出し、`org.apache.axis.attachments.AttachmentPart` オブジェクトを渡します。
1. それ自身のコンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトに添付ファイルの識別情報の値を入力するには、`BLOB` オブジェクトの `setAttachmentID` メソッドを呼び出し、添付ファイルの識別情報の値を渡します。`org.apache.axis.attachments.AttachmentPart` オブジェクトの `getContentId` メソッドを呼び出すと、この値を取得できます。
1. `MyApplication/EncryptDocument` プロセスを呼び出すには、`EncryptDocumentSoapBindingStub` オブジェクトの `invoke` メソッドを呼び出します。DIME 添付ファイルを含む `BLOB` オブジェクトを渡します。このプロセスは、暗号化された PDF ドキュメントを `BLOB` オブジェクト内に返します。
1. 返された `BLOB` オブジェクトの `getAttachmentID` メソッドを呼び出して、添付ファイルの識別情報の値を取得します。このメソッドは、返される添付ファイルの識別情報の値を表す文字列値を返します。
1. `EncryptDocumentSoapBindingStub` オブジェクトの `getAttachments` メソッドを呼び出して、添付ファイルを取得します。このメソッドは、添付ファイルを表す `Objects` の配列を返します。
1. 添付ファイル（`Object` 配列）を反復処理し、添付ファイルの識別情報の値を使用して、暗号化された PDF ドキュメントを取得します。各要素は `org.apache.axis.attachments.AttachmentPart` オブジェクトです。
1. `org.apache.axis.attachments.AttachmentPart` オブジェクトの `getDataHandler` メソッドを呼び出して、添付ファイルに関連付けられた `javax.activation.DataHandler` オブジェクトを取得します。
1. `javax.activation.DataHandler` オブジェクトの `getInputStream` メソッドを呼び出して、`java.io.FileStream` オブジェクトを取得します。
1. バイト配列を作成し、そのバイト配列を `java.io.FileStream` オブジェクトの `read` メソッドに渡します。このメソッドは、暗号化された PDF ドキュメントを表すデータストリームでバイト配列を入力します。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化された PDF ドキュメントを表します。
1. `java.io.FileOutputStream` オブジェクトを作成するには、コンストラクタを使用して `java.io.File` オブジェクトを渡します。
1. `java.io.FileOutputStream` オブジェクトの `write` メソッドを呼び出して、暗号化された PDF ドキュメントを表すデータストリームを含むバイト配列を渡します。

**関連トピック**

[クイックスタート：Java プロジェクトでの DIME を使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAML ベースの認証の使用 {#using-saml-based-authentication}

AEM Forms は、サービスを呼び出す際に、様々な web サービス認証モードをサポートしています。そのうちの 1 つは、web サービスの呼び出しで、基本認証ヘッダーを使用してユーザー名とパスワードの値の両方を指定します。AEM Forms は、SAML アサーションベースの認証もサポートしています。クライアントアプリケーションが web サービスを使用して AEM Forms サービスを呼び出すと、クライアントアプリケーションは以下のいずれかの方法で認証情報を提供できます。

* 基本認証の一部として認証情報を渡す
* WS-Security ヘッダーの一部としてユーザー名トークンを渡す
* WS-Security ヘッダーの一部として SAML アサーションを渡す
* WS-Security ヘッダーの一部として Kerberos トークンを渡す

AEM Forms は、標準の証明書ベースの認証をサポートしていませんが、別の形式による証明書ベースの認証をサポートしています。

>[!NOTE]
>
>「AEM Forms によるプログラミング」の web サービスのクイックスタートでは、認証を実行するユーザー名とパスワードの値を指定します。

AEM Forms ユーザーの ID は、秘密鍵を使用して署名された SAML アサーションを通じて表すことができます。以下の XML コードは、SAML アサーションの例を示しています。

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

この例のアサーションは、管理者ユーザーに対して発行されます。このアサーションには、以下の注目すべき項目が含まれます。

* 一定期間有効です。
* 特定のユーザーに対して発行されます。
* デジタル署名されています。したがって、変更を加えると署名が壊れてしまいます。
* ユーザー名やパスワードと同様に、ユーザーの ID のトークンとして AEM Forms に表示できます。

クライアントアプリケーションは、`AuthResult` オブジェクトを返す AEM Forms AuthenticationManager API からアサーションを取得できます。`AuthResult` インスタンスを取得するには、次の 2 つの方法のいずれかを実行します。

* AuthenticationManager API で公開されている認証メソッドのいずれかを使用して、ユーザーを認証します。通常は、ユーザー名とパスワードを使用します。ただし、証明書認証を使用することもできます。
* `AuthenticationManager.getAuthResultOnBehalfOfUser` メソッドを使用します。このメソッドを使用すると、クライアントアプリケーションは任意の AEM Forms ユーザーの `AuthResult` オブジェクトを取得できます。

AEM Forms ユーザーは、取得した SAML トークンを使用して認証できます。この SAML アサーション（xml フラグメント）は、ユーザー認証用の Web サービス呼び出しで WS-Security ヘッダーの一部として送信できます。通常、クライアントアプリケーションはユーザーを認証しましたが、ユーザー認証情報は保存されていません。（または、ユーザー名とパスワード以外のメカニズムを使用してそのクライアントにログオンします）この場合、クライアントアプリケーションは AEM Forms を呼び出し、AEM Forms の呼び出しを許可されている特定のユーザーとして実行する必要があります。

特定のユーザーとして実行するには、 web サービスを使用して `AuthenticationManager.getAuthResultOnBehalfOfUser` メソッドを呼び出します。このメソッドは、そのユーザーの SAML アサーションを含む `AuthResult` インスタンスを返します。

次に、その SAML アサーションを使用して、認証を必要とするサービスを呼び出します。このアクションでは、SOAP ヘッダーの一部としてアサーションを送信します。このアサーションで web サービスが呼び出されると、AEM Forms はユーザーをそのアサーションで表されるユーザーとして識別します。つまり、アサーションで指定されたユーザーは、サービスを呼び出すユーザーです。

### Apache Axis クラスと SAML ベースの認証の使用 {#using-apache-axis-classes-and-saml-based-authentication}

Axis ライブラリを使用して作成された Java プロキシクラスによって AEM Forms サービスを呼び出すことができます。（[Apache Axis を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)を参照してください）

SAML ベースの認証を使用する AXIS を使用する場合は、Axis にリクエストと応答ハンドラーを登録します。Apache Axis は、呼び出しリクエストを AEM Forms に送信する前にハンドラーを呼び出します。ハンドラーを登録するには、`org.apache.axis.handlers.BasicHandler` を拡張する Java クラスを作成します。

**Axis を持つ AssertionHandler の作成**

次の `AssertionHandler.java` という名前の Java クラスは、`org.apache.axis.handlers.BasicHandler` を拡張する Java クラスの例を示します。

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**ハンドラーを登録**

Axis にハンドラーを登録するには、client-config.wsdd ファイルを作成します。既定では、Axis はこの名前のファイルを検索します。次の XML コードは client-config.wsdd ファイルの例です。詳しくは、Axis のドキュメントを参照してください。

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**AEM Forms サービスを呼び出す**

次のコード例は、SAML ベースの認証を使用して AEM Forms サービスを呼び出します。

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### .NET クライアントアセンブリと SAML ベースの認証の使用 {#using-a-net-client-assembly-and-saml-based-authentication}

.NET クライアントアセンブリと SAML ベースの認証を使用して、Forms サービスを呼び出すことができます。そのためには、Web サービス拡張機能 3.0 (WSE) を使用する必要があります。WSE を使用する .NET クライアントアセンブリの作成については、[DIME を使用する .NET プロジェクトの作成](#creating-a-net-project-that-uses-dime)を参照してください。

>[!NOTE]
>
>DIME セクションでは WSE 2.0 を使用します。SAML ベースの認証を使用するには、DIME のトピックで指定される同様の手順に従います。ただし、WSE 2.0 を WSE 3.0 に置き換えます。開発用コンピューターに Web サービス拡張機能 3.0 をインストールし、Microsoft Visual Studio .NET に統合します。Web サービス拡張機能 3.0 は、[Microsoft ダウンロードセンター](https://www.microsoft.com/downloads/search.aspx)からダウンロードできます。

WSE アーキテクチャは、ポリシー、アサーション、および セキュリティトークンデータタイプを使用します。Web サービスの呼び出しで、ポリシーを指定します。 1 つのポリシーは複数のアサーションを持つことができます。各アサーションには、フィルターを含めることができます。フィルターは、Web サービス呼び出しの特定のステージで呼び出され、その際に SOAP リクエストを変更できます。 詳しくは、 Web サービス拡張機能 3.0 のドキュメントを参照してください。

**アサーションとフィルターの作成**

次の C#コードの例では、フィルタークラスとアサーションクラスを作成します。このコードの例では、SamlAssertionOutputFilter を作成します。このフィルターは、SOAP 要求が AEM Forms に送信される前に、WSE フレームワークによって呼び出されます。

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**SAML トークンの作成**

SAML アサーションを表すクラスを作成します。 このクラスが実行する主なタスクは、データ値を文字列から XML に変換し、空白を保持することです。このアサーション XML は、後で SOAP リクエストに読み込まれます。

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**AEM Forms サービスを呼び出す**

次の C# コードの例では、SAML ベースの認証を使用して Formsサ ービスを呼び出します。

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Web サービスを使用する際の関連事項 {#related-considerations-when-using-web-services}

Web サービスを使用して特定の AEM Forms サービスの操作を呼び出すと、問題が発生することがあります。ここでは、それらの問題を特定し、解決策がある場合は提供することを目的に説明します。

### 非同期でのサービス操作の呼び出し {#invoking-service-operations-asynchronously}

PDF 生成の `htmlToPDF` 操作など、AEM Forms サービスの操作を非同期で呼び出そうとすると、`SoapFaultException` が発生します。この問題を解決するには、カスタム結合 XML ファイルを作成して、`ExportPDF_Result` 要素とその他の要素を異なるクラスにマッピングします。次の XML は、カスタム結合ファイルを表しています。

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

この XML ファイルを使用すると、JAX-WS を使用して Java プロキシファイルを作成できます。（[JAX-WS を使用した Java プロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)を参照してください。）

この XML ファイルは、- `b` コマンドラインオプションを使用して JAX-WS ツール（wsimport.exe）を実行する際に参照します。結合 XML ファイルの `wsdlLocation` 要素を更新して、AEM Forms の URL を指定します。

非同期の呼び出しが確実に機能するように、エンドポイント URL の値を変更して `async=true` を指定します。例えば、JAX-WS で作成した Java プロキシファイルの場合、`BindingProvider.ENDPOINT_ADDRESS_PROPERTY` に次を指定します。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

次のリストでは、非同期で呼び出された場合にカスタム結合ファイルを必要とするその他のサービスを示しています。

* PDFG3D
* タスクマネージャー
* Application Manager
* Directory Manager
* Distiller
* Rights Management
* Document Management

### J2EE アプリケーションサーバーの違い {#differences-in-j2ee-application-servers}

特定の J2EE アプリケーションサーバーを使用して作成されたプロキシライブラリが、別の J2EE アプリケーションサーバーでホストされている AEM Forms を正常に呼び出せない場合があります。WebSphere にデプロイされた AEM Forms を使用してプロキシライブラリを生成する場合について考えてみます。このプロキシライブラリは、JBoss Application Server にデプロイされている AEM Forms のサービスを正常に呼び出せません。

AEM Forms の複雑なデータタイプ（`PrincipalReference` など）の一部は、AEM Forms を WebSphere にデプロイする場合と JBoss Application Server にデプロイする場合とで定義が異なります。異なる J2EE アプリケーションサービスで使用される JDK の違いが、WSDL 定義に違いがある理由です。そのため、同じ J2EE アプリケーションサーバーから生成されたプロキシライブラリを使用します。

### Web サービスを使用した複数のサービスへのアクセス {#accessing-multiple-services-using-web-services}

名前空間の競合により、複数のサービス WSDL 間でデータオブジェクトを共有できません。 様々なサービスでデータ型を共有できるので、サービスは WSDL でこれらの型の定義を共有します。例えば、`BLOB` データ型を含む 2 つの .NET クライアントアセンブリを、同じ .NET クライアントプロジェクトに追加することはできません。これを行おうとすると、コンパイルエラーが発生します。

次のリストは、複数のサービス WSDL 間で共有できないデータタイプを示しています。

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

この問題を回避するには、データタイプを完全に修飾することをお勧めします。例えば、サービス参照を使用して Forms サービスと Signature サービスの両方を参照する .NET アプリケーションについて考えます。両方のサービス参照には、`BLOB` クラスが含まれています。`BLOB` インスタンスを使用するには、`BLOB` オブジェクトを宣言時に完全修飾します。この方法を次のコード例に示します。このコード例について詳しくは、[インタラクティブ Forms のデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)を参照してください。

次の C# コードの例では、Forms サービスでレンダリングされるインタラクティブフォームに署名しています。このクライアントアプリケーションには 2 つのサービス参照があります。Forms サービスに関連付けられた `BLOB` インスタンスは、`SignInteractiveForm.ServiceReference2` 名前空間に属しています。同じように、Signature サービスに関連付けられた `BLOB` インスタンスは、`SignInteractiveForm.ServiceReference1` 名前空間に属しています。署名済みのインタラクティブフォームは、*LoanXFASigned.pdf* という名前の PDF ファイルとして保存されます。

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### I の文字で始まるサービスで無効なプロキシファイルが生成される {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Microsoft .Net 3.5 および WCF を使用する際、AEM Forms で一部のプロキシクラスの名前が間違って生成されます。この問題は、IBMFilenetContentRepositoryConnector、IDPSchedulerService、または名前が I の文字で始まる他のサービスに対してプロキシクラスが作成された場合に発生します。例えば、IBMFileNetContentRepositoryConnector では、生成されたクライアントの名前が `BMFileNetContentRepositoryConnectorClient` である場合です。生成されたプロキシクラスには I の文字がありません。
