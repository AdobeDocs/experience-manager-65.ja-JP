---
title: Remoting を使用した AEM Forms の呼び出し
seo-title: Invoking AEM Forms using Remoting
description: Remoting を使用して AEM Forms プロセスを起動し、Workbench で作成されたプロセスを呼び出します。Flex で作成されたクライアントアプリケーションから AEM Forms プロセスを呼び出すことができます。
seo-description: Use Remoting to invoke an AEM Forms process to invoke processes created in Workbench. You can invoke a AEM Forms process from a client application built with Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '4628'
ht-degree: 100%

---

# Remoting を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-remoting}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Workbench で作成されたプロセスは、Remoting を使用して呼び出すことができます。つまり、Flex で作成されたクライアントアプリケーションから AEM Forms プロセスを呼び出すことができます。この機能は、データサービスに基づいています。

>[!NOTE]
>
>Remoting を使用する場合は、AEM Forms サービスとは異なり、Workbench で作成されたプロセスを呼び出すことをお勧めします。ただし、AEM Forms サービスを直接呼び出すことは可能です。（AEM Forms デベロッパーセンターにある「Remoting を使用した PDF ドキュメントの暗号化」を参照）。

>[!NOTE]
>
>AEM Forms サービスが匿名アクセスを許可するように設定されていない場合、Flex クライアントからのリクエストによって web ブラウザーで問題が発生します。ユーザーは、ユーザー名とパスワードの資格情報を入力する必要があります。

次の AEM Forms の短時間のみ有効なプロセス（`MyApplication/EncryptDocument`）は、Remoting を使って呼び出すことができます。（このプロセスの入力値や出力値などについて詳しくは、[短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md)を参照。）

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Flex アプリケーションを使用して AEM Forms プロセスを呼び出すには、リモートエンドポイントが有効になっていることを確認します。 プロセスをデプロイすると、デフォルトでリモートエンドポイントが有効になります。

このプロセスを呼び出すと、次のアクションが実行されます。

1. 入力値として渡された保護されていない PDF ドキュメントを取得します。 このアクションは `SetValue` 操作に基づいています。入力パラメーターの名前は `inDoc` で、そのデータタイプは `document` です。（`document` データタイプは、Workbench 内で使用できるデータタイプです。）
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。このプロセスの出力値の名前は `outDoc` で、パスワードで暗号化された PDF ドキュメントを表します。outDoc のデータタイプは `document` です。
1. パスワードで暗号化した PDF ドキュメントを PDF ファイルとしてローカルファイルシステムに保存します。このアクションは `WriteDocument` 操作に基づいています。

>[!NOTE]
>
>`MyApplication/EncryptDocument` プロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。

