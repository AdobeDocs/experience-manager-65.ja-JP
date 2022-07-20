---
title: JEE 上の AEM Forms のセキュリティに関する一般的な考慮事項
seo-title: General Security Considerations for AEM Forms on JEE
description: JEE 上の AEM Forms 環境を強化するための準備について説明します。
seo-description: Learn how to prepare for hardening your AEM Forms on JEE environment.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 100%

---

# JEE 上の AEM Forms のセキュリティに関する一般的な考慮事項{#general-security-considerations-for-aem-forms-on-jee}

この記事には、AEM Forms 環境を堅牢化するための準備に役立つ、基本的な情報を記載しています。これには、JEE 上の AEM Forms、オペレーティングシステム、アプリケーションサーバー、データベースセキュリティに関する前提条件の情報も含まれます。環境のロックダウンを継続する前に、この情報を確認してください。

## ベンダー固有のセキュリティ情報 {#vendor-specific-security-information}

この節には、JEE 上の AEM Forms ソリューションに統合されるオペレーティングシステム、アプリケーションサーバーおよびデータベースに関するセキュリティ関連情報を記載しています。

このセクションにあるリンクを使用して、使用しているオペレーティングシステム、データベースおよびアプリケーションサーバーのベンダーに固有のセキュリティ情報を検索してください。

### オペレーティングシステムのセキュリティ情報 {#operating-system-security-information}

オペレーティングシステムを保護する際には、次のようなオペレーティングシステムのベンダーが挙げている対策を実装することを慎重に検討してください。

* ユーザー、ロール、権限を定義し、制御する
* ログと監査記録を監視する
* 不要なサービスとアプリケーションを削除する
* ファイルのバックアップを作成する

JEE 上の AEM Forms がサポートするオペレーティングシステムのセキュリティ情報については、次の表のリソースを参照してください。

<table>
 <thead>
  <tr>
   <th><p>オペレーティングシステム</p> </th>
   <th><p>セキュリティ情報</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM AIX Security Benefits</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016 セキュリティガイド</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP または ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat Enterprise Linux セキュリティガイド</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">セキュリティと強化のガイドライン</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">リリース 7 のセキュリティガイド</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護に関するドキュメント</a></td>
  </tr>
 </tbody>
</table>

### アプリケーションサーバーのセキュリティ情報 {#application-server-security-information}

アプリケーションサーバーを保護する際には、次のようなサーバーのベンダーが挙げている対策を実装することを慎重に検討してください。

* 管理者ユーザー名として推測しにくい名前を使用する
* 不要なサービスを無効にする
* コンソールマネージャーを保護する
* cookie の保護を有効にする
* 不要なポートを閉じる
* IP アドレスまたはドメインでクライアントを制限する
* Java™ Security Manager を使用して、プログラムによって権限を制限する

JEE 上の AEM Forms がサポートするアプリケーションサーバーのセキュリティ情報については、次の表の資料を参照してください。

<table>
 <thead>
  <tr>
   <th><p>アプリケーションサーバー</p> </th>
   <th><p>セキュリティ情報</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p><a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a> で Understanding WebLogic Security を検索してください。</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">アプリケーションとその環境の保護</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">セキュリティサブシステムの設定</a></p> </td>
  </tr>
 </tbody>
</table>

### データベースのセキュリティ情報 {#database-security-information}

データベースを保護する際には、次のようなデータベースのベンダーが挙げている対策を実装することを検討してください。

* アクセス制御リスト（ACL）を使用して操作を制限する
* 非標準ポートを使用する
* ファイアウォールの内側にデータベースを隠す
* 機密データをデータベースに書き込む前に暗号化する（データベース製造元のドキュメントを参照）

JEE 上の AEM Forms がサポートするデータベースのセキュリティ情報については、次の表の資料を参照してください。

<table>
 <thead>
  <tr>
   <th><p>データベース</p> </th>
   <th><p>セキュリティ情報</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2 Product Family ライブラリ</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>「SQL Server 2016: Security」について web を検索してください。</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/ja/security.html">MySQL 5.0 General Security Issues</a></p> <p><a href="https://dev.mysql.com/doc/refman/8.0/ja/security.html">MySQL 5.1 General Security Issues</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>「<a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle 12g Documentation</a>」のセキュリティの章を参照してください。</p> </td>
  </tr>
 </tbody>
