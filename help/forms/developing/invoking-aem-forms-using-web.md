---
title: Web サービスを使用した AEM Forms の呼び出し
seo-title: Web サービスを使用した AEM Forms の呼び出し
description: 'null'
seo-description: 'null'
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '9966'
ht-degree: 6%

---


# Web サービスを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-web-services}

サービスコンテナ内のほとんどのAEM Formsサービスは、Webサービスを公開するように設定されており、Web Service Definition Language(WSDL)の生成を完全にサポートしています。 つまり、AEM FormsサービスのネイティブSOAPスタックを使用するプロキシオブジェクトを作成できます。 その結果、AEM Formsサービスは次のSOAPメッセージを交換して処理できます。

* **SOAP要求**: アクションを要求するクライアントアプリケーションによってFormsサービスに送信されます。
* **SOAP応答**: SOAP要求の処理後、Formsサービスによってクライアントアプリケーションに送信されます。

Webサービスを使用する場合は、Java APIを使用する場合と同じAEM Formsサービス操作を実行できます。 Webサービスを使用してAEM Formsサービスを呼び出す利点の1つは、SOAPをサポートする開発環境でクライアントアプリケーションを作成できる点です。 クライアントアプリケーションが特定の開発環境またはプログラミング言語に結び付けられるわけではありません。 例えば、Microsoft Visual Studio .NETおよびC#をプログラミング言語として使用するクライアントアプリケーションを作成できます。

AEM FormsサービスはSOAPプロトコルで公開され、WSI Basicプロファイル1.1に準拠しています。 Web Services Interoperability(WSI)は、複数のプラットフォーム間でのWebサービスの相互運用性を促進するオープンスタンダード組織です。 詳しくは、https://www.ws-i.org/を参照して [ください](https://www.ws-i.org)。

AEM Formsは、次のWebサービス標準をサポートしています。

* **エンコーディング**: ドキュメントおよびリテラルエンコーディングのみサポートします(WSI基本プロファイルに従った推奨エンコーディング)。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-base64-encoding))。
* **MTOM**: SOAP要求で添付ファイルをエンコードする方法を表します。 (MTOMを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-mtom))。
* **SwaRef**: SOAP要求で添付ファイルをエンコードする別の方法を表します。 (SwaRefを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-swaref))。
* **添付ファイル付きSOAP**: MIMEとDIME(Direct Internet Message Encapsulation)の両方をサポートします。 これらのプロトコルは、標準的なSOAP経由で添付ファイルを送信する方法です。 Microsoft Visual Studio .NETアプリケーションはDIMEを使用します。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-base64-encoding))。
* **WS-Security**: ユーザー名パスワードトークンプロファイルがサポートされます。これは、WSセキュリティSOAPヘッダーの一部として、ユーザー名とパスワードを送信する標準的な方法です。 AEM Formsは、HTTP基本認証もサポートしています。 (WS-Securityヘッダーを使用して秘密鍵証明書を [渡すを参照](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html))。

Webサービスを使用してAEM Formsサービスを呼び出すには、通常、サービスWSDLを使用するプロキシライブラリを作成します。 「Web Servicesを使用したAEM Formsの *呼び出し* 」セクションでは、JAX-WSを使用して、サービスを呼び出すJavaプロキシクラスを作成します。 (「JAX-WSを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-jax-ws)」を参照)。

次のURL定義を指定すると、サービスWDSLを取得できます（角括弧で囲まれた項目はオプションです）。

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

各パラメーターの意味は次のとおりです。

* *your_serverhost* は、J2EEアプリケーションサーバーのホスティングAEM FormsのIPアドレスを表します。
* *your_port* は、J2EEアプリケーションサーバーが使用するHTTPポートを表します。
* *service_name* は、サービス名を表します。
* *version* は、サービスのターゲットバージョンを表します（デフォルトでは、最新のサービスバージョンが使用されます）。
* `async` 非同期呼び出し `true` の追加操作を有効にする値を指定します(デフォルト `false` )。
* *lc_version* は、呼び出すAEM Formsのバージョンを表します。

次の表のリストは、WSDLの定義をサービスします(AEM Formsがローカルホストにデプロイされ、投稿が8080である場合)。

<table>
 <thead>
  <tr>
   <th><p>Service</p></th>
   <th><p>WSDLの定義</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assembler</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>戻る/復元</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>barcoded forms[barcoded forms]</p></td>
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
   <td><p>Encryption </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>フォーム</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Form Data Integration</p></td>
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
   <td><p>リポジトリ</p></td>
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

**AEM FormsプロセスのWSDL定義**

Workbenchで作成されたプロセスに属するWSDLにアクセスするには、WSDL定義内のアプリケーション名とプロセス名を指定する必要があります。 アプリケーションの名前がで、プロセスの名前 `MyApplication` がであるとし `EncryptDocument`ます。 この場合、次のWSDL定義を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>短時間のみ有効なプロセスの例について詳しくは、 `MyApplication/EncryptDocument` 短時間のみ有効なプロセスの例を参照してください [](/help/forms/developing/aem-forms-processes.md)。

>[!NOTE]
>
>アプリケーションには、フォルダーを含めることができます。 この場合、WSDL定義のフォルダー名を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Webサービスを使用した新機能へのアクセス**

新しいAEM Formsサービス機能は、Webサービスを使用してアクセスできます。 例えば、AEM Formsでは、MTOMを使用して添付ファイルをエンコードする機能が導入されます。 (MTOMを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-mtom))。

AEM Formsで導入された新しい機能にアクセスするには、WSDL定義で `lc_version` 属性を指定します。 例えば、新しいサービス機能（MTOMのサポートを含む）にアクセスするには、次のWSDL定義を指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>属性を設定する場合は、3桁の数字を使用していることを確認し `lc_version` ます。 例えば、9.0.1はバージョン9.0と等しくなります。

**WebサービスBLOBデータ型**

AEM FormsサービスWSDLは、多くのデータ型を定義します。 Webサービスで公開される最も重要なデータ型の1つは、 `BLOB` 型です。 AEM FormsのJava APIを使用する場合、このデータ型は `com.adobe.idp.Document` クラスにマッピングされます。 (See [Passing data to AEM Forms services using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

オブジェクトは、 `BLOB` AEM Formsサービスとの間でバイナリデータ（PDFファイル、XMLデータなど）の送受信を行います。 この `BLOB` 型は、サービスWSDLで次のように定義されます。

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

お `MTOM` よび `swaRef` フィールドは、AEM Formsでのみサポートされます。 これらの新しいフィールドは、 `lc_version` プロパティを含むURLを指定した場合にのみ使用できます。

**サービス要求でのBLOBオブジェクトの指定**

AEM Formsサービスの操作で、入力値として `BLOB` 型が必要な場合は、アプリケーションロジックにその `BLOB` 型のインスタンスを作成します。 (「AEM Formsによる *プログラミング」にあるWebサービスのクイック開始の多くは* 、BLOBデータ型の使用方法を示しています)。

次の手順に従って、インスタンスに属するフィールドに値を割り当て `BLOB` ます。

* **Base64**: Base64形式でエンコードされたテキストとしてデータを渡すには、フィールドにデータを設定し、 `BLOB.binaryData` フィールドにデータタイプをMIME形式(例えば、 `application/pdf`)で設定し `BLOB.contentType` ます。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-base64-encoding))。
* **MTOM**: MTOM添付ファイルにバイナリデータを渡すには、フィールドにデータを設定し `BLOB.MTOM` ます。 この設定は、Java JAX-WSフレームワークまたはSOAPフレームワークのネイティブAPIを使用して、データをSOAP要求に添付します。 (MTOMを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-mtom))。
* **SwaRef**: WS-I SwaRef添付ファイルにバイナリデータを渡すには、フィールドにデータを設定し `BLOB.swaRef` ます。 この設定は、Java JAX-WSフレームワークを使用して、SOAP要求にデータを添付します。 (SwaRefを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-swaref))。
* **MIMEまたはDIME添付ファイル**: MIME添付ファイルまたはDIME添付ファイルにデータを渡すには、SOAPフレームワークのネイティブAPIを使用して、SOAP要求にデータを添付します。 フィールドに添付ファイル識別子を設定し `BLOB.attachmentID` ます。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-base64-encoding))。
* **リモートURL**: データがWebサーバーでホストされ、HTTP URL経由でアクセスできる場合は、フィールドにHTTP URLを設定し `BLOB.remoteURL` ます。 (HTTP経由のBLOBデータを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-blob-data-over-http))。

**サービスから返されたBLOBオブジェクトのデータへのアクセス**

返される `BLOB` オブジェクトの送信プロトコルは、複数の要因に依存します。これらの要因は次の順序で考慮され、メイン条件が満たされると停止します。