>[!NOTE]
>
>Remoting を使用して長期間有効なプロセスを呼び出す方法について詳しくは、[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください。

**関連トピック**

[AEM Forms Flex ライブラリファイルを含める](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex で作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Remoting を使用したカスタムコンポーネントサービスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[HTTP トークンを使用した SSO 認証を実行する Flash Builder アプリケーションの作成](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Flex グラフコントロールにプロセスデータを表示する方法について詳しくは、[Flex グラフでの AEM Forms プロセスデータの表示](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)を参照してください。

>[!NOTE]
>
>*crossdomain.xml ファイルを適切な場所に配置してください。例えば、JBoss に AEM Forms をデプロイしたとすると、次の場所にこのファイルを配置します。&lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## AEM Forms Flex ライブラリファイルを含める {#including-the-aem-forms-flex-library-file}

Remoting を使用して AEM Forms プロセスをプログラムで呼び出すには、adobe-remoting-provider.swc ファイルを Flex プロジェクトのクラスパスに追加します。この SWC ファイルは次の場所にあります。

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   ここで、&lt;*install_directory*> は、AEM Forms がインストールされているディレクトリです。

**関連トピック**

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex で作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Remoting を使用したドキュメントの処理 {#handling-documents-with-remoting}

AEM Forms で使用される最も重要な非プリミティブ Java タイプの 1 つは、 `com.adobe.idp.Document` クラスです。ドキュメントは、通常、AEM Forms 操作を呼び出すために必要です。主に PDF ドキュメントですが、SWF、HTML、XML、DOC ファイルなど、他のドキュメントタイプを含めることができます。（[Java API を使用した AEM Forms サービスへのデータの受け渡し](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)を参照。）

Flex で作成されたクライアントアプリケーションは、ドキュメントを直接リクエストできません。例えば、Adobe Reader を起動して、PDF ファイルを生成する URL をリクエストできません。PDF や Microsoft Word ドキュメントなどのドキュメントタイプのリクエストは、URL である結果を返します。URL のコンテンツを表示するのはクライアントの責任です。Document Management サービスは、URL およびコンテンツタイプ情報の生成に役立ちます。XML ドキュメントのリクエストは、結果に完全な XML ドキュメントを返します。

### 入力パラメーターとしてのドキュメントの受け渡し {#passing-a-document-as-an-input-parameter}

Flex で作成されたクライアントアプリケーションは、ドキュメントを AEM Forms プロセスに直接渡すことができません。代わりに、クライアントアプリケーションは `mx.rpc.livecycle.DocumentReference` ActionScript クラスのインスタンスを使用して、`com.adobe.idp.Document` インスタンスを必要とする操作に入力パラメーターを渡します。Flex クライアントアプリケーションには、`DocumentReference` オブジェクトを設定するためのいくつかのオプションがあります。

* ドキュメントがサーバー上にあり、そのファイルの場所がわかっている場合は、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_FILE に設定します。次の例に示すように、fileRef プロパティをファイルの場所に設定します。

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* ドキュメントがサーバー上にあり、その URL がわかっている場合は、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_URL に設定します。次の例に示すように、url プロパティを URL に設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* クライアントアプリケーションのテキスト文字列から DocumentReference オブジェクトを作成するには、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_INLINE に設定します。次の例に示すように、text プロパティを、オブジェクトに含めるテキストに設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* ドキュメントがサーバー上にない場合は、Remoting アップロードサーブレットを使用して、ドキュメントを AEM Forms にアップロードします。AEM Forms の新機能は、セキュアなドキュメントをアップロードする機能です。セキュアなドキュメントをアップロードする場合、*ドキュメントアップロードアプリケーションユーザー*&#x200B;の役割を持つユーザーを使用する必要があります。この役割がないと、ユーザーはセキュアなドキュメントをアップロードできません。セキュアなドキュメントをアップロードする場合は、シングルサインオンを使用することをお勧めします。（[Remoting を使用したプロセスを呼び出すためのセキュアなドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)を参照。）

>[!NOTE]
>セキュアでないドキュメントのアップロードを許可するように AEM Forms が設定されている場合は、ドキュメントのアップロードアプリケーションユーザーの役割を持たないユーザーを使用してドキュメントをアップロードできます。ユーザーは、ドキュメントのアップロード権限を持つこともできます。ただし、AEM Forms がセキュアなドキュメントのみを許可するように設定されている場合は、ユーザーに「ドキュメントのアップロードアプリケーションユーザー」の役割または「ドキュメントのアップロード」権限があることを確認します。（[セキュアなドキュメントとセキュアでないドキュメントを受け入れるための AEM Forms の設定](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)を参照。

指定したアップロード URL には、標準の Flash アップロード機能を使用します：`https://SERVER:PORT/remoting/lcfileupload`。その後、タイプ `Document` の入力パラメーターが予想される場所であればどこでも `DocumentReference` を使用できます
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`Remoting クイックスタートは、Remoting アップロードサーブレットを使用して、PDF ファイルを `MyApplication/EncryptDocument` プロセスに渡します。（[AEM Forms Remoting（AEM Forms では非推奨）を使用してセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)を参照。）

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

Remoting クイックスタートは、Remoting アップロードサーブレットを使用して、PDF ファイルを `MyApplication/EncryptDocument` プロセスに渡します。（[AEM Forms Remoting（AEM forms では非推奨）を使用して、セキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)を参照。）

### クライアントアプリケーションにドキュメントを戻す {#passing-a-document-back-to-a-client-application}

クライアントアプリケーションは、出力パラメーターとして `com.adobe.idp.Document` インスタンスを返すサービス操作のタイプ `mx.rpc.livecycle.DocumentReference` のオブジェクトを受け取ります。クライアントアプリケーションは Java ではなく ActionScript オブジェクトを扱うので、Java ベースの ドキュメントオブジェクトを Flex クライアントに戻すことはできません。代わりに、サーバーはドキュメントの URL を生成し、その URL をクライアントに戻します。`DocumentReference` オブジェクトの `referenceType` プロパティは、コンテンツが `DocumentReference` オブジェクト内にあるか、`DocumentReference.url` プロパティで URL から取得する必要があるかを指定します。`DocumentReference.contentType` プロパティはドキュメントのタイプを指定します。

**関連トピック**

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Flex ライブラリファイルを含める](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex で作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remoting を使用してセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Flex で作成されたアプリケーションから AEM Forms プロセスを呼び出すには、次のタスクを実行します。

1. `mx:RemoteObject` インスタンスを作成します。
1. `ChannelSet` インスタンスを作成します。
1. 必要な入力値を渡します。
1. 戻り値を処理します。

>[!NOTE]
>この節では、セキュアでないドキュメントをアップロードするように AEM Forms が設定されている場合に、AEM Forms プロセスを呼び出してドキュメントをアップロードする方法について説明します。AEM Forms プロセスを呼び出し、セキュアなドキュメントをアップロードする方法、およびセキュアなドキュメントとセキュアでないドキュメントを受け入れるように AEM Forms を設定する方法について詳しくは、[Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)を参照してくだい。

**mx:RemoteObject インスタンスの作成**

`mx:RemoteObject` インスタンス作成して、Workbench で作成された AEM Forms プロセスを呼び出します。`mx:RemoteObject` インスタンスを作成するには、次の値を指定します。

* **id：**&#x200B;呼び出すプロセスを表す `mx:RemoteObject` インスタンスの名前。
* **宛先：**&#x200B;呼び出す AEM Forms プロセスの名前。例えば、`MyApplication/EncryptDocument` プロセスを呼び出すには、`MyApplication/EncryptDocument` を指定します。
* **result：**&#x200B;結果を処理する Flex メソッドの名前。

`mx:RemoteObject` タグで、プロセスの呼び出しメソッドの名前を指定する `<mx:method>` タグを指定します。通常、Forms 呼び出しメソッドの名前は `invoke` です。

次のコードの例では、`MyApplication/EncryptDocument` プロセスを呼び出す `mx:RemoteObject` インスタンスを作成します。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**AEM Forms へのチャネルを作成**

次の ActionScript の例に示すように、クライアントアプリケーションは MXML または ActionScript でチャネルを指定することで、AEM Forms を呼び出すことができます。チャネルは、`AMFChannel`、`SecureAMFChannel`、`HTTPChannel`、`SecureHTTPChannel` のいずれかである必要があります。

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

`ChannelSet` インスタンスを `mx:RemoteObject` インスタンスの `channelSet` フィールドに割り当てます（前のコードの例を参照）。一般的には、`ChannelSet.addChannel` メソッドの呼び出し時に完全修飾名を指定するのではなく、インポートステートメントでチャネルクラスをインポートします。

**入力値の受け渡し**

Workbench で作成されたプロセスは、0 個以上の入力パラメーターを受け取り、出力値を返すことができます。クライアントアプリケーションは、AEM Forms プロセスに属するパラメーターに対応するフィールドをもつ `ActionScript` オブジェクト内の入力パラメーターを渡します。この短時間のみ有効なプロセス（`MyApplication/EncryptDocument`）には、1 つの入力パラメーター（`inDoc`）が必要です。プロセスによって公開される操作の名前は `invoke`（短時間のみ有効なプロセスのデフォルト名）です。（[（AEM Forms では非推奨）AEM Forms リモートを使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)を参照。）

次のコードの例では、PDF ドキュメントを `MyApplication/EncryptDocument` プロセスに渡します。

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

このコードの例では、`pdfDocument` は保護されていない PDF ドキュメントを含む `DocumentReference` インスタンスです。`DocumentReference` について詳しくは、[（AEM Forms では非推奨）AEM Forms リモートによるドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)を参照してください。

**特定のバージョンのサービスの呼び出し**

呼び出しのパラメーターマップで `_version` パラメーターを使用すると、特定のバージョンの Forms サービスを呼び出すことができます。例えば、`MyApplication/EncryptDocument` サービスのバージョン 1.2 を呼び出すには、次のように指定します。

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

`version` パラメーターは、1 つのピリオドを含む文字列である必要があります。ピリオドの左側の値（メジャーバージョン）と右側の値（マイナーバージョン）は整数である必要があります。このパラメーターを指定しない場合、ヘッドアクティブバージョンが呼び出されます。

**戻り値の処理**

AEM Forms プロセスの出力パラメーターは、次の例に示すように、ActionScript オブジェクトにデシリアライズされ、クライアントアプリケーションはこのオブジェクトから名前で特定のパラメーターを抽出します。（`MyApplication/EncryptDocument` プロセスの出力値の名前は `outDoc` です。）

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**MyApplication/EncryptDocument プロセスの呼び出し**

次の手順を実行して `MyApplication/EncryptDocument` プロセスを呼び出すことができます。

1. ActionScript または MXML を使用して `mx:RemoteObject` インスタンスを作成します。「mx:RemoteObject インスタンスの作成」を参照してください。
1. AEM Forms と通信するための `ChannelSet` インスタンスを設定し、それを `mx:RemoteObject` インスタンスに関連付けます。「AEM Forms へのチャネルを作成」を参照してください。
1. ChannelSet の `login` メソッドまたはサービスの `setCredentials` メソッドを呼び出して、ユーザー識別子の値とパスワードを指定します。（[シングルサインオンの使用](invoking-aem-forms-using-remoting.md#using-single-sign-on)を参照。）
1. `mx.rpc.livecycle.DocumentReference` インスタンスに、`MyApplication/EncryptDocument` プロセスに渡す保護されていない PDF ドキュメントを入力します。（[ドキュメントの入力パラメーターとしての受け渡し](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)を参照。）
1. `mx:RemoteObject` インスタンスの `invoke` メソッドを呼び出して PDF ドキュメントを暗号化します。入力パラメーター（保護されていない PDF ドキュメント）を含む `Object` を渡します。「入力値を渡す」を参照してください。
1. プロセスから返される、パスワードで暗号化された PDF ドキュメントを取得します。 「戻り値の処理」を参照してください。

[クイックスタート：（AEM Forms では非推奨）AEM Forms Remoting を使用して保護されていないドキュメントを渡すことにより、短期間のプロセスを呼び出す](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Flex で作成されたクライアントアプリケーションの認証 {#authenticating-client-applications-built-with-flex}

AEM Forms User Manager で Flex アプリケーションからリモートリクエストを認証する方法はいくつかあり、これには、中央のログインサービスを使用した AEM Forms のシングルサインオン、基本認証、カスタム認証などが含まれます。 シングルサインオンも匿名アクセスも有効になっていない場合、リモートリクエストは基本認証（デフォルト）またはカスタム認証のいずれかになります。

基本認証は、web アプリケーションコンテナからの標準の J2EE 基本認証に依存しています。基本認証の場合、HTTP 401 エラーはブラウザーの問題の原因になります。 つまり、Flex アプリケーションからまだログインしていない状態で、RemoteObject を使用して Forms アプリケーションに接続しようとすると、ブラウザーがユーザー名とパスワードの入力を求めます。

カスタム認証の場合、サーバーはクライアントに fault を送信し、認証が必要であることを示します。

>[!NOTE]
>HTTP トークンを使用した認証の実行について詳しくは、[HTTP トークンを使用した SSO 認証を実行する Flash Builder アプリケーションの作成](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)を参照してください。

### カスタム認証の使用 {#using-custom-authentication}

管理コンソールでカスタム認証を有効にするには、リモートエンドポイントの認証方法を「基本」から「カスタム」に変更します。カスタム認証を使用する場合、クライアントアプリケーションはログインには `ChannelSet.login` メソッド、ログアウトには `ChannelSet.logout` メソッドを呼び出します。

>[!NOTE]
>以前のリリースの AEM Forms では、`RemoteObject.setCredentials` メソッドを呼び出して資格情報を宛先に送信していました。`setCredentials` メソッドは、コンポーネントがサーバーへの接続を最初に試みるまで、資格情報を実際にサーバーに渡しませんでした。したがって、コンポーネントが障害イベントを発行した場合、その障害が認証エラーによって発生したか、別の理由で発生したかを確認することはできません。 `ChannelSet.login`メソッドは、呼び出し時にサーバーに接続し、認証の問題をすぐに処理できるようにします。 `setCredentials` メソッドは引き続き使用できますが、`ChannelSet.login` メソッドを使用することをお勧めします。

同じチャンネルと対応する ChannelSet オブジェクトを複数の宛先で使用できるので、1 つの宛先にログインすると、同じ単一のチャンネルまたは同じ複数のチャンネルを使用する他の宛先にログインされます。 2 つのコンポーネントが同じ ChannelSet オブジェクトに異なる資格情報を適用する場合は、最後に適用された資格情報が使用されます。 複数のコンポーネントが同じ認証済み ChannelSet オブジェクトを使用している場合、`logout` メソッドは、すべてのコンポーネントを宛先からログアウトします。

次の例では、`ChannelSet.login` および `ChannelSet.logout` メソッドと RemoteObject コントロールを使用します。 このアプリケーションは、次のアクションを実行します。

* `RemoteObject` コンポーネントによって使用されるチャンネルを表す `creationComplete` ハンドラー内に `ChannelSet` オブジェクトを作成する
* ボタンクリックイベントに応答して `ROLogin` 関数を呼び出すことにより、サーバーに資格情報を渡す
* RemoteObject コンポーネントを使用して、ボタンクリックイベントに応答して文字列をサーバーに送信します。 サーバーが同じ文字列を RemoteObject コンポーネントに返します
* RemoteObject コンポーネントの「結果イベント」を使用して、 TextArea コントロールに文字列を表示します
* ボタンクリックイベントに応答して `ROLogout` 関数を呼び出すことにより、サーバーからログアウトします。

```java
 <?xml version=”1.0”?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%”
     height=”100%” creationComplete=”creationCompleteHandler();”>
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login(“sampleuser”, “samplepassword”);
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case “success”:
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case “Client.Authentication”:
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show(“Login failure: “ + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case “success”:
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show(“Logout failure: “ + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += “Server responded: “+ event.result + “\n”;
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += “Received fault: “ + event.fault + “\n”;
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text=”Enter a text for the server to echo”/>
         <mx:TextInput id=”ti” text=”Hello World!”/>
         <mx:Button label=”Login”
             click=”ROLogin();”/>
         <mx:Button label=”Echo”
             enabled=”{authenticatedCB.selected}”
             click=”remoteObject.echo(ti.text);”/>
         <mx:Button label=”Logout”
             click=”ROLogout();”/>
         <mx:CheckBox id=”authenticatedCB”
             label=”Authenticated?”
             enabled=”false”/>
     </mx:HBox>
     <mx:TextArea id=”ta” width=”100%” height=”100%”/>
 
     <mx:RemoteObject id=”remoteObject”
         destination=”myDest”
         result=”resultHandler(event);”
         fault=”faultHandler(event);”/>
 </mx:Application>
```

`login` および `logout` メソッドは AsyncToken オブジェクトを返します。 結果イベントが「成功した呼び出し」を処理し、障害イベントが失敗を処理するために、イベントハンドラーを AsyncToken オブジェクトに割り当てます。

### シングルサインオンの使用 {#using-single-sign-on}

AEM Forms ユーザーは、複数の AEM Forms web アプリケーションに接続してタスクを実行できます。 ユーザーが web アプリケーション間を移動する際に、web アプリケーションごに個別にログインさせるのは効率的ではありません。 AEM Forms のシングルサインオンメカニズムを使用すると、ユーザーは 1 回ログインして任意の AEM Forms web アプリケーションにアクセスできます。 AEM Forms のデベロッパーは AEM Forms と使用するクライアントアプリケーションを作成できるので、シングルサインオンメカニズムを利用する能力も必要です。

各 AEM Forms web アプリケーションは、独自の web アーカイブ（WAR）ファイルにパッケージ化されます。このファイルは、エンタープライズアーカイブ（EAR）ファイルの一部としてパッケージ化されます。 アプリケーションサーバーでは異なる web アプリケーション間でのセッションデータの共有が許可されないので、AEM Forms では HTTP Cookie を使用して認証情報を保存します。 認証 Cookie を使用すると、ユーザーは Forms アプリケーションにログインしてから、他の AEM Forms web アプリケーションに接続することができます。 この手法は、シングルサインオンと呼ばれます。

AEM Forms のデベロッパーは、フォームガイド（非推奨）の機能を拡張し、Workspace をカスタマイズするためのクライアントアプリケーションを作成します。 例えば、Workspace アプリケーションはプロセスを開始することができます。 次に、クライアントアプリケーションはリモートエンドポイントを使用して Forms サービスからデータを取得します。

AEM Forms Remoting（AEM Forms では非推奨）を使用して AEM Forms サービスが呼び出されると、クライアントアプリケーションは認証 Cookie をリクエストの一部として渡します。 ユーザーは既に認証されているので、クライアントアプリケーションから AEM Forms サービスに接続するために、追加のログインは必要ありません。

>[!NOTE]
>Cookie が無効または見つからない場合、ログインページへの暗黙的なリダイレクトはありません。 そのため、匿名サービスを呼び出すことができます。

AEM Forms のシングルサインオンメカニズムを回避するには、独自にログインおよびログアウトするクライアントアプリケーションを記述します。 シングルサインオンメカニズムを回避する場合は、アプリケーションで基本認証またはカスタム認証を使用できます。

このメカニズムでは AEM Forms のシングルサインオンメカニズムが使用されないので、認証 Cookie はクライアントに書き込まれません。 ログイン資格情報は、リモートチャネルの `ChannelSet` オブジェクトに格納されます。したがって、`ChannelSet`で行う同じ`RemoteObject`の呼び出しは、これらの資格情報のコンテキストで作成されます。

### AEM Formsでのシングルサインオンの設定 {#setting-up-single-sign-on-in-aem-forms}

AEM Forms でシングルサインオンを使用するには、一元化されたログインサービスを含む Forms Workflow コンポーネントをインストールします。 ユーザーが正常にログインすると、一元化されたログインサービスはユーザーに認証 Cookie を返します。 Forms web アプリケーションに対するすべての後続のリクエストには Cookie が含まれます。Cookie が有効な場合、ユーザーは認証済みと見なされ、再度ログインする必要はありません。

### シングルサインオンを使用するクライアントアプリケーションの書き込み {#writing-a-client-application-that-uses-single-sign-on}

シングルサインオンメカニズムを利用する場合、ユーザーがクライアントアプリケーションを起動する前に、一元化されたログインサービスを使用してログインすることが想定されます。つまり、クライアントアプリケーションは、ブラウザーを介してログインしたり `ChannelSet.login` メソッドを呼び出してログインしたりはしません。

AEM Forms のシングルサインオンメカニズムを使用している場合、基本ではなくカスタム認証を使用するようにリモートエンドポイントを設定します。 そうしないと、基本認証を使用する場合、認証エラーによってブラウザーで問題が発生します。これはユーザーには見せたくありません。代わりに、アプリケーションは認証エラーを検出し、一元化されたログインサービスを使用してログインするようユーザーに指示するメッセージを表示します。

次の例に示すように、クライアントアプリケーションは、`RemoteObject`コンポーネントを使用してリモートエンドポイントを介して AEM Forms にアクセスします。

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Flex アプリケーションの実行中に新しいユーザーとしてログイン**

Flex で作成されたアプリケーションは、AEM Forms サービスに対するすべてのリクエストに認証 Cookie を含めます。パフォーマンス上の理由から、AEM Forms はリクエストのたびに cookie を検証しません。ただし、認証 Cookie が別の認証 Cookie に置き換えられた場合、AEM Forms は検知します。

例えば、クライアントアプリケーションを起動し、アプリケーションがアクティブな状態で、一元化されたログインサービスを使用してログアウトします。次に、別のユーザーとしてログインできます。別のユーザーとしてログインすると、既存の認証 Cookie が新しいユーザーの認証 Cookie に置き換えられます。

クライアントアプリケーションからの次のリクエストで、AEM Forms は cookie が変更されたことを検知し、ユーザーをログアウトします。そのため、Cookie を変更した後の最初のリクエストは失敗します。以降のリクエストはすべて、新しい cookie のコンテキストで行われるため成功します。

**ログアウト**

AEM Forms からログアウトしてセッションを無効にするには、クライアントのコンピューターから認証 Cookie を削除する必要があります。シングルサインオンの目的はユーザーが 1 回だけログインするようにすることであるため、クライアントアプリケーションで cookie が削除されることは望ましくありません。このアクションは、ユーザーを効果的にログアウトします。

そのため、クライアントアプリケーションで `RemoteObject.logout` メソッドを呼び出すと、セッションがログアウトされていないことを示すエラーメッセージがクライアントに生成されます。代わりに、ユーザーは一元化されたログインサービスを使用してログアウトして、認証 Cookie を削除できます。

**Flex アプリケーションの実行中にログアウトする**

Flex で構築されたクライアントアプリケーションを起動し、一元化されたログインサービスを使用してログアウトできます。ログアウトプロセスの一環として、認証 Cookie が削除されます。Cookie なしで、または無効な Cookie でリモート処理のリクエストが行われた場合、ユーザーセッションは無効になります。このアクションはログアウトになります。次回、クライアントアプリケーションで AEM Forms サービスに接続しようとするとき、ユーザーはログインする必要があります。

**関連項目**

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex ライブラリファイルを含める](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し {#passing-secure-documents-to-invoke-processes-using-remoting}

1 つまたは複数のドキュメントを必要とするプロセスを呼び出す際に、セキュリティで保護されたドキュメントを AEM Forms に渡すことができます。セキュリティで保護されているドキュメントを渡すことにより、ビジネス情報や機密ドキュメントを保護できます。この場合、ドキュメントとは PDF ドキュメント、XML ドキュメント、Word ドキュメントなどを指しています。セキュリティで保護されているドキュメントを許可するように AEM Forms が設定されている場合は、Flex で記述されたクライアントアプリケーションからセキュリティで保護されているドキュメントを AEM Forms に渡す必要があります（[安全なドキュメントと安全でないドキュメントを受け入れるための AEM Forms の構成](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)を参照）。

セキュリティで保護されているドキュメントを渡す場合は、シングルサインオンを使用し、*ドキュメントアップロードアプリケーションユーザー*&#x200B;の役割を持つ AEM Forms ユーザーを指定します。この役割がないと、ユーザーはセキュアなドキュメントをアップロードできません。プログラムによってユーザーに役割を割り当てることもできます（[役割と権限の管理](/help/forms/developing/users.md#managing-roles-and-permissions)を参照）。

>[!NOTE]
>新しい役割を作成し、その役割のメンバーが安全なドキュメントをアップロードできるようにする場合、ドキュメントのアップロード権限を指定する必要があります。

AEM Forms は、アップロードサーブレットに渡されたトークンを返す `getFileUploadToken` という名前の操作をサポートしています。`DocumentReference.constructRequestForUpload` メソッドには、AEM Forms への URL と `LC.FileUploadAuthenticator.getFileUploadToken` メソッドによって返されたトークンが必要です。このメソッドは、アップロードサーブレットへの呼び出しで使用される `URLRequest` オブジェクトを返します。次のコードは、このアプリケーションロジックの例を示しています。

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### セキュリティで保護されているドキュメントと保護されていないドキュメントを受け入れるための AEM Forms の設定 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

管理コンソールを使用して、ドキュメントを Flex クライアントアプリケーションから AEM Forms プロセスに渡す際に、ドキュメントをセキュリティで保護するかどうかを指定できます。デフォルトでは、AEM Forms はセキュリティで保護されたドキュメントを受け入れるように設定されています。セキュリティで保護されたドキュメントを受け入れるように AEM Forms を設定するには、次の手順を実行します。

1. 管理コンソールにログインします。
1. 「**設定**」をクリックします。
1. 「**コアシステム設定**」をクリックします。
1. 「設定」をクリックします。
1. 「 Flex アプリケーションからセキュリティで保護されていないドキュメントのアップロードを許可する」オプションの選択がオフになっていることを確認します。

>[!NOTE]
>セキュリティで保護されていないドキュメントを受け入れるように AEM Forms を設定するには、「 Flex アプリケーションからセキュリティで保護されていないドキュメントのアップロードを許可する」オプションを選択します。次に、アプリケーションまたはサービスを再起動して、設定が有効になることを確認します。

### クイックスタート：Remoting を使用してセキュリティで保護されたドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

次のコード例では、`MyApplication/EncryptDocument.` を呼び出しています。ユーザーは、ログインして、「ファイルを選択」ボタンをクリックする必要があります。このボタンは、PDF ファイルをアップロードしてプロセスを呼び出すために使用されます。つまり、ユーザーが認証されると、「ファイルを選択」ボタンが有効になります。次の図は、ユーザーが認証された後の Flex クライアントアプリケーションを示しています。Authenticated CheckBox が有効になっていることに注意してください。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

AEM Forms がセキュアなドキュメントのみをアップロードするように設定されていて、ユーザーに&#x200B;*ドキュメントアップロードアプリケーションユーザー*&#x200B;の役割がない場合、例外がスローされます。ユーザーにこの役割が割り当てられている場合は、ファイルがアップロードされ、プロセスが呼び出されます。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef’s url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**関連トピック**

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex ライブラリファイルを含める](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex で作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Remoting を使用したカスタムコンポーネントサービスの呼び出し {#invoking-custom-component-services-using-remoting}

Remoting を使用して、カスタムコンポーネント内のサービスを呼び出すことができます。 例えば、Customer サービスを含む Bank コンポーネントについて考えてみましょう。Flex で記述されたクライアントアプリケーションを使用して、Customer サービスに属する操作を呼び出すことができます。この節に関連するクイックスタートを実行する前に、Bank カスタムコンポーネントを作成する必要があります。

Customer サービスは、`createCustomer` を言う名前の操作を公開します。このディスカッションでは、Customer サービスを呼び出して顧客を作成する Flex クライアントアプリケーションの作成方法を説明します。この操作には、新規顧客を表す `com.adobe.livecycle.sample.customer.Customer` タイプの複合オブジェクトが必要です。次の図に、Customer サービスを呼び出して新しい顧客を作成するクライアントアプリケーションを示します。`createCustomer` 操作は顧客識別子の値を返します。識別子の値は「顧客識別子」テキストボックスに表示されます。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

次のテーブルに、このクライアントアプリケーションの一部であるコントロールを一覧表示します。

<table>
 <thead>
  <tr>
   <th><p>コントロール名</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>顧客の名前（名）を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>顧客の名前（姓）を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>顧客の電話番号を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>顧客の住所（番地）を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>顧客の都道府県を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>顧客の郵便番号を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>顧客の市区町村を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>新しいアカウントが属する顧客識別子の値を指定します。 このテキストボックスには、Customer サービスの <code>createCustomer</code> 操作の戻り値が入力されます。 </p></td>
  </tr>
 </tbody>
</table>

### AEM Forms の複合データタイプのマッピング {#mapping-aem-forms-complex-data-types}

一部の AEM Forms 操作では、入力値として複合データタイプが必要です。これらの複合データタイプは、操作で使用される実行時の値を定義します。例えば、Customer サービスの `createCustomer` 操作にはサービスに必要な実行時の値を含む `Customer` インスタンスが必要です。データタイプがない場合、Customer サービスは例外をスローし、操作を実行しません。

AEM Forms サービスを呼び出す際に、必要な AEM Forms データタイプにマッピングする ActionScript オブジェクトを作成します。操作に必要な複合データタイプごとに、個別の ActionScript オブジェクトを作成します。

ActionScript クラスで、AEM Forms データタイプにマッピングするために `RemoteClass` メタデータタグを使用します。例えば、Customer サービスの `createCustomer` 操作を呼び出す場合、`com.adobe.livecycle.sample.customer.Customer` データタイプにマッピングする ActionScript クラスを作成します。

次の Customer という名前の ActionScript クラスは、AEM Forms データタイプ `com.adobe.livecycle.sample.customer.Customer` にマッピングする方法を示しています。

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

AEM Forms データタイプの完全修飾データタイプがエイリアスタグに割り当てられます。

ActionScript クラスのフィールドは、AEM Forms データタイプに属するフィールドと一致します。Customer ActionScript クラスにある 6 つのフィールドは `com.adobe.livecycle.sample.customer.Customer` に属するフィールドに一致します。

>[!NOTE]
>Forms データタイプに属するフィールド名を判別する良い方法は、web ブラウザーでサービスの WSDL を表示することです。WSDL は、サービスのデータタイプと対応するデータメンバーを指定します。 Customer サービスでは、WSDL `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.` が使用されます。

Customer ActionScript クラスは、customer という名前のパッケージに属しています。AEM Forms データタイプにマッピングするすべての ActionScript クラスは、独自のパッケージに配置することをお勧めします。次の図に示すように、Flex プロジェクトの src フォルダーにフォルダーを作成し、ActionScript ファイルをそのフォルダーに配置します。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### クイックスタート：Remoting を使用した Customer カスタムサービスの呼び出し {#quick-start-invoking-the-customer-custom-service-using-remoting}

次のコード例は、Customer サービスを呼び出して新しい顧客を作成します。このコード例を実行する場合は、必ずすべてのテキストボックスに入力してください。 また、`com.adobe.livecycle.sample.customer.Customer` にマッピングする Customer.as ファイルを必ず作成してください。

>[!NOTE]
>このクイックスタートを実行する前に、Bank カスタムコンポーネントを作成してデプロイする必要があります。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**スタイルシート**

このクイックスタートには *bank.css* という名前のスタイルシートが含まれています。次のコードは、使用されるスタイルシートを表しています。

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**関連トピック**

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flex ライブラリファイルを含める](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[（AEM Forms では非推奨）AEM Forms Remoting を使用したセキュアでないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flex で作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remoting を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