</table>

次の表では、JEE 上の AEM Forms の設定プロセス中に開く必要のあるデフォルトポートについて説明します。https 経由で接続している場合、ポート情報と IP アドレス情報を適宜修正する必要があります。ポートの設定について詳しくは、使用しているアプリケーションサーバー版の「*JEE 上の AEM Forms のインストールおよびデプロイ*」ドキュメントを参照してください。

<table>
 <thead>
  <tr>
   <th><p>製品またはサービス</p> </th>
   <th><p>ポート番号</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic 管理対象サーバー</p> </td>
   <td><p>設定時に管理者によって指定される</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060（Global Security が有効になっている場合、デフォルト SSL ポート値は 9043）</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>BAM サーバー</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>LDAP サーバーを実行しているポート。デフォルトのポートは通常 389 です。ただし、SSL オプションを選択する場合、デフォルトのポートは通常 636 です。どのポートを指定するかは、LDAP の管理者に確認してください。</p> </td>
  </tr>
 </tbody>
</table>

### デフォルト以外の HTTP ポートを使用するための JBoss の設定 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss Application Server は、デフォルトの HTTP ポートとして 8080 を使用します。また、JBoss には事前設定のポート 8180、8280 および 8380 があり、これらは jboss-service.xml ファイルでコメントアウトされています。既にこのポートを使用しているアプリケーションがコンピューター上にある場合は、以下の手順に従って JEE 上の AEM Forms で使用するポートを変更してください。

1. 次のファイルを編集用として開きます。

   シングルサーバーのインストール： [JBoss ルート]/standalone/configuration/standalone.xml

   クラスターのインストール： [JBoss ルート]/domain/configuration/domain.xml

1. **&lt;socket-binding>** タグの **port** 属性の値をカスタムポート番号に変更します。例えば、次の例では、ポート 8090 を使用します。

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. ファイルを保存して閉じます。
1. JBoss アプリケーションサーバーを再起動します。

## JEE 上の AEM Forms セキュリティに関する考慮事項 {#aem-forms-on-jee-security-considerations}

ここでは、理解しておく必要のある JEE 上の AEM Forms 固有のセキュリティの問題について説明します。

### データベース内の電子メールの資格情報は暗号化されない {#email-credentials-not-encrypted-in-database}

アプリケーションに保存されている電子メールの資格情報は、JEE 上の AEM Forms データベースに保存される前に暗号化されません。サービスのエンドポイントで電子メールを使用するように設定した場合、エンドポイント設定の一部として使用したパスワード情報は、データベースに保存される前に暗号化されません。

### データベース内の Rights Management に関する機密性情報 {#sensitive-content-for-rights-management-in-the-database}

JEE 上の AEM Forms は、JEE 上の AEM Forms データベースに、ポリシードキュメントで使用した機密ドキュメントキー情報と暗号化マテリアルを格納します。データベースへの侵入を防御することで、このような機密性の高い情報を保護することができます。

### クリアテキストフォームのパスワード {#password-in-clear-text-format-in-adobe-ds-xml}

JEE 上の AEM Forms を実行するアプリケーションサーバーでは、そのサーバー上に設定されたデータソースを介してデータベースにアクセスするように設定する必要があります。アプリケーションサーバーがデータソース構成ファイルでデータベースパスワードをクリアテキストで公開しないようにしてください。

 lc_[database].xml ファイルには、クリアテキスト形式のパスワードを含めないでください。アプリケーションサーバーのパスワードを暗号化する方法については、アプリケーションサーバーのベンダーにお問い合わせください。

>[!NOTE]
>
>JEE 上の AEM Forms JBoss 自動インストーラーがデータベースのパスワードを暗号化します。

IBM WebSphere Application Server および Oracle WebLogic Server は、デフォルトでデータソースのパスワードを暗号化している可能性があります。ただし、これが行われていることをアプリケーションサーバーのドキュメントで確認してください。

### Trust Store に保管された秘密鍵の保護 {#protecting-the-private-key-stored-in-trust-store}

Trust Store からインポートされた秘密鍵や秘密鍵証明書は、JEE 上の AEM Forms データベースに保管されます。適切な予防策を講じて、データベースを保護し、指名された管理者のみにアクセスを制限します。
