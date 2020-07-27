---
title: REST要求を使用したAEM Formsの呼び出し
seo-title: REST要求を使用したAEM Formsの呼び出し
description: 'null'
seo-description: 'null'
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 4%

---


# REST要求を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-rest-requests}

Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST 要求は HTML ページから送信されます。つまり、REST要求を使用して、Webページから直接Formsプロセスを呼び出すことができます。 例えば、Webページの新しいインスタンスを開くことができます。 次に、Formsプロセスを呼び出し、HTTP POST要求で送信されたデータを含むレンダリングされたPDFドキュメントを読み込みます。

2種類のHTMLクライアントが存在します。 最初のHTMLクライアントは、JavaScriptで記述されるAJAXクライアントです。 2番目のクライアントは、送信ボタンを含むHTMLフォームです。 RESTクライアントとして使用できるのは、HTMLベースのクライアントアプリケーションだけではありません。 HTTP要求をサポートする任意のクライアントアプリケーションは、REST呼び出しを使用してサービスを呼び出すことができます。 例えば、PDFフォームからREST呼び出しを使用してサービスを呼び出すことができます。 (AcrobatからのMyApplication/EncryptDocumentプロセスの [呼び出しを参照](#rest-invocation-examples))。

REST要求を使用する場合は、Formsサービスを直接呼び出さないことをお勧めします。 代わりに、Workbenchで作成されたプロセスを呼び出します。 REST呼び出し用のプロセスを作成する場合は、プログラム型開始ポイントを使用します。 この場合、RESTエンドポイントは自動的に追加されます。 Workbenchでのプロセスの作成について詳しくは、「Workbenchの [使用](https://www.adobe.com/go/learn_aemforms_workbench_63)」を参照してください。

RESTを使用してサービスを呼び出す場合は、AEM formsのユーザー名とパスワードの入力を求められます。 ただし、ユーザー名とパスワードを指定しない場合は、サービスセキュリティを無効にできます。

RESTを使用してFormsサービスを呼び出す（プロセスがアクティブ化されるとプロセスがサービスになります）には、RESTエンドポイントを設定します。 ( [管理ヘルプの「エンドポイントの管理」を参照](https://www.adobe.com/go/learn_aemforms_admin_63))。

RESTエンドポイントを設定した後、HTTP GETメソッドまたはPOSTメソッドを使用してFormsサービスを呼び出すことができます。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必須の `ServiceName` 値は、呼び出すFormsサービスの名前です。 オプションの `OperationName` 値は、サービスの操作の名前です。 この値を指定しない場合、この名前はデフォルトで `invoke`、プロセスを開始する操作名になります。 オプションの `ServiceVersion` 値は、X.Y形式でエンコードされたバージョンです。 この値を指定しない場合は、最新バージョンが使用されます。 値をにすることもでき `enctype` ま `application/x-www-form-urlencoded`す。

## サポートされるデータタイプ {#supported-data-types}

REST要求を使用してAEM Formsサービスを呼び出す場合、次のデータ型がサポートされます。

* Javaプリミティブデータ型（文字列や整数など）
* `com.adobe.idp.Document` データ型
* XMLデータ型( `org.w3c.Document` およびなど) `org.w3c.Element`
* およびなどのコレクションオブジェクト `java.util.List` `java.util.Map`

   これらのデータ型は、一般に、Workbenchで作成されたプロセスへの入力値として受け入れられます。

   HTTP POSTメソッドを使用してFormsサービスを呼び出した場合、HTTP要求本文内で引数が渡されます。 AEM Formsサービスの署名に文字列入力パラメーターが含まれている場合、要求本文には、入力パラメーターのテキスト値を含めることができます。 サービスの署名で複数の文字列パラメーターが定義されている場合、要求は、HTTP `application/x-www-form-urlencoded` 表記の後に、フォームのフィールド名として使用されているパラメーター名を記述することができます。

   Formsサービスが文字列パラメーターを返す場合、結果は出力パラメーターのテキスト表現になります。 サービスが複数の文字列パラメーターを返す場合、出力パラメーターを次の形式でエンコードしたXMLドキュメントが返されます。
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >この `output-paramater1` 値は、出力パラメーター名を表します。

   Formsサービスにパラメーターが必要な場合は、HTTP POSTメソッドを使用した場合のみ、サービスを呼び出すことができます。 `com.adobe.idp.Document` サービスに1つのパラメーターが必要な場合は、HTTP要求本文が入力ドキュメントオブジェクトのコンテンツになります。 `com.adobe.idp.Document`

   AEM Formsサービスに複数の入力パラメーターが必要な場合、HTTP要求本文は、RFC 1867で定義されているマルチパート形式のMIMEメッセージである必要があります。 （RFC 1867は、WebブラウザーがファイルをWebサイトにアップロードする際に使用する標準です）。 各入力パラメーターは、マルチパート形式のメッセージの個別の部分として送信し、 `multipart/form-data` 形式でエンコードする必要があります。 各パーツの名前は、パラメータの名前と一致する必要があります。

   リストとマップは、Workbenchで作成されたAEM Formsプロセスへの入力値としても使用されます。 その結果、RESTリクエストを使用する場合は、これらのデータ型を使用できます。 Java配列は、AEM Formsプロセスの入力値として使用されないため、サポートされません。

   入力パラメーターがリストの場合、RESTクライアントは、リストーの各項目に対して1回ずつパラメーターを繰り返し指定することで、入力パラメーターを送信できます。 例えば、Aがドキュメントのリストである場合、入力はAという名前の複数のパーツから成るマルチパートメッセージである必要があります。この場合、Aという名前の各パーツは、入力リスト内のアイテムになります。 Bが文字列のリストである場合、入力はBという名前の複数のフィールドから成る `application/x-www-form-urlencoded` メッセージにすることができます。この場合、Bという名前の各フォームフィールドは、入力リスト内の項目になります。

   入力パラメーターがマップで、それがサービスのみの入力パラメーターの場合、入力メッセージのすべての部分/フィールドが、マップ内のキー/値レコードになります。 各パーツまたはフィールドの名前がレコードのキーになります。 各パーツまたはフィールドのコンテンツがレコードの値になります。

   入力マップがサービスのみの入力パラメータでない場合は、パラメータ名とレコードのキーを連結した名前のパラメータを使用して、マップに属する各キー/値レコードを送信できます。 例えば、という入力マップ `attributes` は、次のキー/値のペアのリストと共に送信できます。

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   これは、3つのレコードのマップに変換されます。 `Color=red`、 `Shape=box`および `Width=5`。

   リスト型とマップ型の出力パラメーターは、結果のXMLメッセージの一部になります。 出力リストは、リスト内の各項目に対して1つの要素を持つ一連のXML要素としてXMLで表されます。 すべてのリストには、出力要素パラメーターと同じ名前が与えられます。 各XML要素の値は、次の2つのいずれかになります。

* リスト内の項目のテキスト表現(リストが文字列型で構成されている場合)
* ドキュメントのコンテンツを指すURL(リストが `com.adobe.idp.Document` オブジェクトで構成されている場合)

   次の例は、 *リスト*(整数のリスト)という名前の単一の出力パラメーターを持つサービスから返されるXMLメッセージです。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`出力マップパラメーターは、結果のXMLメッセージ内で、マップ内の各レコードに対して1つの要素を持つ一連のXML要素として表されます。 すべての要素には、マップレコードのキーと同じ名前が付けられます。 各要素の値は、マップレコードの値のテキスト表現（マップが文字列値を持つレコードで構成されている場合）またはドキュメントのコンテンツを指すURL（マップが値を持つレコードで構成されている場合）です。 `com.adobe.idp.Document` 次の例は、という名前の単一の出力パラメーターを持つサービスから返されるXMLメッセージの例で `map`す。 このパラメータ値は、レターをオブジェクトに関連付けるレコードで構成されるマップで `com.adobe.idp.Document` す。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同期呼び出し {#asynchronous-invocations}

人間中心の長期間有効なプロセスなど、一部のAEM Formsサービスの完了に長い時間が必要になります。 これらのサービスは、非ブロッキング方式で非同期に呼び出すことができます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

次の例に示すように、AEM Formsサービスは、呼び出しURL `services` の代わりに使用す `async_invoke` ることで、非同期で呼び出すことができます。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

このURLは、この呼び出しを行うジョブの識別子値（「text/plain」形式）を返します。

非同期呼び出しのステータスは、で `services` 置き換えられた呼び出しURLを使用して取得でき `async_status`ます。 URLには、この呼び出しに関連付けられたジョブの識別子値を指定する `job_id` パラメーターが含まれている必要があります。 次に例を示します。

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

このURLは、ジョブマネージャーの仕様に従ってジョブステータスをエンコードする整数値（「text/plain」形式）を返します（例えば、2は実行中、3は完了、4は失敗など）。

ジョブが完了した場合、サービスが同期的に呼び出された場合と同じ結果がURLから返されます。

ジョブが完了し、結果が取得されたら、呼び出しURLを使用してジョブを破棄する `services` ことができ、このURLはに置き換えられ `async_dispose`ます。 URLには、ジョブの識別子の値を指定する `job_id` パラメーターも含める必要があります。 次に例を示します。

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

ジョブが正常に破棄された場合、このURLは空のメッセージを返します。

## エラーレポート {#error-reporting}

サーバーで例外がスローされたために同期または非同期の呼び出し要求を完了できない場合、その例外はHTTP応答メッセージの一部としてレポートされます。 呼び出しURL(または非同期呼び出しの場合は `async_result` URL)に.xmlサフィックスが付いていない場合、RESTプロバイダーはHTTPコードを返し、その後に例外メッセージ `500 Internal Server Error` を返します。

呼び出しURL(または非同期呼び出しの場合は `async_result` URL)に.xmlサフィックスが付いている場合、RESTプロバイダーはHTTPコード `200 OK`の後に、次の形式で例外を説明するXMLドキュメントを返します。

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

この `DSCError` 要素はオプションで、例外がのインスタンスの場合にのみ存在し `com.adobe.idp.dsc.DSCException`ます。

## セキュリティと認証 {#security-and-authentication}

安全な転送でREST呼び出しを行うために、AEM forms管理者は、J2EEアプリケーションサーバーのホストAEM FormsでHTTPSプロトコルを有効にできます。 この設定は、J2EEアプリケーションサーバーに固有のものです。 formsサーバー設定の一部ではありません。

>[!NOTE]
>
>RESTエンドポイントを介してプロセスを公開するWorkbench開発者は、XSSの脆弱性の問題に注意してください。 XSS脆弱性は、cookieの盗用や操作、コンテンツの表示の変更、漏洩した機密情報に使用できます。 XSSの脆弱性が問題となる場合は、追加の入力および出力データ検証ルールを使用してプロセスロジックを拡張することをお勧めします。

## REST呼び出しをサポートするAEM Formsサービス {#aem-forms-services-that-support-rest-invocation}

サービスを直接呼び出すのではなく、Workbenchを使用して作成したプロセスを呼び出すことをお勧めしますが、いくつかのAEM Formsサービスでは、REST呼び出しをサポートしています。 サービスを直接呼び出すのではなく、プロセスを直接呼び出すことをお勧めする理由は、プロセスを呼び出す方が効率的なためです。 次のシナリオを考えてみましょう。 RESTクライアントからポリシーを作成するとします。 つまり、RESTクライアントでポリシー名、オフラインリース期間などの値を定義する必要があります。

ポリシーを作成するには、 `PolicyEntry` オブジェクトなどの複雑なデータ型を定義する必要があります。 オブジェクトは、ポリシーに関連付けられた権限などの属性を定義します。 `PolicyEntry` (ポリシーの [作成を参照](/help/forms/developing/protecting-documents-policies.md#creating-policies))。

ポリシー( `PolicyEntry` オブジェクトなどの複雑なデータ型の定義を含む)を作成するためのREST要求を送信する代わりに、Workbenchを使用してポリシーを作成するプロセスを作成します。 プロセス名を定義する文字列値や、オフラインリース期間を定義する整数など、プリミティブ入力変数を受け入れるプロセスを定義します。

この方法では、操作に必要な複雑なデータ型を含むREST呼び出し要求を作成する必要はありません。 プロセスでは複雑なデータ型が定義され、RESTクライアントから実行するのは、プロセスを呼び出してプリミティブデータ型を渡すことだけです。 RESTを使用したプロセスの呼び出しについて詳しくは、RESTを使用したMyApplication/EncryptDocumentプロセスの [呼び出しを参照してください](#rest-invocation-examples)。

次のリストは、直接REST呼び出しをサポートするAEM Formsサービスを指定します。

* Distiller サービス[Distiller さーびす]
* Rights Management サービス[Rights Management さーびす]
* GeneratePDFサービス
* Generate3dPDFサービス
* FormDataIntegration

## REST呼び出しの例 {#rest-invocation-examples}

次に示すREST呼び出しの例を示します。

* AEM Formsプロセスにブール値を渡す
* AEM Formsプロセスに日付値を渡す
* ドキュメントをAEM Formsプロセスに渡す
* ドキュメント値とテキスト値をAEM Formsプロセスに渡す
* 定義済みリスト値をAEM Formsプロセスに渡す
* RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し
* AcrobatからのMyApplication/EncryptDocumentプロセスの呼び出し

   各例では、様々なデータ型をAEM Formsプロセスに渡す方法を示します

**プロセスにブール値を渡す**

次のHTMLの例では、2つの `Boolean` 値をという名前のAEM Formsプロセスに渡 `RestTest2`します。 呼び出しメソッドの名前はで `invoke` 、バージョンは1.0です。HTML Postメソッドが使用されていることに注意してください。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**プロセスに日付値を渡す**

次のHTMLの例では、という名前のAEM Formsプロセスに日付値を渡し `SOAPEchoService`ます。 呼び出しメソッドの名前はで `echoCalendar`す。 HTML `Post` メソッドが使用されます。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**プロセスにドキュメントを渡す**

次のHTMLの例は、PDFドキュメントを必要とするという名前のAEM Formsプロセス `MyApplication/EncryptDocument` を呼び出します。 このプロセスについて詳しくは、「MTOMを使用したAEM Formsの [呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)」を参照してください。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**プロセスにドキュメント値とテキスト値を渡す**

次のHTMLの例は、という名前のAEM Formsプロセスを呼び出します。このプロセスには、ドキュメント `RestTest3` と2つのテキスト値が必要です。 HTML Postメソッドが使用されていることに注意してください。

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**プロセスに定義済みリスト値を渡す**

次のHTMLの例は、定義済みリスト値を必要とするという名前のAEM Formsプロセス `SOAPEchoService` を呼び出します。 HTML Postメソッドが使用されていることに注意してください。

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し**

RESTを使用して、MyApplication/EncryptDocumentという名前の短時間のみ有効なAEM Forms *を呼び出すことができます* 。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。To follow along with the code example, create a process named `MyApplication/EncryptDocument` using workbench. （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

   REST要求を使用してこのプロセスを呼び出すと、暗号化されたPDFドキュメントがWebブラウザーに表示されます。 PDFドキュメントを表示する前に、パスワードを指定します（セキュリティが無効になっていない場合）。 次のHTMLコードは、プロセスに対するREST呼び出し要求を表してい `MyApplication/EncryptDocument` ます。

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**AcrobatからのMyApplication/EncryptDocumentプロセスの呼び出し** {#invoke-process-acrobat}

Formsプロセスは、REST要求を使用してAcrobatから呼び出すことができます。 例えば、MyApplication/EncryptDocument ** プロセスを呼び出すことができます。 AcrobatからFormsプロセスを呼び出すには、Designer内のXDPファイルに送信ボタンを配置します。 （「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照）。

次の図に示すように、ボタンの「 *Submit to URL* 」フィールド内でプロセスを呼び出すURLを指定します。

プロセスを呼び出すための完全なURLはhttps://hiro-xp:8080/rest/services/MyApplication/EncryptDocumentです。

プロセスで入力値としてPDFドキュメントが必要な場合は、前の図に示すように、必ずPDFとしてフォームを送信してください。 また、プロセスを正常に呼び出すには、プロセスがPDFドキュメントを返す必要があります。 そうしないと、Acrobatは戻り値を処理できず、エラーが発生します。 入力プロセス変数の名前を指定する必要はありません。 例えば、MyApplication/EncryptDocument *プロセスには、という名前の入力変数があ*`inDoc`ります。 フォームがPDFとして送信される限り、inDocを指定する必要はありません。

フォームデータをXMLとしてFormsプロセスに送信することもできます。XMLデータを送信するには、ドロップダウンでXMLが指定されていることを確認し `Submit As` ます。 プロセスの戻り値はPDFドキュメントである必要があるので、PDFドキュメントはAcrobatで表示されます。
