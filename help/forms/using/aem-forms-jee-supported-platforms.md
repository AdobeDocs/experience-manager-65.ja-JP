---
title: JEE 上の AEM Forms でサポートされているプラットフォーム
description: JEE 上の AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: 71a6a9739800c2e2bd9f8b97e3ec2b0245d6e1cd
workflow-type: tm+mt
source-wordcount: '3819'
ht-degree: 96%

---



# JEE 上の AEM Forms でサポートされているプラットフォーム {#supported-platforms-for-aem-forms-on-jee}


## サポートされているプラットフォーム {#supported-platforms}


<div class="preview">


アドビでは、JEE 版 AEM 6.5.23.0 Forms サービスパック 23（6.5.23.0）を含んだ[完全なインストーラー](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)のほか、パッチインストーラーをリリースしました。完全なインストーラーは新しいプラットフォームをサポートするのに対して、パッチインストーラーはバグ修正のみを含んでいます。

新規インストールを実行する場合や、JEE 環境での AEM 6.5.23.0 Forms の最新ソフトウェアを使用することを計画している場合は、AEM 6.5 18 Forms インストーラー（2023年8月31日（PT）にリリース）または AEM 6.5.12 Forms インストーラー（2019年4月8日（PT）にリリース）ではなく、[ JEE 上の AEM 6.5.23.0 Forms の完全なインストーラー](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)（2025年6月6日（PT）にリリース）を使用することをお勧めします。


</div>


### サポートレベル {#support-levels}


JEE サーバー上の AEM Forms は、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、およびメールサーバーを自由に組み合わせて設定できます。


このドキュメントでは、JEE 上の AEM Forms でサポートされているクライアントおよびサーバーのプラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。このドキュメントでは、その他のサポートされているソフトウェアとバージョン、例外事項、パッチ定義、およびサードパーティソフトウェアパッチサポートポリシーも示します。


