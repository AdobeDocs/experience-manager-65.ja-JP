---
title: インプレースアップグレードの実行
description: AEM 6.5 のインプレースアップグレードの実行方法を説明します。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 83%

---

# インプレースアップグレードの実行{#performing-an-in-place-upgrade}

>[!NOTE]
>
>このページでは、AEM 6.5 のアップグレード手順の概要を説明します。インストールがアプリケーションサーバーにデプロイされている場合は、[アプリケーションサーバーのインストールのアップグレード手順](/help/sites-deploying/app-server-upgrade.md)を参照してください。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。また、システムが新しいバージョンの AEM の要件を満たしていることを確認してください。パターン検出によってアップグレードの複雑性を推定できます。また、詳しくは、[アップグレードの計画](/help/sites-deploying/upgrade-planning.md)の「アップグレードの範囲と要件」の節を参照してください。

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移行の前提条件 {#migration-prerequisites}

* **Java バージョンの最小要件：**&#x200B;移行ツールは、Java バージョン 7 以降でのみ機能します。AEM 6.3 以上では、サポートされているバージョンは Oracle の JRE 8 と IBM の JRE 7 および 8 のみです。

* **アップグレード対象のインスタンス：****5.6 よりも古い**&#x200B;バージョンからアップグレードする場合は、6.0 バージョンのアップグレードに関するドキュメントに記載されている手順に従って、AEM 6.0 へのインプレースアップグレードを事前に行うようにしてください。

## AEM クイックスタート jar ファイルの準備 {#prep-quickstart-file}

1. インスタンスが実行中である場合は停止します。

1. 新しい AEM jar ファイルをダウンロードし、それを使用して `crx-quickstart` フォルダーの外部にある古いファイルを置き換えます。

1. 次のコマンドを実行して新しいクイックスタート jar を解凍します。

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## コンテンツリポジトリの移行 {#content-repository-migration}

AEM 6.3 からアップグレードする場合、この移行は必要ありません。アドビでは 6.3 以前のバージョン向けに、リポジトリを AEM 6.3 で使用される新しいバージョンの Oak Segment Tar に移行するためのツールを提供しています。このツールはクイックスタートパッケージの一部として提供され、TarMK を使用するすべてのアップグレードに必須です。MongoMK を使用している環境のアップグレードには、リポジトリの移行は必要ありません。新しい Segment Tar 形式のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions) を参照してください。

実際の移行は、標準のAEM quickstart jar ファイルを使用して実行され、新しい `-x crx2oak` オプション：crx2oak ツールを実行してアップグレードを簡略化し、より堅牢にします。

>[!NOTE]
>
>CRX2Oak Quickstart 拡張を使用して TarMK リポジトリのコンテンツ移行を実行する場合は、移行コマンドラインに以下を追加することで **samplecontent** 実行モードを削除できます。
>
>* `--promote-runmode nosamplecontent`
>

実行すべきコマンドを決定するには、次のコマンドを使用します。

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

 `<<YOUR_PROFILE>>` と `<<ADDITIONAL_FLAGS>>` は、次の表にリストされているプロファイルとフラグに置き換えてください。

<table>
 <tbody>
  <tr>
   <td><strong>ソースリポジトリ</strong></td>
   <td><strong>ターゲットリポジトリ</strong></td>
   <td><strong>プロファイル</strong></td>
   <td><strong>追加のフラグ</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 または TarMK <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>以下のトラブルシューティングの節を参照</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK または crx2 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>以下のトラブルシューティングの節を参照</td>
  </tr>
  <tr>
   <td>データストアなしの TarMK</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>移行は不要</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**この場合：**

* `mongo-host` は、MongoDB サーバーの IP です（例：127.0.0.1）

* `mongo-port` は、MongoDB サーバーのポートです（例：27017）

* `mongo-database-name` は、データベースの名前です（例：aem-author）

**次のシナリオでは、追加のスイッチが必要となる場合もあります。**

* Java メモリマッピングが正しく処理されない Windows システムでアップグレードを実行する場合は、 `--disable-mmap` パラメータをコマンドに追加します。

crx2oak ツールの使用手順について詳しくは、[CRX2Oak 移行ツールの使用](/help/sites-deploying/using-crx2oak.md)を参照してください。crx2oak ヘルパー JAR は、必要に応じて手動でアップグレードできます。その場合は、クイックスタートを解凍した後に、手動で新しいバージョンに置き換えます。AEM インストールフォルダー内の場所は `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar` です。最新バージョンの CRX2Oak 移行ツールは、アドビリポジトリ（[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)）からダウンロードできます。

