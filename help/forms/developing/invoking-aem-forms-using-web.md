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
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# Web サービスを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-web-services}

サービスコンテナ内のほとんどのAEM Formsサービスは、Webサービスを公開するように設定され、Webサービス定義言語(WSDL)の生成を完全にサポートします。 つまり、AEM FormsサービスのネイティブSOAPスタックを使用するプロキシオブジェクトを作成できます。 その結果、AEM Formsサービスは次のSOAPメッセージを交換し、処理できます。

* **SOAPリクエスト**:アクションを要求するクライアントアプリケーションによってFormsサービスに送信されます。
* **SOAP応答**:SOAP要求の処理後、Formsサービスによってクライアントアプリケーションに送信されます。

Webサービスを使用する場合は、Java APIを使用する場合と同じAEM Formsサービス操作を実行できます。 Webサービスを使用してAEM Formsサービスを呼び出す利点の1つは、SOAPをサポートする開発環境でクライアントアプリケーションを作成できることです。 クライアントアプリケーションは、特定の開発言語やプログラミング環境に結び付けられません。 例えば、Microsoft Visual Studio .NETおよびC#をプログラミング言語として使用するクライアントアプリケーションを作成できます。

AEM FormsサービスはSOAPプロトコルを使用して公開され、WSI Basicプロファイル1.1に準拠しています。 Web Services Interoperability(WSI)は、複数のプラットフォーム間でのWebサービスの相互運用性を促進するオープンスタンダード組織です。 詳しくは、https://www.ws-i.org/を参照して [ください](https://www.ws-i.org)。

AEM Formsは、次のWebサービス標準をサポートしています。

* **Encoding**:ドキュメントおよびリテラルエンコーディングのみをサポートします(WSIの基本プロファイルに従う推奨エンコーディング)。 (「Base64エンコ [ーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)」を参照)。
* **MTOM**:SOAP要求で添付ファイルをエンコードする方法を表します。 (「MTOMを使用 [したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom)」を参照)。
* **SwaRef**:SOAP要求で添付ファイルをエンコードする別の方法を表します。 (「SwaRefを使 [用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)」を参照)。
* **添付ファイル付きSOAP**:MIMEとDIME(Direct Internet Message Encapsulation)の両方をサポートします。 これらのプロトコルは、SOAP経由で添付ファイルを送信する標準的な方法です。 Microsoft Visual Studio .NETアプリケーションはDIMEを使用します。 (「Base64エンコ [ーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)」を参照)。
* **WS-Security**:ユーザー名パスワードトークンプロファイルをサポートします。これは、WSセキュリティSOAPヘッダーの一部としてユーザー名とパスワードを送信する標準的な方法です。 AEM Formsは、HTTP基本認証もサポートします。 (WS-Securityヘ [ッダーを使用した秘密鍵証明書の引き渡しを参照](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html))。

