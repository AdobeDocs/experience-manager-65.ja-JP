---
title: TarMK コールドスタンバイによる AEM の実行方法
seo-title: How to Run AEM with TarMK Cold Standby
description: TarMK コールドスタンバイセットアップの作成、設定、維持方法について説明します。
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 50%

---

# TarMK コールドスタンバイによる AEM の実行方法{#how-to-run-aem-with-tarmk-cold-standby}

## はじめに {#introduction}

Tar Micro Kernel のコールドスタンバイ容量を使用すると、1 つ以上のスタンバイAEMインスタンスが 1 つのプライマリインスタンスに接続できます。 同期プロセスは 1 つの方法のみで、プライマリインスタンスからスタンバイインスタンスへのみ実行されます。

スタンバイインスタンスの目的は、マスターリポジトリのライブデータコピーを保証し、何らかの理由でマスターが使用できない場合にデータを失うことなく迅速に切り替えることです。

コンテンツは、プライマリインスタンスとスタンバイインスタンスの間で線形的に同期されますが、ファイルやリポジトリの破損の整合性チェックは行われません。 この設計のため、スタンバイインスタンスはプライマリインスタンスの正確なコピーであり、プライマリインスタンスでの不整合を軽減するのに役立ちません。

>[!NOTE]
>
>コールドスタンバイ機能は、高可用性が必要なシナリオを保護するためのものです。 **作成者** インスタンス。 高可用性が必要な状況の場合： **公開** Tar Micro Kernel を使用するインスタンスの場合、Adobeはパブリッシュファームを使用することをお勧めします。
>
>利用可能なその他のデプロイメントについて詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md)のページを参照してください。

>[!NOTE]
>
>スタンバイインスタンスがプライマリノードから設定または派生した場合、以下のコンソール（管理関連のアクティビティ）へのアクセスのみが許可されます。
>
>* OSGi web コンソール
>
>その他のコンソールにはアクセスできません。

## 仕組み {#how-it-works}

プライマリAEMインスタンスで、TCP ポートが開かれ、受信メッセージをリッスンしています。 現在、スレーブがマスターに送信するメッセージには次の 2 種類があります。

* 現在のヘッドのセグメント ID を要求するメッセージ
* 指定した ID を持つセグメントデータを要求するメッセージ

スタンバイは、プライマリの現在のヘッドのセグメント ID を定期的に要求します。 セグメントがローカルに不明な場合は、取得されます。 既に存在する場合、セグメントが比較され、参照されているセグメントも必要に応じてリクエストされます。

>[!NOTE]
>
>スタンバイインスタンスは、同期のみのモードで実行されているので、いかなるタイプのリクエストも受信しません。スタンバイインスタンスで利用できるセクションは「Web コンソール」だけです（バンドルとサービスの設定を容易にするため）。

一般的な TarMK コールドスタンバイデプロイメント：

![chlimage_1](assets/chlimage_1.png)

## その他の特徴 {#other-characteristics}

### 堅牢性 {#robustness}

データフローは、接続やネットワーク関連の問題を自動的に検出し、処理するように設計されています。 すべてのパケットはチェックサムにバンドルされ、接続や破損したパケットに関する問題が発生した直後に、再試行メカニズムがトリガーされます。

#### パフォーマンス {#performance}

プライマリインスタンスで TarMK コールドスタンバイを有効にしても、パフォーマンスに大きな影響はありません。 追加の CPU 消費量は非常に低く、追加のハードディスクとネットワーク IO でパフォーマンスの問題が発生しないでください。

スタンバイでは、同期プロセス中に CPU の消費が高くなることが予想されます。 マルチスレッド化されていないため、複数のコアを使用して速度を上げることはできません。 データが変更または転送されない場合、測定可能なアクティビティは発生しません。 接続速度は、ハードウェアとネットワーク環境によって異なりますが、リポジトリのサイズや SSL の使用によって異なります。 初期同期に必要な時間を見積もる場合や、プライマリノード上で大量のデータが変更された場合は、この点に注意してください。

#### セキュリティ {#security}

