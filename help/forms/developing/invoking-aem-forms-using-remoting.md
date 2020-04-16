---
title: Invoking AEM Forms using Remoting
seo-title: Invoking AEM Forms using Remoting
description: 'null'
seo-description: 'null'
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Remotingを使用したAEM Formsの呼び出し {#invoking-aem-forms-using-remoting}

Processes created in Workbench can be invoked by using Remoting. つまり、Flexで構築されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。 この機能は、Data Servicesに基づいています。

>[!NOTE]
>
>Remotingを使用する場合は、AEM Formsサービスとは異なり、Workbenchで作成されたプロセスを呼び出すことをお勧めします。 ただし、AEM Formsサービスを直接呼び出すことは可能です。 (AEM Formsデベロッパーセンターにある「Remotingを使用したPDFドキュメントの暗号化」を参照)。

>[!NOTE]
>
>AEM Formsサービスが匿名アクセスを許可するように設定されていない場合、Flexクライアントからの要求はWebブラウザーの課題となります。 ユーザーは、ユーザー名とパスワードの資格情報を入力する必要があります。

次のAEM Formsの短時間のみ有効なプロセスは、Remotingを使 `MyApplication/EncryptDocument`用して呼び出すことができます。 (入力値や出力値など、このプロセスに関する詳細は、 [Short lived process exampleを参照](/help/forms/developing/aem-forms-processes.md))。

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Flexアプリケーションを使用してAEM Formsプロセスを呼び出すには、リモートエンドポイントが有効になっていることを確認します。 By default, a remoting endpoint is enabled when you deploy a process.

このプロセスを呼び出すと、次のアクションが実行されます。

1. 入力値として渡される、保護されていないPDFドキュメントを取得します。 このアクションは `SetValue` 操作に基づいています。入力パラメーターの名前はで、 `inDoc` そのデータタイプはです `document`。 (データ `document` タイプは、Workbench内で使用できるデータタイプです)。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。このプロセスの出力値の名前は、パスワードで暗号化さ `outDoc` れたPDFドキュメントです。 outDocのデータタイプはです `document`。
1. パスワードで暗号化されたPDFドキュメントをPDFファイルとしてローカルファイルシステムに保存します。 このアクションは `WriteDocument` 操作に基づいています。

>[!NOTE]
>
>The `MyApplication/EncryptDocument` process is not based on an existing AEM Forms process. To following along with the code examples, create a process named `MyApplication/EncryptDocument` using Workbench.

>[!NOTE]
>
>Remotingを使用した長期間有効なプロセスの呼び出しについて詳しくは、「人間中心の [長期間有効なプロセスの呼び出し」を参照してください](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

**関連トピック**

[AEM Forms Flexライブラリファイルのインクルード](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remotingでのドキュメントの処理（AEM Formsでは非推奨）](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Passing secure documents to invoke processes using Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Remotingを使用したカスタムコンポーネントサービスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Creating Flash Builder applications that perform SSO authentication using HTTP tokens](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Flexグラフコントロールでプロセスデータを表示する方法について詳しくは、「FlexグラフでのAEM Formsの [プロセスデータの表示」を参照してください](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)。

>[!NOTE]
>
>*crossdomain.xmlファイルを適切な場所に配置するようにしてください。 例えば、JBossにAEM Formsをデプロイした場合、このファイルを次の場所に配置します。&lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## AEM Forms Flexライブラリファイルのインクルード {#including-the-aem-forms-flex-library-file}

Remotingを使用してAEM Formsプロセスをプログラム的に呼び出すには、adobe-remoting-provider.swcファイルをFlexプロジェクトのクラスパスに追加します。 このSWCファイルは、次の場所にあります。

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   &lt;*install_directory*>は、AEM Formsがインストールされているディレクトリです。

**関連トピック**

[AEM Forms Remoting（AEM Formsでは非推奨）を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理（AEM Formsでは非推奨）](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## リモートでのドキュメントの処理 {#handling-documents-with-remoting}

AEM Formsで使用される、最も重要な非プリミティブJava型の1つがクラス `com.adobe.idp.Document` です。 ドキュメントは、通常、AEM Forms操作を呼び出すために必要です。 主にPDFドキュメントですが、SWF、HTML、XML、DOCファイルなど、他のドキュメントタイプを含めることができます。 (See [Passing data to AEM Forms services using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Flexで構築されたクライアントアプリケーションは、アプリケーションを直接リクエストすることはできません。ドキュメント For example, you cannot launch Adobe Reader to request a URL that produces a PDF file. Requests for document types, such as PDF and Microsoft Word documents, return a result that is a URL. It is the client’s responsibility to display the contents of the URL. ドキュメント管理サービスは、URLとコンテンツタイプの情報の生成に役立ちます。 XMLドキュメントの要求は、結果に完全なXMLドキュメントを返します。

### 入力パラメーターとしてドキュメントを渡す {#passing-a-document-as-an-input-parameter}

Flexで構築されたクライアントアプリケーションは、ドキュメントをAEM Formsプロセスに直接渡すことはできません。 代わりに、クライアントアプリケーションは、 `mx.rpc.livecycle.DocumentReference` ActionScriptクラスのインスタンスを使用して、インスタンスを必要とする操作に入力パラメーターを渡 `com.adobe.idp.Document` します。 Flexクライアントアプリケーションには、オブジェクトを設定するためのオプションがいくつか用意さ `DocumentReference` れています。

* ドキュメントがサーバー上にあり、そのファイルの場所がわかっている場合は、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_FILEに設定します。 次の例に示すように、fileRefプロパティをファイルの場所に設定します。

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* ドキュメントがサーバー上にあり、そのURLがわかっている場合は、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_URLに設定します。 Set the url property to the URL, as the following example shows:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* クライアントアプリケーションのテキスト文字列からDocumentReferenceオブジェクトを作成するには、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_INLINEに設定します。 次の例に示すように、textプロパティをオブジェクトに含めるテキストに設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* ドキュメントがサーバー上にない場合は、リモートアップロードサーブレットを使用して、ドキュメントをAEM Formsにアップロードします。 AEM Formsの新機能は、セキュリティで保護されたドキュメントをアップロードする機能です。 セキュアなドキュメントをアップロードする場合は、アプリのアップロードユーザーロールを持つ *ドキュメントを使用する必要があります* 。 このロールがないと、ユーザーは安全なロールをアップロードできません。ドキュメント セキュリティで保護されたドキュメントをアップロードするには、シングルサインオンを使用することをお勧めします。 (Remotingを使用し [てプロセスを呼び出すための安全なドキュメントの引き渡しを参照](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting))。

>[!NOTE]
安全でないドキュメントのアップロードを許可するようにAEM Formsが設定されている場合は、ドキュメントのアップロードアプリケーションのユーザーロールを持たないドキュメントを使用してアプリケーションをアップロードできます。 また、ユーザには「アップロード」ドキュメント権限もあります。 ただし、AEM Formsがセキュリティで保護されたドキュメントのみを許可するように設定されている場合は、ドキュメントに、アプリケーションのアップロードユーザーロールまたはドキュメントのアップロード権限があることを確認します。 (「安全な [ドキュメントと安全でないユーザーを受け入れるためのAEM Formsの設定」を参照](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents))。

指定したアップロードURLに対して、標準のFlashアップロード機能を使用します。 `https://SERVER:PORT/remoting/lcfileupload`. その後、タイプの入力パラメ `DocumentReference` ーターが必要な場合は常にオブジェクトを使用できます。 `Document` Remoting` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`Quick開始は、Remotingアップロードサーブレットを使用してPDFファイルをプロセスに渡 `MyApplication/EncryptDocument`します。 (AEM Forms Remoting(AEM Forms [では非推奨)を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出しを参照](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting))。

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

リモートクイック開始は、Remotingアップロードサーブレットを使用してPDFファイルをプロセスに渡 `MyApplication/EncryptDocument`します。 (AEM Forms Remoting(AEM Forms [では非推奨)を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出しを参照](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting))。

### クライアントドキュメントにアプリケーションを戻す {#passing-a-document-back-to-a-client-application}

クライアントアプリケーションは、出力パラメーターとし `mx.rpc.livecycle.DocumentReference` てインスタンスを返すサービス操作のタ `com.adobe.idp.Document` イプのオブジェクトを受け取ります。 クライアントアプリケーションはJavaではなくActionScriptオブジェクトを扱うので、JavaベースのドキュメントオブジェクトをFlexクライアントに渡すことはできません。 代わりに、サーバーはドキュメントのURLを生成し、URLをクライアントに返します。 オブジ `DocumentReference` ェクトの `referenceType` プロパティは、コンテンツがオブジ `DocumentReference` ェクト内にあるか、プロパティ内のURLから取得する必要があるかを指定 `DocumentReference.url` します。 The `DocumentReference.contentType` property specifies the type of document.

**関連トピック**

[AEM Forms Remoting（AEM Formsでは非推奨）を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Flexライブラリファイルのインクルード](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remotingを使用して、セキュアドキュメントをプロセスを呼び出すために渡す](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remotingを使用して安全でないプロセスを渡すことによる短時間のみ有効なドキュメントの呼び出し {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Flexで構築されたアプリケーションからAEM Formsプロセスを呼び出すには、次のタスクを実行します。

1. Create a `mx:RemoteObject` instance.
1. Create a `ChannelSet` instance.
1. 必要な入力値を渡します。
1. 戻り値を処理します。

>[!NOTE]
この節では、AEM Formsが安全でないドキュメントをアップロードするように設定されている場合に、AEM Formsプロセスを呼び出し、ドキュメントをアップロードする方法について説明します。 AEM Formsプロセスの呼び出し方法、セキュアドキュメントのアップロード方法、およびセキュアドキュメントと非セキュアドキュメントを受け入れるようにAEM Formsを設定する方法について詳しくは、「 [Remotingを使用してセキュアを呼び出す方法](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)」を参照してください。

**mx:RemoteObjectインスタンスの作成**

Workbenchで作成したAEM Forms `mx:RemoteObject` プロセスを呼び出すインスタンスを作成します。 インスタンスを作 `mx:RemoteObject` 成するには、次の値を指定します。

* **id:** 呼び出すプロセ `mx:RemoteObject` スを表すインスタンスの名前。
* **宛先：** 呼び出すAEM Formsプロセスの名前。 例えば、プロセスを呼び出すに `MyApplication/EncryptDocument` は、を指定しま `MyApplication/EncryptDocument`す。
* **結果：** 結果を処理するFlexメソッドの名前です。

タグ内 `mx:RemoteObject` で、プロセ `<mx:method>` スの呼び出しメソッドの名前を指定するタグを指定します。 通常、Forms呼び出しメソッドの名前はです `invoke`。

次のコード例は、プロセスを呼び出 `mx:RemoteObject` すインスタンスを作成 `MyApplication/EncryptDocument` します。

```as3
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**AEM Formsへのチャネルの作成**

クライアントアプリケーションは、次のActionScriptの例に示すように、MXMLまたはActionScriptでチャネルを指定することでAEM Formsを呼び出すことができます。 チャネルは、、、、ま `AMFChannel`たはの `SecureAMFChannel`いず `HTTPChannel`れかです `SecureHTTPChannel`。

```as3
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

インスタ `ChannelSet` ンスをイン `mx:RemoteObject` スタンスのフ `channelSet` ィールドに割り当てます（前のコード例を参照）。 一般に、メソッドの呼び出し時にチャネルの完全修飾名を指定する代わりに、インポートステートメントでメソッドクラスをインポート `ChannelSet.addChannel` します。

**入力値の受け渡し**

Workbenchで作成されたプロセスは、0個以上の入力パラメーターを受け取って、出力値を返すことができます。 クライアントアプリケーションは、AEM Formsプロセスに属 `ActionScript` するパラメーターに対応するフィールドを持つ入力パラメーターをオブジェクト内に渡します。 この名前の短時間のみ有効なプロセスには、とい `MyApplication/EncryptDocument`う名前の入力パラメーターが1つ必要で `inDoc`す。 プロセスによって公開される操作の名前は、 `invoke` （短時間のみ有効なプロセスのデフォルト名）です。 (「AEM Forms [を使用したAEM Formsの呼び出し」（AEM Formsでは非推奨）を参照](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

次のコード例は、PDFドキュメントをプロセスに渡 `MyApplication/EncryptDocument` します。

```as3
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

このコードの例では、は保護さ `pdfDocument` れていな `DocumentReference` いPDFインスタンスを含むドキュメントです。 詳しくは、「AEM Formsでの `DocumentReference`ドキュメントの [処理（AEM Formsでは廃止されています）」を参照してください](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)。

**サービスの特定のバージョンの呼び出し**

呼び出しのパラメーターマップでパラメーターを使用すると、特定のバ `_version` ージョンのFormsサービスを呼び出すことができます。 例えば、サービスのバージョン1.2を呼び出すには、次のように記述 `MyApplication/EncryptDocument` します。

```as3
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

パラメー `version` ターは、1つのピリオドを含む文字列である必要があります。 期間の左、メジャー、右、マイナーバージョンの値は整数である必要があります。 このパラメーターを指定しない場合、headアクティブバージョンが呼び出されます。

**戻り値の処理**

AEM Formsプロセスの出力パラメーターは、次の例に示すように、ActionScriptオブジェクトにデシリアライズされ、クライアントアプリケーションは、特定のパラメーターを名前で抽出します。 (プロセスの出力値 `MyApplication/EncryptDocument` には名前が付 `outDoc`きます)。

```as3
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**MyApplication/EncryptDocumentプロセスの呼び出し**

次の手順を実行するこ `MyApplication/EncryptDocument` とで、プロセスを呼び出すことができます。

1. ActionScriptまたはMXMLを使 `mx:RemoteObject` 用してインスタンスを作成します。 mx:RemoteObjectインスタンスの作成を参照してください。
1. AEM Formsと通信す `ChannelSet` るインスタンスを設定し、そのインスタンスに関連付け `mx:RemoteObject` ます。 「AEM Formsへのチャネルの作成」を参照してください。
1. ChannelSetのメソッドまたはサ `login` ービスのメソッドを呼び出して、ユ `setCredentials` ーザー識別子の値とパスワードを指定します。 (シングル [サインオンの使用を参照](invoking-aem-forms-using-remoting.md#using-single-sign-on))。
1. プロセスに渡 `mx.rpc.livecycle.DocumentReference` す、保護されていないPDFドキュメントを使用してインスタンスを設 `MyApplication/EncryptDocument` 定します。 (入力パラ [メーターとしてドキュメントを渡すを参照](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter))。
1. インスタンスのドキュメントを呼び出して、PDF `mx:RemoteObject` メソッドを暗号化 `invoke` します。 入力パラメ `Object` ーター（保護されていないPDFパラメーター）を含むドキュメントを渡します。 詳しくは、入力値の受け渡しを参照してください。
1. プロセスから返される、パスワードで暗号化されたPDFドキュメントを取得します。 戻り値の処理を参照してください。

[クイック開始:AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Flexで構築されたクライアントアプリケーションの認証 {#authenticating-client-applications-built-with-flex}

AEM Forms User ManagerでFlexアプリケーションからリモート要求を認証する方法はいくつかあります。例えば、中央ログインサービスを通じたAEM Formsのシングルサインオン、基本認証、カスタム認証などです。 シングルサインオンと匿名アクセスのどちらも有効になっていない場合、リモート処理の要求は基本認証（デフォルト）またはカスタム認証のいずれかになります。

基本認証は、Webアプリケーションコンテナの標準のJ2EE基本認証に依存します。 基本認証の場合、HTTP 401エラーが発生するとブラウザーのチャレンジが発生します。 つまり、RemoteObjectを使用してFormsアプリケーションに接続しようとし、Flexアプリケーションからまだログインしていない場合は、ユーザー名とパスワードの入力を求めるプロンプトが表示されます。

カスタム認証の場合、サーバーは認証が必要であることを示すエラーをクライアントに送信します。

>[!NOTE]
HTTPトークンを使用した認証の実行について詳しくは、HTTPトークンを使用し [てSSO認証を実行するFlash Builderアプリケーションの作成を参照してください](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)。

### カスタム認証の使用 {#using-custom-authentication}

管理コンソールでカスタム認証を有効にするには、リモートエンドポイントで認証方法を「基本」から「カスタム」に変更します。 カスタム認証を使用する場合、クライアントアプリケーションは、ログ `ChannelSet.login` インするメソッドとログアウトするメソッド `ChannelSet.logout` を呼び出します。

>[!NOTE]
以前のリリースのAEM Formsでは、メソッドを呼び出すことで、証明書を宛先に送信し `RemoteObject.setCredentials` ました。 メソッ `setCredentials` ドは、コンポーネントが最初にサーバーへの接続を試みるまで、実際にはサーバーに資格情報を渡しませんでした。 したがって、コンポーネントが障害イベントを発行した場合、認証エラーや他の理由で障害が発生したかどうかは不明です。 メソッド `ChannelSet.login` を呼び出すと、サーバーに接続され、認証の問題をすぐに処理できるようになります。 この方法は引き続き使用でき `setCredentials` ますが、使用することをお勧めし `ChannelSet.login` ます。

複数の宛先で同じチャネルを使用し、対応するChannelSetオブジェクトを使用できるので、1つの宛先にログインすると、同じチャネルまたはチャネルを使用する他の宛先にログインします。 2つのコンポーネントが同じChannelSetオブジェクトに異なる資格情報を適用する場合、最後に適用された資格情報が使用されます。 複数のコンポーネントが同じ認証済みChannelSetオブジェクトを使用する場合、メソッドを呼び出すと、す `logout` べてのコンポーネントが宛先からログアウトされます。

次の例では、メソッドとメソッド `ChannelSet.login` をRemoteObject `ChannelSet.logout` コントロールと共に使用しています。 このアプリケーションは、次のアクションを実行します。

* コンポーネント `ChannelSet` で使用される `creationComplete` チャネルを表すオブジェクトをハンドラー内に作成し `RemoteObject` ます
* ボタンのクリックイベントに応答して関数を呼び出す `ROLogin` ことで、サーバーに秘密鍵証明書を渡します。
* RemoteObjectコンポーネントを使用して、ボタンのクリックイベントに応答して文字列をサーバーに送信します。 サーバーは同じ文字列をRemoteObjectコンポーネントに返します
* RemoteObjectコンポーネントの結果イベントを使用して、TextAreaコントロールに文字列を表示します
* ボタンのクリックイベントに応じて関数を呼び出 `ROLogout` し、サーバーからログアウトします。

```as3
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

メソッド `login` およびメ `logout` ソッドは、AsyncTokenオブジェクトを返します。 呼び出しが成功した場合に処理する結果イベントと、失敗した場合に処理するフォルトイベントのAsyncTokenオブジェクトにイベントハンドラーを割り当てます。

### シングルサインオンの使用 {#using-single-sign-on}

AEM Formsユーザーは、複数のAEM Forms Webアプリケーションに接続して、1つのアプリケーションをタスクできます。 ユーザーがWebアプリケーション間を移動する際に、各Webアプリケーションに個別にログインする必要はありません。 AEM Formsのシングルサインオンメカニズムを使用すると、ユーザーは一度ログインし、任意のAEM Forms Webアプリケーションにアクセスできます。 AEM Forms開発者はAEM Formsで使用するクライアントアプリケーションを作成できるので、シングルサインオンのメカニズムも活用できる必要があります。

各AEM Forms Webアプリケーションは、独自のWebアーカイブ(WAR)ファイルにパッケージ化され、その後、エンタープライズアーカイブ(EAR)ファイルの一部としてパッケージ化されます。 アプリケーションサーバーでは異なるWebアプリケーション間でのセッションデータの共有が許可されないので、AEM Formsでは認証情報の保存にHTTP cookieを使用します。 認証cookieを使用すると、ユーザーはFormsアプリケーションにログインし、他のAEM Forms Webアプリケーションに接続できます。 この方法は、シングルサインオンと呼ばれます。

AEM Forms開発者は、フォームガイド（非推奨）の機能を拡張し、Workspaceをカスタマイズするためのクライアントアプリケーションを作成します。 例えば、Workspaceアプリケーションでプロセスを開始できます。 次に、クライアントアプリケーションは、リモートエンドポイントを使用してFormsサービスからデータを取得します。

AEM Forms Remoting（AEM Formsでは非推奨）を使用してAEM Formsサービスが呼び出されると、クライアントアプリケーションは要求の一部として認証cookieを渡します。 ユーザーは既に認証済みなので、クライアントアプリケーションからAEM Formsサービスに接続するために追加のログインは必要ありません。

>[!NOTE]
cookieが無効な場合や存在しない場合、ログインページへの暗黙のリダイレクトは行われません。 したがって、匿名サービスを呼び出すことができます。

AEM Formsのシングルサインオンメカニズムを回避するには、ログインしてログアウトするクライアントアプリケーションを独自に記述します。 シングルサインオンメカニズムを使用しない場合は、アプリケーションで基本認証またはカスタム認証を使用できます。

このメカニズムではAEM Formsのシングルサインオンメカニズムを使用しないので、認証cookieはクライアントに書き込まれません。 ログイン資格情報は、リモートチャネルの `ChannelSet` オブジェクトに保存されます。 したがって、同じ `RemoteObject` 方法で行った呼び出しは、 `ChannelSet` それらの資格情報のコンテキストで行われます。

### AEM Formsでのシングルサインオンの設定 {#setting-up-single-sign-on-in-aem-forms}

AEM Formsでシングルサインオンを使用するには、中央のログインサービスを含むformsワークフローコンポーネントをインストールします。 ユーザーが正常にログインすると、中央管理ログインサービスは認証cookieをユーザーに返します。 Forms Webアプリケーションに対する以降のリクエストには、すべてcookieが含まれます。 Cookieが有効な場合、ユーザーは認証済みと見なされ、再度ログインする必要はありません。

### シングルサインオンを使用するクライアントアプリケーションの作成 {#writing-a-client-application-that-uses-single-sign-on}

シングルサインオンのメカニズムを利用する場合は、クライアントアプリケーションを起動する前に、中央のログインサービスを使用してログインする必要があります。 つまり、クライアントアプリケーションは、ブラウザーを使用したり、メソッドを呼び出したりしてログインすることはあ `ChannelSet.login` りません。

AEM Formsのシングルサインオンメカニズムを使用する場合は、基本ではなくカスタム認証を使用するようにリモートエンドポイントを設定します。 それ以外の場合は、基本認証を使用すると、認証エラーが発生するとブラウザーのチャレンジが発生し、ユーザーに表示されないようにします。 代わりに、アプリケーションは認証エラーを検出し、中央のログインサービスを使用してログインするようにユーザーに指示するメッセージを表示します。

クライアントアプリケーションは、次の例に示すように、コンポーネントを使用してリモートエ `RemoteObject` ンドポイントを通じてAEM Formsにアクセスします。

```as3
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

**Flexアプリケーションの実行中に新しいユーザーとしてログインする**

Flexで構築されたアプリケーションには、AEM Formsサービスへのすべての要求を含む認証cookieが含まれます。 パフォーマンス上の理由から、AEM Formsではリクエストのたびにcookieが検証されません。 ただし、AEM Formsは、認証cookieが別の認証cookieに置き換えられた場合を検出します。

例えば、クライアント開始をアクティブにしている間は、中央のログインサービスを使用してログアウトします。 次に、別のユーザーとしてログインできます。 別のユーザーとしてログインすると、既存の認証cookieが新しいユーザーの認証cookieに置き換えられます。

クライアントアプリケーションからの次の要求時に、AEM Formsはcookieが変更されたことを検出し、ユーザーをログアウトします。 したがって、cookieの変更後の最初のリクエストは失敗します。 以降のすべてのリクエストは、新しいcookieのコンテキストで行われ、成功します。

**ログアウト**

AEM Formsからログアウトし、セッションを無効にするには、認証cookieをクライアントのコンピューターから削除する必要があります。 シングルサインオンの目的は、ユーザーが1回ログインできるようにすることであるので、クライアントアプリケーションがcookieを削除しないようにする必要があります。 この操作により、ユーザーが効果的にログアウトされます。

したがって、クライアントア `RemoteObject.logout` プリケーションでメソッドを呼び出すと、クライアント上で、セッションがログアウトされないことを示すエラーメッセージが生成されます。 代わりに、ユーザーは中央のログインサービスを使用して、認証cookieをログアウトおよび削除できます。

**Flexアプリケーションの実行中にログアウトする**

Flexで構築されたクライアント開始をし、中央のログインサービスを使用してログアウトできます。 ログアウトプロセスの一環として、認証cookieが削除されます。 Cookieなし、または無効なCookieを使用してリモートリクエストが行われた場合、ユーザーセッションは無効になります。 このアクションは、実際にはログアウトされます。 次にクライアントアプリケーションがAEM Formsサービスへの接続を試みると、ユーザーはログインを要求されます。

**関連トピック**

[AEM Forms Remoting（AEM Formsでは非推奨）を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理（AEM Formsでは非推奨）](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルのインクルード](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Remotingを使用して、セキュアドキュメントをプロセスを呼び出すために渡す](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Remotingを使用して、セキュアドキュメントをプロセスを呼び出すために渡す {#passing-secure-documents-to-invoke-processes-using-remoting}

1つ以上のドキュメントを必要とするプロセスを呼び出すときに、セキュリティで保護されたドキュメントをAEM Formsに渡すことができます。 安全なドキュメントを渡すことで、ビジネス情報や機密ドキュメントを保護できます。 この場合、ドキュメントはPDFドキュメント、XMLドキュメント、Wordドキュメントなどを参照できます。 AEM Formsがセキュリティで保護されたドキュメントを許可するように設定されている場合は、Flexで記述されたクライアントアプリケーションからAEM Formsにセキュリティで保護されたドキュメントを渡す必要があります。 (「安全な [ドキュメントと安全でないユーザーを受け入れるためのAEM Formsの設定](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)」を参照)。

安全なドキュメントを渡す場合は、シングルサインオンを使用し、 *ドキュメントアップロードアプリのユーザ* ーロールを持つAEM formsユーザーを指定します。 このロールがないと、ユーザーは安全なロールをアップロードできません。ドキュメント ユーザーにロールをプログラムによって割り当てることができます。 (ロールと [権限の管理を参照](/help/forms/developing/users.md#managing-roles-and-permissions))。

>[!NOTE]
新しいロールを作成し、そのロールのメンバーが安全なドキュメントをアップロードする場合は、ドキュメントのアップロード権限を必ず指定します。

AEM Formsは、アップロードサーブレットに渡 `getFileUploadToken` されるトークンを返すという名前の操作をサポートします。 このメ `DocumentReference.constructRequestForUpload` ソッドには、AEM FormsへのURLと、このメソッドから返されるトークンが必要 `LC.FileUploadAuthenticator.getFileUploadToken` です。 このメソッドは、アップロ `URLRequest` ードサーブレットへの呼び出しで使用されるオブジェクトを返します。 次のコードは、このアプリケーションロジックを示しています。

```as3
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

）

### 安全なドキュメントと安全でないユーザーを受け入れるようにAEM Formsを設定する {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

管理コンソールを使用して、FlexクライアントドキュメントからAEM Formsプロセスにドキュメントを渡す際に、アプリケーションをセキュリティで保護するかどうかを指定できます。 デフォルトでは、AEM Formsはセキュリティで保護されたドキュメントを受け入れます。 次の手順を実行して、セキュリティで保護されたドキュメントを受け入れるようにAEM Formsを設定できます。

1. 管理コンソールにログインします。
1. 「設定」をク **リックしま**&#x200B;す。
1. 「コアシス **テム設定」をクリックします。**
1. 「設定」をクリックします。
1. 「Flexアプリケーションからの保護されていないドキュメントのアップロードを許可する」オプションが選択されていないことを確認します。

>[!NOTE]
AEM Formsでセキュリティで保護されていないドキュメントを受け入れるように設定するには、「セキュリティで保護されていないドキュメントのアップロードをFlexアプリケーションから許可する」オプションを選択します。 次に、アプリケーションまたはサービスを再起動し、設定が有効になることを確認します。

### クイック開始:Remotingを使用して安全なプロセスを渡すことによる短時間のみ有効なドキュメントの呼び出し {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

次のコード例は、 `MyApplication/EncryptDocument.`Aユーザーがログインして、PDFファイルのアップロードとプロセスの呼び出しに使用される「Select File」ボタンをクリックする必要がある場合を呼び出します。 つまり、ユーザーが認証されると、「Select File」ボタンが有効になります。 次の図に、ユーザーが認証された後のFlexクライアントアプリケーションを示します。 認証済みのCheckBoxが有効になっていることに注意してください。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

安全なドキュメントのアップロードのみを許可するようにAEM Formsが設定され、ドキュメントに *のアップロードのユーザーロールがない場合* 、例外が発生します。 ユーザーがこの役割を持っている場合、ファイルがアップロードされ、プロセスが呼び出されます。

```as3
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

[AEM Forms Remoting（AEM Formsでは非推奨）を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理（AEM Formsでは非推奨）](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルのインクルード](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Remotingを使用したカスタムコンポーネントサービスの呼び出し {#invoking-custom-component-services-using-remoting}

Remotingを使用して、カスタムコンポーネント内のサービスを呼び出すことができます。 例えば、Customerサービスを含む銀行コンポーネントについて考えてみましょう。 Flexで記述されたクライアントアプリケーションを使用して、Customerサービスに属する操作を呼び出すことができます。 このセクションに関連付けられたクイック開始を実行する前に、銀行カスタムコンポーネントを作成する必要があります。

Customerサービスは、という名前の操作を公開しま `createCustomer`す。 ここでは、Customerサービスを呼び出して顧客を作成するFlexクライアントアプリケーションの作成方法を説明します。 この操作には、新しい顧客を表すタイプの複雑 `com.adobe.livecycle.sample.customer.Customer` なオブジェクトが必要です。 次の図に、Customerサービスを呼び出し、新しい顧客を作成するクライアントアプリケーションを示します。 この操 `createCustomer` 作は顧客識別子の値を返します。 識別子の値は、「顧客識別子」テキストボックスに表示されます。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

次の表に、このクライアントリストの一部であるコントロールを示します。

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
   <td><p>顧客の名を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>顧客の姓を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>顧客の電話番号を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>顧客の住所名を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>顧客の州を指定します。 </p></td>
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
   <td><p>新しいアカウントが属する顧客識別子の値を指定します。 このテキストボックスには、Customerサービスの操作の戻り値が入力され <code>createCustomer</code> ます。 </p></td>
  </tr>
 </tbody>
</table>

### AEM Forms複合データ型のマッピング {#mapping-aem-forms-complex-data-types}

一部のAEM Forms操作では、入力値として複雑なデータ型が必要です。 これらの複雑なデータ型は、操作で使用される実行時の値を定義します。 例えば、Customerサービスの操作には、サ `createCustomer` ービスに必要な実 `Customer` 行時の値を含むインスタンスが必要です。 複合型がない場合、Customerサービスは例外をスローし、操作を実行しません。

AEM Formsサービスを呼び出す場合は、必要なAEM Forms複合型にマップするActionScriptオブジェクトを作成します。 操作に必要な複雑なデータ型ごとに、個別のActionScriptオブジェクトを作成します。

ActionScriptクラスで、メタデータタグを使 `RemoteClass` 用してAEM Forms複合型にマップします。 例えば、Customerサービスの操作を呼び出す場合、デ `createCustomer` ータ型にマップするActionScriptクラスを作成 `com.adobe.livecycle.sample.customer.Customer` します。

次に示すCustomerというActionScriptクラスは、AEM Formsデータ型にマップする方法を示していま `com.adobe.livecycle.sample.customer.Customer`す。

```as3
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

AEM Forms複合型の完全修飾データ型がエイリアスタグに割り当てられます。

ActionScriptクラスのフィールドは、AEM Forms複合型に属するフィールドと一致します。 Customer ActionScriptクラス内の6つのフィールドは、に属するフィールドと一致しま `com.adobe.livecycle.sample.customer.Customer`す。

>[!NOTE]
Forms複合型に属するフィールド名を判断する良い方法は、WebブラウザーでサービスのWSDLを表示することです。 WSDLは、サービスの複合型と対応するデータメンバーを指定します。 次のWSDLがCustomerサービスで使用されます。 `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

Customer ActionScriptクラスは、customerという名前のパッケージに属します。 複雑なAEM Formsデータ型にマップするすべてのActionScriptクラスを、それぞれのパッケージに配置することをお勧めします。 次の図に示すように、Flexプロジェクトのsrcフォルダーにフォルダーを作成し、そのフォルダーにActionScriptファイルを配置します。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### クイック開始:Remotingを使用したCustomerカスタムサービスの呼び出し {#quick-start-invoking-the-customer-custom-service-using-remoting}

次のコード例は、Customerサービスを呼び出し、新しい顧客を作成します。 このコード例を実行する場合は、必ずすべてのテキストボックスに入力してください。 また、にマップするCustomer.asファイルを必ず作成してくださ `com.adobe.livecycle.sample.customer.Customer`い。

>[!NOTE]
このクイック開始を実行する前に、Bankカスタムコンポーネントを作成し、導入する必要があります。

```as3
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

このクイック開始には、 *bank.cssという名前のスタイルシートが含まれています*。 次のコードは、使用されるスタイルシートを表します。

```as3
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

[AEM Forms Remoting（AEM Formsでは非推奨）を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理（AEM Formsでは非推奨）](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルのインクルード](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting（AEM Formsでは非推奨）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Remotingを使用して、セキュアドキュメントをプロセスを呼び出すために渡す](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
