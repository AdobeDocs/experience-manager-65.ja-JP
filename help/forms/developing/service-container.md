---
title: サービスコンテナ
seo-title: サービスコンテナ
description: サービスコンテナにあるAEM Formsサービス
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 2%

---


# サービスコンテナ{#service-container}

**このドキュメントのサンプルと例は、JEE環境上のAEM Formsに対してのみ提供されています。**

サービスコンテナに配置されたAEM Formsサービス（Encryptionサービス、長期間有効なプロセス、短時間のみ有効なプロセスなどの標準サービスを含む）は、EJBプロバイダーなど、様々なプロバイダーを使用して呼び出すことができます。 EJBプロバイダーを使用すると、AEM FormsサービスをRMI/IIOP経由で呼び出すことができます。 Webサービスプロバイダーは、SOAP/HTTPやSOAP/JMSなどの標準を使用して、サービスをWebサービス（WSDL生成）として公開します。

次の表に、AEM Formsサービスをプログラムで呼び出す様々な方法を示します。

<table>
 <thead>
  <tr>
   <th><p>呼び出しメソッド</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>リモート統合</p></td>
   <td><p>リモート統合は、Flexクライアントがサービス操作を呼び出す機能を提供します。 (「<a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">AEM Formsリモートを使用したAEM Formsの呼び出し(AEM formsでは廃止)</a>」を参照)。</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java APIは、AEM Formsサービスを呼び出すことができます。 Java APIは、クライアントライブラリとJava Invocation APIにまとめられています。 (<a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Java APIを使用したAEM Formsの呼び出し</a>を参照)。</p></td>
  </tr>
  <tr>
   <td><p>Webサービス</p></td>
   <td><p>AEM Formsは、SOAP/HTTPなどのWebサービス標準をサポートしています。 W3Cで定義されるWebサービス標準に準拠したWSDLを使用して、サービスをWebサービスとして公開できます。</p><p>サービスは、.NET FrameworkやSun™ Web Services SDKなど、任意のWebサービススタックから呼び出すことができます。 (「<a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Webサービスを使用したAEM Formsの呼び出し</a>」を参照)。</p></td>
  </tr>
  <tr>
   <td><p>REST要求</p></td>
   <td><p>AEM FormsはREST要求をサポートします。 サービスは、HTMLページから直接呼び出すことができます。 (<a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">REST要求を使用したAEM Formsの呼び出し</a>を参照)。</p></td>
  </tr>
 </tbody>
</table>

次の図に、AEM Formsサービスをプログラムで呼び出す様々な方法を視覚的に示します。

>[!NOTE]
>
>AEM FormsSDKを使用して、AEM Formsサービスを呼び出すクライアントアプリケーションを作成するほか、サービスコンテナにデプロイできるコンポーネントを作成することもできます。 例えば、プロセスで使用できるカスタムデータ型を含むBankコンポーネントを作成できます。 つまり、`com.adobe.idp.BankAccount`などのデータ型を作成できます。 その後、`com.adobe.idp.BankAccount`インスタンスをクライアントアプリケーションに作成できます。

サービスコンテナには次の機能があります。

* 様々なメソッドを使用してAEM Formsサービスを呼び出すことを許可します。 エンドポイントを設定してサービスを設定し、すべてのメソッドを使用して呼び出せるようにします。リモート処理、Java API、WebサービスおよびREST。 （「[エンドポイントのプログラム管理](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)」を参照）。
* 呼び出し要求と呼ばれる正規化された形式にメッセージを変換します。 呼び出し要求がクライアントアプリケーション（または他のサービス）からサービスコンテナ内のサービスに送信されます。 呼び出し要求には、呼び出すサービスの名前や、操作の実行に必要なデータ値などの情報が含まれます。 多くのサービスでは、操作の実行にドキュメントが必要です。 したがって、呼び出し要求には通常、PDFデータ、XDPデータ、XMLデータなどのドキュメントが含まれます。
* 呼び出し要求を適切なサービスにルーティングします（呼び出すサービスの名前は、呼び出し要求の一部です）。
* 呼び出し元が、指定されたサービス操作を呼び出す権限を持っているかどうかを判断するなどのタスクを実行します。 呼び出し要求には、有効なAEM formsユーザー名とパスワードを含める必要があります。

   呼び出し要求をサービスに送信する方法は異なります。 また、必要な入力値をサービスに送信する方法も異なります。 例えば、Java APIを使用してPDFドキュメントを必要とするサービスを呼び出すとします。 対応するJavaメソッドには、PDFドキュメントを受け取るパラメータが含まれています。 この場合、パラメーターのデータ型は`com.adobe.idp.Document`です。 (「[Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)を使用してAEM Formsサービスにデータを渡す」を参照)。

   監視フォルダーを使用してサービスを呼び出す場合、設定済みの監視フォルダーにファイルを配置すると、呼び出し要求が送信されます。 電子メールを使用してサービスを呼び出す場合、設定済みのインボックスに電子メールメッセージが届くと、呼び出し要求がサービスに送信されます。

   サービスコンテナは、操作が実行されると呼び出し応答を返します。 呼び出し応答には、操作の結果などの情報が含まれます。 例えば、操作がPDFドキュメントを変更する場合、呼び出し応答には変更されたPDFドキュメントが含まれます。 操作に失敗した場合は、呼び出し応答にエラーメッセージが含まれます。

   呼び出し応答は、呼び出し要求が送信されるのと同じ方法で取得できます。 つまり、呼び出し要求がJava APIを使用して送信される場合、Java APIを使用して呼び出し応答を取得できます。 例えば、ある操作でPDFドキュメントが変更されたとします。 サービスを呼び出したJavaメソッドの戻り値を取得することで、変更されたPDFドキュメントを取得できます。

   長期間有効なプロセスが呼び出された場合、呼び出し応答には、呼び出し要求に関連付けられた識別子の値が含まれます。 この識別子の値を使用して、後でプロセスのステータスを確認できます。 例えば、MortgageLoanの長期間有効なサービスを考えてみましょう。 識別子の値を使用して、プロセスが正常に完了したかどうかを確認できます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

   次の図に、サービスを呼び出す（Java APIを使用する）クライアントアプリケーションを示します。

   クライアントアプリケーションがサービスを呼び出すと、次の3つのイベントが発生します。

   1. クライアントアプリケーションが呼び出し要求をサービスに送信します。
   1. サービスは、呼び出し要求で指定された操作を実行します。
   1. サービスコンテナは、クライアントアプリケーションに対する呼び出し応答を返します。

**関連トピック**

[AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[AEM Formsリモートを使用したAEM Formsの呼び出し(AEM formsでは廃止)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Java API を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[REST要求を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