すべてのインスタンスが同じイントラネットのセキュリティゾーンで実行されると仮定すると、セキュリティ違反のリスクが大幅に軽減されます。 ただし、スレーブとマスター間の SSL 接続を有効にすることで、セキュリティ層をさらに追加できます。 これにより、データが中間者によって侵害される可能性が低くなります。

さらに、受信リクエストの IP アドレスを制限することで、接続を許可するスタンバイインスタンスを指定できます。 これは、イントラネット内の誰もリポジトリをコピーできないことを保証するのに役立ちます。

>[!NOTE]
>
>Dispatcher と、Coldy Standby 設定の一部であるサーバーとの間にロードバランサーを追加することをお勧めします。 ロードバランサーは、ユーザートラフィックを **プライマリ** インスタンスを使用して、コールドスタンバイメカニズム以外の手段で、整合性を確保し、コンテンツがスタンバイインスタンスにコピーされないようにします。

## AEM TarMK コールドスタンバイセットアップの作成 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>AEM 6.3 では、Segment ノードストアおよび Standby ストアサービスの PID が、以前のバージョンと比較して次のように変更されました。
>
>* org.apache.jackrabbit.oak から&#x200B;**plugins**.segment.standby.store.StandbyStoreService から org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* org.apache.jackrabbit.oak から&#x200B;**plugins**.segment.SegmentNodeStoreService から org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>この変更を反映するために、必要な設定の調整を行ってください。

TarMK コールドスタンバイセットアップを作成するには、まず、プライマリのインストールフォルダー全体のファイルシステムコピーを新しい場所に作成して、スタンバイインスタンスを作成する必要があります。 その後、各インスタンスを、その役割を示す実行モード（`primary` または `standby`）で起動することができます。

以下に、1 つのマスターインスタンスと 1 つのスタンバイインスタンスによるセットアップを作成するために実行する必要のある手順を示します。

1. AEM をインストールします。

