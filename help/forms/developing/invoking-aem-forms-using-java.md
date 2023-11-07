---
title: Java API を使用した AEM Forms の呼び出し
description: リモート呼び出しのための RMI トランスポートプロトコルの AEM Forms Java API、ローカル呼び出しのための VM トランスポート、リモート呼び出しのための SOAP、ユーザー名とパスワードなどの他の認証方法、同期および非同期の呼び出し要求を使用します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '5393'
ht-degree: 47%

---

# Java API を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-the-javaapi}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

AEM Formsは、AEM Forms Java API を使用して呼び出すことができます。 AEM Forms Java API を使用する場合は、呼び出し API または Java クライアントライブラリを使用できます。 Java クライアントライブラリは、Java サービスなどのサービスで使用できます。Rights Managementサービス。 これらの強く型指定された API を使用すると、AEM Formsを呼び出す Java アプリケーションを開発できます。

呼び出し API は、 `com.adobe.idp.dsc` パッケージ。 これらのクラスを使用すると、呼び出し要求をサービスに直接送信し、返された呼び出し応答を処理できます。 呼び出し API を使用して、Workbench を使用して作成された短時間のみ有効なプロセスまたは長時間有効なプロセスを呼び出します。

サービスをプログラムで呼び出す方法として、呼び出し API とは異なり、サービスに対応する Java クライアントライブラリを使用することをお勧めします。 例えば、Encryption サービスを呼び出すには、Encryption サービスのクライアントライブラリを使用します。 Encryption サービス操作を実行するには、Encryption サービスクライアントオブジェクトに属するメソッドを呼び出します。 を呼び出すことで、PDFドキュメントをパスワードで暗号化できます。 `EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッド。

Java API は、次の機能をサポートしています。

* リモート呼び出し用の RMI トランスポートプロトコル
* ローカル呼び出し用の VM トランスポート
* リモート呼び出し用の SOAP
* ユーザー名やパスワードなど、異なる認証
* 同期呼び出しリクエストと非同期呼び出しリクエスト

[AEM Forms Java ライブラリファイルを含める](#including-aem-forms-java-library-files)

[人間中心の長期間有効なプロセスの呼び出し](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md)

[接続プロパティの設定](#setting-connection-properties)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](#invoking-a-service-using-a-java-client-library)

[呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](#invoking-a-short-lived-process-using-the-invocation-api)

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md)

## AEM Forms の Java ライブラリファイルを含める {#including-aem-forms-java-library-files}

Java API を使用してAEM Formsサービスをプログラムで呼び出すには、Java プロジェクトのクラスパスに必要なライブラリファイル（JAR ファイル）を含めます。 クライアントアプリケーションのクラスパスに含める JAR ファイルは、次の要因によって異なります。

* 呼び出すAEM Formsサービス。 クライアントアプリケーションは、1 つ以上のサービスを呼び出すことができます。
* AEM Formsサービスを呼び出すモードです。 EJB または SOAP モードを使用できます。 （[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照）

>[!NOTE]
>
>（自動オプションのみ）EJB 用のサーバー IP を指定するには、コマンド `standalone.bat -b <Server IP> -c lc_turnkey.xml` を使用して AEM Forms サーバーを起動します。

* AEM Formsがデプロイされている J2EE アプリケーションサーバー。

### サービス固有の JAR ファイル {#service-specific-jar-files}

次の表に、AEM Formsサービスを呼び出すために必要な JAR ファイルを示します。

<table>
 <thead>
  <tr>
   <th><p>ファイル</p></th>
   <th><p>説明</p></th>
   <th><p>場所</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Java クライアントアプリケーションのクラスパスに常に含める必要があります。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Java クライアントアプリケーションのクラスパスに常に含める必要があります。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Java クライアントアプリケーションのクラスパスに常に含める必要があります。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Application Manager サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Assembler サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>バックアップおよび復元サービス API を呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>バーコードフォームサービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Convert Convert サービスを呼び出すために必要なPDFです。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Distillerサービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>DocConverter サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Document Management サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Encryption サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Formsサービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Form Data Integration サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Generate Generate サービスを呼び出すために必要なPDFです。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Generate 3DPDFサービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Job Manager サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Output サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Utilities またはXMP Utilities サービスを呼び出すためにPDFが必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Acrobat Reader DC Extensions サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Repository サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs\thirparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Rights Managementサービスを呼び出すために必要です。</p><p>AEM Formsが JBoss にデプロイされている場合は、これらのファイルをすべて含めます。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p><p>JBoss 固有の lib ディレクトリ</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Signature サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Task Manager サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Trust Store サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 接続モードと J2EE アプリケーション JAR ファイル {#connection-mode-and-j2ee-application-jar-files}

次の表に、接続モードと、AEM Formsをデプロイする J2EE アプリケーションサーバーに依存する JAR ファイルを示します。

<table>
 <thead>
  <tr>
   <th><p>ファイル</p> </th>
   <th><p>説明</p> </th>
   <th><p>場所</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>AEM Formsが SOAP モードを使用して呼び出された場合は、次の JAR ファイルを含めます。</p> </td>
   <td><p>&lt;<em>インストールディレクトリ</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>AEM Forms が JBoss Application Server 上にデプロイされている場合は、この JAR ファイルを含めます。</p> <p>jboss-client.jar と参照先の jar ファイルが同じ場所にない場合、クラスローダーは必要なクラスを見つけることができません。</p> </td>
   <td><p>JBoss クライアントライブラリディレクトリ</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバーにデプロイする場合は、このファイルを含める必要はありません。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>AEM Formsが BEA WebLogic Server®にデプロイされている場合は、この JAR ファイルを含めます。</p> </td>
   <td><p>WebLogic 固有の lib ディレクトリ</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバーにデプロイする場合は、このファイルを含める必要はありません。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>AEM Formsが WebSphere Application Server にデプロイされている場合は、次の JAR ファイルを含めます。</p> </li>
     <li><p>(Web サービスの呼び出しにはcom.ibm.ws.webservices.thinclient_6.1.0.jar が必要です )。</p> </li>
    </ul> </td>
   <td><p>WebSphere 固有の lib ディレクトリ (<em>[WAS_HOME]</em>/runtimes)</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバーにデプロイする場合は、これらのファイルを含める必要はありません。</p> </td>
  </tr>
 </tbody>
</table>

### シナリオの呼び出し {#invoking-scenarios}

次の表に、呼び出しシナリオを示し、AEM Formsを正常に呼び出すために必要な JAR ファイルを示します。

<table>
 <thead>
  <tr>
   <th><p>サービス</p> </th>
   <th><p>呼び出しモード</p> </th>
   <th><p>J2EE アプリケーションサーバー</p> </th>
   <th><p>必要な JAR ファイル</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Formsサービス</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formsサービス</p> <p>Acrobat Reader DC Extensions サービス</p> <p>Signature サービス</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formsサービス</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Formsサービス</p> <p>Acrobat Reader DC Extensions サービス</p> <p>Signature サービス</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### JAR ファイルのアップグレード {#upgrading-jar-files}

LiveCycleからAEM Formsにアップグレードする場合は、AEM Forms JAR ファイルを Java プロジェクトのクラスパスに含めることをお勧めします。 例えば、Rights Managementサービスなどのサービスを使用している場合、クラスパスにAEM Forms JAR ファイルを含めないと、互換性の問題が発生します。

AEM Formsにアップグレードすると仮定します。 Rights Managementサービスを呼び出す Java アプリケーションを使用するには、次の JAR ファイルのAEM Formsバージョンを含めます。

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 接続プロパティの設定 {#setting-connection-properties}

Java API を使用する場合は、接続プロパティを設定してAEM Formsを呼び出します。 接続プロパティを設定する場合は、サービスをリモートで呼び出すかローカルで呼び出すかを指定し、接続モードと認証値も指定します。 サービスセキュリティが有効な場合は、認証値が必要です。 ただし、サービスセキュリティが無効の場合は、認証値を指定する必要はありません。

接続モードは、SOAP モードまたは EJB モードのいずれかです。 EJB モードは RMI/IIOP プロトコルを使用し、EJB モードのパフォーマンスは SOAP モードのパフォーマンスよりも優れています。 SOAP モードは、J2EE アプリケーションサーバーの依存関係をなくすため、またはファイアウォールがAEM Formsとクライアントアプリケーションの間に配置されている場合に使用します。 SOAP モードでは、https プロトコルが基になるトランスポートとして使用され、ファイアウォール境界を越えて通信できます。 J2EE アプリケーションサーバーの依存関係もファイアウォールも問題にならない場合は、EJB モードを使用することをお勧めします。

AEM Formsサービスを正常に呼び出すには、次の接続プロパティを設定します。

* **DSC_DEFAULT_EJB_ENDPOINT:** EJB 接続モードを使用している場合、この値は、AEM Formsがデプロイされる J2EE アプリケーションサーバーの URL を表します。 リモートでAEM Formsを呼び出すには、AEM Formsをデプロイする J2EE アプリケーションサーバー名を指定します。 クライアントアプリケーションが同じ J2EE アプリケーションサーバー上にある場合は、`localhost` を指定できます。AEM Forms のデプロイ先 J2EE アプリケーションサーバーに応じて、次のいずれかの値を指定します。

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:SOAP 接続モードを使用している場合、この値は呼び出し要求の送信先のエンドポイントを表します。 リモートでAEM Formsを呼び出すには、AEM Formsをデプロイする J2EE アプリケーションサーバー名を指定します。 クライアントアプリケーションが同じ J2EE アプリケーションサーバー上にある場合は、`localhost`（たとえば `http://localhost:8080`）を指定できます。

   * ポート値 `8080` は、J2EE アプリケーションが JBoss の場合に適用されます。J2EE アプリケーションサーバーが IBM® WebSphere® の場合は、ポート `9080` を使用します。同様に、J2EE アプリケーションサーバーが WebLogic の場合は、ポート `7001` を使用します。( これらの値はデフォルトのポート値です。 ポート値を変更する場合は、該当するポート番号を使用します )。

