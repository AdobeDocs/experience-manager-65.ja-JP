---
title: AEM 6 でのノードストアとデータストアの設定
description: ノードストアとデータストアを設定する方法およびデータストアのガベージコレクションを実行する方法を学習します。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 6257b56c61ae14889d9ecefed5030e123a415fd7
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 98%

---

# AEM 6 でのノードストアとデータストアの設定{#configuring-node-stores-and-data-stores-in-aem}

## はじめに {#introduction}

Adobe Experience Manager（AEM）では、バイナリデータをコンテンツノードとは別に格納できます。バイナリデータはデータストアに格納され、コンテンツノードはノードストアに格納されます。

データストアとノードストアはどちらも OSGi 設定を使用して設定できます。各 OSGi 設定は、永続識別子（PID）を使用して参照されます。

## 設定手順 {#configuration-steps}

ノードストアとデータストアの両方を設定するには、次の手順を実行します。

1. AEM クイックスタート JAR ファイルを AEM のインストールディレクトリにコピーします。
1. インストールディレクトリ内に `crx-quickstart/install` フォルダーを作成します。
1. 最初に、ノードストアを設定します。そのためには、使用するノードストアオプションの名前を持つ設定ファイルを `crx-quickstart/install` ディレクトリに作成します。

   例えば、ドキュメントノードストア（AEM の MongoMK 実装の基盤）では、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` ファイルを使用します。

1. ファイルを編集し、設定オプションを設定します。
1. 使用するデータストアの PID を持つ設定ファイルを作成します。ファイルを編集し、設定オプションを設定します。

   >[!NOTE]
   >
   >設定オプションについては、[ノードストアの設定](#node-store-configurations)および[データストアの設定](#data-store-configurations)を参照してください。

1. AEM を起動します。

## ノードストアの設定 {#node-store-configurations}

>[!CAUTION]
>
>新しいバージョンの Oak では、OSGi 設定ファイルについて新しい命名スキームと形式を採用しています。新しい命名スキームでは、設定ファイルの名前に **.config** を付けることが規定されています。また、新しい形式では、値を型指定することが規定されています。[こちら](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)を参照してください。
>
>古いバージョンの Oak からアップグレードする場合は必ず、`crx-quickstart/install` フォルダーのバックアップを最初に作成してください。アップグレード後、アップグレードしたインストール環境にフォルダーの内容を復元し、設定ファイルの拡張子を **.cfg** から **.config** に変更します。
>
>**AEM 5.x** のインストール環境からのアップグレードに備えてこの記事をお読みになっている場合は、[アップグレード](https://docs.adobe.com/jp/content/docs/ja/aem/6-0/deploy/upgrade.html)に関するドキュメントを先に参照してください。

### セグメントノードストア {#segment-node-store}

セグメントノードストアは、AEM6 におけるアドビの TarMK 実装の基盤です。このストアでは、`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` という PID を設定に使用します。

>[!CAUTION]
>
>セグメントノードストアの PID が、AEM 6 の `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` から AEM 6.3 の `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` に変更されました。この変更を反映するために必要な設定の調整を行ってください。

以下のオプションを設定できます。

* `repository.home`：リポジトリのホームのパスです。リポジトリ関連のデータが格納されます。デフォルトでは、`crx-quickstart/segmentstore` ディレクトリにセグメントファイルが格納されます。

* `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトの最大サイズは 256 MB です。
* `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。AEM 6.3 以降のバージョンのデフォルト値は true です。AEM 6.3 より前のデフォルトは false でした。

以下に、`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` ファイルのサンプルを示します。

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### ドキュメントノードストア {#document-node-store}

ドキュメントノードストアは、AEM の MongoMK 実装の基盤です。このストアでは、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* * という PID を使用します。以下の設定オプションを使用できます。

* `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは `mongodb://localhost:27017` です

* `db`：Mongo データベースの名前です。デフォルトは **Oak** です。``. However, new AEM 6 installations use **aem-author** `` デフォルトのデータベース名として使用します。

* `cache`：キャッシュサイズ（MB 単位）です。これは DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは `256` です

* `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは `256` です

* `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルトは `false` です。

