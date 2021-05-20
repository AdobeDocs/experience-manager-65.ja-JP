---
title: REST要求を使用したAEM Formsの呼び出し
seo-title: REST要求を使用したAEM Formsの呼び出し
description: RESTリクエストを使用して、Workbenchで作成されたプロセスを呼び出します。
seo-description: RESTリクエストを使用して、Workbenchで作成されたプロセスを呼び出します。
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 4%

---

# RESTリクエスト{#invoking-aem-forms-using-rest-requests}を使用したAEM Formsの呼び出し

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST 要求は HTML ページから送信されます。つまり、RESTリクエストを使用して、Webページから直接Formsプロセスを呼び出すことができます。 例えば、Webページの新しいインスタンスを開くことができます。 次に、 Formsプロセスを呼び出し、HTTPPOST要求で送信されたデータを含む、レンダリングされたPDFドキュメントを読み込むことができます。

2種類のHTMLクライアントが存在します。 最初のHTMLクライアントは、JavaScriptで記述されるAJAXクライアントです。 2番目のクライアントは、送信ボタンを含むHTMLフォームです。 HTMLベースのクライアントアプリケーションは、RESTクライアントとしてのみ使用できるわけではありません。 HTTP要求をサポートするクライアントアプリケーションは、REST呼び出しを使用してサービスを呼び出すことができます。 例えば、PDFフォームからのREST呼び出しを使用してサービスを呼び出すことができます。 ([Acrobat](#rest-invocation-examples)からのMyApplication/EncryptDocumentプロセスの呼び出しを参照)。

RESTリクエストを使用する場合、Formsサービスを直接呼び出さないことをお勧めします。 代わりに、Workbenchで作成されたプロセスを呼び出します。 REST呼び出し用のプロセスを作成する場合は、プログラム的なスタートポイントを使用します。 この場合、RESTエンドポイントは自動的に追加されます。 Workbenchでのプロセスの作成について詳しくは、[Workbenchの使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。

RESTを使用してサービスを呼び出すと、AEM formsのユーザー名とパスワードの入力を求められます。 ただし、ユーザー名とパスワードを指定しない場合は、サービスセキュリティを無効にできます。

RESTを使用してFormsサービスを呼び出す（プロセスがアクティブ化されるとプロセスがサービスになる）には、RESTエンドポイントを設定します。 （[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63)の「エンドポイントの管理」を参照）。

RESTエンドポイントが設定されたら、HTTPGETメソッドまたはPOSTメソッドを使用してFormsサービスを呼び出すことができます。

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必須の`ServiceName`値は、呼び出すFormsサービスの名前です。 オプションの`OperationName`値は、サービスの操作の名前です。 この値を指定しない場合、この名前はデフォルトで`invoke`になり、プロセスを開始する操作名になります。 オプションの`ServiceVersion`値は、X.Y形式でエンコードされたバージョンです。 この値を指定しない場合は、最新のバージョンが使用されます。 `enctype`の値は`application/x-www-form-urlencoded`にすることもできます。

## サポートされているデータ型{#supported-data-types}

REST要求を使用してAEM Formsサービスを呼び出す場合、次のデータ型がサポートされます。

* 文字列や整数などのJavaプリミティブデータ型
* `com.adobe.idp.Document` データタイプ
* `org.w3c.Document`や`org.w3c.Element`などのXMLデータ型
* `java.util.List`や`java.util.Map`などのコレクションオブジェクト

   これらのデータ型は、通常、Workbenchで作成されるプロセスへの入力値として受け入れられます。

   HTTPリクエストメソッドを使用してFormsサービスが呼び出された場合、POSTはHTTPリクエスト本文内で渡されます。 AEM Formsサービスの署名に文字列入力パラメーターがある場合、リクエスト本文には入力パラメーターのテキスト値を含めることができます。 サービスの署名で複数の文字列パラメーターが定義されている場合、リクエストはHTTPの`application/x-www-form-urlencoded`表記に従い、フォームのフィールド名にパラメーター名を使用できます。

   Formsサービスが文字列パラメーターを返す場合、結果は出力パラメーターのテキスト表現になります。 サービスが複数の文字列パラメーターを返す場合、結果は次の形式で出力パラメーターをエンコードするXMLドキュメントになります。
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >`output-paramater1`値は、出力パラメーター名を表します。

   Formsサービスに`com.adobe.idp.Document`パラメーターが必要な場合、サービスを呼び出すにはHTTPPOSTメソッドを使用する必要があります。 サービスに1つの`com.adobe.idp.Document`パラメーターが必要な場合、HTTPリクエスト本文が入力Documentオブジェクトのコンテンツになります。

   AEM Formsサービスで複数の入力パラメーターが必要な場合、HTTPリクエスト本文は、RFC 1867で定義されているマルチパートMIMEメッセージである必要があります。 （RFC 1867は、WebブラウザーでファイルをWebサイトにアップロードする際に使用される標準です）。 各入力パラメーターは、マルチパートメッセージの別の部分として送信し、`multipart/form-data`形式でエンコードする必要があります。 各パーツの名前は、パラメータの名前と一致する必要があります。

   リストとマップは、Workbenchで作成されたAEM Formsプロセスへの入力値としても使用されます。 その結果、RESTリクエストを使用する際に、これらのデータ型を使用できます。 Java配列は、AEM Formsプロセスの入力値として使用されないので、サポートされていません。

   入力パラメーターがリストの場合、RESTクライアントは、パラメーターを複数回指定して（リスト内の項目ごとに1回）送信できます。 例えば、Aがドキュメントのリストの場合、入力はAという名前の複数のパーツで構成されるマルチパートメッセージである必要があります。この場合、Aという名前の各パーツが入力リストのアイテムになります。 Bが文字列のリストの場合、入力は、Bという名前の複数のフィールドで構成される`application/x-www-form-urlencoded`メッセージにすることができます。この場合、Bという名前の各フォームフィールドは、入力リストの項目になります。

   入力パラメーターがマップで、それがサービスのみの入力パラメーターである場合、入力メッセージのすべての部分/フィールドがマップ内のキー/値レコードになります。 各パーツ/フィールドの名前が、レコードのキーになります。 各パーツまたはフィールドの内容が、レコードの値になります。

   入力マップがサービスのみの入力パラメータではない場合、マップに属する各キー/値レコードは、パラメータ名とレコードのキーを連結した、という名前のパラメータを使用して送信できます。 例えば、`attributes`という入力マップを、次のキーと値のペアのリストと共に送信できます。

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   これは、次の3つのレコードのマップに変換されます。`Color=red`、`Shape=box`、および`Width=5`。

   list型とmap型の出力パラメーターは、結果のXMLメッセージの一部になります。 出力リストは、一連のXML要素としてXML形式で表され、リスト内の項目ごとに1つの要素が割り当てられます。 すべての要素には、出力リストパラメーターと同じ名前が付けられます。 各XML要素の値は、次の2つのいずれかになります。

* リスト内の項目のテキスト表現（リストが文字列型で構成されている場合）
* ドキュメントのコンテンツを指すURL（リストが`com.adobe.idp.Document`オブジェクトで構成されている場合）

   次の例は、*list*という名前の単一の出力パラメーター（整数のリスト）を持つサービスから返されるXMLメッセージです。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`結果のXMLメッセージ内に出力マップパラメーターが、マップ内の各レコードに対して1つの要素を持つ一連のXML要素として表されます。すべての要素には、マップレコードのキーと同じ名前が付けられます。 各要素の値は、マップレコードの値（マップが文字列値のレコードで構成される場合）のテキスト表現か、ドキュメントのコンテンツを指すURL（マップが`com.adobe.idp.Document`値のレコードで構成される場合）のいずれかです。 次に、`map`という名前の出力パラメーターが1つだけあるサービスから返されるXMLメッセージの例を示します。 このパラメータ値は、レターを`com.adobe.idp.Document`オブジェクトに関連付けるレコードで構成されるマップです。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同期呼び出し{#asynchronous-invocations}

人間中心の長期間有効なプロセスなど、一部のAEM Formsサービスの完了に長い時間が必要です。 これらのサービスは、非ブロック方式で非同期で呼び出すことができます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

次の例に示すように、AEM Formsサービスは、呼び出しURLで`services`を`async_invoke`に置き換えることで、非同期で呼び出すことができます。

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

このURLは、この呼び出しを担当するジョブの識別子の値（「text/plain」形式）を返します。

非同期呼び出しのステータスは、`services`を`async_status`に置き換えた呼び出しURLを使用して取得できます。 URLには、この呼び出しに関連付けられたジョブの識別子の値を指定する`job_id`パラメーターが含まれている必要があります。 以下に例を示します。

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

このURLは、ジョブマネージャーの仕様に従ってジョブステータスをエンコードする整数値（「text/plain」形式）を返します（例えば、2は実行中、3は完了、4は失敗など）。

ジョブが完了した場合、URLは、サービスが同期的に呼び出された場合と同じ結果を返します。

ジョブが完了し、結果が取得されたら、呼び出しURLを`services`で置き換えて`async_dispose`を使用してジョブを破棄できます。 URLには、ジョブの識別子の値を指定する`job_id`パラメーターも含める必要があります。 以下に例を示します。

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

ジョブが正常に破棄された場合、このURLは空のメッセージを返します。

## エラー報告{#error-reporting}

サーバーで例外がスローされたために同期または非同期の呼び出し要求を完了できない場合は、HTTP応答メッセージの一部として例外がレポートされます。 呼び出しURL（または非同期呼び出しの場合は`async_result` URL）に.xmlサフィックスが付かない場合、RESTプロバイダーはHTTPコード`500 Internal Server Error`の後に例外メッセージを返します。

呼び出しURL（または非同期呼び出しの場合は`async_result` URL）に.xmlサフィックスが付いている場合、RESTプロバイダーはHTTPコード`200 OK`の後に、次の形式の例外を記述したXMLドキュメントを返します。

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

`DSCError`要素はオプションで、例外が`com.adobe.idp.dsc.DSCException`のインスタンスの場合にのみ存在します。

## セキュリティと認証{#security-and-authentication}

安全なトランスポートでRESTの呼び出しを行うために、AEM forms管理者は、AEM FormsをホストするJ2EEアプリケーションサーバー上でHTTPSプロトコルを有効にできます。 この設定は、J2EEアプリケーションサーバーに固有です。formsサーバー設定に含まれていません。

>[!NOTE]
>
>RESTエンドポイントを通じてプロセスを公開するWorkbench開発者は、XSSの脆弱性の問題に注意してください。 XSS脆弱性は、Cookieの盗用や操作、コンテンツの表示の変更、機密情報の漏洩などに利用できます。 XSSの脆弱性が問題の場合は、追加の入出力データ検証ルールを使用してプロセスロジックを拡張することをお勧めします。

## REST呼び出し{#aem-forms-services-that-support-rest-invocation}をサポートするAEM Formsサービス

Workbenchを使用して作成したプロセスを直接呼び出すのではなく、Workbenchを使用して作成したプロセスを直接呼び出すことをお勧めしますが、REST呼び出しをサポートするAEM Formsサービスがいくつかあります。 サービスとは異なり、プロセスを直接呼び出すことをお勧めする理由は、プロセスを呼び出す方がより効率的なためです。 次のシナリオについて考えてみましょう。 RESTクライアントからポリシーを作成するとします。 つまり、RESTクライアントで、ポリシー名、オフラインリース期間などの値を定義する必要があります。

ポリシーを作成するには、`PolicyEntry`オブジェクトなどの複雑なデータ型を定義する必要があります。 `PolicyEntry`オブジェクトは、ポリシーに関連付けられた権限などの属性を定義します。 （[ポリシーの作成](/help/forms/developing/protecting-documents-policies.md#creating-policies)を参照）。

ポリシーを作成するRESTリクエストを送信する代わりに（`PolicyEntry`オブジェクトなどの複雑なデータ型の定義を含む）、Workbenchを使用してポリシーを作成するプロセスを作成します。 プロセス名を定義する文字列値や、オフラインリース期間を定義する整数など、プリミティブ入力変数を受け入れるプロセスを定義します。

この方法を使用すると、操作に必要な複雑なデータ型を含むREST呼び出しリクエストを作成する必要がなくなります。 プロセスは複雑なデータ型を定義し、RESTクライアントから実行する操作は、プロセスを呼び出してプリミティブデータ型を渡すことだけです。 RESTを使用したプロセスの呼び出しについて詳しくは、[REST](#rest-invocation-examples)を使用したMyApplication/EncryptDocumentプロセスの呼び出しを参照してください。

次のリストは、直接REST呼び出しをサポートするAEM Formsサービスを指定します。

* Distiller サービス[Distiller さーびす]
* Rights Management サービス[Rights Management さーびす]
* GeneratePDFサービス
* Generate3dPDFサービス
* FormDataIntegration

## REST呼び出しの例{#rest-invocation-examples}

次のREST呼び出し例が提供されています。

* AEM Formsプロセスにブール値を渡す
* AEM Formsプロセスへの日付値の渡し
* ドキュメントをAEM Formsプロセスに渡す
* AEM Formsプロセスへのドキュメントとテキスト値の渡し
* AEM Formsプロセスへの列挙値の引き渡し
* RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し
* AcrobatからのMyApplication/EncryptDocumentプロセスの呼び出し

   各例は、様々なデータ型をAEM Formsプロセスに渡す方法を示しています

**プロセスにブール値を渡す**

次のHTMLの例では、2つの`Boolean`値を`RestTest2`という名前のAEM Formsプロセスに渡します。 呼び出しメソッドの名前は`invoke`で、バージョンは1.0です。HTML Postメソッドが使用されていることに注意してください。

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

**プロセスへの日付値の渡し**

次のHTMLの例では、`SOAPEchoService`という名前のAEM Formsプロセスに日付値を渡します。 呼び出しメソッドの名前は`echoCalendar`です。 HTMLの`Post`メソッドが使用されています。

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

次のHTMLの例は、PDFドキュメントを必要とする`MyApplication/EncryptDocument`という名前のAEM Formsプロセスを呼び出します。 このプロセスについて詳しくは、[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)を参照してください。

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

**プロセスへのドキュメントとテキスト値の渡し**

次のHTMLの例は、ドキュメントと2つのテキスト値を必要とする`RestTest3`という名前のAEM Formsプロセスを呼び出します。 HTML Postメソッドが使用されています。

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

**プロセスへの列挙値の引き渡し**

次のHTMLの例は、列挙値が必要な`SOAPEchoService`という名前のAEM Formsプロセスを呼び出します。 HTML Postメソッドが使用されています。

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

RESTを使用して、*MyApplication/EncryptDocument*&#x200B;という名前のAEM Formsの短時間のみ有効なプロセスを呼び出すことができます。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。コード例に従うには、workbenchを使用して`MyApplication/EncryptDocument`という名前のプロセスを作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

   このプロセスがREST要求を使用して呼び出されると、暗号化されたPDFドキュメントがWebブラウザーに表示されます。 PDFドキュメントを表示する前に、パスワードを指定します（セキュリティが無効になっている場合を除く）。 次のHTMLコードは、`MyApplication/EncryptDocument`プロセスに対するREST呼び出し要求を表しています。

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

RESTリクエストを使用して、AcrobatからFormsプロセスを呼び出すことができます。 例えば、*MyApplication/EncryptDocument*&#x200B;プロセスを呼び出すことができます。 AcrobatからFormsプロセスを呼び出すには、Designer内のXDPファイルに送信ボタンを配置します。 （「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照）。

次の図に示すように、ボタンの「*Submit to URL*」フィールド内でプロセスを呼び出すURLを指定します。

プロセスを呼び出すための完全なURLはhttps://hiro-xp:8080/rest/services/MyApplication/EncryptDocumentです。

プロセスの入力値としてPDFドキュメントが必要な場合は、前の図に示すように、必ずPDFとしてフォームを送信してください。 また、プロセスを正常に呼び出すには、プロセスがPDFドキュメントを返す必要があります。 そうしないと、Acrobatは戻り値を処理できず、エラーが発生します。 入力プロセス変数の名前を指定する必要はありません。 例えば、*MyApplication/EncryptDocument*&#x200B;プロセスには、`inDoc`という名前の入力変数があります。 フォームがPDFとして送信されている限り、inDocを指定する必要はありません。

また、フォームデータをXMLとしてFormsプロセスに送信する場合も、XMLデータを送信するには、`Submit As`ドロップダウンでXMLを指定します。 プロセスの戻り値はPDFドキュメントにする必要があるので、PDFドキュメントはAcrobatに表示されます。
