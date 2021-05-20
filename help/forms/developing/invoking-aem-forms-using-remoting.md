---
title: リモートを使用したAEM Formsの呼び出し
seo-title: リモートを使用したAEM Formsの呼び出し
description: Remotingを使用してAEM Formsプロセスを呼び出し、Workbenchで作成されたプロセスを呼び出します。 Flexで構築されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。
seo-description: Remotingを使用してAEM Formsプロセスを呼び出し、Workbenchで作成されたプロセスを呼び出します。 Flexで構築されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4661'
ht-degree: 1%

---

# リモート{#invoking-aem-forms-using-remoting}を使用したAEM Formsの呼び出し

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Workbenchで作成されたプロセスは、Remotingを使用して呼び出すことができます。 つまり、Flexで構築されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。 この機能は、データサービスに基づいています。

>[!NOTE]
>
>リモート処理を使用する場合は、AEM Formsサービスとは異なり、Workbenchで作成されたプロセスを呼び出すことをお勧めします。 ただし、AEM Formsサービスを直接呼び出すことはできます。 ( AEM Formsデベロッパーセンターにある「 Remotingを使用したPDFドキュメントの暗号化」を参照)。

>[!NOTE]
>
>AEM Formsサービスが匿名アクセスを許可するように設定されていない場合、FlexクライアントからのリクエストによってWebブラウザーの課題が生じます。 ユーザーは、ユーザー名とパスワードの資格情報を入力する必要があります。

次のAEM Formsの短時間のみ有効なプロセス(`MyApplication/EncryptDocument`)は、リモート処理を使用して呼び出すことができます。 （このプロセスの入出力値など、このプロセスについて詳しくは、「[短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md)」を参照してください）。

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Flexアプリケーションを使用してAEM Formsプロセスを呼び出すには、リモートエンドポイントが有効になっていることを確認します。 プロセスをデプロイすると、デフォルトでリモートエンドポイントが有効になります。

このプロセスを呼び出すと、次のアクションが実行されます。

1. 入力値として渡された、保護されていないPDFドキュメントを取得します。 このアクションは `SetValue` 操作に基づいています。入力パラメーターの名前は`inDoc`で、そのデータタイプは`document`です。 （`document`データ型は、Workbench内で使用できるデータ型です）。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。このプロセスの出力値の名前は`outDoc`で、パスワードで暗号化されたPDFドキュメントを表します。 outDocのデータ型は`document`です。
1. パスワードで暗号化されたPDFドキュメントをPDFファイルとしてローカルファイルシステムに保存します。 このアクションは `WriteDocument` 操作に基づいています。

>[!NOTE]
>
>`MyApplication/EncryptDocument`プロセスは、既存のAEM Formsプロセスに基づいていません。 コード例に従って、Workbenchを使用して`MyApplication/EncryptDocument`という名前のプロセスを作成します。