以下に、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` ファイルのサンプルを示します。

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## データストアの設定 {#data-store-configurations}

多数のバイナリを処理する場合は、最大限のパフォーマンスを確保するために、デフォルトのノードストアではなく外部のデータストアを使用することをお勧めします。

例えば、プロジェクトで多数のメディアアセットが必要な場合は、それらをファイルデータストアまたは S3 データストアに格納すると、MongoDB 内に直接格納するよりも迅速にアセットにアクセスできます。

ファイルデータストアを使用すると、MongoDB よりもパフォーマンスが向上します。多数のアセットがある場合は、Mongo のバックアップと復元の処理速度も低下します。

各種データストアと設定の詳細については後述します。

>[!NOTE]
>
>カスタムデータストアを有効にするには、それぞれのノードストア設定ファイル（[セグメントノードストア](/help/sites-deploying/data-store-config.md#segment-node-store)または[ドキュメントノードストア](/help/sites-deploying/data-store-config.md#document-node-store)）で `customBlobStore` が `true` に設定されていることを確認する必要があります。

### ファイルデータストア {#file-data-store}

これは Jackrabbit 2 に含まれる [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) の実装であり、バイナリデータを通常のファイルとしてファイルシステムに格納する手段を提供します。このストアでは、`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` という PID を使用します。

以下の設定オプションを使用できます。

* `repository.home`：リポジトリのホームのパスです。リポジトリ関連の様々なデータが格納されます。デフォルトでは、`crx-quickstart/repository/datastore` ディレクトリにバイナリファイルが格納されます。

* `path`：ファイルを格納するディレクトリのパスです。このオプションを指定すると、`repository.home` より優先されます。

* `minRecordLength`：データストアに格納するファイルの最小サイズ（バイト単位）です。この値よりも小さいバイナリコンテンツはインライン化されます。

>[!NOTE]
>
>NAS を使用して共有ファイルデータストアを格納する場合は、パフォーマンスの問題を回避するために、必ず高性能のデバイスのみを使用してください。

## Amazon S3 データストア {#amazon-s-data-store}

Amazon の Simple Storage Service（S3）にデータを格納するように AEM を設定できます。このストアでは、`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` という PID を設定に使用します。

S3 データストア機能を有効にするには、S3 データストアコネクタを含む機能パックをダウンロードしてインストールする必要があります。[アドビリポジトリ](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)に移動し、1.10.x バージョンの機能パックの中から最新のバージョン（com.adobe.granite.oak.s3connector-1.10.0.zip など）をダウンロードします。さらに、[AEM 6.5 リリースノート](/help/release-notes/release-notes.md)ページに記載されている最新の AEM サービスパックをダウンロードしてインストールする必要もあります。

>[!NOTE]
>
>TarMK を選択して AEM を使用する場合、デフォルトでは、`FileDataStore` にバイナリが格納されます。S3 データストアと共に TarMK を使用するには、以下のように、`crx3tar-nofds` 実行モードを使用して AEM を起動する必要があります。

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

ダウンロードが完了したら、次の手順に従って S3 コネクタをインストールして設定できます。

1. 機能パック zip ファイルの内容を一時フォルダーに解凍します。

1. 一時フォルダーに移動し、次の場所に移動します。

   ```xml
   jcr_root/libs/system/install
   ```

   上述の場所からすべての内容を `<aem-install>/crx-quickstart/install.` にコピーします。

1. Tar または MongoDB ストレージと連携するように AEM を設定済みの場合は、続行する前に、既存の設定ファイルを ***&lt;aem-install>***/*crx-quickstart*/*install* フォルダーから削除します。削除する必要があるファイルは以下のとおりです。

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 機能パックを展開した一時的な場所に戻り、次のフォルダーの内容をコピーします。

   * `jcr_root/libs/system/config`

   コピー先：

   * `<aem-install>/crx-quickstart/install`

   現在の設定に必要な設定ファイルのみをコピーしてください。専用データストアと共有データストアのどちらの設定の場合も、`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` ファイルをコピーします。

   >[!NOTE]
   >
   >クラスターセットアップでは、前述の手順をクラスターのすべてのノードで 1 ノードずつ実行してください。また、すべてのノードで必ず同じ S3 設定を使用してください。

1. ファイルを編集し、設定に必要な設定オプションを追加します。
1. AEM を起動します。

### 1.10.x S3 コネクターの新しいバージョンへのアップグレード {#upgrading-to-a-new-version-of-the-s-connector}

1.10.x S3 コネクターを新しいバージョンにアップグレードする必要がある場合は（1.10.0 から 1.10.4 へのアップグレードなど）、以下の手順に従います。

1. AEM インスタンスを停止します。

1. AEM インストールフォルダーの `<aem-install>/crx-quickstart/install/15` に移動して、その内容のバックアップを作成します。
1. バックアップ後、古いバージョンの S3 コネクターとその依存関係を削除します。そのためには、`<aem-install>/crx-quickstart/install/15` フォルダー内の jar ファイル（以下のファイルなど）をすべて削除します。

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上記のファイル名は説明の目的でのみ使用されます。

1. [アドビリポジトリ](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/)から最新バージョンの 1.10.x 機能パックをダウンロードします。
1. 機能パックの内容を別のフォルダーに展開して、`jcr_root/libs/system/install/15` に移動します。
1. jar ファイルを AEM インストールフォルダーの **&lt;aem-install>**/crx-quickstart/install/15 にコピーします。
1. AEM を起動して、コネクタの機能を確認します。

次のオプションを指定して設定ファイルを使用できます。

* accessKey：AWS アクセスキーです。
* secretKey：AWS 秘密アクセスキーです。**注意：** [IAM ロール](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html)を認証に使用することもできます。IAM ロールを使用する場合、`accessKey` と `secretKey` を指定する必要はありません。

* s3Bucket：バケット名です。
* s3Region：バケットのリージョンです。
* path：データストアのパスです。デフォルト値は **&lt;AEM install folder>/repository/datastore** です。
* minRecordLength：データストアに格納するオブジェクトの最小サイズです。最小／デフォルトは **16 KB** です。
* maxCachedBinarySize：このサイズ以下のバイナリは、メモリキャッシュに格納されます。サイズはバイト単位です。デフォルト値は **17408 **（17 KB）です。

* cacheSize：キャッシュのサイズです。値はバイト単位で指定されます。デフォルト値は **64 GB** です。
* secret：共有データストア設定でバイナリなしのレプリケーションを使用する場合にのみ使用します。
* stagingSplitPercentage：非同期アップロードのステージングに使用するように設定されたキャッシュサイズの割合（％）です。デフォルト値は **10** です。
* uploadThreads：非同期アップロードに使用するアップロードスレッドの数です。デフォルト値は **10** です。
* stagingPurgeInterval：完了したアップロードをステージングキャッシュからパージする間隔（秒単位）です。デフォルト値は **300** 秒（5 分）です。
* stagingRetryInterval：失敗したアップロードの再試行間隔（秒単位）です。デフォルト値は **600** 秒（10 分）です。

### バケットリージョンのオプション {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>米国標準</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>米国西部</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>米国西部（北カリフォルニア）</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>欧州（アイルランド）<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>アジア太平洋（シンガポール）<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>アジア太平洋（シドニー）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>アジア太平洋（東京）</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>南米（サンパウロ）<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**データストアのキャッシュ**

>[!NOTE]
>
>`S3DataStore`、`CachingFileDataStore` および `AzureDataStore` のデータストア実装では、ローカルファイルシステムのキャッシュがサポートされています。`CachingFileDataStore` の実装は、データストアがネットワークファイルシステム（NFS）上にある場合に便利です。

古いキャッシュ実装（Oak 1.6 より前）からアップグレードする場合は、ローカルファイルシステムのキャッシュディレクトリの構造に違いがあります。古いキャッシュ構造では、ダウンロードされたファイルとアップロードされたファイルの両方がキャッシュパスの直下に置かれていました。新しい構造では、ダウンロードとアップロードが分離され、キャッシュパス配下にある `upload` と `download` という名前の 2 つのディレクトリに格納されます。アップグレードプロセスはシームレスに行われ、保留中のアップロードがある場合はアップロードがスケジュールされ、キャッシュ内にダウンロード済みファイルがある場合は初期化時にキャッシュに配置されます。

oak-run の「`datastorecacheupgrade`」コマンドを使用して、キャッシュをオフラインでアップグレードすることもできます。このコマンドの実行方法について詳しくは、oak-run モジュールの [README](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) を参照してください。

キャッシュにはサイズ制限があり、cacheSize パラメーターを使用して設定できます。

**ダウンロード**

データストアからアクセスする前に、要求されたファイル／Blob のレコードがローカルキャッシュでチェックされます。キャッシュにファイルを追加しているときに、キャッシュが設定された制限（`cacheSize` パラメーターを参照）を超えると、領域を再利用できるように、ファイルの一部が消去されます。

**非同期アップロード**

キャッシュでは、データストアへの非同期アップロードがサポートされています。ファイルは（ファイルシステム上の）キャッシュでローカルにステージングされ、非同期ジョブでファイルのアップロードが開始されます。非同期アップロードの数は、ステージングキャッシュのサイズによって制限されます。ステージングキャッシュのサイズは、`stagingSplitPercentage` パラメーターを使用して設定します。このパラメーターでは、ステージングキャッシュに使用するキャッシュサイズの割合（％）を定義します。また、ダウンロードで使用可能なキャッシュの割合は、 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

非同期アップロードはマルチスレッドです。スレッドの数は、`uploadThreads` パラメーターを使用して設定します。

アップロードが完了すると、ファイルはメインダウンロードキャッシュに移動します。ステージングキャッシュのサイズが制限を超えると、それまでの非同期アップロードが完了して、ステージングキャッシュ内の領域を再び使用できるようになるまで、ファイルは同期的にデータストアにアップロードされます。アップロードされたファイルは、定期ジョブによってステージング領域から削除されます。定期ジョブの間隔は、`stagingPurgeInterval` パラメーターで設定します。

（ネットワークの障害などが原因で）失敗したアップロードは再試行キューに配置され、定期的に再試行されます。再試行間隔は、`stagingRetryInterval parameter` パラメーターを使用して設定します。

#### Amazon S3 によるバイナリなしのレプリケーションの設定 {#configuring-binaryless-replication-with-amazon-s}

S3 によるバイナリなしのレプリケーションを設定するには、次の手順を実行する必要があります。

1. オーサーインスタンスとパブリッシュインスタンスをインストールし、それらが正しく開始されたことを確認します。
1. *https://localhost:4502/etc/replication/agents.author/publish.html* ページを開いて、レプリケーションエージェントの設定に移動します。
1. 「**設定**」セクションの「**編集**」ボタンを押します。
1. 「**シリアル化の種類**」オプションを「**バイナリなし**」に変更します。

1. 「`binaryless`= `true`」パラメーターをトランスポート URI に追加します。変更後、URI は次のようになります。

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. オーサーインスタンスとパブリッシュインスタンスをすべて再起動して、変更を有効にします。

#### S3 と MongoDB を使用したクラスターの作成 {#creating-a-cluster-using-s-and-mongodb}

1. 次のコマンドを使用して CQ クイックスタートを展開します。

   `java -jar cq-quickstart.jar -unpack`

1. AEM を展開したら、*crx-quickstart*/*install* フォルダーをインストールディレクトリ内に作成します。

1. 次の 2 つのファイルを `crx-quickstart` フォルダー内に作成します。

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*。*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*。*config*

   ファイルを作成したら、必要に応じて設定オプションを追加します。

1. S3 データストアで必要な、前述の 2 つのバンドルをインストールします。
1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。
1. 次のコマンドを使用して AEM を起動します。

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 2 つ目の AEM インスタンスについて手順 1 ～ 4 を繰り返します。
1. 2 つ目の AEM インスタンスを起動します。

#### 共有データストアの設定 {#configuring-a-shared-data-store}

1. まず、データストアを共有するために必要なデータストア設定ファイルを各インスタンスで作成します。

   * `FileDataStore` を使用する場合、`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` という名前のファイルを作成し、`<aem-install>/crx-quickstart/install` フォルダーに格納します。

   * S3 をデータストアとして使用する場合、前述のように `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` という名前のファイルを `<aem-install>/crx-quickstart/install` フォルダーに作成します。

1. 同じデータストアを指すようにデータストア設定ファイルを各インスタンスで変更します。詳しくは、[こちらの記事](/help/sites-deploying/data-store-config.md#data-store-configurations)を参照してください。
1. インスタンスのクローンが既存のサーバーから作成された場合、リポジトリーがオフラインになっている間に、最新の oak-run ツールを使用して新しいインスタンスの `clusterId` を削除する必要があります。実行する必要があるコマンドは次のとおりです。

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >セグメントノードストアを設定する場合、リポジトリーパスを指定する必要があります。デフォルトでは、パスは `<aem-install-folder>/crx-quickstart/repository/segmentstore.` です。ドキュメントノードストアを設定する場合、[Mongo の接続文字列 URI](https://docs.mongodb.org/manual/reference/connection-string/) を使用できます。

   >[!NOTE]
   >
   >Oak-run ツールは、次の場所からダウンロードできます。
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >AEM インストールで使用している Oak バージョンに応じて、様々なバージョンのツールを使用する必要があることに注意してください。ツールを使用する前に、以下のバージョン要件を確認してください。
   >
   >
   >
   >    * Oak バージョン **1.2.x** については、Oak-run **1.2.12 以降**&#x200B;を使用します
   >    * **上述のものよりも新しい** Oak バージョンについては、AEM インストールの Oak コアと一致するバージョンの oak-run を使用します。


1. 最後に、設定を検証します。そのためには、データストアを共有する各リポジトリによってデータストアに追加された一意のファイルを探す必要があります。ファイルの形式は `repository-[UUID]` です。UUID は、個々のリポジトリーの一意の識別子です。

   つまり、正しい設定には、データストアを共有するリポジトリと同じ数の一意のファイルがあります。

   ファイルは、データストアに応じて別々に格納されます。

   * `FileDataStore` の場合、データストアフォルダーのルートパスにファイルが作成されます。
   * `S3DataStore` の場合、設定済みの S3 バケットの `META` フォルダーにファイルが作成されます。

## Azure データストア {#azure-data-store}

Microsoft の Azure ストレージサービスにデータを格納するように AEM を設定できます。このストアでは、`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` という PID を設定に使用します。

Azure データストア機能を有効にするには、Azure コネクタを含む機能パックをダウンロードしてインストールする必要があります。[アドビリポジトリー](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/)にアクセスし、1.6.x バージョンの機能パックの中から最新バージョン（com.adobe.granite.oak.azureblobconnector-1.6.3.zip など）をダウンロードします。

>[!NOTE]
>
>TarMK を選択して AEM を使用する場合、デフォルトでは FileDataStore にバイナリが格納されます。Azure データストアと共に TarMK を使用するには、次のように、`crx3tar-nofds` 実行モードを使用して AEM を起動する必要があります。

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

ダウンロードが完了したら、次の手順に従って Azure コネクタをインストールして設定できます。

1. 機能パック zip ファイルの内容を一時フォルダーに解凍します。

1. 一時フォルダーに移動し、`jcr_root/libs/system/install` の内容を `<aem-install>crx-quickstart/install` フォルダーにコピーします。
1. Tar または MongoDB ストレージと連動するように AEM を設定済みの場合は、続行する前に、既存の設定ファイルを `/crx-quickstart/install` フォルダーから削除します。削除する必要があるファイルは次のとおりです。

   MongoMK の場合：

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   TarMK の場合：

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 機能パックを展開した一時的な場所に戻り、`jcr_root/libs/system/config` の内容を `<aem-install>/crx-quickstart/install` フォルダーにコピーします。
1. 設定ファイルを編集し、設定に必要な設定オプションを追加します。
1. AEM を起動します。

次のオプションを指定して設定ファイルを使用できます。

* azureSas=&quot;&quot;：コネクタのバージョン 1.6.3 で、Azure Shared Access Signature（SAS）のサポートが追加されました。**SAS とストレージ資格情報の両方が設定ファイルに存在する場合は、SAS が優先されます。** SAS について詳しくは、[公式ドキュメント](https://docs.microsoft.com/ja-jp/azure/storage/common/storage-dotnet-shared-access-signature-part-1)を参照してください。「=」文字は必ず、「\=」のようにエスケープしてください。

* azureBlobEndpoint=&quot;&quot;：Azure Blob エンドポイントです。例えば、https://&lt;storage-account>.blob.core.windows.net などです。
* accessKey=&quot;&quot;：ストレージアカウント名です。Microsoft Azure の認証資格情報について詳しくは、[公式ドキュメント](https://azure.microsoft.com/ja-jp/documentation/articles/storage-create-storage-account)を参照してください。

* secretKey=&quot;&quot;：ストレージアクセスキーです。「=」文字は必ず、「\=」のようにエスケープしてください。
* container=&quot;&quot;：Microsoft Azure の Blob ストレージコンテナ名です。コンテナは、一連の Blob をグループ化したものです。詳しくは、[公式ドキュメント](https://msdn.microsoft.com/ja-jp/library/dd135715.aspx)を参照してください。
* maxConnections=&quot;&quot;：操作ごとの同時要求の数です。デフォルト値は 1 です。
* maxErrorRetry=&quot;&quot;：要求ごとの再試行回数です。デフォルト値は 3 です。
* socketTimeout=&quot;&quot;：要求に使用するタイムアウト間隔（ミリ秒単位）です。デフォルト値は 5 分です。

上述の設定に加えて、次の設定も指定できます。

* path：データストアのパスです。デフォルト値は `<aem-install>/repository/datastore.` です。
* RecordLength：データストアに格納するオブジェクトの最小サイズです。デフォルト値は 16 KB です。
* maxCachedBinarySize：このサイズ以下のバイナリは、メモリキャッシュに格納されます。サイズはバイト数です。デフォルト値は 17408（17 KB）です。
* cacheSize：キャッシュのサイズです。値はバイト数で指定されます。デフォルト値は 64 GB です。
* secret：共有データストア設定でバイナリなしのレプリケーションを使用する場合にのみ使用します。
* stagingSplitPercentage：非同期アップロードのステージングに使用するように設定されたキャッシュサイズの割合（％）です。デフォルト値は 10 です。
* uploadThreads：非同期アップロードに使用するアップロードスレッドの数です。デフォルト値は 10 です。
* stagingPurgeInterval：完了したアップロードをステージングキャッシュからパージする間隔（秒単位）です。デフォルト値は 300 秒（5 分）です。
* stagingRetryInterval：失敗したアップロードの再試行間隔（秒単位）です。デフォルト値は 600 秒（10 分）です。

>[!NOTE]
>
>すべての設定を引用符で囲む必要があります。例：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## データストアのガベージコレクション {#data-store-garbage-collection}

データストアのガベージコレクションプロセスは、データストア内の未使用のファイルを削除するために使用します。このプロセスによって、貴重なディスク領域が解放されます。

データストアのガベージコレクションを実行する手順は次のとおりです。

1. JMX コンソール（*https://&lt;serveraddress:port>/system/console/jmx*）に移動します。
1. **RepositoryManagement** を検索します。見つかった Repository Manager の MBean をクリックして、使用可能なオプションを表示します。
1. ページの末尾までスクロールして、「**startDataStoreGC(boolean markOnly)**」リンクをクリックします。
1. 次に示すダイアログで `markOnly` パラメーターに `false` と入力して、「**Invoke**」をクリックします。

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly` パラメーターは、ガベージコレクションのスイープフェーズを実行するかどうかを示します。

