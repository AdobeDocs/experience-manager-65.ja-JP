---
title: REST リクエストを使用した AEM Forms の呼び出し
seo-title: Invoking AEM Forms using REST Requests
description: REST リクエストを使用して、Workbench で作成されたプロセスを呼び出します。
seo-description: Invoke processes created in Workbench using REST requests.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 97%

---

# REST リクエストを使用した AEM Forms の呼び出し {#invoking-aem-forms-using-rest-requests}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST 要求は HTML ページから送信されます。つまり、REST リクエストを使用して、Web ページから直接 Forms プロセスを呼び出すことができます。例えば、web ページの新しいインスタンスを開くことができます。次に、Forms プロセスを呼び出し、HTTP POST リクエストで送信されたデータを含む、レンダリングされた PDF ドキュメントを読み込むことができます。

2 種類のHTML クライアントが存在します。最初の HTML クライアントは、JavaScript で記述された AJAX クライアントです。2 つ目のクライアントは、送信ボタンを含む HTML フォームです。HTML ベースのクライアントアプリケーションは、REST クライアントとして使用できる唯一のクライアントではありません。HTTP リクエストをサポートするクライアントアプリケーションは、REST 呼び出しを使用してサービスを呼び出すことができます。例えば、PDF フォームからの REST 呼び出しを使用して、サービスを呼び出すことができます。（[Acrobat からの MyApplication／EncryptDocument プロセスの呼び出し](#rest-invocation-examples)を参照。）

REST リクエストを使用する場合は、Forms サービスを直接呼び出さないことをお勧めします。代わりに、Workbench で作成されたプロセスを呼び出します。REST 呼び出し用のプロセスを作成する場合は、プログラム的なスタートポイントを使用します。この場合、REST エンドポイントは自動的に追加されます。Workbench でのプロセスの作成について詳しくは、[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。

REST を使用してサービスを呼び出すと、AEM Forms のユーザー名とパスワードの入力を求められます。ただし、ユーザー名とパスワードを指定しない場合は、Service Security を無効にできます。

REST を使用して Forms サービスを呼び出す（プロセスがアクティブになるとプロセスがサービスになります）には、REST エンドポイントを設定します。(「エンドポイントの管理」( [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63_jp).)

REST エンドポイントを設定した後、HTTP GET メソッドまたは POST メソッドを使用して、Forms サービスを呼び出すことができます。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必須の `ServiceName` 値は、呼び出す Forms サービスの名前です。オプションの `OperationName` 値はサービスの操作の名前です。この値を指定しない場合、この名前はデフォルトで `invoke`（プロセスを開始する操作の名前）になります。オプションの `ServiceVersion` の値は、X.Y 形式でエンコードされたバージョンです。この値を指定しない場合は、最新のバージョンが使用されます。`enctype` 値は `application/x-www-form-urlencoded` にすることもできます。

## サポートされるデータタイプ {#supported-data-types}

REST リクエストを使用してAEM Forms サービスを呼び出す場合、次のデータタイプがサポートされます。

* 文字列や整数などの Java プリミティブデータタイプ
* `com.adobe.idp.Document` データタイプ
* XML データタイプ（例： `org.w3c.Document` および `org.w3c.Element`）
* コレクションオブジェクト（例： `java.util.List` および `java.util.Map`）

   これらのデータタイプは、通常、Workbench で作成されるプロセスへの入力値として受け入れられます。

   HTTP POST メソッドを使用して Froms サービスが呼び出された場合、引数は HTTP リクエスト本文内に渡されます。AEM Forms サービスの署名に文字列入力パラメーターがある場合、リクエスト本文には入力パラメーターのテキスト値を含めることができます。サービスの署名で複数の文字列パラメーターが定義されている場合、リクエストは、フォームのフィールド名として使用されるパラメーターの名前を使用して、HTTP の `application/x-www-form-urlencoded` 表記に従うことができます。

   Forms サービスが文字列パラメーターを返す場合、結果は出力パラメーターのテキスト表現になります。サービスが複数の文字列パラメーターを返す場合、結果は出力パラメーターを次の形式でエンコードする XML ドキュメントになります。
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1` 値は出力パラメーター名を表します。

   Forms サービスに `com.adobe.idp.Document` パラメーターが必要な場合、サービスは HTTP POST メソッドのみを使用して呼び出すことができます。サービスが 1 つの `com.adobe.idp.Document` パラメーターを必要とする場合、HTTP リクエスト本文は入力 Document オブジェクトのコンテンツになります。

   AEM Forms サービスで複数の入力パラメーターが必要な場合、HTTP リクエスト本文は、RFC 1867 で定義されているマルチパート MIME メッセージである必要があります。（RFC 1867 は、web ブラウザーがファイルを web サイトにアップロードする際に使用する標準です）。各入力パラメーターは、マルチパートメッセージの個別の部分として送信し、`multipart/form-data` 形式でエンコードされます。各パーツの名前は、パラメータの名前と一致する必要があります。

   リストとマップは、Workbench で作成される AEM Forms プロセスへの入力値としても使用されます。その結果、REST リクエストを使用する際に、これらのデータタイプを使用できます。Java 配列は、AEM Forms プロセスの入力値として使用されていないので、サポートされていません。

   入力パラメーターがリストの場合、REST クライアントは、パラメーターを複数回指定して（リスト内の項目ごとに 1 回）送信できます。例えば、A がドキュメントのリストの場合、入力は A という名前の複数のパーツで構成されるマルチパートメッセージである必要があります。この場合、A という名前の各パーツは入力リストのアイテムになります。B が文字列のリストの場合、入力は B という名前の複数のフィールドで構成される`application/x-www-form-urlencoded`メッセージ。この場合、B という名前の各フォームフィールドは、入力リストの項目になります。

   入力パラメーターがマップで、それがサービスのみの入力パラメーターの場合、入力メッセージのすべてのパーツやフィールドがマップ内のキーレコードや値レコードになります。各パーツまたはフィールドの名前が、レコードのキーになります。各パーツまたはフィールドのコンテンツが、レコードの値になります。

   入力マップがサービスのみの入力パラメータでない場合、マップに属する各キーレコードや値レコードは、パラメータ名とレコードのキーを連結した名前のパラメータを使用して送信できます。例えば、 `attributes` と呼ばれる入力マップは、次のキーと値のペアのリストと共に送信できます。

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   これは、 `Color=red`、`Shape=box`、および `Width=5` の 3 つのレコードのマップに変換されます。

   List 型と Map 型の出力パラメーターは、結果の XML メッセージの一部になります。出力リストは、一連の XML 要素として XML で表され、リスト内の項目ごとに 1 つの要素を持ちます。すべての要素には、出力リストパラメーターと同じ名前が付けられます。各 XML 要素の値は、次の 2 つのうちのいずれかとなります。

* リスト内の項目のテキスト表現（リストが文字列型で構成されている場合）
* ドキュメントのコンテンツを指す URL（リストが `com.adobe.idp.Document` オブジェクトで構成されている場合）

   次の例は、整数のリストである&#x200B;*リスト*という名前の単一の出力パラメーターを持つサービスから返される XML メッセージです。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`出力マップパラメータは、結果の XML メッセージ内で、マップ内の各レコードに対して 1 つの要素を持つ一連の XML 要素として表されます。すべての要素には、マップレコードのキーと同じ名前が付けられます。各要素の値は、マップレコードの値のテキスト表現か（マップが文字列値を持つレコードで構成される場合）、ドキュメントのコンテンツを指す URL です（マップが `com.adobe.idp.Document` の値を持つレコードで構成される場合）。次は、`map`という名前の単一の出力パラメーターを持つサービスが返す XML メッセージの例を示します。このパラメーター値は、`com.adobe.idp.Document` オブジェクトを持つレターを関連付けるレコードから成るマップです。 
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同期呼び出し {#asynchronous-invocations}

人間中心の長期間有効なプロセスのように、一部の AEM Forms サービスの完了には長い時間が必要です。これらのサービスは、非ブロッキング方式で非同期で呼び出すことができます。（[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

次の例で示されるように、AEM Forms サービスは、URL の呼び出しで `services` を `async_invoke` に置き換えることで非同期に呼び出すことができます。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

この URL は、この呼び出しをおこなうジョブの識別子の値（「text/plain」形式）を返します。

非同期呼び出しのステータスは、 URLの呼び出しを使用して `services` を `async_status` に置き換えることで取得できます。URL は、この呼び出しに関連付けられたジョブの識別子の値を指定する `job_id` パラメーターを含む必要があります。次に例を示します。

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

この URL は、ジョブマネージャの仕様に従ってジョブステータスをエンコードする整数値（「text/plain」形式）を返します（例えば、2 は実行、3 は完了、4 は失敗といった意味で）。

ジョブが完了した場合、URL は、サービスが同期的に呼び出された場合と同じ結果を返します。

ジョブが完了し、結果が取得されたら、 `services` を `async_dispose` で置き換えた呼び出し URL を使用してジョブを破棄できます。URL には、ジョブの識別子の値を指定するパラメーター `job_id` も含まれます。次に例を示します。

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

ジョブが正常に破棄された場合、この URL は空のメッセージを返します。

## エラーレポート {#error-reporting}

サーバーで例外が発生し、同期または非同期の呼び出し要求を完了できない場合、HTTP 応答メッセージの一部として例外がレポートされます。呼び出し URL（または非同期呼び出しの `async_result` URL の場合）に.xml サフィックスが付かない場合、REST プロバイダーは `500 Internal Server Error` HTTP コードを返し、続いて例外メッセージを返します。

呼び出し URL（または非同期呼び出しの `async_result` URL の場合）に.xml サフィックスが付いている場合、REST プロバイダーは `200 OK` HTTP コードを返し、続いて次の形式の例外を説明する XML ドキュメントを返します。

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

この `DSCError` 要素はオプションで、例外が`com.adobe.idp.dsc.DSCException`インスタンスの場合にのみ存在します。

## セキュリティと認証 {#security-and-authentication}

安全なトランスポートで REST の呼び出しを行うために、AEM Forms 管理者は、AEM Forms をホストする J2EE アプリケーションサーバーで HTTPS プロトコルを有効にすることができます。この設定は、J2EE アプリケーションサーバーに固有で、Forms サーバー設定には含まれていません。

>[!NOTE]
>
>REST エンドポイントを介してプロセスを公開する Workbench 開発者は、XSS の脆弱性の問題に注意してください。XSS 脆弱性は、Cookie の盗用や操作、コンテンツの表示の変更、機密情報の侵害に使用される可能性があります。XSS の脆弱性が問題となる場合は、入出力データ検証ルールを追加して、プロセスロジックを拡張することをお勧めします。

## REST 呼び出しをサポートする AEM Forms サービス {#aem-forms-services-that-support-rest-invocation}

サービスを直接呼び出すのではなく、Workbench を使用して作成したプロセスを呼び出すことをお勧めしますが、REST 呼び出しをサポートする AEM Forms サービスもいくつかあります。サービスを直接呼び出すよりも、プロセスを呼び出すことをお勧めする理由は、より効率的なためです。次のシナリオについて考えてみます。REST クライアントからポリシーを作成するとします。つまり、ポリシー名、オフラインリース期間などの値を、REST クライアントで定義する必要があります。

ポリシーを作成するには、`PolicyEntry` オブジェクトのような複雑なデータタイプを定義する必要があります。`PolicyEntry` オブジェクトは、ポリシーに関連付けられた権限などの属性を定義します。（[ポリシーの作成](/help/forms/developing/protecting-documents-policies.md#creating-policies)を参照してください。）

ポリシーを作成するための REST リクエストを送信するのではなく（これには `PolicyEntry` オブジェクトのような複雑なデータタイプを定義することも含まれます）、ポリシーを作成するプロセスを Workbench を使用して作成してください。プロセス名を定義する文字列値や、オフラインリース期間を定義する整数値など、プリミティブな入力変数を受け入れるプロセスを定義します。

これにより、操作で必要になる複雑なデータタイプを含む REST 呼び出しリクエストを作成する必要はなくなります。複雑なデータタイプを定義するのはプロセスであり、REST クライアントから行うのは、プロセスを呼び出してプリミティブなデータタイプを渡すことだけです。REST を使用したプロセスの呼び出しについて詳しくは、[REST を使用した MyApplication/EncryptDocument プロセスの呼び出し](#rest-invocation-examples)を参照してください。

REST の直接呼び出しをサポートする AEM Forms サービスのリストは、次のとおりです。

* Distiller サービス
* Rights Management サービス
* GeneratePDF サービス
* Generate3dPDF サービス
* FormDataIntegration

## REST 呼び出しの例 {#rest-invocation-examples}

REST 呼び出しの例は、次のとおりです。

* AEM Forms のプロセスにブール値を渡す
* AEM Forms のプロセスに日付値を渡す
* AEM Forms のプロセスにドキュメントを渡す
* AEM Forms のプロセスにドキュメントとテキスト値を渡す
* AEM Forms のプロセスに列挙値を渡す
* REST を使用した MyApplication/EncryptDocument プロセスの呼び出し
* Acrobat からの MyApplication/EncryptDocument プロセスの呼び出し

   各例では、AEM Forms のプロセスに様々なデータ型を渡す方法を示しています

**プロセスにブール値を渡す**

次の HTML の例では、`RestTest2` という名前の AEM Forms のプロセスに、2 つの `Boolean` 値を渡します。呼び出しメソッドの名前は `invoke` で、バージョンは 1.0 です。HTML Post メソッドが使用されています。

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

次の HTML の例では、`SOAPEchoService` という名前の AEM Forms のプロセスに日付値を渡します。呼び出しメソッドの名前は `echoCalendar` です。HTML `Post` メソッドが使用されています。

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

次の HTML の例では、PDF ドキュメントを必要とする `MyApplication/EncryptDocument` という名前の AEM Forms のプロセスを呼び出します。このプロセスについて詳しくは、[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)を参照してください。

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

**プロセスにドキュメントとテキスト値を渡す**

次の HTML の例では、1 つのドキュメントと 2 つのテキスト値を必要とする、`RestTest3` という名前の AEM Forms のプロセスを呼び出します。HTML Post メソッドが使用されています。

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

**プロセスに列挙値を渡す**

次の HTML の例では、列挙値を必要とする `SOAPEchoService` という名前の AEM Forms のプロセスを呼び出します。HTML Post メソッドが使用されています。

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

**REST を使用した MyApplication/EncryptDocument プロセスの呼び出し**

REST を使用すると、*MyApplication/EncryptDocument* という名前の短時間のみ有効な AEM Forms のプロセスを呼び出すことができます。

>[!NOTE]
>
>このプロセスは、AEM Forms の既存のプロセスに基づいたものではありません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

   このプロセスが REST リクエストを使用して呼び出されると、暗号化された PDF ドキュメントが web ブラウザーに表示されます。PDF ドキュメントを表示する前に、パスワードを指定します（セキュリティが無効になっていない場合）。次の HTML コードは、 `MyApplication/EncryptDocument` プロセスへの REST 呼び出しリクエストを表しています。

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

**Acrobat からの MyApplication/EncryptDocument プロセスの呼び出し** {#invoke-process-acrobat}

REST リクエストを使用して、Acrobat から Forms プロセスを呼び出すことができます。例えば、*MyApplication/EncryptDocument* プロセスを呼び出すことができます。Acrobat から Forms プロセスを呼び出すには、Designer 内の XDP ファイルに送信ボタンを配置します。（[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63_jp)を参照。）

次の図に示すように、ボタンの&#x200B;*送信先 URL*&#x200B;フィールド内でプロセスを呼び出す URL を指定します。

プロセスを呼び出すための完全な URL は https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument です。

プロセスで PDF ドキュメントを入力値として必要とする場合は、前の図に示すように、必ず PDF としてフォームを送信してください。また、プロセスを正常に呼び出すには、プロセスが PDF ドキュメントを返す必要があります。そうしないと、Acrobat は戻り値を処理できず、エラーが発生します。入力プロセス変数の名前を指定する必要はありません。例えば、*MyApplication/EncryptDocument* プロセスには、`inDoc` という入力変数があります。フォームが PDF として送信されている限り、inDoc を指定する必要はありません。

また、フォームデータを XML としても Forms プロセスに送信できます。XML データを送信する場合は `Submit As` ドロップダウンが XML を指定していることを確認してください。プロセスの戻り値は PDF ドキュメントである必要があるので、PDF ドキュメントは Acrobat に表示されます。
