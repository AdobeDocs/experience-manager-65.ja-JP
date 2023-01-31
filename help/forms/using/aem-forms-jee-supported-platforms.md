---
title: JEE 上の AEM Forms でサポートされているプラットフォーム
seo-title: Supported Platforms for AEM Forms on JEE
description: JEE での AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 26e71c5f09eb9fa3f3eda01deb871ac63e348a30
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 89%

---


# JEE 上の AEM Forms でサポートされているプラットフォーム {#supported-platforms-for-aem-forms-on-jee}

## サポートされているプラットフォーム {#supported-platforms}

<div class="preview">

Adobeが [完全インストーラ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) JEE 上のAEM 6.5 Forms Service Pack 12(6.5.12.0) とパッチインストーラー 完全なインストーラーは新しいプラットフォームをサポートし、パッチインストーラーはバグ修正のみを含みます。

JEE 上のAEM 6.5 Forms環境で最新のソフトウェアを使用する場合は、新規インストールを実行するか、最新のソフトウェアを使用することを計画している場合、Adobeでは [AEM 6.5.12.0 Forms on JEE フルインストーラー](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) 2019 年 4 月 8 日にリリースされた、AEM 6.5 Formsインストーラーの代わりに 2022 年 3 月 3 日にリリースされました。

</div>

### サポートレベル {#support-levels}

JEE サーバー上の AEM Forms は、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、および電子メールサーバーを自由に組み合わせて設定することができます。

このドキュメントでは、JEE 上の AEM Forms でサポートされているクライアントおよびサーバーのプラットフォームを示します。Adobe では、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。このドキュメントでは、その他のサポートされているソフトウェアとバージョン、例外事項、パッチ定義、およびサードパーティソフトウェアパッチサポートポリシーも示します。

>[!NOTE]
>
>- サポートされているサーバープラットフォームへの例外エラーの完全リストについては、[サポートされているサーバープラットフォームへの例外エラー](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)を参照してください。
>- JEE 上の AEM Forms でサポートされるのは、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみです。


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
   <td>Adobe ではこの構成への完全なサポートと保守を提供します。この構成は、Adobe の品質保証プロセスでカバーされます。</td>
  </tr>
  <tr>
   <td>R：限定サポート</td>
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
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E：動作する見込み | この構成は動作する見込みであり、動作しないという報告はありません。 |
| Z：サポート対象外 | この構成はサポートされません。Adobe では、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

>[!NOTE]
>
>AEM Forms をご利用のお客様がオーナーシップのコストを削減し、開発アーキテクチャを簡略化し、開発スタックを近代化できるようにするために、Adobe Experience Manager のエンタープライズプラットフォームはアプリケーションサーバーベースのデプロイメントから、スタンドアロンの OSGi ベースのデプロイメントに移行します。対応するインフラストラクチャコンポーネントは削減されますが、アドビは引き続き AEM Forms JEE スタックをサポートします。
>
>6.5 のリリースでは、お客様の中で最も使用率の低いインフラストラクチャコンポーネントは、次のようにサポートされなくなりました。
>
>- IBM DB2 データベース
>- IBM AIX および Sun Solaris オペレーティングシステム
>
>新規インストールに関しては、可能な場合は AEM Forms を最新の OSGi スタックでデプロイし、モバイル向けのレスポンシブなアダプティブフォーム、マルチチャンネルのインタラクティブ通信、そしてフォームデータモデルを使用したバックエンドのデータ統合などの最新技術を活用することが推奨されます。
>
>既存のお客様は、AEM Forms を引き続き JEE スタック上でデプロイしていただく必要があります。そのような場合は、AEM Forms JEE を本文書に記載されている対応インフラストラクチャでデプロイしていただく必要があります。前回の AEM Forms リリースをサポート対象ではないプラットフォームでご使用で、AEM 6.5 Forms にアップグレードされる場合は、アドビサポートにご連絡ください。サポート対象のプラットフォームへのアップグレードをお手伝いします。