## 共有データストアにおけるデータストアのガベージコレクション {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>クラスターまたは共有データストア設定（Mongo または Segment Tar を使用）でガベージコレクションを実行すると、特定の Blob ID を削除できないことについての警告がログに表示されることがあります。これは、以前のガベージコレクションで削除された Blob ID が、その ID が削除されたことを知らない他のクラスターまたは共有ノードによって誤って再度参照されることが原因で発生します。その結果、前回の実行時に既に削除された ID を、ガベージコレクションで再度削除しようとするので、警告がログに記録されます。この動作はパフォーマンスや機能に影響しません。

>[!NOTE]
> 共有データストアの設定を使用している場合、データストアのガベージコレクションが無効になった状態で、Lucene Binary クリーンアップタスクを実行すると、使用するディスク領域が突然増加することがあります。この問題を回避するには、次の手順に従って、オーサーとパブリッシュの全インスタンスについて BlobTracker を無効にする必要があります。
>
> 1. AEM インスタンスを停止します。
> 2. `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` ファイルで `blobTrackSnapshotIntervalInSecs=L"0"` パラメーターを追加します。このパラメーターを使用するには、Oak 1.12.0 以降のバージョンが必要です。
> 3. AEM インスタンスを再起動します。


新しいバージョンの AEM では、複数のリポジトリによって共有されるデータストアでもガベージコレクションを実行できます。共有データストアでデータストアのガベージコレクションを実行できるようにするには、次の手順に従います。

1. データストアのガベージコレクション用に設定されたメンテナンスタスクが、データストアを共有するすべてのリポジトリインスタンスで無効になっていることを確認します。
1. データストアを共有する&#x200B;**すべての**&#x200B;リポジトリーインスタンスについて、[バイナリガベージコレクション](/help/sites-deploying/data-store-config.md#data-store-garbage-collection)で指示されたステップを実行します。ただし、呼び出しボタンをクリックする前に必ず `markOnly` パラメーターに対して `true` を入力してください。

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 前述の手順がすべてのインスタンスで完了したら、**いずれかの**&#x200B;インスタンスからデータストアのガベージコレクションを再び実行します。

   1. JMX コンソールに移動して、Repository Manager の Mbean を選択します。
   1. 「**startDataStoreGC(boolean markOnly)**」リンクをクリックします。
   1. 次のダイアログで、`markOnly` パラメーターに再度 `false` を入力してください。
   これにより、以前に使用したマークフェーズで見つかったすべてのファイルを照合して、未使用の残りのファイルがデータストアから削除されます。
