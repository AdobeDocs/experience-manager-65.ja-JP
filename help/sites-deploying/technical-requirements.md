---
title: 技術要件
seo-title: 技術要件
description: AEM でサポートされているクライアントおよびサーバーのプラットフォームのリスト。
seo-description: AEM でサポートされているクライアントおよびサーバーのプラットフォームのリスト。
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# 技術要件{#technical-requirements}

アドビは、このドキュメントの以下の情報に記載されているプラットフォームで Adobe Experience Manager（AEM）をサポートしています。

プラットフォームに関連する問題については、プラットフォームのベンダーにお問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームによっては、別のユーザー管理要件が適用される場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件：

* Installed Java Platform, Standard Edition JDK, or other supported [Java Virtual Machines](#java-virtual-machines)
* Experience Manager Quickstart ファイル（スタンドアロン JAR または Web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

Adobe Experience Managerの実行に必要な最小要件：

* 5 GB の空きディスク領域（インストールディレクトリ内）
* 2 GB メモリ

>[!NOTE]
>
>* デジタルアセットを使用する場合は、より多くの基本メモリが必要になります。詳しくは、[デプロイおよびメンテナンス](/help/sites-deploying/deploy.md#default-local-install)を参照してください。
>* [AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)には 15 GB の一時領域が必要です。
>



詳しくは、[ハードウェアのサイジングのガイドライン](/help/managing/hardware-sizing-guidelines.md)を参照してください。

### サポートレベル {#support-levels}

ここでは、Adobe Experience Manager でサポートされているクライアントおよびサーバープラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。

### サポートされる構成 {#supported-configurations}

アドビは以下の構成を推奨し、標準ソフトウェア保守契約の一環として完全なサポートを提供しています。

<table>
 <tbody>
  <tr>
   <td>サポートレベル</td>
   <td>説明<br /> </td>
  </tr>
  <tr>
   <td><strong>A：サポート対象</strong></td>
   <td>アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。</td>
  </tr>
  <tr>
   <td><strong>R：制限サポート</strong></td>
   <td>顧客のプロジェクト成功のために、アドビは、制限されたサポートプログラムの範囲内で完全なサポートを提供します。このサポートプログラムでは、特定の条件を満たす必要があります。R レベルのサポートでは、顧客からの正式な依頼とアドビによる承認が必要です。詳しくは、アドビカスタマーケアにお問い合わせください。</td>
  </tr>
 </tbody>
</table>

### サポートされていない構成 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| **Z：サポート対象外** | この構成はサポートされません。アドビは、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java Virtual Machines {#java-virtual-machines}

このアプリケーションの実行には、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションによって提供されます。

Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

>[!CAUTION]
>
>Java ベンダーが発表するセキュリティ情報を常に確認し、実稼動環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。

<table>
 <tbody>
  <tr>
   <td>プラットフォーム</td>
   <td>サポートレベル<br /> </td>
  </tr>
  <tr>
   <td>Oracle Java SE 12 JDK `\[1]`</td>
   <td>Z：サポート対象外 </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64 ビット</strong></td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK `\[1]`</td>
   <td>Z：サポート対象外 </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK `\[1]`</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64 ビット</td>
   <td>A: Supported `\[3]`<br /> </td>
  </tr>
  <tr>
   <td>IBM J9 VM — ビルド2.9、JRE 1.8.0 `\[2]`</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>IBM J9 VM — ビルド2.8、JRE 1.8.0 `\[2]`</td>
   <td>A：サポート対象</td>
  </tr>
 </tbody>
</table>

1. Oracle は Oracle Java SE 製品の「長期サポート」（LTS）モデルに移行しました。Java 9, Java 10, and Java 12 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). 実稼動環境に AEM をデプロイするために、アドビでは LTS リリース版の Java のみサポートします。

1. IBM JRE は、WebSphere Application Server と共に使用する場合にのみサポートされます。
1. パブリックアップデート終了後の LTS リリースのすべてのメンテナンスアップデートを含む Oracle Java SE JDK のサポートと配布が、アドビによって直接サポートされます。対象となるのは、Oracle Java SE テクノロジーを利用しているすべての AEM ユーザーです。See the [Oracle Java support for Adobe Experience Manager Q&amp;A](assets/adobe-oracle-java-license-agreement.pdf) for more information.

### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリのデプロイには、様々なオプションがあります。サポートされるテクノロジーとストレージオプションについては、以下のリストを参照してください。

| **プラットフォーム** | **説明** | **サポートレベル** |
|---|---|---|
| **TAR ファイルを使用したファイルシステム`\[1]`** | リポジトリ | A：サポート対象 |
| **データストアを持つファイルシステム`\[1]`** | バイナリ | A：サポート対象 |
| ファイルシステムの TAR ファイルへのバイナリの格納 `\[1]` | バイナリ | Z：実稼動環境ではサポート対象外 |
| Amazon S3 | バイナリ | A：サポート対象 |
| Microsoft Azure Blob Storage | バイナリ | A：サポート対象 |
| MongoDB Enterprise 4.0 | リポジトリ | A: Supported [2, 3] |
| MongoDB Enterprise 3.6 | リポジトリ | Z：サポート対象外 |
| MongoDB Enterprise 3.4 | リポジトリ | Z：サポート対象外 |
| IBM DB2 10.5 | リポジトリおよび Forms データベース | R：制限サポート `\[4]` |
| Oracle Database 12c (12.1.x) | リポジトリおよび Forms データベース | R：制限サポート |
| Microsoft SQL Server 2016 | Forms データベース | A：サポート対象 |
| **Apache Lucene（クイックスタート組み込み）** | 検索サービス | A：サポート対象 |
| Apache Solr | 検索サービス | A：サポート対象 |

1. 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
1. MongoDB Sharding は AEM ではサポートされていません。
1. MongoDB Storage Engine WiredTiger のみサポートされています。
1. AEM Forms アップグレード版のお客様にサポートされています。新規インストールの場合はサポートされていません。

>[!NOTE]
>
>AEM コミュニティの機能について詳しくは、[コミュニティのデプロイ](/help/communities/deploy-communities.md)を参照してください。

>[!NOTE]
>
>MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。
>
>MongoDB を利用した AEM デプロイメントを最大限活用するために、アドビでは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。See [Recommended Deployments](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) for more information.
>
>このライセンスには、標準レプリカセットが含まれます。このレプリカセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成されており、これらのインスタンスは、オーサーとパブリッシュのいずれのデプロイメントにも使用できます。
>
>MongoDB でオーサーとパブリッシュの両方を実行したい場合は、2 つのライセンスを個別に購入する必要があります。
>
>アドビカスタマーケアは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。
>
>詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。

>[!NOTE]
>
>上記のサポート対象リレーショナルデータベースはサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。
>
>サポートされているリレーショナルデータベースを使用して AEM 6.5 を実行するには、データベースベンダーと別途サポート契約を締結する必要があります。アドビカスタマーケアは、リレーショナルデータベースを AEM 6.5 で利用することに関連する問題の絞り込みを支援いたします。
>
>**AEM 6.5 では現在、ほとんどのリレーショナルデータベースがレベル R の範囲でサポートされ、前述のレベル R の説明にあるサポートの基準とサポートプログラムが適用されます。**

### サーブレットエンジン／アプリケーションサーバー {#servlet-engines-application-servers}

Adobe Experience Manager はスタンドアロンサーバー（quickstart JAR ファイル）として実行することも、サード-パーティのアプリケーションサーバー内の Web アプリケーション（WAR ファイル）として実行することもできます。

サーブレット API の最低限必要なバージョンはサーブレット 3.1 です。

| プラットフォーム | サポートレベル |
|---|---|
| **Quickstart 組み込みサーブレットエンジン（Jetty 9.4）** | A：サポート対象 |
| Oracle WebLogic Server 12.2（12cR2） | Z：サポート対象外 |
| IBM WebSphere Application Server Continuous Delivery（LibertyProfile）（Web Profile 7.0 および IBM JRE 1.8） | R：新規契約向けの制限サポート `\[2]` |
| IBM WebSphere Application Server 9.0 および IBM JRE 1.8 | R：新規契約向けの制限サポート `\[1]` `\[2]` |
| Apache Tomcat 8.5.x | R：新規契約向けの制限サポート `\[2]` |
| JBoss EAP 7.2.x と JBoss Application Server | Z：サポート対象外 |
| JBoss EAP 7.1.4 と JBoss Application Server | R：新規契約向けの制限サポート `\[1]` `\[2]` |
| JBoss EAP 7.0.x と JBoss Application Server | Z：サポート対象外 |

1. AEM Forms を備えたデプロイメントに推奨されています。
1. アプリケーションサーバーでの AEM 6.5 デプロイメントの起動は制限サポートに移行します。既存のお客様は AEM 6.5 にアップグレードして、アプリケーションサーバーを引き続き使用することができます。新規のお客様には、前述のレベル R の説明にあるサポート基準とサポートプログラムが適用されます。

### サーバーオペレーティングシステム {#server-operating-systems}

実稼働環境の Adobe Experience Manager は次のサーバープラットフォームで動作します。

| **プラットフォーム** | **サポートレベル** |
|---|---|
| **Linux、Red Hat ディストリビューションベース** | A：サポート対象 `\[1]` `\[3]` |
| Linux、Debian ディストリビューションベース（Ubuntu を含む） | A：サポート対象 `\[2]` |
| Linux、SUSE ディストリビューションベース | A：サポート対象 |
| Microsoft Windows Server 2019 `\[4]` | R：新規契約向けの制限サポート |
| Microsoft Windows Server 2016 `\[4]` | R：新規契約向けの制限サポート `\[5]` |
| Microsoft Windows Server 2012 R2 | Z：サポート対象外 |
| Oracle Solaris 11 | Z：サポート対象外 |
| IBM AIX 7.2 | Z：サポート対象外 |

1. Linux Kernel 2.6, 3.x, 4.xには、Red Hat Enterprise Linux、CentOS、Oracle Linux、Amazon Linuxを含む、Red Hatディストリビューションの派生物が含まれています。 AEM Forms のアドオン機能は、CentOS 7 および Red Hat Enterprise Linux 7 でのみサポートされています。
1. AEM Forms は Ubuntu 16.04 LTS でのみサポートされています。
1. Adobe Managed Services でサポートされている Linux ディストリビューション
1. Microsoft Windows 版の実稼働デプロイメントは、お客様が 6.5 にアップグレードする場合と、実稼動以外の用途に使用する場合にサポートされています。AEM Sites および AEM Assets の新規デプロイメントは、お客様の依頼に応じて提供されます。
1. AEM Forms は、サポートレベル R の制限なしに Microsoft Window Server でサポートされています。

### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Microsoft Azure や Amazon Web Services（AWS）など、クラウドコンピューティング環境の仮想マシンでの Adobe Experience Manager の稼動は、このページに記載されている技術要件およびアドビの標準サポート条件に従ってサポートされています。

AEM を Azure または AWS にデプロイする場合は、Adobe Managed Services を使用することをお勧めします。Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。[Adobe Managed Services に関するドキュメント](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)も参照してください。

AEM を Azure や AWS にデプロイするその他あらゆる場合、またはその他のクラウドコンピューティング環境にデプロイする場合、アドビによるサポートは、このページに記載されている技術仕様に従って、仮想コンピューティング環境に対して提供されます。これらのクラウド環境で実行される AEM に関連する問題を報告する場合は、その問題が、クラウドコンピューティング環境に固有のクラウドサービスと関係なく再現可能である必要があります。ただし、クラウドサービスが、このページに記載されている技術要件の一部として特別にサポートされている場合は除きます（Azure Blob ストレージ、AWS S3 など）。

Adobe Managed Services の外部で Azure または AWS に AEM をデプロイする場合は、クラウドプロバイダーまたは使用するクラウド環境への AEM のデプロイメントをサポートするパートナーと直接共同作業することを強くお勧めします。選択したクラウドプロバイダーまたはパートナーは、アーキテクチャのサイズ仕様、設計および実装を担当し、顧客独自のパフォーマンス、負荷、スケーラビリティおよびセキュリティの要件が満たされるように支援します。

### Dispatcher のプラットフォーム（Web サーバー） {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングコンポーネントです。[最新のDispatcherバージョンをダウンロードします](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)。 Experience Manager 6.5 ではバージョン 4.3.2 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.2 で使用する場合は、次の Web サーバーがサポートされています。

| プラットフォーム | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** [1,2] | A：サポート対象 |
| Microsoft IIS 10（Internet Information Server） | A：サポート対象 |
| Microsoft IIS 8.5（Internet Information Server） | Z：サポート対象外 |

1. Apache httpd のソースコードをベースとして構築された Web サーバーは、ベースとした httpd のバージョンと同じサポートレベルでサポートされます。不明な場合は、各サーバー製品に関連するサポートレベルの確認をアドビに依頼してください。 次の場合：

   1. HTTP サーバーが公式の Apache ソースディストリビューションのみを使用して構築されている。または、
   1. HTTP サーバーが実行中のオペレーティングシステムの一部として配布されている。例：IBM HTTP Server、Oracle HTTP Server

1. Dispatcher は、Windows オペレーティングシステム版の Apache 2.4.x ではサポートされていません。

## サポートされているクライアントプラットフォーム {#supported-client-platforms}

### オーサリングユーザーインターフェイス向けにサポートされているブラウザー {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager ユーザーインターフェイスは次のクライアントプラットフォームで動作します。すべてのブラウザーは、デフォルトのプラグインおよびアドインのセットを使用してテストされています。

AEM のユーザーインターフェイスは、大きめの画面（通常はノートブックまたはデスクトップコンピューター）およびタブレットフォームファクター（Apple iPad、Microsoft Surface など）に向けて最適化されています。携帯電話のフォームファクターはサポートされていません。

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート**
>
>Mozilla Firefox、Google Chrome および Microsoft Edge では、数ヶ月ごとに更新プログラムがリリースされます。アドビは、これらのブラウザーの今後のバージョンで以下に示したサポートレベルを維持するために、Adobe Experience Manager の更新プログラムを提供します。

<table>
 <tbody>
  <tr>
   <td><strong>ブラウザー</strong></td>
   <td><strong>UI のサポート<br /> </strong></td>
   <td><strong>クラシック UI のサポート</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome（エバーグリーン）</strong></td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Microsoft Edge（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Mozilla Firefox（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Mozilla Firefox last ESR `\[1]`</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Apple Safari（macOS）（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x（macOS）</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Apple Safari（iOS 12.x）</td>
   <td>A:サポートされる`\[2]`</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Apple Safari （iOS 11.x）</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
 </tbody>
</table>

1. Firefox の延長サポート版（ESR）。[詳しくは、mozilla.org を参照してください。](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. Apple iPad のサポート。

### Web サイト向けにサポートされているブラウザー {#supported-browsers-for-websites}

一般的に、AEM Sites でレンダリングされる Web サイトのブラウザーサポートは、AEM ページテンプレート、デザイン、コンポーネント出力の実装に依存するので、これらの部品を実装する団体によって管理されます。

### WebDAV クライアント {#webdav-clients}

**Microsoft Windows 7 以降**

Microsoft Windows 7 以降を使用して、SSL で保護されていない AEM インスタンスに正常に接続するには、保護されていないネットワーク上での基本認証を Windows で有効にする必要があります。そのためには、Web クライアントの Windows レジストリを次のように変更する必要があります。

1. 次のレジストリのサブキーを探します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. このサブキーに 2 以上の値を使用して、BasicAuthLevel レジストリエントリを追加します。

Windows で WebDav クライアントの応答性を改善する方法については、[Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570) を参照してください。

## プラットフォームに関するその他の注意点 {#additional-platform-notes}

ここでは、Adobe Experience Manager およびそのアドオンの実行に関する注意点や詳細情報を説明します。

### IPv4 と IPv6 {#ipv-and-ipv}

Adobe Experience Manager のすべての要素（インスタンス、Dispatcher）は、IPv4 と IPv6 のいずれのネットワークにもインストールできます。

特別な設定は不要で、シームレスに運用できます。必要に応じて、使用するネットワークの種類に適した形式を使用して IP アドレスを指定できます。

つまり、IP アドレスを指定する必要がある場合には、次の形式から（必要に応じて）選択できます。

* an IPv6 address
for example `https://[ab12::34c5:6d7:8e90:1234]:4502`

* an IPv4 address
for example `https://123.1.1.4:4502`

* a server name
for example, `https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストール用に変換されます。
例：`https://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。See here to [enable Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Dynamic Media を有効にする場合は、以下の追加の技術要件が適用されます。

>[!NOTE]
>
>These system requirements **only** apply if you use Dynamic Media - Hybrid mode; Dynamic Media - Hybrid mode has an embedded image server, which is only certified on certain operating systems.
>
>Dynamic Media - Scene7 モード（**dynamicmedia_scene7** 実行モード）で Dynamic Media を実行する場合は、追加のシステム要件はありません。AEM と同じシステム要件が適用されます。Dynamic Media - Scene7 モードのアーキテクチャではクラウドベースの画像サービスを使用しており、AEM に組み込まれたサービスを使用していません。

#### ハードウェア {#hardware}

次のハードウェア要件は、Linux と Windows の両方に適用されます。

* Intel Xeon または AMD Opteron CPU（4 コア以上）
* 16 GB 以上の RAM

#### Linux {#linux}

Linux でダイナミックメディアを使用する場合は、次の必要条件を満たす必要があります。

* RedHat Enterprise 7 または CentOS 7 以降（最新の修正パッチを適用）
* 64 ビットのオペレーティングシステム
* スワッピング無効（推奨）
* SELinux 無効（以下の注意を参照）

>[!NOTE]
>
>LC_CTYPE（ロケール）が `en_US.UTF-8` 以外に設定されている場合、Dynamic Media は機能しません。値を確認するには、コマンドプロンプトで「locale」と入力します。設定が異なっている場合は、AEM を実行する前に「export LC_CTYPE=」と入力して、LC_CTYPE 環境変数を空の文字列に設定します。

>[!NOTE]
>
>**SELinux の無効化：**&#x200B;画像サービングは、SELinux が有効の場合は動作しません。このオプションはデフォルトで有効です。この問題を修正するには、**/etc/selinux/config** ファイルを編集し、SELinux 値を次のように変更します。
>
>`SELINUX=enforcing` **to**`SELINUX=disabled`

>[!NOTE]
>
>**NUMA アーキテクチャ：** AMD64 および Intel EM64T のプロセッサーを搭載したシステムは、通常は NUMA プラットフォームとして構成されます。このようなプラットフォームでは、カーネルにより、1 つのメモリノードではなく複数のメモリノードがブート時に作成されます。
>
>複数のノードを作成することで、他のノードが使い果たされる前に 1 つ以上のノードでメモリが枯渇する場合があります。メモリの枯渇が発生した場合、カーネルは、空きメモリがあってもプロセス（Image Server、Platform Server など）を強制終了することがあります。
>
>そのため、そのようなシステムを実行している場合は、**numa=off** ブートオプションを使用して NUMA をオフにし、カーネルによるこれらのプロセスの強制終了を防ぐことをお勧めします。

>[!NOTE]
>
>**サーバーのホスト名が解決される必要があります：**&#x200B;サーバーのホスト名が IP アドレスに解決可能であることを確認してください。If that is not possible, add the fully qualified host name and the IP address to **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 物理メモリ（RAM）の 2 倍以上のスワップ領域

Windows で Dynamic Media を使用するには、Microsoft Visual Studio 2010、2013、2015 の x64 および x86 用の再頒布可能パッケージをインストールします。

Windows x64 の場合：

* Get Microsoft Visual Studio 2010 redistributable at [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Get Microsoft Visual Studio 2013 redistributable at [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Get Microsoft Visual Studio 2015 redistributable at [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Windows x86 の場合：

* Get Microsoft Visual Studio 2010 redistributable at [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Get Microsoft Visual Studio 2013 redistributable at [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Get Microsoft Visual Studio 2015 redistributable at [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### MacOS {#macos}

* 10.9.x 以降
* 試用およびデモの目的でのみサポート

### AEM Forms PDF Generator の要件 {#requirements-for-aem-forms-pdf-generator}

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
* PDF Generator サービスでは Microsoft Windows 10 をサポートしていません。
>



### AEM Assets の XMP メタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは次のプラットフォームおよびファイル形式でサポートされ、有効にされます。

* **オペレーティングシステム：**

   * Linux（32 ビット、64 ビットシステムでは 32 ビットアプリケーションのサポートが必要）For steps to install 32-bit client libraries, see [How to enable XMP extraction and write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X（64 ビット）

* **File Formats**:JPEG、PNG、TIFF、PDF、INDD、AIおよびEPS。

### AEM Assetsでメタデータの多いアセットをLinuxで処理するための要件 {#assetsonlinux}

XMPFilesProcessorプロセスが動作するには、ライブラリGLIBC_2.14が必要です。 GLIBC_2.14を含むLinuxカーネルを使用します。例えば、Linuxカーネルバージョン3.1.xを使用します。PSDファイルなど、大量のメタデータを含むアセットの処理パフォーマンスが向上します。 以前のバージョンのGLIBCを使用すると、で始まるログでエラーが発生する `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`。