>[!NOTE]
>
>- サポートされているサーバープラットフォームへの例外エラーの完全リストについては、[サポートされているサーバープラットフォームへの例外エラー](#exceptions-to-supported-server-platforms)を参照してください。
>- JEE 上の AEM Forms でサポートされるのは、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみです。

### アップグレードおよびサポートポリシー

#### 完全なインストーラー

- **完全なインストーラーのアップグレードサポート**：完全なインストーラーは、6 回の AEM サービスパックリリースごとにリリースされます。例えば、6.5.12.0 および 6.5.18.0 SP リリースでは完全なインストーラーがリリースされました。AEM Forms では、最新の 2 つの完全なインストーラーからのみ直接アップグレードできます。例えば、AEM Forms では、最新の 2 つの完全なインストーラー（6.5.18.0 と 6.5.12.0）からのみバージョン 6.5.23.0 への直接アップグレードを簡単に行うことができます。以前のアップグレードからアップグレードする必要がある場合は、マルチホップアップグレードを使用して、最初にサポートされている完全なインストーラーリリースに移行した後、最新のリリースに移行できます。

- **廃止**：プラットフォームのサポートは、完全なインストーラーリリースごとに更新されます。プラットフォームマトリックスで廃止とマークされたソフトウェアは、後続のリリースやソフトウェアのサポートが終了した時点で、サポート対象のプラットフォームから削除される場合があります。

#### サービスパック


- **サービスパックの対象範囲**：アドビでは、最新の 6 つのサービスパックのいずれかを使用して、AEM Forms 環境のテクニカルサポートを提供します。現在のバージョンが最新の 6 つのサービスパックよりも古い場合、最適なパフォーマンス、セキュリティ、継続的なサポートを実現するために、アドビでは最新バージョンにアップグレードすることを強くお勧めします。

- **パッチインストーラーのガイドライン**：パッチインストーラーを使用して更新する場合、基になる完全なインストーラーバージョンが 2 リリース以内のものであることを確認することが重要です。例えば、サービスパック 6.5.23.0 のインストール中に、基になる完全なインストーラーのバージョンが 6.5.18.0 または 6.5.12.0 であることを確認します。

<!--
- **Patch Upgrade Support**: You can upgrade from an older service pack to a newer one (for example, from 6.5.18.0 to 6.5.23.0) using the patch installer, as long as the destination platform (OS, JDK, application server, etc.) is supported by the newer service pack.-->

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
>><br>
>>6.5 のリリースでは、アドビのお客様の中で最も使用率の低い、以下のインフラストラクチャコンポーネントはサポートされなくなりました。
>
> - IBM® DB2® データベース
> - IBM® AIX® および Sun Solaris™ オペレーティングシステム
>
>
>新規インストールに関しては、可能な場合は AEM Forms を最新の OSGi スタックでデプロイし、モバイル向けのレスポンシブなアダプティブフォーム、マルチチャンネルのインタラクティブ通信、そしてフォームデータモデルを使用したバックエンドのデータ統合などの最新技術を活用することが推奨されます。
>
>既存のお客様は、AEM Forms を引き続き JEE スタック上でデプロイしていただく必要があります。そのような場合は、AEM Forms JEE を本文書に記載されている対応インフラストラクチャでデプロイしていただく必要があります。前回の AEM Forms リリースをサポート対象ではないプラットフォームでご使用で、AEM 6.5 Forms にアップグレードされる場合は、アドビサポートにご連絡ください。サポート対象のプラットフォームへのアップグレードをお手伝いします。

### Java™ 仮想マシン（JVM） {#java-virtual-machines-jvm}


Adobe Experience Manager Forms を使用するには、Java™ 仮想マシンが必要です。Java 仮想マシンは、Java™ Development Kit（JDK）ディストリビューションに付属しています。Adobe Experience Manager は、次のバージョンの Java™ 仮想マシンで動作します。


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
  <td>Azul Zulu OpenJDK 11（64 ビット）</td>
  <td>Z：サポート対象外</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Azul Zulu OpenJDK 8（64 ビット）</td>
  <td>Z：サポート対象外</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Oracle Java™ SE 8（64 ビット）</td>
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
>- Java™ ベンダーが発表するセキュリティ情報を常に確認し、実稼働環境の安全性とセキュリティを確保すること、および最新の Java™ アップデートをインストールすることをお勧めします。
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
  <td><p> MongoDB Enterprise 6.0（廃止） </p> </td>
  <td><p>リポジトリ Microkernel</p> </td>
  <td><p>サポート対象</p> </td>
 </tr>
 <tr>
  <td><p> MongoDB Enterprise 7.0 </p> </td>
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
  <td></td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2019（廃止予定） </p> </td>
  <td><p>リポジトリ Microkernel</p> </td>
  <td><p>サポート対象</p> </td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2022 </p> </td>
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
  <td>MySQL 8.0.27（非推奨） </td>
  <td>-</td>
  <td>R：限定サポート</td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.4</td>
  <td>-</td>
  <td>R：限定サポート</td>
 </tr>
</tbody>
</table>


- IBM® DB2® は、新規インストールではサポートされていません。AEM 6.5 Forms にアップグレードする既存のお客様の場合のみサポートされます。
- MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB ライセンスポリシー](https://www.mongodb.org/about/licensing/)を参照してください。
- AEMAdobeのデプロイメントを最大限に活用するには、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。
@@ -242,187 +206,150 @@ Adobe Experience Manager Formsを実行するには、Java™ 仮想マシンが必要です、wh
- Document Security モジュールは、コンテンツリポジトリを使用しません。つまり、Document Security のみを使用していて、HTML Workspace、HTML5 フォーム、アダプティブフォームを使用する予定がない場合は、コンテンツリポジトリをインストールしないでください。
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
  <td><p>MySQL Connector/J 5.7（非推奨）</p> </td>
  <td><p>JEE のインストールで AEM Forms に付属</p> </td>
 </tr>
 <tr>
  <td>MySQL</td>
  <td><p>MySQL Connector/J 8.4</p> </td>
  <td><p>JEE のインストールで AEM Forms に付属</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Microsoft® SQL Server JDBC ドライバー 8.2.2<br /> </p> <p>sqljdbc8.jar（廃止） </p> </td>
  <td><p>Microsoft® の web サイトからダウンロードします。</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Microsoft® SQL Server JDBC ドライバー 12.10.0<br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
  <td><p>Microsoft® の web サイトからダウンロードします。</p> </td>
 </tr>
 <tr>
  <td>Oracle</td>
  <td><p>Oracle Database 19.3.0.0.0 JDBC ドライバー</p> <p>ojdbc8.jar（バージョン 19.3.0.0.0）<br /> </p> </td>
  <td><p><a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle web サイト</a>からダウンロードします。</p> </td>
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
  <td>Oracle WebLogic Server 12.2.1（12c R2）（非推奨）<sup>[9]</sup></td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td>Oracle WebLogic Server 14c <sup>[9]</sup></td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
  <td><p>A：サポート対象</p> </td>
  <td><p>対応の EAP バージョンのパッチと累積パッチ</p> </td>
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
  <td>Microsoft® Windows Server 2019（64 ビット版）（非推奨）</td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
    <tr>
  <td>Microsoft® Windows Server 2022（64 ビット版）</td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td>Ubuntu 20.04</td>
  <td>A：サポート対象</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 8（Kernel 4.x）（64 ビット版）（廃止）</p> </td>
  <td><p>A：サポート対象</p> </td>
  <td><p>マイナーリリース、累積アップデート、需要なアップデート</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 7（Kernel 3.x）（64 ビット版）（非推奨）</td>
  <td><p>A：サポート対象</p> </td>
  <td><p>マイナーリリース、累積アップデート、需要なアップデート</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 9（Kernel 4.x）（64 ビット版）</p> </td>
  <td><p>A：サポート対象</p> </td>
  <td><p>マイナーリリース、累積アップデート、需要なアップデート</p> </td>
 </tr>
 <tr>
  <td><p>SUSE® Linux® Enterprise Server 15 SP6（64 ビット版） </p> </td>
  <td><p>A：サポート対象</p> </td>
  <td><p>サービスパック、累積パッチ、重要なセキュリティアップデート</p> </td>
 </tr>
 <tr>
  <td>OracleLinux® 7 Update 3（64 ビット）</td>
  <td>A：サポート対象</td>
  <td>サービスパック、累積パッチ、重要なセキュリティアップデート</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
> Linux® ベースのサーバーの場合、必要なランタイム依存関係は次のとおりです。
>
> - glibc.x86_64（2.17-196）
> - libX11.x86_64（1.6.7-4）
> - zlib.x86-64（1.2.7-17）
> - libxcb.x86_64（1.13-1.el7）
> - libXau.x86_64（1.0.8-2.1.el7）
> - glibc-locale.x86_64（2.17 以降）
> - OpenSSL 3（OS のデフォルトの場所で必要）。

OpenSSL 3 のインストールの場合：ライブラリ libcrypto.so.3 および libssl.so.3 は、環境変数 LD_LIBRARY_PATH によって表されるデフォルトのライブラリパスで使用できる必要があります。それらが非標準の場所にインストールされている場合は、サーバーを起動する前に、このパスが LD_LIBRARY_PATH に追加されていることを確認してください。

#### 仮想化環境 {#virtualized-environment}


AEM Forms on JEE は、物理マシンまたは仮想環境で実行できます。ただし、仮想環境での AEM Forms の使用に問題が発生した場合は、物理マシン上で問題を再現してみてください。物理マシン上でも問題が発生する場合は、アドビサポートにお問い合わせいただき、解決を試みてください。物理マシン上で再現することができない問題に関しては、バーチャル環境のベンダーにお問い合わせください。


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

### 対応のサーバープラットフォームの例外事項 {#exceptions-to-supported-server-platforms}


AEM Forms on JEE サーバーの設定でプラットフォームを選択するときは、次の例外事項を考慮してください。


1. AEM Forms on JEE では、MySQL を搭載した IBM® WebSphere® をサポートしていません。
1. AEM Forms on JEE では、SUSE® Linux® Enterprise Server 12 上での JBoss をサポートしていません。SUSE® Linux® Enterprise Server 12 上では、IBM® WebSphere® のみがサポートされています。
1. AEM Forms on JEE では、Oracle Java™ SE 以外の JBoss® を使用する JDK をサポートしていません。
1. AEM Forms on JEE では、IBM® JDK 以外の IBM® WebSphere® を使用する JDK をサポートしていません。
1. CRX リポジトリは、TarMK、MongoDB、およびリレーショナルデータベース（RDBMK）の永続性をサポートします。アプリケーションサーバーと CRX リポジトリ間に 2 つの異なるデータベースシステムを持つことはできません。ただし、JEE 上のAEM Forms環境では、CRX リポジトリで MongoMK を使用でき、アプリケーションサーバーでサポートしているリレーショナルデータベースを使用できます。
@@ -432,12 +359,12 @@AEM F を設定するプラットフォームを選ぶ際には、次の例外を考慮してください
1. 1.8.0_281 より後の JDK バージョンは、WebLogic サーバーではサポートされていません。（FORMS-8498）
1. JDK 11.0.20 では、AEM Forms on JEE インストーラーのインストールをサポートしていません。AEM Forms on JEE インストーラーのインストールは、JDK 11.0.19 以前のバージョンのみがサポートしています。

1. [!DNL Microsoft® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss® EAP 7.1] をサポートしていないので、[!DNL Microsoft® Windows Server 2019] は [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later] の自動インストールをサポートしていません。（CQDOC-18312）


この他に、AEM Forms on JEE の導入のためにソフトウェアを選択する際には、次の項目を考慮してください。


- AEM Forms on JEE では、対応ソフトウェアの指定されたメジャーおよびマイナーバージョンに加えて、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーバージョンまたはマイナーバージョンに対するアップデートは、特に記載がない限りサポートされていません。
- クラスターベースのインストールは、TarMK 永続性をサポートしていません。サポートされている永続性については、[AEM Forms のインストールでの永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。
- AEM Forms on JEE は、Adobeの [ サードパーティソフトウェアサポートポリシー ](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p) に従って、様々なサードパーティソフトウェアをサポートします。
@@ -449,274 +376,219 @@さらに、Adobe AEMのソフトウェアを選択する際は、次の点を考慮してください

### LDAP サーバー（オプション） {#ldap-servers-optional}


<table>
<tbody>
 <tr>
  <th><p><strong>製品（基本バージョン）</strong></p> </th>
  <th><p><strong>サポートしているパッチ定義</strong></p> </th>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2016（非推奨）</td>
  <td>メンテナンスリリースと修正パック</td>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2022</td>
  <td>メンテナンスリリースと修正パック</td>
 </tr>
 <tr>
  <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
  <td><p>フィーチャーパックと暫定フィックス</p> </td>
 </tr>
</tbody>
</table>


### メールサーバー（オプション） {#email-servers-optional}


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
  <td>IBM® Content Manager サーバー（非推奨） </td>
  <td>8.5 Fix pack 2</td>
 </tr>
  <tr>
  <td> IBM® Content Manager クライアント（非推奨）</td>
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

### PDF Generator に関する考慮事項

<table>
<tbody>
 <tr>
  <th><p><strong>製品</strong></p> </th>
  <th><p><strong>PDF への変換でサポートされる形式</strong></p> </th>
 </tr>
 <tr>
   <td><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> 最新バージョン</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM</td>
  </tr>
 <tr>
  <td>Microsoft® Office 2021  </td>
  <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
 </tr>
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
  <td>Microsoft® Publisher 2021<br /> </td>
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
>PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、日本語版のみをサポートしています。
>
>さらに、次の点に注意してください。
>
>- PDF Generator で変換を実行するには、Adobe Acrobat Pro DC（32 ビット）が必要です。
>- PDF Generator では、32 ビット版の Microsoft® Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>- Microsoft® Office Professional Plus のインストールでは、リテールまたは MAK／KMS／AD ベースのボリュームライセンスを使用する場合があります。
>- ボリュームライセンスインストールで指定期間内に KMS ホストが見つからないなど、何らかの理由で Microsoft® Office インストールが非アクティブ化またはライセンス解除された場合、インストールのライセンスを再度取得して再アクティブ化するまでは、変換が失敗する場合があります。
>- PDF Generator は Microsoft® Office 365 をサポートしていません。
>- PDF Generator は、Linux® オペレーティングシステム上の 32 ビット版の OpenOffice をサポートしています。
>- PDF Generator の OpenOffice 向け変換機能は、Windows と Linux® でのみサポートされています。
>- OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
>- Acrobat のバージョンは、PDF Generator 機能を有効にするために AEM Forms にバンドルされています。バンドルされたバージョンには、AEM Forms PDF Generator で使用するために、AEM Forms のライセンス期間中に AEM Forms でのみプログラムでアクセスする必要があります。詳しくは、デプロイメント（[オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html)または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html)）に応じた AEM Forms 製品説明を参照してください。
>- PDF Generator サービスでは Microsoft® Windows 10 をサポートしていません。
>- PDF Generator は、Microsoft® Visio 2019 を使用してファイルを変換できません。
>- PDF Generator は、Microsoft® Project 2019 を使用してファイルを変換できません。

PDF Generator では、32 ビット版の Microsoft® Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。


Microsoft® Office Professional Plus のインストールでは、リテールまたは MAK／KMS／AD ベースのボリュームライセンスを使用する場合があります。


ボリュームライセンスインストールで指定期間内に KMS ホストが見つからないなど、何らかの理由で Microsoft® Office インストールが非アクティブ化またはライセンス解除された場合、インストールのライセンスを再度取得して再アクティブ化するまでは、変換が失敗する場合があります。

<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->


### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}


AEM Forms の以下のサブシステムは、[リハビリテーション法 508 条](https://www.section508.gov/)に準拠していません。


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
  <td>Microsoft® Windows Server</td>
  <td>インテル Xeon® E5-2680、2.4 GHz プロセッサーまたは同等の <br />VMWare ESX 5.1 以降<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：15 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）</td>
 </tr>
 <tr>
  <td>SUSE® Linux® Enterprise Server</td>
  <td>インテル Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー <br />AWS m3.medium（3 つの ECU）<br />RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：6 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）</td>
 </tr>
 <tr>
  <td>Red Hat® Enterprise Linux®</td>
  <td>Intel Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー <br />AWS m3.medium（3 つの ECU）<br />RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：6 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）<br /> </td>
 </tr>
 <tr>
  <td>小規模な実稼動環境向けのハードウェア要件</td>
  <td>
   <ul>
    <li><strong>Intel® 搭載環境</strong>：Intel Xeon® E5-2680、2.4 GHz 以上。デュアルコアプロセッサーを使用するとパフォーマンスがさらに向上します。</li>
    <li><strong>メモリ：</strong>4 GB <br /> </li>
   </ul> </td>
 </tr>
</tbody>
</table>


上記以外の要件については、以下を参照してください。

- [JEE デプロイメント上でのシングルサーバー AEM Forms の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_jp)
- [クラスター化された AEM Forms on JEE の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_jp)


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
>Acrobat DC 製品ファミリーでは、異なる製品である Acrobat と Reader のそれぞれに、「Classic」と「Continuous」の 2 種類のトラックが用意されています。2 つのトラックについての詳細や比較については、[https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html) を参照してください。

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
  <td>Microsoft® Windows® 2019 Server（非推奨）</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
 <tr>
  <td>Microsoft® Windows® 2022 Server</td>
  <td>サービスパックと重要なアップデート</td>
 </tr>
</tbody>
</table>


- インストールのためのディスク空き容量： 1.7 GB（Workbench のみ）、2.7 GB（Workbench、 Designer 、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB （一時的インストールディレクトリ）、200 MB （ユーザー一時ディレクトリ）、および200 MB（Windows 一時ディレクトリ）。これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。


- Workbench を実行するためのメモリ：2 GB の RAM
- ハードウェア要件： Intel® Pentium® 4 または AMD® の同等の 1 GHz プロセッサー
- 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
- JEE サーバー上の AEM Forms に対する TCP/IPv4 または TCP/IPv6 ネットワーク接続
- Workbench を Windows にインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。


### Designer {#designer}


- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10 または Windows® 11
- 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
- 1 GB の RAM （32 ビット OS の場合）または 2 GB の RAM （64 ビット OS の場合）
@@ -729,49 +601,45 @@その他の要件については、以下を参照してください。
- Designer をインストールするための管理者権限。
- Microsoft® Visual C++ 2019（VC 14.28 以降）32 ビットランタイム


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
>以下にデスクトップに対する一部のブラウザー関連の例外事項を示します。
>
>- Correspondence Management は、AEM 6.1 Forms で Windows® Internet Explorer 9.0 をサポートしていません。
>- フォームポータルは、アクセシビリティのために、JAWS 14.0 画面読み上げソフトウェアを Internet Explorer 11 でサポートしています。

#### モバイルクライアント {#mobile-clients}


<table>
<tbody>
 <tr>
  <th><p><strong>ブラウザー（ベース）</strong></p> </th>
  <th><p><strong>サポートされているパッチ定義</strong></p> </th>
 </tr>
 <tr>
  <td><p>Chrome（Android™ 4.1.2 以降）</p> </td>
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
  <td>Android™ 4.4 以降のネイティブ Android ブラウザー</td>
  <td>すべてのアップデート</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- Forms Portal は iPad の Safari でのみサポートされています。

### AEM Forms アプリケーション {#aem-forms-workspace-app}


#### モバイルデバイスのサポート {#mobile-device-support}


AEM Forms アプリケーションは次のプラットフォームで利用可能です。


| **プラットフォーム** | **サポートされているデバイス** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple の iPhone、iPad、iPad Air、iPad mini [iOS 15.1 以降] |
| Google Android™ | Android™ 5.1 以降。AEM Forms アプリケーションは、7 インチと 10 インチの Samsung Galaxy タブレット、および主要なスマートフォンで動作確認されています。 |
| Microsoft® Windows | Microsoft の Windows 10 オペレーティングシステムを実行している Microsoft® Surface のデバイス、タブレット、ノートパソコン、およびデスクトップ PC |


### Adobe Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}


Adobe Document Security Extension for Microsoft® Office の必要システム構成を確認するには、[ここ](https://www.adobe.com/jp/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。


### クライアントサポートの例外事項 {#exceptions-to-client-support}


AEM Forms on JEE では、対応ソフトウェアの指定されたメジャーおよびマイナーバージョンに加えて、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーバージョンまたはマイナーバージョンに対するアップデートは、特に記載がない限りサポートされていません。


## サードパーティパッチサポートポリシー {#third-party-patch-support-policy}


JEE 版 AEM Forms のサードパーティソフトウェア要件は、それぞれの製品ドキュメントの「必要システム構成」の節に記載されています。すべてのドキュメントは、[https://adobe.com/go/learn_aemforms_documentation_65_jp](https://adobe.com/go/learn_aemforms_documentation_65_jp) からアクセスすることができます。


JEE 上の AEM Forms のサードパーティ参照プラットフォームは、JEE 上の AEM Forms の開発とリリースの時点において最新だったサードパーティ製インフラストラクチャの特定のパッチレベルを、そのバージョンの JEE 上の AEM Forms でサポートしているインフラストラクチャの最小のパッチまたはサービスパックのレベルから記載しています。


アドビでは、サードパーティベンダーがリリース時に JEE 上の AEM Forms がサポートするバージョンとの後方互換性を保証していると仮定して、サードパーティベンダーの緊急および推奨パッチをサポートします。JEE 上の AEM Forms ドキュメントに記載の最小パッチレベル後にリリースされたパッチのみが、アドビのサポート対象です。


場合によっては、主要な機能を変更しそのために完全な後方互換性をサポートしなくなったサードパーティアップデートはサポートされません。サポートされているアップデートの詳細については、[サポートされているパッチ定義](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html)で特定のベンダー製品とアドビがサポートするパッチタイプを参照してください。


アドビの管理の及ばない状況においては、後方互換性を主張しているサードパーティ製パッチによって、アドビ製品またはお客様の環境に悪い影響を及ぼす可能性があります。このような場合、お客様がサードパーティからの緊急パッチを重要なシステムに適用する前に、その影響を評価することが推奨されます。アドビはサードパーティと共に妥当なビジネス努力を払って、通常のアドビサポートプログラムを通してあるいはサードパーティがパッチの問題を修正することによって、そのような問題を解決します。このことは、アドビによってサポートされる新たにリリースされたサードパーティパッチが、ベンダーによってマニュアルに記載されているように、または JEE 上の AEM Forms と機能することを保証するものではありません。


アドビは、任意の時点で、JEE 上の AEM Forms リリースおよびそれらのサポートされているパッチ定義によってサポートされているサードパーティリファレンスプラットフォームを変更する権利を留保します。


サードパーティパッチの追加情報は、アドビのエンタープライズサポートサイトで、ご使用の製品に関するナレッジベース記事を検索することでも確認できます。


<!--

## Platform updates {#platform-updates}
The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:
- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016
The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016
The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:
- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit)
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2
-->




## 変更履歴 {#revision-history}


<!--
- 6.5.18.0 (Aug 31, 2023)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - MongoDB Enterprise 4.4
   - Oracle WebLogic Server 14c
   - My SQL JDBC connector 8
   - Active Directory 2022
   - Microsoft&reg; Windows Server 2022 (64-bit)
 - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
   - Windows Server 2016 (64-bit)
   - MongoDB Enterprise 4.0
   - Oracle Database 12c Release 2 (12.2.0.1.0)
   - MySQL 5.7.35
   - Microsoft&reg; SQL Server 2016
   - JBoss&reg; EAP 7.1.4
   - My SQL JDBC connector 5.1.44
   - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
   - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
   - Microsoft&reg; JDBC Driver 8.x for SQL Server
   The release has also removed support for the following platforms for PDF Generator and in-general:
   - Microsoft&reg; Sharepoint 2016
   - Microsoft&reg; Office 2016
   - Microsoft&reg; Office Visio 2016
   - Microsoft&reg; Publisher 2016
   - Microsoft&reg; Project 2016
   - OpenOffice 4.1.2
   - Acrobat 2017 (Classic track) Version 17.011.30078 or later
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Microsoft&reg; Windows Server 2019 (64-bit)
   - Microsoft&reg; Active Directory 2016
  
- 6.5.13.0 (June 2, 2022)
 The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 - Microsoft&reg; SharePoint 2016
- 6.5.12.0 (March 3, 2022)
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
     - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
     - Oracle Database 12c Release 1
     - Oracle Database 18c
     - Oracle Unified Directory (OUD) 11g Release 2
     - IBM&reg; Lotus Domino 9.0
     - IBM&reg; FileNet 5.2
     - Adobe Flash Player
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
     - MongoDB Enterprise 4.0
     - MongoDB Enterprise 4.2
     - IBM&reg; DB2&reg; 11.1
     - Oracle Database 12c Release 2
     - MySQL 5.7.35
     - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
     - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
     - IBM&reg; Content Manager Server 8.5 Fix pack 2
     - IBM&reg; Content Manager Client 8.5
     - Microsoft&reg; SQL Server 2016
- 6.5.10.0 (Sep 01, 2022)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
   - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
   - Microsoft&reg; Windows Server 2016 (64-bit)
   - Microsoft&reg; Office 2016
   - OpenOffice 4.1.2
### Release 6.5.23.0 (June 06, 2025)
| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 |    MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 |SUSE&reg; Linux&reg; Enterprise Server 12 (64-bit) | MYSQL 8.0.27 |
| Microsoft&reg; SQL Server 2022 | |Microsoft&reg; SQL Server 2019 |
| Microsoft&reg; SQL Server JDBC driver 12.8 | | Microsoft&reg; SQL Server JDBC driver 8.2 |
| Microsoft&reg; Office 2021 | | Microsoft&reg; Office 2019 |
| Red Hat&reg; Enterprise Linux&reg; 9 (Kernel 4.x) (64-bit) | |Red Hat&reg; Enterprise Linux&reg; 8 (Kernel 4.x) (64-bit)  |
-->

### リリース 6.5.23.0（2025年6月6日（PT））

| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 | MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MySQL 8.4 | SUSE® Linux® Enterprise Server 12（64 ビット版） | MySQL 8.0.27 |
| Microsoft® SQL Server 2022 | CentOS 7 | Microsoft® SQL Server 2019 |
| Microsoft® SQL Server JDBC ドライバー 12.10.0 | | Microsoft® SQL Server JDBC ドライバー 8.2 |
| Red Hat® Enterprise Linux® 9（Kernel 4.x）（64 ビット版） | | Red Hat® Enterprise Linux® 8（Kernel 4.x）（64 ビット版） |

### リリース 6.5.22.0（2024年11月29日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| SUSE® Linux® Enterprise Server 15 SP6（64 ビット版） | |  |

### リリース 6.5.21.0（2024年6月13日（PT））

| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| Microsoft® Office 2021 |  |  |

### リリース 6.5.19.1（2023年12月15日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 | MongoDB Enterprise 4.4 |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |


### リリース 6.5.18.0（2023年8月31日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016（64 ビット版） | Microsoft® Windows Server 2019（64 ビット版） |
|  | Acrobat 2017（クラシックトラック）バージョン 17.011.30078 以降 |  |

### リリース 6.5.13.0（2022年6月2日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |

### リリース 6.5.12.0（2022年3月3日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
|  | IBM® J9 Virtual Machine（ビルド 2.8、JRE 1.8.0） | MongoDB Enterprise 4.0 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### リリース 6.5.10.0（2022年9月1日（PT））


| 追加したサポート | 削除したサポート | 非推奨のサポート |
| -------------- | --------------- | ------------------- |
| アプリケーションサーバー JBoss® EAP 7.4 用の Oracle Java™ SE 11（64 ビット版）SDK | | [Adobe Acrobat 2017 - Adobe Acrobat 2017 のコアサポートは 2022年6月6日（PT）に終了します。](https://helpx.adobe.com/jp/support/programs/eol-matrix.html) |
|  | | OpenOffice 4.1.2 |

>[!NOTE]
>
> 非推奨のプラットフォームは、次回の完全なインストーラーリリースまで、またはサードパーティベンダーによるプラットフォームのサポートが終了するまでのどちらか早い方までサポートされます。

<!--
- Oct 10, 2021
 - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.
- Sep 07, 2021
 - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - [!DNL Adobe Acrobat 2020]
   - [!DNL Ubuntu 20.04]
   - [!DNL Open Office 4.1.10]
   - [!DNL Microsoft&reg;&reg; Office 2016]
   - [!DNL Microsoft&reg;&reg; Windows Server 2016]
   - [!DNL RHEL8]
- Dec 03, 2020
 - Support added with AEM Forms 6.5.7.0 or later for the following platform:
   - [!DNL Microsoft&reg;&reg; SQL Server 2019]
- Sep 09, 2020
   - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.
   -->