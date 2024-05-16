---
title: デプロイとメンテナンス
description: AEM のインストールを開始する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: ht
source-wordcount: '1792'
ht-degree: 100%

---

# デプロイとメンテナンス {#deploying-and-maintaining}

このページの内容は次のとおりです。

* [基本概念](#basic-concepts)

   * [AEM とは](#what-is-aem)
   * [典型的な開発](#typical-deployment-scenarios)

      * [オンプレミス](#on-premise)
      * [Cloud Manager を使用した Managed Services](#managed-services-using-cloud-manager)

* [はじめに](#getting-started)

   * [前提条件](#prerequisites)
   * [ソフトウェアの入手](#getting-the-software)
   * [デフォルトのローカルインストール](#default-local-install)
   * [オーサーとパブリッシュのインストール](#author-and-publish-installs)
   * [展開されたインストールディレクトリ](#unpacked-install-directory)
   * [起動と停止](#starting-and-stopping)

これらの基本を理解したうえで、より高度かつ詳細な情報を習得するには、次のサブページを参照してください。

* [技術要件](/help/sites-deploying/technical-requirements.md)
* [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)
* [カスタムスタンドアロンインストール](/help/sites-deploying/custom-standalone-install.md)
* [アプリケーションサーバーのインストール](/help/sites-deploying/application-server-install.md)
* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
* [コマンドラインによる起動と停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)
* [e コマース](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定方法に関する記事](/help/sites-deploying/ht-deploy.md)
* [Web コンソール](/help/sites-deploying/web-console.md)
* [レプリケーションのトラブルシューティング](/help/sites-deploying/troubleshoot-rep.md)
* [ベストプラクティス](/help/sites-deploying/best-practices.md)
* [Communities のデプロイ](/help/communities/deploy-communities.md)
* [AEM プラットフォームの概要](/help/sites-deploying/platform.md)
* [パフォーマンスガイドライン](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 使用の手引き](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens とは](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=ja)

## 基本概念 {#basic-concepts}

### AEM とは {#what-is-aem}

Adobe Experience Manager は、商用 web サイトおよび関連サービスを構築、管理、デプロイするための、web ベースのクライアントサーバーシステムです。インフラストラクチャレベルおよびアプリケーションレベルのいくつかの機能を組み合わせて、単一の統合パッケージにします。

インフラストラクチャレベルで、AEM は次の機能を提供します。

* **Web アプリケーションサーバー**：AEM は、スタンドアロンモードで（統合 Jetty Web サーバーを含む）、またはサードパーティのアプリケーションサーバー内の web アプリケーションとしてデプロイできます。
* **Web アプリケーションフレームワーク**：AEM には Sling web アプリケーションフレームワークが組み込まれており、RESTful でコンテンツ指向 web アプリケーションを簡単に記述できます。
* **コンテンツリポジトリ**：AEM には、非構造化データと半構造化データ用に特別に設計された階層データベースの一種である、Java™ コンテンツリポジトリ（JCR）が含まれています。リポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレート、内部データも保存されます。

この基盤の上に、AEM では以下の管理のためにアプリケーションレベルの機能もいくつか提供しています。

* **Web サイト**
* **モバイルアプリケーション**
* **デジタルパブリケーション**
* **フォームとドキュメント**
* **デジタルアセット**
* **Communities**
* **オンライン取引**

最後に、ユーザーはこれらのインフラストラクチャレベルおよびアプリケーションレベルの構築ブロックを使用して、独自のアプリケーションを構築することで、カスタマイズされたソリューションを作成できます。

AEM サーバーは **Java ベース**&#x200B;であり、Java のプラットフォームをサポートするほとんどのオペレーティングシステムで動作します。クライアントと AEM のやり取りはすべて、**web ブラウザー**&#x200B;経由で行います。

>[!NOTE]
>
>AEM 6.5 クイックスタートで使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### 典型的なデプロイメントシナリオ {#typical-deployment-scenarios}

AEM の用語では、「インスタンス」とはサーバー上で実行されている AEM のコピーを指します。一般的に、AEM のインストールには少なくとも 2 つのインスタンスが必要であり、通常は別々のコンピューターで実行されます。

* **オーサー**：コンテンツの作成、アップロードおよび編集や web サイトの管理に使用される AEM インスタンス。公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
* **公開**：公開の準備が整ったコンテンツを公開する AEM インスタンス。

インストールされるソフトウェアという点では、これらのインスタンスは同一です。その違いは設定のみです。さらに、ほとんどのインストールでは、次の Dispatcher を使用します。

* **Dispatcher**：AEM Dispatcher モジュールで補強された、静的 web サーバー（Apache httpd、Microsoft® IIS など）。パブリッシュインスタンスで生成された web ページをキャッシュして、パフォーマンスを向上します。

高度なオプションや詳細設定が多数ありますが、オーサー、パブリッシュおよび Dispatcher という基本的なパターンは、多くのデプロイメントの中核となります。ここではまず、比較的シンプルな設定に焦点を当てます。高度なデプロイメントオプションについては、後述します。

以下のセクションでは、両方のシナリオについて説明します。

* **オンプレミス**：AEM はユーザーの企業環境に配置され管理されます。

* **Managed Services - Adobe Experience Manager Cloud Manager**：AEM は、Adobe Managed Services によってデプロイおよび管理されます。

### オンプレミス {#on-premise}

企業環境のサーバーに AEM をインストールできます。一般的なインストールインスタンスには、開発環境、テスト環境、パブリッシュ環境が含まれます。AEM ソフトウェアをローカルにインストールする方法の基本的な詳細については、[はじめに](/help/sites-deploying/deploy.md#getting%20started)を参照してください。

一般的なオンプレミスデプロイメントについて詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)を参照してください。

### Cloud Manager を使用した Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services は、デジタルエクスペリエンスの管理のための完全なソリューションです。オンプレミスデプロイメントの制御、セキュリティ、カスタマイズのあらゆる利点を維持しながら、クラウドでエクスペリエンス配信ソリューションの利点を得ることができます。AEM Managed Services は、クラウドに導入されるだけでなく、ベストプラクティスを修得し、アドビのサポートを得ることにより、お客様はより迅速にサービスを開始できます。組織やビジネスユーザーは、最小限の時間で顧客を獲得し、市場シェアを拡大し、IT の負担を軽減しながら、革新的なマーケティングキャンペーンの作成に集中できます。

AEM Managed Services を使用すると、お客様は次のような利点を得ることができます。

**市場投入までの時間の短縮：** Adobe Managed Services の柔軟なクラウドインフラストラクチャにより、組織は成功するデジタルエクスペリエンスを迅速に計画し、立ち上げ、最適化することができます。アドビがクラウドアーキテクチャを管理するので、投資、ハードウェア、ソフトウェアを追加する必要がありません。アドビのカスタマーサクセスエンジニアが、AEM のアーキテクチャ、プロビジョニング、バックエンドアプリとの接続のカスタマイズ、実稼働に向けてのベストプラクティスに関する支援を提供します。

**より高い性能：** 99.5％、99.9％、99.95％、および 99.99％ の 4 つのサービス可用性オプションで、ビジネスに信頼性の高いデジタル体験を提供します。また、自動バックアップとマルチモードの障害復旧モデルにより、信頼性と危機管理性の確保をサポートします。

**最適化された IT コスト：**&#x200B;事前のガイダンスと専門知識により、組織は AEM のバージョンを常に最新の状態に保つことができます。AMS Enterprise／Basic の新規導入には、アドビのプラチナメンテナンスとサポートが自動的に含まれており、組織がミッションクリティカルなアプリケーションを維持するのに役立つ、技術的な専門知識と運用経験が提供されます。無料で使える基本的な Analytics または Target の機能は、特に分析とパーソナライゼーションのニーズが限られている中堅企業にさらなる価値を提供します。

**最高のセキュリティ：**&#x200B;カスタマーアプリケーションを、アクセスが制限された施設、ファイアウォールシステムの背後や、仮想プライベートクラウド内でホストすることで、エンタープライズクラスの物理、ネットワーク、およびデータのセキュリティを確保します。堅牢なデータストレージ暗号化、ウイルス対策、データ分離を備えた、シングルテナントの仮想マシンも含まれています。

**Cloud Manager**：Adobe Experience Manager Managed Services 製品の 1 つである Cloud Manager は、クラウドにおける Adobe Experience Manager の管理を組織内で行えるようにするセルフサービスポータルです。このサービスには最新の継続的インテグレーションと継続的デリバリー（CI／CD）のパイプラインが含まれており、IT チームや実装パートナーは、パフォーマンスやセキュリティを妥協することなく、カスタマイズや更新を迅速に配信できます。Cloud Manager をご利用いただけるのは、Adobe Managed Service のお客様のみです。

Cloud Manger とそのリソースについて詳しくは、[**Cloud Manager ユーザーガイド**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja)を参照してください。

## はじめに {#getting-started}

### 前提条件 {#prerequisites}

実稼動インスタンスは公式にサポートされている OS（[技術的要件](/help/sites-deploying/technical-requirements.md)を参照）を実行している専用のマシンで実行されますが、実際には Experience Manager サーバーは [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8) をサポートするすべてのシステムで動作します。

AEM に習熟したい場合や、AEM で開発する場合は、Apple OS X またはデスクトップ版の Microsoft® Windows または Linux® を実行しているローカルマシンにインストールされたインスタンスを使用するのが一般的です。

クライアント側では、AEM は、デスクトップとタブレットの両方のオペレーティングシステムにおけるすべてのブラウザー（**Microsoft® Edge**、**Internet Explorer** 11、**Chrome **51 以上****、**Firefox 47 以上**、**Safari** 8 以上）に対応します。詳細に関しては、[サポートされているクライアントプラットフォーム](/help/sites-deploying/technical-requirements.md#supported-client-platforms)を参照してください。

### ソフトウェアの入手 {#getting-the-software}

メンテナンスおよびサポートの有効な契約を締結済みのお客様には、コードが記載されているメール通知が届き、[**アドビライセンス web サイト**](https://licensing.adobe.com/)から AEM をダウンロードできます。ビジネスパートナーは、[**spphelp@adobe.com**](mailto:spphelp@adobe.com) 宛てにダウンロードアクセスをリクエストできます。

AEM ソフトウェアパッケージには、次の 2 つの形式があります。

* **cq-quickstart-6.5.0.jar：**&#x200B;スタンドアロンの実行可能 *jar* ファイル。実行するために必要なすべてのものが含まれています。

* **cq-quickstart-6.5.0.war：**&#x200B;サードパーティのアプリケーションサーバーにデプロイするための *war* ファイル。

次の節では、**スタンドアロンインストール**&#x200B;について説明します。アプリケーションサーバーへの AEM のインストールについて詳しくは、[アプリケーションサーバーのインストール](/help/sites-deploying/application-server-install.md)を参照してください。

### デフォルトのローカルインストール {#default-local-install}

1. ローカルマシンにインストールディレクトリを作成します。例：

   UNIX® のインストール先：**/opt/aem**

   Windows のインストール先： **`C:\Program Files\aem`**

   同様に、デスクトップ上のフォルダーにサンプルインスタンスをインストールするのが一般的です。いずれの場合も、通常この場所は次のように参照します。

   `<aem-install>`

   *ファイルディレクトリのパスには、US ASCII 文字のみを含めてください。*

1. このディレクトリに **jar** ファイルと **license** ファイルを配置します。

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   `license.properties` ファイルを指定しない場合、AEM の起動時にブラウザーに&#x200B;**ようこそ**&#x200B;画面が表示され、ここでライセンスキーを入力できます。アドビの有効なライセンスキーをお持ちでない場合は、依頼する必要があります。

1. GUI 環境でインスタンスを起動するには、**`cq-quickstart-6.5.0.jar`** ファイルをダブルクリックします。

   または、AEM はコマンドラインから起動することもできます。

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM では、jar ファイルを解凍し、自身をインストールして起動するまでに数分かかります。上記の手順では、次の結果になります。

* **AEM オーサー**&#x200B;インスタンスが、
* **localhost** 上の
* ポート **4502**

インスタンスにアクセスするには、ブラウザーで次の場所を指定します。

**`https://localhost:4502`**

オーサーインスタンスの結果は、上の **`localhost:4503`** パブリッシュインスタンスに接続するように自動的に設定されます&#x200B;**。**

### オーサーとパブリッシュのインストール {#author-and-publish-installs}

デフォルトのインストール（**上の**&#x200B;オーサー&#x200B;**`localhost:4502`**&#x200B;インスタンス）は、初めて起動する前に `jar` ファイルの名前を変更することによって変更できます。命名パターンは次のとおりです。

**`cq-<instance-type>-p<port-number>.jar`**

例えば、ファイル名を

**`cq-author-p4502.jar`**

に変更してから起動すると、オーサーインスタンスが **`localhost:4502`** 上で実行されます。

同様に、ファイル名を

**`cq-publish-p4503.jar`**

に変更してから起動すると、パブリッシュインスタンスが **`localhost:4503`** 上で実行されます。

これら 2 つのインスタンスを、例えば次の場所にインストールします。

`<aem-install>/author`および

**`<aem-install>/publish`**

インストールのカスタマイズについて詳しくは、以下を参照してください。

* [カスタムスタンドアロンインストール](/help/sites-deploying/custom-standalone-install.md)
* [実行モード](/help/sites-deploying/configure-runmodes.md)

### 展開されたインストールディレクトリ {#unpacked-install-directory}

quickstart jar を初めて起動すると、同じディレクトリの `crx-quickstart` という新しいサブディレクトリの下に解凍されます。最終的に、次のような構成になります。

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

インスタンスを UI からインストールした場合は、ブラウザーウィンドウが自動的に開き、デスクトップアプリケーションウィンドウも開いて、インスタンスのホストおよびポートと、オン／オフのスイッチが表示されます。

![起動画面](assets/screen_shot_.png)

>[!NOTE]
>
>symlinks を使用している場合は、[symlink に関する問題](https://helpx.adobe.com/jp/experience-manager/kb/changing-symlink.html)を確認してください。

### 起動と停止 {#starting-and-stopping}

AEM を初めて展開して起動した場合は、インストールディレクトリの jar ファイルをダブルクリックするだけでインスタンスが起動します。再インストールは行われません。

GUI からインスタンスを停止するには、デスクトップアプリケーションウィンドウの&#x200B;**オン／オフ**&#x200B;スイッチをクリックします。

AEM はコマンドラインからも停止および起動できます。インスタンスの初めてのインストールが完了している場合は、**コマンドラインスクリプト** は次の場所にあります。

**`<aem-install>/crx-quickstart/bin/`**

このフォルダーには、次の UNIX® bash シェルスクリプトが含まれています。

* **`start`**: インスタンスを開始
* `stop`: インスタンスを停止
* **`status`**: インスタンスのステータスを報告
* **`quickstart`**：必要に応じて開始情報の設定に使用

Windows 用に同等の **`bat`** ファイルもあります。詳しくは、以下を参照してください。

* [コマンドラインによる起動と停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM が起動し、Web ブラウザーが適切なページに自動的にリダイレクトされます。通常は、次のようなログインページが表示されます。

`https://localhost:4502/`

![ログイン画面](assets/screen_shot_2019-04-08at83533am.png)

ログインすると、AEM にアクセスできるようになります。詳しくは、ご自分の役割に応じて以下を参照してください。

* [オーサリング](/help/sites-authoring/first-steps.md)
* [管理](/help/sites-administering/home.md)
* [開発](/help/sites-developing/getting-started.md)
* [管理](/help/managing/best-practices.md)

## 高度なデプロイメント {#advanced-deployment}

上記のセクションは、基本的な AEM のインストールについて説明したものです。ただし、AEM の完全な実稼動システムをインストールする場合は、大幅に複雑になる可能性があります。高度なインストールについての詳しい説明は、次のサブページを参照してください。

* [技術要件](/help/sites-deploying/technical-requirements.md)
* [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)
* [カスタムスタンドアロンインストール](/help/sites-deploying/custom-standalone-install.md)
* [アプリケーションサーバーのインストール](/help/sites-deploying/application-server-install.md)
* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
* [コマンドラインによる起動と停止](/help/sites-deploying/command-line-start-and-stop.md)
* [設定](/help/sites-deploying/configuring.md)
* [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)
* [e コマース](/help/commerce/cif-classic/deploying/ecommerce.md)
* [設定方法に関する記事](/help/sites-deploying/ht-deploy.md)
* [Web コンソール](/help/sites-deploying/web-console.md)
* [レプリケーションのトラブルシューティング](/help/sites-deploying/troubleshoot-rep.md)
* [ベストプラクティス](/help/sites-deploying/best-practices.md)
* [Communities のデプロイ](/help/communities/deploy-communities.md)
* [AEM プラットフォームの概要](/help/sites-deploying/platform.md)
* [パフォーマンスガイドライン](/help/sites-deploying/performance-guidelines.md)
* [AEM Mobile 使用の手引き](/help/mobile/getting-started-aem-mobile.md)
* [AEM Screens とは](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=ja)