* **DSC_TRANSPORT_PROTOCOL**：EJB 接続モードを使用している場合は、この値に `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` を指定します。SOAP 接続モードを使用している場合は `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL` を指定します。
* **DSC_SERVER_TYPE**：AEM Forms のデプロイ先 J2EE アプリケーションサーバーを指定します。有効な値は `JBoss`、`WebSphere`、`WebLogic` です。

   * この接続プロパティを `WebSphere` に設定すると、`java.naming.factory.initial` 値は `com.ibm.ws.naming.util.WsnInitCtxFactory` に設定されます。
   * この接続プロパティを `WebLogic` に設定すると、`java.naming.factory.initial` 値は `weblogic.jndi.WLInitialContextFactory` に設定されます。
   * 同様に、この接続プロパティを `JBoss` に設定すると、`java.naming.factory.initial` 値は `org.jnp.interfaces.NamingContextFactory` に設定されます。
   * デフォルトの値を使用しない場合、`java.naming.factory.initial` プロパティを要件を満たす値に設定することができます。

  >[!NOTE]
  >
  >注意：文字列を使用して `DSC_SERVER_TYPE` 接続プロパティを設定する代わりに、`ServiceClientFactoryProperties` クラスの静的メンバーを使用できます。使用できる値は `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、`ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`、`ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE` です。

* **DSC_CREDENTIAL_USERNAME:** AEM forms ユーザー名を指定します。 ユーザーがAEM Formsサービスを正常に呼び出すには、サービスユーザーロールが必要です。 ユーザーは、サービスの呼び出し権限を含む別の役割を持つこともできます。 それ以外の場合は、サービスを呼び出そうとすると例外がスローされます。 サービスセキュリティが無効の場合、この接続プロパティを指定する必要はありません。
* **DSC_CREDENTIAL_PASSWORD:** 対応するパスワード値を指定します。 サービスセキュリティが無効の場合、この接続プロパティを指定する必要はありません。
* **DSC_REQUEST_TIMEOUT**：SOAP 要求のデフォルト要求タイムアウト制限は、1200000 ミリ秒（20 分）です。リクエストの処理が完了するまでに長い時間が必要になる場合があります。 例えば、大量のレコードを取得する SOAP リクエストの場合、タイムアウト制限が長くなる場合があります。 `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` を使用して、SOAP 要求の要求呼び出しタイムアウト制限を増やすことができます。

  **注意**：SOAP ベースの呼び出しのみが DSC_REQUEST_TIMEOUT プロパティをサポートしています。

接続プロパティを設定するには、次のタスクを実行します。

1. コンストラクタを使用して `java.util.Properties` オブジェクトを作成します。
1. 次の手順で `DSC_DEFAULT_EJB_ENDPOINT` connection プロパティ、を呼び出す `java.util.Properties` オブジェクトの `setProperty` メソッドを使用して、次の値を渡します。

   * `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 列挙値
   * AEM Forms をホストする J2EE アプリケーションサーバーの URL を指定する文字列値

   >[!NOTE]
   >
   >SOAP 接続モードを使用している場合は、`ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 列挙値ではなく `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 列挙値を指定します。

