---
title: JEE 上の AEM Forms でサポートされているプラットフォーム
seo-title: JEE 上の AEM Forms でサポートされているプラットフォーム
description: JEE での AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
seo-description: JEE での AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# JEE 上の AEM Forms でサポートされているプラットフォーム{#supported-platforms-for-aem-forms-on-jee}

## サポートされているプラットフォーム {#supported-platforms}

### サポートレベル {#support-levels}

JEE サーバー上の AEM Forms は、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、および電子メールサーバーを自由に組み合わせて設定することができます。

このドキュメントでは、JEE 上の AEM Forms でサポートされているクライアントおよびサーバーのプラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。このドキュメントでは、その他のサポートされているソフトウェアとバージョン、例外事項、パッチ定義、およびサードパーティソフトウェアパッチサポートポリシーも示します。

>[!NOTE]
>
>* サポートされているサーバープラットフォームへの例外エラーの完全リストについては、[サポートされているサーバープラットフォームへの例外エラー](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)を参照してください。
>* JEE 上の AEM Forms でサポートされるのは、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみです。
>



### 推奨設定 {#recommendedconfigurations}

アドビはこれらの設定を推奨し、標準ソフトウェア保守契約の一部として全面的または制限的サポートを提供します。

<table>
 <tbody>
  <tr>
   <th>サポートレベル</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>A：サポート対象<br /> </td>
   <td>アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。</td>
  </tr>
  <tr>
   <td>R：制限サポート</td>
   <td>アドビは、特定の前提条件が満たされている場合、この設定に対して全面的なサポートを提供します。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。</td>
  </tr>
  <tr>
   <td>L：限定的サポート</td>
   <td>特定の条件が満たされている場合、アドビは、この設定に対して全面的なサポートと保守サービスを提供します。この設定の場合、一部の機能については使用できません。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。<br /> </td>
  </tr>
 </tbody>
</table>

### サポート対象外の設定 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| E：動作する見込み | この構成は動作する見込みであり、動作しないという報告はありません。 |
| Z：サポート対象外 | この構成はサポートされません。アドビは、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

>[!NOTE]
>
>AEM Forms をご利用のお客様がオーナーシップのコストを削減し、開発アーキテクチャを簡略化し、開発スタックを近代化できるようにするために、Adobe Experience Manager のエンタープライズプラットフォームはアプリケーションサーバーベースのデプロイメントから、スタンドアロンの OSGi ベースのデプロイメントに移行します。対応するインフラストラクチャコンポーネントは削減されますが、アドビは引き続き AEM Forms JEE スタックをサポートします。
>
>6.5のリリースでは、お客様の中で最も使用率の低いインフラストラクチャコンポーネントは、次のようにサポートされなくなりました。
>・ Oracle WebLogicアプリケーション・サーバ
>・ IBM DB2データベース
>・ IBM AIXおよびSun Solarisオペレーティング・システム
>
>新規インストールに関しては、可能な場合は AEM Forms を最新の OSGi スタックでデプロイし、モバイル向けのレスポンシブなアダプティブフォーム、マルチチャネルのインタラクティブ通信、そしてフォームデータモデルを使用したバックエンドのデータ統合などの最新技術を活用することが推奨されます。
>
>既存のユーザーは、引き続きJEE上のAEM Formsスタックのデプロイを行う必要があることを認識します。 そのような場合は、AEM Forms JEE を本文書に記載されている対応インフラストラクチャでデプロイしていただく必要があります。前回の AEM Forms リリースをサポート対象ではないプラットフォームでご使用で、AEM 6.5 Forms にアップグレードされる場合は、アドビサポートにご連絡ください。サポート対象のプラットフォームへのアップグレードをお手伝いします。

### Java 仮想マシン (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms を使用するには、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションに付属しています。Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11（64 ビット版）</p> </td>
   <td><p>Z：サポート対象外</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8（64 ビット版）</td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（ビルド 2.8、JRE 1.8.0）</td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（ビルド 2.9、JRE 1.8.0）<br /> </td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* JEE 上の AEM Forms では、実稼動環境に対して 64 ビットの JVM のみがサポートされています。
>* Java ベンダーが発表するセキュリティ情報を常に確認し、実稼働環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。
>



