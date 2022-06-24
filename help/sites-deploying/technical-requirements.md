---
title: 技術要件
seo-title: Technical Requirements
description: AEM でサポートされているクライアントおよびサーバーのプラットフォームのリスト。
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 3643534fa0f24a1c2ea00c35853a2671b156bf9a
workflow-type: tm+mt
source-wordcount: '3329'
ht-degree: 95%

---

# 技術要件{#technical-requirements}

アドビは、このドキュメントの以下の情報に記載されているプラットフォームで Adobe Experience Manager（AEM）をサポートしています。

プラットフォームに関連する問題については、プラットフォームのベンダーにお問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームによっては、別のユーザー管理要件が適用される場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件：

* Java Platform, Standard Edition JDK または他のサポートされている [Java 仮想マシン](#java-virtual-machines)がインストールされていること
* Experience Manager Quickstart ファイル（スタンドアロン JAR または web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

 Adobe Experience Manager を実行するための最小要件：

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
| **Z：サポート対象外** | この構成はサポートされません。Adobe では、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java 仮想マシン {#java-virtual-machines}

このアプリケーションの実行には、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションによって提供されます。

Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

>[!CAUTION]
>
>Java ベンダーが発表するセキュリティ情報を常に確認し、実稼動環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。

| **プラットフォーム** | **サポートレベル** | **リンク** |
|---|---|---|
| Oracle Java SE 11 JDK - 64 ビット | A：サポート対象 `[1]` | [ダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java SE 10 JDK | Z：サポート対象外 `[1]` |
| Oracle Java SE 9 JDK | Z：サポート対象外 `[1]` |
| Oracle Java SE 8 JDK - 64 ビット | A：サポート対象 `[1]` | [ダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM - ビルド 2.9、JRE 1.8.0 | A：サポート対象 `[2]` |
| IBM J9 VM - ビルド 2.8、JRE 1.8.0 | A：サポート対象 `[2]` |
| Azul Zulu OpenJDK 11 - 64 ビット | A：サポート対象 `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 ビット | A：サポート対象 `[3]` |  |

1. Oracle は Oracle Java SE 製品の「長期サポート」（LTS）モデルに移行しました。Java 9、Java 10、Java 12 は Oracle による非 LTS でのリリースです（[Oracle Java SE サポートロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html)を参照）。実稼動環境に AEM をデプロイするために、アドビでは LTS リリース版の Java のみサポートします。パブリックアップデート終了後の LTS リリースのすべてのメンテナンスアップデートを含む Oracle Java SE JDK のサポートと配布が、アドビによって直接サポートされます。対象となるのは、Oracle Java SE テクノロジーを利用しているすべての AEM ユーザーです。詳しくは、 [Adobe Experience Managerの Java サポートポリシー](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) を参照してください。


1. IBM JRE は、WebSphere Application Server と共に使用する場合にのみサポートされます。

1. Azul Zulu OpenJDK LTS バージョンは、バージョン 6.5 SP9 以降のオンプレミスのAEM展開でサポートされます。 Azul Zulu JDK LTS バージョンのサポートと配布は、お客様が Azul から直接ライセンスを受ける必要があります。


### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリのデプロイには、様々なオプションがあります。サポートされるテクノロジーとストレージオプションについては、以下のリストを参照してください。

| **プラットフォーム** | **説明** | **サポートレベル** |
|---|---|---|
| **TAR ファイルを使用したファイルシステム** `[1]` | リポジトリー | A：サポート対象 |
| **データストアを使用したファイルシステム** `[1]` | バイナリ | A：サポート対象 |
| ファイルシステムの TAR ファイルへのバイナリの格納 `[1]` | バイナリ | Z：実稼動環境ではサポート対象外 |
| Amazon S3 | バイナリ | A：サポート対象 |
| Microsoft Azure Blob Storage | バイナリ | A：サポート対象 |
| MongoDB Enterprise 4.2 | リポジトリ | A：サポート対象 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | リポジトリ | Z：サポート対象外 |
| MongoDB Enterprise 3.6 | リポジトリー | Z：サポート対象外 |
| MongoDB Enterprise 3.4 | リポジトリー | Z：サポート対象外 |
| IBM DB2 10.5 | リポジトリおよび Forms データベース | R：制限サポート `[5]` |
| Oracle Database 12c（12.1.x） | リポジトリおよび Forms データベース | R：制限サポート |
| Microsoft SQL Server 2016 | Forms データベース | A：サポート対象 |
| **Apache Lucene（クイックスタート組み込み）** | 検索サービス | A：サポート対象 |
| Apache Solr | 検索サービス | A：サポート対象 |

1. 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
1. MongoDB Enterprise 4.2 を使用するには、最低でもAEM 6.5 SP9 が必要です。
1. MongoDB Sharding は AEM ではサポートしていません。
1. MongoDB Storage Engine WiredTiger のみサポートされています。
1. AEM Forms アップグレード版のお客様にサポートされています。新規インストールの場合はサポートされていません。

>[!NOTE]
>
>AEM コミュニティの機能について詳しくは、[コミュニティのデプロイ](/help/communities/deploy-communities.md)を参照してください。

>[!NOTE]
>
>MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。
>
>MongoDB を利用した AEM デプロイメントを最大限活用するために、アドビでは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。詳しくは、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)」を参照してください。
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
| IBM WebSphere Application Server Continuous Delivery（LibertyProfile）（Web Profile 7.0 および IBM JRE 1.8） | R：新規契約向けの制限サポート `[2]` |
| IBM WebSphere Application Server 9.0 および IBM JRE 1.8 | R：新規契約向けの制限サポート `[1]` `[2]` |
| Apache Tomcat 8.5.x | R：新規契約向けの制限サポート `[2]` |
| JBoss EAP 7.2.x と JBoss Application Server | Z：サポート対象外 |
| JBoss EAP 7.1.4 と JBoss Application Server | R：新規契約向けの制限サポート `[1]` `[2]` |
| JBoss EAP 7.0.x と JBoss Application Server | Z：サポート対象外 |

1. AEM Forms を備えたデプロイメントに推奨されています。
1. アプリケーションサーバーでの AEM 6.5 デプロイメントの起動は制限サポートに移行します。既存のお客様は AEM 6.5 にアップグレードして、アプリケーションサーバーを引き続き使用することができます。新規のお客様には、前述のレベル R の説明にあるサポート基準とサポートプログラムが適用されます。

### サーバーオペレーティングシステム {#server-operating-systems}

実稼働環境の Adobe Experience Manager は次のサーバープラットフォームで動作します。

| **プラットフォーム** | **サポートレベル** |
|---|---|
| **Linux、Red Hat ディストリビューションベース** | A：サポート対象 `[1]` `[3]` |
| Linux、Debian ディストリビューションベース（Ubuntu を含む） | A：サポート対象 `[2]` |
| Linux、SUSE ディストリビューションベース | A：サポート対象 |
| Microsoft Windows Server 2019 `[4]` | R：新規契約向けの制限サポート |
| Microsoft Windows Server 2016 `[4]` | R：新規契約向けの制限サポート `[5]` |
| Microsoft Windows Server 2012 R2 | Z：サポート対象外 |
| Oracle Solaris 11 | Z：サポート対象外 |
| IBM AIX 7.2 | Z：サポート対象外 |

1. Linux Kernel 2.6、3.x および 4.x には、Red Hat ディストリビューションの派生 OS（Red Hat Enterprise Linux、CentOS、Oracle Linux、Amazon Linux など）が含まれます。AEM Formsアドオン機能は、CentOS 7、Red Hat Enterprise Linux 7、および Red Hat Enterprise Linux 8 でのみサポートされています。
1. AEM Forms は Ubuntu 16.04 LTS でのみサポートされています。
1. Adobe Managed Services でサポートされている Linux ディストリビューション
1. Microsoft Windows 版の実稼働デプロイメントは、お客様が 6.5 にアップグレードする場合と、実稼動以外の用途に使用する場合にサポートされています。AEM Sites および AEM Assets の新規デプロイメントは、お客様の依頼に応じて提供されます。
1. AEM Forms は、サポートレベル R の制限なしに Microsoft Window Server でサポートされています。。


### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Microsoft Azure や Amazon Web Services（AWS）など、クラウドコンピューティング環境の仮想マシンでの Adobe Experience Manager の稼動は、このページに記載されている技術要件およびアドビの標準サポート条件に従ってサポートされています。

クラウドネイティブな環境の場合は、AEM製品ラインで最新のオファーを確認します。Adobe Experience Manager as a Cloud Service。 詳しくは、 [Adobe Experience Manager as a Cloud Service Documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) 」を参照してください。

Adobeでは、AEMを Azure またはAWSにデプロイするための Adobe Managed Services も提供しています。 Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。[Adobe Managed Services に関するドキュメント](https://www.adobe.com/jp/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)も参照してください。

AEM を Azure や AWS にデプロイするその他あらゆる場合、またはその他のクラウドコンピューティング環境にデプロイする場合、アドビによるサポートは、このページに記載されている技術仕様に従って、仮想コンピューティング環境に対して提供されます。これらのクラウド環境で実行される AEM に関連する問題を報告する場合は、その問題が、クラウドコンピューティング環境に固有のクラウドサービスと関係なく再現可能である必要があります。ただし、クラウドサービスが、このページに記載されている技術要件の一部として特別にサポートされている場合は除きます（Azure Blob ストレージ、AWS S3 など）。

Adobe Managed Services の外部で Azure または AWS に AEM をデプロイする場合は、クラウドプロバイダーまたは使用するクラウド環境への AEM のデプロイメントをサポートするパートナーと直接共同作業することを強くお勧めします。選択したクラウドプロバイダーまたはパートナーは、アーキテクチャのサイズ仕様、設計および実装を担当し、顧客独自のパフォーマンス、負荷、スケーラビリティおよびセキュリティの要件が満たされるように支援します。

### Dispatcher のプラットフォーム（Web サーバー） {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングコンポーネントです。[最新バージョンの Dispatcher をダウンロード](https://helpx.adobe.com/jp/experience-manager/dispatcher/release-notes.html)します。Experience Manager 6.5 ではバージョン 4.3.2 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.2 で使用する場合は、次の Web サーバーがサポートされています。

| プラットフォーム | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A：サポート対象 |
| Microsoft IIS 10（Internet Information Server） | A：サポート対象 |
| Microsoft IIS 8.5（Internet Information Server） | Z：サポート対象外 |

1. Apache httpd のソースコードをベースとして構築された Web サーバーは、ベースとした httpd のバージョンと同じサポートレベルでサポートされます。これらに当てはまるか不明の場合は、アドビに問い合わせて、それぞれのサーバー製品に関するサポートレベルを確認してください。以下の場合に該当します。

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
   <td>Mozilla Firefox 最新 ESR [1]</td>
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
   <td>A：サポート対象 [2]</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Apple Safari（iOS 11.x）</td>
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

Windows での WebDav クライアントの応答性を向上させるには、 [Microsoftサポート KB 2445570](https://support.microsoft.com/kb/2445570)

## プラットフォームに関するその他の注意点 {#additional-platform-notes}

ここでは、Adobe Experience Manager およびそのアドオンの実行に関する注意点や詳細情報を説明します。

### IPv4 と IPv6 {#ipv-and-ipv}

Adobe Experience Manager のすべての要素（インスタンス、Dispatcher）は、IPv4 と IPv6 のいずれのネットワークにもインストールできます。

特別な設定は不要で、シームレスに運用できます。必要に応じて、使用するネットワークの種類に適した形式を使用して IP アドレスを指定できます。

つまり、IP アドレスを指定する必要がある場合には、次の形式から（必要に応じて）選択できます。

* IPv6 アドレス
例： `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 アドレス
例： `https://123.1.1.4:4502`

* サーバー名
例：`https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストール用に変換されます。
例：`https://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。[Dynamic Media の有効化](/help/assets/config-dynamic.md#enabling-dynamic-media)についてはこちらを参照してください。

Dynamic Media を有効にする場合は、以下の追加の技術要件が適用されます。

>[!NOTE]
>
>これらのシステム要件は、Dynamic Media - ハイブリッドモードを使用する場合に&#x200B;**のみ**&#x200B;適用されます。Dynamic Media - ハイブリッドモードには画像サーバーが組み込まれており、特定のオペレーティングシステムでのみ認定されています。
>
>Dynamic Media - Scene7 モード（**dynamicmedia_scene7** 実行モード）で Dynamic Media を実行する場合は、追加のシステム要件はありません。AEM と同じシステム要件が適用されます。Dynamic Media - Scene7 モードのアーキテクチャではクラウドベースの画像サービスを使用しており、AEM に組み込まれたサービスを使用していません。

#### ハードウェア {#hardware}

次のハードウェア要件は、Linux と Windows の両方に適用されます。

* Intel Xeon または AMD Opteron CPU（4 コア以上）
* 16 GB 以上の RAM

#### Linux {#linux}

Linux で Dynamic Media を使用する場合は、次の必要条件を満たす必要があります。

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
>`SELINUX=enforcing`**コピー先：**`SELINUX=disabled`

>[!NOTE]
>
>**NUMA アーキテクチャ：** AMD64 および Intel EM64T のプロセッサーを搭載したシステムは、通常は NUMA プラットフォームとして構成されます。このようなプラットフォームでは、カーネルにより、1 つのメモリノードではなく複数のメモリノードがブート時に作成されます。
>
>複数のノードを作成することで、他のノードが使い果たされる前に 1 つ以上のノードでメモリが枯渇する場合があります。メモリの枯渇が発生した場合、カーネルは、空きメモリがあってもプロセス（Image Server、Platform Server など）を強制終了することがあります。
>
>そのため、そのようなシステムを実行している場合は、**numa=off** ブートオプションを使用して NUMA をオフにし、カーネルによるこれらのプロセスの強制終了を防ぐことをお勧めします。

>[!NOTE]
>
>**サーバーのホスト名が解決される必要があります：**&#x200B;サーバーのホスト名が IP アドレスに解決可能であることを確認してください。解決できない場合は、完全修飾ホスト名と IP アドレスを **/etc/hosts** に次のように追加してください。
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 物理メモリ（RAM）の 2 倍以上のスワップ領域

Windows で Dynamic Media を使用するには、Microsoft Visual Studio 2010、2013、2015 の x64 および x86 用の再頒布可能パッケージをインストールします。

Windows x64 の場合：

* Microsoft Visual Studio 2010 の再頒布可能パッケージを入手する（[https://www.microsoft.com/ja-jp/download/details.aspx?id=13523](https://www.microsoft.com/ja-jp/download/details.aspx?id=13523)）
* Microsoft Visual Studio 2013 の再頒布可能パッケージを入手する（[https://www.microsoft.com/ja-jp/download/details.aspx?id=40784](https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)）
* Microsoft Visual Studio 2015 の再頒布可能パッケージを入手する（[https://www.microsoft.com/ja-jp/download/details.aspx?id=48145](https://www.microsoft.com/ja-jp/download/details.aspx?id=48145)）

Windows x86 の場合：

* Microsoft Visual Studio 2010 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/ja-jp/download/details.aspx?id=5555)）
* Microsoft Visual Studio 2013 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)）
* Microsoft Visual Studio 2015 の再頒布可能パッケージを入手する（[https://www.microsoft.com/ja-jp/download/details.aspx?id=52685](https://www.microsoft.com/ja-jp/download/details.aspx?id=52685)）

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
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 クラシックトラック</a> 最新バージョン</td>
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
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator では、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみがサポートされます。
>
>さらに、次の点に注意してください。
>
>* PDF Generator で変換を実行するには、32 ビット版の [Acrobat 2017 クラシックトラックバージョン 17.011.30078 以降](https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html)が必要です。
>* PDF Generator では、32 ビットリテール版の Microsoft Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>* PDF Generator では Microsoft Office 365 をサポートしていません。
>* PDF Generator の OpenOffice 向け変換機能は、Windows と Linux でのみサポートされています。
>* 「OCR PDF」、「PDF を最適化」、「PDF を書き出し」の各機能は、Windows でのみサポートされています。
>* Acrobat のバージョンは、PDF Generator 機能を有効にするために、AEM Forms にバンドルされます。バンドルされたバージョンは、AEM Forms PDF Generator で使用するために、AEM Forms ライセンスの期間中、AEM Forms でのみプログラムによってアクセスされます。詳しくは、デプロイメント（[オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html)または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html)）に応じた AEM Forms 製品説明を参照してください。
>
>* PDF Generator サービスでは Microsoft Windows 10 をサポートしていません。
>


### AEM Forms Designer の要件 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server または Microsoft® Windows® 10
* 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
* 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
* 16 GB のディスク空き容量（32-bit OS の場合）または 20 GB のディスク空き容量（64-bit OS の場合）
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。
* Designer をインストールするための管理者権限。

### AEM Assets の XMP メタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは次のプラットフォームおよびファイル形式でサポートされ、有効にされます。

* **オペレーティングシステム：**

   * Linux（32 ビット、64 ビットシステムでは 32 ビットアプリケーションのサポートが必要）32 ビットのクライアントライブラリをインストールする手順については、[64 ビット RedHat Linux で XMP の抽出と書き戻しを有効にする方法](https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。

   * Windows Server
   * Mac OS X（64 ビット）

* **ファイル形式**：JPEG、PNG、TIFF、PDF、INDD、AI、EPS

### AEM Assets がメタデータの多いアセットを Linux で処理するための要件 {#assetsonlinux}

XMPFilesProcessor プロセスを実行するには、ライブラリ GLIBC_2.14 が必要です。GLIBC_2.14 を含む Linux カーネルを使用します。例えば、Linux カーネルバージョン 3.1.x です。PSD ファイルなど、大量のメタデータを含むアセットの処理パフォーマンスが向上します。以前のバージョンの GLIBC を使用するとエラーが発生し、`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP` で始まるメッセージがログに記録されます。