1. 次の手順で `DSC_TRANSPORT_PROTOCOL` connection プロパティ、を呼び出す `java.util.Properties` オブジェクトの `setProperty` メソッドを使用して、次の値を渡します。

   * `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 列挙値
   * `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 列挙値

   >[!NOTE]
   >
   >SOAP 接続モードを使用している場合は、`ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 列挙値ではなく `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL` 列挙値を指定します。

1. 次の手順で `DSC_SERVER_TYPE` connection プロパティ、を呼び出す `java.util.Properties` オブジェクトの `setProperty` メソッドを使用して、次の値を渡します。

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE` 列挙値
   * AEM Forms をホストする J2EE アプリケーションサーバーを指定する文字列値（例えば、AEM Forms が JBoss にデプロイされている場合は `JBoss` を指定します）。

      1. 次の手順で `DSC_CREDENTIAL_USERNAME` connection プロパティ、を呼び出す `java.util.Properties` オブジェクトの `setProperty` メソッドを使用して、次の値を渡します。

   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 列挙値
   * AEM Forms を呼び出すのに必要なユーザー名を指定する文字列値

      1. 次の手順で `DSC_CREDENTIAL_PASSWORD` connection プロパティ、を呼び出す `java.util.Properties` オブジェクトの `setProperty` メソッドを使用して、次の値を渡します。

   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 列挙値
   * 対応するパスワード値を指定する文字列値

**JBoss 用の EJB 接続モードの設定**

次の Java コードの例では、JBoss にデプロイされ、EJB 接続モードを使用してAEM Formsを呼び出す接続プロパティを設定します。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**WebLogic 用の EJB 接続モードの設定**

