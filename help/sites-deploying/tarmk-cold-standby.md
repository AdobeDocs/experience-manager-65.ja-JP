---
title: TarMK コールドスタンバイによる AEM の実行方法
description: TarMK コールドスタンバイセットアップの作成、設定およびメンテナンスの方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 98%

---

# TarMK コールドスタンバイによる AEM の実行方法{#how-to-run-aem-with-tarmk-cold-standby}

## はじめに {#introduction}

Tar Micro Kernel のコールドスタンバイ機能を使用すると、1 つ以上のスタンバイ Adobe Experience Manager（AEM）インスタンスを 1 つのプライマリインスタンスに接続できます。同期プロセスは、プライマリインスタンスからスタンバイインスタンスの方向のみ実行されるという意味で単方向です。

スタンバイインスタンスの目的は、メインリポジトリのライブデータのコピーを保証して、メインが何らかの理由で利用できなくなった場合にデータ損失なしにすぐに切り替えられるようにすることです。

コンテンツはプライマリインスタンスとスタンバイインスタンス間で線形的に同期されます。この際、ファイルやリポジトリの破損に関する整合性チェックは実行されません。このような設計のため、スタンバイインスタンスはプライマリインスタンスの完全なコピーであり、プライマリインスタンスの不整合を軽減するものではありません。

>[!NOTE]
>
>コールドスタンバイ機能は、**オーサー**&#x200B;インスタンスで高可用性が必要なシナリオを保護するためのものです。Tar Micro Kernel を使用する&#x200B;**パブリッシュ**&#x200B;インスタンスで高可用性が必要な場合、パブリッシュファームを使用することをお勧めします。
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

プライマリ AEM インスタンスで TCP ポートが開き、受信メッセージをリッスンしています。現在、セカンダリがメインに送信するメッセージには次の 2 種類があります。

* 現在のヘッドのセグメント ID をリクエストするメッセージ
* 指定した ID のセグメントデータをリクエストするメッセージ

スタンバイは、プライマリの現在のヘッドのセグメント ID を定期的にリクエストします。そのセグメントがローカルに存在しない場合は、セグメントを取得します。既存のセグメントの場合は、セグメントを比較して、必要に応じて参照先のセグメントもリクエストします。

>[!NOTE]
>
>スタンバイインスタンスは、同期のみのモードで実行されているので、いかなるタイプのリクエストも受信しません。スタンバイインスタンスで利用できるセクションは「Web コンソール」だけです（バンドルとサービスの設定を容易にするため）。

一般的な TarMK コールドスタンバイデプロイメント：

![chlimage_1](assets/chlimage_1.png)

## その他の特徴 {#other-characteristics}

### 堅牢性 {#robustness}

データフローは、接続やネットワーク関連の問題を自動的に検出して処理するように設計されています。すべてのパケットはチェックサムにバンドルされ、接続の問題が発生したりパケットが破損したりした場合、再試行メカニズムがトリガーされます。

#### パフォーマンス {#performance}

プライマリインスタンスで TarMK コールドスタンバイを有効にしても、パフォーマンスへの影響はほぼありません。CPU 使用率の増加は少なく、追加のハードディスクやネットワーク I/O によるパフォーマンスの問題は発生しない見込みです。

スタンバイでは、同期プロセスの実行中に高い CPU 使用率になることが予想されます。この処理はマルチスレッドではないので、複数のコアの利用による高速化は図れません。変更されたデータや送信されるデータがない場合は、測定可能なアクティビティは発生しません。接続速度は、ハードウェアおよびネットワーク環境によって変わりますが、リポジトリのサイズや SSL の利用とは関係ありません。初期の同期に必要になる時間を推測するときや、プライマリノードでしばらく大量のデータが変更されたときには、この点に注意してください。

#### セキュリティ {#security}

すべてのインスタンスが同じイントラネットのセキュリティゾーン内で実行されると想定すると、セキュリティ侵害のリスクは大幅に軽減されます。それでも、セカンダリとメイン間での SSL 通信を有効にして、一層のセキュリティレイヤーを追加できます。この構成によって、データが中間者によって侵害される可能性が低下します。

さらに、受信するリクエストの IP アドレスを制限することで、接続を許可するスタンバイインスタンスを指定できます。この指定によって、イントラネット内でリポジトリをコピーできないことを保証できます。

>[!NOTE]
>
>Dispatcher と、コールドスタンバイセットアップに含まれるサーバーの間に、ロードバランサーを追加することを推奨します。ロードバランサーは、ユーザートラフィックを&#x200B;**プライマリ**&#x200B;インスタンスのみに転送するように設定する必要があります。これは、一貫性を確保し、コールドスタンバイメカニズム以外の手段でコンテンツがスタンバイインスタンスにコピーされるのを防ぐために必要です。