### データベースと CRX の永続性 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>プラットフォーム</strong></p> </td>
   <td><p><strong> 説明</strong></p> </td>
   <td><p><strong>サポートレベル</strong></p> </td>
  </tr>
  <tr>
   <td><p>ファイルシステム</p> </td>
   <td><p>Repository Microkernel（TAR MK ファイル）</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12cリリース1</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td>Oracle Database 18c </td>
   <td>リポジトリ Microkernel</td>
   <td>サポート対象</td>
  </tr> 
   <tr>
   <td>Oracle Database 19c </td>
   <td>リポジトリ</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>リポジトリ Microkernel</td>
   <td>R：制限サポート</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R：制限サポート</td>
  </tr>
 </tbody>
</table>

* IBM DB2 への新規インストールはサポートされていません。AEM 6.5 Forms にアップグレードされる既存のお客様の場合のみサポートされます。
* MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。
* AEM デプロイメントを最大限活用するために、アドビは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。
* アドビカスタマーケアは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
* 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
* MongoDB Storage Engine WiredTiger のみサポートされます。
* MongoDB Sharding は AEM ではサポートされていません。
* JEE 上の AEM Forms はRDBMK 永続性タイプの MySQL をサポートしません。
* Document Security モジュールは、Content Repository を使用しません。Document Security のみを使用して、HTML Workspace、HTML5 フォーム、アダプティブフォームを使用しない場合は、Content Repository をインストールしないでください。
* JEE上のAEM Formsは、AEMリポジトリ(CRX-Repository)の永続化にMySQLを使用することをサポートしていません。


### データベースドライバー {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>データベース </th>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar（バージョン 5.1.44）</p> </td>
   <td><p>JEE での AEM Forms のインストールに付属</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>JEE での AEM Forms のインストールに付属</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC ドライバー</p> <p>ojdbc8.jar（バージョン 19.3.0.0.0）<br /> </p> </td>
   <td><p><a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">Oracle Web サイト</a>からダウンロードしてください。</p> </td>
  </tr>
 </tbody>
</table>

### アプリケーションサーバー {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> プラットフォーム</strong></p> </td>
   <td><p><strong>サポートレベル</strong></p> </td>
   <td><p><strong>サポートされているパッチ定義</strong></p> </td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>パッチと累積パッチ（サポート対象の EAP バージョン用）</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>IBM® WebSphere® のクラスターは、Network Deployment エディションでのみサポートされます。

### サーバーオペレーティングシステム {#server-operating-systems}

#### 実稼動環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> プラットフォーム</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016（64ビット）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) （64ビット）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、および緊急アップデート</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64ビット）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパック、累積パッチ、および緊急セキュリティアップデート</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3（64 ビット）</td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td>
  </tr>
  <tr>
   <td>CentOS 7 (64-bit)<sup> [6]</sup></td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td>
  </tr>
 </tbody>
</table>

#### 視覚化環境 {#virtualized-environment}

JEE 上の AEM Forms は、物理マシンまたはバーチャル環境で実行できます。ただし、バーチャル環境での AEM Forms の使用に問題が発生した場合は、その問題の物理マシン上での再現を試みてください。問題が物理マシン上で引き続き発生する場合は、アドビサポートに問い合わせて解決してください。 物理マシン上で再現することができない問題に関しては、バーチャル環境のベンダーにお問い合わせください。

#### 開発環境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム（基本バージョン）</strong></p> </th>
   <th>サポートレベル</th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64-bit</p> </td>
   <td>E：動作する見込み</td>
   <td><p>サービスパックと重要なアップデート</p> </td>
  </tr>
 </tbody>
</table>

### サポートされているサーバープラットフォームの例外事項 {#exceptions-to-supported-server-platforms}

JEE サーバーでの AEM Forms の設置でプラットフォームを選択するときは、次の例外事項を考慮してください。

1. JEE上のAEM Formsは、IBM® WebSphere®をMySQLでサポートしていません。
1. JEE 上の AEM Forms では、SUSE Linux Enterprise Server 12 上での および JBoss をサポートしていません。SUSE Linux Enterprise Server 12 上では、IBM WebSphere のみがサポートされています。
1. JEE 上の AEM Forms は、JBoss® では Oracle Java™ SE 以外のいかなる JDK もサポートしていません。
1. JEE 上の AEM Forms は、IBM® WebSphere® では IBM® JDK 以外のいかなる JDK もサポートしていません。
1. CRX-repositoryは、TarMK、MongoDB、およびリレーショナルデータベース(RDBMK)の永続性タイプをサポートします。 アプリケーションサーバーとCRX-repositoryの間に2つの異なるデータベースシステムを置くことはできません。 ただし、JEE上のAEM Forms環境では、MongoMKをCRXリポジトリで使用し、サポートされているリレーショナルデータベースをアプリケーションサーバーで使用できます。
1. JEE 上の AEM Forms は CentOS 上の WebSphere Application Server をサポートしていません。
1. JEE 上の AEM Forms では、JBoss ロールベースのアクセス制御（RBAC）をサポートしていません。