移行が正常に完了すると、ツールは終了コード 0 で終了します。さらに、AEM インストールディレクトリの `crx-quickstart/logs` にある `upgrade.log` ファイルで WARN および ERROR メッセージがないかどうかを確認してください。これらのメッセージは、移行中に発生した致命的ではないエラーを示している場合があります。

`crx-quickstart/install`フォルダーにある設定ファイルを確認します。移行が必要だった場合は、ターゲットリポジトリを反映するように更新されます。

**データストアに関するメモ：**

AEM 6.3 インストールでは新しく `FileDataStore` がデフォルトになっていますが、外部データストアの使用は必須ではありません。実稼動デプロイメントのベストプラクティスとして外部データストアを使用することをお勧めしますが、これはアップグレードの前提条件ではありません。AEM のアップグレードは既に複雑な処理なので、データストアを移行せずにアップグレードを行うことをお勧めします。必要に応じて、後でデータストアの移行を別の作業として実行できます。

## 移行に関する問題のトラブルシューティング {#troubleshooting-migration-issues}

6.3 からアップグレードする場合は、この節をスキップしてください。提供された crx2oak プロファイルは、ほとんどの顧客のニーズを満たす必要がありますが、追加のパラメーターが必要な場合があります。 移行中にエラーが発生する場合は、お使いの環境に、追加の設定オプションの指定が必要な事項が存在する可能性があります。その場合は、次のエラーが発生することがあります。

**外部データストアが指定されていないので、チェックポイントはコピーされません。 これにより、最初の起動時にリポジトリ全体のインデックスが再作成されます。--skip-checkpoints を使用して移行を強制するか、https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration で詳細を確認してください。**

何らかの理由で、移行プロセスがデータストア内のバイナリにアクセスする必要がありますが、データストアを見つけることができません。データストアの設定を指定するには、次のフラグを `<<ADDITIONAL_FLAGS>>` 移行コマンドの一部：

**S3 データストアの場合：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

`/path/to/SharedS3DataStore.config`は、S3 データストア設定ファイルのパスを表します。`/path/to/datastore`は、S3 データストアのパスを表します。

**ファイルデータストアの場合：**

```shell
--src-datastore=/path/to/datastore
```

`/path/to/datastore`は、ファイルデータストアのパスを表します。

## アップグレードの実行 {#performing-the-upgrade}

**S3 を使用している場合：**

1. 以前のバージョンの S3 コネクタに関連する、`crx-quickstart/install` 内の jar を削除します。

1. [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) から 1.10.x S3 コネクタの最新リリースをダウンロードします。

1. パッケージを一時フォルダーに抽出し、`jcr_root/libs/system/install` の内容を `crx-quickstart/install` フォルダーにコピーします。

### 適切なアップグレード開始コマンドの確認 {#determining-the-correct-upgrade-start-command}

アップグレードを実行するには、jar ファイルを使用して AEM を起動し、インスタンスを起動することが重要です。6.5 へのアップグレードについては、 [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) アップグレードコマンドで選択できます。

>[!IMPORTANT]
>
>oracleJava 11（または通常は 8 より新しいバージョンの Java）を実行している場合は、AEMの起動時に、追加のスイッチをコマンドラインに追加する必要があります。 詳しくは、 [Java 11 に関する考慮事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)を参照してください。

起動スクリプトから AEM を起動した場合、アップグレードは開始されません。ほとんどのお客様は、起動スクリプトを使用してAEMを起動し、この起動スクリプトをカスタマイズして、メモリ設定やセキュリティ証明書などの環境設定用のスイッチを含めています。 そのため、次の手順に従って、適切なアップグレードコマンドを確認することをお勧めします。

1. 実行中の AEM インスタンスで、コマンドラインから次のコマンドを実行します。

   ```shell
   ps -ef | grep java
   ```

1. AEM プロセスを探します。次のように表示されます。

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 既存の jar のパス（この場合は `crx-quickstart/app/aem-quickstart*.jar`）を `crx-quickstart` フォルダーと同じ階層にある新しい jar に置き換えて、コマンドを変更します。例として前述のコマンドを使用すると、コマンドは次のようになります。

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   これにより、適切なメモリ設定、カスタム実行モードおよびその他の環境パラメーターすべてがアップグレードに適用されます。アップグレードが完了すると、それ以降の起動時には起動スクリプトからインスタンスを起動できます。

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新したコードベースをデプロイする必要があります。ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックおよびトラブルシューティングを実行 {#perform-post-upgrade-check-troubleshooting}

[アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