次の Java コードの例では、WebLogic にデプロイされ、EJB 接続モードを使用してAEM Formsを呼び出す接続プロパティを設定します。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**WebSphere 用の EJB 接続モードの設定**

次の Java コードの例では、WebSphere にデプロイされ、EJB 接続モードを使用してAEM Formsを呼び出すように接続プロパティを設定します。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**SOAP 接続モードの設定**

次の Java コードの例では、JBoss にデプロイされたAEM Formsを呼び出すように、SOAP モードで接続プロパティを設定します。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>SOAP 接続モードを選択する場合は、追加の JAR ファイルをクライアントアプリケーションのクラスパスに含める必要があります。

**サービスセキュリティが無効な場合の接続プロパティの設定**

次の Java コードの例では、サービスセキュリティが無効な場合に JBoss Application Server にデプロイされた AEM Forms を呼び出すために必要な接続プロパティを設定します。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>AEM Formsでのプログラミングに関連するすべての Java クイックスタートには、EJB と SOAP の両方の接続設定が表示されます。

**カスタム要求のタイムアウト制限を使用した SOAP 接続モードの設定**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Context オブジェクトを使用したAEM Formsの呼び出し**

`com.adobe.idp.Context` オブジェクトを使用して、認証されたユーザーで AEM Forms サービスを呼び出すことができます（`com.adobe.idp.Context` オブジェクトが認証されたユーザーを表します）。`com.adobe.idp.Context` オブジェクトを使用している場合は、`DSC_CREDENTIAL_USERNAME` または `DSC_CREDENTIAL_PASSWORD` プロパティを設定する必要はありません。次の URL を入手できます： `com.adobe.idp.Context` オブジェクトを使用してユーザーを認証する場合 `AuthenticationManagerServiceClient` オブジェクトの `authenticate` メソッド。

`authenticate` メソッドは、認証の結果を含む `AuthResult` オブジェクトを返します。コンストラクタを呼び出すことによって、`com.adobe.idp.Context` オブジェクトを作成できます。次に、 `com.adobe.idp.Context` オブジェクトの `initPrincipal` メソッドを使用して、 `AuthResult` オブジェクトに含まれる値を指定します。

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

代わりに、 `DSC_CREDENTIAL_USERNAME` または `DSC_CREDENTIAL_PASSWORD` プロパティを使用すると、 `ServiceClientFactory` オブジェクトの `setContext` メソッドを使用して、 `com.adobe.idp.Context` オブジェクト。 AEM forms ユーザーを使用してサービスを呼び出す場合は、という名前のロールがあることを確認します。 `Services User` AEM Formsサービスを呼び出すために必要な