>[!NOTE]
>
>リモート処理を使用して長期間有効なプロセスを呼び出す方法について詳しくは、[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください。

**関連トピック**

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remotingでのドキュメントの処理(AEM formsでは非推奨)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[リモート処理を使用したカスタムコンポーネントサービスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[HTTPトークンを使用したSSO認証を実行するFlash Builder・アプリケーションの作成](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Flexグラフコントロールにプロセスデータを表示する方法について詳しくは、「[FlexグラフでのAEM Formsプロセスデータの表示](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html)」を参照してください。

>[!NOTE]
>
>*crossdomain.xmlファイルを適切な場所に配置するようにしてください。例えば、JBossにAEM Formsをデプロイした場合は、次の場所にこのファイルを配置します。&lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## AEM Forms Flexライブラリファイル{#including-the-aem-forms-flex-library-file}を含める

Remotingを使用してAEM Formsプロセスをプログラムで呼び出すには、adobe-remoting-provider.swcファイルをFlexプロジェクトのクラスパスに追加します。 このSWCファイルは次の場所にあります。

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   ここで、&lt;*install_directory*&#x200B;は、AEM Formsがインストールされているディレクトリです。

**関連トピック**

[(AEM formsでは非推奨)AEM Forms Remotingを使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理(AEM formsでは非推奨)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## リモート処理{#handling-documents-with-remoting}でのドキュメントの処理

AEM Formsで使用される非プリミティブJava型のうち、最も重要なものの1つは`com.adobe.idp.Document`クラスです。 ドキュメントは、通常、AEM Forms操作を呼び出すために必要です。 主にPDFドキュメントですが、SWF、HTML、XML、DOCファイルなど、他のドキュメントタイプを含めることができます。 ([Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)を使用してAEM Formsにデータを渡すを参照)。

Flexで構築されたクライアントアプリケーションは、ドキュメントを直接要求できません。 例えば、Adobe Readerを起動してPDFファイルを生成するURLを要求することはできません。 PDFやMicrosoft Wordドキュメントなどのドキュメントタイプに対する要求では、URLを返します。 URLのコンテンツを表示するのはクライアントの責任です。 Document Managementサービスは、URLおよびコンテンツタイプ情報の生成に役立ちます。 XMLドキュメントのリクエストは、結果内の完全なXMLドキュメントを返します。

### ドキュメントを入力パラメーター{#passing-a-document-as-an-input-parameter}として渡す

Flexで構築されたクライアントアプリケーションは、ドキュメントをAEM Formsプロセスに直接渡すことはできません。 代わりに、クライアントアプリケーションは`mx.rpc.livecycle.DocumentReference`ActionScriptクラスのインスタンスを使用して、`com.adobe.idp.Document`インスタンスを必要とする操作に入力パラメーターを渡します。 Flexクライアントアプリケーションには、`DocumentReference`オブジェクトを設定するためのオプションがいくつか用意されています。

* ドキュメントがサーバー上にあり、そのファイルの場所がわかっている場合は、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_FILEに設定します。 次の例に示すように、 fileRefプロパティをファイルの場所に設定します。

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* ドキュメントがサーバー上にあり、そのURLがわかっている場合は、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_URLに設定します。 次の例に示すように、urlプロパティをURLに設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* クライアントアプリケーションのテキスト文字列からDocumentReferenceオブジェクトを作成するには、DocumentReferenceオブジェクトのreferenceTypeプロパティをREF_TYPE_INLINEに設定します。 次の例に示すように、 textプロパティを、オブジェクトに含めるテキストに設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* ドキュメントがサーバー上にない場合は、リモートアップロードサーブレットを使用して、ドキュメントをAEM Formsにアップロードします。 AEM Formsの新機能は、セキュリティで保護されたドキュメントをアップロードする機能です。 安全なドキュメントをアップロードする場合は、*Document Upload Application User*&#x200B;の役割を持つユーザーを使用する必要があります。 このロールがないと、ユーザーは保護されたドキュメントをアップロードできません。 セキュリティで保護されたドキュメントをアップロードする場合は、シングルサインオンを使用することをお勧めします。 （[リモート処理を使用してプロセスを呼び出すための保護されたドキュメントの引き渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)を参照）。

>[!NOTE]
安全でないドキュメントのアップロードをAEM Formsで許可するように設定されている場合は、「ドキュメントのアップロードアプリケーションユーザー」の役割を持たないユーザーを使用してドキュメントをアップロードできます。 ユーザーは、ドキュメントのアップロード権限を持つこともできます。 ただし、AEM Formsが保護されたドキュメントのみを許可するように設定されている場合は、そのユーザーに「ドキュメントのアップロードアプリケーションユーザー」ロールまたは「ドキュメントのアップロード」権限があることを確認してください。 ([安全なドキュメントと安全でないドキュメントを受け入れるようにAEM Formsを設定する](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)を参照してください。

指定したアップロードURLには、標準のFlashアップロード機能を使用します。`https://SERVER:PORT/remoting/lcfileupload`. その後、`Document`型の入力パラメーターが必要な場合は常に、`DocumentReference`オブジェクトを使用できます
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`リモート処理クイックスタートは、リモート処理アップロードサーブレットを使用してPDFファイルを`MyApplication/EncryptDocument`プロセスに渡します。 ([AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)を使用して保護されていないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出しを参照)。

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

リモート処理クイックスタートは、リモート処理アップロードサーブレットを使用してPDFファイルを`MyApplication/EncryptDocument`プロセスに渡します。 ([AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)を使用して保護されていないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出しを参照)。

### クライアントアプリケーションにドキュメントを渡す{#passing-a-document-back-to-a-client-application}

クライアントアプリケーションは、`com.adobe.idp.Document`インスタンスを出力パラメーターとして返すサービス操作のタイプ`mx.rpc.livecycle.DocumentReference`のオブジェクトを受け取ります。 クライアントアプリケーションはJavaではなくActionScriptオブジェクトを扱うので、JavaベースのDocumentオブジェクトをFlexクライアントに渡すことはできません。 代わりに、サーバーはドキュメントのURLを生成し、そのURLをクライアントに渡します。 `DocumentReference`オブジェクトの`referenceType`プロパティは、コンテンツが`DocumentReference`オブジェクトに含まれるか、`DocumentReference.url`プロパティのURLから取得する必要があるかを指定します。 `DocumentReference.contentType`プロパティはドキュメントの種類を指定します。

**関連トピック**

[(AEM formsでは非推奨)AEM Forms Remotingを使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## リモート処理{#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}を使用して保護されていないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し

Flexで構築されたアプリケーションからAEM Formsプロセスを呼び出すには、次のタスクを実行します。

1. `mx:RemoteObject`インスタンスを作成します。
1. `ChannelSet`インスタンスを作成します。
1. 必要な入力値を渡します。
1. 戻り値を処理します。

>[!NOTE]
この節では、安全でないドキュメントをアップロードするようにAEM Formsが設定されている場合に、AEM Formsプロセスを呼び出してドキュメントをアップロードする方法について説明します。 AEM Formsプロセスを呼び出し、保護されたドキュメントをアップロードする方法、および保護されたドキュメントと保護されていないドキュメントを受け入れるようにAEM Formsを設定する方法について詳しくは、[Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)を使用して保護されたドキュメントを渡すを参照してください。

**mx:RemoteObjectインスタンスの作成**

`mx:RemoteObject`インスタンスを作成して、Workbenchで作成したAEM Formsプロセスを呼び出します。 `mx:RemoteObject`インスタンスを作成するには、次の値を指定します。

* **id:** 呼び出すプロ `mx:RemoteObject` セスを表すインスタンスの名前。
* **destination:** 呼び出すAEM Formsプロセスの名前。例えば、`MyApplication/EncryptDocument`プロセスを呼び出すには、`MyApplication/EncryptDocument`と指定します。
* **result:** 結果を処理するFlexメソッドの名前。

`mx:RemoteObject`タグ内で、プロセスの呼び出しメソッドの名前を指定する`<mx:method>`タグを指定します。 通常、Forms呼び出しメソッドの名前は`invoke`です。

次のコード例では、`MyApplication/EncryptDocument`プロセスを呼び出す`mx:RemoteObject`インスタンスを作成します。

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**AEM Formsへのチャネルの作成**

クライアントアプリケーションは、次のActionScript例に示すように、MXMLまたはActionScriptでチャネルを指定することで、AEM Formsを呼び出すことができます。 チャネルは、`AMFChannel`、`SecureAMFChannel`、`HTTPChannel`または`SecureHTTPChannel`にする必要があります。

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

`ChannelSet`インスタンスを`mx:RemoteObject`インスタンスの`channelSet`フィールドに割り当てます（前のコードの例で示したように）。 通常、`ChannelSet.addChannel`メソッドを呼び出す際に完全修飾名を指定するのではなく、import文でchannelクラスを読み込みます。

**入力値を渡す**

Workbenchで作成されたプロセスは、0個以上の入力パラメーターを受け取り、出力値を返すことができます。 クライアントアプリケーションは、AEM Formsプロセスに属するパラメーターに対応するフィールドを持つ`ActionScript`オブジェクト内に入力パラメーターを渡します。 `MyApplication/EncryptDocument`という短時間のみ有効なプロセスには、`inDoc`という名前の1つの入力パラメーターが必要です。 プロセスによって公開される操作の名前は`invoke`（短時間のみ有効なプロセスのデフォルト名）です。 (「[(AEM formsでは非推奨)AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)を使用したAEM Formsの呼び出し」を参照)。

次のコードの例では、PDFドキュメントを`MyApplication/EncryptDocument`プロセスに渡します。

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

このコード例では、`pdfDocument`は保護されていないPDFドキュメントを含む`DocumentReference`インスタンスです。 `DocumentReference`について詳しくは、「 [でのドキュメントの処理(AEM formsでは非推奨) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting) 」を参照してください。

**特定のバージョンのサービスの呼び出し**

呼び出しのパラメーターマップで`_version`パラメーターを使用して、特定のバージョンのFormsサービスを呼び出すことができます。 例えば、`MyApplication/EncryptDocument`サービスのバージョン1.2を呼び出すには、次のようにします。

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

`version`パラメーターは、1つのピリオドを含む文字列にする必要があります。 期間の左、メジャー、右、マイナーの各バージョンの値は整数にする必要があります。 このパラメーターを指定しない場合、headのアクティブなバージョンが呼び出されます。

**戻り値の処理**

AEM Formsプロセスの出力パラメーターは、ActionScriptオブジェクトに逆シリアル化され、クライアントアプリケーションは、次の例に示すように、名前で特定のパラメーターを抽出します。 （`MyApplication/EncryptDocument`プロセスの出力値は`outDoc`という名前です）。

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**MyApplication/EncryptDocumentプロセスの呼び出し**

`MyApplication/EncryptDocument`プロセスを呼び出すには、次の手順を実行します。

1. `mx:RemoteObject`インスタンスをActionScriptまたはMXMLを使用して作成します。 mx:RemoteObjectインスタンスの作成を参照してください。
1. AEM Formsと通信する`ChannelSet`インスタンスを設定し、`mx:RemoteObject`インスタンスに関連付けます。 詳しくは、 AEM Formsへのチャネルの作成を参照してください。
1. ChannelSetの`login`メソッドまたはサービスの`setCredentials`メソッドを呼び出して、ユーザー識別子の値とパスワードを指定します。 （[シングルサインオンの使用](invoking-aem-forms-using-remoting.md#using-single-sign-on)を参照）。
1. `MyApplication/EncryptDocument`プロセスに渡す保護されていないPDFドキュメントを`mx.rpc.livecycle.DocumentReference`インスタンスに設定します。 （[ドキュメントを入力パラメーターとして渡す](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter)を参照）。
1. `mx:RemoteObject`インスタンスの`invoke`メソッドを呼び出して、PDFドキュメントを暗号化します。 入力パラメーター（保護されていないPDFドキュメント）を含む`Object`を渡します。 入力値を渡すを参照してください。
1. プロセスから返された、パスワードで暗号化されたPDFドキュメントを取得します。 戻り値の処理を参照してください。

[クイックスタート：(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Flex {#authenticating-client-applications-built-with-flex}で構築されたクライアントアプリケーションの認証

AEM forms User ManagerでFlexアプリケーションからRemoting要求を認証する方法はいくつかあります。これには、中央のログインサービスを介したAEM Formsのシングルサインオン、基本認証、カスタム認証が含まれます。 シングルサインオンも匿名アクセスも有効になっていない場合、リモート処理リクエストは、基本認証（デフォルト）とカスタム認証のどちらにもなります。

基本認証は、Webアプリケーションコンテナからの標準J2EE基本認証に基づいています。 基本認証の場合、HTTP 401エラーが発生すると、ブラウザーの課題が発生します。 つまり、RemoteObjectを使用してFormsアプリケーションに接続しようとし、Flexアプリケーションからまだログインしていない場合、ブラウザーには、ユーザー名とパスワードの入力が求められます。

カスタム認証の場合、サーバーは認証が必要であることを示すエラーをクライアントに送信します。

>[!NOTE]
HTTPトークンを使用したFlash Builderの実行については、[HTTPトークン](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)を使用したSSO認証を実行する認証アプリケーションの作成を参照してください。

### カスタム認証{#using-custom-authentication}の使用

管理コンソールでカスタム認証を有効にするには、リモートエンドポイントで認証方法を「基本」から「カスタム」に変更します。 カスタム認証を使用する場合、クライアントアプリケーションは`ChannelSet.login`メソッドを呼び出してログインし、`ChannelSet.logout`メソッドを呼び出してログアウトします。

>[!NOTE]
以前のリリースのAEM Formsでは、 `RemoteObject.setCredentials`メソッドを呼び出して資格情報を宛先に送信しました。 `setCredentials`メソッドは、コンポーネントが最初にサーバーに接続を試みるまで、資格情報を実際にサーバーに渡しませんでした。 したがって、コンポーネントが障害イベントを発行した場合、その障害が認証エラーまたは別の理由で発生したかどうかを確認することはできません。 `ChannelSet.login`メソッドは、呼び出し時にサーバーに接続し、認証の問題を直ちに処理できるようにします。 `setCredentials`メソッドは引き続き使用できますが、`ChannelSet.login`メソッドを使用することをお勧めします。

複数の宛先で同じチャネルと対応するChannelSetオブジェクトを使用できるので、1つの宛先にログインすると、同じチャネルを使用する他の宛先にユーザーがログインします。 2つのコンポーネントが同じChannelSetオブジェクトに異なる資格情報を適用する場合は、最後に適用された資格情報が使用されます。 複数のコンポーネントが同じ認証済みChannelSetオブジェクトを使用する場合、 `logout`メソッドを呼び出すと、すべてのコンポーネントが宛先からログに記録されます。

次の例では、 `ChannelSet.login`メソッドと`ChannelSet.logout`メソッドをRemoteObjectコントロールと共に使用します。 このアプリケーションは、次のアクションを実行します。

* `RemoteObject`コンポーネントで使用されるチャネルを表す`ChannelSet`オブジェクトを`creationComplete`ハンドラーに作成します
* ボタンクリックイベントに応答して`ROLogin`関数を呼び出すことで、資格情報をサーバーに渡します
* RemoteObjectコンポーネントを使用して、Button clickイベントに応答して文字列をサーバーに送信します。 サーバーが同じ文字列をRemoteObjectコンポーネントに返す
* RemoteObjectコンポーネントのresultイベントを使用して、 TextAreaコントロールにStringを表示します
* Button clickイベントに応答して`ROLogout`関数を呼び出し、サーバーからログアウトします。

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

`login`メソッドと`logout`メソッドはAsyncTokenオブジェクトを返します。 成功した呼び出しを処理する結果イベントと失敗を処理する障害イベントに、AsyncTokenオブジェクトにイベントハンドラーを割り当てます。

### シングルサインオン{#using-single-sign-on}の使用

AEM formsユーザーは、複数のAEM Forms Webアプリケーションに接続して、1つのタスクを実行できます。 ユーザーがWebアプリケーション間を移動する際に、各Webアプリケーションに別々にログインする必要が生じるのは効率的ではありません。 AEM Formsのシングルサインオンメカニズムを使用すると、ユーザーは1回ログインして、任意のAEM Forms Webアプリケーションにアクセスできます。 AEM Forms開発者はAEM Formsで使用するクライアントアプリケーションを作成できるので、シングルサインオンメカニズムも利用できる必要があります。

各AEM Forms Webアプリケーションは、独自のWebアーカイブ(WAR)ファイルにパッケージ化され、エンタープライズアーカイブ(EAR)ファイルの一部としてパッケージ化されます。 アプリケーションサーバーでは異なるWebアプリケーション間でのセッションデータの共有が許可されないので、AEM FormsではHTTP Cookieを使用して認証情報を保存します。 認証Cookieを使用すると、ユーザーはFormsアプリケーションにログインして、他のAEM Forms Webアプリケーションに接続できます。 この手法は、シングルサインオンと呼ばれます。

AEM Forms開発者は、フォームガイド（非推奨）の機能を拡張し、Workspaceをカスタマイズするためのクライアントアプリケーションを作成します。 例えば、Workspaceアプリケーションはプロセスを開始できます。 次に、クライアントアプリケーションは、リモートエンドポイントを使用してFormsサービスからデータを取得します。

(AEM formsでは非推奨)AEM Forms Remotingを使用してAEM Formsサービスを呼び出すと、クライアントアプリケーションは認証Cookieをリクエストの一部として渡します。 ユーザーは既に認証されているので、クライアントアプリケーションからAEM Formsサービスに接続するために追加のログインは必要ありません。

>[!NOTE]
cookieが無効な場合や見つからない場合、ログインページへの暗黙のリダイレクトはありません。 したがって、匿名サービスを呼び出すことができます。

AEM Formsのシングルサインオンメカニズムをバイパスするには、独自にログインおよびログアウトするクライアントアプリケーションを記述します。 シングルサインオンメカニズムを回避する場合は、アプリケーションで基本認証またはカスタム認証を使用できます。

このメカニズムではAEM Formsのシングルサインオンメカニズムが使用されないので、認証Cookieはクライアントに書き込まれません。 ログイン資格情報は、リモートチャネルの`ChannelSet`オブジェクトに保存されます。 したがって、同じ`ChannelSet`を介して行う`RemoteObject`呼び出しは、これらの資格情報のコンテキストで行われます。

### AEM Forms {#setting-up-single-sign-on-in-aem-forms}でのシングルサインオンの設定

AEM Formsでシングルサインオンを使用するには、一元化されたログインサービスを含むフォームワークフローコンポーネントをインストールします。 ユーザーが正常にログインした後、一元化されたログインサービスはユーザーに認証cookieを返します。 Forms Webアプリケーションに対する以降のリクエストには、すべてcookieが含まれます。 このcookieが有効な場合、ユーザーは認証済みと見なされ、再度ログインする必要はありません。

### シングルサインオン{#writing-a-client-application-that-uses-single-sign-on}を使用するクライアントアプリケーションの書き込み

シングルサインオンメカニズムを利用する場合、クライアントアプリケーションを起動する前に、一元化されたログインサービスを使用してログインする必要があります。 つまり、クライアントアプリケーションは、ブラウザーを使用したり、`ChannelSet.login`メソッドを呼び出したりしてログインすることはありません。

AEM Formsのシングルサインオンメカニズムを使用している場合、基本ではなくカスタム認証を使用するようにリモートエンドポイントを設定します。 そうしないと、基本認証を使用する場合、認証エラーが発生すると、ブラウザーの課題が発生し、ユーザーには表示されなくなります。 代わりに、アプリケーションは認証エラーを検出し、一元化されたログインサービスを使用してログインするようにユーザーに指示するメッセージを表示します。

次の例に示すように、クライアントアプリケーションは、 `RemoteObject`コンポーネントを使用して、リモートエンドポイントを通じてAEM Formsにアクセスします。

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

**Flexアプリケーションの実行中に新しいユーザーとしてログインする**

Flexを使用して構築されたアプリケーションには、AEM Formsサービスに対するすべてのリクエストを含む認証Cookieが含まれます。 パフォーマンス上の理由から、AEM FormsではリクエストごとにCookieが検証されません。 ただし、AEM Formsは、認証cookieが別の認証cookieに置き換えられたかどうかを検出します。

例えば、クライアントアプリケーションを起動し、アプリケーションがアクティブな間は、一元化されたログインサービスを使用してログアウトします。 次に、別のユーザーとしてログインできます。 別のユーザーとしてログインすると、既存の認証cookieが新しいユーザーの認証cookieに置き換えられます。

クライアントアプリケーションからの次のリクエストで、AEM Formsはcookieが変更されたことを検出し、ユーザーをログアウトします。 したがって、Cookieの変更後の最初のリクエストは失敗します。 以降のリクエストはすべて、新しいcookieのコンテキストでおこなわれ、成功します。

**ログアウト**

AEM Formsからログアウトしてセッションを無効にするには、クライアントのコンピューターから認証Cookieを削除する必要があります。 シングルサインオンの目的は、ユーザーが1回ログインすることを許可することなので、クライアントアプリケーションでCookieを削除する必要はありません。 この操作により、ユーザーが効果的にログアウトされます。

したがって、クライアントアプリケーションで`RemoteObject.logout`メソッドを呼び出すと、クライアント上でセッションがログアウトされていないことを示すエラーメッセージが生成されます。 代わりに、一元化されたログインサービスを使用して、認証Cookieをログアウトおよび削除できます。

**Flexアプリケーションの実行中にログアウトする**

Flexで構築されたクライアントアプリケーションを起動し、一元化されたログインサービスを使用してログアウトできます。 ログアウトプロセスの一環として、認証Cookieが削除されます。 Cookieがない、または無効なCookieを持つリモート要求がおこなわれた場合、ユーザーセッションは無効化されます。 このアクションはログアウトされます。 クライアントアプリケーションが次回AEM Formsサービスに接続しようとすると、ユーザーはログインを要求されます。

**関連トピック**

[(AEM formsでは非推奨)AEM Forms Remotingを使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理(AEM formsでは非推奨)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## リモート処理{#passing-secure-documents-to-invoke-processes-using-remoting}を使用してプロセスを呼び出すための安全なドキュメントを渡す

1つ以上のドキュメントを必要とするプロセスを呼び出す際に、セキュリティで保護されたドキュメントをAEM Formsに渡すことができます。 安全なドキュメントを渡すことで、ビジネス情報や機密ドキュメントを保護できます。 この場合、1つのドキュメントでPDFドキュメント、XMLドキュメント、Wordドキュメントなどを参照できます。 セキュリティで保護されたドキュメントを許可するようにAEM Formsを設定する場合、Flexで記述されたクライアントアプリケーションからAEM Formsにセキュアなドキュメントを渡す必要があります。 ([安全なドキュメントと安全でないドキュメントを受け入れるようにAEM Formsを設定する](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)を参照)。

安全なドキュメントを渡す場合は、シングルサインオンを使用し、*Document Upload Application User*&#x200B;の役割を持つAEM formsユーザーを指定します。 このロールがないと、ユーザーは保護されたドキュメントをアップロードできません。 プログラムによって役割をユーザーに割り当てることができます。 （[役割と権限の管理](/help/forms/developing/users.md#managing-roles-and-permissions)を参照）。

>[!NOTE]
新しいロールを作成し、そのロールのメンバーに保護されたドキュメントをアップロードする場合は、ドキュメントのアップロード権限を必ず指定してください。

AEM Formsは、アップロードサーブレットに渡されたトークンを返す`getFileUploadToken`という操作をサポートします。 `DocumentReference.constructRequestForUpload`メソッドには、`LC.FileUploadAuthenticator.getFileUploadToken`メソッドで返されるトークンと共に、AEM FormsへのURLが必要です。 このメソッドは、アップロードサーブレットへの呼び出しで使用される`URLRequest`オブジェクトを返します。 次のコードは、このアプリケーションロジックの例を示しています。

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

）

### 安全なドキュメントと安全でないドキュメントを受け入れるようにAEM Formsを設定する{#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

管理コンソールを使用して、FlexクライアントアプリケーションからAEM Formsプロセスにドキュメントを渡す際に、ドキュメントをセキュリティで保護するかどうかを指定できます。 デフォルトでは、AEM Formsはセキュリティで保護されたドキュメントを受け入れるように設定されています。 次の手順を実行して、セキュリティで保護されたドキュメントを受け入れるようにAEM Formsを設定できます。

1. 管理コンソールにログインします。
1. 「**設定**」をクリックします。
1. **Core System Settings.**&#x200B;をクリックします。
1. 「設定」をクリックします。
1. 「 Flexアプリケーションからのドキュメントのアップロードを保護しないことを許可する」オプションが選択されていないことを確認します。

>[!NOTE]
セキュリティで保護されていないドキュメントを受け入れるようにAEM Formsを設定するには、「Flexアプリケーションからのセキュリティで保護されていないドキュメントのアップロードを許可」オプションを選択します。 次に、アプリケーションまたはサービスを再起動して、設定が有効になるようにします。

### クイックスタート：リモート処理{#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}を使用して保護されたドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し

次のコード例は、`MyApplication/EncryptDocument.`を呼び出します。ユーザーは、PDFファイルのアップロードとプロセスの呼び出しに使用する「Select File」ボタンをクリックするためにログインする必要があります。 つまり、ユーザーが認証されると、「 Select File 」ボタンが有効になります。 次の図に、ユーザーが認証された後のFlexクライアントアプリケーションを示します。 Authenticated CheckBoxが有効になっています。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

AEM Formsが、セキュリティで保護されたドキュメントのアップロードのみを許可するように設定され、ユーザーに&#x200B;*Document Upload Application User*&#x200B;の役割がない場合は、例外がスローされます。 この役割を持つユーザーは、ファイルをアップロードし、プロセスを呼び出します。

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

[(AEM formsでは非推奨)AEM Forms Remotingを使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理(AEM formsでは非推奨)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## リモート{#invoking-custom-component-services-using-remoting}を使用したカスタムコンポーネントサービスの呼び出し

リモート処理を使用して、カスタムコンポーネント内のサービスを呼び出すことができます。 例えば、顧客サービスを含む銀行コンポーネントを考えてみます。 Flexで記述されたクライアントアプリケーションを使用して、顧客サービスに属する操作を呼び出すことができます。 このセクションに関連付けられたクイックスタートを実行する前に、Bankカスタムコンポーネントを作成する必要があります。

カスタマーサービスは、`createCustomer`という名前の操作を公開します。 このディスカッションでは、Customer Serviceを呼び出して顧客を作成するFlexクライアントアプリケーションの作成方法を説明します。 この操作には、新しい顧客を表す`com.adobe.livecycle.sample.customer.Customer`型の複雑なオブジェクトが必要です。 次の図に、顧客サービスを呼び出して新しい顧客を作成するクライアントアプリケーションを示します。 `createCustomer`操作は顧客識別子の値を返します。 識別子の値は、「顧客識別子」テキスト・ボックスに表示されます。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

次の表に、このクライアントアプリケーションに含まれるコントロールを示します。

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
   <td><p>顧客の住所を指定します。</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>顧客の状態を指定します。 </p></td>
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
   <td><p>新しいアカウントが属する顧客識別子の値を指定します。 このテキストボックスには、カスタマーサービスの<code>createCustomer</code>操作の戻り値が設定されます。 </p></td>
  </tr>
 </tbody>
</table>

### AEM Forms複合データ型{#mapping-aem-forms-complex-data-types}のマッピング

一部のAEM Forms操作では、入力値として複雑なデータ型が必要です。 これらの複雑なデータ型は、操作で使用される実行時の値を定義します。 例えば、顧客サービスの`createCustomer`操作には、サービスに必要な実行時の値を含む`Customer`インスタンスが必要です。 複合型がない場合、Customerサービスは例外をスローし、操作を実行しません。

AEM Formsサービスを呼び出す場合は、必要なAEM Forms複合型にマッピングするActionScriptオブジェクトを作成します。 操作に必要な複雑なデータ型ごとに、個別のActionScriptオブジェクトを作成します。

ActionScriptクラスでは、 `RemoteClass`メタデータタグを使用してAEM Forms複合型にマッピングします。 例えば、顧客サービスの`createCustomer`操作を呼び出す場合、`com.adobe.livecycle.sample.customer.Customer`データ型にマッピングするActionScriptクラスを作成します。

次のActionScriptクラスは、AEM Formsデータ型`com.adobe.livecycle.sample.customer.Customer`にマッピングする方法を示しています。

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

AEM Forms複合型の完全修飾データ型がエイリアスタグに割り当てられます。

ActionScriptクラスのフィールドは、AEM Forms複合タイプに属するフィールドと一致します。 顧客ActionScriptクラスの6つのフィールドは、`com.adobe.livecycle.sample.customer.Customer`に属するフィールドと一致します。

>[!NOTE]
Forms複合型に属するフィールド名を判断する良い方法は、WebブラウザーでサービスのWSDLを表示することです。 WSDLは、サービスの複合型と対応するデータメンバを指定します。 顧客サービスでは、次のWSDLが使用されます。`https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

顧客ActionScriptクラスは、customerという名前のパッケージに属しています。 複雑なAEM Formsデータ型にマッピングするすべてのActionScriptクラスは、独自のパッケージに配置することをお勧めします。 次の図に示すように、FlexプロジェクトのsrcフォルダーにActionScriptーを作成し、フォルダー内にフォルダーファイルを配置します。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### クイックスタート：リモート処理{#quick-start-invoking-the-customer-custom-service-using-remoting}を使用した顧客カスタムサービスの呼び出し

次のコード例は、顧客サービスを呼び出して新しい顧客を作成します。 このコード例を実行する場合は、すべてのテキストボックスに必ず入力してください。 また、`com.adobe.livecycle.sample.customer.Customer`にマッピングするCustomer.asファイルを作成してください。

>[!NOTE]
このクイックスタートを実行する前に、Bankカスタムコンポーネントを作成してデプロイする必要があります。

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

このクイックスタートには、*bank.css*&#x200B;という名前のスタイルシートが含まれています。 次のコードは、使用されるスタイルシートを表しています。

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

[(AEM formsでは非推奨)AEM Forms Remotingを使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Remotingでのドキュメントの処理(AEM formsでは非推奨)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[(AEM formsでは非推奨)AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで構築されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
