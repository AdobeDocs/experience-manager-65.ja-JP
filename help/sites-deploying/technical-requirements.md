---
title: 技術要件
description: Adobe Experience Managerでサポートされているクライアントおよびサーバープラットフォームのリストです。
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 32af8ee1680bb0a357e64d614f22234ed331d314
workflow-type: tm+mt
source-wordcount: '3513'
ht-degree: 57%

---

# 技術要件 {#technical-requirements}

Adobeは、このドキュメントで次の情報に従って、プラットフォームで (AEM)Adobe Experience Managerをサポートします。

プラットフォームに関する問題については、プラットフォームのベンダーにお問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームに応じて、ユーザー管理に関する一連の要件が異なる場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件

* Java™ Platform, Standard Edition JDK またはその他のサポート対象の JDK をインストールしました。 [Java™仮想マシン](#java-virtual-machines)
* Experience Manager Quickstart ファイル（スタンドアロン JAR または web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

 Adobe Experience Manager を実行するための最小要件：

* 5 GB の空きディスク領域（インストールディレクトリ内）
* 2 GB メモリ

>[!NOTE]
>
>* デジタルアセットのユースケースには、より多くのベースメモリが必要です。詳しくは、「[デプロイと保守](/help/sites-deploying/deploy.md#default-local-install)」を参照してください。
>* [AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)には 15 GB の一時領域が必要です。
>


詳しくは、「[ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md)」を参照してください。

### サポートレベル {#support-levels}

このドキュメントには、Adobe Experience Manager でサポートされるクライアントおよびサーバーのプラットフォームが一覧化されています。アドビでは、推奨設定とその他の設定の両方について、複数のレベルのサポートを提供しています。

### サポートされる設定 {#supported-configurations}

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
   <td><strong>R：限定サポート</strong></td>
   <td>お客様のプロジェクトを確実に成功させるために、Adobeは、制限付きのサポートプログラム内で完全なサポートを提供します。このプログラムでは、特定の条件を満たす必要があります。 R レベルのサポートでは、正式なお客様のリクエストとアドビの確認が必要です。詳しくは、アドビカスタマーケアにお問い合わせください。</td>
  </tr>
 </tbody>
</table>

### サポートされていない設定 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| **Z：サポート対象外** | この設定はサポートされていません。 Adobeは、設定が機能するかどうかに関する記述を行わず、設定をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java™仮想マシン {#java-virtual-machines}

このアプリケーションを実行するには、Java™ Virtual Machine が必要です。Java™ Development Kit(JDK) ディストリビューションによって提供されます。

Adobe Experience Managerは、次のバージョンの Java™ Virtual Machines で動作します。

>[!CAUTION]
>
>Java™ベンダーからのセキュリティ速報を追跡します。 これにより、実稼動環境の安全性とセキュリティが確保されます。 また、常に最新の Java™アップデートをインストールしてください。

| **プラットフォーム** | **サポートレベル** | **リンク** |
|---|---|---|
| OracleJava™ SE 17 JDK | Z：サポート対象外 `[1]` |
| OracleJava™ SE 11 JDK - 64 ビット | A：サポート対象 `[1]` | [ダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| OracleJava™ SE 10 JDK | Z：サポート対象外 `[1]` |
| OracleJava™ SE 9 JDK | Z：サポート対象外 `[1]` |
| OracleJava™ SE 8 JDK - 64 ビット | A：サポート対象 `[1]` | [ダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM — ビルド 2.9、JRE 1.8.0 | A：サポート対象 `[2]` |
| IBM® J9 VM — ビルド 2.8、JRE 1.8.0 | A：サポート対象 `[2]` |
| Azul Zulu OpenJDK 11 - 64 ビット | A：サポート対象 `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 ビット | A：サポート対象 `[3]` |  |

1. Oracleは、OracleJava™ SE 製品の「長期サポート」(LTS) モデルに移行しました。 Java™ 9、Java™ 10、Java™ 12 は、Oracle別の非 LTS リリースです ( [OracleJava™ SE サポート・ロードマップ](https://www.oracle.com/jp/technetwork/java/eol-135779.html)) をクリックします。 実稼動環境にAEMをデプロイするために、Adobeは Java™の LTS リリースのみをサポートしています。 oracleJava™ SE JDK のサポートと配布は、OracleJava™ SE テクノロジーを使用するすべてのAEMのお客様に対して、LTS リリースの公開以降のすべてのメンテナンスアップデートを含め、Adobeで直接サポートされます。 詳しくは、 [Adobe Experience Managerの Java™サポートポリシー](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
**重要：OracleJava™ 11 は、2026 年 9 月まで少なくともサポートされます。 oracleJava™ 17 のサポートは準備中です。**

1. IBM® JRE は、WebSphere® Application Server と共にのみサポートされます。

1. Azul Zulu OpenJDK LTS バージョンは、バージョン 6.5 SP9 以降のオンプレミスの AEM デプロイメントでサポートされます。Azul Zulu JDK LTS バージョンのサポートと配布は、Adobeのお客様が Azul から直接ライセンスを受ける必要があります。


### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリをデプロイするには、様々なオプションがあります。次のリストに、サポートされるテクノロジーとストレージのオプションを示します。

| **プラットフォーム** | **説明** | **サポートレベル** |
|---|---|---|
| **TAR ファイルを使用したファイルシステム** `[1]` | リポジトリ | A：サポート対象 |
| **データストアを使用したファイルシステム** `[1]` | バイナリ | A：サポート対象 |
| ファイルシステムの TAR ファイルへのバイナリの格納 `[1]` | バイナリ | Z：実稼動環境ではサポートされていません |
| Amazon S3 | バイナリ | A：サポート対象 |
| Microsoft® Azure Blob Storage | バイナリ | A：サポート対象 |
| MongoDB Enterprise 4.4 | リポジトリ | A：サポート対象 `[2, 3, 4]` |
| MongoDB Enterprise 4.2 | リポジトリ | A：サポート対象 `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | リポジトリ | Z：サポート対象外 |
| MongoDB Enterprise 3.6 | リポジトリ | Z：サポート対象外 |
| MongoDB Enterprise 3.4 | リポジトリ | Z：サポート対象外 |
| IBM® DB2® 10.5 | リポジトリと Forms データベース | R：制限サポート `[5]` |
| Oracle Database 12c（12.1.x） | リポジトリと Forms データベース | R：制限サポート |
| Microsoft® SQL Server 2016 | Forms データベース | A：サポート対象 |
| **Apache Lucene（Quickstart 組み込み）** | 検索サービス | A：サポート対象 |
| Apache Solr | 検索サービス | A：サポート対象 |

1. 「ファイルシステム」には、POSIX に準拠したブロックストレージが含まれます。ネットワークストレージテクノロジーを含む。 ファイルシステムのパフォーマンスは異なり、全体的なパフォーマンスに影響を与える場合があることに注意してください。ネットワーク/リモートファイルシステムを使用してテストAEMをロードします。
1. MongoDB Enterprise バージョン 4.2 および 4.4 には、最低でも AEM 6.5 SP9 が必要です。
1. MongoDB Sharding は AEM ではサポートしていません。
1. MongoDB Storage Engine WiredTiger のみがサポートされています。
1. AEM Forms のアップグレードのお客様に対してサポートされます。新規インストールの場合はサポートされていません。

>[!NOTE]
AEM Communities の機能について詳しくは、[Communities のデプロイ](/help/communities/deploy-communities.md)を参照してください。

>[!NOTE]
MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、 [MongoDB ライセンスポリシー](https://www.mongodb.com/community/licensing) ページ。
MongoDB を使用した AEM のデプロイメントを最大限に活用するには、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。詳しくは、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)」を参照してください。
ライセンスには、標準レプリカセットが含まれています。このセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成され、オーサーデプロイメントまたはパブリッシュデプロイメントのどちらかに使用できます。
MongoDB でオーサーとパブリッシュの両方を実行する場合は、2 つの異なるライセンスを購入する必要があります。
Adobeカスタマーケアは、AEMでの MongoDB の使用に関する問題の認定に役立ちます。
詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。

>[!NOTE]
サポートされる上記のリレーショナルデータベースはサードパーティのソフトウェアであり、AEM ライセンスパッケージには含まれていません。
サポートされているリレーショナルデータベースで AEM 6.5 を実行するには、データベースベンダーとの個別のサポート契約が必要です。Adobeカスタマーケアは、AEM 6.5 でリレーショナルデータベースを使用する際の問題の絞り込みに役立ちます。
**現在、ほとんどのリレーショナルデータベースは、AEM 6.5 のレベル R でサポートされています。ここでは、上記のレベル R の説明に記載されているサポート基準とサポートプログラムが提供されます。**

### サーブレットエンジン / アプリケーションサーバー {#servlet-engines-application-servers}

Adobe Experience Manager は、スタンドアロンサーバー（Quickstart JAR ファイル）として、またはサードパーティのアプリケーションサーバー内の web アプリケーション（WAR ファイル）として実行できます。

サーブレット API の必要な最小バージョンは Servlet 3.1 です

| Platform | サポートレベル |
|---|---|
| **Quickstart 組み込みサーブレットエンジン（Jetty 9.4）** | A：サポート対象 |
| Oracle WebLogic Server 12.2（12cR2） | Z：サポート対象外 |
| IBM® WebSphere® Application Server Continuous Delivery(LibertyProfile) と Web Profile 7.0 およびIBM® JRE 1.8 | R：新規契約向けの制限サポート `[2]` |
| IBM® WebSphere® Application Server 9.0 およびIBM® JRE 1.8 | R：新規契約向けの制限サポート `[1]` `[2]` |
| Apache Tomcat 8.5.x | R：新規契約向けの制限サポート `[2]` |
| JBoss® EAP 7.2.x と JBoss® Application Server | Z：サポート対象外 |
| JBoss® EAP 7.1.4 と JBoss® Application Server | R：新規契約向けの制限サポート `[1]` `[2]` |
| JBoss® EAP 7.0.x と JBoss® Application Server | Z：サポート対象外 |

1. AEM Forms を使用したデプロイメントに推奨されます。
1. アプリケーションサーバーで AEM 6.5 デプロイメントを開始すると、制限付きサポートに移行します。既存のお客様は AEM 6.5 にアップグレードして、引き続きアプリケーションサーバーを使用することができます。新規のお客様の場合は、上記の Level-R の説明に記載されているサポート基準とサポートプログラムが付属しています。

### サーバーオペレーティングシステム {#server-operating-systems}

Adobe Experience Manager は、実稼動環境では次のサーバープラットフォームで動作します。

| **プラットフォーム** | **サポートレベル** |
|---|---|
| **Red Hat®ディストリビューションに基づく Linux®** | A：サポート対象 `[1]` `[3]` |
| Debian ディストリビューションに基づく Linux®。 Ubuntu を含む） | A：サポート対象 `[1]` `[2]` |
| Linux®(SUSE®配布に基づく ) | A：サポート対象 `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R：新規契約向けの制限サポート `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R：新規契約向けの制限サポート `[5]` |
| Microsoft® Windows Server 2012 R2 | Z：サポート対象外 |
| OracleSolaris™ 11 | Z：サポート対象外 |
| IBM® AIX® 7.2 | Z：サポート対象外 |

1. Linux® Kernel 2.6, 3. x、4.x および 5.x には、Red Hat® Enterprise Linux®、CentOS、OracleLinux®、Amazon Linux®など、Red Hat®ディストリビューションの派生製品が含まれます。 AEM Formsアドオン機能は、CentOS 7、Red Hat® Enterprise Linux® 7、Red Hat® Enterprise Linux® 8、および Red Hat® Enterprise Linux® 9 でのみサポートされます。
1. AEM Forms は Ubuntu 20.04 LTS でサポートされています。
1. Adobe Managed Services でサポートされる Linux®ディストリビューション。
1. Microsoft® Windows の実稼動デプロイメントは、6.5 にアップグレードするお客様と、実稼動以外の使用に対してサポートされます。 新しいデプロイメントは、AEM Sites および Assets に対してリクエストに応じて行われます。
1. AEM Formsは、Microsoft® Window Server でサポートされていますが、サポートレベルの R 制限はありません。

>[!NOTE]
AEM Forms 6.5 をインストールする場合は、次の 32 ビット版のMicrosoft® Visual C++再頒布可能パッケージがインストールされていることを確認してください。
* Microsoft® Visual C++ 2008 2008 再頒布可能パッケージ
* Microsoft® Visual C++ 2010 の再頒布可能パッケージ
* Microsoft® Visual C++ 2012 再頒布可能パッケージ
* Microsoft® Visual C++ 2013 の再頒布可能パッケージ（6.5 時点）



### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Adobe Experience Managerは、クラウドコンピューティング環境上の仮想マシンでの実行をサポートしています。 これらの環境には、Microsoft® Azure およびAmazon Web Services(AWS) として、このページに記載されている技術要件に従って実行される環境、Adobeの標準サポート条件に従って実行される環境が含まれます。

クラウドネイティブな環境の場合は、AEM 製品ラインの最新オファー、Adobe Experience Manager as a Cloud Service をご確認ください。詳しくは、[Adobe Experience Manager as a Cloud Service ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)を参照してください。

アドビは、AEM を Azure または AWS にデプロイするための Adobe Managed Services も提供しています。Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。[Adobe Managed Services に関するドキュメント](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t)を参照してください。

Azure、AWS、またはその他のクラウドコンピューティング環境にAEMをデプロイするその他すべての場合は、Adobeからのサポートが仮想コンピューティング環境に含まれます。 この仮想環境は、このページに示す技術仕様に従って実行する必要があります。 これらのクラウド環境のいずれかで実行されているAEMに関して報告された問題は、クラウドコンピューティング環境に固有のクラウドサービスとは独立して再現可能である必要があります。 つまり、このページに記載されている技術要件の一部として Cloud Service がサポートされていない限り ( 例：Azure Blob ストレージやAWS S3)。

AEMを Azure またはAWSにデプロイする方法に関する推奨事項については、Adobe Managed Services の外部で、クラウドプロバイダーを直接操作することをお勧めします。 または、お客様が選択したAdobe環境でのAEMのデプロイメントをサポートするクラウドパートナーと協力します。 選択したクラウドプロバイダーまたはパートナーは、特定のパフォーマンス、負荷、拡張性、セキュリティ要件を満たすように、アーキテクチャのサイズ設定、設計、実装を担当します。

### Dispatcher プラットフォーム（web サーバー） {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングのコンポーネントです。 [最新バージョンの Dispatcher をダウンロード](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en)します。Experience Manager 6.5 ではバージョン 4.3.2 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.2 での使用では、次の web サーバーがサポートされています。

| Platform | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A：サポート対象 |
| Microsoft® IIS 10(Internet Information Server) | A：サポート対象 |
| Microsoft® IIS 8.5 (Internet Information Server) | Z：サポート対象外 |

1. Apache httpd ソースコードに基づいて構築された Web サーバーは、ベースとなる httpd のバージョンと同じくらい多くのサポートを持っています。 これらに当てはまるか不明の場合は、アドビに問い合わせて、それぞれのサーバー製品に関するサポートレベルを確認してください。以下の場合に該当します。

   1. HTTP サーバーは、公式の Apache ソース配布のみを使用して構築されています。
   1. HTTP サーバーは、HTTP サーバーが実行されているオペレーティングシステムの一部として配信されました。例：IBM® HTTP Server、OracleHTTP Server

1. Dispatcher は、Windows オペレーティングシステム用の Apache 2.4.x では使用できません。

## サポートされているクライアントプラットフォーム {#supported-client-platforms}

### オーサリングユーザーインターフェイスでサポートされているブラウザー {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager のユーザーインターフェイスは、次のクライアントプラットフォームで使用できます。すべてのブラウザーは、デフォルトのプラグインとアドオンのセットを使用してテストされます。

AEMのユーザーインターフェイスは、大きな画面（通常はノートブックやデスクトップコンピューター）とタブレットのフォームファクタ (Apple iPadやMicrosoft® Surface など ) に最適化されています。 電話のフォームファクターはサポートされていません。

>[!NOTE]
**リリースサイクルの短いブラウザーのサポート：**
Mozilla Firefox、Google Chrome、Microsoft® Edge のリリースは、数か月ごとに更新されます。 アドビは、これらのブラウザーの今後のバージョンで以下に示すサポートレベルを維持するために、Adobe Experience Manager のアップデートの提供に取り組んでいます。

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
   <td>Microsoft® Edge（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
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
   <td>macOS の Apple Safari（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>macOS の Apple Safari 11 x</td>
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

1. Firefox の拡張サポートリリース [mozilla.org の詳細](https://www.mozilla.org/en-US/firefox/enterprise/)
1. Apple iPad のサポート

### Web サイトでサポートされているブラウザー {#supported-browsers-for-websites}

一般に、AEM Sites でレンダリングされる web サイトのブラウザーサポートは、AEM ページテンプレートの実装、設計およびコンポーネントの出力に依存するので、これらの部分を実装する当事者の管理下にあります。

### WebDAV クライアント {#webdav-clients}

**Microsoft® Windows 7 以降**

Microsoft® Windows 7 以降を使用して、SSL で保護されていないAEMインスタンスに接続する場合、Windows でセキュリティで保護されていないネットワークを介した基本認証を有効にする必要があります。 WebClient の Windows レジストリの変更が必要です。

1. 以下のレジストリサブキーを探します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2 つ以上の値を使用して、このサブキーに BasicAuthLevel レジストリのエントリを追加します。

## プラットフォームに関するその他の注意事項 {#additional-platform-notes}

このセクションでは、Adobe Experience Manager とそのアドオンの実行に関する特別な注意事項と詳細情報を説明します。

### IPv4 と IPv6 {#ipv-and-ipv}

Adobe Experience Manager（インスタンス、Dispatcher）のすべての要素は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定が不要なので、操作はシームレスです。必要に応じて、ネットワークの種類に適した形式で IP アドレスを指定します。

IP アドレスを指定する必要がある場合は、次の中から（必要に応じて）選択できます。

* IPv6 アドレス。例： `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 アドレス。例： `https://123.1.1.4:4502`

* サーバー名。例： `https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストールで解釈されます。 例：`https://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。[Dynamic Media の有効化](/help/assets/config-dynamic.md#enabling-dynamic-media)についてはこちらを参照してください。

Dynamic Media を有効にする場合は、以下の追加の技術要件が適用されます。

>[!NOTE]
これらのシステム要件は、Dynamic Media - ハイブリッドモードを使用する場合に&#x200B;**のみ**&#x200B;適用されます。Dynamic Media - ハイブリッドモードには画像サーバーが組み込まれており、特定のオペレーティングシステムでのみ認定されています。
Dynamic Media - Scene7モード ( つまり、 **dynamicmedia_scene7** 実行モード )、追加の必要システム構成はありません。AEMと同じシステム要件のみ。 Dynamic Media - Scene7 モードのアーキテクチャでは、AEM に埋め込まれたサービスではなく、クラウドベースの画像サービスを使用します。

#### ハードウェア {#hardware}

Linux®と Windows の両方に適用できるハードウェア要件は次のとおりです。

* Intel Xeon®または AMD® Opteron CPU と 4 つ以上のコア
* 16 GB 以上の RAM

#### Linux® {#linux}

Linux®でDynamic Mediaを使用している場合は、次の前提条件を満たす必要があります。

* 最新の修正パッチが適用された Red Hat® Enterprise 7 または CentOS 7 以降
* 64 ビットオペレーティングシステム
* スワップ無効（推奨）
* SELinux 無効（後述の注意を参照）

>[!NOTE]
LC_CTYPE（ロケール）が `en_US.UTF-8` 以外に設定されている場合、Dynamic Media は機能しません。値を確認するには、コマンドプロンプトに対して「locale」と入力します。 適切に設定されていない場合、AEMを実行する前に&quot;export LC_CTYPE=&quot;と入力して、LC_CTYPE 環境変数を空の文字列に設定します。

>[!NOTE]
**SELinux の無効化：** SELinux がオンの場合、画像サービングは機能しません。このオプションはデフォルトで有効です。この問題を修正するには、 **/etc/selinux/config** ファイルを開き、SELinux 値を次の値から変更します。
`SELINUX=enforcing`**を、**`SELINUX=disabled` に変更

>[!NOTE]
**NUMA アーキテクチャ：** AMD64 および Intel® EM64Tを搭載したプロセッサを搭載したシステムは、通常、NUMA(Non-Uniform Memory Architecture) プラットフォームとして構成されます。 つまり、カーネルは、単一のメモリノードを構築するのではなく、ブート時に複数のメモリノードを構築します。
複数のノード構成体を使用すると、他のノードが消費される前に、1 つまたは複数のノードでメモリが枯渇する可能性があります。メモリが枯渇した場合、使用可能なメモリがあっても、カーネルはプロセス（画像サーバーやプラットフォームサーバーなど）を強制終了する可能性があります。
そのため、そうしたシステムを実行する場合は、**numa=off** 起動オプションを使用して NUMA をオフにし、カーネルがこれらのプロセスを強制終了するのを避けるようにすることをお勧めします。

>[!NOTE]
**サーバーホスト名を解決する必要があります。**&#x200B;サーバーのホスト名が IP アドレスに解決できることを確認します。解決できない場合は、完全修飾ホスト名と IP アドレスを **/etc/hosts** に次のように追加してください。
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 物理メモリ（RAM）の少なくとも 2 倍の容量に等しいスワップ領域

Windows でDynamic Mediaを使用するには、x64 および x86 用のMicrosoft® Visual Studio 2010、2013、および 2015 の再頒布可能パッケージをインストールします。

Windows x64 の場合：

* Microsoft® Visual Studio 2010 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999)
* Microsoft® Visual Studio 2013 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)
* Microsoft® Visual Studio 2015 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/ja-jp/download/details.aspx?id=48145)

Windows x86 の場合：

* Microsoft® Visual Studio 2010 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999)
* Microsoft® Visual Studio 2013 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Microsoft® Visual Studio 2015 の再頒布可能パッケージを入手する ( ) [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/ja-jp/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x 以降
* 体験版およびデモ版のみサポート

### AEM Forms PDF Generator の要件 {#requirements-for-aem-forms-pdf-generator}

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
PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、および日本語版のみをサポートしています。
さらに、
* PDF Generator で変換を実行するには、32 ビット版の [Acrobat 2020 Classic トラックバージョン 20.004.30006](https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html) または Acrobat 2017 バージョン 17.011.30078 が必要です。
* OpenOffice 用のPDFジェネレーター変換は、Windows と Linux®でのみサポートされています。
* PDFジェネレーターは、Microsoft® Office Professional Plus の 32 ビット版の小売版と、Windows オペレーティングシステムでの変換に必要なその他のソフトウェアのみをサポートしています。
* PDFジェネレーターは、Linux®オペレーティングシステム上の OpenOffice の 32 ビット版および 64 ビット版をサポートしています。
* PDFジェネレータはMicrosoft® Office 365 をサポートしていません。
* OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
* Acrobat のバージョンは、PDF Generator 機能を有効にするために AEM Forms にバンドルされています。バンドルされたバージョンには、AEM FormsPDFジェネレーターで使用するために、AEM Formsライセンスの期間中に、プログラムによってAEM Formsでのみアクセスします。 詳しくは、デプロイメントに応じたAEM Forms製品の説明 ([オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html) または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* PDFジェネレーターサービスは、Microsoft® Windows 10 をサポートしていません。
* PDFジェネレータは、Microsoft® Visio 2019 を使用してファイルを変換できません。 Microsoft® Visio 2016 を引き続き使用して変換できます `.VSD` および `.VSDX` ファイル。
* PDFジェネレーターが、Microsoft® Project 2019 を使用してファイルを変換できません。 Microsoft® Project 2016 を引き続き使用して、変換を行うことができます `.VSD` および `.VSDX` ファイル。
>


### AEM Forms Designer の要件 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server または Microsoft® Windows® 10
* 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
* 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
* 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC。
* Designer をインストールするための管理者権限。

### AEM Assets XMPメタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは、次のプラットフォームおよびファイル形式でサポートされ、有効になります。

* **オペレーティングシステム：**

   * Linux®（64 ビットシステムでは 32 ビットおよび 32 ビットアプリケーションがサポートされます）。 32 ビットクライアントライブラリのインストール手順については、 [64 ビット Red Hat® Linux®でXMPの抽出と書き戻しを有効にする方法](https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X（64 ビット）

* **ファイル形式**：JPEG、PNG、TIFF、PDF、INDD、AI、EPS

### AEM Assets がメタデータの多いアセットを Linux で処理するための要件® {#assetsonlinux}

XMPFilesProcessor プロセスを実行するには、ライブラリ GLIBC_2.14 が必要です。GLIBC_2.14 を含む Linux®カーネルを使用します。例えば、Linux®カーネルバージョン 3.1.x です。PSDファイルなど、大量のメタデータを含むアセットの処理パフォーマンスが向上します。 以前のバージョンの GLIBC を使用するとエラーが発生し、`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP` で始まるメッセージがログに記録されます。
