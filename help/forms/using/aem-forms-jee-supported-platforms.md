---
title: JEE 上のAEM Formsでサポートされるプラットフォーム
description: JEE 上のAEM Formsのインストールに必要な、およびサポートされるインフラストラクチャコンポーネントのリスト
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3693'
ht-degree: 43%

---


# JEE 上のAEM Formsでサポートされるプラットフォーム {#supported-platforms-for-aem-forms-on-jee}

## サポートされているプラットフォーム {#supported-platforms}

<div class="preview">

アドビでは、JEE 版 AEM 6.5 Forms サービスパック 18（6.5.18.0）を含んだ[完全なインストーラー](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)のほか、パッチインストーラーをリリースしました。完全なインストーラーは新しいプラットフォームに対するサポートを提供するのに対して、パッチインストーラーはバグ修正のみを含んでいます。JEE 上のAEM 6.5 Forms環境で最新のソフトウェアを使用する場合は、新規インストールを実行するか、最新のソフトウェアを使用することを計画している場合、Adobeでは、 [AEM 6.5.18.0 Forms on JEE フルインストーラー](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) 2019 年 4 月 8 日にリリースされたAEM 6.5 Formsインストーラーや、2022 年 3 月 3 日にリリースされたAEM 6.5.12 Formsインストーラーに代わって、2023 年 8 月 31 日にリリースされました。

</div>

### サポートレベル {#support-levels}

JEE 上のAEM Formsサーバーは、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、電子メールサーバーの任意の組み合わせを使用して設定できます。

このドキュメントでは、JEE 上のAEM Formsでサポートされているクライアントおよびサーバープラットフォームを示します。 Adobeは、Adobe推奨設定とその他の設定の両方に対して、複数のレベルのサポートを提供します。 このドキュメントでは、その他のサポート対象ソフトウェアとそのバージョン、例外事項、パッチ定義、およびサードパーティのソフトウェアパッチサポートポリシーも示します。