1. **TargetURLは送信プロトコルを指定します**。 SOAP呼び出しで指定されたターゲットURLにパラメータ `blob="`*BLOB_TYPE *&quot;が含まれている場合、* BLOB_TYPE *が送信プロトコルを決定します。* BLOB_TYPE *は、base64、dime、mime、http、mtomまたはswarefのプレースホルダです。
1. **サービスSOAPエンドポイントがスマート**。 次の条件が真の場合、出力ドキュメントは入力ドキュメントと同じ送信プロトコルを使用して返されます。

   * サービスのSOAPエンドポイントパラメーター「Default Protocol For Output Blob Objects」が「Smart」に設定されている。

      SOAPエンドポイントを持つ各サービスに対して、返されたBLOBの送信プロトコルを管理コンソールで指定できます。 (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Formsサービスは、1つ以上のドキュメントを入力として受け取ります。

1. **サービスSOAPエンドポイントがスマートではありません**。 構成されたプロトコルはドキュメント送信プロトコルを決定し、対応する `BLOB` フィールドにデータを返す。 例えば、SOAPエンドポイントがDIMEに設定されている場合、返されるBLOBは、入力ドキュメントの送信プロトコルに関係なく、 `blob.attachmentID` フィールドに含まれます。
1. **それ以外の場合**。 サービスがドキュメントタイプを入力として受け取らない場合、HTTPプロトコルを介した `BLOB.remoteURL` フィールドに出力ドキュメントが返されます。

最初の条件で説明したように、次のようにサフィックスを付けたSOAPエンドポイントURLを拡張することで、返されるドキュメントの送信タイプを確認できます。

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

送信タイプとデータの取得元のフィールドとの相関関係を次に示します。

* **Base64形式**: フィ `blob` ールドにデータを返す `base64` には、サフィックスをに設定し `BLOB.binaryData` ます。
* **MIMEまたはDIME添付ファイル**: サフィックスをに設定する `blob` か、フ `DIME``MIME``BLOB.attachmentID` ィールドに添付ファイル識別子が返されたデータを、対応する添付ファイルの種類として返します。 SOAPフレームワーク固有のAPIを使用して、添付ファイルからデータを読み取ります。
* **リモートURL**: サフィックスを「」に設定 `blob` して、データをアプリケーションサーバーに保持し、 `http``BLOB.remoteURL` フィールド内のデータを示すURLを返します。
* **MTOMまたはSwaRef**: サフィックスをに設定する `blob` か、または `mtom` フィールドに返される添付ファイル識別子を持つデータを対応する添付ファイルタイプとして返し `swaref``BLOB.MTOM``BLOB.swaRef` ます。 SOAPフレームワークのネイティブAPIを使用して、添付ファイルからデータを読み取ります。

>[!NOTE]
>
>オブジェクトのメソッドを呼び出して `BLOB` オブジェクトを埋め込む場合は、30 MBを超えないようにして `setBinaryData` ください。 そうしないと、 `OutOfMemory` 例外が発生する可能性があります。

>[!NOTE]
>
>MTOM送信プロトコルを使用するJAX WSベースのアプリケーションは、送受信データの量が25 MBに制限されます。 この制限は、JAX-WSのバグが原因です。 送受信ファイルの合計サイズが25 MBを超える場合は、MTOM送信プロトコルの代わりにSwaRef送信プロトコルを使用します。 そうしないと、 `OutOfMemory` 例外が発生する可能性があります。

**base64エンコードされたバイト配列のMTOM送信**

MTOMプロトコルは、 `BLOB` オブジェクトに加えて、複合型のバイト配列パラメータまたはバイト配列フィールドをサポートします。 つまり、MTOMをサポートするクライアントSOAPフレームワークは、（base64エンコードされたテキストではなく）任意の `xsd:base64Binary` 要素をMTOM添付ファイルとして送信できます。 AEM FormsSOAPエンドポイントは、この種類のバイト配列エンコーディングを読み取ることができます。 ただし、AEM Formsサービスは、常にbase64エンコードされたテキストとしてバイト配列型を返します。 出力バイト配列パラメーターはMTOMをサポートしていません。

大量のバイナリデータを返すAEM Formsサービスは、バイト配列型ではなくドキュメント/BLOB型を使用します。 ドキュメントタイプは、大量のデータを送信する場合に、より効率的です。

## Webサービスのデータ型 {#web-service-data-types}

次の表に、Javaデータ型のリストと、対応するWebサービスデータ型を示します。

<table>
 <thead>
  <tr>
   <th><p>Javaデータ型</p></th>
   <th><p>Webサービスのデータ型</p></th>
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
   <td><p>サービスWSDLで次のように定義される <code>DATE</code> 型です。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が <code>java.util.Date</code> 値を入力として受け取る場合、SOAPクライアントアプリケーションは、 <code>DATE.date</code> フィールドに日付を渡す必要があります。 この場合、 <code>DATE.calendar</code> フィールドを設定するとランタイムの例外が発生します。 サービスがaを返す場合 <code>java.util.Date</code>、日付は <code>DATE.date</code> フィールドに返されます。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>サービスWSDLで次のように定義される <code>DATE</code> 型です。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が <code>java.util.Calendar</code> 値を入力として受け取る場合、SOAPクライアントアプリケーションは、 <code>DATE.caledendar</code> フィールドに日付を渡す必要があります。 この場合、 <code>DATE.date</code> フィールドを設定すると実行時例外が発生します。 サービスが値を返す場合 <code>java.util.Calendar</code>は、日付が <code>DATE.calendar</code> フィールドに返されます。 </p></td>
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
   <td><p>サービス <code>apachesoap:Map</code>WSDLで次のように定義される。</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>マップは、キー/値のペアのシーケンスとして表されます。</p></td>
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
   <td><p>XML型。サービスWSDLで次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が <code>org.w3c.dom.Document</code> 値を受け取る場合は、XMLデータを <code>XML.document</code> フィールドに渡します。</p><p>この <code>XML.element</code> フィールドを設定すると、ランタイム例外が発生します。 サービスがXMLを返す場合 <code>org.w3c.dom.Document</code>、XMLデータが <code>XML.document</code> フィールドに返されます。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML型。サービスWSDLで次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が入力と <code>org.w3c.dom.Element</code> してを受け取る場合は、XMLデータを <code>XML.element</code> フィールドに渡します。</p><p>この <code>XML.document</code> フィールドを設定すると、ランタイム例外が発生します。 サービスがXMLデータを返す場合 <code>org.w3c.dom.Element</code>、XMLデータは <code>XML.element</code> フィールドに返されます。</p></td>
  </tr>
 </tbody>
</table>

**Adobe Developer Web サイト**

アドビ開発者Webサイトには、WebサービスAPIを使用してAEM Formsサービスを呼び出す方法について説明する次の記事が含まれています。

[フォームレンダリングASP.NETアプリケーションの作成](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[カスタムコンポーネントを使用したWebサービスの呼び出し](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>カスタムコンポーネントを使用してWebサービスを呼び出すには、サードパーティのWebサービスを呼び出すAEM Formsコンポーネントを作成する方法を説明します。

## JAX-WSを使用したJavaプロキシクラスの作成 {#creating-java-proxy-classes-using-jax-ws}

JAX-WSを使用して、FormsサービスのWSDLをJavaプロキシクラスに変換できます。 AEM Formsサービスの操作を呼び出すことを可能にするクラスです。 Apache Antでは、AEM FormsサービスWSDLを参照してJavaプロキシクラスを生成するビルドスクリプトを作成できます。 JAX-WSプロキシファイルは、次の手順を実行して生成できます。

1. クライアントコンピューターにApache Antをインストールします。 (https://ant.apache.org/bindownload.cgi [を参照](https://ant.apache.org/bindownload.cgi))。

   * 追加binディレクトリからクラスパスに移動します。
   * 環境変数を、Antをインストールしたディレクトリに設定します。 `ANT_HOME`

1. JDK 1.6以降をインストールします。

   * JDK binデ追加ィレクトリをクラスパスに追加します。
   * JRE binデ追加ィレクトリをクラスパスに格納します。 このbinは、 `[JDK_INSTALL_LOCATION]/jre` ディレクトリ内にあります。
   * 環境変数に、JDKをインストールしたディレクトリを設定します。 `JAVA_HOME`

   JDK 1.6には、build.xmlファイルで使用されるwsimportプログラムが含まれています。 JDK 1.5には、このプログラムは含まれていません。

1. JAX-WSをクライアントコンピューターにインストールします。 (「 [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)」を参照)。
1. JAX-WSとApache Antを使用してJavaプロキシクラスを生成します。 このタスクを実行するAntビルドスクリプトを作成します。 次のスクリプトは、build.xmlという名前のAnt構築スクリプトの例です。

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

   このAnt構築スクリプトでは、 `url` プロパティがlocalhostで実行されているEncryptionサービスWSDLを参照するように設定されています。 お `username` よび `password` プロパティは、有効なAEM formsのユーザー名とパスワードに設定する必要があります。 URLに属性が含まれていることに注意してくだ `lc_version` さい。 この `lc_version` オプションを指定しないと、新しいAEM Formsサービス操作を呼び出すことはできません。

   >[!NOTE]
   >
   >Javaプロキシクラス `EncryptionService`を使用して呼び出すAEM Formsサービス名に置き換えます。 例えば、Rights Managementサービス用のJavaプロキシクラスを作成するには、次のように指定します。

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. BATファイルを作成して、Ant構築スクリプトを実行します。 次のコマンドは、Ant構築スクリプトを実行するBATファイル内にあります。

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   ANTビルドスクリプトをC:\Program Files\Java\jaxws-ri\bin directoryフォルダーに配置します。 スクリプトは、にJAVAファイルを書き込みます。/classesフォルダー スクリプトによって、サービスを呼び出すことのできるJAVAファイルが生成されます。

1. JAVAファイルをJARファイルにパッケージ化します。 Eclipseを使用する場合は、次の手順に従います。

   * プロキシJAVAファイルをJARファイルにパッケージ化するために使用する新しいJavaプロジェクトを作成します。
   * プロジェクトにソースフォルダーを作成します。
   * Sourceフォルダーで `com.adobe.idp.services` パッケージを作成します。
   * パッケージを選択 `com.adobe.idp.services` し、adobe/idp/servicesフォルダーからパッケージにJAVAファイルを読み込みます。
   * 必要に応じて、Sourceフォルダーに `org/apache/xml/xmlsoap` パッケージを作成します。
   * ソースフォルダーを選択し、org/apache/xml/xmlsoapフォルダーからJAVAファイルを読み込みます。
   * Javaコンパイラーの準拠レベルを5.0以上に設定します。
   * プロジェクトをビルドします。
   * プロジェクトをJARファイルとしてエクスポートします。
   * このJARファイルをクライアントプロジェクトのクラスパスに読み込みます。 さらに、&lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdpartyにあるすべてのJARファイルをインポートします。

   >[!NOTE]
   >
   >「AEM Formsによるプログラミング」にあるすべてのJava Webサービスのクイック開始（Formsサービスを除く）は、JAX-WSを使用してJavaプロキシファイルを作成します。 また、すべてのJava Webサービスクイック開始では、SwaRefを使用します。 (SwaRefを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-swaref))。

**関連トピック**

[Apache Axisを使用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)

[Base64エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP経由のBLOBデータを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

[SwaRefを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)

## Apache Axisを使用したJavaプロキシクラスの作成 {#creating-java-proxy-classes-using-apache-axis}

Apache Axis WSDL2Javaツールを使用して、FormsサービスをJavaプロキシクラスに変換できます。 Formsサービス操作を呼び出すことができるクラスです。 Apache Antを使用して、サービスWSDLからAxisライブラリファイルを生成できます。 Apache Axisはhttps://ws.apache.org/axis/のURLからダウンロードでき [ます](https://ws.apache.org/axis/)。

>[!NOTE]
>
>Formsサービスに関連付けられているWebサービスクイック開始は、Apache Axisを使用して作成されたJavaプロキシクラスを使用します。 Forms Webサービスのクイック開始では、エンコードの種類としてBase64も使用されます。 (「 [FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)」を参照)。

次の手順を実行して、Axis Javaライブラリファイルを生成できます。

1. クライアントコンピューターにApache Antをインストールします。 https://ant.apache.org/bindownload.cgiで入手でき [ます](https://ant.apache.org/bindownload.cgi)。

   * 追加binディレクトリからクラスパスに移動します。
   * 環境変数を、Antをインストールしたディレクトリに設定します。 `ANT_HOME`

1. Apache Axis 1.4をクライアントコンピューターにインストールします。 https://ws.apache.org/axis/で入手でき [ます](https://ws.apache.org/axis/.md)。
1. WebサービスクライアントでAxis JARファイルを使用するためのクラスパスを設定します。詳しくは、https://ws.apache.org/axis/java/install.htmlのAxisインストール手順を参照してく [ださい](https://ws.apache.org/axis/java/install.html)。
1. Apache WSDL2Javaツールを軸で使用してJavaプロキシクラスを生成します。 このタスクを実行するAntビルドスクリプトを作成します。 次のスクリプトは、build.xmlという名前のAnt構築スクリプトの例です。

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

   このAnt構築スクリプトでは、 `url` プロパティがlocalhostで実行されているEncryptionサービスWSDLを参照するように設定されています。 お `username` よび `password` プロパティは、有効なAEM formsのユーザー名とパスワードに設定する必要があります。

1. BATファイルを作成して、Ant構築スクリプトを実行します。 次のコマンドは、Ant構築スクリプトを実行するBATファイル内にあります。

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVAファイルは、C:\JavaFiles folder as specified by the `output` プロパティに書き込まれます。 Formsサービスを正常に呼び出すには、これらのJAVAファイルをクラスパスに読み込みます。

   デフォルトでは、これらのファイルは、という名前のJavaパッケージに属してい `com.adobe.idp.services`ます。 これらのJAVAファイルは、JARファイルに配置することをお勧めします。 次に、JARファイルをクライアントアプリケーションのクラスパスに読み込みます。

   >[!NOTE]
   >
   >.JAVAファイルをJARに配置する方法はいくつかあります。 1つは、EclipseのようなJava IDEを使用する方法です。 Javaプロジェクトを作成し、 `com.adobe.idp.services`パッケージを作成します（すべての.JAVAファイルがこのパッケージに属します）。 次に、すべての.JAVAファイルをパッケージにインポートします。 最後に、プロジェクトをJARファイルとしてエクスポートします。

1. クラス内のURLを修正して、エンコーディングタイプを指定します。 `EncryptionServiceLocator` 例えば、base64を使用する場合は、 `?blob=base64``BLOB` オブジェクトがバイナリデータを返すように指定します。 つまり、 `EncryptionServiceLocator` クラス内で次のコード行を探します。

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   次に変更します。

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 次追加のAxis JARファイルをJavaプロジェクトのクラスパスに追加します。

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

   これらのJARファイルは、 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` ディレクトリにあります。

**関連トピック**

[JAX-WSを使用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)

[Base64エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP経由のBLOBデータを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

## Base64エンコーディングを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-base64-encoding}

Base64エンコーディングを使用してAEM Formsサービスを呼び出すことができます。 Base64エンコードは、Webサービス呼び出し要求で送信される添付ファイルをエンコードします。 つまり、 `BLOB` データはBase64エンコードされ、SOAPメッセージ全体ではありません。

「Base64エンコーディングを使用したAEM Formsの呼び出し」では、Base64エンコーディングを使用して名前が付けられた、以下のAEM Formsの短時間のみ有効なプロセス `MyApplication/EncryptDocument` を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

### Base64エンコーディングを使用する.NETクライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NETクライアントアセンブリを作成して、Microsoft Visual Studio .NETプロジェクトからFormsサービスを呼び出すことができます。 base64エンコーディングを使用する.NETクライアントアセンブリを作成するには、次の手順を実行します。

1. AEM Formsの呼び出しURLに基づいてプロキシクラスを作成します。
1. .NETクライアントアセンブリを作成するMicrosoft Visual Studio .NETプロジェクトを作成します。

**プロキシクラスの作成**

Microsoft Visual Studioに付属のツールを使用して、.NETクライアントアセンブリの作成に使用するプロキシクラスを作成できます。 ツールの名前はwsdl.exeで、Microsoft Visual Studioのインストールフォルダーにあります。 プロキシクラスを作成するには、コマンドプロンプトを開き、wsdl.exeファイルが格納されているフォルダーに移動します。 wsdl.exeツールの詳細については、 *MSDNヘルプを参照してください*。

コマンドプロンプトで次のコマンドを入力します。

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

デフォルトでは、このツールは、WSDLの名前に基づいて同じフォルダーにCSファイルを作成します。 この場合、EncryptDocumentService.csという名前のCSファイルが作成さ *れます*。 このCSファイルを使用して、呼び出しURLで指定されたサービスを呼び出すためのプロキシオブジェクトを作成します。

プロキシクラスのURLを修正し、オブジェクトがバイナリデータ `?blob=base64` を確実に返すようにを含めるようにし `BLOB` ます。 プロキシクラスで、次のコード行を探します。

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

次に変更します。

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

「Base64 Encodingを使用した *AEM Formsの* 呼び出し `MyApplication/EncryptDocument` 」の節では、例としてを使用しています。 別のFormsサービス用に.NETクライアントアセンブリを作成する場合は、をサービス名に置き換え `MyApplication/EncryptDocument` てください。

**.NETクライアントアセンブリの開発**

.NETクライアントアセンブリを生成するVisual Studioクラスライブラリプロジェクトを作成します。 wsdl.exeを使用して作成したCSファイルは、このプロジェクトに読み込むことができます。 このプロジェクトは、DLLファイル（.NETクライアントアセンブリ）を生成し、他のVisual Studio .NETプロジェクトで使用してサービスを呼び出すことができます。

1. 開始Microsoft Visual Studio .NET。
1. クラスライブラリプロジェクトを作成し、DocumentServiceという名前を付けます。
1. wsdl.exeを使用して作成したCSファイルを読み込みます。
1. [ **プロジェクト****]メニューで、[**&#x200B;参照]を選択します。
1. [追加参照]ダイアログボックスで、[ **System.Web.Services.dll**]を選択します。
1. Click **Select** and then click **OK**.
1. プロジェクトをコンパイルしてビルドします。

>[!NOTE]
>
>この手順では、DocumentService.dllという名前の.NETクライアントアセンブリが作成されます。このアセンブリを使用して、SOAP要求をサー `MyApplication/EncryptDocument` ビスに送信できます。

>[!NOTE]
>
>.NETクライアントアセンブリ `?blob=base64` の作成に使用するプロキシクラスのURLにを追加していることを確認してください。 そうしないと、 `BLOB` オブジェクトからバイナリデータを取得できません。

**.NETクライアントアセンブリの参照**

新しく作成した.NETクライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。 .NETクライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 プロジェクトから `System.Web.Services` ライブラリも参照します。 このライブラリを参照しない場合、.NETクライアントアセンブリを使用してサービスを呼び出すことはできません。

1. [ **プロジェクト****]メニューで、[**&#x200B;参照]を選択します。
1. Click the **.NET** tab.
1. 「 **参照** 」をクリックし、DocumentService.dllファイルを探します。
1. Click **Select** and then click **OK**.

**Base64エンコーディングを使用する.NETクライアントアセンブリを使用してサービスを呼び出す**

Base64エンコーディングを使用する.NETクライアントアセンブリを使用して、（Workbenchで構築された） `MyApplication/EncryptDocument` サービスを呼び出すことができます。 サー `MyApplication/EncryptDocument` ビスを呼び出すには、次の手順を実行します。

1. サービスWSDLを使用するMicrosoft .NETクライアントアセンブリを作成し `MyApplication/EncryptDocument` ます。
1. クライアントMicrosoft .NETプロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NETクライアントアセンブリを参照します。 参照先 `System.Web.Services`。
1. Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `MyApplication_EncryptDocumentService` オブジェクトを作成します。
1. オブジェクトのプロ `MyApplication_EncryptDocumentService` パティをオブジ `Credentials``System.Net.NetworkCredential` ェクトに設定します。 コンストラクター内で、AEM Formsのユーザー名と対応するパスワードを指定します。 `System.Net.NetworkCredential` 認証値を設定して、.NETクライアントアプリケーションがSOAPメッセージをAEM Formsと正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、プロセスに渡されるPDFドキュメントの保存に使用され `MyApplication/EncryptDocument` ます。
1. Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
1. オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
1. オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
1. オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``binaryData` オブジェクトを入力します。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出し、PDFドキュメントを含む `MyApplication_EncryptDocumentService``invoke``BLOB` オブジェクトを渡して、プロセスを呼び出します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. コンストラクターを呼び出し、パスワードで暗号化されたドキュメントーのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
1. オブジェクトのメソッドから返される `BLOB` オブジェクトのデータ内容を格納するバイト配列 `MyApplicationEncryptDocumentService` を作成し `invoke` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡して、 `System.IO.BinaryWriter``Write` バイト配列の内容をPDFファイルに書き込みます。

### JavaプロキシクラスとBase64エンコーディングを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

JavaプロキシクラスとBase64を使用して、AEM Formsサービスを呼び出すことができます。 Javaプロキシクラスを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次の手順を実行します。

1. サー `MyApplication/EncryptDocument` ビスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを作成します。 次のWSDLエンドポイントを使用します。

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >J2EE Application ServierのホスティングAEM Forms `hiro-xp`*のIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、 `MyApplicationEncryptDocumentService` オブジェクトを作成 `getEncryptDocument` します。
1. 次のデータメンバーに値を割り当てて、AEM Formsの呼び出しに必要な接続値を設定します。

   * WSDLの終点とエンコードの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。 Base64エンコーディングを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次のURL値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM formsユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコードの例は、このアプリケーションロジックを示しています。

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクターを使用してオブジェクトを作成し、 `MyApplication/EncryptDocument` プロセスに送信するPDFドキュメントを取得し `java.io.FileInputStream` ます。 PDFドキュメントの場所を指定するstring値を渡します。
1. バイト配列を作成し、 `java.io.FileInputStream` オブジェクトのコンテンツを設定します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. メソッドを呼び出し、バイト配列を渡して、 `BLOB` オブジェクトを入力し `setBinaryData` ます。 Base64エンコ `BLOB` ーディングを使用している場合に呼び出すメソッドは、オブジェクト `setBinaryData` です。 サービス要求でのBLOBオブジェクトの供給を参照してください。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出して、 `MyApplicationEncryptDocument` プロセスを呼び出し `invoke` ます。 PDFドキュメントを含む `BLOB` オブジェクトを渡します。 呼び出しメソッドは、暗号化されたPDFドキュメントを含む `BLOB` オブジェクトを返します。
1. オブジェクトのメソッドを呼び出して、暗号化されたPDFドキュメントを含むバイト配列を作成 `BLOB` し `getBinaryData` ます。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。 バイト配列をファイルに書き込みます。

**関連トピック**

[クイック開始: JavaプロキシファイルとBase64エンコーディングを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOMを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-mtom}

AEM Formsサービスは、Webサービス標準のMTOMを使用して呼び出すことができます。 この標準は、PDFドキュメントなどのバイナリデータをインターネットまたはイントラネット経由で送信する方法を定義します。 MTOMの特徴は、 `XOP:Include` 要素の使用です。 この要素は、SOAPメッセージのバイナリ添付ファイルを参照するために、XML Binary Optimized Packaging(XOP)仕様で定義されます。

The discussion here is about using MTOM to invoke the following AEM Forms short-lived process named `MyApplication/EncryptDocument`.

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>MTOMのサポートは、AEM Forms9で追加されました。

>[!NOTE]
>
>MTOM送信プロトコルを使用するJAX WSベースのアプリケーションは、送受信データの量が25 MBに制限されます。 この制限は、JAX-WSのバグが原因です。 送受信ファイルの合計サイズが25 MBを超える場合は、MTOM送信プロトコルの代わりにSwaRef送信プロトコルを使用します。 そうしないと、 `OutOfMemory` 例外が発生する可能性があります。

ここでは、Microsoft .NETプロジェクト内でMTOMを使用してAEM Formsサービスを呼び出す方法について説明します。 使用される.NETフレームワークは3.5で、開発環境はVisual Studio 2008です。 開発用コンピューターにWeb Service Enhancements (WSE)がインストールされている場合は、それを削除します。 .NET 3.5フレームワークは、Windows Communication Foundation (WCF)という名前のSOAPフレームワークをサポートしています。 MTOMを使用してAEM Formsを呼び出す場合、WCF（WSEではない）のみがサポートされます。

### MTOMを使用してサービスを呼び出す.NETプロジェクトの作成 {#creating-a-net-project-that-invokes-a-service-using-mtom}

Webサービスを使用してAEM Formsサービスを呼び出すことができるMicrosoft .NETプロジェクトを作成できます。 まず、Visual Studio 2008を使用してMicrosoft .NETプロジェクトを作成します。 AEM Formsサービスを呼び出すには、プロジェクト内で呼び出すAEM Formsサービスへのサービス参照を作成します。 サービス参照を作成する場合、AEM FormsサービスへのURLを指定します。

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

AEM Forms `localhost` をホストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。 呼び出 `MyApplication/EncryptDocument` すAEM Formsサービスの名前に置き換えます。 例えば、Rights Management操作を呼び出すには、次のように指定します。

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

この `lc_version` オプションを使用すると、MTOMなどのAEM Forms機能を使用できるようになります。 この `lc_version` オプションを指定しないと、MTOMを使用してAEM Formsを呼び出すことはできません。

サービス参照を作成すると、AEM Formsサービスに関連付けられたデータ型を.NETプロジェクト内で使用できるようになります。 AEM Formsサービスを呼び出す.NETプロジェクトを作成するには、次の手順を実行します。

1. Microsoft Visual Studio 2008を使用して.NETプロジェクトを作成します。
1. 「 **プロジェクト****」メニューで、「**&#x200B;サービス参照」を選択します。
1. 「 **アドレス** 」ダイアログボックスで、AEM FormsサービスのWSDLを指定します。 例：

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Click **Go** and then click **OK**.

### .NETプロジェクトでMTOMを使用してサービスを呼び出す {#invoking-a-service-using-mtom-in-a-net-project}

保護されていないPDFドキュメントを受け取り、パスワードで暗号化されたPDFドキュメントを返す `MyApplication/EncryptDocument` プロセスについて検討します。 MTOMを使用して（Workbenchで構築された） `MyApplication/EncryptDocument` プロセスを呼び出すには、次の手順を実行します。

1. Microsoft .NETプロジェクトを作成します。
1. Create a `MyApplication_EncryptDocumentClient` object by using its default constructor.
1. Create a `MyApplication_EncryptDocumentClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに渡し、エンコードの種類を指定するstring値を渡します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、必ず指定を行ってください `?blob=mtom`。

   >[!NOTE]
   >
   >J2EE Application ServierのホスティングAEM Forms `hiro-xp`*のIPアドレスに置き換えます。*

1. データメンバの値を取得して、 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `EncryptDocumentClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
1. オブジェクトの `System.ServiceModel.BasicHttpBinding` デー `MessageEncoding` タメンバをに設定し `WSMessageEncoding.Mtom`ます。 この値により、MTOMが使用されます。
1. 次のタスクを実行して、基本的なHTTP認証を有効にします。

   * AEM Formsのユーザー名をデータメンバーに割り当て `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`ます。
   * 対応するパスワード値をデータメンバーに割り当て `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`ます。
   * 定数値をデータメンバ `HttpClientCredentialType.Basic` ーに割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をデータメンバ `BasicHttpSecurityMode.TransportCredentialOnly` ーに割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

   次のコードの例は、これらのタスクを示しています。

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

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、プロセスに渡すPDFドキュメントの格納に使用され `MyApplication/EncryptDocument` ます。
1. Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
1. オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
1. オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
1. バイト配列の内容を `BLOB``MTOM` データメンバに割り当てて、オブジェクトを入力します。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出して、 `MyApplication_EncryptDocumentClient` プロセスを呼び出し `invoke` ます。 PDFドキュメントを含む `BLOB` オブジェクトを渡します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. コンストラクターを呼び出し、保護されたPDF `System.IO.FileStream` ドキュメントーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
1. メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `invoke` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

>[!NOTE]
>
>ほとんどのAEM Formsサービス操作には、MTOMのクイック開始があります。 これらのクイック開始は、サービスの対応するクイック開始セクションで表示できます。 例えば、「Outputのクイック開始」の節については、「 [Output Service APIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)」を参照してください。

**関連トピック**

[クイック開始: .NETプロジェクトでMTOMを使用してサービスを呼び出す](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Webサービスを使用した複数のサービスへのアクセス](#accessing-multiple-services-using-web-services)

[人間中心の長期間有効なプロセスを呼び出すASP.NET Webアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRefを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-swaref}

SwaRefを使用してAEM Formsサービスを呼び出すことができます。 XML要素のコンテンツは、添付ファイルへの参照を格納するSOAP本体内の添付ファイルとして送信されます。 `wsi:swaRef` SwaRefを使用してFormsサービスを呼び出す場合は、Java API for XML Web Services(JAX-WS)を使用してJavaプロキシクラスを作成します。 (「 [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)」を参照)。

ここでは、SwaRefを使用して名前が付けられた、以下のFormsの短時間のみ有効なプロセス `MyApplication/EncryptDocument` を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>AEM FormsにSwaRefのサポートが追加されました

以下では、Javaクライアントアプリケーション内でSwaRefを使用してFormsサービスを呼び出す方法について説明します。 Javaアプリケーションは、JAX-WSを使用して作成されたプロキシクラスを使用します。

### SwaRefを使用するJAX-WSライブラリファイルを使用してサービスを呼び出す {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

JAX-WSとSwaRefを使用して作成されたJavaプロキシファイルを使用して `MyApplication/EncryptDocument` プロセスを呼び出すには、次の手順を実行します。

1. サー `MyApplication/EncryptDocument` ビスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを作成します。 次のWSDLエンドポイントを使用します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、「JAX-WSを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-jax-ws)」を参照してください。

   >[!NOTE]
   >
   >J2EE Application Server `hiro-xp`*のホストAEM FormsのIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、 `MyApplicationEncryptDocumentService` オブジェクトを作成 `getEncryptDocument` します。
1. 次のデータメンバーに値を割り当てて、AEM Formsの呼び出しに必要な接続値を設定します。

   * WSDLの終点とエンコードの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。 SwaRefエンコーディングを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次のURL値を指定します。

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM formsユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコードの例は、このアプリケーションロジックを示しています。

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクターを使用してオブジェクトを作成し、 `MyApplication/EncryptDocument` プロセスに送信するPDFドキュメントを取得し `java.io.File` ます。 PDFドキュメントの場所を指定するstring値を渡します。
1. Create a `javax.activation.DataSource` object by using the `FileDataSource` constructor. Pass the `java.io.File` object.
1. コンストラクタを使用して `javax.activation.DataHandler` オブジェクトを渡すことによって、`javax.activation.DataSource` オブジェクトを作成します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. メソッドを呼び出し、オブジェクトを渡すことで、 `BLOB` オブジェクトを入力し `setSwaRef` ま `javax.activation.DataHandler` す。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出し、PDFドキュメントを含む `MyApplicationEncryptDocument``invoke``BLOB` オブジェクトを渡して、プロセスを呼び出します。 呼び出しメソッドは、暗号化されたPDFドキュメントを含む `BLOB` オブジェクトを返します。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び出して、 `BLOB` オブジェクトを入力し `getSwaRef` ます。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び出して、 `java.io.InputSteam` オブジェクトを `javax.activation.DataHandler``getInputStream` インスタンスに変換します。
1. 暗号化されたPDF `java.io.InputSteam` ドキュメントを表すPDFファイルにインスタンスを書き込みます。

>[!NOTE]
>
>ほとんどのAEM Formsサービス操作には、SwaRefのクイック開始があります。 これらのクイック開始は、サービスの対応するクイック開始セクションで表示できます。 例えば、「Outputのクイック開始」の節については、「 [Output Service APIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)」を参照してください。

**関連トピック**

[クイック開始: JavaプロジェクトでのSwaRefを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP経由のBLOBデータを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-blob-data-over-http}

Webサービスを使用してAEM Formsサービスを呼び出し、HTTP経由でBLOBデータを渡すことができます。 HTTP経由でBLOBデータを渡す方法は、base64エンコード、DIME、またはMIMEを使用する代わりに、代替の方法です。 例えば、Web Service Enhancement 3.0を使用するMicrosoft .NETプロジェクトで、DIMEやMIMEをサポートしていないデータをHTTP経由で渡すことができます。 HTTP経由でBLOBデータを使用する場合、AEM Formsサービスが呼び出される前に入力データがアップロードされます。

「HTTP経由のBLOBデータを使用したAEM Formsの呼び出し」では、HTTP経由でBLOBデータを渡すことによって名前が付けられた、以下のAEM Formsーの短時間のみ有効なプロセス `MyApplication/EncryptDocument` を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>SOAPを使用したAEM Formsの呼び出しについて詳しくあることをお勧めします。 (See [Invoking AEM Forms using Web Services](#invoking-aem-forms-using-web-services).)

### HTTP経由のデータを使用する.NETクライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-data-over-http}

HTTP経由でデータを使用するクライアントアセンブリを作成するには、Base64エンコーディングを使用したAEM Formsの [呼び出しで指定したプロセスに従い](#invoking-aem-forms-using-base64-encoding)ます。 ただし、プロキシクラスのURLを修正して、の `?blob=http` 代わりにを含めるようにし `?blob=base64`ます。 この操作により、データはHTTP経由で渡されます。 プロキシクラスで、次のコード行を探します。

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

次に変更します。

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clientMyApplication/EncryptDocumentアセンブリの参照**

新しい.NETクライアントアセンブリを、クライアントアプリケーションを開発するコンピューターに配置します。 .NETクライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 プロジェクトから `System.Web.Services` ライブラリを参照します。 このライブラリを参照しない場合、.NETクライアントアセンブリを使用してサービスを呼び出すことはできません。

1. [ **プロジェクト****]メニューで、[**&#x200B;参照]を選択します。
1. Click the **.NET** tab.
1. 「 **参照** 」をクリックし、DocumentService.dllファイルを探します。
1. Click **Select** and then click **OK**.

**HTTP経由でBLOBデータを使用する.NETクライアントアセンブリを使用してサービスを呼び出す**

HTTP経由のデータを使用する.NETクライアントアセンブリを使用して、（Workbenchで構築された） `MyApplication/EncryptDocument` サービスを呼び出すことができます。 サー `MyApplication/EncryptDocument` ビスを呼び出すには、次の手順を実行します。

1. .NETクライアントアセンブリを作成します。
1. Microsoft .NETクライアントアセンブリを参照します。 クライアントMicrosoft .NETプロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NETクライアントアセンブリを参照します。 参照先 `System.Web.Services`。
1. Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して `MyApplication_EncryptDocumentService` オブジェクトを作成します。
1. オブジェクトのプロ `MyApplication_EncryptDocumentService` パティをオブジ `Credentials``System.Net.NetworkCredential` ェクトに設定します。 コンストラクター内で、AEM Formsのユーザー名と対応するパスワードを指定します。 `System.Net.NetworkCredential` 認証値を設定して、.NETクライアントアプリケーションがSOAPメッセージをAEM Formsと正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、プロセスにデータを渡すために使用され `MyApplication/EncryptDocument` ます。
1. サー `BLOB` ビスに渡すPDFドキュメントのURIの場所を指定する、 `remoteURL` オブジェクトの `MyApplication/EncryptDocument`データメンバーに文字列値を割り当てます。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出し、オブジェクトを渡して、 `MyApplication_EncryptDocumentService``invoke``BLOB` プロセスを呼び出します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. コンストラクターを使用し、返される `System.UriBuilder` オブジェクトの `BLOB``remoteURL` データメンバーの値を渡して、オブジェクトを作成します。
1. オブジェクト `System.UriBuilder` をオブジェクトに変換し `System.IO.Stream` ます。 (このリストの後のC#クイック開始は、このタスクの実行方法を示しています)。
1. バイト配列を作成し、 `System.IO.Stream` オブジェクト内のデータを使用して配置します。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡して、 `System.IO.BinaryWriter``Write` バイト配列の内容をPDFファイルに書き込みます。

### JavaプロキシクラスとBLOBデータを使用したHTTP経由のサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

JavaAEM FormsクラスとBLOBデータをHTTP経由で使用してプロキシサービスを呼び出すことができます。 Javaプロキシクラスを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次の手順を実行します。

1. サー `MyApplication/EncryptDocument` ビスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを作成します。 次のWSDLエンドポイントを使用します。

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、「JAX-WSを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-jax-ws)」を参照してください。

   >[!NOTE]
   >
   >J2EE Application Server `hiro-xp`*のホストAEM FormsのIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、 `MyApplicationEncryptDocumentService` オブジェクトを作成 `getEncryptDocument` します。
1. 次のデータメンバーに値を割り当てて、AEM Formsの呼び出しに必要な接続値を設定します。

   * WSDLの終点とエンコードの種類を `javax.xml.ws.BindingProvider` オブジェクトの `ENDPOINT_ADDRESS_PROPERTY` フィールドに割り当てます。 BLOB over HTTPエンコーディングを使用して `MyApplication/EncryptDocument` サービスを呼び出すには、次のURL値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM formsユーザーを `javax.xml.ws.BindingProvider` オブジェクトの `USERNAME_PROPERTY` フィールドに割り当てます。
   * 対応するパスワード値を `javax.xml.ws.BindingProvider` オブジェクトの `PASSWORD_PROPERTY` フィールドに割り当てます。

   次のコードの例は、このアプリケーションロジックを示しています。

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
1. メソッドを呼び出して、 `BLOB` オブジェクトを入力し `setRemoteURL` ます。 サービスに渡すPDFドキュメントのURI位置を指定するstring値を渡し `MyApplication/EncryptDocument` ます。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出し、PDFドキュメントを含む `MyApplicationEncryptDocument``invoke``BLOB` オブジェクトを渡して、プロセスを呼び出します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. 暗号化されたPDFドキュメントを表すデータストリームを格納するバイト配列を作成します。 オブジェクトの `BLOB` メソッドを呼び出します( `getRemoteURL` メソッドが返す `BLOB``invoke` オブジェクトを使用します)。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. オブジェクトの `java.io.FileOutputStream` メソッドを呼び出し `write` ます。 暗号化されたPDFドキュメントを表すデータストリームを含むbyte配列を渡します。

## DIMEを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-dime}

添付ファイルを持つSOAPを使用してAEM Formsサービスを呼び出すことができます。 AEM Formsは、MIMEとDIMEの両方のWebサービス標準をサポートしています。 DIMEを使用すると、添付ファイルをエンコードする代わりに、PDFドキュメントなどのバイナリ添付ファイルを呼び出し要求と共に送信できます。 「DIMEを使用したAEM Formsの *呼び出し」節では、DIMEを使用した短時間プロセスの呼び出しについて説明*`MyApplication/EncryptDocument` します。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

このプロセスは、既存の AEM Forms プロセスに基づいていません。To follow along with the code examples, create a process named `MyApplication/EncryptDocument` using Workbench. （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

>[!NOTE]
>
>DIMEを使用したAEM Formsサービス操作の呼び出しは、非推奨です。 MTOMを使用することをお勧めします。 (MTOMを使用したAEM Formsの [呼び出しを参照](#invoking-aem-forms-using-mtom))。

### DIMEを使用する.NETプロジェクトの作成 {#creating-a-net-project-that-uses-dime}

DIMEを使用してFormsサービスを呼び出すことができる.NETプロジェクトを作成するには、次のタスクを実行します。

* 開発用コンピューターにWeb Services Enhancements 2.0をインストールします。
* .NETプロジェクト内から、FormsAEM FormsサービスへのWeb参照を作成します。

**Web Services Enhancements 2.0のインストール**

Web Services Enhancements 2.0を開発用コンピューターにインストールし、Microsoft Visual Studio .NETと統合します。 Web Services Enhancements 2.0は、 [Microsoftダウンロードセンターからダウンロードできます。](https://www.microsoft.com/downloads/search.aspx)

このWebページで、Web Services Enhancements 2.0を検索し、開発用コンピューターにダウンロードします。 このダウンロードにより、Microsoft WSE 2.0 SPI.msiという名前のファイルがコンピューターに配置されます。 インストールプログラムを実行し、オンラインの指示に従います。

>[!NOTE]
>
>Web Services Enhancements 2.0はDIMEをサポートします。 Web Services Enhancements 2.0を使用する場合、サポートされるMicrosoft Visual Studioのバージョンは2003です。Web Services Enhancements 3.0はDIMEをサポートしません。 しかし、MTOMをサポートしています。

**AEM FormsサービスへのWeb参照の作成**

Web Services Enhancements 2.0を開発コンピューターにインストールし、Microsoft .NETプロジェクトを作成したら、FormsサービスへのWeb参照を作成します。 例えば、プロセスへのWeb参照を作成し、Formsがローカルコンピューターにインストールされている場合は、次のURLを指定します。 `MyApplication/EncryptDocument`

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Web参照を作成した後、.NETプロジェクト内で使用できるプロキシデータには次の2種類があります。 `EncryptDocumentService` と `EncryptDocumentServiceWse`。 DIMEを使用して `MyApplication/EncryptDocument` プロセスを呼び出すには、 `EncryptDocumentServiceWse` 型を使用します。

>[!NOTE]
>
>FormsサービスへのWeb参照を作成する前に、プロジェクトでWeb Services Enhancements 2.0が参照されていることを確認してください。 （「Web Services Enhancements 2.0のインストール」を参照）。

**WSEライブラリの参照**

1. プロジェクトメニューで、「参照」追加を選択します。
1. [追加参照]ダイアログボックスで、[Microsoft.Web.Services2.dll]を選択します。
1. System.Web.Services.dllを選択します。
1. 「選択」をクリックし、「OK」をクリックします。

**FormsサービスへのWeb参照の作成**

1. プロジェクトメニューで、「追加Web参照」を選択します。
1. URLダイアログボックスで、FormsサービスのURLを指定します。
1. 「Go」をクリックし、「追加Reference」をクリックします。

>[!NOTE]
>
>.NETプロジェクトでWSEライブラリを使用できるようにしていることを確認します。 Project Explorerで、プロジェクト名を右クリックし、「WSE 2.0を有効にする」を選択します。表示されるダイアログボックスのチェックボックスが選択されていることを確認します。

**.NETプロジェクトでDIMEを使用してサービスを呼び出す**

DIMEを使用してFormsサービスを呼び出すことができます。 保護されていないPDFドキュメントを受け取り、パスワードで暗号化されたPDFドキュメントを返す `MyApplication/EncryptDocument` プロセスについて検討します。 DIMEを使用して `MyApplication/EncryptDocument` プロセスを呼び出すには、次の手順を実行します。

1. DIMEを使用してFormsサービスを呼び出せるMicrosoft .NETプロジェクトを作成します。 Web Services Enhancements 2.0が含まれていることを確認し、AEM FormsサービスへのWeb参照を作成します。
1. プロセスにWeb参照を設定した後、デフォルトのコンストラクターを使用して `MyApplication/EncryptDocument``EncryptDocumentServiceWse` オブジェクトを作成します。
1. オブジェクトの `EncryptDocumentServiceWse` データメンバーに、AEM formsのユーザー名とパスワードの値を指定する `Credentials``System.Net.NetworkCredential` 値を設定します。
1. Create a `Microsoft.Web.Services2.Dime.DimeAttachment` object by using its constructor and passing the following values:

   * GUID値を指定するstring値。 メソッドを呼び出して、GUID値を取得でき `System.Guid.NewGuid.ToString` ます。
   * コンテンツタイプを指定するstring値。 このプロセスにはPDFドキュメントが必要なので、を指定し `application/pdf`ます。
   * 定義済みリスト `TypeFormat` 値。 Specify `TypeFormat.MediaType`.
   * AEM Formsプロセスに渡すPDFドキュメントの場所を指定するstring値。

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. オ追加ブジェクトのデータメンバーにオブジェクトの `BLOB` データメンバー値を割り当てることで、 `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトにDIME添付ファイルを指定します。 `Id` オブジェクトの `BLOB``attachmentID` データメンバーには、DIMEデータを割り当てます。
1. メソッドを呼び出し `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` て、 `Microsoft.Web.Services2.Dime.DimeAttachment` オブジェクトを渡します。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出し、DIME添付ファイルを含む `EncryptDocumentServiceWse``invoke``BLOB` オブジェクトを渡して、プロセスを呼び出します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. 返される `BLOB` オブジェクトの `attachmentID` データメンバーの値を取得して、添付ファイル識別子の値を取得します。
1. にある添付ファイルを繰り返し処理 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` し、添付ファイル識別子の値を使用して暗号化されたPDFドキュメントを取得します。
1. オブジェクトの `System.IO.Stream` データメンバの値を取得して、 `Attachment` オブジェクトを取得し `Stream` ます。
1. バイト配列を作成し、そのバイト配列を `System.IO.Stream` オブジェクトの `Read` メソッドに渡します。 このメソッドは、暗号化されたPDFドキュメントを表すデータストリームをバイト配列に入力します。
1. コンストラクターを呼び出し、PDFファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

### DIMEを使用するApache Axis Javaプロキシクラスの作成 {#creating-apache-axis-java-proxy-classes-that-use-dime}

Apache Axis WSDL2Javaツールを使用して、サービスWSDLをJavaプロキシクラスに変換し、サービス操作を呼び出すことができます。 Apache Antを使用すると、AEM FormsサービスWSDLからAxisライブラリファイルを生成して、サービスを呼び出すことができます。 (「Apache Axisを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。

Apache Axis WSDL2Javaツールは、SOAP要求をサービスに送信するために使用されるメソッドを含むJAVAファイルを生成します。 サービスが受信したSOAP要求は、軸生成ライブラリによってデコードされ、メソッドと引数に戻されます。

Axisで生成されたライブラリファイルとDIMEを使用して（Workbenchで構築された） `MyApplication/EncryptDocument` サービスを呼び出すには、次の手順を実行します。

1. Apache Axisを使用して、 `MyApplication/EncryptDocument` サービスWSDLを使用するJavaプロキシクラスを作成します。 (「Apache Axisを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。
1. クラスパスにJavaプロキシクラスを含めます。
1. コンストラクタを使用して `MyApplicationEncryptDocumentServiceLocator` オブジェクトを作成します。
1. コンストラクタを使用し、AEM FormsサービスのWSDL定義を指定する文字列値を渡して、 `URL` オブジェクトを作成します。 SOAPエンドポイントURL `?blob=dime` の末尾に必ず指定してください。 例えば、

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. コンストラクターを呼び出し、 `EncryptDocumentSoapBindingStub` オブジェクトとオブジ `MyApplicationEncryptDocumentServiceLocator`ェクトを渡して、オブジ `URL` ェクトを作成します。
1. オブジェクトおよびメソッドを呼び出して、AEM formsのユーザー名とパスワ `EncryptDocumentSoapBindingStub` ードの値を設定し `setUsername``setPassword` ます。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. オブジェクトを作成して、 `MyApplication/EncryptDocument` サービスに送信するPDFドキュメントを取得し `java.io.File` ます。 PDFドキュメントーの場所を指定するstring値を渡します。
1. Create a `javax.activation.DataHandler` object by using its constructor and passing a `javax.activation.FileDataSource` object. この `javax.activation.FileDataSource` オブジェクトは、コンストラクターを使用し、PDFドキュメントを表す `java.io.File` オブジェクトを渡すことで作成できます。
1. Create an `org.apache.axis.attachments.AttachmentPart` object by using its constructor and passing the `javax.activation.DataHandler` object.
1. オブジェクトの `EncryptDocumentSoapBindingStub` メソッドを呼び出し、オブジェクトを渡して、添付ファイルを添付し `addAttachment``org.apache.axis.attachments.AttachmentPart` ます。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。オブジェクトの `BLOB` メソッドを呼び出し、添付ファイル識別子の値を渡すことで、 `BLOB` オブジェクトに添付ファイル識別子の `setAttachmentID` 値を入力します。 この値は、 `org.apache.axis.attachments.AttachmentPart` オブジェクトの `getContentId` メソッドを呼び出して取得できます。
1. オブジェクトの `MyApplication/EncryptDocument` メソッドを呼び出して、 `EncryptDocumentSoapBindingStub` プロセスを呼び出し `invoke` ます。 DIME添付ファイルを含む `BLOB` オブジェクトを渡します。 このプロセスは、暗号化されたPDFドキュメントを `BLOB` オブジェクト内で返します。
1. 返された `BLOB` オブジェクトのメソッドを呼び出して、添付ファイル識別子の値を取得し `getAttachmentID` ます。 このメソッドは、返される添付ファイルの識別子の値を表すstring値を返します。
1. オブジェクトのメソッドを呼び出して、添付 `EncryptDocumentSoapBindingStub` ファイルを取得し `getAttachments` ます。 このメソッドは、添付ファイルを表す配列 `Objects` を返します。
1. 添付ファイル( `Object` 配列)を繰り返し処理し、添付ファイル識別子の値を使用して暗号化されたPDFドキュメントを取得します。 各要素は1つの `org.apache.axis.attachments.AttachmentPart` オブジェクトです。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び出して、添付ファイルに関連付けられた `org.apache.axis.attachments.AttachmentPart` オブジェクトを取得し `getDataHandler` ます。
1. オブジェクトの `java.io.FileStream` メソッドを呼び出して、 `javax.activation.DataHandler` オブジェクトを取得し `getInputStream` ます。
1. バイト配列を作成し、そのバイト配列を `java.io.FileStream` オブジェクトの `read` メソッドに渡します。 このメソッドは、暗号化されたPDFドキュメントを表すデータストリームをバイト配列に入力します。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. オブジェクトの `java.io.FileOutputStream``write` メソッドを呼び出し、暗号化されたPDFドキュメントを表すデータストリームを含むバイト配列を渡します。

**関連トピック**

[クイック開始: JavaプロジェクトでのDIMEを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAMLベースの認証の使用 {#using-saml-based-authentication}

AEM Formsは、サービスを呼び出すときに、様々なWebサービス認証モードをサポートします。 1つの認証モードでは、Webサービス呼び出しの基本的な認証ヘッダーを使用してユーザー名とパスワードの値の両方を指定します。 AEM Formsは、SAMLアサーションベースの認証もサポートします。 クライアントアプリケーションがWebサービスを使用してAEM Formsサービスを呼び出す場合、クライアントアプリケーションは次のいずれかの方法で認証情報を提供できます。

* 基本認証の一部として資格情報を渡す
* WS-Securityヘッダーの一部としてユーザー名トークンを渡す
* WS-Securityヘッダーの一部としてSAMLアサーションを渡す
* WS-Securityヘッダーの一部としてKerberosトークンを渡す

AEM Formsは、標準の証明書ベースの認証をサポートしていませんが、別の形式の証明書ベースの認証をサポートしています。

>[!NOTE]
>
>「AEM Forms付きプログラミング」のWebサービスクイック開始では、認証を実行するためのユーザー名とパスワードの値を指定します。

AEM FormsユーザーのIDは、秘密キーを使用して署名されたSAMLアサーションを通じて表すことができます。 次のXMLコードは、SAMLアサーションの例を示しています。

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

この例のアサーションは、管理者ユーザーに対して発行されます。 このアサーションには、次の顕著な項目が含まれています。

* 一定の期間有効です。
* 特定のユーザーに対して発行されます。
* デジタル署名されています。 そのため、変更を加えると署名が破損します。
* ユーザー名とパスワードに類似したユーザーのIDのトークンとして、AEM Formsに表示できます。

クライアントアプリケーションは、オブジェクトを返すAEM FormsAuthenticationManager APIからアサーションを取得でき `AuthResult` ます。 次の2つの方法のいずれかを実行して、 `AuthResult` インスタンスを取得できます。

* AuthenticationManager APIによって公開されている任意の認証方法を使用したユーザーの認証。 通常、ユーザー名とパスワードを使用します。 ただし、証明書認証を使用することもできます。
* メソッドを使用し `AuthenticationManager.getAuthResultOnBehalfOfUser` ます。 このメソッドを使用すると、クライアントアプリケーションは任意のAEM formsユーザーの `AuthResult` オブジェクトを取得できます。

aem formsユーザーは、取得したSAMLトークンを使用して認証できます。 このSAMLアサーション（xmlフラグメント）は、WS-Securityヘッダーの一部として、ユーザー認証用のWebサービス呼び出しと共に送信できます。 通常、クライアントアプリケーションはユーザーを認証していますが、ユーザー資格情報を保存していません。 （または、ユーザーがユーザー名とパスワード以外のメカニズムを使用してそのクライアントにログオンした。） この場合、クライアントアプリケーションは、AEM Formsを呼び出し、AEM Formsの呼び出しを許可される特定のユーザーを装う必要があります。

特定のユーザーを装うには、Webサービスを使用して `AuthenticationManager.getAuthResultOnBehalfOfUser` メソッドを呼び出します。 このメソッドは、そのユーザーのSAMLアサーションを含む `AuthResult` インスタンスを返します。

次に、SAMLアサーションを使用して、認証が必要なすべてのサービスを呼び出します。 この操作では、SOAPヘッダーの一部としてアサーションを送信します。 このアサーションを使用してWebサービスが呼び出されると、AEM Formsはユーザーをそのアサーションが表すユーザーとして識別します。 つまり、アサーションで指定されるユーザーは、サービスを呼び出すユーザーです。

### Apache AxisクラスとSAMLベースの認証の使用 {#using-apache-axis-classes-and-saml-based-authentication}

Axisライブラリを使用して作成されたJavaAEM Formsクラスでプロキシサービスを呼び出すことができます。 (「Apache Axisを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。

SAMLベースの認証を使用するAXISを使用する場合は、リクエストおよび応答ハンドラーをAxisに登録します。 Apache Axisは、呼び出し要求をAEM Formsに送信する前にハンドラーを呼び出します。 ハンドラーを登録するには、拡張するJavaクラスを作成し `org.apache.axis.handlers.BasicHandler`ます。

**Axisを使用したAssertionHandlerの作成**

次のJavaクラス（という名前） `AssertionHandler.java`は、拡張するJavaクラスの例を示してい `org.apache.axis.handlers.BasicHandler`ます。

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

**ハンドラーの登録**

ハンドラーをAxisに登録するには、client-config.wsddファイルを作成します。 デフォルトでは、Axisはこの名前を持つファイルを探します。 次のXMLコードは、client-config.wsddファイルの例です。 詳しくは、Axisのドキュメントを参照してください。

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

**AEM Formsサービスの呼び出し**

次のコードの例は、SAMLベースの認証を使用してAEM Formsサービスを呼び出します。

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

### .NETクライアントアセンブリとSAMLベースの認証の使用 {#using-a-net-client-assembly-and-saml-based-authentication}

.NETクライアントアセンブリとSAMLベースの認証を使用して、Formsサービスを呼び出すことができます。 そのためには、Web Service Enhancements 3.0(WSE)を使用する必要があります。 WSEを使用する.NETクライアントアセンブリの作成については、「DIMEを使用する.NETプロジェクトの [作成](#creating-a-net-project-that-uses-dime)」を参照してください。

>[!NOTE]
>
>DIMEセクションではWSE 2.0を使用します。SAMLベースの認証を使用するには、DIMEトピックで指定されている手順と同じ手順に従います。 ただし、WSE 2.0をWSE 3.0に置き換えてください。Web Services Enhancements 3.0を開発用コンピューターにインストールし、Microsoft Visual Studio .NETに統合してください。 Web Services Enhancements 3.0は、 [Microsoftダウンロードセンターからダウンロードできます](https://www.microsoft.com/downloads/search.aspx)。

WSEアーキテクチャでは、ポリシー、アサーション、SecurityTokenの各データ型が使用されます。 簡単に言うと、Webサービスの呼び出しの場合は、ポリシーを指定します。 ポリシーには複数のアサーションを含めることができます。 各アサーションにはフィルターを含めることができます。 Webサービス呼び出しの特定のステージでフィルターが呼び出され、その時点でSOAP要求を変更できます。 詳しくは、Web Service Enhancements 3.0のドキュメントを参照してください。

**アサーションとフィルターの作成**

次のC#コードの例は、フィルタークラスとアサーションクラスを作成します。 次のコードの例は、SamlAssertionOutputFilterを作成します。 このフィルターは、SOAP要求がAEM Formsに送信される前に、WSEフレームワークによって呼び出されます。

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

**SAMLトークンの作成**

SAMLアサーションを表すクラスを作成します。 このクラスが実行する主なタスクは、データ値を文字列からxmlに変換し、空白を保持することです。 このアサーションxmlは、後でSOAP要求に読み込まれます。

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

**AEM Formsサービスの呼び出し**

次のC#コードの例は、SAMLベースの認証を使用してFormsサービスを呼び出します。

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

## Webサービスを使用する場合の関連する考慮事項 {#related-considerations-when-using-web-services}

Webサービスを使用して特定のAEM Formsサービス操作を呼び出すと、問題が発生する場合があります。 この説明の目的は、これらの問題を特定し、解決策がある場合はそれを提供することです。

### サービス操作を非同期で呼び出す {#invoking-service-operations-asynchronously}

Generate PDFの操作など、AEM Formsサービスの操作を非同期で呼び出そうとすると、 `htmlToPDF` エラーが発生 `SoapFaultException` します。 この問題を解決するには、要素と他の要素を異なるクラスにマップするカスタムバインディングXMLファイルを作成し `ExportPDF_Result` ます。 次のXMLは、カスタム連結ファイルを表しています。

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

JAX-WSを使用してJavaプロキシファイルを作成する場合は、このXMLファイルを使用します。 (「JAX-WSを使用したJavaプロキシクラスの [作成](#creating-java-proxy-classes-using-jax-ws)」を参照)。

JAX-WSツール(wsimport.exe)を実行する際に、- `b` コマンドラインオプションを使用してこのXMLファイルを参照します。 AEM FormsのURLを指定するために、連結XMLファイルの `wsdlLocation` 要素を更新します。

非同期呼び出しを確実に動作させるには、エンドポイントURL値を変更し、を指定し `async=true`ます。 例えば、JAX-WSで作成されるJavaプロキシファイルの場合は、に次のように指定し `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`ます。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

次のリストは、非同期に呼び出された場合にカスタム連結ファイルを必要とする他のサービスを指定します。

* PDFG 3D
* タスクマネージャ
* Application Manager
* ディレクトリマネージャ
* Distiller
* Rights Management
* Document Management

### J2EEアプリケーションサーバーの違い {#differences-in-j2ee-application-servers}

特定のJ2EEアプリケーションサーバーを使用して作成されたプロキシライブラリが、別のJ2EEアプリケーションサーバーでホストされているAEM Formsを正常に呼び出さない場合があります。 WebSphereにデプロイされているAEM Formsを使用して生成されるプロキシライブラリを考えてみましょう。 このプロキシライブラリは、JBoss Application ServerにデプロイされたAEM Formsサービスを正常に呼び出すことができません。

一部のAEM Formsでは、複雑なデータ型が使用されます。例えば、AEM FormsをWebSphereにデプロイする場合 `PrincipalReference`は、JBoss Application Serverとは異なる定義が行われます。 異なるJ2EEアプリケーションサービスで使用されるJDKの違いが、WSDL定義に違いがある理由です。 その結果、同じJ2EEアプリケーションサーバーから生成されたプロキシライブラリを使用します。

### Webサービスを使用した複数のサービスへのアクセス {#accessing-multiple-services-using-web-services}

名前空間の競合が原因で、複数のサービスWSDL間でデータオブジェクトを共有できません。 データ型を共有できるサービスは異なるので、サービスはWSDLでこれらの型の定義を共有します。 例えば、 `BLOB` データ型を含む2つの.NETクライアントアセンブリを同じ.NETクライアントプロジェクトに追加することはできません。 これを行うと、コンパイルエラーが発生します。

次のリストは、複数のサービスWSDL間で共有できないデータ型を指定します。

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

この問題を回避するには、データタイプを完全に限定することをお勧めします。 例えば、サービス参照を使用してFormsサービスとSignatureサービスの両方を参照する.NETアプリケーションを考えてみましょう。 両方のサービス参照には、1つの `BLOB` クラスが含まれます。 インスタンスを使用するには、 `BLOB` オブジェクトを宣言するときに `BLOB` オブジェクトを完全修飾します。 この方法は、次のコード例に示します。 このコード例について詳しくは、「インタラクティブフォームへの [デジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)」を参照してください。

次のC#コードの例は、Formsサービスによってレンダリングされるインタラクティブフォームに署名します。 クライアントアプリケーションには2つのサービス参照があります。 Formsサービスに関連付けられている `BLOB` インスタンスは、 `SignInteractiveForm.ServiceReference2` 名前空間に属しています。 同様に、Signatureサービスに関連付けられている `BLOB` インスタンスは、 `SignInteractiveForm.ServiceReference1` 名前空間に属しています。 署名済みのインタラクティブフォームは、LoanXFASigned.pdfというPDFファイル *として保存されます*。

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

### 無効なプロキシファイルを生成するレターで始まるサービス {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Microsoft .Net 3.5およびWCFを使用する場合に、生成された一部のAEM Formsのプロキシクラス名が正しくありません。 この問題は、IBMFilenetContentRepositoryConnector、IDPSchedulerService、または名前が文字Iで開始する他のサービス用にプロキシクラスが作成された場合に発生します。例えば、IBMFileNetContentRepositoryConnectorの場合は、生成されたクライアントの名前で `BMFileNetContentRepositoryConnectorClient`す。 生成されたプロキシクラスにレターIがありません。

