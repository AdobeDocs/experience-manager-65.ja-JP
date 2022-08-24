---
title: サービスコンテナ
seo-title: Service container
description: サービスコンテナ内の AEM Forms サービス
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 100%

---

# サービスコンテナ {#service-container}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

サービスコンテナに配置された AEM Forms サービス（暗号化サービス、長期間有効なプロセス、短時間有効なプロセスなどの標準サービスを含む）は、EJB プロバイダーなどの様々なプロバイダーを使用して呼び出すことができます。EJB プロバイダーを使用すると、RMI/IIOP 経由で AEM Forms サービスを呼び出すことができます。Web サービスプロバイダーは、SOAP/HTTP や SOAP/JMS などの標準規格を使用して、web サービス（WSDL Generation）としてサービスを公開します。

次の表に、AEM Forms サービスをプログラムで呼び出す様々な方法を示します。

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
   <td><p>リモート統合により、Flex クライアントがサービス操作を呼び出す機能が提供されます。（<a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">（AEM Forms では非推奨）AEM Forms Remoting を使用した AEM Forms の呼び出し</a>を参照。）</p></td>
  </tr>
  <tr>
   <td><p>Java API</p></td>
   <td><p>Java API は、AEM Forms サービスを呼び出すことができます。Java API は、クライアントライブラリと Java Invocation API で構成されています。（<a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Java API を使用した AEM Forms の呼び出し</a>を参照。）</p></td>
  </tr>
  <tr>
   <td><p>Web サービス</p></td>
   <td><p>AEM Forms は、SOAP/HTTP などの web サービス標準規格をサポートしています。W3C で定義された web サービス標準規格に準拠した WSDL を使用して、サービスを web サービスとして公開できます。</p><p>サービスは、.NET Framework や Sun™ Web Services SDK など、任意の web サービススタックから呼び出すことができます。（<a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Web サービスを使用した AEM Forms の呼び出し</a>を参照。）</p></td>
  </tr>
  <tr>
   <td><p>REST リクエスト</p></td>
   <td><p>AEM Forms は、REST リクエストをサポートします。サービスは、HTML ページから直接呼出しできます。（<a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">REST リクエストを使用した AEM Forms の呼び出し</a>を参照。）</p></td>
  </tr>
 </tbody>
</table>

次の図は、AEM Forms サービスをプログラムで呼び出す様々な方法を視覚的に示しています。

>[!NOTE]
>
>AEM Forms SDK を使用して AEM Forms サービスを呼び出すクライアントアプリケーションを作成するほか、サービスコンテナにデプロイできるコンポーネントを作成することもできます。例えば、プロセスで使用できるカスタムデータタイプを含む Bank コンポーネントを作成できます。つまり、`com.adobe.idp.BankAccount` のようなデータタイプを作成できます。次に、クライアントアプリケーションで `com.adobe.idp.BankAccount` インスタンスを作成します。

サービスコンテナには次の機能が用意されています。

* 異なるメソッドを使用して AEM Forms サービスを呼び出すことを許可します。サービスを設定するには、エンドポイントを設定して、すべてのメソッド（Remoting、Java API、web サービスおよび REST）で呼び出せるようにします。（[プログラムによるエンドポイントの管理](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints)を参照）。
* メッセージを呼び出しリクエストと呼ばれる正規化された形式に変換します。呼び出しリクエストは、クライアントアプリケーション（または他のサービス）から、サービスコンテナ内のサービスに送信されます。呼び出しリクエストには、呼び出すサービスの名前や、操作の実行に必要なデータ値などの情報が含まれます。多くのサービスでは、操作を実行するためにドキュメントが必要です。したがって、呼び出しリクエストには通常、PDF データ、XDP データ、XML データなどのドキュメントが含まれます。
* 呼び出しリクエストを適切なサービスにルーティングします（呼び出すサービスの名前は呼び出しリクエストの一部です）。
* 呼び出し元が、指定されたサービス操作を呼び出す権限を持っているかどうかを判断するなどのタスクを実行します。呼び出しリクエストには、有効な AEM Forms のユーザー名とパスワードが含まれている必要があります。

   呼び出しリクエストをサービスに送信する方法は異なります。また、必要な入力値をサービスに送信する方法は異なります。例えば、Java API を使用して、PDF ドキュメントを必要とするサービスを呼び出すと仮定します。対応する Java メソッドには、PDF ドキュメントを受け入れるパラメーターが含まれています。この場合、パラメーターのデータタイプは `com.adobe.idp.Document` です。（[Java API を使用した AEM Forms サービスへのデータの引き渡し](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)を参照）。

   監視フォルダーを使用してサービスを呼び出すと、設定済みの監視フォルダーにファイルを配置すると、呼び出しリクエストが送信されます。メールを使用してサービスを呼び出す場合、メールメッセージが設定済みのインボックスに届くと、呼び出しリクエストがサービスに送信されます。

   サービスコンテナは、操作の実行後に呼び出し応答を返します。呼び出し応答には、操作の結果などの情報が含まれます。例えば、操作によって PDF ドキュメントが変更された場合、呼び出し応答には変更された PDF ドキュメントが含まれます。操作が失敗した場合、呼び出し応答にはエラーメッセージが含まれます。

   呼び出し応答は、呼び出し要求が送信されるのと同じ方法で取得できます。つまり、呼び出し要求が Java API を使用して送信された場合、呼び出し応答も Java API を使用して取得できます。例えば、操作によって PDF ドキュメントが変更されたとします。サービスを呼び出した Java メソッドの戻り値を取得することで、変更された PDF ドキュメントを取得できます。

   長期間有効なプロセスが呼び出されると、呼び出し応答には呼び出し要求に関連付けられた識別子の値が含まれます。この識別子の値を使用して、後でプロセスのステータスを確認できます。例えば、長期間有効なサービス MortgageLoan を考えてみましょう。識別子の値を使用して、プロセスが正常に完了したかどうかを確認できます。（[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください）。

   次の図は、サービスを呼び出すクライアントアプリケーション（Java API を使用）を示しています。

   クライアントアプリケーションがサービスを呼び出すと、次の 3 つのイベントが発生します。

   1. クライアントアプリケーションが呼び出し要求をサービスに送信します。
   1. サービスは、呼び出し要求で指定された操作を実行します。
   1. サービスコンテナは、クライアントアプリケーションに呼び出し応答を返します。

**関連トピック**

[AEM Forms プロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[（AEM Forms では非推奨 ）AEM Forms Remoting を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Java API を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[REST リクエストを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
