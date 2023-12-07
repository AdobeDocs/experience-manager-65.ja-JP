---
title: パフォーマンスガイドライン
description: この記事では、AEM デプロイメントのパフォーマンスを最適化する方法に関する一般的なガイドラインを示します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 99%

---

# パフォーマンスガイドライン{#performance-guidelines}

このページでは、AEMデプロイメントのパフォーマンスを最適化する方法に関する一般的なガイドラインを示します。AEM を初めて使用する場合は、パフォーマンスガイドラインを読む前に、次のページを確認してください。

* [AEM の基本概念](/help/sites-deploying/deploy.md#basic-concepts)
* [AEM のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)
* [技術要件](/help/sites-deploying/technical-requirements.md)

以下に AEM で使用できるデプロイメントオプションを示します（すべてのオプションを表示するにはスクロールしてください）。

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>製品</strong></p> </td>
   <td><p><strong>トポロジ</strong></p> </td>
   <td><p><strong>オペレーティングシステム</strong></p> </td>
   <td><p><strong>アプリケーションサーバー</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>セキュリティ</strong></p> </td>
   <td><p><strong>マイクロカーネル</strong></p> </td>
   <td><p><strong>データストア</strong></p> </td>
   <td><p><strong>インデックス作成</strong></p> </td>
   <td><p><strong>Web サーバー</strong></p> </td>
   <td><p><strong>ブラウザー</strong></p> </td>
   <td><p><strong>Experience Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>非 HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>セグメント</p> </td>
   <td><p>プロパティ</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>ターゲット</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>パブリッシュ - HA</p> </td>
   <td><p>Solaris™</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM®</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>File</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analytics</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>オーサー - CS</p> </td>
   <td><p>Red Hat®</p> </td>
   <td><p>WebSphere®</p> </td>
   <td><p>HP</p> </td>
   <td><p>OAuth</p> </td>
   <td><p>RDB／Oracle</p> </td>
   <td><p>S3／Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>Firefox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>オーサー - オフロード</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB／DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>モバイル</p> </td>
   <td><p>オーサー - クラスター</p> </td>
   <td><p>IBM® AIX®</p> </td>
   <td><p>JBoss®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB／MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>対象読者</p> </td>
  </tr>
  <tr>
   <td><p>Multi-site</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB／SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Assets</p> </td>
  </tr>
  <tr>
   <td><p>コマース</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>アクティベーション</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>モバイル</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>スクリーン</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Doc Security</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Process Mgt</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>デスクトップアプリケーション</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>パフォーマンスガイドラインは主に AEM Sites に適用されます。

## パフォーマンスガイドラインを使用するタイミング {#when-to-use-the-performance-guidelines}

パフォーマンスガイドラインは次の状況で使用します。

* **初回のデプロイメント**：AEM Sites または Assets の初めてのデプロイを計画する場合は、使用可能なオプションを理解しておくことが重要です。特に、マイクロカーネル、ノードストアおよびデータストアを設定する場合（デフォルト設定と比較）。例えば、TarMK のデータストアのデフォルト設定をファイルデータストアに変更する場合などです。
* **新しいバージョンへのアップグレード**：新しいバージョンにアップグレードする場合は、実行中の環境と比較してパフォーマンスの違いを理解することが重要です。例えば、AEM 6.1 から 6.2 へ、または AEM 6.0 CRX2 から 6.2 OAK にアップグレードする場合などです。
* **応答時間が遅い**：選択したノードストアアーキテクチャが要件を満たしていない場合は、他のトポロジオプションと比較してパフォーマンスの違いを理解することが重要です。例えば、MongoMK の代わりに TarMK をデプロイしたり、Amazon S3 または Microsoft® Azure データストアの代わりにファイルデータストアを使用したりする場合です。
* **オーサーの追加**：推奨 TarMK トポロジがパフォーマンス要件を満たさず、オーサーノードのサイズ拡張が使用可能な最大容量に達した場合は、パフォーマンスの違いを理解する必要があります。その際、3 つ以上のオーサーノードで MongoMK を使用する場合と比較します。例えば、TarMK の代わりに MongoMK をデプロイする場合などです。
* **コンテンツの追加**：推奨されるデータストアアーキテクチャが要件を満たしていない場合は、他のデータストアオプションと比較してパフォーマンスの違いを理解することが重要です。 例えば、ファイルデータストアの代わりに Amazon S3 または Microsoft® Azure データストアを使用する場合などです。

## はじめに {#introduction}

この章では、AEM のアーキテクチャと AEM の最も重要なコンポーネントの大まかな概要を説明します。また、開発ガイドラインを示し、TarMK および MongoMK ベンチマークテストで使用されるテストシナリオについて説明します。

### AEM のプラットフォーム {#the-aem-platform}

AEM のプラットフォームは、次のコンポーネントで構成されています。

![chlimage_1](assets/chlimage_1a.png)

AEM のプラットフォームについて詳しくは、[AEM とは](/help/sites-deploying/deploy.md#what-is-aem)を参照してください。

### AEM のアーキテクチャ {#the-aem-architecture}

AEM のデプロイメントに重要な 3 つのビルディングブロックがあります。**オーサーインスタンス**&#x200B;は、コンテンツ作成者、編集者、および承認者がコンテンツの作成およびレビューを行うために使用します。コンテンツが承認されると、**パブリッシュインスタンス**&#x200B;という名前の 2 番目のインスタンスタイプに公開され、エンドユーザーはここからコンテンツにアクセスします。3 番目のビルディングブロックは **Dispatcher** で、これはキャッシュおよび URL フィルタリングを処理するモジュールとして、web サーバーにインストールされます。AEM のアーキテクチャについて詳しくは、[典型的なデプロイメントシナリオ](/help/sites-deploying/deploy.md#typical-deployment-scenarios)を参照してください。

![chlimage_1-1](assets/chlimage_1-1a.png)

### マイクロカーネル {#micro-kernels}

マイクロカーネルは AEM で永続性マネージャーとして機能します。AEM で使用されるマイクロカーネルには、TarMK、MongoDB、リレーショナルデータベース（制限付きサポート）の 3 つのタイプがあります。インスタンスの目的と検討しているデプロイメントタイプによって、ニーズに合うマイクロカーネルを選択します。マイクロカーネルについて詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)のページを参照してください。

![chlimage_1-2](assets/chlimage_1-2a.png)

### ノードストア {#nodestore}

AEM では、バイナリデータをコンテンツノードとは別に格納できます。バイナリデータの格納先は&#x200B;**データストア**&#x200B;と呼ばれます。一方、コンテンツノードおよびプロパティの格納先は&#x200B;**ノードストア**&#x200B;と呼ばれます。

>[!NOTE]
>
>アドビでは、AEM オーサーインスタンスとパブリッシュインスタンスの両方について、顧客がデフォルトで使用する永続性技術として TarMK を推奨します。

>[!CAUTION]
>
>リレーショナルデータベースマイクロカーネルは制限付きでサポートされます。このタイプのマイクロカーネルを使用する前に、[アドビカスタマーケア](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support)にお問い合わせください。

![chlimage_1-3](assets/chlimage_1-3a.png)

### データストア {#data-store}

多数のバイナリを処理する場合は、最大限のパフォーマンスを確保するために、デフォルトのノードストアではなく外部のデータストアを使用することをお勧めします。例えば、プロジェクトで多数のメディアアセットが必要な場合は、それらをファイルデータストアまたは Azure／S3 データストアに格納すると、MongoDB 内に直接格納する場合よりも迅速にアセットにアクセスできます。

使用可能な設定オプションについて詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

>[!NOTE]
>
>アドビでは、Adobe Managed Services を使用して Azure または Amazon Web Services（AWS）に AEM をデプロイするオプションを選択することをお勧めします。お客様は、これらのクラウドコンピューティング環境で AEM をデプロイおよび運用する経験とスキルを持つチームのメリットを享受できます。[Adobe Managed Services に関するドキュメント](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t)を参照してください。
>
>Adobe Managed Services の外部で Azure または AWS に AEM をデプロイする場合のレコメンデーションは、クラウドプロバイダーと直接共同作業することです。または、任意のクラウド環境での AEM のデプロイをサポートするアドビのパートナーと協力することもできます。選択したクラウドプロバイダーまたはパートナーは、アーキテクチャのサイズ仕様、設計、および実装を担当し、顧客独自のパフォーマンス、負荷、スケーラビリティおよびセキュリティの要件が満たされるように支援します。
>
>>[技術要件](/help/sites-deploying/technical-requirements.md#supported-platforms)ページも参照してください。

### 検索 {#search-features}

この節では AEM で使用されるカスタムインデックスプロバイダーを示します。インデックス作成について詳しくは、[Oak クエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。

>[!NOTE]
>
>アドビでは、ほとんどのデプロイメントで Lucene Index を使用することを推奨します。Solr は、特殊で複雑なデプロイメントでスケーラビリティを確保するためにのみ使用してください。

![chlimage_1-4](assets/chlimage_1-4a.png)

### 開発のガイドライン {#development-guidelines}

AEM は&#x200B;**パフォーマンスとスケーラビリティ**&#x200B;を目標として開発してください。指針にすることができるベストプラクティスを次に示します。

**DO**

* 表示、ロジック、およびコンテンツを分離する
* 既存の AEM API（Sling など）およびツール（レプリケーションなど）を使用する
* 実際のコンテンツのコンテキストで開発する
* キャッシュ可能性が最適になるように開発する
* 保存の回数を最小限に抑える（一時的なワークフローなどを使用）
* すべての HTTP エンドポイントが RESTful であるようにする
* JCR 監視の範囲を制限
* 非同期スレッドに留意する

**DON&#39;T**

* 可能な場合は、JCR API を直接使用しない
* /libs を変更せずに、オーバーレイを使用する
* 可能な限りクエリを使用しない
* Java™ コードで OSGi サービスを取得する場合は、Sling Binding を使用せずに以下を使用してください。

   * DS コンポーネントの @Reference
   * Sling Model の @Inject
   * Sightly Use クラスの sling.getService()
   * JSP の sling.getService()
   * ServiceTracker
   * OSGi サービスレジストリへの直接アクセス

AEM での開発について詳しくは、[開発の基本](/help/sites-developing/the-basics.md)を参照してください。その他のベストプラクティスについては、[開発のベストプラクティス](/help/sites-developing/best-practices.md)を参照してください。

### ベンチマークのシナリオ {#benchmark-scenarios}

>[!NOTE]
>
>このページに表示されているすべてのベンチマークテストは、ラボ設定で行われています。

以下で説明するテストシナリオは、TarMK、MongoMk、および TarMK と MongoMk の章のベンチマークの節で使用されています。特定のベンチマークテストで使用されているシナリオを確認するには、[技術仕様](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark)表のシナリオフィールドを参照してください。

**単一製品シナリオ**

AEM Assets：

* ユーザーインタラクション：アセットを参照／アセットを検索／アセットをダウンロード／アセットメタデータを読み取り／アセットメタデータを更新／アセットをアップロード／アセットのアップロードワークフローを実行
* 実行モード：同時ユーザー、ユーザーごとの単一インタラクション

**混合製品シナリオ**

AEM Sites + Assets：

* Sites ユーザーのインタラクション：記事ページを読み取り／ページを読み取り／パラグラフの作成／パラグラフを編集／コンテンツページを作成／コンテンツページをアクティブ化／作成者検索
* Assets ユーザーのインタラクション：アセットを参照／アセットを検索／アセットをダウンロード／アセットメタデータを読み取り／アセットメタデータを更新／アセットをアップロード／アセットのアップロードワークフローを実行
* 実行モード：同時ユーザー、ユーザーごとの混合インタラクション

**垂直方向のユースケースのシナリオ**

メディア：

* `Read Article Page (27.4%), Read Page (10.9%), Create Session (2.6%), Activate Content Page (1.7%), Create Content Page (0.4%), Create Paragraph (4.3%), Edit Paragraph (0.9%), Image Component (0.9%), Browse Assets (20%), Read Asset Metadata (8.5%), Download Asset (4.2%), Search Asset (0.2%), Update Asset Metadata (2.4%), Upload Asset (1.2%), Browse Project (4.9%), Read Project (6.6%), Project Add Asset (1.2%), Project Add Site (1.2%), Create Project (0.1%), Author Search (0.4%)`
* 実行モード：同時ユーザー、ユーザーごとの混合インタラクション

## TarMK {#tarmk}

この章では、最小のアーキテクチャ要件および設定を指定した TarMK の一般的なパフォーマンスガイドラインを示します。さらに明確にするためにベンチマークテストも示します。

アドビでは、すべてのデプロイメントシナリオにおいて、AEM オーサーインスタンスとパブリッシュインスタンスの両方に対し TarMK をデフォルトの優先使用する技術とすることを顧客に推奨します。

TarMK について詳しくは、[デプロイメントのシナリオ](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)および [Tar ストレージ](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage)を参照してください。

### TarMK 最小アーキテクチャガイドライン {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>以下に示す最小アーキテクチャガイドラインは、実稼動環境および高トラフィックサイト向けです。これらのガイドラインは、AEM を実行するための[最小仕様](/help/sites-deploying/technical-requirements.md#prerequisites)では&#x200B;**ありません**。

TarMK の使用時に優れたパフォーマンスを実現するには、次のアーキテクチャから開始してください。

* 1 つのオーサーインスタンス
* 2 つのパブリッシュインスタンス
* 2 つの Dispatcher

以下に AEM Sites および AEM Assets でのアーキテクチャガイドラインを示します。

>[!NOTE]
>
>ファイルデータストアを共有する場合は、バイナリなしのレプリケーションを&#x200B;**オン**&#x200B;にする必要があります。

**AEM Sites での Tar アーキテクチャガイドライン**

![chlimage_1-5](assets/chlimage_1-5a.png)

**AEM Assets での Tar アーキテクチャガイドライン**

![chlimage_1-6](assets/chlimage_1-6a.png)

### TarMK 設定ガイドライン {#tarmk-settings-guideline}

パフォーマンスを高めるには、次に示す設定ガイドラインに従う必要があります。設定を変更する手順については、[このページを参照してください](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ja)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>パラメーター</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>Sling ジョブキュー</td>
   <td><code>queue.maxparallel</code></td>
   <td>CPU コア数の半分の値に設定します。 </td>
   <td>デフォルトでは、ジョブキューあたりの同時スレッド数は、CPU コア数と同じです。</td>
  </tr>
  <tr>
   <td>Granite 一時ワークフローキュー</td>
   <td><code>Max Parallel</code></td>
   <td>CPU コア数の半分の値に設定します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM パラメーター</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>大規模なクエリによってシステムが過負荷になることを防ぐため、AEM の起動スクリプトにこれらの JVM パラメーターを追加します。</td>
  </tr>
  <tr>
   <td>Lucene インデックス設定</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Enabled</p> <p>Enabled</p> <p>Enabled</p> </td>
   <td>利用可能なパラメーターについて詳しくは、<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">このページ</a>を参照してください。</td>
  </tr>
  <tr>
   <td>データストア = S3 データストア</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576（1 MB）以下</p> <p>最大ヒープサイズの 2～10％</p> </td>
   <td><a href="/help/sites-deploying/data-store-config.md#data-store-configurations">データストアの設定</a>も参照してください。</td>
  </tr>
  <tr>
   <td>DAM アセットの更新ワークフロー</td>
   <td><code>Transient Workflow</code></td>
   <td>チェック済み</td>
   <td>このワークフローではアセットの更新を管理します.</td>
  </tr>
  <tr>
   <td>DAM メタデータの書き戻し</td>
   <td><code>Transient Workflow</code></td>
   <td>チェック済み</td>
   <td>このワークフローでは、元のバイナリへの XMP の書き戻しを管理し、JCR で最終変更日を設定します。</td>
  </tr>
 </tbody>
</table>

### TarMK パフォーマンスベンチマーク {#tarmk-performance-benchmark}

#### 技術仕様 {#technical-specifications}

以下の仕様に基づいてベンチマークテストが実行されました。

| | **オーサーノード** |
|---|---|
| サーバー | ベアメタルハードウェア（HP） |
| オペレーティングシステム | Red Hat® Linux® |
| CPU／コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア |
| RAM | 32 GB |
| ディスク | 磁気 |
| Java™ | Oracle JRE バージョン 8 |
| JVM ヒープ | 16 GB |
| 製品 | AEM 6.2 |
| ノードストア | TarMK |
| データストア | ファイル DS |
| シナリオ | 単一の製品：アセット／30 個の同時スレッド |

#### パフォーマンスベンチマーク結果 {#performance-benchmark-results}

>[!NOTE]
>
>以下に示す数値は、ベースラインとして 1 に正規化されており、実際のスループットの数値ではありません。

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

TarMK よりも MongoMK 永続性バックエンドを選択する主な理由は、インスタンスを水平方向にスケールできることです。つまり、常に 2 つ以上のアクティブなオーサーインスタンスが動作しており、MongoDB が永続性ストレージシステムとして使用されます。複数のオーサーインスタンスを実行する必要があるのは、通常、1 台のサーバーの CPU とメモリの処理能力では、同時に実行されるすべてのオーサリングアクティビティをサポートできないからです。

TarMK について詳しくは、[デプロイメントのシナリオ](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)および [Mongo ストレージ](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage)を参照してください。

### MongoMK 最小アーキテクチャガイドライン {#mongomk-minimum-architecture-guidelines}

MongoMK の使用時に優れたパフォーマンスを実現するには、次のアーキテクチャを出発点にする必要があります。

* 3 つのオーサーインスタンス
* 2 つのパブリッシュインスタンス
* 3 つの MongoDB インスタンス
* 2 つの Dispatcher

>[!NOTE]
>
>実稼動環境では、MongoDB は常に、プライマリと 2 つのセカンダリを持つレプリカセットとして使用されます。プライマリで読み取りと書き込みが行われ、セカンダリでは読み取りが行われることがあります。ストレージを利用できない場合、セカンダリの 1 つをアービターに置き換えることができますが、MongoDB レプリカセットは常に奇数のインスタンスで構成する必要があります。

>[!NOTE]
>
>ファイルデータストアを共有する場合は、バイナリなしのレプリケーションを&#x200B;**オン**&#x200B;にする必要があります。

![chlimage_1-9](assets/chlimage_1-9a.png)

### MongoMK 設定ガイドライン {#mongomk-settings-guidelines}

パフォーマンスを高めるには、次に示す設定ガイドラインに従う必要があります。設定を変更する手順については、[このページを参照してください](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ja)。

<table>
 <tbody>
  <tr>
   <td><strong>設定</strong></td>
   <td><strong>パラメーター</strong></td>
   <td><strong>値（デフォルト）</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>Sling ジョブキュー</td>
   <td><code>queue.maxparallel</code></td>
   <td>CPU コア数の半分の値に設定します。 </td>
   <td>デフォルトでは、ジョブキューあたりの同時スレッド数は、CPU コア数と同じです。</td>
  </tr>
  <tr>
   <td>Granite 一時ワークフローキュー</td>
   <td><code>Max Parallel</code></td>
   <td>CPU コア数の半分の値に設定します。</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM パラメーター</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>大規模なクエリによってシステムが過負荷になることを防ぐため、AEM の起動スクリプトにこれらの JVM パラメーターを追加します。</td>
  </tr>
  <tr>
   <td>Lucene インデックス設定</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Enabled</p> <p>Enabled</p> <p>Enabled</p> </td>
   <td>使用可能なパラメーターについて詳しくは、<a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">このページ</a>を参照してください。</td>
  </tr>
  <tr>
   <td>データストア = S3 データストア</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576（1 MB）以下</p> <p>最大ヒープサイズの 2～10％</p> </td>
   <td><a href="/help/sites-deploying/data-store-config.md#data-store-configurations">データストアの設定</a>も参照してください。</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35（25）</p> <p>20（10）</p> <p>30（5）</p> <p>10（3）</p> <p>4（4）</p> <p>。/cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>キャッシュのデフォルトサイズは 256 MB に設定されています。</p> <p>キャッシュの無効化の実行にかかる時間に影響します。</p> </td>
  </tr>
  <tr>
   <td>oak-observation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>最小および最大 = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### MongoMK パフォーマンスベンチマーク {#mongomk-performance-benchmark}

### 技術仕様 {#technical-specifications-1}

以下の仕様に基づいてベンチマークテストが実行されました。

| | **オーサーノード** | **MongoDB ノード** |
|---|---|---|
| サーバー | ベアメタルハードウェア（HP） | ベアメタルハードウェア（HP） |
| オペレーティングシステム | Red Hat® Linux® | Red Hat® Linux® |
| CPU／コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア | Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア |
| RAM | 32 GB | 32 GB |
| ディスク | 磁気 - 1,000 IOPS を超える | 磁気 - 1,000 IOPS を超える |
| Java™ | Oracle JRE バージョン 8 | 該当なし |
| JVM ヒープ | 16 GB | 該当なし |
| 製品 | AEM 6.2 | MongoDB 3.2 WiredTiger |
| ノードストア | MongoMK | 該当なし |
| データストア | ファイル DS | 該当なし |
| シナリオ | 単一の製品：アセット／30 個の同時スレッド | 単一の製品：アセット／30 個の同時スレッド |

### パフォーマンスベンチマーク結果 {#performance-benchmark-results-1}

>[!NOTE]
>
>以下に示す数値は、ベースラインとして 1 に正規化されており、実際のスループットの数値ではありません。

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK と MongoMK {#tarmk-vs-mongomk}

この 2 つのうちのどちらかを選択する際に考慮すべき基本ルールは、TarMK はパフォーマンス重視で設計されており、MongoMK はスケーラビリティ重視で使用されているということです。アドビでは、AEM オーサーインスタンスと AEM パブリッシュインスタンスの両方について、すべてのデプロイメントシナリオで顧客がデフォルトで使用する永続性技術として TarMK をお勧めします。

TarMK よりも MongoMK 永続性バックエンドを選択する主な理由は、インスタンスを水平方向にスケールできることです。つまり、常に 2 つ以上のアクティブなオーサーインスタンスが動作しており、MongoDB が永続性ストレージシステムとして使用されます。複数のオーサーインスタンスを実行する必要があるのは、通常、1 台のサーバーの CPU とメモリの処理能力では、同時に実行されるすべてのオーサリングアクティビティをサポートできないからです。

TarMK と MongoMK の比較について詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use)を参照してください。

### TarMK と MongoMk のガイドライン {#tarmk-vs-mongomk-guidelines}

**TarMK の利点**

* コンテンツ管理アプリケーション専用に設計されています。
* 常にファイルの一貫性が保たれ、任意のファイルベースのバックアップツールを使用してファイルをバックアップできます。
* フェイルオーバーメカニズムを備えています。詳しくは、[コールドスタンバイ](/help/sites-deploying/tarmk-cold-standby.md)を参照してください。
* 運用上のオーバーヘッドを最小限に抑えながら、パフォーマンスと信頼性の高いデータストレージを提供します。
* TCO（総保有コスト）を削減します。

**MongoMK を選択する基準**

* 1 日に接続する名前付きユーザーの数：数千人以上
* 同時ユーザーの数：数百人以上
* 1 日に取り込むアセットのボリューム：数十万件以上
* 1 日あたりのページ編集のボリューム：数十万件以上
* 1 日あたりの検索件数：数万件以上

### TarMK と MongoMK のベンチマーク比較 {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>以下に示す数値はベースラインとして 1 に正規化されており、実際のスループット数値ではありません。

### シナリオ 1 技術仕様 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>OAK オーサーノード</strong></td>
   <td><strong>MongoDB ノード</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>サーバー</td>
   <td>ベアメタルハードウェア（HP）</td>
   <td>ベアメタルハードウェア（HP）</td>
   <td> </td>
  </tr>
  <tr>
   <td>オペレーティングシステム</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU／コア</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2.40GHz、8 コア</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>ディスク</td>
   <td>磁気 - 1,000 IOPS を超える</td>
   <td>磁気 - 1,000 IOPS を超える</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE バージョン 8</td>
   <td>該当なし</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM ヒープ 16 GB</td>
   <td>16 GB</td>
   <td>該当なし</td>
   <td> </td>
  </tr>
  <tr>
   <td>製品 </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>ノードストア</td>
   <td>TarMK または MongoMK</td>
   <td>該当なし</td>
   <td> </td>
  </tr>
  <tr>
   <td>データストア</td>
   <td>ファイル DS </td>
   <td>該当なし</td>
   <td> </td>
  </tr>
  <tr>
   <td>シナリオ</td>
   <td><p><br /> 単一の製品：Assets／実行あたり 30 個の同時スレッド</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### シナリオ 1 パフォーマンスベンチマークの結果 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### シナリオ 2 技術仕様 {#scenario-technical-specifications-1}

>[!NOTE]
>
>1 つの TarMK システムを使用した場合と同じ数のオーサーを MongoDB で有効にするには、2 つの AEM ノードを含むクラスターが必要です。4 ノードの MongoDB クラスターで処理できるオーサーの数は、1 つの TarMK インスタンスの 1.8 倍です。8 ノードの MongoDB クラスターで処理できるオーサーの数は、1 つの TarMK インスタンスの 2.3 倍です。

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>TarMK オーサーノード</strong></td>
   <td><strong>MongoMK オーサーノード</strong></td>
   <td><strong>MongoDB ノード</strong></td>
  </tr>
  <tr>
   <td>サーバー</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>オペレーティングシステム</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
  </tr>
  <tr>
   <td>CPU／コア</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60 GB</td>
   <td>60 GB</td>
   <td>60 GB</td>
  </tr>
  <tr>
   <td>ディスク</td>
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
   <td>SSD - 10k IOPS</td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE バージョン 8</td>
   <td><br /> Oracle JRE バージョン 8</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>JVM ヒープ 16 GB</td>
   <td>30 GB</td>
   <td>30 GB</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>製品 </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>ノードストア</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> 該当なし</td>
  </tr>
  <tr>
   <td>データストア</td>
   <td>ファイル DS </td>
   <td><br /> ファイル DS</td>
   <td><br /> 該当なし</td>
  </tr>
  <tr>
   <td>シナリオ</td>
   <td><p><br /> <br /> 垂直方向の使用例：メディア／2000 の同時スレッド</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### シナリオ 2 パフォーマンスベンチマークの結果 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### AEM Sites および AEM Assets のアーキテクチャスケーラビリティのガイドライン {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## パフォーマンスガイドラインの概要  {#summary-of-performance-guidelines}

このページに示されているガイドラインの概要は次の通りです。

* **ファイルデータストアを使用する TarMK** - 大部分の顧客に対する推奨アーキテクチャ：

   * 最小トポロジ：1 つのオーサーインスタンス、2 つのパブリッシュインスタンス、2 つの Dispatcher
   * ファイルデータストアを共有する場合は、バイナリレスレプリケーションを有効にします

* **ファイルデータストアを使用する MongoMK** - オーサー層の水平方向のスケーラビリティのための推奨アーキテクチャ：

   * 最小トポロジ：3 つのオーサーインスタンス、3 つの MongoDB インスタンス、2 つのパブリッシュインスタンス、2 つの Dispatcher
   * ファイルデータストアを共有する場合は、バイナリレスレプリケーションを有効にします

* **ノードストア** - ネットワーク接続ストレージ（NAS）ではなくローカルディスクに格納
* **Amazon S3** を使用する場合：

   * Amazon S3 データストアは、オーサー層とパブリッシュ層の間で共有されます
   * バイナリレスレプリケーションを有効にする必要があります
   * データストアのガベージコレクションを使用するには、最初にすべてのオーサーノードとパブリッシュノードで実行してから、オーサーノードでもう一度実行する必要があります

* **標準提供のインデックスに加えて、カスタムインデックスを作成する必要があります** - 最も一般的な検索に基づく

   * カスタムインデックスには Lucene インデックスを使用する必要があります

* **ワークフローをカスタマイズすると、パフォーマンスを大幅に改善できます** - 「アセットを更新」ワークフローのビデオ手順を削除したり、使用されていないリスナーを無効化したりします。

詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)のページも参照してください。
