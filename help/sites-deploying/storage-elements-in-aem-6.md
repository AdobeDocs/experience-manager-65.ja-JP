---
title: AEM 6.5 のストレージ要素
description: AEM 6.5 で使用可能なノードストレージ実装およびリポジトリのメンテナンス方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 100%

---

# AEM 6.5 のストレージ要素{#storage-elements-in-aem}

この記事では、次の内容について説明します。

* [AEM 6 のストレージの概要](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [リポジトリのメンテナンス](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6 のストレージの概要 {#overview-of-storage-in-aem}

AEM 6 で最も重要な変更の 1 つは、リポジトリレベルでのイノベーションです。

現在、AEM6 では 2 つのストレージ実装（Tar ストレージと MongoDB ストレージ）を使用できます。

### Tar ストレージ {#tar-storage}

#### 新規にインストールした AEM インスタンスと Tar ストレージの実行 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>セグメントノードストアの PID は、以前のバージョンの AEM 6 の org.apache.jackrabbit.oak.AEM 6 の旧バージョンの **plugins**.segment.SegmentNodeStoreService から AEM 6.3 の org.apache.jackrabbit.oak.segment.SegmentNodeStoreService。変更が反映されるように、必要な設定調整が行われていることを確認します。

デフォルトでは、AEM 6 は Tar ストレージを使用して、デフォルトの設定オプションを使用してノードとバイナリを保存します。次の操作を行うことで、ストレージ設定を手動で設定できます。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダーに配置します。
1. 次を実行して AEM を解凍します。

   `java -jar cq-quickstart-6.jar -unpack`

1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。

1. 新しく作成したフォルダー内に `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` というファイルを作成します。

1. ファイルを編集して、設定オプションを指定します。AEM Tar ストレージ実装の基盤となるセグメントノードストアでは、次のオプションを使用できます。

   * `repository.home`：リポジトリのホームのパスで、リポジトリ関連の様々なデータが格納されます。デフォルトでは、crx-quickstart/segmentstore ディレクトリにセグメントファイルが格納されます。
   * `tarmk.size`：セグメントの最大サイズ（MB 単位）です。デフォルトは 256 MB です。

1. AEM を起動します。

### Mongo ストレージ {#mongo-storage}

#### 新規にインストールした AEM インスタンスと Mongo ストレージの実行 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

次の手順に従って、AEM 6 を MongoDB ストレージと共に実行するように設定できます。

1. AEM 6 quickstart jar をダウンロードし、新しいフォルダーに配置します。
1. 次のコマンドを実行して AEM を解凍します。

   `java -jar cq-quickstart-6.jar -unpack`

1. MongoDB がインストールされていること、および `mongod` のインスタンスが実行されていることを確認します。詳しくは、[MongoDB のインストール](https://docs.mongodb.org/manual/installation/)を参照してください。
1. インストールディレクトリ内に `crx-quickstart\install` というフォルダーを作成します。
1. 使用する設定の名前を持つ設定ファイルを `crx-quickstart\install` ディレクトリに作成することで、ノードストアを設定します。

   ドキュメントノードストア（AEM の MongoDB ストレージ実装の基盤）では、`org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg` というファイルを使用します。

1. ファイルを編集して、設定オプションを指定します。以下のオプションが利用できます。

   * `mongouri`：Mongo データベースに接続するために必要な [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) です。デフォルトは `mongodb://localhost:27017` です
   * `db`：Mongo データベースの名前です。新しい AEM 6 のインストールでは、デフォルトのデータベース名として **aem-author** を使用します。
   * `cache`：キャッシュサイズ（メガバイト単位）です。このキャッシュサイズは、DocumentNodeStore で使用される様々なキャッシュに分散されます。デフォルトは 256 です。
   * `changesSize`：Mongo で差分出力のキャッシュに使用される capped コレクションのサイズ（MB 単位）です。デフォルトは 256 です。
   * `customBlobStore`：カスタムデータストアが使用されることを示すブール値です。デフォルトは false です。

1. 使用するデータストアの PID を持つ設定ファイルを作成し、そのファイルを編集して設定オプションを指定します。詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

1. 次のコマンドを実行して、AEM 6 jar を MongoDB ストレージバックエンドと共に起動します。

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   バックエンドの実行モードが **`-r`** の場合、MongoDB のサポートで始まる例です。

#### Transparent Huge Pages の無効化 {#disabling-transparent-huge-pages}

Red Hat Linux では、Transparent Huge Pages（THP）と呼ばれるメモリ管理アルゴリズムが使用されます。AEM は詳細な読み取りと書き込みを実行しますが、THP は大規模な操作に最適化されています。したがって、Tar と Mongo ストレージの両方で THP を無効にすることをお勧めします。アルゴリズムを無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. **grub.conf** ファイルに次の行を追加します。

   ```
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が反映されていることを確認します。

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効になっている場合、上記のコマンドの出力は次のようになります。

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>次のリソースを参照してください。
>
>* Red Hat® Linux® 上の Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。
>* Linux® のチューニングのヒントについて詳しくは、こちらの[記事](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ja)を参照してください。
>

## リポジトリのメンテナンス {#maintaining-the-repository}

リポジトリを更新するたびに、コンテンツのリビジョンが作成されます。その結果、更新のたびにリポジトリのサイズが大きくなります。リポジトリの制御不能な増加を回避するには、古いリビジョンをクリーンアップして、ディスクリソースを解放する必要があります。このメンテナンス機能は、リビジョンクリーンアップと呼ばれます。リビジョンクリーンアップのメカニズムによって、ディスク領域を再利用するために、リポジトリから古いデータが削除されます。リビジョンクリーンアップについて詳しくは、[リビジョンクリーンアップのページ](/help/sites-deploying/revision-cleanup.md)を参照してください。