次のコードの例では、`EncryptionServiceClient` オブジェクトを作成するために使用される接続設定内で `com.adobe.idp.Context` オブジェクトを使用する方法を示します。

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>ユーザーの認証について詳しくは、 [ユーザーの認証](/help/forms/developing/users.md#authenticating-users).

### シナリオの呼び出し {#invoking_scenarios-1}

この節では、次の呼び出しシナリオについて説明します。

* 独自の Java 仮想マシン (JVM) で実行されているクライアントアプリケーションは、スタンドアロンのAEM Formsインスタンスを呼び出します。
* 独自の JVM で実行されているクライアントアプリケーションは、クラスター化されたAEM Formsインスタンスを呼び出します。

### スタンドアロンAEM Formsインスタンスを呼び出すクライアントアプリケーション {#client-application-invoking-a-stand-alone-aem-forms-instance}

次の図は、独自の JVM で実行され、スタンドアロンのAEM Formsインスタンスを呼び出すクライアントアプリケーションを示しています。

このシナリオでは、クライアントアプリケーションが独自の JVM で実行され、AEM Formsサービスを呼び出します。

>[!NOTE]
>
>このシナリオは、すべてのクイックスタートの基となる呼び出しシナリオです。

### クラスター化されたAEM Formsインスタンスを呼び出すクライアントアプリケーション {#client-application-invoking-clustered-aem-forms-instances}

次の図は、独自の JVM で実行され、クラスター内のAEM Formsインスタンスを呼び出すクライアントアプリケーションを示しています。

このシナリオは、スタンドアロンのAEM Formsインスタンスを呼び出すクライアントアプリケーションに似ています。 ただし、プロバイダー URL は異なります。 クライアントアプリケーションが特定の J2EE アプリケーションサーバーに接続する場合、アプリケーションは、特定の J2EE アプリケーションサーバーを参照するように URL を変更する必要があります。

特定の J2EE アプリケーションサーバーの参照は、アプリケーションサーバーが停止した場合にクライアントアプリケーションとAEM Forms間の接続が終了するので、お勧めしません。 プロバイダー URL は、特定の J2EE アプリケーションサーバーではなく、セルレベルの JNDI マネージャーを参照することをお勧めします。

SOAP 接続モードを使用するクライアントアプリケーションは、クラスターに HTTP ロードバランサーポートを使用できます。 EJB 接続モードを使用するクライアントアプリケーションは、特定の J2EE アプリケーションサーバーの EJB ポートに接続できます。 このアクションは、クラスターノード間のロードバランシングを処理します。

**WebSphere**

次の例は、WebSphere にデプロイされるAEM Formsに接続するために使用される jndi.properties ファイルの内容を示しています。

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

次の例は、WebLogic にデプロイされるAEM Formsに接続するために使用される jndi.properties ファイルの内容を示しています。

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

次の例は、JBoss にデプロイされているAEM Formsへの接続に使用される jndi.properties ファイルの内容を示しています。

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>J2EE アプリケーションサーバーの名前とポート番号については、管理者に問い合わせてください。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java API を使用した AEM Forms サービスへのデータの引き渡し {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Formsサービス操作は、通常、PDFドキュメントを消費または生成します。 サービスを呼び出す場合、PDFドキュメント（または XML データなどの他のドキュメントタイプ）をサービスに渡す必要が生じることがあります。 同様に、サービスから返されたPDFドキュメントを処理する必要が生じる場合があります。 AEM Forms サービスとの間でデータをやりとりできるようにする Java クラスは、`com.adobe.idp.Document` です。

AEM Forms サービスは、PDF ドキュメントを `java.io.InputStream` オブジェクトやバイト配列などの他のデータ型としては受け入れません。`com.adobe.idp.Document` オブジェクトを使用して、XML データなどの他のタイプのデータをサービスに渡すこともできます。

`com.adobe.idp.Document` オブジェクトは Java のシリアライズ可能な型であるため、RMI 呼び出しで渡すことができます。受信側は、同じホスト、同じクラスローダー、ローカル（同じホスト、異なるクラスローダー）、リモート（異なるホスト）のいずれかを同時に配置できます。 ドキュメントコンテンツの受け渡しは、ケースごとに最適化されます。 例えば、送信者と受信者が同じホスト上にある場合、コンテンツはローカルファイルシステムを介して渡されます。 （場合によっては、ドキュメントをメモリに渡すことができます）。

`com.adobe.idp.Document` オブジェクトのサイズに応じて、データは `com.adobe.idp.Document` オブジェクト内に保持されるか、サーバーのファイルシステムに格納されます。`com.adobe.idp.Document` オブジェクトが占有していた一時的なストレージリソースは、`com.adobe.idp.Document` の破棄時に自動的に削除されます（[Document オブジェクトの廃棄](invoking-aem-forms-using-java.md#disposing-document-objects)を参照）。

場合により、サービスに渡す前に、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを知っておく必要があります。たとえば、操作で `application/pdf` などの特定のコンテンツタイプが必要な場合は、コンテンツタイプを確認することをお勧めします（[ドキュメントのコンテンツタイプの確認](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)を参照）。

`com.adobe.idp.Document` オブジェクトは、提示されたデータを使用してコンテンツタイプの判別を試行します。提示されたデータからコンテンツタイプを取得できない場合（例えば、データがバイト配列として提示された場合）は、コンテンツタイプを設定します。コンテンツタイプを設定するには、 `com.adobe.idp.Document` オブジェクトの `setContentType` メソッド。 （[ドキュメントのコンテンツタイプの確認](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)を参照。）

コラテラルファイルが同じファイルシステム上にある場合は、`com.adobe.idp.Document` オブジェクトを作成する方が効率的です。コラテラルファイルがリモートファイルシステム上に格納されていると、コピー操作を実行する必要があり、パフォーマンスに影響します。

アプリケーションには、`com.adobe.idp.Document` と `org.w3c.dom.Document` データタイプの両方を含めることができます。ただし、`org.w3c.dom.Document` データタイプの条件を完全に満たすようにしてください。`org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトに変換する方法については、[クイックスタート（EJB モード）：Java API を使用した流動レイアウトによるフォームの事前入力](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)を参照してください。

>[!NOTE]
>
>WebLogic で `com.adobe.idp.Document` オブジェクトの使用時にメモリリークが発生しないようにするには、ドキュメント情報を 2048 バイト以下のチャンクで読み取ります。例えば、次のコードは、2048 バイトのチャンクでドキュメント情報を読み取ります。

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### ドキュメントの作成 {#creating-documents}

入力値として PDF ドキュメント（または他のドキュメントタイプ）を必要とするサービス操作を呼び出す前に、`com.adobe.idp.Document` オブジェクトを作成します。`com.adobe.idp.Document` クラスは、次のコンテンツタイプからドキュメントを作成できるコンストラクターを提供します。

* バイト配列
* 既存の `com.adobe.idp.Document` オブジェクト
* `java.io.File` オブジェクト
* `java.io.InputStream` オブジェクト
* `java.net.URL` オブジェクト

#### バイト配列に基づいたドキュメントの作成 {#creating-a-document-based-on-a-byte-array}

次のコードの例では、バイト配列に基づいた `com.adobe.idp.Document` オブジェクトを作成します。

**バイト配列に基づく Document オブジェクトの作成**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 別のドキュメントに基づくドキュメントの作成 {#creating-a-document-based-on-another-document}

次のコードの例では、別の `com.adobe.idp.Document` オブジェクトに基づいた `com.adobe.idp.Document` オブジェクトを作成します。

**別のドキュメントに基づく Document オブジェクトの作成**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### ファイルに基づくドキュメントの作成 {#creating-a-document-based-on-a-file}

次のコードの例では、*map.pdf* という名前の PDF ファイルに基づいた `com.adobe.idp.Document` オブジェクトを作成します。このファイルは C ハードドライブのルートにあります。 このコンストラクターは、ファイル拡張子を使用して `com.adobe.idp.Document` オブジェクトの MIME コンテンツタイプの設定を試行します。

`com.adobe.idp.Document` オブジェクトを受け入れる `java.io.File` コンストラクターは、ブール型パラメーターも受け入れます。このパラメーターを `true` に設定すると、`com.adobe.idp.Document` オブジェクトによってファイルが削除されます。このアクションは、ファイルを `com.adobe.idp.Document` コンストラクターに渡した後にファイルを削除する必要がないことを意味します。

このパラメーターを `false` に設定すると、このファイルの所有権が保持されます。このパラメーターを `true` に設定する方が効率的です。理由は、`com.adobe.idp.Document` オブジェクトがファイルをコピーする（この処理はより時間がかかる）のではなくローカルの管理対象領域に直接移動できるためです。

**PDF・ファイルに基づく Document オブジェクトの作成**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### InputStream オブジェクトに基づくドキュメントの作成 {#creating-a-document-based-on-an-inputstream-object}

次の Java コードの例では、`java.io.InputStream` オブジェクトに基づいた `com.adobe.idp.Document` オブジェクトを作成します。

**InputStream オブジェクトに基づくドキュメントの作成**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### URL からアクセス可能なコンテンツに基づくドキュメントの作成 {#creating-a-document-based-on-content-accessible-from-an-url}

次の Java コードの例では、*map.pdf* という名前の PDF ファイルに基づいた `com.adobe.idp.Document` オブジェクトを作成します。このファイルは、`localhost` で実行されている `WebApp` という名前の web アプリケーション内にあります。このコンストラクタは、 `com.adobe.idp.Document` URL プロトコルで返されるコンテンツタイプを使用する、オブジェクトの MIME コンテンツタイプ。

次の例に示すように、`com.adobe.idp.Document` オブジェクトに提供される URL は、元の `com.adobe.idp.Document` オブジェクトが作成されるのに伴って必ず読み取られます。

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

C:/temp/input.pdf ファイルは、（サーバーコンピューターではなく）クライアントコンピューター上に置く必要があります。クライアントコンピューター上で URL が読み取られ、`com.adobe.idp.Document` オブジェクトが作成されます。

**URL からアクセス可能なコンテンツに基づくドキュメントの作成**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**関連トピック：**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### 返されたドキュメントの処理 {#handling-returned-documents}

PDF ドキュメント（または XML データなどの他のデータ型）を出力値として返すサービス操作では、`com.adobe.idp.Document` オブジェクトが返されます。受け取った `com.adobe.idp.Document` オブジェクトは、次の形式に変換できます。

* `java.io.File` オブジェクト
* `java.io.InputStream` オブジェクト
* バイト配列

次のコード行では、`com.adobe.idp.Document` オブジェクトを `java.io.InputStream` オブジェクトに変換します。`myPDFDocument` が `com.adobe.idp.Document` オブジェクトを表すものとします。

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同様に、次のタスクを実行することによって、`com.adobe.idp.Document` の内容をローカルファイルにコピーできます。

1. `java.io.File` オブジェクトを作成します。
1. `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出し、`java.io.File` オブジェクトを渡します

次のコードの例では、`com.adobe.idp.Document` オブジェクトの内容を *AnotherMap.pdf* という名前のファイルにコピーします。

**ドキュメントオブジェクトの内容をファイルにコピーする**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**関連トピック：**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### ドキュメントのコンテンツタイプの確認 {#determining-the-content-type-of-a-document}

の MIME タイプの決定 `com.adobe.idp.Document` を呼び出すことによって、オブジェクトを `com.adobe.idp.Document` オブジェクトの `getContentType` メソッド。 このメソッドは、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを指定する文字列値を返します。次の表に、AEM Formsが返す様々なコンテンツタイプを示します。

<table>
 <thead>
  <tr>
   <th><p>MIME タイプ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>PDF ドキュメント</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>書き出された XML フォームアーキテクチャ（XFA）フォームに使用される XML データパッケージ（XDP）</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>ブックマーク、添付ファイル、またはその他の XML ドキュメント</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>書き出された Acrobat フォームに使用されるフォームデータフォーマット（FDF）</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>書き出された Acrobat フォームに使用される XML フォームデータフォーマット（XFDF）</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>リッチデータフォーマットと XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>汎用のデータフォーマット</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>不特定の MIME タイプ</p></td>
  </tr>
 </tbody>
</table>

次のコードの例では、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを確認します。

**Document オブジェクトのコンテンツタイプの確認**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**関連トピック：**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### Document オブジェクトの廃棄 {#disposing-document-objects}

`Document` オブジェクトが不要になったら、その `dispose` メソッドを呼び出すことで破棄することをお勧めします。各 `Document` オブジェクトは、アプリケーションのホストプラットフォーム上のファイル記述子と最大 75 MB の RAM 容量を消費します。 `Document` オブジェクトが破棄されていない場合、Java のガベージコレクションプロセスによって破棄されます。ただし、`dispose` メソッドを使用してより早く廃棄することによって、`Document` オブジェクトが占有するメモリを解放することができます。

**関連トピック：**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java クライアントライブラリを使用したサービスの呼び出し {#invoking-a-service-using-a-java-client-library}

AEM Formsサービスの操作は、Java クライアントライブラリと呼ばれる、サービスの強く型指定された API を使用して呼び出すことができます。 A *Java クライアントライブラリ* は、サービスコンテナにデプロイされたサービスへのアクセスを提供する具体的なクラスのセットです。 呼び出し API を使用して `InvocationRequest` オブジェクトを作成する代わりに、呼び出すサービスを表す Java オブジェクトをインスタンス化します。呼び出し API は、Workbench で作成された長期間有効なプロセスなどのプロセスを呼び出すために使用されます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

サービス操作を実行するには、Java オブジェクトに属するメソッドを呼び出します。 Java クライアントライブラリには、通常、1 対 1 をサービス操作にマッピングするメソッドが含まれています。 Java クライアントライブラリを使用する場合、必要な接続プロパティを設定します。 （[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照）

接続プロパティを設定したら、サービスを呼び出すための Java オブジェクトをインスタンス化するために使用される `ServiceClientFactory` オブジェクトを作成します。Java クライアントライブラリを持つ各サービスには、対応するクライアントオブジェクトがあります。例えば、Repository サービスを呼び出すには、コンストラクターを使用して `ResourceRepositoryClient` オブジェクトを渡すことによって `ServiceClientFactory` オブジェクトを作成します。`ServiceClientFactory` オブジェクトは、AEM Forms サービスを呼び出すために必要な接続設定を維持する役割を果たします。

`ServiceClientFactory` の取得は通常は高速ですが、ファクトリを初めて使用するときにはオーバーヘッドが発生します。このオブジェクトは再利用のために最適化されているため、複数の Java クライアントオブジェクトを作成する場合は、可能であれば同じ `ServiceClientFactory` オブジェクトを使用してください。つまり、作成するクライアントライブラリオブジェクトごとに個別の `ServiceClientFactory` オブジェクトを作成しないでください。

`ServiceClientFactory` オブジェクトに影響を与える `com.adobe.idp.Context` オブジェクト内部の SAML アサーションの有効期間を制御する User Manager 設定があります。この設定は、Java API を使用して実行されるすべての呼び出しを含む、AEM Forms 全体のすべての認証コンテキストの有効期間を制御します。デフォルトでは、`ServiceCleintFactory` オブジェクトを使用できる期間は 2 時間です。

>[!NOTE]
>
>Java API を使用してサービスを呼び出す方法を説明するには、Repository サービスの `writeResource` 操作が呼び出されました。 この操作により、新しいリソースがリポジトリに配置されます。

Java クライアントライブラリを使用し、次の手順を実行することで、Repository サービスを呼び出すことができます。

1. Java プロジェクトのクラスパスに、adobe-repository-client.jar などのクライアント JAR ファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. サービスを呼び出すために必要な接続プロパティを設定します。
1. の作成 `ServiceClientFactory` を呼び出すことによって、オブジェクトを `ServiceClientFactory` オブジェクトの静的 `createInstance` メソッドおよび `java.util.Properties` 接続プロパティを含むオブジェクト。
1. コンストラクタを使用して `ResourceRepositoryClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ResourceRepositoryClient` オブジェクトを使用して、Repository サービスの操作を呼び出します。
1. そのコンストラクタを使用して `null` を渡すことによって、`RepositoryInfomodelFactoryBean` オブジェクトを作成します。このオブジェクトを使用すると、リポジトリに追加されるコンテンツを表す `Resource` オブジェクトを作成できます。
1. の作成 `Resource` を呼び出すことによって、オブジェクトを `RepositoryInfomodelFactoryBean` オブジェクトの `newImage` メソッドを使用して、次の値を渡します。

   * 一意の ID（`new Id()` を指定する）。
   * 一意の UUID 値（`new Lid()` を指定する）。
   * リソースの名前。 XDP ファイルのファイル名を指定できます。

   戻り値を `Resource` にキャストします。

1. の作成 `ResourceContent` を呼び出すことによって、オブジェクトを `RepositoryInfomodelFactoryBean` オブジェクトの `newImage` メソッドを使用し、戻り値を `ResourceContent`. このオブジェクトはリポジトリに追加されるコンテンツを表します。
1. リポジトリに追加する XDP ファイルを格納する `java.io.FileInputStream` オブジェクトを渡して、`com.adobe.idp.Document` オブジェクトを作成します（[InputStream オブジェクトに基づいたドキュメントの作成](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)を参照）。
1. 次のコンテンツを追加： `com.adobe.idp.Document` オブジェクトを `ResourceContent` を呼び出すことによって、オブジェクトを `ResourceContent` オブジェクトの `setDataDocument` メソッド。 `com.adobe.idp.Document` オブジェクトを渡します。
1. を呼び出して、リポジトリに追加する XDP ファイルの MIME タイプを設定します。 `ResourceContent` オブジェクトの `setMimeType` メソッドとパス `application/vnd.adobe.xdp+xml`.
1. 次のコンテンツを追加： `ResourceContent` オブジェクトを `Resource` を呼び出すことによって、オブジェクトを `Resource` オブジェクトの `setContent` メソッドおよび `ResourceContent` オブジェクト。
1. を呼び出して、リソースの説明を追加します。 `Resource` オブジェクトの `setDescription` メソッドを使用して、リソースの説明を表す string 値を渡すことができます。
1. を呼び出して、フォームデザインをリポジトリに追加します。 `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを使用して、次の値を渡します。

   * 新しいリソースを含むリソースコレクションへのパスを指定する文字列値
   * 作成された `Resource` オブジェクト

**関連トピック**

[クイックスタート（EJB モード）：Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 呼び出し API を使用した短時間のみ有効なプロセスの呼び出し {#invoking-a-short-lived-process-using-the-invocation-api}

Java 呼び出し API を使用して、短時間のみ有効なプロセスを呼び出すことができます。 Invocation API を使用して短期間有効なプロセスを呼び出す場合は、`java.util.HashMap` オブジェクトを使用して必須のパラメーター値を渡します。サービスに渡すパラメーターごとに、 `java.util.HashMap` オブジェクトの `put` メソッドを参照し、指定した操作を実行するためにサービスで必要な名前と値のペアを指定します。 短時間のみ有効なプロセスに属するパラメーターの正確な名前を指定します。

>[!NOTE]
>
>長期間有効なプロセスの呼び出しについて詳しくは、 [人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

ここでは、Invocation API を使用して、`MyApplication/EncryptDocument` という名前の次の AEM Forms（短期間有効のプロセス）を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください）。

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡されたPDFドキュメントを取得します。 このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`inDoc` という名前の `document` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

### Java invocation API を使用した MyApplication/EncryptDocument（短期間有効なプロセス）の呼び出し {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Java invocation API を使用して短期間有効なプロセスの `MyApplication/EncryptDocument` を呼び出します。

1. Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。 （[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. `ServiceClient` オブジェクトを作成するには、コントラクターを使用して、`ServiceClientFactory` オブジェクトを渡します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクターを使用して `java.util.HashMap` オブジェクトを作成します。
1. を呼び出す `java.util.HashMap` オブジェクトの `put` メソッドを使用して、長期間有効なプロセスに渡すことができます。 短期間有効なプロセスの `MyApplication/EncryptDocument` では、`Document` 型の入力パラメーターが 1 つ必要です。次の例に示すように、`put` メソッドを呼び出す必要があるのは 1 回だけです。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. の作成 `InvocationRequest` を呼び出すことによって、オブジェクトを `ServiceClientFactory` オブジェクトの `createInvocationRequest` メソッドを使用して、次の値を渡します。

   * 呼び出す長期間有効なプロセスの名前を指定する文字列値。`MyApplication/EncryptDocument` プロセスを呼び出すには、`MyApplication/EncryptDocument` を指定します。
   * プロセス操作名を表す文字列値。通常、短期間有効なプロセス操作の名前は `invoke` です。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * 同期要求を作成する `true` を指定するブール値（この値は、短期間有効なプロセスを呼び出すために適用されます）。

1. を呼び出して、呼び出し要求をサービスに送信します。 `ServiceClient` オブジェクトの `invoke` メソッドおよび `InvocationRequest` オブジェクト。 `invoke` メソッドは、`InvocationReponse` オブジェクトを返します。

   >[!NOTE]
   >
   >`createInvocationRequest` メソッドの 4 番目のパラメーターとして値 `false` を渡すことによって、長期間有効なプロセスを呼び出すことができます。値 `false`**&#x200B;を渡すと、非同期要求が作成されます。

1. を呼び出して、プロセスの戻り値を取得します。 `InvocationReponse` オブジェクトの `getOutputParameter` メソッドを使用し、出力パラメーターの名前を指定する string 値を渡す。 この場合、`outDoc` を指定します（`outDoc` は `MyApplication/EncryptDocument` プロセスの出力パラメーターの名前です）。以下の例のように、戻り値を `Document` にキャストします。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
1. を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 `getOutputParameter` メソッドから返された `com.adobe.idp.Document` オブジェクトを必ず使用してください。

**関連トピック**

[クイックスタート：Invocation API を使用した短期間有効なプロセスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[AEM Forms Java ライブラリファイルの組み込み](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
