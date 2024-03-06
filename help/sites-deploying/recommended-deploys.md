---
title: 推奨されるデプロイメント
description: この記事では、AEMで推奨されるトポロジについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 36%

---

# 推奨されるデプロイメント{#recommended-deployments}

>[!NOTE]
>
>このページでは、AEM の推奨されるトポロジについて説明します。クラスター化機能およびその設定方法について詳しくは、[Apache Sling Discovery API のドキュメント](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)を参照してください。

AEM 6.2 以降、MicroKernels は永続性マネージャーとして機能します。ニーズに合わせた MicroKernel の選択は、インスタンスの目的と検討しているデプロイメントタイプによって決まります。

次の例は、最も一般的なAEMの設定で推奨される使用例を示しています。

## デプロイメントシナリオ {#deployment-scenarios}

### 単一の TarMK インスタンス {#single-tarmk-instance}

このシナリオでは、1 つの TarMK インスタンスが 1 つのサーバーで実行されます。

**これは、オーサーインスタンスのデフォルトのデプロイメントです。**

![chlimage_1-15](assets/chlimage_1-15.png)

メリット：

* シンプル
* メンテナンスが容易
* 優れたパフォーマンス

デメリットは次のとおりです。

* サーバー容量の制限を超える拡張性がない
* フェイルオーバー機能はない

### TarMK コールドスタンバイ {#tarmk-cold-standby}

1 つの TarMK インスタンスがプライマリインスタンスとして機能します。 プライマリからのリポジトリは、スタンバイフェイルオーバーシステムにレプリケートされます。

完全なリポジトリが常にフェイルオーバーサーバーにレプリケートされるので、コールドスタンバイメカニズムをバックアップとして使用することもできます。 フェールオーバーサーバーはコールドスタンバイモードで動作しています。つまり、インスタンスの HttpReceiver のみが実行されています。

![chlimage_1-16](assets/chlimage_1-16.png)

メリット：

* シンプルさ
* 保守性
* パフォーマンス
* フェイルオーバー

デメリットは次のとおりです。

* サーバー容量の制限を超える拡張性がない
* 1 台のサーバがほとんどの場合アイドル状態です
* フェールオーバーは自動ではありません。 フェイルオーバーシステムが要求の処理を開始する前に、外部から検出する必要があります。

>[!NOTE]
>
>TarMK コールドスタンバイを使用した AEM の設定方法について詳しくは、[この](/help/sites-deploying/tarmk-cold-standby.md)記事を参照してください。

