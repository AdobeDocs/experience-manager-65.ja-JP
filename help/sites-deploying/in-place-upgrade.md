---
title: インプレースアップグレードの実行
description: インプレースアップグレードの実行方法を説明します。
topic-tags: upgrading
feature: Upgrading
exl-id: aef6ef00-993c-4252-b0ad-ddc4917beaf7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 47%

---

# インプレースアップグレードの実行{#performing-an-in-place-upgrade}

>[!NOTE]
>
>このページでは、AEM 6.5 のアップグレード手順について説明します。アプリケーションサーバーにデプロイされているインストールがある場合は、 [アプリケーションサーバーインストールのアップグレード手順](/help/sites-deploying/app-server-upgrade.md).

## アップグレード前の手順 {#pre-upgrade-steps}

アップグレードを実行する前に、いくつかの手順を完了する必要があります。 詳しくは、 [コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md) および [アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) を参照してください。 さらに、お使いのシステムが新しいバージョンのAEMの要件を満たしていることを確認します。 パターン検出を使用して、アップグレードの複雑さを推定する方法を確認します。また、 [アップグレードの計画](/help/sites-deploying/upgrade-planning.md) を参照してください。

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 移行の前提条件 {#migration-prerequisites}

* **必要な Java の最小バージョン：** 移行ツールは、Java バージョン 7 以降でのみ機能します。 AEM 6.3 以上では、サポートされているバージョンは Oracle の JRE 8 と IBM の JRE 7 および 8 のみです。

* **アップグレードされたインスタンス：** バージョンからアップグレードする場合 **5.6 より古い**&#x200B;アップグレードに関するドキュメントの 6.0 バージョンに記載されている手順に従って、AEM 6.0 へのインプレースアップグレードを必ず実行してください。

## AEM クイックスタート jar ファイルの準備 {#prep-quickstart-file}

1. インスタンスが実行中である場合は停止します。

1. 新しい AEM jar ファイルをダウンロードし、それを使用して `crx-quickstart` フォルダーの外部にある古いファイルを置き換えます。

1. 次のコマンドを実行して新しいクイックスタート jar を解凍します。

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## コンテンツリポジトリの移行 {#content-repository-migration}

AEM 6.3 からアップグレードする場合は、この移行は必要ありません。6.3 より前のAdobeでは、AEM 6.3 に存在する Oak Segment Tar の新しいバージョンにリポジトリを移行するために使用できるツールが提供されています。これはクイックスタートパッケージの一部として提供され、TarMK を使用するアップグレードに必須です。 MongoMK を使用している環境のアップグレードには、リポジトリの移行は必要ありません。 新しい Segment Tar 形式の利点について詳しくは、 [Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

実際の移行は、標準の AEM クイックスタート jar ファイルを使用して行います。この jar ファイルは、新しい `-x crx2oak` オプションを指定して実行します。このオプションにより crx2oak ツールが実行され、アップグレードが容易になり、より堅牢になります。

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
   <td>以下の「トラブルシューティング」の節を参照してください。</td>
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
   <td>以下の「トラブルシューティング」の節を参照してください。</td>
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

* Java のメモリマッピングが正しく処理されない Windows システムでアップグレードを行う場合は、`--disable-mmap`パラメーターをコマンドに追加してください。

crx2oak ツールの使用に関する追加の手順については、 [CRX2Oak 移行ツール](/help/sites-deploying/using-crx2oak.md). crx2oak ヘルパー JAR は、必要に応じて手動でアップグレードできます。その場合は、クイックスタートを展開した後に、手動で新しいバージョンに置き換えます。 AEMインストールフォルダー内の場所は次のとおりです。 `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. 最新バージョンの CRX2Oak 移行ツールは、アドビリポジトリ（[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)）からダウンロードできます。

移行が正常に完了すると、ツールは終了コード 0 で終了します。さらに、AEM インストールディレクトリの `crx-quickstart/logs` にある `upgrade.log` ファイルで WARN および ERROR メッセージがないかどうかを確認してください。これらのメッセージは、移行中に発生した致命的ではないエラーを示している場合があります。

`crx-quickstart/install`フォルダーにある設定ファイルを確認します。移行が必要な場合は、ターゲットリポジトリを反映するように更新されます。

**データストアに関する注意：**

AEM 6.3 インストールでは新しく `FileDataStore` がデフォルトになっていますが、外部データストアの使用は必須ではありません。実稼動デプロイメントのベストプラクティスとして、外部データストアを使用することをお勧めしますが、アップグレードの前提条件ではありません。 AEMのアップグレードには既に複雑さが伴うので、Adobeでは、データストアの移行をおこなわずにアップグレードを実行することをお勧めします。 必要に応じて、後でデータストアの移行を個別の作業として実行できます。

## 移行に関する問題のトラブルシューティング {#troubleshooting-migration-issues}

6.3 からアップグレードする場合は、この節をスキップしてください。提供された crx2oak プロファイルは、ほとんどの顧客のニーズを満たす必要がありますが、追加のパラメーターが必要な場合があります。 移行中にエラーが発生した場合は、環境の中に追加の設定オプションの提供が必要な要素が存在する可能性があります。 その場合は、次のエラーが発生する可能性があります。

**外部データストアが指定されていないので、チェックポイントはコピーされません。 これにより、最初の起動時にリポジトリ全体のインデックスが再作成されます。 —skip-checkpoints を使用して強制的に移行します。詳しくは、https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migrationを参照してください。**

何らかの理由で、移行プロセスはデータストア内のバイナリにアクセスする必要があり、見つかりません。 データストア設定を指定するには、移行コマンドの `<<ADDITIONAL_FLAGS>>` 部分に以下のフラグを挿入します。

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

**S3 を使用する場合：**

1. 以前のバージョンの S3 コネクタに関連する、`crx-quickstart/install` 内の jar を削除します。

1. [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) から 1.10.x S3 コネクタの最新リリースをダウンロードします。

1. パッケージを一時フォルダーに抽出し、`jcr_root/libs/system/install` の内容を `crx-quickstart/install` フォルダーにコピーします。

### 適切なアップグレード開始コマンドの確認 {#determining-the-correct-upgrade-start-command}

アップグレードを実行するには、jar ファイルを使用してAEMを起動し、インスタンスを起動することが重要です。 6.5 にアップグレードする場合は、アップグレードコマンドで選択できる[遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)のその他のコンテンツ再構築および移行オプションも検討してください。

>[!IMPORTANT]
>
>Oracle Java 11（または一般にバージョン 8 より新しい Java）を実行している場合は、AEM の起動時にコマンドラインにさらにスイッチを追加する必要があります。詳しくは、 [Java 11 に関する考慮事項](/help/sites-deploying/custom-standalone-install.md#java-considerations)を参照してください。

開始スクリプトからAEMを起動しても、アップグレードは開始されません。 ほとんどのお客様は、起動スクリプトを使用してAEMを起動し、この起動スクリプトをカスタマイズして、メモリ設定、セキュリティ証明書などの環境設定用のスイッチを含めています。 このため、Adobeでは、適切なアップグレードコマンドを判断するために、次の手順に従うことを推奨します。

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

   これにより、適切なメモリ設定、カスタム実行モード、その他の環境パラメーターがすべてアップグレードに適用されます。 アップグレードが完了した後、今後の起動時に開始スクリプトからインスタンスを起動できます。

## アップグレードされたコードベースのデプロイ {#deploy-upgraded-codebase}

インプレースアップグレードプロセスが完了したら、更新されたコードベースをデプロイする必要があります。 ターゲットバージョンの AEM で動作するようにコードベースを更新するための手順については、[コードおよびカスタマイズのアップグレード](/help/sites-deploying/upgrading-code-and-customizations.md)のページを参照してください。

## アップグレード後のチェックとトラブルシューティングの実行 {#perform-post-upgrade-check-troubleshooting}

詳しくは、 [アップグレード後のチェックとトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