Webサービスを使用してAEM Formsサービスを呼び出すには、通常、サービスWSDLを使用するプロキシライブラリを作成します。 「Webサ *ービスを使用したAEM Formsの呼び出し* 」セクションでは、JAX-WSを使用して、サービスを呼び出すJavaプロキシクラスを作成します。 (JAX-WSを使 [用したJavaプロキシクラスの作成を参照](#creating-java-proxy-classes-using-jax-ws))。

次のURL定義を指定すると、サービスWDSLを取得できます（角括弧で囲まれた項目はオプションです）。

```as3
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

各パラメーターの意味は次のとおりです。

* *your_serverhostは* 、AEM FormsをホストするJ2EEアプリケーションサーバーのIPアドレスを表します。
* *your_portは* 、J2EEアプリケーションサーバーが使用するHTTPポートを表します。
* *service_nameは* 、サービス名を表します。
* *versionは* 、サービスのターゲットバージョンを表します（デフォルトでは、最新のサービスバージョンが使用されます）。
* `async` 非同期呼び出し `true` の追加操作を有効にする値を指定します(デフォ `false` ルト)。
* *lc_versionは* 、呼び出すAEM Formsのバージョンを表します。

次の表のリストは、WSDL定義をサービスします（AEM Formsがローカルホストにデプロイされ、投稿が8080である場合）。

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
   <td><p>Forms</p></td>
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

**AEM Forms Process WSDLの定義**

Workbenchで作成されたプロセスに属するWSDLにアクセスするには、WSDL定義内でアプリケーション名とプロセス名を指定する必要があります。 アプリケーションの名前がで、プロ `MyApplication` セスの名前がであるとします `EncryptDocument`。 この場合、次のWSDL定義を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>短時間のみ有効なプロセスの例につ `MyApplication/EncryptDocument` いて詳しくは、短時間のみ有効なプロ [セスの例を参照してくださ](/help/forms/developing/aem-forms-processes.md)い。

>[!NOTE]
>
>アプリケーションにはフォルダーを含めることができます。 この場合、WSDL定義でフォルダー名を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Webサービスを使用した新機能へのアクセス**

AEM Formsの新しいサービス機能は、Webサービスを使用してアクセスできます。 例えば、AEM Formsでは、MTOMを使用して添付ファイルをエンコードする機能が導入されました。 (「MTOMを使用 [したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom)」を参照)。

AEM Formsで導入された新しい機能にアクセスするには、WSDL定義で `lc_version` 属性を指定します。 例えば、新しいサービス機能（MTOMのサポートを含む）にアクセスするには、次のWSDL定義を指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>属性を設定する際 `lc_version` は、必ず3桁の数字を使用してください。 例えば、9.0.1はバージョン9.0と等しくなります。

**WebサービスBLOBデータ型**

AEM FormsサービスのWSDLでは、多くのデータ型が定義されています。 Webサービスで公開される最も重要なデータ型の1つは、型 `BLOB` です。 AEM Forms Java APIを使用する場合、このデ `com.adobe.idp.Document` ータ型はクラスにマッピングされます。 (See [Passing data to AEM Forms services using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

オブジ `BLOB` ェクトは、AEM Formsサービスとの間でバイナリデータ（PDFファイル、XMLデータなど）を送受信します。 この型 `BLOB` は、サービスWSDLで次のように定義されます。

```as3
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

およびフ `MTOM` ィール `swaRef` ドはAEM Formsでのみサポートされます。 これらの新しいフィールドは、プロパティを含むURLを指定した場合にのみ使用で `lc_version` きます。

**サービス要求へのBLOBオブジェクトの指定**

AEM Formsサービスの操作で入力値として型が `BLOB` 必要な場合は、アプリケーションロジックでその型のイ `BLOB` ンスタンスを作成します。 (「AEM formsによるプログラミング」にあるWebサービスのク *イック開始の多くは* 、BLOBデータ型の使用方法を示しています)。

次の手順で、インスタンスに属するフィールドに値 `BLOB` を割り当てます。

* **Base64**:Base64形式でエンコードされたテキストとしてデータを渡すには、フィールドにデータを設定し、フ `BLOB.binaryData` ィールドにデータタイプをMIME形式(例えば、 `application/pdf`)で設定し `BLOB.contentType` ます。 (「Base64エンコ [ーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)」を参照)。
* **MTOM**:MTOM添付ファイルにバイナリデータを渡すには、フィールドにデータを設定 `BLOB.MTOM` します。 この設定は、Java JAX-WSフレームワークまたはSOAPフレームワークのネイティブAPIを使用して、SOAP要求にデータを添付します。 (「MTOMを使用 [したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom)」を参照)。
* **SwaRef**:WS-I SwaRef添付ファイルにバイナリデータを渡すには、フィールドにデータを設定し `BLOB.swaRef` ます。 この設定は、Java JAX-WSフレームワークを使用してSOAP要求にデータを添付します。 (「SwaRefを使 [用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)」を参照)。
* **MIMEまたはDIME添付ファイル**:MIMEまたはDIME添付ファイルにデータを渡すには、SOAPフレームワークのネイティブAPIを使用してSOAP要求にデータを添付します。 フィールドに添付ファイル識別子を設定 `BLOB.attachmentID` します。 (「Base64エンコ [ーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)」を参照)。
* **リモートURL**:データがWebサーバー上でホストされ、HTTP URL経由でアクセス可能な場合は、フィールドにHTTP URLを設定し `BLOB.remoteURL` ます。 (「HTTP経由 [のBLOBデータを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)」を参照)。

**サービスから返されたBLOBオブジェクト内のデータへのアクセス**

返されるオブジェクトの送信 `BLOB` プロトコルは、いくつかの要因に依存します。これらの要因は、次の順序で考慮され、メイン条件が満たされると停止します。

1. **ターゲットURLは送信プロトコルを指定します**。 SOAP呼び出しで指定されたターゲットURLに `blob="`*BLOB_TYPE *&quot;というパラメータが含まれている場合、**BLOB_TYPEは送信プロトコルを決定します。* BLOB_TYPEは&#x200B;*、base64、dime、mime、http、mtomまたはswarefのプレースホルダです。
1. **サービスSOAPエンドポイントはスマートです**。 次の条件が真の場合、出力ドキュメントは入力プロトコルと同じ送信プロトコルを使用して返されます。ドキュメント

   * サービスのSOAPエンドポイントパラメーター「Default Protocol For Output Blob Objects」が「Smart」に設定されている。

      SOAPエンドポイントを持つ各サービスに対して、管理コンソールでは、返されたBLOBの送信プロトコルを指定できます。 (See [administration help](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Formsサービスは、1つ以上のドキュメントを入力として受け取ります。

1. **サービスSOAPエンドポイントがスマートではありません**。 設定されたプロトコルはドキュメント送信プロトコルを決定し、対応するフィールドにデータを返 `BLOB` します。 例えば、SOAPエンドポイントがDIMEに設定されている場合、返されるBLOBは、入力ドキュメントの送信プロトコルに関係な `blob.attachmentID` く、フィールドに含まれます。
1. **それ以外**。 サービスがドキュメントタイプを入力として受け取らない場合、出力ドキュメントはHTTPプロトコル経由のフィー `BLOB.remoteURL` ルドに返されます。

最初の条件で説明したように、次のようにサフィックスを付けてSOAPエンドポイントURLを拡張することで、返されるドキュメントの送信タイプを確認できます。

```as3
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

次に、送信タイプとデータの取得元のフィールドの相関関係を示します。

* **Base64形式**:フィールドに `blob` データを返す `base64` には、サフィックスをに設定 `BLOB.binaryData` します。
* **MIMEまたはDIME添付ファイル**:サフィックスを `blob` に設定 `DIME` するか、 `MIME` フィールドに返される添付ファイル識別子を持つ、対応する添付ファイルの種類としてデータを返 `BLOB.attachmentID` します。 SOAPフレームワーク固有のAPIを使用して、添付ファイルからデータを読み取ります。
* **リモートURL**:サフィックスを `blob` に設定し `http` て、アプリケーションサーバー上のデータを保持し、フィールド内のデータを指すURLを返 `BLOB.remoteURL` します。
* **MTOMまたはSwaRef**:サフィックスを `blob` に設定 `mtom` するか、ま `swaref` たはフィールドで返される添付ファイル識別子を持つ、対応する添付ファイルの種類としてデータを返 `BLOB.MTOM` すように `BLOB.swaRef` します。 SOAPフレームワークのネイティブAPIを使用して、添付ファイルからデータを読み取ります。

>[!NOTE]
>
>メソッドを呼び出してオブジェクトを入力する場合は、30 MBを超えないよ `BLOB` うにすることをお勧め `setBinaryData` します。 そうしないと、例外が発生する可能性が `OutOfMemory` あります。

>[!NOTE]
>
>MTOM送信プロトコルを使用するJAX WSベースのアプリケーションでは、送受信データの量が25 MBに制限されます。 この制限は、JAX-WSのバグが原因です。 送受信したファイルの合計サイズが25 MBを超える場合は、MTOM送信プロトコルの代わりにSwaRef送信プロトコルを使用します。 そうでないと、例外が発生する可能性があ `OutOfMemory` ります。

**base64エンコードされたバイト配列のMTOM送信**

MTOMプロトコルは、オブジ `BLOB` ェクトに加えて、複合型のバイト配列パラメータまたはバイト配列フィールドもサポートします。 つまり、MTOMをサポートするクライアントSOAPフレームワークは、(base64でエンコードさ `xsd:base64Binary` れたテキストの代わりに)任意の要素をMTOM添付ファイルとして送信できます。 AEM Forms SOAPエンドポイントは、このタイプのバイト配列エンコーディングを読み取ることができます。 ただし、AEM Formsサービスは、常にbase64エンコードされたテキストとしてバイト配列型を返します。 出力バイト配列パラメーターはMTOMをサポートしていません。

大量のバイナリデータを返すAEM Formsサービスでは、バイト配列型ではなく、ドキュメント/BLOB型が使用されます。 ドキュメントタイプは、大量のデータを送信する場合に、はるかに効率的です。

## Webサービスのデータ型 {#web-service-data-types}

次の表に、Javaリストのデータ型を示し、対応するWebサービスのデータ型を示します。

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
   <td><p>サー <code>DATE</code> ビスWSDLで次のように定義される型。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作で値を入力と <code>java.util.Date</code> して受け取る場合、SOAPクライアントアプリケーションはフィールドに日付を渡す必要があ <code>DATE.date</code> ります。 この場合、フ <code>DATE.calendar</code> ィールドを設定すると、実行時例外が発生します。 サービスが値を返す場 <code>java.util.Date</code>合は、フィールドに日付が返さ <code>DATE.date</code> れます。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>サー <code>DATE</code> ビスWSDLで次のように定義される型。</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作で値を入力と <code>java.util.Calendar</code> して受け取る場合、SOAPクライアントアプリケーションはフィールドに日付を渡す必要があ <code>DATE.caledendar</code> ります。 この場合、フ <code>DATE.date</code> ィールドを設定すると、実行時例外が発生します。 サービスが値を返す <code>java.util.Calendar</code>場合は、フィールドに日付が返され <code>DATE.calendar</code> ます。 </p></td>
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
   <td><p>サー <code>apachesoap:Map</code>ビスWSDLで次のように定義される。</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>マップは、キーと値のペアのシーケンスとして表されます。</p></td>
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
   <td><p>XML型。サービスWSDLで次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が値を受け入れ <code>org.w3c.dom.Document</code> る場合は、XMLデータをフィールドに渡 <code>XML.document</code> します。</p><p>このフィールドを設 <code>XML.element</code> 定すると、ランタイム例外が発生します。 サービスがXMLを返す <code>org.w3c.dom.Document</code>場合、XMLデータがフィールドに返さ <code>XML.document</code> れます。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML型。サービスWSDLで次のように定義されます。</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Formsサービスの操作が入力として受け取る <code>org.w3c.dom.Element</code> 場合は、XMLデータをフィールドに渡 <code>XML.element</code> します。</p><p>このフィールドを設 <code>XML.document</code> 定すると、ランタイム例外が発生します。 サービスがXMLデータを返 <code>org.w3c.dom.Element</code>す場合、XMLデータがフィールドに返さ <code>XML.element</code> れます。</p></td>
  </tr>
 </tbody>
</table>

**Adobe Developer Web サイト**

Adobe Developer Webサイトには、WebサービスAPIを使用したAEM Formsサービスの呼び出しについて説明する次の記事が含まれています。

[フォームレンダリングASP.NETアプリケーションの作成](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[カスタムコンポーネントを使用したWebサービスの呼び出し](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>カスタムコンポーネントを使用したWebサービスの呼び出しでは、サードパーティのWebサービスを呼び出すAEM Formsコンポーネントの作成方法を説明します。

## JAX-WSを使用したJavaプロキシクラスの作成 {#creating-java-proxy-classes-using-jax-ws}

JAX-WSを使用して、FormsサービスのWSDLをJavaプロキシクラスに変換できます。 AEM Formsサービスの操作を呼び出すことができるクラスです。 Apache Antでは、AEM FormsサービスのWSDLを参照してJavaプロキシクラスを生成するビルドスクリプトを作成できます。 次の手順を実行して、JAX-WSプロキシファイルを生成できます。

1. クライアントコンピューターにApache Antをインストールします。 (https://ant.apache.org/bindownload.cgiを参 [照](https://ant.apache.org/bindownload.cgi))。

   * 追加binディレクトリからクラスパスに移動します。
   * Antをインストール `ANT_HOME` した環境にディレクトリ変数を設定します。

1. JDK 1.6以降をインストールします。

   * ク追加ラスパスのJDK binディレクトリ。
   * JRE 追加 binディレクトリをクラスパスに置きます。 このbinは、ディレクトリ内にあ `[JDK_INSTALL_LOCATION]/jre` ります。
   * JDKをインス `JAVA_HOME` トールしたディレクトリに環境変数を設定します。
   JDK 1.6には、build.xmlファイルで使用するwsimportプログラムが含まれています。 JDK 1.5にはこのプログラムは含まれません。

1. JAX-WSをクライアントコンピューターにインストールします。 ( [Java API for XML Web Servicesを参照](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html))。
1. JAX-WSとApache Antを使用してJavaプロキシクラスを生成します。 この操作を行うAnt構築スクリプトを作成します。タスク 次のスクリプトは、build.xmlという名前のAntビルドスクリプトの例です。

   ```as3
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

   このAnt構築スクリプト内で、localhostで実行され `url` ているEncryptionサービスWSDLを参照するようにプロパティが設定されています。 およびプ `username` ロパテ `password` ィは、有効なAEM formsのユーザー名とパスワードに設定する必要があります。 URLに属性が含まれていることに注意して `lc_version` ください。 このオプションを指 `lc_version` 定しないと、新しいAEM Formsサービス操作を呼び出すことはできません。

   >[!NOTE]
   >
   >Javaプロ `EncryptionService`キシクラスを使用して呼び出すAEM Formsサービス名に置き換えます。 例えば、Rights Managementサービス用のJavaプロキシクラスを作成するには、次のように指定します。

   ```as3
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Ant構築スクリプトを実行するBATファイルを作成します。 次のコマンドは、Ant構築スクリプトを実行するBATファイル内に配置できます。

   ```as3
    ant -buildfile "build.xml" wsdl
   ```

   ANTビルドスクリプトをC:\Program Files\Java\jaxws-ri\bin directoryフォルダーに配置します。 このスクリプトは、にJAVAファイルを書き込みます。/classesフォルダー このスクリプトは、サービスを呼び出すことのできるJAVAファイルを生成します。

1. JAVAファイルをJARファイルにパッケージ化します。 Eclipseを使用する場合は、次の手順に従います。

   * プロキシJAVAファイルをJARファイルにパッケージ化するために使用する新しいJavaプロジェクトを作成します。
   * プロジェクト内にソースフォルダを作成します。
   * Sourceフォルダー `com.adobe.idp.services` でパッケージを作成します。
   * パッケージ `com.adobe.idp.services` を選択し、adobe/idp/servicesフォルダーからパッケージにJAVAファイルを読み込みます。
   * 必要に応じて、Sourceフォルダー `org/apache/xml/xmlsoap` にパッケージを作成します。
   * ソースフォルダーを選択し、org/apache/xml/xmlsoapフォルダーからJAVAファイルを読み込みます。
   * Javaコンパイラの準拠レベルを5.0以上に設定します。
   * プロジェクトを構築します。
   * プロジェクトをJARファイルとしてエクスポートします。
   * このJARファイルをクライアントプロジェクトのクラスパスに読み込みます。 さらに、&lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdpartyにあるすべてのJARファイルをインポートします。
   >[!NOTE]
   >
   >「AEM formsによるプログラミング」にあるすべてのJava Webサービスのクイック開始（Formsサービスを除く）は、JAX-WSを使用してJavaプロキシファイルを作成します。 また、すべてのJava Webサービスのクイック開始では、SwaRefを使用します。 (「SwaRefを使 [用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)」を参照)。

**関連トピック**

[Apache Axisを使用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)

[Base64エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP経由のBLOBデータを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

[SwaRefを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-swaref)

## Apache Axisを使用したJavaプロキシクラスの作成 {#creating-java-proxy-classes-using-apache-axis}

Apache Axis WSDL2Javaツールを使用して、FormsサービスをJavaプロキシクラスに変換できます。 これらのクラスを使用して、Formsサービス操作を呼び出すことができます。 Apache Antを使用して、サービスWSDLからAxisライブラリファイルを生成できます。 Apache AxisはURL https://ws.apache.org/axis/からダウンロードでき [ます](https://ws.apache.org/axis/)。

>[!NOTE]
>
>Formsサービスに関連付けられたWebサービスのクイック開始は、Apache Axisを使用して作成されたJavaプロキシクラスを使用します。 Forms Webサービスのクイック開始では、エンコーディングの種類としてBase64も使用されます。 ( [FormsサービスAPIのクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts))。

次の手順を実行して、Axis Javaライブラリファイルを生成できます。

1. クライアントコンピューターにApache Antをインストールします。 https://ant.apache.org/bindownload.cgiで入手でき [ます](https://ant.apache.org/bindownload.cgi)。

   * 追加binディレクトリからクラスパスに移動します。
   * Antをインストール `ANT_HOME` した環境にディレクトリ変数を設定します。

1. クライアントコンピューターにApache Axis 1.4をインストールします。 https://ws.apache.org/axis/で入手でき [ます](https://ws.apache.org/axis/.md)。
1. WebサービスクライアントでAxis JARファイルを使用するためのクラスパスを設定します。詳しくは、https://ws.apache.org/axis/java/install.htmlのAxisのインストール手順を参照してく [ださい](https://ws.apache.org/axis/java/install.html)。
1. Javaプロキシクラスを生成するには、Apache WSDL2JavaツールをAxisで使用します。 この操作を行うAnt構築スクリプトを作成します。タスク 次のスクリプトは、build.xmlという名前のAntビルドスクリプトの例です。

   ```as3
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

   このAnt構築スクリプト内で、localhostで実行され `url` ているEncryptionサービスWSDLを参照するようにプロパティが設定されています。 およびプ `username` ロパテ `password` ィは、有効なAEM formsのユーザー名とパスワードに設定する必要があります。

1. Ant構築スクリプトを実行するBATファイルを作成します。 次のコマンドは、Ant構築スクリプトを実行するBATファイル内に配置できます。

   ```as3
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVAファイルは、C:\JavaFiles folder as specified by the プロパティに書き込まれます `output` 。 Formsサービスを正常に呼び出すには、これらのJAVAファイルをクラスパスに読み込みます。

   デフォルトでは、これらのファイルはという名前のJavaパッケージに属していま `com.adobe.idp.services`す。 これらのJAVAファイルは、JARファイルに配置することをお勧めします。 次に、JARファイルをクライアントアプリケーションのクラスパスに読み込みます。

   >[!NOTE]
   >
   >.JAVAファイルをJARに配置する方法は異なります。 1つの方法は、EclipseのようなJava IDEを使用することです。 Javaプロジェクトを作成し、パッケージを作 `com.adobe.idp.services`成します（すべての.JAVAファイルがこのパッケージに属します）。 次に、すべての.JAVAファイルをパッケージに読み込みます。 最後に、プロジェクトをJARファイルとして書き出します。

1. クラス内のURLを修正して、エ `EncryptionServiceLocator` ンコーディングタイプを指定します。 例えば、base64を使用する場合は、オブジェクトがバ `?blob=base64` イナリデータを確実に返すよ `BLOB` うに指定する必要があります。 つまり、クラス内で、 `EncryptionServiceLocator` 次のコード行を探します。

   ```as3
    http://localhost:8080/soap/services/EncryptionService;
   ```

   次のように変更します。

   ```as3
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 次の追加Axis JARファイルをJavaプロジェクトのクラスパスに追加します。

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
   これらのJARファイルは、ディレクトリにあ `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` ります。

**関連トピック**

[JAX-WSを使用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-jax-ws)

[Base64エンコーディングを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-base64-encoding)

[HTTP経由のBLOBデータを使用したAEM Formsの呼び出し](#invoking-aem-forms-using-blob-data-over-http)

## Base64エンコーディングを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-base64-encoding}

Base64エンコーディングを使用してAEM Formsサービスを呼び出すことができます。 Base64エンコードは、Webサービスの呼び出し要求で送信される添付ファイルをエンコードします。 つまり、データは `BLOB` SOAPメッセージ全体ではなく、Base64でエンコードされます。

「Base64エンコーディングを使用したAEM Formsの呼び出し」では、Base64エンコーディングを使用して名前が付けられた、次のAEM Formsの短時間のみ有効なプロセス `MyApplication/EncryptDocument` を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

### Base64エンコーディングを使用する.NETクライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NETクライアントアセンブリを作成して、Microsoft Visual Studio .NETプロジェクトからFormsサービスを呼び出すことができます。 base64エンコーディングを使用する.NETクライアントアセンブリを作成するには、次の手順を実行します。

1. AEM Formsの呼び出しURLに基づいてプロキシクラスを作成します。
1. .NETクライアントアセンブリを生成するMicrosoft Visual Studio .NETプロジェクトを作成します。

**プロキシクラスの作成**

Microsoft Visual Studioに付属するツールを使用して、.NETクライアントアセンブリの作成に使用するプロキシクラスを作成できます。 ツールの名前はwsdl.exeで、Microsoft Visual Studioのインストールフォルダーにあります。 プロキシクラスを作成するには、コマンドプロンプトを開き、wsdl.exeファイルが格納されているフォルダーに移動します。 wsdl.exeツールの詳細については、 *MSDNヘルプを参照してください*。

コマンドプロンプトで次のコマンドを入力します。

```as3
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

デフォルトでは、このツールは、WSDLの名前に基づいて同じフォルダーにCSファイルを作成します。 この場合、EncryptDocumentService.csという名前のCSファイル *が作成されます*。 このCSファイルを使用して、呼び出しURLで指定されたサービスを呼び出すためのプロキシオブジェクトを作成します。

オブジェクトがバイナリデータを返すように、プロキシ `?blob=base64` クラスのURLを修正し、を含め `BLOB` るようにします。 プロキシクラスで、次のコード行を探します。

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

次のように変更します。

```as3
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

「Base64エ *ンコーディングを使用したAEM Formsの呼び出し* 」セクションでは、例 `MyApplication/EncryptDocument` としてを使用しています。 別のFormsサービス用に.NETクライアントアセンブリを作成する場合は、必ずサービスの名前に置き換 `MyApplication/EncryptDocument` えてください。

**.NETクライアントアセンブリの開発**

.NETクライアントアセンブリを生成するVisual Studioクラスライブラリプロジェクトを作成します。 wsdl.exeを使用して作成したCSファイルを、このプロジェクトに読み込むことができます。 このプロジェクトは、DLLファイル（.NETクライアントアセンブリ）を生成し、他のVisual Studio .NETプロジェクトでサービスを呼び出すために使用できます。

1. 開始Microsoft Visual Studio .NET
1. クラスライブラリプロジェクトを作成し、DocumentServiceという名前を付けます。
1. wsdl.exeを使用して作成したCSファイルを読み込みます。
1. [プロジェ **クト** ]メニューの[参照 **]を選**&#x200B;追加択します。
1. [参照追加]ダイアログボックスで、 **System.Web.Services.dllを選択します**。
1. Click **Select** and then click **OK**.
1. プロジェクトをコンパイルしてビルドします。

>[!NOTE]
>
>この手順では、SOAP要求をサービスに送信するために使用できる、DocumentService.dllという.NETクライアントアセンブリを作成 `MyApplication/EncryptDocument` します。

>[!NOTE]
>
>.NETクライアントアセン `?blob=base64` ブリの作成に使用するプロキシクラスのURLに追加したことを確認します。 そうしないと、オブジェクトからバイナリデータを取得でき `BLOB` ません。

**.NETクライアントアセンブリの参照**

新しく作成した.NETクライアントアセンブリを、クライアントアプリケーションを開発するコンピューター上に配置します。 .NETクライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 また、プロジェクトの `System.Web.Services` ライブラリも参照します。 このライブラリを参照しない場合、.NETクライアントアセンブリを使用してサービスを呼び出すことはできません。

1. [プロジェ **クト** ]メニューの[参照 **]を選**&#x200B;追加択します。
1. Click the **.NET** tab.
1. 「 **Browse** 」をクリックし、DocumentService.dllファイルを探します。
1. Click **Select** and then click **OK**.

**Base64エンコーディングを使用する.NETクライアントアセンブリを使用したサービスの呼び出し**

Base64エンコーディングを使 `MyApplication/EncryptDocument` 用する.NETクライアントアセンブリを使用して、（Workbenchに組み込まれていた）サービスを呼び出すことができます。 サービスを呼び出 `MyApplication/EncryptDocument` すには、次の手順を実行します。

1. サービスWSDLを使用するMicrosoft .NETクライアントアセンブリを `MyApplication/EncryptDocument` 作成します。
1. クライアントのMicrosoft .NETプロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NETクライアントアセンブリを参照します。 参照も参照してくだ `System.Web.Services`さい。
1. Microsoft .NETクライアントアセンブリを使用し、デフォルトのコンストラク `MyApplication_EncryptDocumentService` タを呼び出してオブジェクトを作成します。
1. オブジェクト `MyApplication_EncryptDocumentService` のプロパティをオ `Credentials` ブジェクトで設定 `System.Net.NetworkCredential` します。 コンストラクタ `System.Net.NetworkCredential` ー内で、AEM formsのユーザー名と対応するパスワードを指定します。 認証値を設定して、.NETクライアントアプリケーションがAEM FormsとSOAPメッセージを正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、プロセスに渡されるPDFドキュメントの保存に使用さ `MyApplication/EncryptDocument` れます。
1. Create a `System.IO.FileStream` object by invoking its constructor. PDFファイルの場所と、ファイルを開くドキュメントを表すstring値を渡します。
1. オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
1. オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
1. オブジェクトに `BLOB` バイト配列の内容を割り当 `binaryData` てて、オブジェクトにデータを入力します。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出 `MyApplication_EncryptDocumentService` し、PDF `invoke` メソッドを含むオブ `BLOB` ジェクトを渡して、プロセスを呼び出します。ドキュメント このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. コンストラクター `System.IO.FileStream` を呼び出し、パスワードで暗号化されたオブジェクトのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
1. オブジェクトのメソッドによって返されるオブジェクトのデ `BLOB` ータ内容を格納するバ `MyApplicationEncryptDocumentService` イト配列を作成 `invoke` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `binaryData` 定します。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡すこ `System.IO.BinaryWriter` とで、バイト配列 `Write` の内容をPDFファイルに書き込みます。

### JavaプロキシクラスとBase64エンコーディングを使用したサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

JavaプロキシクラスとBase64を使用してAEM Formsサービスを呼び出すことができます。 Javaプロキシクラスを使 `MyApplication/EncryptDocument` 用してサービスを呼び出すには、次の手順を実行します。

1. サービスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを `MyApplication/EncryptDocument` 作成します。 次のWSDLエンドポイントを使用します。

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >AEM Formsをホ `hiro-xp`*ストするJ2EEアプリケーションサービスのIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、オ `MyApplicationEncryptDocumentService` ブジェクトを作成 `getEncryptDocument` します。
1. AEM Formsの呼び出しに必要な接続値を設定するには、次のデータメンバーに値を割り当てます。

   * WSDLのエンドポイントとエンコードの種類をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `ENDPOINT_ADDRESS_PROPERTY` てます。 Base64エンコーディン `MyApplication/EncryptDocument` グを使用してサービスを呼び出すには、次のURL値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM formsユーザーをオブジェクトのフィ `javax.xml.ws.BindingProvider` ールドに割り当 `USERNAME_PROPERTY` てます。
   * 対応するパスワード値をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `PASSWORD_PROPERTY` てます。
   次のコード例は、このアプリケーションロジックを示しています。

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクターを使用してドキュメントを作成 `MyApplication/EncryptDocument` し、プロセスに送信するPDF `java.io.FileInputStream` コンストラクターを取得します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
1. バイト配列を作成し、オブジェクトの内容を設定し `java.io.FileInputStream` ます。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. メソッドを呼び `BLOB` 出し、バイト配列を渡 `setBinaryData` すことで、オブジェクトを入力します。 Base64エン `BLOB` コーディングを使 `setBinaryData` 用する場合、オブジェクトが呼び出すメソッドです。 サービス要求へのBLOBオブジェクトの指定を参照してください。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出し `MyApplicationEncryptDocument` て、プロセスを呼び出 `invoke` します。 PDFを含むオ `BLOB` ブジェクトを渡します。ドキュメント 呼び出しメソッドは、暗号化されたPDF `BLOB` メソッドを含むオブジェクトを返しますドキュメント。
1. オブジェクトのメソッドを呼び出して、暗号化されたPDFドキュメントを含むバイト `BLOB` 配列を作成 `getBinaryData` します。
1. 暗号化されたPDFドキュメントをPDFファイルとして保存します。 バイト配列をファイルに書き込みます。

**関連トピック**

[クイック開始:JavaプロキシファイルとBase64エンコーディングを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOMを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-mtom}

AEM Formsサービスは、Webサービス標準のMTOMを使用して呼び出すことができます。 この標準は、PDFデータなどのバイナリデータをインターネットやドキュメント経由で送信する方法を定義します。 MTOMの特徴は、要素の使用で `XOP:Include` す。 この要素は、SOAPメッセージのバイナリ添付ファイルを参照するために、XML Binary Optimized Packaging(XOP)仕様で定義されています。

The discussion here is about using MTOM to invoke the following AEM Forms short-lived process named `MyApplication/EncryptDocument`.

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>AEM Formsバージョン9でMTOMサポートが追加されました。

>[!NOTE]
>
>MTOM送信プロトコルを使用するJAX WSベースのアプリケーションでは、送受信データの量が25 MBに制限されます。 この制限は、JAX-WSのバグが原因です。 送受信したファイルの合計サイズが25 MBを超える場合は、MTOM送信プロトコルの代わりにSwaRef送信プロトコルを使用します。 そうでないと、例外が発生する可能性があ `OutOfMemory` ります。

ここでは、Microsoft .NETプロジェクト内でMTOMを使用してAEM Formsサービスを呼び出す方法について説明します。 使用される.NETフレームワークは3.5で、開発環境はVisual Studio 2008です。 Web Service Enhancements(WSE)が開発コンピューターにインストールされている場合は、削除します。 .NET 3.5フレームワークは、Windows Communication Foundation (WCF)という名前のSOAPフレームワークをサポートします。 MTOMを使用してAEM Formsを呼び出す場合、WCF（WSEではない）のみがサポートされます。

### MTOMを使用してサービスを呼び出す.NETプロジェクトの作成 {#creating-a-net-project-that-invokes-a-service-using-mtom}

Webサービスを使用してAEM Formsサービスを呼び出すことのできるMicrosoft .NETプロジェクトを作成できます。 まず、Visual Studio 2008を使用してMicrosoft .NETプロジェクトを作成します。 AEM Formsサービスを呼び出すには、プロジェクト内で呼び出すAEM Formsサービスのサービス参照を作成します。 サービス参照を作成する際に、AEM FormsサービスのURLを指定します。

```as3
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

AEM Formsをホ `localhost` ストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。 呼び出 `MyApplication/EncryptDocument` すAEM Formsサービスの名前に置き換えます。 例えば、Rights Management操作を呼び出すには、次のように指定します。

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

このオ `lc_version` プションを使用すると、MTOMなどのAEM Formsの機能を使用できます。 このオプションを指 `lc_version` 定しないと、MTOMを使用してAEM Formsを呼び出すことはできません。

サービス参照を作成すると、AEM Formsサービスに関連付けられたデータ型を.NETプロジェクト内で使用できるようになります。 AEM Formsサービスを呼び出す.NETプロジェクトを作成するには、次の手順を実行します。

1. Microsoft Visual Studio 2008を使用して.NETプロジェクトを作成します。
1. [プロジェク **ト** ]メニューの[サービス参照 **追加]を選択します**。
1. 「 **Address** 」ダイアログで、AEM FormsサービスのWSDLを指定します。 以下に例を示します。

   ```as3
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Click **Go** and then click **OK**.

### .NETプロジェクトでMTOMを使用してサービスを呼び出す {#invoking-a-service-using-mtom-in-a-net-project}

セキュリティで保護さ `MyApplication/EncryptDocument` れていないPDFドキュメントを受け取り、パスワードで暗号化されたPDFドキュメントを返すプロセスを検討します。 MTOMを使用して(Workbench `MyApplication/EncryptDocument` で構築された)プロセスを呼び出すには、次の手順を実行します。

1. Microsoft .NETプロジェクトを作成します。
1. Create a `MyApplication_EncryptDocumentClient` object by using its default constructor.
1. Create a `MyApplication_EncryptDocumentClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに渡し、エンコードの種類を指定するstring値を渡します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、必ず、を指定してくださ `?blob=mtom`い。

   >[!NOTE]
   >
   >AEM Formsをホ `hiro-xp`*ストするJ2EEアプリケーションサービスのIPアドレスに置き換えます。*

1. データメン `System.ServiceModel.BasicHttpBinding` バーの値を取得して、オブジェクトを `EncryptDocumentClient.Endpoint.Binding` 作成します。 戻り値を `BasicHttpBinding` にキャストします。
1. オブジェクト `System.ServiceModel.BasicHttpBinding` のデータメンバ `MessageEncoding` ーをに設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
1. 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

   * AEM formsユーザー名をデータメンバーに割り当てま `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`す。
   * 対応するパスワード値をデータメンバーに割り当てま `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`す。
   * 定数値をデータメン `HttpClientCredentialType.Basic` バーに割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をデータメン `BasicHttpSecurityMode.TransportCredentialOnly` バーに割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   次のコードの例に、これらのタスクを示します。

   ```as3
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、プロセスに渡すPDFドキュメントの保存に使用さ `MyApplication/EncryptDocument` れます。
1. Create a `System.IO.FileStream` object by invoking its constructor. PDFファイルの場所と、ファイルを開くドキュメントを表すstring値を渡します。
1. オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
1. オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
1. データメン `BLOB` バーにバイト配列の内容 `MTOM` を割り当てて、オブジェクトを入力します。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出し `MyApplication_EncryptDocumentClient` て、プロセスを呼び出 `invoke` します。 PDFを含むオ `BLOB` ブジェクトを渡します。ドキュメント このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. コンストラクタ `System.IO.FileStream` ーを呼び出し、保護されたPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
1. メソッドによって返されたオブジェクトのデータ内容を `BLOB` 格納するバイト配列を作成 `invoke` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

>[!NOTE]
>
>ほとんどのAEM Formsサービスの操作には、MTOMクイック開始があります。 これらのクイック開始は、サービスの対応するクイック開始セクションで表示できます。 例えば、Outputクイック開始の節を参照するには、 [Output Service APIクイック開始を参照してください](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**関連トピック**

[クイック開始:.NETプロジェクトでMTOMを使用してサービスを呼び出す](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Webサービスを使用した複数のサービスへのアクセス](#accessing-multiple-services-using-web-services)

[人間中心の長期間有効なプロセスを呼び出すASP.NET Webアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRefを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-swaref}

SwaRefを使用してAEM Formsサービスを呼び出すことができます。 XML要素のコンテンツ `wsi:swaRef` は、添付ファイルへの参照を格納するSOAP本体内の添付ファイルとして送信されます。 SwaRefを使用してFormsサービスを呼び出す場合、Java API for XML Web Services(JAX-WS)を使用してJavaプロキシクラスを作成します。 ( [Java API for XML Web Servicesを参照](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html))。

ここでは、SwaRefを使用して名前が付けられた次のFormsの短時間のみ有効なプロセスを呼び出す `MyApplication/EncryptDocument` 方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>AEM Formsで追加されたSwaRefサポート

以下では、Javaクライアントアプリケーション内でSwaRefを使用してFormsサービスを呼び出す方法について説明します。 Javaアプリケーションは、JAX-WSを使用して作成されたプロキシクラスを使用します。

### SwaRefを使用するJAX-WSライブラリファイルを使用したサービスの呼び出し {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

JAX-WSおよびSwaRefを使 `MyApplication/EncryptDocument` 用して作成されたJavaプロキシファイルを使用してプロセスを呼び出すには、次の手順を実行します。

1. サービスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを `MyApplication/EncryptDocument` 作成します。 次のWSDLエンドポイントを使用します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、「JAX-WSを使 [用したJavaプロキシクラスの作成」を参照してください](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >AEM Formsをホ `hiro-xp`*ストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、オ `MyApplicationEncryptDocumentService` ブジェクトを作成 `getEncryptDocument` します。
1. AEM Formsの呼び出しに必要な接続値を設定するには、次のデータメンバーに値を割り当てます。

   * WSDLのエンドポイントとエンコードの種類をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `ENDPOINT_ADDRESS_PROPERTY` てます。 SwaRefエンコーディングを使 `MyApplication/EncryptDocument` 用してサービスを呼び出すには、次のURL値を指定します。

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM formsユーザーをオブジェクトのフィ `javax.xml.ws.BindingProvider` ールドに割り当 `USERNAME_PROPERTY` てます。
   * 対応するパスワード値をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `PASSWORD_PROPERTY` てます。
   次のコード例は、このアプリケーションロジックを示しています。

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクターを使用してドキュメントを作成 `MyApplication/EncryptDocument` し、プロセスに送信するPDF `java.io.File` コンストラクターを取得します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
1. Create a `javax.activation.DataSource` object by using the `FileDataSource` constructor. Pass the `java.io.File` object.
1. コンストラクタを使用して `javax.activation.DataHandler` オブジェクトを渡すことによって、`javax.activation.DataSource` オブジェクトを作成します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. メソッドを呼び `BLOB` 出し、オブジェク `setSwaRef` トを渡すことで、オブジェクトを入 `javax.activation.DataHandler` 力します。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出 `MyApplicationEncryptDocument` し、PDF `invoke` メソッドを含むオブ `BLOB` ジェクトを渡して、プロセスを呼び出します。ドキュメント 呼び出しメソッドは、暗号化されたPDF `BLOB` メソッドを含むオブジェクトを返しますドキュメント。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び出して、オ `BLOB` ブジェクトを入力 `getSwaRef` します。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び `java.io.InputSteam` 出して、オブジェク `javax.activation.DataHandler` トをインスタンスに変 `getInputStream` 換します。
1. 暗号化されたPDF `java.io.InputSteam` ファイルを表すPDFファイルにインスタンスを書き込みます。ドキュメント

>[!NOTE]
>
>ほとんどのAEM Formsサービスの操作には、SwaRefクイック開始があります。 これらのクイック開始は、サービスの対応するクイック開始セクションで表示できます。 例えば、Outputクイック開始の節を参照するには、 [Output Service APIクイック開始を参照してください](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**関連トピック**

[クイック開始:JavaプロジェクトでのSwaRefを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP経由のBLOBデータを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-blob-data-over-http}

Webサービスを使用してAEM Formsサービスを呼び出し、HTTP経由でBLOBデータを渡すことができます。 HTTP経由でBLOBデータを渡す方法は、base64エンコーディング、DIME、MIMEを使用する代わりに、別の方法です。 例えば、DIMEやMIMEをサポートしていないWeb Service Enhancement 3.0を使用するMicrosoft .NETプロジェクトで、HTTP経由でデータを渡すことができます。 HTTP経由でBLOBデータを使用する場合、AEM Formsサービスが呼び出される前に入力データがアップロードされます。

「HTTP経由のBLOBデータを使用したAEM Formsの呼び出し」では、HTTP経由でBLOBデータを渡すことによって名前が付けられた、次のAEM Formsの短 `MyApplication/EncryptDocument` 時間プロセスを呼び出す方法を説明しています。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

>[!NOTE]
>
>SOAPを使用したAEM Formsの呼び出しに関する知識があることをお勧めします。 (See [Invoking AEM Forms using Web Services](#invoking-aem-forms-using-web-services).)

### HTTP経由のデータを使用する.NETクライアントアセンブリの作成 {#creating-a-net-client-assembly-that-uses-data-over-http}

HTTP経由でデータを使用するクライアントアセンブリを作成するには、「Base64エンコーディングを使用したAEM Formsの呼 [び出し」で指定したプロセスに従います](#invoking-aem-forms-using-base64-encoding)。 ただし、代わりに、プロキシクラスのURLを修正して、を含めるよ `?blob=http` うにしま `?blob=base64`す。 この操作により、データがHTTP経由で渡されます。 プロキシクラスで、次のコード行を探します。

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

次のように変更します。

```as3
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clientMyApplication/EncryptDocumentアセンブリの参照**

新しい.NETクライアントアセンブリを、クライアントアプリケーションを開発するコンピューター上に配置します。 .NETクライアントアセンブリをディレクトリに配置した後、プロジェクトから参照できます。 プロジェクトから `System.Web.Services` ライブラリを参照します。 このライブラリを参照しない場合、.NETクライアントアセンブリを使用してサービスを呼び出すことはできません。

1. [プロジェ **クト** ]メニューの[参照 **]を選**&#x200B;追加択します。
1. Click the **.NET** tab.
1. 「 **Browse** 」をクリックし、DocumentService.dllファイルを探します。
1. Click **Select** and then click **OK**.

**HTTP経由でBLOBデータを使用する.NETクライアントアセンブリを使用してサービスを呼び出す**

HTTP経由のデータを使 `MyApplication/EncryptDocument` 用する.NETクライアントアセンブリを使用して、（Workbenchで構築された）サービスを呼び出すことができます。 サービスを呼び出 `MyApplication/EncryptDocument` すには、次の手順を実行します。

1. .NETクライアントアセンブリを作成します。
1. Microsoft .NETクライアントアセンブリを参照します。 クライアントのMicrosoft .NETプロジェクトを作成します。 クライアントプロジェクトでMicrosoft .NETクライアントアセンブリを参照します。 参照も参照してくだ `System.Web.Services`さい。
1. Microsoft .NETクライアントアセンブリを使用し、デフォルトのコンストラク `MyApplication_EncryptDocumentService` タを呼び出してオブジェクトを作成します。
1. オブジェクト `MyApplication_EncryptDocumentService` のプロパティをオ `Credentials` ブジェクトで設定 `System.Net.NetworkCredential` します。 コンストラクタ `System.Net.NetworkCredential` ー内で、AEM formsのユーザー名と対応するパスワードを指定します。 認証値を設定して、.NETクライアントアプリケーションがAEM FormsとSOAPメッセージを正常に交換できるようにします。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、プロセスにデータを渡すために使用 `MyApplication/EncryptDocument` されます。
1. サービスに渡すPDFドキュメントのURI `BLOB` の場所を指 `remoteURL` 定する、オブジェクトのデータメンバーにstring値を割り当 `MyApplication/EncryptDocument`てます。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出 `MyApplication_EncryptDocumentService` し、オブジ `invoke` ェクトを渡して、プロセスを呼び出 `BLOB` します。 このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. コンストラクタ `System.UriBuilder` ーを使用し、返されたオブジェクトのデータメンバーの値を渡して、オ `BLOB` ブジェクトを作 `remoteURL` 成します。
1. オブジェクト `System.UriBuilder` をオブジェクトに変 `System.IO.Stream` 換します。 (このリストの後のC#クイック開始では、このタスクの実行方法を示します)。
1. バイト配列を作成し、オブジェクト内のデータを設定し `System.IO.Stream` ます。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡すこ `System.IO.BinaryWriter` とで、バイト配列 `Write` の内容をPDFファイルに書き込みます。

### JavaプロキシクラスとBLOBデータを使用したHTTP経由のサービスの呼び出し {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

HTTP経由でJavaプロキシクラスとBLOBデータを使用して、AEM Formsサービスを呼び出すことができます。 Javaプロキシクラスを使 `MyApplication/EncryptDocument` 用してサービスを呼び出すには、次の手順を実行します。

1. サービスWSDLを使用するJAX-WSを使用して、Javaプロキシクラスを `MyApplication/EncryptDocument` 作成します。 次のWSDLエンドポイントを使用します。

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   詳しくは、「JAX-WSを使 [用したJavaプロキシクラスの作成」を参照してください](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >AEM Formsをホ `hiro-xp`*ストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。*

1. JAX-WSを使用して作成したJavaプロキシクラスをJARファイルにパッケージ化します。
1. 次のパスにあるJavaプロキシJARファイルとJARファイルを含めます。

   &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   をJavaクライアントプロジェクトのクラスパスに追加します。

1. コンストラクタを使用して `MyApplicationEncryptDocumentService` オブジェクトを作成します。
1. オブジェクトの `MyApplicationEncryptDocument` メソッドを呼び出して、オ `MyApplicationEncryptDocumentService` ブジェクトを作成 `getEncryptDocument` します。
1. AEM Formsの呼び出しに必要な接続値を設定するには、次のデータメンバーに値を割り当てます。

   * WSDLのエンドポイントとエンコードの種類をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `ENDPOINT_ADDRESS_PROPERTY` てます。 BLOB over HTTPエンコーデ `MyApplication/EncryptDocument` ィングを使用してサービスを呼び出すには、次のURL値を指定します。

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM formsユーザーをオブジェクトのフィ `javax.xml.ws.BindingProvider` ールドに割り当 `USERNAME_PROPERTY` てます。
   * 対応するパスワード値をオブジェクトのフ `javax.xml.ws.BindingProvider` ィールドに割り当 `PASSWORD_PROPERTY` てます。
   次のコード例は、このアプリケーションロジックを示しています。

   ```as3
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. メソッドを呼び `BLOB` 出して、オブジェクトを入力 `setRemoteURL` します。 サービスに渡すPDFドキュメントのURIの場所を指定するstring値を渡し `MyApplication/EncryptDocument` ます。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出 `MyApplicationEncryptDocument` し、PDF `invoke` メソッドを含むオブ `BLOB` ジェクトを渡して、プロセスを呼び出します。ドキュメント このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. 暗号化されたPDFデータストリームを格納するバイト配列を作成します。ドキュメント オブジェクト `BLOB` のメソッド `getRemoteURL` を呼び出します(メソッド `BLOB` によって返されるオブジェ `invoke` クトを使用)。
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. オブジェクトの `java.io.FileOutputStream` メソッドを呼び出 `write` します。 暗号化されたPDFデータストリームを含むバイト配列を渡します。ドキュメント

## DIMEを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-dime}

SOAPと添付ファイルを使用して、AEM Formsサービスを呼び出すことができます。 AEM Formsは、MIMEとDIMEの両方のWebサービス標準をサポートしています。 DIMEを使用すると、添付ファイルをエンコードする代わりに、PDFドキュメントなどのバイナリ添付ファイルを呼び出し要求と共に送信できます。 「DIMEを使 *用したAEM Formsの呼び出し* 」の節では、DIMEを使用して名前が付けられた、以下のAEM Formsの短時間のみ有効なプロセスを呼び出す方法につ `MyApplication/EncryptDocument` いて説明します。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

このプロセスは、既存の AEM Forms プロセスに基づいていません。To follow along with the code examples, create a process named `MyApplication/EncryptDocument` using Workbench. （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

>[!NOTE]
>
>DIMEを使用したAEM Formsサービス操作の呼び出しは非推奨です。 MTOMを使用することをお勧めします。 (「MTOMを使用 [したAEM Formsの呼び出し](#invoking-aem-forms-using-mtom)」を参照)。

### DIMEを使用する.NETプロジェクトの作成 {#creating-a-net-project-that-uses-dime}

DIMEを使用してFormsサービスを呼び出すことのできる.NETプロジェクトを作成するには、次のタスクを実行します。

* Web Services Enhancements 2.0を開発用コンピューターにインストールします。
* .NETプロジェクト内から、FormsAEM FormsサービスへのWeb参照を作成します。

**Webサービスのインストールの強化2.0**

Web Services Enhancements 2.0を開発コンピューターにインストールし、Microsoft Visual Studio .NETと統合します。 Web Services Enhancements 2.0は、 [Microsoftダウンロードセンターからダウンロードできます。](https://www.microsoft.com/downloads/search.aspx)

このWebページから、Web Services Enhancements 2.0を検索し、開発用コンピューターにダウンロードします。 このダウンロードにより、Microsoft WSE 2.0 SPI.msiという名前のファイルがコンピューターに配置されます。 インストールプログラムを実行し、オンラインの指示に従います。

>[!NOTE]
>
>Web Services Enhancements 2.0はDIMEをサポートします。 Web Services Enhancements 2.0を使用する場合、Microsoft Visual Studioのサポートされるバージョンは2003です。Web Services Enhancements 3.0はDIMEをサポートしません。しかし、MTOMをサポートしています。

**AEM FormsサービスへのWeb参照の作成**

Web Services Enhancements 2.0を開発コンピューターにインストールし、Microsoft .NETプロジェクトを作成したら、FormsサービスへのWeb参照を作成します。 例えば、プロセスへのWeb参照を作成し、Formsがローカ `MyApplication/EncryptDocument` ルコンピューターにインストールされている場合は、次のURLを指定します。

```as3
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Web参照を作成した後、.NETプロジェクト内で使用できる2つのプロキシデータ型を次に示します。 `EncryptDocumentService` と `EncryptDocumentServiceWse`DIMEを使用してプロセ `MyApplication/EncryptDocument` スを呼び出すには、型を使用 `EncryptDocumentServiceWse` します。

>[!NOTE]
>
>FormsサービスへのWeb参照を作成する前に、プロジェクトでWeb Services Enhancements 2.0を参照していることを確認します。 （「Web Services Enhancements 2.0のインストール」を参照）。

**WSEライブラリの参照**

1. プロジェクトメニューで、「参照」を選追加択します。
1. [参照]追加ダイアログボックスで、[Microsoft.Web.Services2.dll]を選択します。
1. System.Web.Services.dllを選択します。
1. 「選択」をクリックし、「OK」をクリックします。

**FormsサービスへのWeb参照の作成**

1. プロジェクトメニューで、「Web参照」追加を選択します。
1. URLダイアログボックスで、FormsサービスのURLを指定します。
1. 「移動」をクリックし、「参照」をク追加リックします。

>[!NOTE]
>
>.NETプロジェクトでWSEライブラリを使用できるようにしてください。 プロジェクトエクスプローラで、プロジェクト名を右クリックし、[WSE 2.0を有効にする]を選択します。表示されるダイアログボックスのチェックボックスが選択されていることを確認します。

**.NETプロジェクトでDIMEを使用したサービスの呼び出し**

DIMEを使用してFormsサービスを呼び出すことができます。 セキュリティで保護さ `MyApplication/EncryptDocument` れていないPDFドキュメントを受け取り、パスワードで暗号化されたPDFドキュメントを返すプロセスを検討します。 DIMEを使用してプロセス `MyApplication/EncryptDocument` を呼び出すには、次の手順を実行します。

1. DIMEを使用してFormsサービスを呼び出せるMicrosoft .NETプロジェクトを作成します。 Web Services Enhancements 2.0が含まれていることを確認し、AEM FormsサービスへのWeb参照を作成します。
1. プロセスにWeb参照を設定した後、デフォル `MyApplication/EncryptDocument` トのコンストラクターを使 `EncryptDocumentServiceWse` 用してオブジェクトを作成します。
1. オブジェクト `EncryptDocumentServiceWse` のデータメ `Credentials` ンバーに、AEM formsのユ `System.Net.NetworkCredential` ーザー名とパスワードの値を指定する値を設定します。
1. Create a `Microsoft.Web.Services2.Dime.DimeAttachment` object by using its constructor and passing the following values:

   * GUID値を指定するstring値です。 メソッドを呼び出すと、GUID値を取得でき `System.Guid.NewGuid.ToString` ます。
   * コンテンツタイプを指定するstring値。 このプロセスにはPDFドキュメントが必要です。 `application/pdf`
   * `TypeFormat` 定義済みリスト値。 Specify `TypeFormat.MediaType`.
   * AEM Formsプロセスに渡すPDFドキュメントの場所を指定するstring値。

1. コンストラクタを使用して `BLOB` オブジェクトを作成します。
1. オ追加ブジェクトのデータメンバーにオブジ `BLOB` ェクトのデ `Microsoft.Web.Services2.Dime.DimeAttachment` ータメンバー値を割り当てる `Id` ことによ `BLOB` って、オブジェクトにDIME `attachmentID` 添付。
1. メソッドを呼 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` び出し、オブジェクトを渡 `Microsoft.Web.Services2.Dime.DimeAttachment` します。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出 `EncryptDocumentServiceWse` し、DIME添付フ `invoke` ァイルを含むオブジェクトを `BLOB` 渡すことで、プロセスを呼び出します。 このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. 返されたオブジェクトのデータメンバの値を取得して、添付フ `BLOB` ァイル識別子の値 `attachmentID` を取得します。
1. にある添付ファイルを繰り返し処 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 理し、添付ファイル識別子の値を使用して暗号化されたPDFドキュメントを取得します。
1. オブジェクト `System.IO.Stream` のデータメンバーの値を取得して、オ `Attachment` ブジェクトを `Stream` 取得します。
1. バイト配列を作成し、そのバイト配列をオブジェクトのメ `System.IO.Stream` ソッドに渡 `Read` します。 このメソッドは、暗号化されたPDFメソッドを表すデータストリームをバイト配列に入力します。ドキュメント
1. コンストラクタ `System.IO.FileStream` ーを呼び出し、PDFファイルの場所を表すstring値を渡して、オブジェクトを作成します。 このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
1. オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

### DIMEを使用するApache Axis Javaプロキシクラスの作成 {#creating-apache-axis-java-proxy-classes-that-use-dime}

Apache Axis WSDL2Javaツールを使用して、サービスWSDLをJavaプロキシクラスに変換し、サービス操作を呼び出すことができます。 Apache Antを使用すると、AEM FormsサービスのWSDLからAxisライブラリファイルを生成し、サービスを呼び出すことができます。 (「Apache Axisを使 [用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。

Apache Axis WSDL2Javaツールは、SOAP要求をサービスに送信するためのメソッドを含むJAVAファイルを生成します。 サービスが受け取ったSOAP要求は、軸生成ライブラリによってデコードされ、メソッドと引数に戻されます。

Axisで生成されたラ `MyApplication/EncryptDocument` イブラリファイルとDIMEを使用して（Workbenchで構築された）サービスを呼び出すには、次の手順を実行します。

1. Apache Axisを使用して、サービスWSDLを使用するJava `MyApplication/EncryptDocument` プロキシクラスを作成します。 (「Apache Axisを使 [用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。
1. クラスパスにJavaプロキシクラスを含めます。
1. コンストラクタを使用して `MyApplicationEncryptDocumentServiceLocator` オブジェクトを作成します。
1. コンストラク `URL` ターを使用し、AEM FormsサービスのWSDL定義を指定する文字列値を渡して、オブジェクトを作成します。 SOAPエンドポイントURL `?blob=dime` の末尾で指定する必要があります。 例えば、

   ```as3
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. コンストラクタ `EncryptDocumentSoapBindingStub` ーを呼び出し、オブジェクトとオブジ `MyApplicationEncryptDocumentServiceLocator`ェクトを渡して、オブジェクトを作 `URL` 成します。
1. AEM formsのユーザー名とパスワードの値を設定するには、オブジェクト `EncryptDocumentSoapBindingStub` とメソッドを呼び `setUsername` 出し `setPassword` ます。

   ```as3
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. オブジェクトを作成して、ドキュメントに送信するPDF `MyApplication/EncryptDocument` サービスを取得 `java.io.File` します。 PDFの場所を指定するstring値を渡します。ドキュメントの場合は
1. Create a `javax.activation.DataHandler` object by using its constructor and passing a `javax.activation.FileDataSource` object. オブジ `javax.activation.FileDataSource` ェクトは、コンストラクターを使用し、PDFドキュメントを表すオブジェクトを渡 `java.io.File` すことで作成できます。
1. Create an `org.apache.axis.attachments.AttachmentPart` object by using its constructor and passing the `javax.activation.DataHandler` object.
1. オブジェクトのメソッドを呼び出し、オ `EncryptDocumentSoapBindingStub` ブジェクトを渡す `addAttachment` ことによって添付ファイルを添 `org.apache.axis.attachments.AttachmentPart` 付します。
1. コンストラクタを使用して `BLOB` オブジェクトを作成します。オブジェクト `BLOB` のメソッドを呼び出し、添付ファイル識別子 `BLOB` の値を渡すことで、オ `setAttachmentID` ブジェクトに添付ファイル識別子の値を設定します。 この値は、オブジェクトのメソッドを呼び出す `org.apache.axis.attachments.AttachmentPart` ことで取得で `getContentId` きます。
1. オブジェクト `MyApplication/EncryptDocument` のメソッドを呼び出し `EncryptDocumentSoapBindingStub` て、プロセスを呼び出 `invoke` します。 DIME添付ファイル `BLOB` を含むオブジェクトを渡します。 このプロセスは、オブジェクト内の暗号化されたPDFドキュメントを返 `BLOB` します。
1. 返されたオブジェクトのメソッドを呼び出して、添付フ `BLOB` ァイル識別子の値を取 `getAttachmentID` 得します。 このメソッドは、返される添付ファイルの識別子の値を表すstring値を返します。
1. オブジェクトのメソッドを呼び出して、 `EncryptDocumentSoapBindingStub` 添付ファイルを取 `getAttachments` 得します。 このメソッドは、添付ファイルを表 `Objects` す配列を返します。
1. 添付ファイル（配列）を繰り返し処 `Object` 理し、添付ファイル識別子の値を使用して、暗号化されたPDFドキュメントを取得します。 各要素はオブジェクト `org.apache.axis.attachments.AttachmentPart` です。
1. オブジェクトの `javax.activation.DataHandler` メソッドを呼び出して、添付ファイルに関連付け `org.apache.axis.attachments.AttachmentPart` られたオブジェクトを取 `getDataHandler` 得します。
1. オブジェクトの `java.io.FileStream` メソッドを呼び出して、オ `javax.activation.DataHandler` ブジェクトを取得 `getInputStream` します。
1. バイト配列を作成し、そのバイト配列をオブジェクトのメ `java.io.FileStream` ソッドに渡 `read` します。 このメソッドは、暗号化されたPDFメソッドを表すデータストリームをバイト配列に入力します。ドキュメント
1. コンストラクタを使用して `java.io.File` オブジェクトを作成します。このオブジェクトは、暗号化されたPDFドキュメントを表します。
1. コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
1. オブジェクト `java.io.FileOutputStream` のメソッドを `write` 呼び出し、暗号化されたPDFメソッドを表すデータストリームを含むバイト配列を渡します。ドキュメント

**関連トピック**

[クイック開始:JavaプロジェクトでのDIMEを使用したサービスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAMLベースの認証の使用 {#using-saml-based-authentication}

AEM Formsでは、サービスを呼び出す際に、様々なWebサービス認証モードをサポートしています。 1つの認証モードは、Webサービス呼び出しの基本認証ヘッダーを使用して、ユーザー名とパスワードの両方の値を指定します。 AEM Formsは、SAMLアサーションベースの認証もサポートします。 クライアントアプリケーションがWebサービスを使用してAEM Formsサービスを呼び出す場合、クライアントアプリケーションは次のいずれかの方法で認証情報を提供できます。

* 基本認証の一部としての資格情報の受け渡し
* WS-Securityヘッダーの一部としてユーザー名トークンを渡す
* WS-Securityヘッダーの一部としてSAMLアサーションを渡す
* WS-Securityヘッダーの一部としてKerberosトークンを渡す

AEM Formsは、標準の証明書ベースの認証をサポートしていませんが、別のフォームの証明書ベースの認証をサポートしています。

>[!NOTE]
>
>「AEM Formsによるプログラミング」のWebサービスのクイック開始では、認証を実行するためのユーザー名とパスワードの値を指定します。

AEM FormsユーザーのIDは、秘密キーを使用して署名されたSAMLアサーションを通じて表現できます。 次のXMLコードは、SAMLアサーションの例を示しています。

```as3
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

この例のアサーションは、管理者ユーザーに対して発行されます。 このアサーションには、次の顕著な項目が含まれます。

* これは、特定の期間有効です。
* 特定のユーザーに対して発行されます。
* デジタル署名されています。 そのため、変更を加えると署名が破られます。
* AEM Formsには、ユーザー名やパスワードに類似したユーザーのIDのトークンとして表示できます。

クライアントアプリケーションは、オブジェクトを返す任意のAEM Forms AuthenticationManager APIからアサーションを取得で `AuthResult` きます。 次の2つの方法のい `AuthResult` ずれかを実行して、インスタンスを取得できます。

* AuthenticationManager APIで公開されているいずれかの認証方法を使用したユーザーの認証。 通常、ユーザー名とパスワードを使用します。ただし、証明書認証を使用することもできます。
* メソッドを使 `AuthenticationManager.getAuthResultOnBehalfOfUser` 用します。 このメソッドを使用すると、クライアントアプリケーションで任意のAEM forms `AuthResult` ユーザーのオブジェクトを取得できます。

aem formsユーザーは、取得したSAMLトークンを使用して認証できます。 このSAMLアサーション（xmlフラグメント）は、WS-Securityヘッダーの一部として、ユーザー認証のためのWebサービス呼び出しと共に送信できます。 通常、クライアントアプリケーションはユーザーを認証しましたが、ユーザーの資格情報を保存していません。 （または、ユーザーがユーザー名とパスワード以外のメカニズムを使用してそのクライアントにログオンした場合）。この場合、クライアントアプリケーションはAEM Formsを呼び出し、AEM Formsの呼び出しを許可されている特定のユーザーを装う必要があります。

特定のユーザーを装うには、Webサービスを使用し `AuthenticationManager.getAuthResultOnBehalfOfUser` てメソッドを呼び出します。 このメソッドは、そのユー `AuthResult` ザーのSAMLアサーションを含むインスタンスを返します。

次に、そのSAMLアサーションを使用して、認証が必要なサービスを呼び出します。 この操作では、SOAPヘッダーの一部としてアサーションを送信します。 このアサーションを使用してWebサービスが呼び出されると、AEM Formsはユーザーをそのアサーションが表すユーザーとして識別します。 つまり、アサーションで指定されたユーザーは、サービスを呼び出すユーザーです。

### Apache AxisクラスとSAMLベースの認証の使用 {#using-apache-axis-classes-and-saml-based-authentication}

Axisライブラリを使用して作成されたJavaプロキシクラスによってAEM Formsサービスを呼び出すことができます。 (「Apache Axisを使 [用したJavaプロキシクラスの作成](#creating-java-proxy-classes-using-apache-axis)」を参照)。

SAMLベースの認証を使用するAXISを使用する場合は、Axisにリクエストおよび応答ハンドラーを登録します。 Apache Axisは、呼び出し要求をAEM Formsに送信する前にハンドラーを呼び出します。 ハンドラーを登録するには、拡張するJavaクラスを作成しま `org.apache.axis.handlers.BasicHandler`す。

**軸を使用したAssertionHandlerの作成**

次のJavaクラスは、という名前 `AssertionHandler.java`で、拡張するJavaクラスの例を示していま `org.apache.axis.handlers.BasicHandler`す。

```as3
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

ハンドラーをAxisに登録するには、client-config.wsddファイルを作成します。 デフォルトでは、Axisはこの名前のファイルを検索します。 次のXMLコードは、client-config.wsddファイルの例です。 詳しくは、Axisのドキュメントを参照してください。

```as3
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

次のコード例は、SAMLベースの認証を使用してAEM Formsサービスを呼び出します。

```as3
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

.NETクライアントアセンブリとSAMLベースの認証を使用して、Formsサービスを呼び出すことができます。 これを行うには、Web Service Enhancements 3.0(WSE)を使用する必要があります。 WSEを使用する.NETクライアントアセンブリの作成については、「DIMEを使用する.NET [プロジェクトの作成」を参照してください](#creating-a-net-project-that-uses-dime)。

>[!NOTE]
>
>DIMEセクションではWSE 2.0を使用します。SAMLベースの認証を使用するには、DIMEトピックで指定されているのと同じ手順に従います。 ただし、WSE 2.0をWSE 3.0に置き換えます。Web Services Enhancements 3.0を開発コンピューターにインストールし、Microsoft Visual Studio .NETと統合します。 Web Services Enhancements 3.0は、 [Microsoftダウンロードセンターからダウンロードできます](https://www.microsoft.com/downloads/search.aspx)。

WSEアーキテクチャは、ポリシー、アサーション、SecurityTokenの各データ型を使用します。 簡単に、Webサービスの呼び出しの場合は、ポリシーを指定します。 ポリシーには複数のアサーションを含めることができます。 各アサーションにはフィルターを含める。 フィルターは、Webサービス呼び出しの特定のステージで呼び出され、その時点でSOAP要求を変更できます。 詳しくは、Web Service Enhancements 3.0のドキュメントを参照してください。

**アサーションとフィルターの作成**

次のC#コードの例は、filterクラスとassertionクラスを作成します。 このコード例では、SamlAssertionOutputFilterを作成します。 このフィルターは、SOAP要求がAEM Formsに送信される前に、WSEフレームワークによって呼び出されます。

```as3
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

SAMLアサーションを表すクラスを作成します。 このクラスが実行するメインタスクは、データ値を文字列からxmlに変換し、空白を保持することです。 このアサーションxmlは、後でSOAP要求に読み込まれます。

```as3
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

```as3
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

### サービス操作の非同期呼び出し {#invoking-service-operations-asynchronously}

Generate PDFの操作など、AEM Formsサービスの操作を非同期で呼び出そうとすると、 `htmlToPDF` が発生し `SoapFaultException` ます。 この問題を解決するには、要素と他の要素を異なるクラスにマップするカスタ `ExportPDF_Result` ム連結XMLファイルを作成します。 次のXMLは、カスタム連結ファイルを表しています。

```as3
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

JAX-WSを使用してJavaプロキシファイルを作成する場合は、このXMLファイルを使用します。 (JAX-WSを使 [用したJavaプロキシクラスの作成を参照](#creating-java-proxy-classes-using-jax-ws))。

JAX-WSツール(wsimport.exe)を実行する際に、 — コマンドラインオプションを使用してこのXMLファイル `b` を参照します。 連結XMLフ `wsdlLocation` ァイル内の要素を更新し、AEM FormsのURLを指定します。

非同期呼び出しが確実に機能するようにするには、エンドポイントURL値を変更し、を指定しま `async=true`す。 例えば、JAX-WSで作成されるJavaプロキシファイルの場合、に次のように指定します `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

次のリストは、非同期で呼び出された場合にカスタム連結ファイルを必要とする他のサービスを指定します。

* PDFG 3D
* タスクマネージャ
* Application Manager
* ディレクトリマネージャ
* Distiller
* Rights Management
* Document Management

### J2EEアプリケーションサーバーの違い {#differences-in-j2ee-application-servers}

特定のJ2EEアプリケーションサーバーを使用して作成されたプロキシライブラリが、別のJ2EEアプリケーションサーバーでホストされているAEM Formsを正常に呼び出せない場合があります。 WebSphereにデプロイされたAEM Formsを使用して生成されるプロキシライブラリを考えてみましょう。 このプロキシライブラリは、JBoss Application ServerにデプロイされたAEM Formsサービスを正常に呼び出すことができません。

AEM Formsの複雑なデータ型の中には、例えば、AEM FormsをWebSphereにデプロイする場合とJBoss Application Serverとで `PrincipalReference`は異なる方法で定義されるものもあります。 WSDL定義に違いがあるのは、異なるJ2EEアプリケーションサービスで使用されるJDKの違いです。 その結果、同じJ2EEアプリケーションサーバーから生成されたプロキシライブラリを使用します。

### Webサービスを使用した複数のサービスへのアクセス {#accessing-multiple-services-using-web-services}

名前空間の競合により、データオブジェクトを複数のサービスWSDL間で共有することはできません。 様々なサービスでデータ型を共有できるので、WSDLでこれらの型の定義を共有します。 例えば、データ型を含む2つの.NETクライアントアセンブリを同じ.NET `BLOB` クライアントプロジェクトに追加することはできません。 これを行うと、コンパイルエラーが発生します。

次のリストは、複数のサービスWSDL間で共有できないデータ型を指定します。

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

この問題を回避するには、データタイプを完全に修飾することをお勧めします。 例えば、サービス参照を使用してFormsサービスとSignatureサービスの両方を参照する.NETアプリケーションを考えてみましょう。 両方のサービス参照にはクラスが含ま `BLOB` れます。 インスタンスを使 `BLOB` 用するには、宣言時にオブジェ `BLOB` クトを完全修飾します。 この方法は、次のコード例に示します。 このコード例について詳しくは、「インタラクティブフォームへ [の電子署名」を参照してくださ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)い。

次のC#コードの例は、Formsサービスによってレンダリングされるインタラクティブフォームに署名します。 クライアントアプリケーションには2つのサービス参照があります。 Formsサー `BLOB` ビスに関連付けられているインスタンスは、そのサービスに属し `SignInteractiveForm.ServiceReference2` ています。 同様に、Signatureサー `BLOB` ビスに関連付けられているインスタンスは、そのインスタンスに属し `SignInteractiveForm.ServiceReference1` ます。 署名済みのインタラクティブフォームは、 *LoanXFASigned.pdfというPDFファイルとして保存されます*。

```as3
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

### 無効なプロキシファイルを生成する文字で始まるサービス {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Microsoft .Net 3.5およびWCFを使用する場合、AEM Formsで生成された一部のプロキシクラスの名前が正しくありません。 この問題は、IBMFilenetContentRepositoryConnector、IDPSchedulerServiceまたは名前が文字Iで開始される他のサービス用のプロキシクラスが作成された場合に発生します。例えば、IBMFileNetContentRepositoryConnectorの場合は、生成されたクライアントの名前がになりま `BMFileNetContentRepositoryConnectorClient`す。 生成されたプロキシクラスにレターIがありません。

