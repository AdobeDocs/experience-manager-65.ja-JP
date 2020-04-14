---
title: Java API を使用した AEM Forms の呼び出し
seo-title: Java API を使用した AEM Forms の呼び出し
description: 'null'
seo-description: 'null'
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# Java API を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-the-javaapi}

AEM Forms Java API を使用して AEM Forms を呼び出すことができます。AEM Forms Java API を使用している場合、呼び出し API または Java クライアントライブラリを使用できます。Java クライアントライブラリは、Rights Management サービスなどのサービスで使用できます。これらの強く型付けされた API を使用することによって、AEM Forms を呼び出す Java アプリケーションを開発できます。

呼び出し API は、`com.adobe.idp.dsc` パッケージに含まれるクラスです。これらのクラスを使用して、呼び出し要求をサービスに直接送信し、返される呼び出し応答を処理することができます。Workbench を使用して作成された長期間有効なプロセスまたは短時間のみ有効なプロセスを、呼び出し API を使用して呼び出します。

プログラムでサービスを呼び出すには、呼び出し API ではなくサービスに対応する Java クライアントライブラリを使用することをお勧めします。例えば、Encryption サービスを呼び出すには、Encryption サービスのクライアントライブラリを使用します。Encryption サービスの操作を実行するには、Encryption サービスクライアントオブジェクトに属するメソッドを呼び出します。`EncryptionServiceClient` オブジェクトの `encryptPDFUsingPassword` メソッドを使用して、PDF ドキュメントをパスワードで暗号化することができます。

Java API は次の機能をサポートしています。

* リモート呼び出しのための RMI トランスポートプロトコル
* ローカル呼び出しのための VM トランスポート
* リモート呼び出しのための SOAP
* ユーザー名とパスワードなどの、他の認証方法
* 同期および非同期の呼び出し要求

**Adobe Developer Web サイト**

Adobe Developer の Web サイトには、Java API を使用して AEM Forms サービスを呼び出す方法が記載されています。