### Java 仮想マシン（JVM） {#java-virtual-machines-jvm}

Adobe Experience Manager Forms を使用するには、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションに付属しています。Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr> 
   <td><p>OracleJava™ SE 11（64 ビット） <sup> [8] </sup> </p>  </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリースとアップデート </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64 ビット</td>
   <td>Z：サポート対象外</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64 ビット</td>
   <td>Z：サポート対象外</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8（64 ビット版）</td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（ビルド 2.9、JRE 1.8.0）IBM® JDK SR6-FP26<br /> </td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM JAVA1.8.0_291（ビルド 8.0.6.30）<br /> </td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Java ベンダーが発表するセキュリティ情報を常に確認し、実稼働環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることをお勧めします。
>- JEE 上の AEM Forms では、実稼動環境に対して 64 ビットの JVM のみがサポートされています。


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
   <td><p> MongoDB Enterprise 4.0（非推奨） </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>Oracleデータベース 12c リリース 2(12.2.0.1.0)（非推奨）</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c（Standard、Real Application Clusters（RAC）および Enterprise エディション） </td>
   <td>Microkernal リポジトリ </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016（非推奨）</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1（非推奨）</td>
   <td>リポジトリ Microkernel</td>
   <td>R：限定サポート</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35（非推奨） </td>
   <td>-</td>
   <td>R：限定サポート</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R：限定サポート</td>
  </tr>
 </tbody>
</table>

- IBM DB2 への新規インストールはサポートされていません。AEM 6.5 Forms にアップグレードされる既存のお客様の場合のみサポートされます。
- MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。
- AEM デプロイメントを最大限活用するために、アドビは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。
- Adobe カスタマーサービスは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
- 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
- MongoDB Storage Engine WiredTiger のみサポートされます。
- MongoDB Sharding は AEM ではサポートしていません。
- JEE 上の AEM Forms はRDBMK 永続性タイプの MySQL をサポートしません。
- Document Security モジュールは、Content Repository を使用しません。Document Security のみを使用して、HTML Workspace、HTML5 フォーム、アダプティブフォームを使用しない場合は、Content Repository をインストールしないでください。
- JEE 上の AEM Forms は、AEM リポジトリ（CRX リポジトリ）を永続化するための MySQL の使用をサポートしていません。

### データベースドライバー {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>データベース </th>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar（バージョン 5.1.44）</p> </td>
   <td><p>JEE での AEM Forms のインストールに付属</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 6.2.1.0（非推奨）<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>AEM Forms on JEE のインストールに付属</p> </td>
  </tr>
    <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>AEM Forms on JEE のインストールに付属</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Microsoft の web サイトからダウンロードします。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC ドライバー</p> <p>ojdbc8.jar（バージョン 19.3.0.0.0）<br /> </p> </td>
   <td><p><a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle Web サイト</a>からダウンロードしてください。</p> </td>
  </tr>
 </tbody>
</table>

### アプリケーションサーバー {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> プラットフォーム</strong></p> </td>
   <td><p><strong>サポートレベル</strong></p> </td>
   <td><p><strong>サポートしているパッチ定義</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1（12c R2）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup> （廃止） </p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>パッチと累積パッチ（サポート対象の EAP バージョン用）</p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
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
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft Windows Server 2019（64 ビット版）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td> Microsoft Windows Server 2016（64 ビット版）（非推奨）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8（Kernel 4.x）（64 ビット版）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、および緊急アップデート</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7（Kernel 3.x）（64 ビット版）（非推奨）</td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、および緊急アップデート</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64 ビット版）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパック、累積パッチ、および緊急セキュリティアップデート</p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7 Update 3（64 ビット）</td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td>
  </tr>
  <tr>
   <td>CentOS 7（64 ビット版）<sup>[6]</sup></td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td>
  </tr>
 </tbody>
</table>

#### 視覚化環境 {#virtualized-environment}