>[!NOTE]
>
>- サポートされているサーバープラットフォームに対する例外の完全なリストについては、 [サポート対象のサーバープラットフォームに対する例外](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- JEE 上のAEM Formsは、サポートされているオペレーティングシステムとアプリケーションの英語、フランス語、ドイツ語、日本語バージョンのみをサポートしています。

### 推奨設定 {#recommendedconfigurations}

Adobeは、これらの設定を推奨し、標準のソフトウェア保守契約の一環として、次の完全なサポートまたは制限付きサポートを提供します。

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
   <td>Adobeは、特定の前提条件を満たした後で、この設定を完全にサポートします。 Adobeのエンタープライズサポートに問い合わせて、前提条件を確認し、サポートのリクエストを送信します。</td>
  </tr>
  <tr>
   <td>L：制限付きサポート</td>
   <td>Adobeは、特定の前提条件が満たされた後、この設定に対する完全なサポートとメンテナンスを提供します。 すべての機能が設定で使用できるわけではありません。 Adobeのエンタープライズサポートに問い合わせて、前提条件を確認し、サポートのリクエストを送信します。<br /> </td>
  </tr>
 </tbody>
</table>

### サポートされていない設定 {#unsupported-configurations}

| サポートレベル | 説明 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E：動作する見込み | この構成は動作する見込みであり、動作しないという報告はありません。 |
| Z：サポート対象外 | この構成はサポートされません。Adobe では、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

>[!NOTE]
>
>AEM Formsのお客様が所有コストを削減し、デプロイメントアーキテクチャをシンプル化し、開発スタックを最新化できるよう、Adobe Experience Manager Enterprise Platform は、アプリケーションサーバーベースのデプロイメントから離れ、スタンドアロンの OSGi ベースのデプロイメントに置き換わりました。 Adobeは、インフラストラクチャコンポーネントのマトリックスを削減し、AEM Forms JEE スタックを引き続きサポートします。
>
>6.5 のリリースでは、Adobeのお客様の間で最も使用率の低いインフラストラクチャコンポーネントは、次のようにサポートされなくなりました。
>
>- IBM® DB2®データベース
- IBM® AIX®および Sun Solaris™オペレーティングシステム
>
新規インストールの場合、最新の OSGi スタックにAEM Formsをデプロイして、モバイル、マルチチャネルのインタラクティブ通信、およびフォームデータモデルを使用したバックエンドデータ統合にレスポンシブFormsの最新のイノベーションを使用することをお勧めします。
>
Adobeは、既存のユーザーが JEE 上のAEM Formsスタックのデプロイを続行する必要があることを認識します。 このような場合、Adobeでは、このドキュメントで説明するように、サポート対象のインフラストラクチャにAEM Forms JEE をデプロイする必要があります。 AEM 6.5 Formsにアップグレードし、以前のAEM Formsリリースでサポートされていないプラットフォームを使用している場合、サポートされているプラットフォームへのアップグレードに関するヘルプについては、Adobeサポートにお問い合わせください。

### Java™仮想マシン (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Formsでは、Java™ Virtual Machine を実行する必要があります。Java™ Development Kit(JDK) ディストリビューションによって提供されます。 Adobe Experience Manager は、次のバージョンの Java™ 仮想マシンで動作します。

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11（64 ビット）<sup> [8] </sup> </p>  </td>
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
   <td>OracleJava™ SE 8（64 ビット）</td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine（ビルド 2.9、JRE 1.8.0）IBM® JDK SR6-FP26<br /> </td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291（ビルド 8.0.6.30）<br /> </td>
   <td>A：サポート対象</td>
   <td>マイナーリリースとアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Java™ベンダーのセキュリティ速報を追跡して、実稼動環境の安全性とセキュリティを確保し、最新の Java™アップデートをインストールします。
- JEE 上のAEM Formsは、実稼動環境での 64 ビット JVM のみをサポートしています。

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
   <td><p>リポジトリ Microkernel（TAR MK ファイル）</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.4 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c（Standard、Real Application Clusters（RAC）および Enterprise エディション） </td>
   <td>Microkernal リポジトリ </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1（非推奨）</td>
   <td>リポジトリ Microkernel</td>
   <td>R：限定サポート</td>
  </tr>
  <tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R：限定サポート</td>
  </tr>
 </tbody>
</table>

- IBM® DB2®は、新規インストールではサポートされていません。 AEM 6.5 Formsにアップグレードする既存のお客様のみがサポートされます。
- MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、 [MongoDB ライセンスポリシー](https://www.mongodb.org/about/licensing/).
- AEMのデプロイメントを最大限に活用するには、Adobeで、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。
- アドビカスタマーケアは、MongoDB を AEM で利用することに関連する問題の絞り込みを支援いたします。詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
- 「ファイルシステム」には、POSIX に準拠したブロックストレージが含まれます。これには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスは異なり、全体的なパフォーマンスに影響を与える場合があることに注意してください。network/remote ファイルシステムでテスト用AEMを読み込むことをお勧めします。
- MongoDB Storage Engine WiredTiger のみがサポートされています。
- MongoDB Sharding は AEM ではサポートしていません。
- JEE 上のAEM Formsは、RDBMK 永続性用の MySQL をサポートしていません。
- Document Security モジュールは、コンテンツリポジトリを使用しません。 つまり、Document Security のみを使用していて、HTMLWorkspace、HTML5 フォーム、アダプティブフォームを使用する予定がない場合は、コンテンツリポジトリをインストールしないでください。
- JEE 上のAEM Formsは、AEMリポジトリ (CRX-Repository) を永続化するための MySQL の使用をサポートしていません。

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
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(version 5.1.44)</p> </td>
   <td><p>JEE 上のAEM Formsのインストールに付属</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Microsoft® Web サイトからダウンロードします。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC ドライバー</p> <p>ojdbc8.jar（バージョン 19.3.0.0.0）<br /> </p> </td>
   <td><p>ダウンロード元 <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">OracleWeb サイト</a>.</p> </td>
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
   <td>Oracle WebLogic Server 12.2.1（12c R2）（非推奨）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td>OracleWebLogic Server 14c </td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サポートされる EAP バージョンのパッチと累積パッチ</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
IBM® WebSphere®クラスターは、Network Deployment エディションでのみサポートされます。

### サーバのオペレーティングシステム {#server-operating-systems}

#### 実稼動環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> プラットフォーム</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019（64 ビット）（非推奨）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022（64 ビット）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8(Kernel 4.x)（64 ビット）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、および重要なアップデート</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7(Kernel 3.x)（64 ビット）（非推奨）</td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、および重要なアップデート</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12（64 ビット版）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパック、累積パッチ、および重要なセキュリティ更新</p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7 Update 3（64 ビット）</td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および重要なセキュリティ更新</td>
  </tr>
  <tr>
   <td>CentOS 7（64 ビット版）<sup>[6]</sup></td>
   <td>A：サポート対象</td>
   <td>サービスパック、累積パッチ、および重要なセキュリティ更新</td>
  </tr>
 </tbody>
</table>

#### 仮想化環境 {#virtualized-environment}

JEE 上のAEM Formsは、物理マシンまたは仮想環境で実行できます。 ただし、仮想環境でAEM Formsに問題が発生した場合は、物理マシンでその問題を複製してみてください。 物理マシン上でも問題が発生する場合は、アドビサポートにお問い合わせいただき、解決を試みてください。物理マシン上で再現することができない問題に関しては、バーチャル環境のベンダーにお問い合わせください。

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
   <td><p>サービスパックと重要な更新</p> </td>
  </tr>
 </tbody>
</table>

### サポート対象のサーバープラットフォームに対する例外 {#exceptions-to-supported-server-platforms}

JEE サーバー上のAEM Formsを設定するプラットフォームを選択する際は、次の例外を考慮してください。

1. JEE 上のAEM Formsは、IBM® WebSphere®を MySQL でサポートしていません。
1. JEE 上のAEM Formsは、SUSE® Linux® Enterprise Server 12 上の JBoss®をサポートしていません。 SUSE® Linux® Enterprise Server 12 では、IBM® WebSphere®のみがサポートされています。
1. JEE 上のAEM Formsは、JBoss®ではOracleJava™ SE 以外の JDK をサポートしていません。
1. JEE 上のAEM Formsは、IBM® WebSphere®ではIBM® JDK 以外の JDK をサポートしていません。
1. CRX リポジトリは、TarMK、MongoDB、およびリレーショナルデータベース（RDBMK）の永続性をサポートします。アプリケーションサーバーと CRX リポジトリ間に 2 つの異なるデータベースシステムを持つことはできません。ただし、AEM Forms on JEE 環境では、CRX リポジトリで MongoMK を使用でき、アプリケーションサーバーでサポートしているリレーショナルデータベースを使用できます。
1. JEE 上のAEM Formsは、CentOS 上の WebSphere®アプリケーションサーバーをサポートしていません。
1. JEE 上のAEM Formsは、JBoss®の役割に基づくアクセス制御 (RBAC) をサポートしていません。
1. JEE 上のAEM Formsは、OracleJava™ SE 11（64 ビット）SDK( アプリケーションサーバー JBoss® EAP 7.4 のみ ) をサポートします。

また、JEE 上のAEM FormsのデプロイメントでAdobeソフトウェアを選択する際は、次の点を考慮してください。

- AEM Forms on JEE は、指定されたメジャーバージョンおよびマイナーバージョンのサポート対象ソフトウェアに、アップデート、パッチ、および修正パックをサポートします。 ただし、次のメジャーバージョンまたはマイナーバージョンへの更新は、特に指定のない限りサポートされません。
- クラスターベースのインストールでは TarMK 永続性をサポートしていません。 サポートされる永続性について詳しくは、 [AEM Formsインストールの永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- JEE 上のAEM Formsは、Adobeの [サードパーティのソフトウェアサポートポリシー](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- JEE 上のAEM Formsは、サードパーティベンダーが提供するサポートに従って、プラットフォームをサポートします。 一部の組み合わせは、サードパーティベンダーで許可されていない可能性があります。 例えば、多くのベンダーは、自社のアプリケーションサーバーをOracleで認定していません。 その結果、JEE 上のAEM Formsでもこれらの組み合わせをサポートしていません。 サポートしているソフトウェアバージョンを確実に選択するようにするために、サードパーティベンダーのサポート表もチェックしてください。
- JEE 上のAEM Formsは TarMK コールドスタンバイをサポートしていません。
- JEE 上のAEM Formsは垂直クラスタリングをサポートしていません。
- JEE 上のAEM Formsは、クラスター環境での MySQL データベースをサポートしていません。
- 削除または更新されたプラットフォームの一覧は、[AEM 6.5 Forms 新機能の概要](../../forms/using/whats-new.md)のドキュメントを参照してください。

### LDAP サーバー（オプション） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品（基本バージョン）</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2016 （非推奨）</td>
   <td>メンテナンスリリースおよび修正パック</td>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2022</td>
   <td>メンテナンスリリースおよび修正パック</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>機能パックと中間修正</p> </td>
  </tr>
 </tbody>
</table>

### 電子メールサーバー（オプション） {#email-servers-optional}

| 製品 |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### コンテンツマネージャーと対応するコネクタ {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>製品<br /> </strong></td>
   <td><strong>バージョン</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server（非推奨） </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> IBM® Content Manager Client（廃止）</td>
   <td>8.5 </td>
  </tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova のサポート {#support-for-cordova}

AEM Forms アプリケーションで Apache Cordova がサポートされるようになりました。サポートされている Cordova プラットフォームのバージョンは以下のとおりです。

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### PDF Generator のソフトウェアサポート {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品</strong></p> </th>
   <th><p><strong>PDF への変換でサポートされる形式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 Classic トラック</a> 最新バージョン</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP、WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、日本語版のみをサポートしています。
>
さらに、次の点に注意してください。：
>
- PDF Generatorには 32 ビット版のが必要です [Acrobat 2020 classic track バージョン 20.004.30006](https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html) をクリックして変換を実行します。
- PDF Generatorは、32 ビット版のMicrosoft® Office Professional Plus と、変換に必要なその他のソフトウェアの小売バージョンのみをサポートしています。
- PDF Generator は Microsoft® Office 365 をサポートしていません。
- PDF Generator の OpenOffice 向け変換機能は、Windows と Linux® でのみサポートされています。
- OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
- Acrobat のバージョンは、PDF Generator 機能を有効にするために AEM Forms にバンドルされています。バンドルされたバージョンには、AEM Forms PDF Generator で使用するために、AEM Forms のライセンス期間中に AEM Forms でのみプログラムでアクセスする必要があります。詳しくは、デプロイメントに応じたAEM Forms製品の説明 ([オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html) または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
- PDF Generator サービスでは Microsoft® Windows 10 をサポートしていません。-PDF Generatorは、Microsoft® Visio 2019 を使用してファイルを変換できません。 Microsoft® Visio 2016 を引き続き使用して、.VSD ファイルと.VSDX ファイルを変換できます。
- PDF Generatorは、Microsoft® Project 2019 を使用してファイルを変換できません。引き続き、 Microsoft® Project 2016 を使用して.MPP ファイルを変換できます。
- PDF Generator は、Microsoft® Visio 2019 を使用してファイルを変換できません。
- PDF Generatorは、Microsoft® Project 2019 を使用してファイルを変換できません。
>

### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}

次のAEM Formsのサブシステムは [508](https://www.section508.gov/) 準拠：

- アダプティブFormsオーサリング UI
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
   <td>Microsoft® Windows Server</td>
   <td>インテル Xeon® E5-2680、2.4 GHz プロセッサーまたは同等の<br /> VMWare ESX 5.1 以降<br /> RAM:6 GB（64 ビット OS、64 ビット JVM）<br /> 空きディスク容量： 15 GB の一時領域と 22 GB の容量<br /> (JEE 上のAEM Forms)</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>インテル Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium (3 ECU)<br /> RAM:6 GB（64 ビット OS、64 ビット JVM）<br /> 空きディスク容量：6 GB の一時領域と 22 GB の容量<br /> (JEE 上のAEM Forms)</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>インテル Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium (3 ECU)<br /> RAM:6 GB（64 ビット OS、64 ビット JVM）<br /> 空きディスク容量：6 GB の一時領域と 22 GB の容量<br /> (JEE 上のAEM Forms)<br /> </td>
  </tr>
  <tr>
   <td>小規模な実稼動環境向けのハードウェア要件</td>
   <td>
    <ul>
     <li><strong>インテル®搭載環境</strong>:Intel Xeon® E5-2680、2.4 GHz 以上。 デュアルコアプロセッサを使用すると、パフォーマンスがさらに向上します。</li>
     <li><strong>メモリ：</strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

上記以外の要件については、以下を参照してください。

- [JEE デプロイメント上でのシングルサーバー AEM Forms の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_jp)
- [クラスター化された AEM Forms on JEE の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_jp)

## JEE 上のAEM Formsでサポートされているクライアント {#supported-clients-for-aem-forms-on-jee}

### ワークベンチ {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10（Enterprise、Pro、Basic）</p> <p>32 または 64 ビット版</p> <p> </p> </td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2019 Server （非推奨）</td>
   <td>サービスパックと重要な更新</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2022 Server</td>
   <td>サービスパックと重要な更新</td>
  </tr>
 </tbody>
</table>

- インストールのためのディスク空き容量： 1.7 GB（Workbench のみ）、2.7 GB（Workbench、 Designer 、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB （一時的インストールディレクトリ）、200 MB （ユーザー一時ディレクトリ）、および200 MB（Windows 一時ディレクトリ）。これらの場所がすべて 1 台のドライブ上に存在する場合は、インストール時に 1.5 GB の空き容量が必要です。 一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

- Workbench を実行するためのメモリ：2 GB の RAM
- ハードウェア要件： Intel® Pentium® 4 または AMD®同等の 1 GHz プロセッサ
- 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
- JEE 上のAEM Formsサーバーへの TCP/IPv4 または TCP/IPv6 ネットワーク接続
- Windows に Workbench をインストールするには、管理者権限が必要です。 管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server または Microsoft® Windows® 10
- 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
- 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
- 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
- グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
- 2.35 GB のハードディスク空き容量
- 1024 x 768 ピクセル以上のモニター解像度
- ビデオハードウェアアクセラレーション（オプション）
- Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC
- Designer をインストールするための管理者権限。
- Microsoft® Visual C++ 2019 （VC 14.28 以降） 32 ビットランタイム

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

</tbody>
</table>

>[!NOTE]
>
Acrobat DC製品ファミリでは、AcrobatとReaderの両方で、「クラシック」と「継続的」の 2 つのトラックを紹介しています。 2 つのトラックの詳細と比較については、 [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

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
   <td><p>Microsoft® Edge（エバーグリーン）</p> </td>
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
   <td>macOS の Apple Safari</td>
   <td>A：サポート対象</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
デスクトップに関する一部のブラウザー関連の例外は次のとおりです。
>
- Safari は Macintosh OS X でのみサポートされています。
- Acrobat DC 以降のバージョンでは、Workspace は Macintosh OS X 10.6 および 10.7 上の Safari 5.1 をサポートしています。Safari 5.1 の Adobe Reader、Acrobat との互換性については、[https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html) を参照してください。
- 管理コンソールは Safari ではサポートされていません。
- Correspondence Management は、AEM 6.1 Forms で Windows® Internet Explorer 9.0 をサポートしていません。
- Forms Portal は、アクセシビリティのために、JAWS 14.0 スクリーンリーダーソフトウェアを Internet Explorer 11 でサポートしています。

#### モバイルクライアント {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>ブラウザー（ベース）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome(Android™ 4.1.2 以降 )</p> </td>
   <td><p>すべてのアップデート</p> </td>
  </tr>
  <tr>
   <td>Safari（iOS 15.1 以降）</td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>すべてのアップデート<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 以降のネイティブ Android™ブラウザー</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Forms Portal は iPad の Safari でのみサポートされています。

### AEM Forms アプリケーション {#aem-forms-workspace-app}

#### モバイルデバイスのサポート {#mobile-device-support}

AEM Formsアプリは、次のプラットフォームで使用できます。

| **プラットフォーム** | **サポートされるデバイス** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple の iPhone、iPad、iPad Air、iPad mini [iOS 15.1 以降] |
| Google Android™ | Android™ 5.1 以降。 AEM Formsアプリは、7 インチと 10 インチの Samsung Galaxy タブレットと人気のスマートフォンで認定されています。 |
| Microsoft® Windows | Microsoft® Microsoft® Windows 10 オペレーティングシステムを実行するサーフェスデバイス、タブレット、ノートパソコンおよびデスクトップ。 |

### Microsoft® Office 用AdobeDocument Security Extension {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office の必要システム構成を確認するには、[ここ](https://www.adobe.com/jp/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。

### クライアントサポートの例外 {#exceptions-to-client-support}

AEM Forms on JEE は、指定されたメジャーバージョンおよびマイナーバージョンのサポート対象ソフトウェアに、アップデート、パッチ、および修正パックをサポートします。 ただし、次のメジャーバージョンまたはマイナーバージョンへの更新は、特に指定のない限りサポートされません。

## サードパーティ製パッチのサポートポリシー {#third-party-patch-support-policy}

JEE 版 AEM Forms のサードパーティソフトウェア要件は、それぞれの製品ドキュメントの「必要システム構成」の節に記載されています。すべてのドキュメントにアクセスするには、 [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65_jp) .

AEM Forms on JEE のサードパーティ参照プラットフォームは、AEM Forms on JEE の開発とリリースの時点において最新だったサードパーティ製インフラストラクチャの特定のパッチレベルを、そのバージョンの AEM Forms on JEE でサポートしているインフラストラクチャの最小のパッチまたはサービスパックのレベルから記述しています。

Adobeは、サードパーティベンダーが JEE 上のAEM Formsでサポートされるバージョンとの後方互換性を保証していると想定し、サードパーティベンダーのリリース時に発行される緊急または推奨パッチをサポートします。 Adobeは、JEE 上のAEM Formsドキュメントに記載されている最小パッチレベルの後にリリースされたパッチのみをサポートします。

Adobeでは、主な機能を変更するサードパーティの更新がサポートされず、その結果、完全な後方互換性がサポートされない場合があります。 サポートされているアップデートの詳細については、[サポートされているパッチ定義](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html)で特定のベンダー製品とアドビがサポートするパッチタイプを参照してください。

アドビの管理の及ばない状況においては、後方互換性を主張しているサードパーティ製パッチによって、アドビ製品またはお客様の環境に悪い影響を及ぼす可能性があります。このような場合、Adobeでは、お客様は、緊急パッチを重要なシステムに適用する前に、サードパーティからの緊急パッチの影響を評価することをお勧めします。 Adobeは、通常のAdobeサポートプログラムを通じて、またはパッチの問題を修正した第三者によって、妥当なビジネス努力を払って、サードパーティと連携して問題を解決します。 これは、Adobeでサポートされる新たにリリースされたサードパーティ製パッチが、ベンダーによってドキュメントに記載されているように、または JEE 上のAEM Formsと共に動作することを保証するものではありません。

Adobeは、任意の時点で、JEE 上のAEM Formsリリースでサポートされているサードパーティの参照プラットフォームと、そのサポートされているパッチ定義を変更する権利を留保します。

サードパーティ製パッチの追加情報は、Adobeのエンタープライズサポートサイトで、製品に関するナレッジベース記事を検索することでも確認できます。

## プラットフォームのアップデート {#platform-updates}

2023 年 8 月 31 日のAEM Forms 6.5.18.0リリースでは、次のプラットフォームは非推奨（廃止予定）となります。

- Microsoft® Windows Server 2019（64 ビット）
- Microsoft® Active Directory 2016

2022年6月2日（PT）の AEM Forms 6.5.13.0 リリースで、以下のプラットフォームは非推奨（廃止予定）になっています。
- Microsoft® SharePoint 2016

2022年3月3日の AEM Forms 6.5.12.0 リリースでは、以下のプラットフォームは非推奨（廃止予定）となります。

- MongoDB Enterprise 4.0
- MongoDB Enterprise 4.2
- IBM® DB2® 11.1
- Oracle Database 12c リリース 2
- MySQL 5.7.35
- Microsoft® SQL Server JDBC ドライバー 6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM® Content Manager Server 8.5 Fix pack 2
- IBM® Content Manager Client 8.5
- Microsoft® SQL Server 2016

2021年9月7日の AEM Forms 6.5.10.0 リリースでは、以下のプラットフォームは非推奨（廃止予定）となります。

- Adobe Acrobat 2017 - [Adobe Acrobat 2017 のコアサポートは 2022年6月6日に終了します](https://helpx.adobe.com/jp/support/programs/eol-matrix.html)。
- Red Hat® Enterprise Linux® 7(Kernel 3.x)（64 ビット）
- Microsoft® Office 2016
- OpenOffice 4.1.2


>[!NOTE]
>
廃止されたプラットフォームは、プラットフォームが削除済みとマークされるか、プラットフォームのサードパーティベンダーサポートが提供終了（いずれか最初）に達するまで、引き続きサポートを受けます。

## 変更履歴 {#revision-history}

- 6.5.18.0（2023 年 8 月 31 日）
   - **プラットフォームのアップデート**：JEE 上の [!DNL Adobe Experience Manager Forms] は、以下のプラットフォームをサポートするようになりました。
      - MongoDB Enterprise 4.4
      - OracleWebLogic Server 14c
      - My SQL JDBC コネクタ 8
      - Active Directory 2022
      - Microsoft® Windows Server 2022（64 ビット）

   - **プラットフォームの更新**: [!DNL Adobe Experience Manager Forms] JEE 上では、次のプラットフォームのサポートを削除しました。
      - Windows Server 2016（64 ビット）
      - MongoDB Enterprise 4.0
      - Oracle Database 12c リリース 2（12.2.0.1.0）
      - MySQL 5.7.35
      - Microsoft® SQL Server 2016
      - JBoss® EAP 7.1.4
      - My SQL JDBC connector 5.1.44
      - Microsoft® SQL Server JDBC ドライバー 6.2.1.0
      - Microsoft® SQL Server JDBC ドライバー 6.2.2.0
      - Microsoft® JDBC Driver 8.x for SQL Server

   - **プラットフォームサービスのPDF Generator更新**: [!DNL Adobe Experience Manager Forms] JEE 上では、以下のプラットフォームに対するPDF Generatorおよび一般的なサポートを削除しました。
      - Microsoft® Sharepoint 2016
      - Microsoft® Office 2016
      - Microsoft® Office Visio 2016
      - Microsoft® Publisher 2016
      - Microsoft® Project 2016
      - OpenOffice 4.1.2
      - Acrobat 2017（クラシックトラック）バージョン 17.011.30078以降

- 6.5.10.0（2022 年 9 月 1 日）

   - アプリケーションOracleJBoss® EAP 7.4 用の Java™ SE 11 （64 ビット） SDK のサポートを追加しました。

- 2022 年 3 月 03 日（PT）

   - 次のサポートを削除しました。
      - IBM® J9 Virtual Machine（ビルド 2.8、JRE 1.8.0）
      - Oracle Database 12c リリース 1
      - Oracle Database 18c
      - Oracle Unified Directory（OUD）11g リリース 2
      - IBM® Lotus Domino 9.0
      - IBM® FileNet 5.2
      - Adobe Flash Player

- 2021年10月10日

   - AEM Forms アプリケーションの iOS のサポート対象バージョンを iOS 15.1 に変更しました。以前のバージョンは iOS 12 でした。

- 2021年9月7日
   - **プラットフォームのアップデート**：JEE 上の [!DNL Adobe Experience Manager Forms] は、以下のプラットフォームをサポートするようになりました。
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft®® Office 2016]
      - [!DNL Microsoft®® Windows Server 2016]
      - [!DNL RHEL8]

- 2020年12月3日（PT）
   - AEM Forms 6.5.7.0 以降で次のプラットフォームのサポートが追加されました。
      - [!DNL Microsoft®® SQL Server 2019]

- 2020年9月9日

   - AEM Forms アプリケーションの iOS のサポート対象バージョンを iOS 12 に変更しました。以前のバージョンは iOS 11 でした。