[Java サーブレットを使用した AEM Forms プロセスの呼び出し](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Java からの AEM Forms Distiller API の呼び出し](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](#including-aem-forms-java-library-files)

[人間中心の長期間有効なプロセスの呼び出し](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md)

[接続プロパティの設定](#setting-connection-properties)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](#invoking-a-service-using-a-java-client-library)

[呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](#invoking-a-short-lived-process-using-the-invocation-api)

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md)

## AEM Forms Java ライブラリファイルを含める {#including-aem-forms-java-library-files}

Java API を使用してプログラムで AEM Forms サービスを呼び出すには、Java プロジェクトのクラスパスに必要なライブラリファイル（JAR ファイル）を含めます。クライアントアプリケーションのクラスパスに含める JAR ファイルは、いくつかの要因によって異なります。

* 呼び出す AEM Forms サービス。クライアントアプリケーションは 1 つ以上のサービスを呼び出すことができます。
* AEM Forms サービスを呼び出すモード。EJB モードまたは SOAP モードを使用できます。（[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>（自動オプションのみ）AEM Formsサーバーを開始し、EJB用のサー `standalone.bat -b <Server IP> -c lc_turnkey.xml` バーIPを指定するコマンドを使用します。

* AEM Forms のデプロイ先 J2EE アプリケーションサーバー。

### サービス固有の JAR ファイル {#service-specific-jar-files}

次の表に、AEM Forms サービスを呼び出すために必要な JAR ファイルを示します。

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
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk//client-libs/&lt;アプリケーションサーバー&gt;</p></td>
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
   <td><p>Backup and Restore サービス API を呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Barcoded Forms サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Convert PDF サービスを呼び出すために必要です。 </p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Distiller サービスを呼び出すために必要です。</p></td>
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
   <td><p>Forms サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Form Data Integration サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Generate PDF サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Generate 3D PDF サービスを呼び出すために必要です。</p></td>
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
   <td><p>PDF Utilities サービスまたは XMP Utilities サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Acrobat Reader DC エクステンションサービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Repository サービスを呼び出すために必要です。</p></td>
   <td><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>インストールディレクトリ</i>&gt;/sdk/client-libs/thirdparty</p></td>
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
   <td><p>Rights Management サービスを呼び出すために必要です。</p><p>AEM Forms が JBoss 上にデプロイされている場合は、これらのファイルをすべて含めます。 </p></td>
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

次の表に、接続モードと AEM Forms のデプロイ先 J2EE アプリケーションサーバーに依存する JAR ファイルを示します。

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
   <td><p>AEM Forms を SOAP モードを使用して呼び出す場合は、これらの JAR ファイルを含めます。</p> </td>
   <td><p>&lt;<em>インストールディレクトリ</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>AEM Forms が JBoss Application Server 上にデプロイされている場合は、この JAR ファイルを含めます。</p> <p>jboss-client.jarと参照先のjarが共存していない場合、必須のクラスはクラスローダーで見つかりません。</p> </td>
   <td><p>JBoss クライアントの lib ディレクトリ</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバー上にデプロイする場合は、このファイルを含める必要はありません。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>AEM Forms が BEA WebLogicServer® 上にデプロイされている場合は、この JAR ファイルを含めます。</p> </td>
   <td><p>WebLogic 固有の lib ディレクトリ</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバー上にデプロイする場合は、このファイルを含める必要はありません。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>AEM Forms が WebSphere Application Server 上にデプロイされている場合は、これらの JAR ファイルを含めます。</p> </li>
     <li><p>（Web サービスの呼び出しには com.ibm.ws.webservices.thinclient_6.1.0.jar が必要です）。</p> </li>
    </ul> </td>
   <td><p>WebSphere 固有の lib ディレクトリ（<em>[過去のホームディレクトリ]</em>/runtimes）</p> <p>クライアントアプリケーションを同じ J2EE アプリケーションサーバーにデプロイする場合は、これらのファイルを含める必要はありません。</p> </td>
  </tr>
 </tbody>
</table>

### 呼び出しシナリオ {#invoking-scenarios}

次の表に、呼び出しシナリオと、AEM Forms を正常に呼び出すために必要な JAR ファイルを示します。

<table>
 <thead>
  <tr>
   <th><p>サービス</p> </th>
   <th><p>呼び出しモード</p> </th>
   <th><p>J2EE アプリケーションサーバー</p> </th>
   <th><p>必須の JAR ファイル</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Forms サービス</p> </td>
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
   <td><p>Forms サービス</p> <p>Acrobat Reader DC エクステンションサービス</p> <p>Signature サービス</p> </td>
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
   <td><p>Forms サービス</p> </td>
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
   <td><p>Forms サービス</p> <p>Acrobat Reader DC エクステンションサービス</p> <p>Signature サービス</p> </td>
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

LiveCycle から AEM Forms にアップグレードする場合は、Java プロジェクトのクラスパスに AEM Forms JAR ファイルを含めることをお勧めします。例えば、Rights Management サービスなどのサービスを使用している場合、クラスパスに AEM Forms JAR ファイルを含めないと、互換性の問題が発生します。

AEM Forms にアップグレードするとします。Rights Management サービスを呼び出す Java アプリケーションを使用するには、次の JAR ファイルの AEM Forms バージョンを含めます。

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 接続プロパティの設定 {#setting-connection-properties}

Java API を使用している場合、AEM Forms を呼び出すためには接続プロパティを設定します。接続プロパティを設定する場合は、サービスをリモートとローカルのどちらで呼び出すかどうかを指定し、接続モードと認証値も指定します。サービスセキュリティが有効な場合は、認証値が必要です。ただし、サービスセキュリティが無効の場合は、認証値を指定する必要はありません。

接続モードは、SOAP モードまたは EJB モードです。EJB モードは RMI/IIOP プロトコルを使用し、EJB モードのパフォーマンスは SOAP モードのパフォーマンスよりも優れています。SOAP モードは、J2EE アプリケーションサーバーの依存関係を解消するため、または AEM Forms とクライアントアプリケーションの間にファイアウォールが設定されている場合に使用されます。SOAP モードでは、基礎のトランスポートとして https プロトコルを使用するので、ファイアウォールの境界を越えて通信できます。J2EE アプリケーションサーバーの依存関係もファイアウォールも問題でない場合は、EJB モードを使用することをお勧めします。

AEM Forms サービスを正常に呼び出すには、次の接続プロパティを設定します。

* **DSC_DEFAULT_EJB_ENDPOINT**：EJB 接続モードを使用している場合、この値は AEM Forms のデプロイ先 J2EE アプリケーションサーバーの URL を表します。リモートで AEM Forms を呼び出すには、AEM Forms のデプロイ先 J2EE アプリケーションサーバー名を指定します。クライアントアプリケーションが同じ J2EE アプリケーションサーバー上にある場合は、`localhost` を指定できます。AEM Forms のデプロイ先 J2EE アプリケーションサーバーに応じて、次のいずれかの値を指定します。

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**：SOAP 接続モードを使用している場合、この値は呼び出し要求が送信されるエンドポイントを表します。リモートで AEM Forms を呼び出すには、AEM Forms のデプロイ先 J2EE アプリケーションサーバー名を指定します。クライアントアプリケーションが同じ J2EE アプリケーションサーバー上にある場合は、`localhost`（例えば `http://localhost:8080`）を指定できます。

   * ポート値 `8080` は、J2EE アプリケーションが JBoss の場合に適用されます。J2EE アプリケーションサーバーが IBM® WebSphere® の場合は、ポート `9080` を使用します。同様に、J2EE アプリケーションサーバーが WebLogic の場合は、ポート `7001` を使用します。（これらの値はデフォルトのポート値です。ポートの値を変更する場合は、適用可能なポート番号を使用してください。）

* **DSC_TRANSPORT_PROTOCOL**：EJB 接続モードを使用している場合は、この値に `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` を指定します。If you are using the SOAP connection mode, specify `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**：AEM Forms のデプロイ先 J2EE アプリケーションサーバーを指定します。Valid values are `JBoss`, `WebSphere`, `WebLogic`.

   * If you set this connection property to `WebSphere`, the `java.naming.factory.initial` value is set to `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * If you set this connection property to `WebLogic`, the `java.naming.factory.initial` value is set to `weblogic.jndi.WLInitialContextFactory`.
   * Likewise, if you set this connection property to `JBoss`, the `java.naming.factory.initial` value is set to `org.jnp.interfaces.NamingContextFactory`.
   * デフォルトの値を使用しない場合、`java.naming.factory.initial` プロパティを要件を満たす値に設定することができます。
   ***Note**: Instead of using a string to set the `DSC_SERVER_TYPE` connection property, you can use a static member of the `ServiceClientFactoryProperties` class. The following values can be used: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`, or `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME**：AEM Forms ユーザー名を指定します。ユーザーが AEM Forms サービスを正常に呼び出すには、サービスユーザーのロールが必要です。ユーザーは、サービス呼び出し権限を含む別のロールを持つこともできます。権限を持たないユーザーの場合、サービスの呼び出しを試行するときに例外が発生します。サービスセキュリティが無効の場合、この接続プロパティを指定する必要はありません。
* **DSC_CREDENTIAL_PASSWORD**：対応するパスワード値を指定します。サービスセキュリティが無効の場合、この接続プロパティを指定する必要はありません。
* **DSC_REQUEST_TIMEOUT**：SOAP 要求のデフォルト要求タイムアウト制限は、1200000 ミリ秒（20 分）です。場合によって、要求の操作が完了するのに長い時間を要することがあります。例えば、大量のレコードセットを取得する SOAP 要求では、より長いタイムアウト制限が必要になることがあります。`ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` を使用して、SOAP 要求の要求呼び出しタイムアウト制限を増やすことができます。

   **注意**：SOAP ベースの呼び出しのみが DSC_REQUEST_TIMEOUT プロパティをサポートしています。

接続プロパティを設定するには、次のタスクを実行します。

1. コンストラクタを使用して `java.util.Properties` オブジェクトを作成します。
1. To set the `DSC_DEFAULT_EJB_ENDPOINT` connection property, invoke the `java.util.Properties` object’s `setProperty` method and pass the following values:

   * The `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` enumeration value
   * AEM Forms をホストする J2EE アプリケーションサーバーの URL を指定する文字列値
   >[!NOTE]
   >
   >If you are using the SOAP connection mode, specify the `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` enumeration value instead of the `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` enumeration value.

1. To set the `DSC_TRANSPORT_PROTOCOL` connection property, invoke the `java.util.Properties` object’s `setProperty` method and pass the following values:

   * The `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` enumeration value
   * The `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` enumeration value
   >[!NOTE]
   >
   >If you are using the SOAP connection mode, specify the `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`enumeration value instead of the `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` enumeration value.

1. To set the `DSC_SERVER_TYPE` connection property, invoke the `java.util.Properties` object’s `setProperty` method and pass the following values:

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE`定義済みリスト値
   * AEM Forms をホストする J2EE アプリケーションサーバーを指定する文字列値（例えば、AEM Forms が にデプロイされている場合は `JBoss`JBoss を指定します）。

      1. To set the `DSC_CREDENTIAL_USERNAME` connection property, invoke the `java.util.Properties` object’s `setProperty` method and pass the following values:
   * The `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` enumeration value
   * AEM Forms を呼び出すのに必要なユーザー名を指定する文字列値

      1. To set the `DSC_CREDENTIAL_PASSWORD` connection property, invoke the `java.util.Properties` object’s `setProperty` method and pass the following values:
   * The `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` enumeration value
   * 対応するパスワード値を指定する文字列値



**JBoss用のEJB接続モードの設定**

次の Java コードの例では、JBoss にデプロイされ EJB 接続モードを使用している AEM Forms を呼び出すための接続プロパティを設定しています。

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

次の Java コードの例では、WebLogic にデプロイされ EJB 接続モードを使用している AEM Forms を呼び出すための接続プロパティを設定しています。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**WebSphere 用の EJB 接続モードの設定**

次の Java コードの例では、WebSphere にデプロイされ EJB 接続モードを使用している AEM Forms を呼び出すための接続プロパティを設定しています。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**SOAP 接続モードの設定**

次の Java コードの例では、SOAP モードで接続プロパティを設定して、JBoss にデプロイされた AEM Forms を呼び出します。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>SOAP 接続モードを選択した場合は、クライアントアプリケーションのクラスパスに追加の JAR ファイルを含めるようにしてください。

**サービスセキュリティが無効な場合の接続プロパティの設定**

次の Java コードの例では、サービスセキュリティが無効な場合に JBoss Application Server にデプロイされた AEM Forms を呼び出すために必要な接続プロパティを設定します。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>AEM Forms でのプログラミングに関連するすべての Java クイックスタートは、EJB と SOAP の両方の接続設定を示します。

**カスタム要求タイムアウト制限を含む SOAP 接続モードの設定**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Context オブジェクトを使用した AEM Forms の呼び出し**

`com.adobe.idp.Context` オブジェクトを使用して、認証されたユーザーで AEM Forms サービスを呼び出すことができます（`com.adobe.idp.Context` オブジェクトが認証されたユーザーを表します）。When using a `com.adobe.idp.Context` object, you do not need to set the `DSC_CREDENTIAL_USERNAME` or `DSC_CREDENTIAL_PASSWORD` properties. You can obtain a `com.adobe.idp.Context` object when authenicating users by using the `AuthenticationManagerServiceClient` object’s `authenticate` method.

`authenticate` メソッドは、認証の結果を含む `AuthResult` オブジェクトを返します。コンストラクタを呼び出すことによって、`com.adobe.idp.Context` オブジェクトを作成できます。次に、次のコードに示すように、`com.adobe.idp.Context` オブジェクトの `initPrincipal` メソッドを呼び出し、`AuthResult` オブジェクトを渡します。

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Instead of setting the `DSC_CREDENTIAL_USERNAME` or `DSC_CREDENTIAL_PASSWORD` properties, you can invoke the `ServiceClientFactory` object’s `setContext` method and pass the `com.adobe.idp.Context` object. When using a AEM forms user to invoke a service, ensure that they have the role named `Services User` that is required to invoke a AEM Forms service.

次のコードの例では、`com.adobe.idp.Context` オブジェクトを作成するために使用される接続設定内で `EncryptionServiceClient` オブジェクトを使用する方法を示します。

```as3
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
>ユーザーの認証の詳細については、[ユーザーの認証](/help/forms/developing/users.md#authenticating-users)を参照してください。

### 呼び出しシナリオ {#invoking_scenarios-1}

この節では、以下の呼び出しシナリオについて説明します。

* 独自の Java 仮想マシン（JVM）で実行されているクライアントアプリケーションは、スタンドアロンの AEM Forms インスタンスを呼び出します。
* 独自の JVM で実行されているクライアントアプリケーションは、クラスター化された AEM Forms インスタンスを呼び出します。

### スタンドアロン AEM Forms インスタンスを呼び出すクライアントアプリケーション {#client-application-invoking-a-stand-alone-aem-forms-instance}

次の図は、独自の JVM で実行され、スタンドアロン AEM Forms インスタンスを呼び出すクライアントアプリケーションを示しています。

このシナリオでは、クライアントアプリケーションが独自の JVM で実行され、AEM Forms サービスを呼び出します。

>[!NOTE]
>
>このシナリオは、すべてのクイックスタートが基づいている呼び出しシナリオです。

### クラスター化された AEM Forms インスタンスを呼び出すクライアントアプリケーション {#client-application-invoking-clustered-aem-forms-instances}

次の図は、独自の JVM で実行され、クラスター内にある AEM Forms インスタンスを呼び出すクライアントアプリケーションを示しています。

このシナリオは、スタンドアロン AEM Forms インスタンスを呼び出すクライアントアプリケーションに似ています。ただし、プロバイダーの URL が異なります。クライアントアプリケーションが特定の J2EE アプリケーションサーバーに接続する場合、アプリケーションはその特定の J2EE アプリケーションサーバーを参照するように URL を変更する必要があります。

特定の J2EE アプリケーションサーバーを参照することは推奨されません。これは、アプリケーションサーバーが停止すると、クライアントアプリケーションと AEM Forms との間の接続が終了するためです。プロバイダー URL では、特定の J2EE アプリケーションサーバーではなく、セルレベルの JNDI マネージャーを参照することをお勧めします。

SOAP 接続モードを使用するクライアントアプリケーションは、クラスター用に HTTP ロードバランサーポートを使用できます。EJB 接続モードを使用するクライアントアプリケーションは、特定の J2EE アプリケーションサーバーの EJB ポートに接続できます。このアクションは、クラスターノード間の負荷分散を処理します。

**WebSphere**

次の例は、WebSphere にデプロイされた AEM Forms に接続するために使用される jndi.properties ファイルの内容を示しています。

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

次の例は、WebLogic にデプロイされた AEM Forms に接続するために使用される jndi.properties ファイルの内容を示しています。

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

次の例は、JBoss にデプロイされている AEM Forms に接続するために使用される jndi.properties ファイルの内容を示しています。

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>管理者に相談して、J2EE アプリケーションサーバーの名前とポート番号を確認してください。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java API を使用した AEM Forms サービスへのデータの引き渡し](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java API を使用した AEM Forms サービスへのデータの引き渡し {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms サービス操作では、通常、PDF ドキュメントを使用または生成します。サービスを呼び出すときに、PDF ドキュメント（または XML データなどの他のドキュメントタイプ）をサービスに渡す必要がある場合があります。同様に、サービスから返される PDF ドキュメントを処理する必要があることもあります。AEM Forms サービスとの間でデータをやりとりできるようにする Java クラスは、`com.adobe.idp.Document` です。

AEM Forms サービスは、PDF ドキュメントを `java.io.InputStream` オブジェクトやバイト配列などの他のデータ型としては受け入れません。`com.adobe.idp.Document` オブジェクトを使用して、XML データなどの他のタイプのデータをサービスに渡すこともできます。

`com.adobe.idp.Document` オブジェクトは Java のシリアライズ可能な型であるため、RMI 呼び出しで渡すことができます。受信側は、同時配置（同じホスト、同じクラスローダー）することも、ローカル（同じホスト、別のクラスローダー）またはリモート（別のホスト）に配置することもできます。ドキュメントコンテンツの引き渡しは、それぞれの場合に最適化されます。例えば、送信者と受信者が同じホスト上にある場合、コンテンツはローカルファイルシステムを介して渡されます。（ドキュメントがメモリ内で渡される場合もあります）。

`com.adobe.idp.Document` オブジェクトのサイズに応じて、データは引き渡し用に `com.adobe.idp.Document` オブジェクト内に保持されるか、サーバーのファイルシステムに格納されます。`com.adobe.idp.Document` オブジェクトが占有していた一時的なストレージリソースは、`com.adobe.idp.Document` の破棄時に自動的に削除されます。（[Document オブジェクトの廃棄](invoking-aem-forms-using-java.md#disposing-document-objects)を参照。）

サービスに渡す前に、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを知る必要がある場合があります。例えば、操作で `application/pdf` などの特定のコンテンツタイプが必要な場合は、コンテンツタイプを確認することをお勧めします。（[ドキュメントのコンテンツタイプの確認](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)を参照。）

`com.adobe.idp.Document` オブジェクトは、提示されたデータを使用してコンテンツタイプの判別を試行します。提示されたデータからコンテンツタイプを取得できない場合（例えば、データがバイト配列として提示された場合）は、コンテンツタイプを設定します。To set the content type, invoke the `com.adobe.idp.Document` object’s `setContentType` method. （[ドキュメントのコンテンツタイプの確認](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)を参照。）

コラテラルファイルが同じファイルシステム上にある場合は、`com.adobe.idp.Document` オブジェクトを作成する方が効率的です。コラテラルファイルがリモートファイルシステム上に存在する場合は、コピー操作を実行する必要があるためパフォーマンスに影響します。

An application can contain both `com.adobe.idp.Document` and `org.w3c.dom.Document` data types. However, ensure that you fully qualify the `org.w3c.dom.Document` data type. `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトに変換する方法については、[クイックスタート（EJB モード）：Java API を使用した流動レイアウトによるフォームの事前入力](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)を参照してください。

>[!NOTE]
>
>WebLogic で `com.adobe.idp.Document` オブジェクトの使用時にメモリリークが発生しないようにするには、ドキュメント情報を 2048 バイト以下のチャンクで読み取ります。例えば、次のコードは 2048 バイトのチャンクでドキュメント情報を読み取ります。

```as3
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

入力値として PDF ドキュメント（または他のドキュメントタイプ）を必要とするサービス操作を呼び出す前に、`com.adobe.idp.Document` オブジェクトを作成します。`com.adobe.idp.Document` クラスは、次のコンテンツタイプからドキュメントを作成できるコンストラクタを提供します。

* バイト配列
* An existing `com.adobe.idp.Document` object
* オブジェクト `java.io.File` です。
* オブジェクト `java.io.InputStream` です。
* オブジェクト `java.net.URL` です。

#### バイト配列に基づいたドキュメントの作成 {#creating-a-document-based-on-a-byte-array}

次のコードの例では、バイト配列に基づいた `com.adobe.idp.Document` オブジェクトを作成します。

**バイト配列に基づいた Document オブジェクトの作成**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### 別のドキュメントに基づいたドキュメントの作成 {#creating-a-document-based-on-another-document}

次のコードの例では、別の `com.adobe.idp.Document` オブジェクトに基づいた `com.adobe.idp.Document` オブジェクトを作成します。

**別のドキュメントに基づいた Document オブジェクトの作成**

```as3
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

#### ファイルに基づいたドキュメントの作成 {#creating-a-document-based-on-a-file}

The following code example creates a `com.adobe.idp.Document` object that is based on a PDF file named *map.pdf*. このファイルは C ハードドライブのルートにあります。このコンストラクタは、ファイル拡張子を使用して `com.adobe.idp.Document` オブジェクトの MIME コンテンツタイプの設定を試行します。

`com.adobe.idp.Document` オブジェクトを受け入れる `java.io.File` コンストラクタは、ブール型パラメーターも受け入れます。このパラメーターを `true` に設定すると、`com.adobe.idp.Document` オブジェクトによってファイルが削除されます。このアクションは、ファイルを `com.adobe.idp.Document` コンストラクタに渡した後にファイルを削除する必要がないことを意味します。

このパラメーターを `false` に設定すると、このファイルの所有権が保持されます。このパラメーターを `true` に設定する方が効率的です。理由は、`com.adobe.idp.Document` オブジェクトがファイルをコピーする（これは遅い操作です）のではなくローカルの管理対象領域に直接移動できるためです。

**PDF ファイルに基づいた Document オブジェクトの作成**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### InputStream オブジェクトに基づいたドキュメントの作成 {#creating-a-document-based-on-an-inputstream-object}

次の Java コードの例では、`com.adobe.idp.Document` オブジェクトに基づいた `java.io.InputStream` オブジェクトを作成します。

**InputStream オブジェクトに基づいたドキュメントの作成**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### URL からアクセス可能なコンテンツに基づいたドキュメントの作成 {#creating-a-document-based-on-content-accessible-from-an-url}

The following Java code example creates a `com.adobe.idp.Document` object that is based on a PDF file named *map.pdf*. このファイルは、`WebApp` で実行されている `localhost` という名前の Web アプリケーション内にあります。このコンストラクタは、URL プロトコルで返されるコンテンツタイプを使用して `com.adobe.idp.Document` オブジェクトの MIME コンテンツタイプの設定を試行します。

次の例に示すように、`com.adobe.idp.Document` オブジェクトに提供される URL は、元の `com.adobe.idp.Document` オブジェクトが作成されるのに伴って必ず読み取られます。

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

C:/temp/input.pdf ファイルは、（サーバーコンピューターではなく）クライアントコンピューター上に置く必要があります。クライアントコンピューター上で URL が読み取られ、`com.adobe.idp.Document` オブジェクトが作成されます。

**URL からアクセス可能なコンテンツに基づいたドキュメントの作成**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### 返されたドキュメントの処理 {#handling-returned-documents}

PDF ドキュメント（または XML データなどの他のデータ型）を出力値として返すサービス操作では、`com.adobe.idp.Document` オブジェクトが返されます。受け取った `com.adobe.idp.Document` オブジェクトは、次の形式に変換できます。

* オブジェクト `java.io.File` です。
* オブジェクト `java.io.InputStream` です。
* バイト配列

次のコード行では、`com.adobe.idp.Document` オブジェクトを `java.io.InputStream` オブジェクトに変換します。Assume that `myPDFDocument` represents a `com.adobe.idp.Document` object:

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同様に、次のタスクを実行することによって、`com.adobe.idp.Document` の内容をローカルファイルにコピーできます。

1. Create a `java.io.File` object.
1. Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass the `java.io.File`object.

次のコードの例では、`com.adobe.idp.Document` オブジェクトの内容を *AnotherMap.pdf* という名前のファイルにコピーします。

**Document オブジェクトの内容のファイルへのコピー**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### ドキュメントのコンテンツタイプの確認 {#determining-the-content-type-of-a-document}

Determine the MIME type of a `com.adobe.idp.Document` object by invoking the `com.adobe.idp.Document` object’s `getContentType` method. このメソッドは、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを指定する文字列値を返します。次の表で、AEM Forms が返す様々なコンテンツタイプについて説明します。

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

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)

### Document オブジェクトの廃棄 {#disposing-document-objects}

`Document` オブジェクトが不要になったら、その `dispose` メソッドを呼び出すことで破棄することをお勧めします。各 `Document` オブジェクトは、アプリケーションのホストプラットフォーム上でファイル記述子と最大 75 MB の RAM 領域を消費します。`Document` オブジェクトが破棄されていない場合、Java のガベージコレクションプロセスによって破棄されます。ただし、`dispose` メソッドを使用してより早く廃棄することによって、`Document` オブジェクトが占有するメモリを解放することができます。

**関連トピック**

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Java クライアントライブラリを使用したサービスの呼び出し](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Java クライアントライブラリを使用したサービスの呼び出し {#invoking-a-service-using-a-java-client-library}

AEM Forms サービス操作は、サービスの強く型付けされた API である Java クライアントライブラリを使用して呼び出すことができます。*Java クライアントライブラリ*&#x200B;は、サービスコンテナにデプロイされたサービスへのアクセスを提供する具象クラスのセットです。呼び出し API を使用して `InvocationRequest` オブジェクトを作成する代わりに、呼び出すサービスを表す Java オブジェクトをインスタンス化します。呼び出し API は、Workbench で作成された長期間有効なプロセスなどのプロセスを呼び出すために使用されます。（[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

サービス操作を実行するには、Java オブジェクトに属するメソッドを呼び出します。通常、Java クライアントライブラリにはサービス操作に 1 対 1 で対応するメソッドが含まれています。Java クライアントライブラリを使用している場合は、必要な接続プロパティを設定します。（[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

接続プロパティを設定したら、サービスを呼び出すための Java オブジェクトをインスタンス化するために使用される `ServiceClientFactory` オブジェクトを作成します。Java クライアントライブラリを持つ各サービスには、対応するクライアントオブジェクトがあります。例えば、Repository サービスを呼び出すには、コンストラクタを使用して `ResourceRepositoryClient` オブジェクトを渡すことによって `ServiceClientFactory` オブジェクトを作成します。`ServiceClientFactory` オブジェクトは、AEM Forms サービスを呼び出すために必要な接続設定を維持する役割を果たします。

`ServiceClientFactory` の取得は通常は高速ですが、ファクトリを初めて使用するときにはオーバーヘッドが発生します。このオブジェクトは再利用のために最適化されているため、複数の Java クライアントオブジェクトを作成する場合は、可能であれば同じ `ServiceClientFactory` オブジェクトを使用してください。つまり、作成するクライアントライブラリオブジェクトごとに個別の `ServiceClientFactory` オブジェクトを作成しないでください。

`com.adobe.idp.Context` オブジェクトに影響を与える `ServiceClientFactory` オブジェクトの内部にある SAML アサーションの有効期間を制御する User Manager 設定があります。この設定は、Java API を使用して実行されるすべての呼び出しを含む、AEM Forms 全体のすべての認証コンテキストの有効期間を制御します。デフォルトでは、`ServiceCleintFactory` オブジェクトを使用できる期間は 2 時間です。

>[!NOTE]
>
>Java API を使用してサービスを呼び出す方法を説明するために、Repository サービスの `writeResource` 操作が呼び出されます。この操作により、新しいリソースがリポジトリに配置されます。

Java クライアントライブラリを使用して次の手順を実行することにより、Repository サービスを呼び出すことができます。

1. adobe-repository-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. サービスを呼び出すために必要な接続プロパティを設定します。
1. Create a `ServiceClientFactory` object by invoking the `ServiceClientFactory` object’s static `createInstance` method and passing the `java.util.Properties` object that contains connection properties.
1. コンストラクタを使用して `ResourceRepositoryClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ResourceRepositoryClient` オブジェクトを使用して、Repository サービス操作を呼び出します。
1. そのコンストラクタを使用して `RepositoryInfomodelFactoryBean` を渡すことによって、`null` オブジェクトを作成します。このオブジェクトを使用すると、リポジトリに追加されるコンテンツを表す `Resource` オブジェクトを作成できます。
1. Create a `Resource` object by invoking the `RepositoryInfomodelFactoryBean` object’s `newImage` method and passing the following values:

   * A unique ID value by specifying `new Id()`.
   * A unique UUID value by specifying `new Lid()`.
   * リソースの名前。XDP ファイルのファイル名を指定できます。
   戻り値を `Resource` にキャストします。

1. Create a `ResourceContent` object by invoking the `RepositoryInfomodelFactoryBean` object’s `newImage` method and casting the return value to `ResourceContent`. このオブジェクトはリポジトリに追加されるコンテンツを表します。
1. リポジトリに追加する XDP ファイルを格納する `com.adobe.idp.Document` オブジェクトを渡して、`java.io.FileInputStream` オブジェクトを作成します。（[InputStream オブジェクトに基づいたドキュメントの作成](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)を参照。）
1. Add the content of the `com.adobe.idp.Document` object to the `ResourceContent` object by invoking the `ResourceContent` object’s `setDataDocument` method. Pass the `com.adobe.idp.Document` object.
1. Set the MIME type of the XDP file to add to the repository by invoking the `ResourceContent` object’s `setMimeType` method and passing `application/vnd.adobe.xdp+xml`.
1. Add the content of the `ResourceContent` object to the `Resource` object by invoking the `Resource` object ‘s `setContent` method and passing the `ResourceContent` object.
1. `Resource` オブジェクトの `setDescription` メソッドを呼び出して、リソースの説明を表す文字列値を渡すことによって、リソースの説明を追加します。
1. `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを呼び出し、次の値を渡すことによってフォームデザインをリポジトリに追加します。

   * 新しいリソースを含むリソースコレクションへのパスを指定する文字列値
   * 作成された `Resource` オブジェクト

**関連トピック**

[クイックスタート（EJB モード）：Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Java API を使用した AEM Forms の呼び出し](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 呼び出し API を使用した短時間のみ有効なプロセスの呼び出し {#invoking-a-short-lived-process-using-the-invocation-api}

Java 呼び出し API を使用して、短時間のみ有効なプロセスを呼び出すことができます。呼び出し API を使用して短時間のみ有効なプロセスを呼び出す場合は、`java.util.HashMap` オブジェクトを使用して必須のパラメーター値を渡します。各パラメーターをサービスに渡すには、`java.util.HashMap` オブジェクトの `put` メソッドを呼び出し、指定された操作を実行するためにサービスが必要とする名前と値のペアを指定します。短時間のみ有効なプロセスに属するパラメーターの正確な名前を指定します。

>[!NOTE]
>
>長期間有効なプロセスの呼び出しの詳細については、[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください。

ここでは、呼び出し API を使用して `MyApplication/EncryptDocument` という名前の短時間のみ有効な AEM Forms を呼び出す方法について説明します。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このコードの例の流れを追うには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

このプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡された保護されていない PDF ドキュメントを取得します。このアクションは `SetValue` 操作に基づいています。このプロセスの入力パラメーターは、`document` という名前の `inDoc` プロセス変数です。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。パスワードで暗号化された PDF ドキュメントは、`outDoc` という名前のプロセス変数として返されます。

### Java 呼び出し API を使用した短時間のみ有効なプロセス MyApplication/EncryptDocument の呼び出し {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Java 呼び出し API を使用して短時間のみ有効なプロセスの `MyApplication/EncryptDocument` を呼び出します。

1. adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。（[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクタを使用して `ServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクタを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。短時間のみ有効なプロセスの `MyApplication/EncryptDocument` では、`Document` 型の入力パラメーターが 1 つ必要です。次の例に示すように、`put` メソッドを呼び出す必要があるのは 1 回だけです。

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Create an `InvocationRequest` object by invoking the `ServiceClientFactory` object’s `createInvocationRequest` method and passing the following values:

   * 長期間有効なプロセスを指定する文字列値。プロセスを呼び出す `MyApplication/EncryptDocument` には、を指定しま `MyApplication/EncryptDocument`す。
   * プロセス操作名を表す文字列値。通常、短時間のみ有効なプロセス操作の名前は `invoke` です。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * `true` を指定するブール値。これを渡すと同期要求が作成されます（この値は、短時間のみ有効なプロセスを呼び出すために適用されます）。

1. `ServiceClient` オブジェクトの `invoke` メソッドを呼び出し、`InvocationRequest` オブジェクトを渡すことによって、呼び出し要求をサービスに送信します。The `invoke` method returns an `InvocationReponse` object.

   >[!NOTE]
   >
   >`false` メソッドの 4 番目のパラメーターとして `createInvocationRequest` を渡すことによって、長期間有効なプロセスを呼び出すことができます。値 `false`* を渡すと、非同期要求が作成されます。*

1. `InvocationReponse` オブジェクトの `getOutputParameter` メソッドを呼び出して、出力パラメーターの名前を指定する文字列値を渡すことによって、プロセスの戻り値を取得します。In this situation, specify `outDoc` ( `outDoc` is the name of the output parameter for the `MyApplication/EncryptDocument` process). 以下の例のように、戻り値を `Document` にキャストします。

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
1. Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. `com.adobe.idp.Document` メソッドから返された `getOutputParameter` オブジェクトを必ず使用してください。

**関連トピック**

[クイックスタート：呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[AEM Forms Java ライブラリファイルを含める](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)