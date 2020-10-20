---
title: インプレースアップグレードの実行
seo-title: インプレースアップグレードの実行
description: インプレースアップグレードの実行方法について説明します。
seo-description: インプレースアップグレードの実行方法について説明します。
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
translation-type: tm+mt
source-git-commit: 1718aac3d39662fb35336a4db3e3403641f9529a
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 80%

---


# インプレースアップグレードの実行{#performing-an-in-place-upgrade}

>[!NOTE]
>
>このページでは、AEM 6.5 のアップグレード手順の概要を説明します。インストールがアプリケーションサーバーにデプロイされている場合は、[アプリケーションサーバーのインストール環境のアップグレード手順](/help/sites-deploying/app-server-upgrade.md)を参照してください。

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了しておく必要があります。詳しくは、[コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)および[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を参照してください。また、システムが新しいバージョンの AEM の要件を満たしていることを確認してください。パターン検出によってアップグレードの複雑性を推定できます。また、詳しくは、[アップグレードの計画](/help/sites-deploying/upgrade-planning.md)の「アップグレードの範囲と要件」の節を参照してください。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移行の前提条件 {#migration-prerequisites}

* **Java バージョンの最小要件：**&#x200B;移行ツールは、Java バージョン 7 以降でのみ動作します。AEM 6.3 以上では、サポートされているバージョンは Oracle の JRE 8 と IBM の JRE 7 および 8 のみです。

* **アップグレード対象のインスタンス：**&#x200B;アップグレード対象のインスタンスのバージョンが **5.6 よりも古い**&#x200B;場合は、6.0 バージョンのアップグレードに関するドキュメントに記載されている手順に従って、AEM 6.0 へのインプレースアップグレードを事前におこなってください。

## AEM クイックスタート jar ファイルの準備 {#prep-quickstart-file}

1. インスタンスが実行中である場合は停止します。

1. 新しい AEM jar ファイルをダウンロードし、それを使用して `crx-quickstart` フォルダーの外部にある古いファイルを置き換えます。

1. 次のコマンドを実行して新しいクイックスタート jar を解凍します。

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## コンテンツリポジトリの移行 {#content-repository-migration}

AEM 6.3 からアップグレードする場合、この移行は必要ありません。6.3 以前のバージョンでは、リポジトリを AEM 6.3 で使用される新しいバージョンの Oak Segment Tar に移行するためのツールを提供しています。このツールはクイックスタートパッケージの一部として提供され、TarMK を使用するアップグレードには必須です。MongoMK を使用している環境のアップグレードでは、リポジトリを移行する必要はありません。新しい Segment Tar 形式の利点について詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions) を参照してください。

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool in order to simplify the upgrade and make it more robust.

>[!NOTE]
>
>CRX2Oak Quickstart 拡張を使用して TarMK リポジトリのコンテンツ移行を実行する場合は、移行コマンドラインに以下を追加することで **samplecontent** 実行モードを削除できます。
>
>* `--promote-runmode nosamplecontent`

>



実行するコマンドを次に示します。

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>ソースリポジトリ</strong></td>
   <td><strong>ターゲットリポジトリ</strong></td>
   <td><strong>プロファイル</strong></td>
   <td><strong>追加のフラグ</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2またはTarMKと <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>後述のトラブルシューティングに関する節を参照</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMKまたはcrx2 <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>後述のトラブルシューティングに関する節を参照</td>
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

* `mongo-host` は、MongoDB サーバーの IP です（例：127.0.0.1）。

* `mongo-port` は、MongoDB サーバーのポートです（例：27017）。

* `mongo-database-name` は、データベースの名前です（例：aem-author）。

**次のシナリオでは、追加のスイッチが必要となる場合もあります。**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, please add the `--disable-mmap` parameter to the command.

* If you are using Java 7, add the `-XX:MaxPermSize=2048m` parameter just after the `-Xmx` parameter.

crx2oak ツールの使用について詳しくは、[CRX2Oak 移行ツールの使用](/help/sites-deploying/using-crx2oak.md)を参照してください。crx2oak ヘルパーの JAR は、必要に応じて手動でアップグレードできます。そのためには、クイックスタートを展開した後、手動で新しいバージョンに置き換えます。AEM インストールフォルダー内のヘルパー JAR ファイルの場所は次のとおりです。 `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. 最新バージョンの CRX2Oak 移行ツールは、アドビリポジトリ（[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)）からダウンロードできます。

移行が正常に完了すると、ツールは終了コード 0 で終了します。さらに、AEM インストールディレクトリの `upgrade.log` にある `crx-quickstart/logs` ファイルで WARN および ERROR メッセージがないかどうかを確認してください。これらのメッセージは、移行中に発生した致命的ではないエラーを示している場合があります。

Check the configuration files beneath `crx-quickstart/install` folder. 移行が必要であった場合、これらの設定ファイルは、ターゲットリポジトリを反映するように更新されます。

**データストアに関する注意点：**

AEM 6.3 インストールでは新しく `FileDataStore` がデフォルトになっていますが、外部データストアの使用は必須ではありません。実稼動デプロイメントのベストプラクティスとして外部データストアを使用することをお勧めしますが、アップグレードの前提条件ではありません。AEM のアップグレードは既に複雑な処理なので、データストアを移行せずにアップグレードをおこなうことをお勧めします。必要であれば、別の作業として後からデータストアの移行を実行できます。

## 移行に関する問題のトラブルシューティング {#troubleshooting-migration-issues}

6.3 からアップグレードする場合、この節の説明はスキップしてください。提供されている crx2oak プロファイルはほとんどの環境のニーズに適合しますが、追加のパラメーターが必要になる場合もあります。移行中にエラーが発生する場合、お使いの環境の特定の特性に追加の設定オプションの指定が必要である可能性があります。その場合は、次のエラーが発生することがあります。

**Checkpoints won&#39;t be copied, because no external datastore has been specified.This will result in the full repository reindexing on the first start.Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

何らかの理由で、移行プロセスがデータストア内のバイナリにアクセスする必要がありますが、データストアを見つけることができません。In order to specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**S3 データストアの場合：**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**ファイルデータストアの場合：**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

## アップグレードの実行 {#performing-the-upgrade}

**S3 を使用している場合：**

1. 以前のバージョンの S3 コネクタに関連する、`crx-quickstart/install` 内の jar を削除します。

1. Download the latest release of the 1.8.x S3 connector from [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extract the package to a temporary folder and copy the contents of `jcr_root/libs/system/install` to the `crx-quickstart/install` folder.

### 適切なアップグレード開始コマンドの確認 {#determining-the-correct-upgrade-start-command}

アップグレードをおこなうには、jar ファイルを使用して AEM を起動し、インスタンスを実行することが重要です。For upgrading to 6.5, please also see other content restructuring and migration options in [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) that you can choose with the upgrade command.

>[!IMPORTANT]
>
>Oracle Java 11（または一般にバージョン 8 より新しい Java）を実行している場合は、AEM の起動時にコマンドラインにさらにスイッチを追加する必要があります。詳しくは、「 [Java 11の考慮事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)」を参照してください。

起動スクリプトから AEM を起動した場合、アップグレードは開始されません。ほとんどの顧客は、起動スクリプトを使用して AEM を起動します。また、メモリ設定、セキュリティ証明書など、環境設定に関するスイッチを追加するように起動スクリプトをカスタマイズしています。そのため、次の手順に従って、適切なアップグレードコマンドを確認することをお勧めします。

1. 実行中の AEM インスタンスで、コマンドラインから次のコマンドを実行します。

   ```shell
   ps -ef | grep java
   ```

1. AEM プロセスを探します。次のようになります。

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 既存の jar のパス（この場合は `crx-quickstart/app/aem-quickstart*.jar`）を `crx-quickstart` フォルダーと同じ階層にある新しい jar に置き換えて、コマンドを変更します。前のコマンドを例として使用すると、次のコマンドが実行されます。

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   これにより、適切なメモリ設定、カスタム実行モードおよびその他の環境パラメーターすべてがアップグレードに適用されます。アップグレードが完了すると、それ以降の起動時には起動スクリプトからインスタンスを起動できます。

## アップグレードしたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新したコードベースをデプロイする必要があります。Steps for updating the code base to work in the target version of AEM can be found in [Upgrade Code and Customizations page](/help/sites-deploying/upgrading-code-and-customizations.md).

## アップグレード後のチェックおよびトラブルシューティングの実行 {#perform-post-upgrade-check-troubleshooting}

[アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を参照してください。
