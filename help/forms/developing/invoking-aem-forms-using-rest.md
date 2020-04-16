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
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# REST要求を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-rest-requests}

Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST 要求は HTML ページから送信されます。つまり、REST要求を使用して、Webページから直接Formsプロセスを呼び出すことができます。 例えば、Webページの新しいインスタンスを開くことができます。 次に、Formsプロセスを呼び出し、HTTP POST要求で送信されたデータを含むレンダリングされたPDFドキュメントを読み込みます。

HTMLクライアントには2種類あります。 最初のHTMLクライアントは、JavaScriptで書き込まれるAJAXクライアントです。 2番目のクライアントは、送信ボタンを含むHTMLフォームです。 HTMLベースのクライアントアプリケーションだけがRESTクライアントとして使用できるわけではありません。 HTTP要求をサポートするクライアントアプリケーションは、REST呼び出しを使用してサービスを呼び出すことができます。 例えば、PDFフォームからREST呼び出しを使用してサービスを呼び出すことができます。 (Acrobatから [のMyApplication/EncryptDocumentプロセスの呼び出しを参照](#rest-invocation-examples))。

REST要求を使用する場合は、Formsサービスを直接呼び出さないことをお勧めします。 代わりに、Workbenchで作成されたプロセスを呼び出します。 REST呼び出し用のプロセスを作成する場合は、プログラム的な開始ポイントを使用します。 この場合、RESTエンドポイントが自動的に追加されます。 Workbenchでのプロセスの作成について詳しくは、「Workbenchの使用」を参 [照してくださ](https://www.adobe.com/go/learn_aemforms_workbench_63)い。

RESTを使用してサービスを呼び出すと、AEM formsのユーザー名とパスワードの入力を求められます。 ただし、ユーザー名とパスワードを指定しない場合は、サービスセキュリティを無効にできます。

RESTを使用してFormsサービスを呼び出す（プロセスがアクティブ化されると、プロセスはサービスになります）には、RESTエンドポイントを設定します。 (管理ヘルプの「エンドポイントの管理」 [を参照](https://www.adobe.com/go/learn_aemforms_admin_63))。

RESTエンドポイントの設定後、HTTP GETメソッドまたはPOSTメソッドを使用してFormsサービスを呼び出すことができます。

```as3
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

必須の値 `ServiceName` は、呼び出すFormsサービスの名前です。 オプション `OperationName` の値は、サービスの操作の名前です。 この値を指定しない場合、この名前はデフォルトで `invoke`プロセスを開始する操作名になります。 オプション `ServiceVersion` の値は、X.Y形式でエンコードされたバージョンです。 この値を指定しない場合は、最新のバージョンが使用されます。 値は、 `enctype` にすることもできま `application/x-www-form-urlencoded`す。

## サポートされるデータ型 {#supported-data-types}

REST要求を使用してAEM Formsサービスを呼び出す場合、次のデータ型がサポートされます。

* Javaプリミティブデータ型（文字列や整数など）
* `com.adobe.idp.Document` データ型
* やなどのXMLデータ型 `org.w3c.Document` 。 `org.w3c.Element`
* およびなどのコレクションオブジ `java.util.List` ェクト `java.util.Map`

   一般に、これらのデータ型は、Workbenchで作成されたプロセスの入力値として受け入れられます。

   HTTP POSTメソッドを使用してFormsサービスが呼び出された場合、引数はHTTP要求本文内で渡されます。 AEM Formsサービスの署名に文字列入力パラメーターがある場合、要求本文には入力パラメーターのテキスト値を含めることができます。 サービスの署名で複数の文字列パラメーターが定義されている場合、要求はHTTP表記の後に、フォームのフィールド名として使用さ `application/x-www-form-urlencoded` れるパラメーターの名前を付けることができます。

   Formsサービスが文字列パラメーターを返す場合、結果は出力パラメーターのテキスト表現になります。 サービスが複数の文字列パラメーターを返す場合、出力ドキュメントーを次の形式でエンコードしたXMLパラメーターが生成されます。
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >この値 `output-paramater1` は、出力パラメーター名を表します。

   Formsサービスにパラメーターが必要 `com.adobe.idp.Document` な場合、サービスはHTTP POSTメソッドを使用してのみ呼び出すことができます。 サービスに1つのパラメー `com.adobe.idp.Document` ターが必要な場合、HTTP要求の本文が入力パラメーターオブジェクトのドキュメントになります。

   AEM Formsサービスで複数の入力パラメーターが必要な場合、HTTP要求の本文は、RFC 1867で定義されているマルチパートMIMEメッセージである必要があります。 （RFC 1867は、WebブラウザーがファイルをWebサイトにアップロードする際に使用する標準です）。各入力パラメーターは、マルチパートメッセージの個別の部分として送信し、形式でエンコードする必要があ `multipart/form-data` ります。 各パーツの名前は、パラメータの名前と一致する必要があります。

   リストとマップは、Workbenchで作成されたAEM Formsプロセスへの入力値としても使用されます。 その結果、REST要求を使用する場合は、これらのデータ型を使用できます。 Java配列はAEM Formsプロセスの入力値として使用されないので、サポートされません。

   入力パラメーターがリストの場合、RESTクライアントは、リスト内の各項目に対して1回ずつパラメーターを複数回指定することで、パラメーターを送信できます。 例えば、Aがドキュメントのリストの場合、Aという名前の複数の部分から成るマルチパートメッセージを入力する必要があります。この場合、Aという名前の各部品は、入力アイテムになります。リスト Bが文字列のリストである場合、Bという名前の複数のフィールドで構成され `application/x-www-form-urlencoded` るメッセージを入力として使用できます。この場合、Bという名前の各フォームフィールドは、入力アイテムになります。リスト

   入力パラメーターがマップで、それがサービスのみの入力パラメーターである場合、入力メッセージのすべての部分/フィールドが、マップ内のキー/値レコードになります。 各パーツ/フィールドの名前がレコードのキーになります。 各パーツ/フィールドの内容がレコードの値になります。

   入力マップがサービスのみの入力パラメータでない場合、マップに属する各キー/値レコードは、パラメータ名とレコードのキーを連結した名前のパラメータを使用して送信できます。 例えば、という入力マップは、 `attributes` 次のキーと値のペアのリストと共に送信できます。

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   これは、次の3つのレコードのマップに変換されます。 `Color=red`、、 `Shape=box`および `Width=5`。

   出力パラメーターのリストとマップ型は、結果のXMLメッセージの一部になります。 出力リストは、XMLで一連のXML要素として表され、要素内の各項目に対して1つの要素が割り当てられます。リスト すべての要素には、出力パラメーターと同じ名前がリストされます。 各XML要素の値は、次の2つのいずれかになります。

* リスト内の項目のテキスト表現(リストが文字列型で構成される場合)
* ドキュメントのコンテンツを指すURL(リストがオブジェクトで構成されている `com.adobe.idp.Document` 場合)

   次の例は、整数のリストである **リストという名前の単一の出力パラメーターを持つサービスから返されるXMLメッセージです。
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`出力マップパラメーターは、結果のXMLメッセージ内で、マップ内の各レコードに対して1つの要素を持つ一連のXML要素として表されます。 すべての要素には、マップレコードのキーと同じ名前が付けられます。 各ドキュメントの値は、マップレコードの値のテキスト表現（マップが文字列値を持つレコードで構成される場合）または要素のコンテンツを指すURL（マップが値を持つレコードで構成される場合）のいずれかです。 `com.adobe.idp.Document` 次の例は、という名前の単一の出力パラメーターを持つサービスから返されるXMLメッセージの例で `map`す。 このパラメータ値は、レターをオブジェクトに関連付けるレコードで構成されるマップ `com.adobe.idp.Document` です。
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## 非同期呼び出し {#asynchronous-invocations}

人間中心の長期間有効なプロセスなど、一部のAEM Formsサービスの完了には長い時間が必要です。 これらのサービスは、非ブロック方式で非同期に呼び出すことができます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

次の例に示すように、AEM Formsサービスは、呼び出しURL `services` 内で `async_invoke` をに置き換えることで、非同期で呼び出すことができます。

```as3
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

このURLは、この呼び出しを行うジョブの識別子の値（「text/plain」形式）を返します。

非同期呼び出しのステータスは、で置換された呼び出しURLを使用して取得 `services` できま `async_status`す。 URLには、この呼び出しに関連付けら `job_id` れたジョブの識別子の値を指定するパラメーターが含まれている必要があります。 次に例を示します。

```as3
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

このURLは、ジョブマネージャーの仕様に従ってジョブステータスをエンコードする整数値（「text/plain」形式）を返します（例えば、2は実行中、3は完了、4は失敗など）。

ジョブが完了した場合、URLは、サービスが同期的に呼び出された場合と同じ結果を返します。

ジョブが完了し、結果が取得されると、呼び出しURLを使用してジョブを破棄し、に置き換え `services` ることができま `async_dispose`す。 URLには、ジョブの識別子の値を `job_id` 指定するパラメーターも含める必要があります。 次に例を示します。

```as3
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

ジョブが正常に破棄された場合、このURLは空のメッセージを返します。

## エラーレポート {#error-reporting}

サーバーで例外がスローされたために同期または非同期の呼び出し要求が完了しなかった場合、その例外はHTTP応答メッセージの一部としてレポートされます。 呼び出しURL(または非同期呼び出しの場合は `async_result` URL)に.xmlというサフィックスが付いていない場合、RESTプロバイダーはHTTPコードを返し、その後に例外メ `500 Internal Server Error` ッセージを返します。

呼び出しURL(または非同期呼び出しの場合は `async_result` URL)のサフィックスが.xmlである場合、RESTプロバイダーはHTTPコードの後に、次の形式で例外を説明する `200 OK`XMLドキュメントを返します。

```as3
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

この要 `DSCError` 素はオプションで、例外がのインスタンスの場合にのみ存在しま `com.adobe.idp.dsc.DSCException`す。

## セキュリティと認証 {#security-and-authentication}

安全なトランスポートでREST呼び出しを行うために、AEM Forms管理者は、AEM FormsをホストするJ2EEアプリケーションサーバーでHTTPSプロトコルを有効にできます。 この設定は、J2EEアプリケーションサーバーに固有のものです。formsサーバー設定の一部ではありません。

>[!NOTE]
>
>RESTエンドポイントを通じてプロセスを公開するWorkbench開発者の場合は、XSSの脆弱性の問題に注意してください。 XSS脆弱性は、cookieの盗用や操作、コンテンツの表示の変更、機密情報の漏洩などに使用できます。 XSSの脆弱性が問題となる場合は、追加の入出力データ検証ルールを使用してプロセスロジックを拡張することをお勧めします。

## REST呼び出しをサポートするAEM Formsサービス {#aem-forms-services-that-support-rest-invocation}

サービスを直接呼び出すのではなく、Workbenchを使用して作成したプロセスを呼び出すことをお勧めしますが、REST呼び出しをサポートするAEM Formsサービスがいくつかあります。 サービスを直接呼び出すのではなく、プロセスを直接呼び出すことをお勧めするのは、プロセスを呼び出す方が効率的なためです。 次のシナリオを考えてみましょう。 RESTクライアントからポリシーを作成するとします。 つまり、RESTクライアントでポリシー名やオフラインリース期間などの値を定義する必要があります。

ポリシーを作成するには、オブジェクトなどの複雑なデータ型を定義する必要があ `PolicyEntry` ります。 オブジェ `PolicyEntry` クトは、ポリシーに関連付けられた権限などの属性を定義します。 (ポリシー [の作成を参照](/help/forms/developing/protecting-documents-policies.md#creating-policies))。

ポリシーを作成するREST要求（オブジェクトなどの複雑なデータ型の定義を含む）を送信する代わりに、Workbenchを使用してポリシーを作成するプロセスを作成します。 `PolicyEntry` プロセス名を定義する文字列値や、オフラインリース期間を定義する整数など、プリミティブ入力変数を受け入れるプロセスを定義します。

この方法では、操作に必要な複雑なデータ型を含むREST呼び出し要求を作成する必要はありません。 プロセスでは複雑なデータ型が定義され、RESTクライアントから実行する操作は、プロセスを呼び出してプリミティブデータ型を渡すことです。 RESTを使用したプロセスの呼び出しについて詳しくは、RESTを使用したMyApplication/EncryptDocument [プロセスの呼び出しを参照してください](#rest-invocation-examples)。

次のリストでは、直接REST呼び出しをサポートするAEM Formsサービスを指定します。

* Distiller サービス[Distiller さーびす]
* Rights Management サービス[Rights Management さーびす]
* GeneratePDFサービス
* Generate3dPDFサービス
* FormDataIntegration

## REST呼び出しの例 {#rest-invocation-examples}

次のREST呼び出しの例を示します。

* AEM Formsプロセスへのブール値の渡し
* AEM Formsプロセスへの日付値の渡し
* AEM Formsプロセスへのドキュメントの引き渡し
* AEM Formsプロセスへのドキュメント値とテキスト値の受け渡し
* AEM Formsプロセスへの定義済みリスト値の受け渡し
* RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し
* AcrobatからのMyApplication/EncryptDocumentプロセスの呼び出し

   各例では、様々なデータ型をAEM Formsプロセスに渡す方法を示します。

**プロセスにブール値を渡す**

次のHTMLの例では、2つの値を `Boolean` という名前のAEM Formsプロセスに渡しま `RestTest2`す。 呼び出しメソッドの名前はで `invoke` 、バージョンは1.0です。HTML Postメソッドが使用されます。

```as3
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

次のHTMLの例では、という名前のAEM Formsプロセスに日付値を渡していま `SOAPEchoService`す。 呼び出しメソッドの名前はです `echoCalendar`。 HTMLメソッドが使用さ `Post` れていることに注意してください。

```as3
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**プロセスへのドキュメントの引き渡し**

次のHTMLの例は、PDFプロセスを必要とするAEM Formsプロ `MyApplication/EncryptDocument` セスを呼び出します。ドキュメント このプロセスに関する詳細は、「MTOMを使用したAEM [Formsの呼び出し」を参照してください](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)。

```as3
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

**ドキュメント値とテキスト値をプロセスに渡す**

次のHTMLの例は、1つのテキストと2つのテキスト値を必要とする、とい `RestTest3` う名前のAEM Formsドキュメントを呼び出します。 HTML Postメソッドが使用されます。

```as3
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

**プロセスへの定義済みリスト値の受け渡し**

次のHTMLの例は、名前に定義済みリスト値が必要なAEM Formsプロセス `SOAPEchoService` を呼び出します。 HTML Postメソッドが使用されます。

```as3
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

RESTを使用して、 *MyApplication/EncryptDocumentという名前のAEM Formsの短時間のみ有効なプロセスを呼び出すことができます* 。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。To follow along with the code example, create a process named `MyApplication/EncryptDocument` using workbench. （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

   REST要求を使用してこのプロセスを呼び出すと、暗号化されたPDFドキュメントがWebブラウザーに表示されます。 PDFドキュメントを表示する前に、パスワードを指定します（セキュリティが無効になっている場合を除く）。 次のHTMLコードは、プロセスに対するREST呼び出し要求を表し `MyApplication/EncryptDocument` ています。

   ```as3
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

**AcrobatからのMyApplication/EncryptDocumentプロセスの呼び出し**{#invoke-process-acrobat}

REST要求を使用して、AcrobatからFormsプロセスを呼び出すことができます。 例えば、MyApplication/EncryptDocumentプロセスを呼び出す *ことができます* 。 AcrobatからFormsプロセスを呼び出すには、Designer内のXDPファイルに送信ボタンを配置します。 （「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照）。

次の図に示すように、ボタンの「 *Submit to URL* 」フィールド内でプロセスを呼び出すURLを指定します。

プロセスを呼び出すための完全なURLはhttps://hiro-xp:8080/rest/services/MyApplication/EncryptDocumentです。

プロセスで入力値としてPDFドキュメントが必要な場合は、前の図に示すように、フォームをPDFとして送信します。 また、プロセスを正常に呼び出すには、プロセスがPDFドキュメントを返す。 そうでない場合、Acrobatは戻り値を処理できず、エラーが発生します。 入力プロセス変数の名前を指定する必要はありません。 例えば、MyApplication/EncryptDocument *プロセスには* 、という名前の入力変数がありま `inDoc`す。 フォームがPDFとして送信される限り、inDocを指定する必要はありません。

また、フォームデータをXMLとしてFormsプロセスに送信することもできます。XMLデータを送信するには、ドロップダウンでXMLが指定さ `Submit As` れていることを確認します。 プロセスの戻り値はPDFドキュメントである必要があるので、PDFドキュメントはAcrobatで表示されます。