1. インスタンスをシャットダウンし、コールドスタンバイインスタンスを実行する場所にインストールフォルダーをコピーします。 異なるマシンから実行する場合でも、各フォルダーにわかりやすい名前を付けてください ( *aem-primary* または *aem-standby*) を使用してインスタンスを区別します。
1. プライマリインスタンスのインストールフォルダーに移動し、以下の手順に従ってください。

   1. `aem-primary/crx-quickstart/install` に以前の OSGi 設定があるかどうかを確認し、ある場合は削除します。

   1. `aem-primary/crx-quickstart/install` の下に `install.primary` というフォルダーを作成します。

   1. 使用するノードストアおよびデータストアに必要な設定を `aem-primary/crx-quickstart/install/install.primary` の下に作成します。
   1. `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` というファイルを同じ場所に作成し、適切に設定します。設定オプションについて詳しくは、[設定](/help/sites-deploying/tarmk-cold-standby.md#configuration)を参照してください。

   1. 外部データストアを使用して AEM TarMK インスタンスを実行している場合は、`crx3` という名前の `aem-primary/crx-quickstart/install` の下に `crx3` という名前のフォルダーを作成します。

   1. データストア設定ファイルを `crx3` フォルダーに配置します。

   例えば、外部ファイルデータストアを使用して AEM TarMK インスタンスを実行している場合は、次の設定ファイルが必要です。

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   以下に、プライマリインスタンスのサンプル設定を示します。

   **のサンプル** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config のサンプル**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config のサンプル**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. プライマリを起動し、プライマリ実行モードを必ず指定します。

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. の新しい Apache Sling Logging Logger を作成します。 **org.apache.jackrabbit.oak.segment** パッケージ。 ログレベルを「デバッグ」に設定し、ログの出力先を個別のログファイル（*/logs/tarmk-coldstandby.log* など）に指定します。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。
1. 次の場所に移動： **セカンダリ** インスタンスを作成し、jar を実行して起動します。
1. プライマリの場合と同じログ設定を作成します。 次に、インスタンスを停止します。
1. 次に、スタンバイインスタンスを準備します。 それには、プライマリインスタンスの場合と同じ手順を実行します。

   1. `aem-standby/crx-quickstart/install` の下にファイルがある場合は削除します。
   1. `aem-standby/crx-quickstart/install` の下に `install.standby` という新規フォルダーを作成します。

   1. 次の 2 つの設定ファイルを作成します。

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. `aem-standby/crx-quickstart/install` の下に `crx3` という新規フォルダーを作成します。

   1. データストア設定を作成し、`aem-standby/crx-quickstart/install/crx3` の下に配置します。この例では、作成する必要のあるファイルは次のようになります。

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. ファイルを編集し、必要な設定を作成します。

   一般的なスタンバイインスタンスの設定ファイルの例を次に示します。

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config のサンプル**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config のサンプル**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config のサンプル**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. を開始します。 **セカンダリ** スタンバイ実行モードを使用したインスタンス：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

このサービスは、次の方法で Web コンソールから設定することもできます。

1. Web コンソール（*https://serveraddress:serverport/system/console/configMgr*）にアクセスします。
1. と呼ばれるサービスを探しています **Apache Jackrabbit Oak Segment Tar Cold Standby Service** をクリックし、設定を編集します。
1. 設定を保存してインスタンスを再起動し、新しい設定を有効にします。

>[!NOTE]
>
>インスタンスの役割は、Sling Settings Web コンソールで&#x200B;**プライマリ**&#x200B;または&#x200B;**スタンバイ**&#x200B;実行モードの存在をチェックすることで、いつでも確認できます。
>
>この操作は、*https://localhost:4502/system/console/status-slingsettings* にアクセスし、「**実行モード**」の行をチェックすることで実行できます。

## 初回の同期 {#first-time-synchronization}

準備が完了し、スタンバイが初めて開始されると、スタンバイがプライマリに追い付くので、インスタンス間に大量のネットワークトラフィックが発生します。 ログを参照して、同期のステータスを確認できます。

スタンバイの *tarmk-coldstandby.log* では、次のようなエントリを確認できます。

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

スタンバイの *error.log*&#x200B;に設定すると、次のようなエントリが表示されます。

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

上記のログスニペットで、 *10.20.30.40* は、プライマリの IP アドレスです。

内 **プライマリ** *tarmk-coldstandby.log*&#x200B;に設定すると、次のようなエントリが表示されます。

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

この場合、ログに記載されている「クライアント」は **セカンダリ** インスタンス。

これらのエントリがログに表示されなくなったら、同期処理が完了したと見なしても問題ありません。

前述のエントリはポーリングメカニズムが正常に機能していることを示しますが、多くの場合、ポーリングが発生している間にデータが同期されているかどうかを把握するために役立ちます。そのためには、次のようなエントリを探します。

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

また、非共有 `FileDataStore` での実行時には、バイナリファイルが正しく送信されていることを示す次のようなメッセージが表示されます。

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 設定 {#configuration}

コールドスタンバイサービスでは、次の OSGi 設定を使用できます。

* **Persist Configuration：**&#x200B;有効にした場合、従来の OSGi 設定ファイルではなくリポジトリに設定が保存されます。本番システムでは、プライマリ設定がスタンバイによって取得されないように、この設定を無効にすることを推奨します。

* **Mode（`mode`）：**&#x200B;インスタンスの実行モードを選択します。

* **ポート（port）：**&#x200B;通信に使用するポート。デフォルトは、`8023` です。

* **Primary host（`primary.host`）：** — プライマリインスタンスのホスト。この設定は、スタンバイにのみ適用されます。
* **Sync interval（`interval`）：** - この設定は、同期リクエストの間隔を決定し、スタンバイインスタンスにのみ適用されます。

* **Allowed IP-Ranges（`primary.allowed-client-ip-ranges`）：** - プライマリへの接続を許可する IP の範囲。
* **保護（`secure`）：** SSL 暗号化を有効にします。この設定を利用するには、すべてのインスタンスで有効にする必要があります。
* **Standby Read Timeout（`standby.readtimeout`）：**&#x200B;スタンバイインスタンスから発行されたリクエストのタイムアウト（ミリ秒）。デフォルト値は 60000（1 分）です。

* **Standby Automatic Cleanup（`standby.autoclean`）：**&#x200B;同期サイクルでストアのサイズが増加した場合は、cleanup メソッドを呼び出します。

>[!NOTE]
>
>プライマリ ID とスタンバイ ID は、オフロードなどのサービスで個別に識別可能にするために、異なるリポジトリ ID を持つことを強くお勧めします。
>
>これを確実にカバーする最善の方法は、 *sling.id* ファイルをスタンバイ上に置き、インスタンスを再起動します。

## フェイルオーバー手順 {#failover-procedures}

何らかの理由でプライマリインスタンスに障害が発生した場合、以下の方法で起動時の実行モードを変更して、プライマリの役割を引き継ぐようにスタンバイインスタンスのいずれかを設定することができます。

>[!NOTE]
>
>設定ファイルについても、プライマリインスタンスに使用される設定と一致するように変更する必要があります。

1. スタンバイインスタンスがインストールされている場所に移動して、そのインスタンスを停止します。

1. このセットアップでロードバランサーを設定している場合は、この時点でロードバランサーの設定からプライマリを削除できます。
1. スタンバイのインストールフォルダーから `crx-quickstart` フォルダーをバックアップします。このフォルダーは、新しいスタンバイのセットアップ時に開始点として使用できます。

1. `primary` 実行モードを使用してインスタンスを再起動します。

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 新しいプライマリをロードバランサーに追加します。
1. 新しいスタンバイインスタンスを作成して起動します。詳しくは、前述の [AEM TarMK コールドスタンバイセットアップの作成](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)を参照してください。

## コールドスタンバイセットアップへのホットフィックスの適用 {#applying-hotfixes-to-a-cold-standby-setup}

セットアップにより、ホットフィックスをコールドスタンバイに適用する場合は、プライマリインスタンスにインストールし、ホットフィックスをインストールして新しいコールドスタンバイインスタンスにクローンを作成する方法をお勧めします。

それには、次の手順に従います。

1. JMX コンソールに移動し、**org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**bean を使用してコールドスタンバイインスタンスの同期処理を停止します。この方法について詳しくは、[監視](#monitoring)に関するセクションを参照してください。
1. コールドスタンバイインスタンスを停止します。
1. ホットフィックスをプライマリインスタンスにインストールします。 ホットフィックスのインストール方法について詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。
1. インストール後の問題に対してインスタンスをテストします。
1. インストールフォルダを削除して、コールドスタンバイインスタンスを削除します。
1. プライマリインスタンスを停止し、インストールフォルダ全体のファイルシステムコピーをコールドスタンバイの場所に実行して、インスタンスのクローンを作成します。
1. 新しく作成したクローンを、コールドスタンバイインスタンスとして機能するように再設定します。 詳しくは、 [AEM TarMK コールドスタンバイセットアップの作成。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. プライマリインスタンスとコールドスタンバイインスタンスの両方を起動します。

## モニタリング {#monitoring}

この機能は、JMX または MBeans を使用して情報を公開します。これにより、[JMX コンソール](/help/sites-administering/jmx-console.md)を使用して、スタンバイとマスターの現在の状態を検査することができます。この情報は、`type org.apache.jackrabbit.oak:type="Standby"` の`Status`という MBean で見ることができます。

**スタンバイ**

スタンバイインスタンスを観察すると、1 つのノードが公開されます。 ID は通常、汎用の UUID です。

このノードには 5 つの読み取り専用属性があります。

* `Running:` 同期プロセスが実行中かどうかを示すブール値。

* `Mode:` クライアント：インスタンスの識別用の UUID が続きます。この UUID は、設定が更新されるたびに変更されます。

* `Status:` 現在の状態をテキストで表現したもの（`running` または `stopped` など）。

* `FailedRequests:` 連続的に発生したエラーの回数。
* `SecondsSinceLastSuccess:` サーバーと最後に通信が成功してからの秒数。通信に成功しなかった場合は、`-1` と表示されます。

次のような 3 つの呼び出し可能なメソッドもあります。

* `start():` 同期プロセスを開始します。
* `stop():` 同期プロセスを停止します。
* `cleanup():` スタンバイでクリーンアップ操作を実行します。

**プライマリ**

プライマリを監視すると、TarMK スタンバイサービスが使用するポート番号が ID 値の MBean 経由で一部の一般情報が公開されます（デフォルトでは 8023）。 ほとんどのメソッドと属性は、スタンバイの場合と同じですが、次の点で異なります。

* `Mode:` 常に `primary` の値を表示します。

さらに、マスターに接続されている最大 10 個のクライアント（スタンバイインスタンス）の情報を取得できます。 MBean ID はインスタンスの UUID です。 これらの MBean には呼び出し可能なメソッドはありませんが、次に示す非常に役立つ読み取り専用属性があります。

* `Name:` クライアントの ID。
* `LastSeenTimestamp:` 最後のリクエストのタイムスタンプをテキストで表現したもの。
* `LastRequest:` クライアントの前回の要求。
* `RemoteAddress:` クライアントの IP アドレス。
* `RemotePort:` 前回の要求でクライアントが使用したポート。
* `TransferredSegments:` このクライアントに送信された総セグメント数。
* `TransferredSegmentBytes:` このクライアントに送信された総バイト数。

## コールドスタンバイリポジトリのメンテナンス {#cold-standby-repository-maintenance}

### リビジョンクリーンアップ {#revision-clean}

>[!NOTE]
>
>プライマリインスタンスで[オンラインリビジョンクリーンアップ](/help/sites-deploying/revision-cleanup.md)を実行する場合は、以下に示す手動での手順は必要ありません。また、オンラインリビジョンクリーンアップを使用している場合、待機インスタンスに対する `cleanup ()` 操作が自動的に実行されます。

>[!NOTE]
>
>スタンバイでオフラインでのリビジョンクリーンアップを実行しないでください。 その操作は不要であり、実行してもセグメントストアのサイズは小さくなりません。

アドビは、時間の経過とともにリポジトリが過度に増加するのを防ぐため、定期的にメンテナンスを実行することを推奨しています。コールドスタンバイリポジトリのメンテナンスを手動で実行するには、次の手順に従います。

1. JMX コンソールに移動し、**org.apache.jackrabbit.oak: ステータス（&quot;スタンバイ&quot;）** Bean を使用して、スタンバイインスタンスのスタンバイプロセスを停止します。この方法について詳しくは、[監視](/help/sites-deploying/tarmk-cold-standby.md#monitoring)に関する前述のセクションを参照してください。

1. プライマリAEMインスタンスを停止します。
1. プライマリインスタンスで oak コンパクションツールを実行します。 詳しくは、[リポジトリの保守](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)を参照してください。
1. プライマリインスタンスを起動します。
1. 最初の手順で説明したのと同じ JMX Bean を使用して、スタンバイインスタンスでスタンバイプロセスを開始します。
1. ログを監視し、同期が完了するまで待ちます。この時点で、スタンバイリポジトリのサイズがかなり大きくなっていることがあります。
1. 待機インスタンスで、最初の手順で説明したのと同じ JMX Bean を使用して、`cleanup()` 操作を実行します。

オフライン圧縮ではリポジトリ履歴が実質的には書き直されるので、リポジトリでの変更の計算により多くの時間がかかり、スタンバイインスタンスとプライマリとの同期が完了するまで通常より時間がかかる場合があります。このプロセスの完了後、スタンバイリポジトリのサイズはプライマリリポジトリのサイズとほぼ同じになることにも注意してください。

別の方法として、プライマリリポジトリは、プライマリでコンパクションを実行した後に手動でスタンバイにコピーできます。つまり、コンパクションが実行されるたびにスタンバイを再構築します。

### データストアのガベージコレクション {#data-store-garbage-collection}

ファイルデータストアインスタンスに対してガベージコレクションをときどき実行することが重要です。そうしないと、削除されたバイナリがファイルシステムに残り、最終的にドライブがいっぱいになります。ガベージコレクションを実行するには、以下の手順に従います。

1. [前述](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)の節で説明したように、コールドスタンバイリポジトリのメンテナンスを実行します。
1. メンテナンスプロセスが完了し、インスタンスが再起動したら、次の手順を実行します。

   * [この記事](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)で説明しているように、関連する JMX Bean を使用してプライマリでデータストアのガベージコレクションを実行します。
   * スタンバイでは、データストアのガベージコレクションは、**BlobGarbageCollection** MBean - `startBlobGC()` によってのみ行うことができます。RepositoryManagement MBean はスタンバイでは使用できません。

   >[!NOTE]
   >
   >共有データストアを使用していない場合は、ガベージコレクションを最初にプライマリで実行してから、スタンバイで実行する必要があります。