この他に、JEE 上での Adobe AEM Forms の導入のためにソフトウェアを選択する際には、次の項目を考慮してください。

* JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。
* クラスタベースのインストールは、TarMK 永続性タイプをサポートしません。サポートされている永続性については、[AEM Forms のインストールに永続性タイプを選択する](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。
* JEE 上の AEM Forms では、弊社の[サードパーティソフトウェアサポートポリシー](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)に従い、さまざまなサードパーティ製のソフトウェアをサポートしています。
* JEE 上の AEM Forms では、サードパーティベンダーによって提供されているサポートに基づいてプラットフォームをサポートします。組み合わせによっては、サードパーティベンダーが許可しない場合があります。例えば、多くのベンダーが、自社のアプリケーションサーバーを Oracle で使用することを認めていません。この結果、JEE 上の AEM Forms でもこれらの組み合わせをサポートしていません。サポートされているソフトウェアバージョンを確実に選択するようにするために、サードパーティベンダーのサポート表もチェックしてください。
* JEE 上の AEM Forms は TarMK コールドスタンバイをサポートしません。
* JEE 上の AEM Forms は垂直クラスタリングをサポートしません。
* JEE 上の AEM Forms では、クラスター環境での MySQL データベースをサポートしていません。
* 削除または更新されたプラットフォームの一覧は、[AEM 6.5 Forms 新機能の概要](../../forms/using/whats-new.md)の文書を参照ししてください。

### LDAP サーバー (オプション) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品（基本バージョン）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle Unified Directory（OUD）11g リリース 2</td>
   <td>サービスパック</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>メンテナンスリリースおよび修正パック</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>フィーチャーパックと暫定フックス</p> </td>
  </tr>
 </tbody>
</table>

### 電子メールサーバー (オプション) {#email-servers-optional}

| 製品 |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### コンテンツマネージャーと対応するコネクタ {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>製品<br /> </strong></td>
   <td><strong>バージョン</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager サーバー</td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td>IBM Content Manager クライアント</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova のサポート {#support-for-cordova}

AEM FormsアプリケーションでApache Cordovaがサポートされるようになりました。次に、サポートされるCordovaのプラットフォーム固有のバージョンを示します。

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### PDF Generator のソフトウェアサポート {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品</strong></p> </th>
   <th><p><strong>PDF への変換でサポートされている形式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 Classic最新バージョンを追跡</a> （英語のみ）</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式(BMP、GIF、JPG、TIF、TIFF、TIFF、TIFF、TIF、TIFJPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator では、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみがサポートされます。
>
>さらに、次の点に注意してください。
>
>* PDF Generator requires 32-bit version of [Acrobat 2017 classic track version 17.011.30078 or later](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) to perform the conversion.
>* PDF Generator では、32 ビットリテール版の Microsoft Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>* PDF Generator では Microsoft Office 365 をサポートしていません。
>* PDF Generator の OpenOffice 向け変換機能は、Windows と Linux でのみサポートされています。
>* 「OCR PDF」、「PDF を最適化」、「PDF を書き出し」の各機能は、Windows でのみサポートされています。
>* Acrobat のバージョンは、PDF Generator 機能を有効にするために、AEM Forms にバンドルされます。バンドルされたバージョンは、AEM Forms PDF Generator で使用するために、AEM Forms ライセンスの期間中、AEM Forms でのみプログラムによってアクセスされます。For more information, refer to AEM Forms product description as per your deployment ([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) or [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
   >
   >
* PDF Generator サービスは、Microsoft Windows 10 をサポートしていません。
>



### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}

AEM Forms の次のサブシステムは、[リハビリテーション法 508 条](https://www.section508.gov/)に準拠していません。

* アダプティブフォームオーサリング UI
* Forms Manager オーサリング UI
* Correspondence Management オーサリング UI
* 管理 UI（管理コンソール UI）

## JEE 上の AEM Forms の必要システム構成 {#system-requirements-for-aem-forms-on-jee}

### 最小ハードウェア要件 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>プラットフォーム</td>
   <td>最小ハードウェア要件</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680、2.4 GHz プロセッサー（またはそれと同等のプロセッサー）<br /> VMWare ESX 5.1 以降<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：15GB の一時的空き容量のほかに、<br />JEF 上の AEM Forms 用に22GB の空き容量</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2、1 つの vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium（3 つの ECU）<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br /> JEF 上の AEM Forms 用に 22GB の空き容量</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2、1 つの vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium（3 つの ECU）<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br />JEE 上の AEM Forms 用に 22 GB の空き容量<br /> </td>
  </tr>
  <tr>
   <td>小規模な実稼働環境の場合のハードウェア要件</td>
   <td>
    <ul>
     <li><strong>Intel を使用している環境</strong>：Intel® Xeon® E5-2680、2.4 GHz 以上デュアルコアプロセッサーを使用するとパフォーマンスがさらに向上します。</li>
     <li><strong>メモリ：</strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

上記以外の要件については、以下を参照してください。

* [JEE上のシングルサーバーAEM Formsの導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [JEE 上でのクラスター化された AEM Forms の導入に必要なシステム構成
   ](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## JEE 上の AEM Forms でサポートされているクライアント {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10(Enterprise、Pro、Basic)</p> <p>32 または 64 ビット版</p> <p> </p> </td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
 </tbody>
</table>

* インストールのためのディスク空き容量： 1.7 GB（Workbench のみ）、2.7 GB（Workbench、 Designer 、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB （一時的インストールディレクトリ）、200 MB （ユーザー一時ディレクトリ）、および200 MB（Windows 一時ディレクトリ）。これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

* Workbench を実行するためのメモリ：2 GB の RAM
* ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー
* 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
* JEE サーバーの AEM Forms に対する TCP/IPv4 または TCP/IPv6 ネットワーク接続
* Workbench を Windows にインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### Designer {#designer}

>[!NOTE]
>
>WindowsにDesignerをインストールするには、管理者権限でインストーラーを実行します。

* Microsoft® Windows® 2016 Server、Microsoft Windows 10

   * 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
   * 1 GB の RAM（32-bit OS の場合）または 2 GB の RAM（64-bit OS の場合）
   * 16 GB のディスク空き容量（32-bit OS の場合）または 20 GB のディスク空き容量（64-bit OS の場合）

* グラフィックメモリ — 128 MBのGPU（256 MBを推奨）
* 2.35 GB のハードディスク空き容量
* DVD-ROM ドライブ
* Internet Explorer 10 または 11; Firefox 45.x
* 1024 X 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。

### Adobe Acrobat と Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat および Adobe Reader（Base）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017（クラシックトラック）</td>
   <td>バージョン 17.011.30078 以降<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat DC Product Family では、基本的に別々の製品である Acrobat と Reader のそれぞれに、「クラシック」と「継続」の 2 種類のトラックが用意されています。For details and a comparison of the two tracks, see [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### ブラウザー {#browsers}

#### デスクトップ {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>ブラウザー（ベース）</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge（エバーグリーン）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパックとアップデート</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox（エバーグリーン）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E：動作する見込み</td>
   <td> すべてのアップデート</td>
  </tr>
  <tr>
   <td><p>Google Chrome（エバーグリーン）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Google Chrome および Firefox（MAC OS X 上）</td>
   <td>A：サポート対象<br /> <br /> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A：サポート対象</td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A：サポート対象</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>以下にデスクトップに対する一部のブラウザー関連の例外事項を示します。
>
>* 多くの最新のブラウザーは現在、NPAPI ベースのプラグインをサポートしていません。For information about how it impacts AEM Forms applications and workflows, see [Discontinuation of NPAPI browser plugins and its impact](https://helpx.adobe.com/jp/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* Safari は Macintosh OS X でのみサポートされています。
>* Acrobat DC 以降のバージョンでは、Workspace は Macintosh OS X 10.6 および 10.7 上の Safari 5.1 をサポートしています。For more information about Safari 5.1 compatibility with Adobe Reader, Acrobat, see [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* Administration Console は Safari ではサポートされていません。
>* Correspondence Managementは、AEM 6.1 FormsのWindows® Internet Explorer 9.0をサポートしていません。
>* Forms ポータルは、アクセシビリティのために、JAWS 14.0 画面読み上げソフトウェアを Internet Explorer 11 でサポートしています。
>



#### モバイルクライアント {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>ブラウザー（ベース）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome on Android™ 4.1.2 以降</p> </td>
   <td><p>すべてのアップデート</p> </td>
  </tr>
  <tr>
   <td>Safari（iOS 11.0 以降）</td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>すべてのアップデート<br /> </td>
  </tr>
  <tr>
   <td>ネイティブの Andriod ブラウザー（Android™ 4.4 以降で稼働するブラウザー）</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal は iPad の Safari でのみサポートされています。
>



### AEM Forms アプリケーション {#aem-forms-workspace-app}

#### モバイルデバイスのサポート {#mobile-device-support}

AEM Forms アプリケーションは次のプラットフォームで利用可能です。

| **プラットフォーム** | **サポートされているデバイス** |
|---|---|
| Apple iOS 以上 | iOS 11以降を実行するApple iPhone、iPad、iPad Air、iPad mini。 |
| Google Android | Android 5.1 以降。AEM Formsアプリは、7インチと10インチのSamsung Galaxyタブレットと人気のあるスマートフォンで認定されています。 |
| Microsoft Windows | Microsoft Windows 10オペレーティングシステムを実行するMicrosoft Surfaceデバイス、タブレット、ラップトップ、およびデスクトップ。 |

### Adobe Flash Player {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player（ベース）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Flash Player 最新版</p> </td>
   <td><p>マイナーバージョンとアップデート</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe will [stop updating and distributing the Flash Player at the end of 2020](https://theblog.adobe.com/adobe-flash-update/).

### Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office の必要システム構成を見るには、[ここ](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。

### クライアントサポートの例外事項 {#exceptions-to-client-support}

JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。

## サードパーティパッチサポートポリシー {#third-party-patch-support-policy}

JEE 上の AEM Forms のサードパーティソフトウェアの必要システム構成は、それぞれの製品ドキュメントの「必要システム構成」セクションに記述されています。All documentation can be accessed from [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

JEE 上の AEM Forms のサードパーティリファレンスプラットフォームは、JEE 上の AEM Forms の開発とリリースの時点におけるサードパーティインフラストラクチャの特定のパッチレベルを記述してあり、そのバージョンの JEE 上の AEM Forms によってサポートされているインフラストラクチャの最小パッチ/サービスパックレベルを形成しています。

アドビシステムズ社では、サードパーティベンダーがリリース時に JEE 上の AEM Forms がサポートするバージョンとの後方互換性を保証していると仮定して、サードパーティベンダーの緊急および推奨パッチをサポートします。アドビシステムズ社は、JEE 上の AEM Forms ドキュメントに記載の最小パッチレベル後にリリースされたパッチのみをサポートします。

場合によっては、アドビシステムズ社は、主要な機能を変更しそのために完全な後方互換性をサポートしなくなったサードパーティアップデートをサポートしません。For details on the supported updates, see [Supported patch definitions](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html) for specific vendor products and the patch types Adobe supports.

アドビシステムズ社の管理の及ばない状況においては、後方互換性を主張しているサードパーティ製パッチは、アドビ製品またはお客様の環境に悪い影響を及ぼす可能性があります。このような場合、アドビシステムズ社は、お客様がサードパーティからの緊急パッチを重要なシステムに適用する前にその影響を評価することを推奨します。アドビシステムズ社はサードパーティと共に妥当なビジネス努力を払って、通常のアドビサポートプログラムを通してあるいはサードパーティがパッチの問題を修正することによって、そのような問題を解決します。このことは、アドビによってサポートされる新たにリリースされたサードパーティ製パッチが、ベンダーによってマニュアルに記載されているようにまたは JEE 上の AEM Forms と機能することを保証するものではありません。

アドビシステムズ社は、任意の時点で、JEE 上の AEM Forms リリースおよびそれらのサポートされているパッチ定義によってサポートされているサードパーティリファレンスプラットフォームを変更する権利を保留します。

サードパーティ製パッチのその他の情報については、Adobe Enterprise Support サイトで、ご使用の製品に関するナレッジベース記事を検索することによっても見つけられることがあります。
