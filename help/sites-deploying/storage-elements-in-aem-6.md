---
title: AEM 6.5 のストレージ要素
seo-title: AEM 6.5 のストレージ要素
description: AEM 6.5 で使用できるノードストレージ実装およびリポジトリのメンテナンス方法について説明します。
seo-description: AEM 6.5 で使用できるノードストレージ実装およびリポジトリのメンテナンス方法について説明します。
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 80%

---


# AEM 6.5 のストレージ要素{#storage-elements-in-aem}

この記事では、以下について説明します。

* [AEM 6 のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [リポジトリのメンテナンス](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 のストレージの概要 {#overview-of-storage-in-aem}

AEM 6 における最も重要な変更点の 1 つは、リポジトリレベルでの刷新です。

現在、AEM6 には Tar ストレージと MongoDB ストレージという 2 つのノードストレージ実装があります。

### Tar ストレージ {#tar-storage}

#### 新規にインストールした AEM インスタンスと Tar ストレージの実行 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>セグメントノードストアのPIDがorg.apache.jackrabbit.oakから変更されました。**aem 6の旧バージョンからorg.apache.jackrabbit.oak.segment.SegmentNodeStoreService(AEM 6.3)へのplugins**.segment.SegmentNodeStoreService。この変更を反映するために必要な設定調整を行ってください。

デフォルトでは、AEM 6 は Tar ストレージを使用して、デフォルトの設定オプションによって、ノードおよびバイナリを保存します。ストレージ設定を手動でおこなうには、次の手順に従ってください。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダー内に配置します。
1. 次のコマンドを実行して AEM を展開します。

   `java -jar cq-quickstart-6.jar -unpack`

1. Create a folder named `crx-quickstart\install` in the installation directory.

1. 新しく作成したフォルダー内に `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` というファイルを作成します。

1. ファイルを編集し、設定オプションを設定します。セグメントノードストア（AEM の Tar ストレージ実装の基盤）では以下のオプションが利用できます。

   * `repository.home`：リポジトリのホームのパスです。リポジトリ関連の様々なデータが格納されます。デフォルトでは、crx-quickstart/segmentstore ディレクトリにセグメントファイルが格納されます。
   * `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトは 256MB です。

1. AEM を起動します。

### Mongo ストレージ {#mongo-storage}

#### 新規にインストールした AEM インスタンスと Mongo ストレージの実行 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

次の手順に従って、AEM 6 を MongoDB ストレージと共に実行するように設定できます。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダー内に配置します。
1. 次のコマンドを実行して AEM を展開します。

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。詳しくは、[MongoDB のインストール](https://docs.mongodb.org/manual/installation/)を参照してください。
1. Create a folder named `crx-quickstart\install` in the installation directory.
1. ノードストアを設定します。使用する設定の名前を持つ設定ファイルを `crx-quickstart\install` ディレクトリに作成します。

   The Document Node Store (which is the basis for AEM&#39;s MongoDB storage implementation) uses a file called `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. ファイルを編集し、設定オプションを設定します。以下のオプションが利用できます。

   * `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは です。`mongodb://localhost:27017`
   * `db`：Mongo データベースの名前です。新しい AEM 6 のインストールでは、デフォルトのデータベース名として **aem-author** を使用します。
   * `cache`：キャッシュサイズ（MB 単位）です。これは DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは 256 です。
   * `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは 256 です。
   * `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルト値は false です。

1. 使用するデータストアの PID を持つ設定ファイルを作成し、そのファイルを編集して設定オプションを設定します。詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

1. 次のコマンドを実行して、AEM 6 jar を MongoDB ストレージバックエンドと共に起動します。

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Where **`-r`** is the backend runmode. この例では、MongoDB サポートを指定して起動します。

#### Transparent Huge Pages の無効化 {#disabling-transparent-huge-pages}

Red Hat Linux では、Transparent Huge Pages（THP）と呼ばれるメモリ管理アルゴリズムが使用されます。AEM はきめ細かい読み取りと書き込みを実行しますが、THP は大規模な操作に最適化されています。この理由から、Tar と Mongo の両方のストレージで THP を無効にすることをお勧めします。アルゴリズムを無効にするには、次の手順に従います。

1. Open the `/etc/grub.conf` file in the text editor of your choice.
1. **grub.conf** ファイルに対する次の行。

   ```
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が有効になっているかどうかを確認します。

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効になっている場合、このコマンドの出力は次のようになります。

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>さらに、次の資料も参考にできます。
>
>* For more information regarding Transparent Huge Pages on Red Hat Linux, see this [article](https://access.redhat.com/solutions/46111).
>* For Linux tuning tips, see this [article](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html).

>



## リポジトリのメンテナンス {#maintaining-the-repository}

リポジトリが更新されるたびに、新しいコンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。 リポジトリのサイズが無制限に増大しないように、古いリビジョンをクリーンアップして、ディスクリソースを解放する必要があります。このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。リビジョンのクリーンアップメカニズムは、リポジトリから古いデータを削除してディスク領域を再利用します。 リビジョンクリーンアップについて詳しくは、[リビジョンクリーンアップのページ](/help/sites-deploying/revision-cleanup.md)を参照してください。