JEE 上の AEM Forms は、物理マシンまたはバーチャル環境で実行できます。ただし、バーチャル環境での AEM Forms の使用に問題が発生した場合は、その問題の物理マシン上での再現を試みてください。物理マシン上でも問題が発生する場合は、アドビサポートにお問い合わせいただき、解決を試みてください。物理マシン上で再現することができない問題に関しては、バーチャル環境のベンダーにお問い合わせください。

#### 開発環境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム（基本バージョン）</strong></p> </th>
   <th>サポートレベル</th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64 ビット版</p> </td>
   <td>E：動作する見込み</td>
   <td><p>サービスパックと重要なアップデート</p> </td>
  </tr>
 </tbody>
</table>

### サポートされているサーバープラットフォームの例外事項 {#exceptions-to-supported-server-platforms}

JEE サーバーでの AEM Forms の設置でプラットフォームを選択するときは、次の例外事項を考慮してください。

1. AEM Forms on JEE では、MySQL を搭載した IBM® WebSphere® をサポートしていません。
1. AEM Forms on JEE では、SUSE Linux Enterprise Server 12 上での JBoss をサポートしていません。SUSE Linux Enterprise Server 12 上では、IBM WebSphere のみがサポートされています。
1. JEE 上のAEM Formsは、JBoss®ではOracleJava™ SE 以外の JDK をサポートしていません。
1. JEE 上のAEM Formsは、IBM® WebSphere®ではIBM® JDK 以外の JDK をサポートしていません。
1. CRX リポジトリは、TarMK、MongoDB、およびリレーショナルデータベース（RDBMK）の永続性をサポートします。アプリケーションサーバーと CRX リポジトリ間に 2 つの異なるデータベースシステムを持つことはできません。ただし、AEM Forms on JEE 環境では、CRX リポジトリで MongoMK を使用でき、アプリケーションサーバーでサポートしているリレーショナルデータベースを使用できます。
1. AEM Forms on JEE は CentOS 上の WebSphere Application Server をサポートしていません。
1. JEE 上の AEM Forms では、JBoss ロールベースのアクセス制御（RBAC）をサポートしていません。
1. JEE 上のAEM Formsは、OracleJava™ SE 11（64 ビット）SDK（アプリケーションサーバー JBoss EAP 7.4 用のみ）をサポートしています。

この他に、JEE 上での Adobe AEM Forms の導入のためにソフトウェアを選択する際には、次の項目を考慮してください。

- JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。
- クラスタベースのインストールは、TarMK 永続性タイプをサポートしません。サポートされている永続性については、[AEM Forms のインストールに永続性タイプを選択する](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。
- JEE 上の AEM Forms では、弊社の[サードパーティソフトウェアサポートポリシー](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)に従い、さまざまなサードパーティ製のソフトウェアをサポートしています。
- JEE 上の AEM Forms では、サードパーティベンダーによって提供されているサポートに基づいてプラットフォームをサポートします。組み合わせによっては、サードパーティベンダーが許可しない場合があります。例えば、多くのベンダーが、自社のアプリケーションサーバーを Oracle で使用することを認めていません。その結果、JEE 上のAEM Formsでもこれらの組み合わせをサポートしていません。 サポートしているソフトウェアバージョンを確実に選択するようにするために、サードパーティベンダーのサポート表もチェックしてください。
- JEE 上の AEM Forms は TarMK コールドスタンバイをサポートしません。
- JEE 上の AEM Forms は垂直クラスタリングをサポートしません。
- JEE 上のAEM Formsは、クラスター環境では MySQL データベースをサポートしていません。
- 削除または更新されたプラットフォームの一覧は、[AEM 6.5 Forms 新機能の概要](../../forms/using/whats-new.md)のドキュメントを参照してください。

### LDAP サーバー（オプション） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品（基本バージョン）</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
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

### 電子メールサーバー（オプション） {#email-servers-optional}

| 製品 |
| ----------------------- |
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
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager サーバー（非推奨） </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> IBM Content Manager クライアント（非推奨）</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2016 年（廃止）<br /> </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint </td>
   <td>2019年<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova のサポート {#support-for-cordova}

AEM Forms アプリケーションで Apache Cordova がサポートされるようになりました。サポートされている Cordova プラットフォームのバージョンは以下のとおりです。

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android 6.0.0
- Cordova Windows 4.4.3

### PDF Generator のソフトウェアサポート {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品</strong></p> </th>
   <th><p><strong>PDF への変換でサポートされている形式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 Classic トラック</a> 最新バージョン</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 Classic トラック</a> 最新バージョン（非推奨）</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 （非推奨）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（非推奨）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（非推奨）<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016（非推奨）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 （非推奨）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
PDF Generator では、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみがサポートされます。
さらに、次の点に注意してください。
- PDF Generator で変換を実行するには、32 ビット版の [Acrobat 2020 Classic トラックバージョン 20.004.30006](https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html) または Acrobat 2017 バージョン 17.011.30078 が必要です。
- PDF Generator では、32 ビットリテール版の Microsoft Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
- PDF Generator では Microsoft Office 365 をサポートしていません。
- PDF Generator の OpenOffice 向け変換機能は、Windows と Linux でのみサポートされています。
- OCR PDF、PDF 最適化、PDF 書き出しの各機能は、Windows でのみサポートされます。
- Acrobat のバージョンは、PDF Generator 機能を有効にするために、AEM Forms にバンドルされます。バンドルされたバージョンは、AEM Forms PDF Generator で使用するために、AEM Forms ライセンスの期間中、AEM Forms でのみプログラムによってアクセスされます。詳しくは、デプロイメントに応じて、 AEM Forms製品の説明 ([オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html) または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
- PDF Generator サービスでは Microsoft Windows 10 をサポートしていません。
- PDFジェネレータは、Microsoft Visio 2019 を使用してファイルを変換できません。 Microsoft Visio 2016 を引き続き使用して、 .VSD および.VSDX ファイルを変換できます。
- PDFジェネレーターが、Microsoft Project 2019 を使用してファイルを変換できません。 引き続き、 Microsoft Project 2016 を使用して.MPP ファイルを変換できます。
>


### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}

AEM Forms の次のサブシステムは、[リハビリテーション法 508 条](https://www.section508.gov/)に準拠していません。

- アダプティブフォームオーサリング UI
- Forms Manager オーサリング UI
- Correspondence Management オーサリング UI
- 管理 UI（管理コンソール UI）

## AEM Forms on JEE の必要システム構成 {#system-requirements-for-aem-forms-on-jee}

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

- [JEE デプロイメント上でのシングルサーバー AEM Forms の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_jp)
- [クラスター化された AEM Forms on JEE の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_jp)

## JEE 上の AEM Forms でサポートされているクライアント {#supported-clients-for-aem-forms-on-jee}

### ワークベンチ {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10（Enterprise、Pro、Basic）</p> <p>32 または 64 ビット版</p> <p> </p> </td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
 </tbody>
</table>

- インストールのためのディスク空き容量： 1.7 GB（Workbench のみ）、2.7 GB（Workbench、 Designer 、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB （一時的インストールディレクトリ）、200 MB （ユーザー一時ディレクトリ）、および200 MB（Windows 一時ディレクトリ）。これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

- Workbench を実行するためのメモリ：2 GB の RAM
- ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー
- 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
- JEE サーバーの AEM Forms に対する TCP/IPv4 または TCP/IPv6 ネットワーク接続
- Workbench を Windows にインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server または Microsoft® Windows® 10
- 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
- 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
- 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
- グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
- 2.35 GB のハードディスク空き容量
- 1024 x 768 ピクセル以上のモニター解像度
- ビデオハードウェアアクセラレーション（オプション）
- Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。
- Designer をインストールするための管理者権限。

### Adobe Acrobat と Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat および Adobe Reader（Base）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020（クラシックトラック）</td>
   <td>バージョン 20.004.30006 以降<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017（クラシックトラック）（非推奨）</td>
   <td>バージョン 17.011.30078 以降<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
Acrobat DC Product Family では、基本的に異なる製品であるAcrobatとReaderの両方に 2 つのトラックを導入しています。「クラシック」と「連続」 2 つのトラックについての詳細や比較については、[https://www.adobe.com/go/acrobatdctracks_jp](https://www.adobe.com/go/acrobatdctracks_jp) を参照してください。

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
   <td>Mozilla Firefox ESR</td>
   <td>E：動作する見込み</td>
   <td> すべてのアップデート</td>
  </tr>
  <tr>
   <td><p>Google Chrome（Evergreen）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Apple Safari(macOS)</td>
   <td>A：サポート対象</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
以下にデスクトップに対する一部のブラウザー関連の例外事項を示します。
- Safari は Macintosh OS X でのみサポートされています。
- Acrobat DC 以降のバージョンでは、Workspace は Macintosh OS X 10.6 および 10.7 上の Safari 5.1 をサポートしています。Safari 5.1 の Adobe Reader、Acrobat との互換性については、[https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html) を参照してください。
- 管理コンソールは Safari ではサポートされていません。
- Correspondence Management は、AEM 6.1 Forms で Windows® Internet Explorer 9.0 をサポートしていません。
- Forms ポータルは、アクセシビリティのために、JAWS 14.0 画面読み上げソフトウェアを Internet Explorer 11 でサポートしています。


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
   <td>Safari（iOS 15.1 以降）</td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>すべてのアップデート<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 以降のネイティブ Android ブラウザー</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
- Forms Portal は iPad の Safari でのみサポートされています。


### AEM Forms アプリケーション {#aem-forms-workspace-app}

#### モバイルデバイスのサポート {#mobile-device-support}

AEM Forms アプリケーションは次のプラットフォームで利用可能です。

| **プラットフォーム** | **サポートされているデバイス** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple の iPhone、iPad、iPad Air、iPad mini [iOS 15.1 以降] |
| Google Android | Android 5.1 以降。AEM Forms アプリケーションは、7 インチと 10 インチの Samsung Galaxy タブレット、および主要なスマートフォンで動作確認されています。 |
| Microsoft Windows | Microsoft の Windows 10 オペレーティングシステムを実行している Microsoft Surface のデバイス、タブレット、ノートパソコン、およびデスクトップ PC |

### Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office の必要システム構成を確認するには、[ここ](https://www.adobe.com/jp/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。

### クライアントサポートの例外事項 {#exceptions-to-client-support}

JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。

## サードパーティパッチサポートポリシー {#third-party-patch-support-policy}

JEE 上のAEM Formsのサードパーティのソフトウェア要件は、それぞれの製品ドキュメントの「必要システム構成」セクションに記載されています。 すべてのドキュメントは、[https://adobe.com/go/learn_aemforms_documentation_65_jp](https://adobe.com/go/learn_aemforms_documentation_65_jp) からアクセスすることができます。

JEE 上のAEM Formsのサードパーティの参照プラットフォームには、JEE 上のAEM Formsの開発とリリースの際に最新であったサードパーティインフラストラクチャの特定のパッチレベルと、そのバージョンの JEE 上のAEM Formsでサポートされるインフラストラクチャの最小パッチ/サービスパックレベルが示されます。

アドビシステムズ社では、サードパーティベンダーがリリース時に JEE 上の AEM Forms がサポートするバージョンとの後方互換性を保証していると仮定して、サードパーティベンダーの緊急および推奨パッチをサポートします。アドビシステムズ社は、JEE 上の AEM Forms ドキュメントに記載の最小パッチレベル後にリリースされたパッチのみをサポートします。

場合によっては、アドビは、主要な機能が変更され、そのために完全な後方互換性がサポートされなくなったサードパーティ製のアップデートはサポートしません。サポートされているアップデートの詳細については、[サポートされているパッチ定義](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html)で特定のベンダー製品とアドビがサポートするパッチタイプを参照してください。

Adobeの管理の及ばない状況下では、後方互換性を主張するサードパーティ製パッチは、Adobe製品やお客様の環境に悪影響を及ぼす場合があります。 このような場合、アドビシステムズ社は、お客様がサードパーティからの緊急パッチを重要なシステムに適用する前にその影響を評価することを推奨します。アドビシステムズ社はサードパーティと共に妥当なビジネス努力を払って、通常のアドビサポートプログラムを通してあるいはサードパーティがパッチの問題を修正することによって、そのような問題を解決します。このことは、アドビによってサポートされる新たにリリースされたサードパーティ製パッチが、ベンダーによってマニュアルに記載されているようにまたは JEE 上の AEM Forms と機能することを保証するものではありません。

アドビシステムズ社は、任意の時点で、JEE 上の AEM Forms リリースおよびそれらのサポートされているパッチ定義によってサポートされているサードパーティリファレンスプラットフォームを変更する権利を保留します。

サードパーティ製パッチのその他の情報については、Adobe Enterprise Support サイトで、ご使用の製品に関するナレッジベース記事を検索することによっても見つけられることがあります。

## プラットフォームのアップデート {#platform-updates}

2022 年 6 月 2 日のAEM Forms 6.5.13.0リリースでは、次のプラットフォームは非推奨（廃止予定）となります。

- Microsoft SharePoint 2016

2022年3月3日の AEM Forms 6.5.12.0 リリースでは、以下のプラットフォームは非推奨（廃止予定）となります。

- MongoDB Enterprise 4.0
- IBM DB2 11.1
- Oracle Database 12c リリース 2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC ドライバー 6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM Content Manager サーバー 8.5 Fix pack 2
- IBM Content Manager クライアント 8.5
- Microsoft SQL Server 2016

2021年9月7日の AEM Forms 6.5.10.0 リリースでは、以下のプラットフォームは非推奨（廃止予定）となります。

- Adobe Acrobat 2017 - [Adobe Acrobat 2017 のコアサポートは 2022年6月6日に終了します](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)。
- Microsoft Windows Server 2016（64 ビット版）
- Red Hat Enterprise Linux 7（Kernel 3.x）（64 ビット版）
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
プラットフォームは [AEM Forms 6.5.12.0 および 6.5.10.0 で非推奨となり、AEM Forms 6.5 サービスパック 18（6.5.18.0）リリースまでは引き続きサポートされます](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)。

## 変更履歴 {#revision-history}

- 2022 年 9 月 1 日

   - oracleJava™ SE 11 （64 ビット） SDK のサポートを、アプリケーションサーバー JBoss EAP 7.4 に追加しました。

- 2022 年 3 月 03 日（PT）

   - 次のサポートを削除しました。
      - IBM® J9 Virtual Machine（ビルド 2.8、JRE 1.8.0）
      - Oracle Database 12c リリース 1
      - Oracle Database 18c
      - Oracle Unified Directory（OUD）11g リリース 2
      - IBM Lotus Domino 9.0
      - IBM FileNet 5.2
      - Adobe Flash Player

- 2021年10月10日

   - AEM Forms アプリケーションの iOS のサポート対象バージョンを iOS 15.1 に変更しました。以前のバージョンは iOS 12 でした。

- 2021年9月7日
   - **プラットフォームのアップデート**：JEE 上の [!DNL Adobe Experience Manager Forms] は、以下のプラットフォームをサポートするようになりました。
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft Office 2019]
      - [!DNL Microsoft Windows Server 2019]
      - [!DNL RHEL8]

- 2020 年 12 月 3 日
   - 次のプラットフォームのAEM Forms 6.5.7.0 以降でのサポートが追加されました。
      - [!DNL Microsoft SQL Server 2019]

- 2020年9月9日

   - AEM Forms アプリケーションの iOS のサポート対象バージョンを iOS 12 に変更しました。以前のバージョンは iOS 11 でした。

