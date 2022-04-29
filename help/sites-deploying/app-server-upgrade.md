---
title: アプリケーションサーバーのインストール環境のアップグレード手順
description: アプリケーションサーバーからデプロイされる AEM のインスタンスのアップグレード方法について説明します。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: 5e875e0420540ca209e7d677046e8d010ae4e145
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 98%

---

# アプリケーションサーバーのインストール環境のアップグレード手順{#upgrade-steps-for-application-server-installations}

ここでは、アプリケーションサーバーインストール用の AEM を更新するために必要になる手順を説明します。

この手順では、どの例でも JBoss をアプリケーションサーバーとして使用し、有効な AEM のバージョンが既にデプロイされているものとします。ここでは、**AEM バージョン 6.4 から 6.5** へのアップグレードについて説明します。

1. まず、TomCat を起動してください。 ほとんどの状況で、`./catalina.sh` 起動スクリプトを実行することで起動できます。このために、ターミナルから次のコマンドを実行します。

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM 6.4 が既にデプロイされている場合は、以下にアクセスしてバンドルが正常に動作していることを確認します。

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 次に、AEM 6.4 のデプロイを解除します。これは、TomCat App Manager（`http://serveraddress:serverport/manager/html`）から実行できます。

1. 次に、crx2oak 移行ツールを使用してリポジトリを移行してください。これをおこなうには、crx2oak の最新バージョンを [この場所](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/) からダウンロードしてください。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 次の操作をおこなって、sling.properties ファイル内の必要なプロパティを削除します。

   1. `crx-quickstart/launchpad/sling.properties` に置かれたファイルを開きます。
   1. 次のプロパティを削除してファイルを保存します。

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 不要なファイルとフォルダーを削除します。具体的に削除する必要のある項目は次のとおりです。

   * **launchpad/startup フォルダー**：ターミナルで次のコマンドを実行して削除できます。`rm -rf crx-quickstart/launchpad/startup`

   * **base.jar ファイル**：`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt ファイル**：`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * **sling.options.file** を以下を実行することにより削除します：`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 次に、AEM 6.5 で使用されるノードストアとデータストアを作成します。そのためには、次の名前を持つ 2 つのファイルを `crx-quickstart\install` の下に作成します。

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   この 2 つのファイルにより、AEM が TarMK ノードストアとファイルデータストアを使用するように設定されます。

1. 設定ファイルを編集し、使用できる状態にします。具体的には、次のように編集します。

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` に次の行を追加します。

      `customBlobStore=true`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` に次の行を追加します。

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 今度は、AEM 6.5 war ファイル内の実行モードを変更する必要があります。変更するには、まず AEM 6.5 war を格納する一時フォルダーを作成します。次の例のフォルダー名は、`temp` です。war ファイルをコピーしたら、temp フォルダー内で次のコマンドを実行して、内容を抽出します。

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 内容を抽出したら、**WEB-INF** フォルダーに移動して web.xml ファイルを編集し、実行モードを変更します。XML での実行モードの設定場所を探すには、`sling.run.modes` 文字列を検索します。見つかったら、コードの次の行で実行モードを変更します。デフォルトでは、author に設定されています。

   ```bash
   <param-value >author</param-value>
   ```

1. 上述の author という値を変更し、実行モードを `author,crx3,crx3tar` に設定します。最終的なコードブロックは次のようになります。

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 編集後の内容で jar を再作成します。

   ```bash
   jar cvf aem65.war
   ```

1. 最後に、TomCat に新しい war ファイルをデプロイします。