>[!NOTE]
>
>この TarMK の例のコールドスタンバイデプロイメントでは、フェイルオーバーサーバーに定期的にレプリケートされるので、プライマリインスタンスとスタンバイインスタンスの両方が別々にライセンスされている必要があります。ライセンスの詳細については、 [Adobeの一般ライセンス条項](https://www.adobe.com/jp/legal/terms/enterprise-licensing.html).

### TarMK ファーム {#tarmk-farm}

複数の Oak インスタンスは、それぞれ 1 つの TarMK インスタンスで実行されます。 TarMK リポジトリは独立しており、同期を維持する必要があります。

リポジトリの同期を維持することで、オーサーサーバーが各ファームメンバーに同じコンテンツを公開していることがわかります。 詳しくは、 [レプリケーション](/help/sites-deploying/replication.md).

AEM Communitiesの場合、ユーザー生成コンテンツ (UGC) はレプリケートされません。 TarMK ファームでの UGC のサポートについて詳しくは、「[AEM Communities に関する考慮事項](#considerations-for-aem-communities)」を参照してください。

**これは、パブリッシュ環境のデフォルトのデプロイメントです。**

![chlimage_1-17](assets/chlimage_1-17.png)

メリット：

* パフォーマンス
* 読み取りアクセスの拡張性
* フェイルオーバー

### 単一のデータセンターでの高可用性を実現する MongoMK フェイルオーバーを備えた Oak クラスタ {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

このアプローチは、1 つのデータセンター内の MongoDB レプリカセットに複数の Oak インスタンスがアクセスし、AEMオーサー環境のアクティブ — アクティブクラスターが作成されることを意味します。 MongoDB のレプリカセットは、ハードウェアまたはネットワークの障害が発生した場合に高い可用性と冗長性を提供するために使用されます。

![chlimage_1-18](assets/chlimage_1-18.png)

メリット：

* 新しいAEMオーサーインスタンスで水平方向に拡大・縮小可能
* データ層の高可用性、冗長性、自動フェイルオーバー

デメリットは次のとおりです。

* 一部のシナリオでは、TarMK よりもパフォーマンスが低くなる場合があります

### 複数のデータセンターでの MongoMK フェイルオーバーを備えた Oak クラスター {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

このアプローチは、複数の Oak インスタンスが複数のデータセンターをまたいで MongoDB レプリカセットにアクセスし、AEMオーサー環境のアクティブ — アクティブクラスターを作成することを意味します。 MongoDB のレプリケーションでは、複数のデータセンターを使用する場合にも同じ高可用性と冗長性を提供しますが、さらにデータセンターの停止に対処する機能も追加されました。

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

メリット：

* 新しいAEMオーサーインスタンスで水平方向に拡大・縮小可能
* データ層の高可用性、冗長性、自動フェイルオーバー（データセンターの停止を含む）

>[!NOTE]
>
>上の図では、データセンター 2 の AEM サーバーとデータセンター 1 の MongoDB プライマリノードとのネットワーク遅延が、[ここ](/help/sites-deploying/aem-with-mongodb.md#checklists)に記載されている要件よりも大きいと仮定して、AEM サーバー 3 と AEM サーバー 4 のステータスが非アクティブになっています。例えば、可用性ゾーンの使用などにより、最大遅延が要件に反しない場合は、データセンター 2 の AEM サーバーもアクティブになることができ、結果として、複数のデータセンターにまたがるアクティブ-アクティブ構成の AEM クラスターとなります。

>[!NOTE]
>
>この節で説明した MongoDB アーキテクチャの概念について詳しくは、[MongoDB の レプリケーションに関するドキュメント](https://docs.mongodb.org/manual/replication/)を参照してください。

## マイクロカーネル：使用するもの {#microkernels-which-one-to-use}

利用可能な 2 つのマイクロカーネルの間で選択する際に考慮する必要がある基本的なルールは、TarMK はパフォーマンスを目的として設計されているのに対し、MongoMK はスケーラビリティに使用されている点です。

これらの決定マトリックスを使用して、要件に最適なデプロイメントのタイプを決定できます。

Adobeでは、以下の使用例を除き、AEMオーサーインスタンスとパブリッシュインスタンスの両方について、すべてのデプロイメントシナリオで顧客が使用するデフォルトの永続性テクノロジーを TarMK にすることを強くお勧めします。

### オーサーインスタンスで TarMK よりもAEM MongoMK を選択する際の例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

TarMK よりも MongoMK 永続性バックエンドを選択する主な理由は、インスタンスを水平方向にスケールできることです。つまり、2 つ以上のアクティブなオーサーインスタンスが常に実行され、MongoDB を永続性ストレージシステムとして使用します。 複数のオーサーインスタンスを実行する必要があるのは、通常、1 台のサーバーの CPU とメモリの処理能力では、同時に実行されるすべてのオーサリングアクティビティをサポートできないからです。

新しいサイトが実稼働した後に、正確な同時実行モデルがどのようになるかを予測することは、ほとんど不可能です。 したがって、Adobeでは、MongoMK と 2 つ以上のオーサーアクティブノードを使用するかどうかを評価する際に、次の条件を考慮することをお勧めします。

1. 1 日に接続する名前付きユーザー数（数千人以上）
1. 同時ユーザー数（数百人以上）
1. 1 日あたりのアセット収集のボリューム（数十万件以上）
1. 1 日あたりのページ編集のボリューム（数十万件以上）（Multi Site Manager やニュースフィードの収集などによる自動化された更新を含む）
1. 1 日あたりの検索のボリューム（数万件以上）

>[!NOTE]
>
>Tough Day は、デプロイされたハードウェア構成のコンテキストにおけるお客様のアプリケーションのパフォーマンスを評価するために使用できます。 このツールの詳細については、を参照してください。 [ここ](/help/sites-developing/tough-day.md).

MongoDB を使用した最小のデプロイメントは、通常、次のトポロジで行われます。

* 1 つのプライマリノードと 2 つのセカンダリノードで構成された MongoDB レプリカセット。各 MongoDB インスタンスは、各ノード間の遅延が 15 ミリ秒未満の可用性ゾーンで実行されます。
* 1 つのリーダーノード、1 つの非リーダーノード、および両方が常にアクティブなオーサーインスタンスのクラスターで、各オーサーインスタンスが MongoDB プライマリインスタンスとセカンダリインスタンスが実行されている各データセンターで実行されます。

また、アセットやバイナリが MongoDB 内に保存されないように、共有ファイルシステムまたはAmazon S3 上にデータストアを設定することを強くお勧めします。 これにより、デプロイメント内での最適なパフォーマンスが確保されます。

2 つ以上のオーサーインスタンスのクラスターを持つ MongoDB レプリカセットを展開するメリットの 1 つは、オーサーインスタンス、MongoDB レプリカ、または完全なデータセンター障害がある場合に、ダウンタイムを最小限に抑えて自動復元シナリオを使用することです。 しかし、TarMK は制御されたフェイルオーバーメカニズムを使用して最小限のダウンタイムソリューションを提供できるので、TarMK に対する MongoMK の選択は、リカバリ要件によってのみ実行されるべきではありません。

デプロイメントの最初の 18 か月間に上記の条件が満たされないと思われる場合は、まず TarMK を使用してAEMをデプロイし、次に上記の条件が適用される後日に設定を再評価し、最後に TarMK に残るか MongoMK に移行するかを決定します。

### パブリッシュインスタンスで TarMK よりもAEM MongoMK を選択する際の例外 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

パブリッシュインスタンスに MongoMK をデプロイすることはお勧めしません。 デプロイメントのパブリッシュ層は、ほぼ常に、TarMK を実行する完全に独立したパブリッシュインスタンスのファームとしてデプロイされます。オーサーインスタンスからコンテンツをレプリケートすることで、同期が維持されます。 パブリッシュインスタンスに適したこの「何も共有しない」アーキテクチャを使用すると、パブリッシュ層のデプロイメントを線形的に水平方向に拡大/縮小できます。 ファームトポロジには、パブリッシュインスタンスにローリングベースで更新またはアップグレードを適用するメリットもあり、パブリッシュ層に対する変更にダウンタイムは必要ありません。

これは、複数のパブリッシャーがある場合は、パブリッシュ層での MongoMK クラスターの使用AEM Communitiesには当てはまりません。 JSRP を選択する場合は（[コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照）、選択した MK（MongoDB や RDB など）に関係なく任意のパブリッシュ側クラスターが適切であるように、MongoMK クラスターが適切です。

### MongoMK を使用して AEM をデプロイする際の前提条件とレコメンデーション {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

AEM 用の MongoMK デプロイメントを検討する場合、一連の前提条件とレコメンデーションがあります。

**MongoDB デプロイメントの必須の前提条件：**

1. AEMに詳しいAdobeコンサルティングまたは MongoDB アーキテクトの支援を受けて、MongoDB デプロイメントアーキテクチャとサイズ設定をプロジェクト実装の一部にする必要があります。
1. MongoDB の専門知識は、既存または新しい MongoDB 環境の維持と維持に自信を持つために、パートナーまたは顧客チーム内に存在する必要があります。
1. MongoDB の商用またはオープンソースバージョン (AEMは両方をサポート ) をデプロイすることを選択できますが、MongoDB Inc から直接 MongoDB Maintenance and Support 契約を購入する必要があります。
1. AEMと MongoDB の全体的なアーキテクチャとインフラストラクチャは、AdobeのAEM Architect が明確に定義し、検証する必要があります。
1. MongoDB を含むAEMデプロイメントのサポートモデルを確認します。

**MongoDB デプロイメントの重要なレコメンデーション：**

* MongoDB for Adobe Experience Manager に関する[記事](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
* MongoDB の実稼働[チェックリスト](https://docs.mongodb.org/manual/administration/production-checklist/)を確認してください。
* [こちら](https://university.mongodb.com/)から、MongoDB の認定クラスにオンラインで参加できます。

>[!NOTE]
>
>これらのガイドライン、前提条件および推奨事項に関するその他の質問は、にお問い合わせください。 [Adobeカスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html).

### AEM Communitiesの考慮事項 {#considerations-for-aem-communities}

デプロイ予定のサイトの場合 [AEM Communities](/help/communities/overview.md)を使用する場合は、次の操作をお勧めします。 [配置を選択](/help/communities/working-with-srp.md#characteristicsofstorageoptions) コミュニティメンバーがパブリッシュ環境から投稿した UGC の処理に最適化されています。

次を使用： [共通店](/help/communities/working-with-srp.md)を使用する場合、UGC の一貫性のある表示を得るために、オーサーインスタンスと他のパブリッシュインスタンス間で UGC をレプリケートする必要はありません。

デプロイメントに最適な永続性のタイプを選択する際に役立つ、一連の意思決定のマトリクスを次に示します。

#### オーサーインスタンス用のデプロイメントタイプの選択 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### パブリッシュインスタンス用のデプロイメントタイプの選択 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB ライセンスポリシー](https://www.mongodb.org/about/licensing/)のページを参照してください。
>
>AEM のデプロイメントを最大限に活用するには、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。
>
>ライセンスには、標準レプリカセットが含まれています。このセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成され、オーサーデプロイメントまたはパブリッシュデプロイメントのどちらかに使用できます。
>
>MongoDB でオーサーとパブリッシュの両方を実行する場合は、2 つの異なるライセンスを購入する必要があります。
>
>詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
