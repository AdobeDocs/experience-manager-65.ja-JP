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
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 44%

---

# JEE 上の AEM Forms のセキュリティに関する一般的な考慮事項{#general-security-considerations-for-aem-forms-on-jee}

この記事では、AEM Forms環境を強化するための準備に役立つ入門情報を提供します。 これには、JEE 上の AEM Forms、オペレーティングシステム、アプリケーションサーバー、データベースセキュリティに関する前提条件の情報も含まれます。環境のロックダウンを継続する前に、この情報を確認してください。

## ベンダー固有のセキュリティ情報 {#vendor-specific-security-information}

この節では、JEE 上のAEM Formsソリューションに組み込まれるオペレーティングシステム、アプリケーションサーバー、データベースに関するセキュリティ関連の情報について説明します。

このセクションのリンクを使用して、オペレーティングシステム、データベース、およびアプリケーションサーバーのベンダー固有のセキュリティ情報を検索します。

### オペレーティングシステムのセキュリティ情報 {#operating-system-security-information}

オペレーティングシステムを保護する際には、次のようなオペレーティングシステムのベンダーが挙げている対策を実装することを慎重に検討してください。

* ユーザー、役割および権限の定義と制御
* ログと監査証跡の監視
* 不要なサービスやアプリケーションの削除
* ファイルのバックアップ

JEE 上の AEM Forms がサポートするオペレーティングシステムのセキュリティ情報については、次の表のリソースを参照してください。

<table>
 <thead>
  <tr>
   <th><p>オペレーティングシステム</p> </th>
   <th><p>セキュリティリソース</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM® AIX®セキュリティのメリット</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016 セキュリティガイド</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP または ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat® Enterprise Linux®セキュリティガイド</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">セキュリティと強化のガイドライン</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">リリース 7 のセキュリティガイド</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保護に関するドキュメント</a></td>
  </tr>
 </tbody>
</table>

### アプリケーションサーバーのセキュリティ情報 {#application-server-security-information}

アプリケーションサーバーを保護する際には、次のようなサーバーのベンダーが挙げている対策を実装することを慎重に検討してください。

* 不明な管理者ユーザー名の使用
* 不要なサービスの無効化
* コンソールマネージャの保護
* セキュリティで保護された cookie の有効化
* 不要なポートを閉じる
* IP アドレスまたはドメインでクライアントを制限する
* Java™ Security Manager を使用したプログラムによる特権の制限

JEE 上のAEM Formsがサポートするアプリケーションサーバーのセキュリティ情報については、次の表のリソースを参照してください。

<table>
 <thead>
  <tr>
   <th><p>アプリケーションサーバー</p> </th>
   <th><p>セキュリティリソース</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>「Understanding WebLogic Security」( ) を検索します。 <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">アプリケーションとその環境の保護</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">セキュリティサブシステムの設定</a></p> </td>
  </tr>
 </tbody>
</table>

### データベースのセキュリティ情報 {#database-security-information}

データベースを保護する際には、次のようなデータベースのベンダーが挙げている対策を実装することを検討してください。

* アクセス制御リスト (ACL) を使用して操作を制限する
* 非標準ポートの使用
* ファイアウォールの背後にデータベースを隠す
* 機密データをデータベースに書き込む前に暗号化する（データベースの製造元のドキュメントを参照）

JEE 上のAEM Formsがサポートするデータベースのセキュリティ情報については、次の表の資料を参照してください。

<table>
 <thead>
  <tr>
   <th><p>データベース</p> </th>
   <th><p>セキュリティリソース</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2® Product Family Library</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>「SQL Server 2016: Security」という文字列で web を検索</td>
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

次の表に、JEE 上のAEM Forms設定プロセスで開く必要があるデフォルトポートを示します。 https 経由で接続している場合は、ポート情報と IP アドレスを適宜調整してください。 ポートの構成の詳細については、 *JEE 上のAEM Formsのインストールとデプロイ* ドキュメントを作成します。

