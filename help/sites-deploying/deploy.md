---
title: デプロイとメンテナンス
description: AEM のインストールを開始する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 52%

---

# デプロイとメンテナンス {#deploying-and-maintaining}

このページでは、次の情報を確認できます。

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

これらの基本事項に慣れたら、次のサブページで、より高度で詳細な情報を確認できます。

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

Adobe Experience Managerは、商用 Web サイトや関連サービスを構築、管理、デプロイする Web ベースのクライアントサーバーシステムです。 インフラストラクチャレベルおよびアプリケーションレベルのいくつかの機能を組み合わせて単一の統合パッケージにします。

インフラストラクチャレベルで、AEM は次の機能を提供します。

* **Web アプリケーションサーバー**：AEM は、スタンドアロンモードで（統合 Jetty Web サーバーを含む）、またはサードパーティのアプリケーションサーバー内の web アプリケーションとしてデプロイできます。
* **Web アプリケーションフレームワーク**：AEM には Sling web アプリケーションフレームワークが組み込まれており、RESTful でコンテンツ指向 web アプリケーションを簡単に記述できます。
* **コンテンツリポジトリ**:AEMには、非構造化データおよび半構造化データ専用に設計された、Java™ Content Repository(JCR) という階層データベースが含まれています。 リポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレート、内部データも保存されます。

この基盤を基に、AEMは、次の管理のためのアプリケーションレベルの機能も提供します。

* **Web サイト**
* **モバイルアプリケーション**
* **デジタルパブリケーション**
* **Forms &amp; Documents**
* **デジタルアセット**
* **Communities**
* **オンライン取引**

最後に、ユーザーはこれらのインフラストラクチャレベルおよびアプリケーションレベルの構築ブロックを使用して、独自のアプリケーションを構築することで、カスタマイズされたソリューションを作成できます。

AEMサーバーは **Java ベース** およびは、そのプラットフォームをサポートするほとんどのオペレーティングシステムで動作します。 クライアントとAEMとのやり取りはすべて、 **web ブラウザー**.

>[!NOTE]
>
>アダプティブFormsの機能 (AEM 6.5 QuickStart で使用可能 ) は、調査と評価の目的でのみ設計されています。 アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### 典型的なデプロイメントシナリオ {#typical-deployment-scenarios}

AEMの用語では、「インスタンス」とは、サーバー上で実行されているAEMのコピーです。 通常、AEMのインストールには少なくとも 2 つのインスタンスが含まれ、通常は別々のコンピューターで実行されます。

* **オーサー**：コンテンツの作成、アップロードおよび編集や web サイトの管理に使用される AEM インスタンス。公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
* **公開**：公開の準備が整ったコンテンツを公開する AEM インスタンス。

インストールされるソフトウェアという点では、これらのインスタンスは同一です。その違いは設定のみです。さらに、ほとんどのインストールでは、Dispatcher を使用します。

* **Dispatcher**:AEM Dispatcher モジュールで拡張された静的 Web サーバー (Apache httpd、Microsoft® IIS など )。 パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

この設定には多くの高度なオプションと詳細がありますが、オーサー、パブリッシュ、Dispatcher の基本パターンは、ほとんどのデプロイメントの中核となっています。 まず、単純な設定に焦点を当ててみましょう。 高度なデプロイメントオプションに関する議論は以下のとおりです。

以下のセクションでは、両方のシナリオについて説明します。

* **オンプレミス**：AEM はユーザーの企業環境に配置され管理されます。

* **Managed Services - Adobe Experience Manager Cloud Manager**：AEM は、Adobe Managed Services によってデプロイおよび管理されます。

### オンプレミス {#on-premise}