## AEM TarMK コールドスタンバイセットアップの作成 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>セグメントノードストアおよびスタンバイストアサービスの PID は、AEM 6.3 では以前のバージョンと比較して次のように変更されました。
>
>* org.apache.jackrabbit.oak から&#x200B;**plugins**.segment.standby.store.StandbyStoreService から org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* org.apache.jackrabbit.oak から&#x200B;**plugins**.segment.SegmentNodeStoreService から org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>この変更が反映されるように、必要に応じて設定を調整してください。

TarMK コールドスタンバイのセットアップを作成するには、まずプライマリのインストールフォルダー全体のファイルシステムコピーを実行して新しい場所にコピーし、スタンバイインスタンスを作成します。その後、各インスタンスを、その役割を示す実行モード（`primary` または `standby`）で起動することができます。

以下に、1 つのマスターインスタンスと 1 つのスタンバイインスタンスによるセットアップを作成するために実行する必要のある手順を示します。

1. AEM をインストールします。

1. インスタンスをシャットダウンし、コールドスタンバイインスタンスを実行する場所にインストールフォルダーをコピーします。別のマシンから実行する場合でも、各フォルダーにわかりやすい名前を付けて（*aem-primary* や *aem-standby* など）、各インスタンスを区別するようにしてください。
1. プライマリインスタンスのインストールフォルダーに移動し、次の手順を実行します。

   1. `aem-primary/crx-quickstart/install` に以前の OSGi 設定があるかどうかを確認し、ある場合は削除します。

   1. `aem-primary/crx-quickstart/install` の下に `install.primary` というフォルダーを作成します。

   1. 使用するノードストアおよびデータストアに必要な設定を `aem-primary/crx-quickstart/install/install.primary` の下に作成します。
   1. `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` というファイルを同じ場所に作成し、適切に設定します。設定オプションについて詳しくは、[設定](/help/sites-deploying/tarmk-cold-standby.md#configuration)を参照してください。

   1. 外部データストアを使用して AEM TarMK インスタンスを実行している場合は、`crx3` という名前の `aem-primary/crx-quickstart/install` の下に `crx3` という名前のフォルダーを作成します。

   1. データストア設定ファイルを `crx3` フォルダーに配置します。

   例えば、外部ファイルデータストアで AEM TarMK インスタンスを実行している場合は、次の設定ファイルが必要です。

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   以下に、プライマリインスタンスのサンプル設定を示します。

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config** **のサンプル**

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

1. プライマリ実行モードを指定していることを確認して、プライマリを起動します。

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. **org.apache.jackrabbit.oak.segment** パッケージに対して、Apache Sling Logging Logger を作成します。ログレベルを「デバッグ」に設定し、ログの出力先を個別のログファイル（*/logs/tarmk-coldstandby.log* など）に指定します。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。
1. **スタンバイ**&#x200B;インスタンスの場所に移動し、jar を実行して起動します。
1. プライマリと同じログ設定を作成します。その後、インスタンスを停止します。
1. 次に、スタンバイインスタンスを準備します。そのためには、プライマリインスタンスの場合と同様の手順を実行します。

   1. `aem-standby/crx-quickstart/install` にファイルがある場合は削除します。
   1. `aem-standby/crx-quickstart/install` に `install.standby` というフォルダーを作成します。

   1. 次の 2 つの設定ファイルを作成します。

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. `aem-standby/crx-quickstart/install` に `crx3` というフォルダーを作成します。

   1. データストア設定を作成し、`aem-standby/crx-quickstart/install/crx3` に配置します。この例では、作成する必要があるファイルは次のとおりです。

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. ファイルを編集し、必要な設定を作成します。

   以下に、典型的なスタンバイインスタンスのサンプル設定ファイルを示します。

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

1. スタンバイ実行モードを使用して&#x200B;**スタンバイ**&#x200B;インスタンスを起動します。

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

このサービスは、次の手順により web コンソール経由で設定することもできます。

1. Web コンソール（*https://serveraddress:serverport/system/console/configMgr*）にアクセスします。
1. **Apache Jackrabbit Oak Segment Tar Cold Standby Service** というサービスを探し、ダブルクリックして設定を編集します。
1. 設定を保存してインスタンスを再起動し、新しい設定を有効にします。

>[!NOTE]
>
>インスタンスの役割は、Sling 設定 web コンソールで&#x200B;**プライマリ**&#x200B;または&#x200B;**スタンバイ**&#x200B;の実行モードの存在をチェックすることで、いつでも確認できます。
>
>この操作は、*https://localhost:4502/system/console/status-slingsettings* にアクセスし、「**実行モード**」の行をチェックすることで実行できます。

## 初回の同期 {#first-time-synchronization}

準備が完了し、スタンバイが初めて開始された後は、スタンバイがプライマリに追い付こうとするので、インスタンス間に大量のネットワークトラフィックが発生します。ログを参照して、同期の状況を確認できます。

スタンバイの *tarmk-coldstandby.log* では、次のようなエントリを確認できます。

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

スタンバイの *error.log* では、次のようなエントリを確認できます。

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

上記のログのスニペットにある *10.20.30.40* は、プライマリの IP アドレスです。

**プライマリ**&#x200B;の *tarmk-coldstandby.log* では、次のようなエントリを確認できます。

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

この場合、ログに示されている「クライアント」は、**スタンバイ**&#x200B;インスタンスのことです。

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

* **設定を保持：**&#x200B;有効にした場合、設定は従来の OSGi 設定ファイルではなく、リポジトリに保存されます。Adobe では、プライマリ構成がスタンバイによってプルされないように、本番システムではこの設定を無効にしておくことをお勧めします。

* **モード（`mode`）：**&#x200B;インスタンスの実行モードを選択します。

* **ポート（port）：**&#x200B;通信に使用するポート。デフォルトは、`8023` です。

* **Primary host（`primary.host`）：** — プライマリインスタンスのホスト。この設定は、スタンバイにのみ適用されます。
* **Sync interval（`interval`）：** - この設定は、同期リクエストの間隔を決定し、スタンバイインスタンスにのみ適用されます。

* **許可 IP 範囲（`primary.allowed-client-ip-ranges`）：** - プライマリへの接続を許可する IP の範囲。
* **保護（`secure`）：** SSL 暗号化を有効にします。この設定を使用するには、すべてのインスタンスで有効にする必要があります。
* **Standby Read Timeout（`standby.readtimeout`）：**&#x200B;スタンバイインスタンスから発行されたリクエストのタイムアウト（ミリ秒）。デフォルト値は 60000（1 分）です。

* **Standby Automatic Cleanup（`standby.autoclean`）：**&#x200B;同期サイクルでストアのサイズが増加した場合は、cleanup メソッドを呼び出します。

>[!NOTE]
>
>Adobeでは、オフロードなどのサービスで個別に識別できるように、プライマリとスタンバイは異なるリポジトリ ID を持つようにすることをお勧めします。
>
>確実にこの設定が適用されていることを確認する良い方法は、スタンバイで *sling.id* を削除し、インスタンスを再起動することです。

## フェイルオーバー手順 {#failover-procedures}

何らかの理由でプライマリインスタンスに障害が発生した場合、以下の方法で起動時の実行モードを変更して、プライマリの役割を引き継ぐようにスタンバイインスタンスのいずれかを設定することができます。

>[!NOTE]
>
>設定ファイルを編集し、プライマリインスタンスで使用される設定と一致するようにします。

1. スタンバイインスタンスがインストールされている場所に移動して、そのインスタンスを停止します。

1. このセットアップでロードバランサーを設定している場合は、この時点でロードバランサーの設定からプライマリを削除できます。
1. スタンバイのインストールフォルダーから `crx-quickstart` フォルダーをバックアップします。このフォルダーは、新しいスタンバイのセットアップ時に開始点として使用できます。

1. `primary` 実行モードを使用してインスタンスを再起動します。

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 新しいプライマリをロードバランサーに追加します。
1. 新しいスタンバイインスタンスを作成して起動します。 詳しくは、上の手順を参照してください [AEM TarMK コールドスタンバイセットアップの作成](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## コールドスタンバイのセットアップへのホットフィックスの適用 {#applying-hotfixes-to-a-cold-standby-setup}

コールドスタンバイのセットアップにホットフィックスを適用する場合は、ホットフィックスをプライマリインスタンスにインストールしてから、新しいコールドスタンバイインスタンスにホットフィックスがインストールされたクローンを作成する方法が推奨されます。

これを行うには、次に示す手順に従います。

1. JMX コンソールに移動し、**org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**bean を使用してコールドスタンバイインスタンスの同期処理を停止します。この方法について詳しくは、[監視](#monitoring)に関するセクションを参照してください。
1. コールドスタンバイインスタンスを停止します。
1. ホットフィックスをプライマリインスタンスにインストールします。ホットフィックスのインストール方法について詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。
1. インストール後の問題に対してインスタンスをテストします。
1. インストールフォルダーを削除して、コールドスタンバイインスタンスを削除します。
1. プライマリインスタンスを停止し、インストールフォルダー全体のファイルシステムコピーをコールドスタンバイの場所に実行して、インスタンスのクローンを作成します。
1. 新しく作成したクローンがコールドスタンバイインスタンスとして機能するように再設定します。詳しくは、[AEM TarMK コールドスタンバイ設定の作成](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)を参照してください。
1. プライマリインスタンスとコールドスタンバイインスタンスの両方を起動します。

## モニタリング {#monitoring}

この機能は、JMX または MBean を使用して情報を公開します。 これにより、スタンバイとマスターの現在の状態を、 [JMX コンソール](/help/sites-administering/jmx-console.md). この情報は、`type org.apache.jackrabbit.oak:type="Standby"` の`Status`という MBean で見ることができます。

**スタンバイ**

スタンバイインスタンスを確認して、1 つのノードを公開します。ID は通常、汎用の UUID です。

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

プライマリを確認すると、TarMK スタンバイサービスが使用するポート番号（デフォルトでは 8023）を ID 値とする MBean を介して、一部の一般情報が公開されます。ほとんどのメソッドと属性は、スタンバイの場合と同じですが、次の点で異なります。

* `Mode:` は常に値 `primary` を表示します。

さらに、マスターに接続されている最大 10 個のクライアント（スタンバイインスタンス）の情報を取得できます。MBean ID はインスタンスの UUID です。これらの MBean には呼び出し可能なメソッドはありませんが、次に示す便利な読み取り専用属性があります。

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
>プライマリインスタンスで[オンラインリビジョンクリーンアップ](/help/sites-deploying/revision-cleanup.md)を実行する場合は、以下に示す手動での手順は必要ありません。また、オンラインでのリビジョンクリーンアップを使用している場合、スタンバイインスタンスに対する `cleanup ()` 操作が自動的に実行されます。

>[!NOTE]
>
>スタンバイではオフラインでのリビジョンクリーンアップを実行しないでください。その操作は不要であり、実行してもセグメントストアのサイズは小さくなりません。

時間の経過と共にリポジトリが過度に増大するのを防ぐために、メンテナンスを定期的に実行することをお勧めします。コールドスタンバイのリポジトリのメンテナンスを手動で実行するには、次の手順に従います。

1. JMX コンソールに移動し、**org.apache.jackrabbit.oak: ステータス（&quot;スタンバイ&quot;）** Bean を使用して、スタンバイインスタンスのスタンバイプロセスを停止します。この方法について詳しくは、[監視](/help/sites-deploying/tarmk-cold-standby.md#monitoring)に関する前述のセクションを参照してください。

1. プライマリの AEM インスタンスを停止します。
1. プライマリインスタンスで Oak 圧縮ツールを実行します。詳しくは、[リポジトリの保守](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)を参照してください。
1. プライマリインスタンスを起動します。
1. 最初の手順で説明したものと同じ JMX bean を使用して、スタンバイインスタンスでスタンバイプロセスを開始します。
1. ログを監視し、同期が完了するまで待ちます。この時点で、スタンバイリポジトリのサイズがかなり大きくなっていることがあります。
1. 待機インスタンスで、最初の手順で説明したのと同じ JMX Bean を使用して、`cleanup()` 操作を実行します。

オフライン圧縮ではリポジトリ履歴が実質的には書き直されるので、リポジトリでの変更の計算により多くの時間がかかり、スタンバイインスタンスとプライマリとの同期が完了するまで通常より時間がかかる場合があります。このプロセスの完了後、スタンバイリポジトリのサイズはプライマリリポジトリのサイズとほぼ同じになります。

別の方法として、プライマリで圧縮した後にプライマリリポジトリをスタンバイに手動でコピーすることもできます。つまり、圧縮するたびにスタンバイを再構築します。

### データストアのガベージコレクション {#data-store-garbage-collection}

ファイルデータストアのインスタンスに対してガベージコレクションを時々実行することが重要です。そうしないと、削除されたバイナリがファイルシステムに残り、最終的にドライブがいっぱいになります。ガベージコレクションを実行するには、以下の手順に従います。

1. [前述](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)の節で説明したように、コールドスタンバイリポジトリのメンテナンスを実行します。
1. メンテナンスプロセスが完了し、インスタンスが再起動したら、次の手順を実行します。

   * プライマリで、関連する JMX Bean を使用してデータストアのガベージコレクションを実行します。詳しくは、[こちらの記事](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)を参照してください。
   * スタンバイでは、データストアのガベージコレクションは **BlobGarbageCollection** MBean - `startBlobGC()` を使用してのみ行うことができます。**RepositoryManagement** MBean はスタンバイでは使用できません。

   >[!NOTE]
   >
   >共有データストアを使用していない場合は、ガベージコレクションを最初にプライマリで実行してから、スタンバイで実行します。