<table>
 <thead>
  <tr>
   <th><p>製品またはサービス</p> </th>
   <th><p>ポート番号</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic Managed Server</p> </td>
   <td><p>設定時に管理者が設定</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060。Global Security が有効な場合、デフォルトの SSL ポート値は 9043 です。</p> <p>9080</p> </td>
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
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>LDAP サーバーが実行されているポート。 デフォルトのポートは通常 389 です。ただし、SSL オプションを選択する場合、デフォルトのポートは通常 636 です。どのポートを指定するかは、LDAP の管理者に確認してください。</p> </td>
  </tr>
 </tbody>
</table>

### デフォルト以外の HTTP ポートを使用するように JBoss®を設定する {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server は、8080 をデフォルトの HTTP ポートとして使用します。 また、JBoss®には事前設定済みのポート 8180、8280、8380 があり、jboss-service.xml ファイルでコメントアウトされています。 このポートを既に使用しているアプリケーションがコンピューター上にある場合は、次の手順に従って、JEE 上のAEM Formsが使用するポートを変更します。

1. 次のファイルを編集用として開きます。

   シングルサーバーインストール： [JBoss®ルート]/standalone/configuration/standalone.xml

   クラスターのインストール： [JBoss®ルート]/domain/configuration/domain.xml

1. の値を変更 **ポート** 属性 **&lt;socket-binding>** タグをカスタムポート番号に追加します。 例えば、次の例では、ポート 8090 を使用します。

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. ファイルを保存して閉じます。
1. JBoss®アプリケーションサーバーを再起動します。

## JEE 上のAEM Formsのセキュリティに関する考慮事項 {#aem-forms-on-jee-security-considerations}

ここでは、知っておくべき JEE 上のAEM Forms固有のセキュリティ上の問題について説明します。

### データベースで暗号化されていない電子メール資格情報 {#email-credentials-not-encrypted-in-database}

アプリケーションに保存される電子メール資格情報は、JEE 上のAEM Formsデータベースに保存される前に暗号化されません。 電子メールを使用するようにサービスエンドポイントを設定する場合、そのエンドポイント設定の一部として使用されるパスワード情報は、データベースに保存される際に暗号化されません。

### データベース内のRights Managementに関する機密コンテンツ {#sensitive-content-for-rights-management-in-the-database}

JEE 上の AEM Forms は、JEE 上の AEM Forms データベースに、ポリシードキュメントで使用した機密ドキュメントキー情報と暗号化マテリアルを格納します。データベースへの侵入を防御することで、このような機密性の高い情報を保護することができます。

### クリアテキストフォームのパスワード {#password-in-clear-text-format-in-adobe-ds-xml}

JEE 上の AEM Forms を実行するアプリケーションサーバーでは、そのサーバー上に設定されたデータソースを介してデータベースにアクセスするように設定する必要があります。アプリケーションサーバーがデータソース構成ファイルでデータベースパスワードをクリアテキストで公開しないようにしてください。

 lc_[database].xml ファイルには、クリアテキスト形式のパスワードを含めないでください。アプリケーションサーバーのパスワードを暗号化する方法については、アプリケーションサーバーのベンダーにお問い合わせください。

>[!NOTE]
>
>JEE 上のAEM Forms JBoss®自動インストーラーがデータベースのパスワードを暗号化します。

IBM® WebSphere® Application Server およびOracleWebLogic Server は、デフォルトでデータソースのパスワードを暗号化する場合があります。 ただし、アプリケーションサーバーのドキュメントで、この処理がおこなわれていることを確認する必要があります。

### Trust Store に保存された秘密鍵の保護 {#protecting-the-private-key-stored-in-trust-store}

Trust Store に読み込まれた秘密鍵または資格情報は、JEE 上のAEM Formsデータベースに保存されます。 データベースを保護し、指定された管理者のみにアクセスを制限するには、適切な注意を払ってください。