企業環境のサーバーに AEM をインストールできます。一般的なインストールインスタンスには、開発、テスト、パブリッシュ環境が含まれます。 詳しくは、 [はじめに](/help/sites-deploying/deploy.md#getting%20started) AEMソフトウェアをローカルにインストールする方法の基本的な詳細。

一般的なオンプレミスデプロイメントの詳細については、 [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md).

### Cloud Manager を使用した Managed Services {#managed-services-using-cloud-manager}

AEM Managed Services は、デジタルエクスペリエンスの管理のための完全なソリューションです。オンプレミスデプロイメントの制御、セキュリティ、カスタマイズのメリットをすべて保持しながら、クラウドでのエクスペリエンス配信ソリューションのメリットを提供します。 AEM Managed Services は、クラウドに導入されるだけでなく、ベストプラクティスを修得し、アドビのサポートを得ることにより、お客様はより迅速にサービスを開始できます。組織やビジネスユーザーは、最小限の時間で顧客を獲得し、市場シェアを拡大し、IT の負担を軽減しながら、革新的なマーケティングキャンペーンの作成に集中できます。

AEM Managed Services を使用すると、お客様は次のような利点を得ることができます。

**市場投入までの時間の短縮：** AdobeManaged Servicesの柔軟なクラウドインフラストラクチャを使用して、組織は成功するデジタルエクスペリエンスを迅速に計画、立ち上げ、最適化できます。 アドビがクラウドアーキテクチャを管理するので、投資、ハードウェア、ソフトウェアを追加する必要がありません。アドビのカスタマーサクセスエンジニアが、AEM のアーキテクチャ、プロビジョニング、バックエンドアプリとの接続のカスタマイズ、実稼働に向けてのベストプラクティスに関する支援を提供します。

**より高い性能：** 99.5％、99.9％、99.95％、および 99.99％ の 4 つのサービス可用性オプションで、ビジネスに信頼性の高いデジタル体験を提供します。また、自動バックアップとマルチモードの災害復旧モデルを使用して、信頼性とコンティンジェンシー管理を確保できます。

**最適化された IT コスト：** プロアクティブなガイダンスと専門知識は、組織が最新バージョンのAEMを常に利用できるように支援します。 Adobeプラチナメンテナンスとサポートは、AMS Enterprise/Basic の新しい導入に自動的に組み込まれ、組織がミッションクリティカルなアプリケーションを維持するのに役立つ技術的な専門知識と運用経験を提供します。 無料で使える基本的な Analytics または Target の機能は、特に分析とパーソナライゼーションのニーズが限られている中堅企業にさらなる価値を提供します。

**最高のセキュリティ：**&#x200B;カスタマーアプリケーションを、アクセスが制限された施設、ファイアウォールシステムの背後や、仮想プライベートクラウド内でホストすることで、エンタープライズクラスの物理、ネットワーク、およびデータのセキュリティを確保します。堅牢なデータストレージ暗号化、ウイルス対策、データ分離を備えた、シングルテナントの仮想マシンも含まれています。

**Cloud Manager**：Adobe Experience Manager Managed Services 製品の 1 つである Cloud Manager は、クラウドにおける Adobe Experience Manager の管理を組織内で行えるようにするセルフサービスポータルです。このサービスには最新の継続的インテグレーションと継続的デリバリー（CI／CD）のパイプラインが含まれており、IT チームや実装パートナーは、パフォーマンスやセキュリティを妥協することなく、カスタマイズや更新を迅速に配信できます。Cloud Manager をご利用いただけるのは、Adobe Managed Service のお客様のみです。

Cloud Manager とそのリソースについて詳しくは、 [**Cloud Manager ユーザーガイド**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja).

## はじめに {#getting-started}

### 前提条件 {#prerequisites}

本番用インスタンスは、正式にサポートされている OS を実行する専用マシンで実行されます ( [技術要件](/help/sites-deploying/technical-requirements.md)) の場合、Experience Managerサーバーは、実際にはをサポートする任意のシステムで実行されます。 [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

慣習化を目的とし、AEMでの開発のために、Apple OS X またはMicrosoft® Windows または Linux®のデスクトップバージョンを実行するローカルマシンにインストールされたインスタンスを使用するのが一般的です。

クライアント側では、AEMはすべての最新のブラウザーで動作します (**Microsoft® Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47 以降， **Safari** 8 以降 ) をデスクトップとタブレットの両方のオペレーティングシステムで使用できます。 詳細に関しては、[サポートされているクライアントプラットフォーム](/help/sites-deploying/technical-requirements.md#supported-client-platforms)を参照してください。

### ソフトウェアの入手 {#getting-the-software}

有効なメンテナンスおよびサポート契約を締結しているお客様には、コードが記載された電子メール通知が届き、AEMを [**Adobeライセンス Web サイト**](https://licensing.adobe.com/). ビジネスパートナーは、からのダウンロードアクセスをリクエストできます。 [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

AEMソフトウェアパッケージは、次の 2 つの形式で使用できます。

* **cq-quickstart-6.5.0.jar:** スタンドアロンの実行可能ファイル *jar* 実行に必要なすべての情報を含むファイル。

* **cq-quickstart-6.5.0.war：**&#x200B;サードパーティのアプリケーションサーバーにデプロイするための *war* ファイル。

次の節では、 **スタンドアロンインストール**. アプリケーションサーバーへのAEMのインストールについて詳しくは、 [アプリケーションサーバーのインストール](/help/sites-deploying/application-server-install.md).

### デフォルトのローカルインストール {#default-local-install}

1. ローカルマシンにインストールディレクトリを作成します。例：

   UNIX®のインストール場所： **/opt/aem**

   Windows のインストール先： **`C:\Program Files\aem`**

   同様に、デスクトップ上のフォルダーにサンプルインスタンスをインストールするのが一般的です。いずれの場合も、Adobeはこの場所を一般的に次のように参照します。

   `<aem-install>`

   *ファイルディレクトリのパスは、US ASCII 文字のみで構成する必要があります。*

1. このディレクトリに **jar** ファイルと **license** ファイルを配置します。

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   次の項目を指定しない場合、 `license.properties` ファイルを使用して、AEMはブラウザーを **ようこそ** 起動時の画面。ライセンスキーを入力できます。 有効なライセンスキーがまだない場合は、Adobeに有効なライセンスキーをリクエストする必要があります。

1. GUI 環境でインスタンスを起動するには、 **`cq-quickstart-6.5.0.jar`** ファイル。

   または、AEM はコマンドラインから起動することもできます。

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEMは、jar ファイルを解凍し、自身をインストールして、起動するまでに数分かかります。 上記の手順では、次の結果になります。

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

を起動すると、オーサーインスタンスがで実行されます。 **`localhost:4502`**.

同様に、ファイル名を

**`cq-publish-p4503.jar`**

その結果、パブリッシュインスタンスがで実行されます。 **`localhost:4503`**.

これら 2 つのインスタンスを、例えば次の場所にインストールします。

`<aem-install>/author`および

**`<aem-install>/publish`**

インストールのカスタマイズについて詳しくは、以下を参照してください。

* [カスタムスタンドアロンインストール](/help/sites-deploying/custom-standalone-install.md)
* [実行モード](/help/sites-deploying/configure-runmodes.md)

### 展開されたインストールディレクトリ {#unpacked-install-directory}

quickstart jar を初めて起動すると、同じディレクトリ内の、という新しいサブディレクトリの下に自身をアンパックします。 `crx-quickstart`. 以下が必要です。

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

インスタンスが UI からインストールされた場合は、ブラウザーウィンドウが自動的に開き、デスクトップアプリケーションウィンドウも開き、インスタンスのホストとポート、オン/オフスイッチが表示されます。

![起動画面](assets/screen_shot_.png)

>[!NOTE]
>
>symlinks を使用している場合は、[symlink に関する問題](https://helpx.adobe.com/jp/experience-manager/kb/changing-symlink.html)を確認してください。

### 起動と停止 {#starting-and-stopping}

AEMが初めてパックを解除して起動したら、インストールディレクトリの jar ファイルをダブルクリックするだけでインスタンスが起動し、再インストールは行われません。

GUI からインスタンスを停止するには、 **オン/オフ** デスクトップアプリケーションウィンドウをオンにします。

また、コマンドラインからAEMを停止して起動することもできます。 インスタンスを初めてインストールした場合は、 **コマンドラインスクリプト** は次の場所にあります。

**`<aem-install>/crx-quickstart/bin/`**

このフォルダーには、次の UNIX® bash シェルスクリプトが含まれます。

* **`start`**: インスタンスを開始
* `stop`: インスタンスを停止
* **`status`**: インスタンスのステータスを報告
* **`quickstart`**：必要に応じて開始情報の設定に使用

Windows 用に同等の **`bat`** ファイルもあります。詳しくは、以下を参照してください。

* [コマンドラインによる起動と停止](/help/sites-deploying/command-line-start-and-stop.md)

AEM が起動し、Web ブラウザーが適切なページに自動的にリダイレクトされます。通常は、次のようなログインページが表示されます。

`https://localhost:4502/`

![ログイン画面](assets/screen_shot_2019-04-08at83533am.png)

ログイン後、AEMにアクセスできます。 詳しくは、役割に応じて、以下を参照してください。

* [オーサリング](/help/sites-authoring/home.md)
* [管理](/help/sites-administering/home.md)
* [開発](/help/sites-developing/home.md)
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
