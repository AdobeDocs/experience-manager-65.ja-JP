---
title: AEM 6 でのノードストアとデータストアの設定
seo-title: AEM 6 でのノードストアとデータストアの設定
description: ノードストアとデータストアを設定する方法およびデータストアのガベージコレクションを実行する方法を学習します。
seo-description: ノードストアとデータストアを設定する方法およびデータストアのガベージコレクションを実行する方法を学習します。
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: f0ec3415ffef70c985828f17b32dc0d453c1ae7c
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 69%

---


# AEM 6 でのノードストアとデータストアの設定{#configuring-node-stores-and-data-stores-in-aem}

## 概要 {#introduction}

Adobe Experience Manager（AEM）では、バイナリデータをコンテンツノードとは別に格納できます。バイナリデータはデータストアに格納され、コンテンツノードはノードストアに格納されます。

データストアとノードストアはどちらも OSGi 設定を使用して設定できます。各 OSGi 設定は、永続識別子（PID）を使用して参照されます。

## 設定手順 {#configuration-steps}

ノードストアとデータストアの両方を設定するには、次の手順を実行します。

1. AEM クイックスタート JAR ファイルを AEM のインストールディレクトリにコピーします。
1. Create a folder `crx-quickstart/install` in the installation directory.
1. 最初に、ノードストアを設定します。そのためには、使用するノードストアオプションの名前を持つ設定ファイルを `crx-quickstart/install` ディレクトリに作成します。

   For example, the Document node store (which is the basis for AEM&#39;s MongoMK implementation) uses the file `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

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
>**AEM 5.x** のインストール環境からのアップグレードに備えてこの記事をお読みになっている場合は、[アップグレード](https://docs.adobe.com/content/docs/ja/aem/6-0/deploy/upgrade.html)に関するドキュメントを先に参照してください。

### セグメントノードストア {#segment-node-store}

セグメントノードストアは、AEM6 におけるアドビの TarMK 実装の基盤です。このストアでは、`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` という PID を設定に使用します。

>[!CAUTION]
>
>セグメントノードストアのPIDがAEM 6からAEM 6.3 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` に変更され `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` ました。この変更を反映するために必要な構成の調整を行ってください。

以下のオプションを設定できます。

* `repository.home`：リポジトリのホームのパスです。リポジトリ関連のデータが格納されます。デフォルトでは、`crx-quickstart/segmentstore` ディレクトリにセグメントファイルが格納されます。

* `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトの最大サイズは 256 MB です。
* `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルト値は、AEM 6.3以降のバージョンではtrueです。 AEM 6.3 より前のデフォルトは false でした。

The following is a sample `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` file:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### ドキュメントノードストア {#document-node-store}

ドキュメントノードストアは、AEM MongoMK実装の基盤です。 It uses the `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. 以下の設定オプションを使用できます。

* `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは です。`mongodb://localhost:27017`

* `db`：Mongo データベースの名前です。デフォルトのデータベース名は **Oak**``. However, new AEM 6 installations use **aem-author** ``です。

* `cache`：キャッシュサイズ（MB 単位）です。これは DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは です。`256`

* `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは です。`256`

* `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルトは、`false` です。

The following is a sample `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` file:

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
>カスタムデータストアを有効にするには、それぞれのノードストア設定ファイル（`customBlobStore`セグメントノードストア`true`または[ドキュメントノードストア](/help/sites-deploying/data-store-config.md#segment-node-store)）で [ が ](/help/sites-deploying/data-store-config.md#document-node-store) に設定されていることを確認する必要があります。

### ファイルデータストア {#file-data-store}

これは Jackrabbit 2 に含まれる [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) の実装であり、バイナリデータを通常のファイルとしてファイルシステムに格納する手段を提供します。It uses the `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID.

以下の設定オプションを使用できます。

* `repository.home`：リポジトリのホームのパスです。リポジトリ関連の様々なデータが格納されます。By default, binary files would be stored under `crx-quickstart/repository/datastore` directory

* `path`：ファイルを格納するディレクトリのパスです。If specified then it takes precedence over `repository.home` value

* `minRecordLength`：データストアに格納するファイルの最小サイズ（バイト単位）です。この値よりも小さいバイナリコンテンツはインライン化されます。

>[!NOTE]
>
>NAS を使用して共有ファイルデータストアを格納する場合は、パフォーマンスの問題を回避するために、必ず高性能のデバイスのみを使用してください。

## Amazon S3 データストア {#amazon-s-data-store}

Amazon の Simple Storage Service（S3）にデータを格納するように AEM を設定できます。このストアでは、`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` という PID を設定に使用します。

S3 データストア機能を有効にするには、S3 データストアコネクタを含む機能パックをダウンロードしてインストールする必要があります。[Adobeリポジトリに移動し](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) 、機能パックの1.10.xバージョン（例：com.adobe.granite.oak.s3connector-1.10.0.zip）から最新バージョンをダウンロードします。 Additionally, you also need to download and install the latest AEM service pack as listed on the [AEM 6.5 Release Notes](/help/release-notes/sp-release-notes.md) page.

>[!NOTE]
>
>TarMK を選択して AEM を使用する場合、デフォルトでは、`FileDataStore` にバイナリが格納されます。To use TarMK with the S3 Datastore, you need to start AEM using the `crx3tar-nofds` runmode, for example:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

ダウンロードが完了したら、次の手順に従って S3 コネクタをインストールして設定できます。

1. 機能パック zip ファイルの内容を一時フォルダーに解凍します。

1. 一時フォルダーに移動し、次の場所に移動します。

   ```xml
   jcr_root/libs/system/install
   ```

   Copy all the contents from the above location to `<aem-install>/crx-quickstart/install.`

1. If AEM is already configured to work with the Tar or MongoDB storage, remove any existing configuration files from the ***&lt;aem-install>***/*crx-quickstart*/*install* folder before proceeding. The files that need to be removed are:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 機能パックを展開した一時的な場所に戻り、次のフォルダーの内容をコピーします。

   * `jcr_root/libs/system/config`

   を

   * `<aem-install>/crx-quickstart/install`

   現在の設定に必要な設定ファイルのみをコピーしてください。専用データストアと共有データストアのどちらの設定の場合も、`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` ファイルをコピーします。

   >[!NOTE]
   >
   >クラスターセットアップでは、前述の手順をクラスターのすべてのノードで 1 ノードずつ実行してください。また、すべてのノードで必ず同じ S3 設定を使用してください。

1. ファイルを編集し、設定に必要な設定オプションを追加します。
1. AEM を起動します。

### 新しいバージョンの 1.10.x S3 コネクタへのアップグレード {#upgrading-to-a-new-version-of-the-x-s-connector}

新しいバージョンの 1.10.x S3 コネクタにアップグレードする必要がある場合は（1.10.0 から 1.10.4 へのアップグレードなど）、次の手順に従います。

1. AEM インスタンスを停止して 

1. AEM インストールフォルダーの `<aem-install>/crx-quickstart/install/15` に移動して、その内容のバックアップを作成します。
1. After the backup, delete the old version of the S3 Connector and its dependencies by deleting all the jar files in the `<aem-install>/crx-quickstart/install/15` folder, for example:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述のファイル名は例として使用しているだけであり、他の名前である場合もあります。

1. [アドビリポジトリ](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)から最新バージョンの 1.8.x 機能パックをダウンロードします。
1. Unzip the contents to a separate folder, then navigate to `jcr_root/libs/system/install/15`.
1. Copy the jar files to **&lt;aem-install>**/crx-quickstart/install/15 in the AEM installation folder.
1. AEM を起動して、コネクタの機能を確認します。

次のオプションを指定して設定ファイルを使用できます。

* accessKey:AWSアクセスキー。
* secretKey：AWS 秘密アクセスキーです。**注意：** または、 [IAMロール](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) (IAM roles)を使用して認証を行うこともできます。 If you are using IAM roles you no longer need to specify the `accessKey` and `secretKey`.

* s3Bucket：バケット名です。
* s3Region：バケットのリージョンです。
* path：データストアのパスです。デフォルト値は **&lt;AEM install folder>/repository/datastore** です。
* minRecordLength：データストアに格納するオブジェクトの最小サイズです。The minimum/default is **16KB.**
* maxCachedBinarySize:このサイズ以下のバイナリは、メモリキャッシュに格納されます。サイズはバイト単位です。デフォルトは**17408 **(17 KB)です。

* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret:共有データストアの設定にバイナリレスレプリケーションを使用する場合にのみ使用します。
* stagingSplitPercentage:ステージング用の非同期アップロードに使用するように設定されたキャッシュサイズの割合。 デフォルト値は **10** です。
* uploadThreads:非同期アップロードで使用されるアップロードスレッドの数です。 デフォルト値は **10** です。
* stagingPurgeInterval:ステージングキャッシュからの完了したアップロードを削除する間隔（秒）です。 The default value is **300** seconds (5 minutes).
* stagingRetryInterval:失敗したアップロードの再試行間隔（秒単位）。 The default value is **600** seconds (10 minutes).

### バケットのリージョンのオプション {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>米国スタンダード</td>
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
   <td>アジアパシフィック（シンガポール）<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>アジアパシフィック（シドニー）<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>アジアパシフィック（東京）</td>
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
>The DataStore implementations of `S3DataStore`, `CachingFileDataStore` and `AzureDataStore` support local file system caching. The `CachingFileDataStore` implementation is useful when the DataStore is on NFS (Network File System).


古いキャッシュ実装（Oak 1.6 より前）からアップグレードする場合は、ローカルファイルシステムのキャッシュディレクトリの構造に違いがあります。古いキャッシュ構造では、ダウンロードされたファイルとアップロードされたファイルの両方がキャッシュパスの直下に置かれていました。新しい構造では、ダウンロードとアップロードが分離され、キャッシュパスの下の `upload` と `download` という名前の 2 つのディレクトリに格納されます。アップグレードプロセスはシームレスにおこなわれ、保留中のアップロードがある場合はアップロードがスケジュールされ、キャッシュ内に以前にダウンロードされたファイルがある場合は初期化時にキャッシュに配置されます。

You can also upgrade the cache offline by using the `datastorecacheupgrade` command of oak-run. このコマンドの実行方法について詳しくは、oak-run モジュールの [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) を参照してください。

キャッシュにはサイズ制限があり、cacheSizeパラメーターを使用して設定できます。

**ダウンロード**

データストアからアクセスする前に、要求されたファイル／Blob のレコードがローカルキャッシュでチェックされます。ファイルをキャッシュに追加しているときに、設定された制限（`cacheSize` パラメーターを参照）をキャッシュが超えると、領域を再利用できるように、ファイルの一部が消去されます。

**非同期アップロード**

キャッシュでは、データストアへの非同期アップロードがサポートされています。ファイルは（ファイルシステム上の）キャッシュでローカルにステージングされ、非同期ジョブでファイルのアップロードが開始されます。非同期アップロードの数は、ステージングキャッシュのサイズによって制限されます。ステージングキャッシュのサイズは、`stagingSplitPercentage` パラメーターを使用して設定します。このパラメーターでは、ステージングキャッシュに使用するキャッシュサイズの割合（％）を定義します。Also, the percentage of cache available for downloads is calculated as **(100 -`stagingSplitPercentage`) *`cacheSize`**.

The asynchronous uploads are multi-threaded and the number of threads is configured by using the `uploadThreads` parameter.

アップロードが完了すると、ファイルはメインダウンロードキャッシュに移動します。ステージングキャッシュのサイズが制限を超えると、それまでの非同期アップロードが完了して、ステージングキャッシュ内の領域を再び使用できるようになるまで、ファイルは同期的にデータストアにアップロードされます。The uploaded files are removed from the staging area by a periodic job whose interval is configured by the `stagingPurgeInterval` parameter.

（ネットワークの障害などが原因で）失敗したアップロードは再試行キューに配置され、定期的に再試行されます。The retry interval is configured by using the `stagingRetryInterval parameter`.

#### Amazon S3 によるバイナリなしのレプリケーションの設定 {#configuring-binaryless-replication-with-amazon-s}

S3 によるバイナリなしのレプリケーションを設定するには、次の手順を実行する必要があります。

1. オーサーインスタンスとパブリッシュインスタンスをインストールし、それらが正しく開始されたことを確認します。
1. Go to the replication agent settings, by opening a page to *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. 「**設定**」セクションの「**編集**」ボタンを押します。
1. 「**シリアル化の種類**」オプションを「**バイナリなし**」に変更します。

1. Add the parameter &quot; `binaryless`= `true`&quot; in the transport uri. 変更後、URI は次のようになります。

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. オーサーインスタンスとパブリッシュインスタンスをすべて再起動して、変更を有効にします。

#### S3 と MongoDB を使用したクラスターの作成 {#creating-a-cluster-using-s-and-mongodb}

1. 次のコマンドを使用して CQ クイックスタートを展開します。

   `java -jar cq-quickstart.jar -unpack`

1. AEM を展開したら、*crx-quickstart*/*install* フォルダーをインストールディレクトリ内に作成します。

1. 次の 2 つのファイルを `crx-quickstart` フォルダー内に作成します。

   * *org.apache.jackrabbit.oak.plugins.ドキュメント.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   ファイルを作成したら、必要に応じて設定オプションを追加します。

1. S3 データストアで必要な、前述の 2 つのバンドルをインストールします。
1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。
1. 次のコマンドを使用して AEM を起動します。

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 2 つ目の AEM インスタンスについて手順 1 ～ 4 を繰り返します。
1. 2 つ目の AEM インスタンスを起動します。

#### 共有データストアの設定 {#configuring-a-shared-data-store}

1. まず、データストアを共有するために必要なデータストア設定ファイルを各インスタンスで作成します。

   * If you are using a `FileDataStore`, create a file named `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` and place it in the `<aem-install>/crx-quickstart/install` folder.

   * If using S3 as the data store, create a file named o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` in the `<aem-install>/crx-quickstart/install` folder as above.

1. 同じデータストアを指すようにデータストア設定ファイルを各インスタンスで変更します。詳しくは、[こちらの記事](/help/sites-deploying/data-store-config.md#data-store-configurations)を参照してください。
1. インスタンスのクローンが既存のサーバーから作成された場合、リポジトリがオフラインになっている間に、最新の oak-run ツールを使用して新しいインスタンスの `clusterId` を削除する必要があります。実行する必要があるコマンドは次のとおりです。

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >セグメントノードストアを設定する場合、リポジトリパスを指定する必要があります。By default, the path is `<aem-install-folder>/crx-quickstart/repository/segmentstore.` If a Document node store is configured you can use a [Mongo Connection String URI](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >oak-run ツールは、次の場所からダウンロードできます。
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >AEM インストールで使用している Oak バージョンに応じて、様々なバージョンのツールを使用する必要があることに注意してください。ツールを使用する前に、以下のバージョン要件を確認してください。
   >
   >
   >
   >    * Oak バージョン **1.2.x** については、oak-run **1.2.12 以降**&#x200B;を使用します。
   >    * **上述のものよりも新しい** Oak バージョンについては、AEM インストールの Oak コアと一致するバージョンの oak-run を使用します。


1. 最後に、設定を検証します。そのためには、データストアを共有する各リポジトリによってデータストアに追加された一意のファイルを探す必要があります。The format of the files is `repository-[UUID]`, where the UUID is a unique identifier of each individual repository.

   つまり、正しい設定には、データストアを共有するリポジトリと同じ数の一意のファイルがあります。

   ファイルは、データストアに応じて別々に格納されます。

   * `FileDataStore` の場合、データストアフォルダーのルートパスにファイルが作成されます。
   * For the `S3DataStore` the files are created in the configured S3 bucket under the `META` folder.

## Azure データストア {#azure-data-store}

Microsoft の Azure ストレージサービスにデータを格納するように AEM を設定できます。このストアでは、`org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` という PID を設定に使用します。

Azure データストア機能を有効にするには、Azure コネクタを含む機能パックをダウンロードしてインストールする必要があります。[Adobeリポジトリに移動し](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 、機能パックの1.6.xバージョン（例：com.adobe.granite.oak.azureblobconnector-1.6.3.zip）から最新バージョンをダウンロードします。

>[!NOTE]
>
>TarMK を選択して AEM を使用する場合、デフォルトでは、FileDataStore にバイナリが格納されます。To use TarMK with the Azure DataStore, you need to start AEM using the `crx3tar-nofds` runmode, for example:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

ダウンロードが完了したら、次の手順に従って Azure コネクタをインストールして設定できます。

1. 機能パック zip ファイルの内容を一時フォルダーに解凍します。

1. Go to the temporary folder and copy the contents of `jcr_root/libs/system/install` to the `<aem-install>crx-quickstart/install` folder.
1. If AEM is already configured to work with the Tar or MongoDB storage, remove any existing configuration files from the `/crx-quickstart/install` folder before proceeding. 削除する必要があるファイルは次のとおりです。

   MongoMK の場合：

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   TarMKの場合：

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Return to the temporary location where the feature pack has been extracted and copy the contents of `jcr_root/libs/system/config` to the `<aem-install>/crx-quickstart/install` folder.
1. 設定ファイルを編集し、設定に必要な設定オプションを追加します。
1. AEM を起動します。

次のオプションを指定して設定ファイルを使用できます。

* azureSas=&quot;&quot;:コネクタのバージョン1.6.3では、Azure Shared Access Signature (SAS)のサポートが追加されました。 **SAS とストレージ資格情報の両方が設定ファイルに存在する場合は、SAS が優先されます。** SASの詳細については、 [公式ドキュメントを参照してください](https://docs.microsoft.com/ja-jp/azure/storage/common/storage-dotnet-shared-access-signature-part-1)。 「=」文字は、「\=」のようにエスケープされていることを確認してください。

* azureBlobEndpoint=&quot;&quot;：Azure Blob エンドポイントです。例えば、https://&lt;ストレージアカウント>.blob.core.windows.netのように指定します。
* accessKey=&quot;&quot;：ストレージアカウント名です。Microsoft Azure の認証の資格情報について詳しくは、[公式ドキュメント](https://azure.microsoft.com/ja-jp/documentation/articles/storage-create-storage-account)を参照してください。

* secretKey=&quot;&quot;：ストレージアクセスキーです。「=」文字は、「\=」のようにエスケープされていることを確認してください。
* container=&quot;&quot;：Microsoft Azure の Blob ストレージコンテナ名です。コンテナは、一連の Blob をグループ化したものです。詳しくは、[公式ドキュメント](https://msdn.microsoft.com/en-us/library/dd135715.aspx)を参照してください。
* maxConnections=&quot;&quot;：操作ごとの同時要求の数です。デフォルト値は 1 です。
* maxErrorRetry=&quot;&quot;:リクエストあたりの再試行数。 デフォルト値は 3 です。
* socketTimeout=&quot;&quot;:要求に使用されるタイムアウト間隔（ミリ秒）。 デフォルト値は 5 分です。

上述の設定に加えて、次の設定も指定できます。

* path: The path of the data store. The default is `<aem-install>/repository/datastore.`
* RecordLength:データストアに格納する必要があるオブジェクトの最小サイズです。 デフォルト値は 16 KB です。
* maxCachedBinarySize:このサイズ以下のバイナリは、メモリキャッシュに格納されます。サイズはバイト単位です。デフォルトは17408(17 KB)です。
* cacheSize:キャッシュのサイズ。値はバイト単位で指定します。デフォルトは64GBです。
* secret:共有データストアの設定にバイナリレスレプリケーションを使用する場合にのみ使用します。
* stagingSplitPercentage:ステージング用の非同期アップロードに使用するように設定されたキャッシュサイズの割合。 デフォルト値は 10 です。
* uploadThreads:非同期アップロードで使用されるアップロードスレッドの数です。 デフォルト値は 10 です。
* stagingPurgeInterval:ステージングキャッシュからの完了したアップロードを削除する間隔（秒）です。 デフォルト値は300秒（5分）です。
* stagingRetryInterval:失敗したアップロードの再試行間隔（秒単位）。 デフォルト値は600秒（10分）です。

>[!NOTE]
>
>次のように、すべての設定は引用符で囲む必要があります。

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## データストアのガベージコレクション {#data-store-garbage-collection}

データストアのガベージコレクションプロセスは、データストア内の未使用のファイルを削除するために使用します。このプロセスによって、貴重なディスク領域が解放されます。

データストアのガベージコレクションは次の方法で実行できます。

1. Going to the JMX console located at *https://&lt;serveraddress:port>/system/console/jmx*
1. **RepositoryManagement** を検索します。見つかった Repository Manager の MBean をクリックして、使用可能なオプションを表示します。
1. ページの末尾までスクロールして、「**startDataStoreGC(boolean markOnly)**」リンクをクリックします。
1. 次に示すダイアログの `false` パラメーターに `markOnly` と入力して、「**Invoke**」をクリックします。

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >`markOnly` パラメーターは、ガベージコレクションのスイープフェーズを実行するかどうかを示します。

## 共有データストアにおけるデータストアのガベージコレクション {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>（Mongo または Segment Tar を備えた）クラスターまたは共有データストアのセットアップでガベージコレクションを実行するときに、特定の blob ID を削除できないことを知らせる警告がログに表示される場合があります。これは、以前のガベージコレクションで削除されたblob IDが、ID削除に関する情報を持たない他のクラスターまたは共有ノードによって誤って参照されるためです。 その結果、前回の実行時に既に削除された ID を、ガベージコレクションで再度削除しようとするので、警告がログに記録されます。この動作はパフォーマンスや機能に影響しません。

新しいバージョンの AEM では、複数のリポジトリによって共有されるデータストアでもガベージコレクションを実行できます。共有データストアでデータストアのガベージコレクションを実行できるようにするには、次の手順に従います。

1. データストアのガベージコレクション用に設定されたメンテナンスタスクが、データストアを共有するすべてのリポジトリインスタンスで無効になっていることを確認します。
1. データストアを共有するす [べてのリポジトリインスタンスで、](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) バイナリガベージコレクション **(Binary Garbage Collection** )に記載されている手順を個別に実行します。 ただし、「呼び出し」ボタンをクリックする前に、 `true``markOnly` パラメーターのを必ず入力してください。

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 前述の手順がすべてのインスタンスで完了したら、**いずれかの**&#x200B;インスタンスからデータストアのガベージコレクションを再び実行します。

   1. JMX コンソールに移動して、Repository Manager の Mbean を選択します。
   1. 「**startDataStoreGC(boolean markOnly)**」リンクをクリックします。
   1. In the following dialogue, enter `false` for the `markOnly` parameter again.

   これにより、以前に使用したマークフェーズで見つかったすべてのファイルを照合して、未使用の残りのファイルがデータストアから削除されます。

