---
title: アプリケーションサーバーのインストール環境のアップグレード手順
seo-title: アプリケーションサーバーのインストール環境のアップグレード手順
description: アプリケーションサーバーからデプロイされる AEM のインスタンスのアップグレード方法について説明します。
seo-description: アプリケーションサーバーからデプロイされる AEM のインスタンスのアップグレード方法について説明します。
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 95%

---


# アプリケーションサーバーのインストール環境のアップグレード手順{#upgrade-steps-for-application-server-installations}

ここでは、アプリケーションサーバーインストール用の AEM を更新するために必要になる手順を説明します。

この手順では、どの例でも JBoss をアプリケーションサーバーとして使用し、有効な AEM のバージョンが既にデプロイされているものとします。ここでは、**AEM バージョン 5.6 から 6.3** へのアップグレードについて説明します。

1. 最初に、JBoss を起動します。ほとんどの状況で、`standalone.sh` 起動スクリプトを実行することで起動できます。そのためには、ターミナルから次のコマンドを実行します。

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. AEM 5.6 が既にデプロイされている場合は、次のコマンドを実行してバンドルが正常に動作していることを確認します。

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 次に、AEM 5.6 のデプロイを解除します。

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. JBoss を停止します。

1. 次に、crx2oak 移行ツールを使用してリポジトリを移行します。

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >この例では、oak-repository は、新しく変換されたリポジトリが配置される一時ディレクトリです。この手順を実行する前に、crx2oak.jar が最新バージョンであることを確認してください。

1. 次の操作をおこなって、sling.properties ファイル内の必要なプロパティを削除します。

   1. Open the file located at `crx-quickstart/launchpad/sling.properties`
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

   * **base.jarファイル**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * The **BootstrapCommandFile_timestamp.txt file**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. 新しく移行された segmentstore を適切な場所にコピーします。

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. datastore もコピーします。

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. 次に、アップグレード後の新しいインスタンスで使用する OSGi 設定を格納するためのフォルダーを作成する必要があります。具体的には、install というフォルダーを **crx-quickstart** の下に作成する必要があります。

1. 次に、AEM 6.3 で使用されるノードストアとデータストアを作成します。そのためには、次の名前を持つ 2 つのファイルを **crx-quickstart\install** の下に作成します。

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   この 2 つのファイルにより、AEM が TarMK ノードストアとファイルデータストアを使用するように設定されます。

1. 設定ファイルを編集し、使用できる状態にします。具体的には、次のように編集します。

   * Add the following line to **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:\
      `customBlobStore=true`

   * Then add the following lines to **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. 次のコマンドを実行して crx2 実行モードを削除します。

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. 今度は、AEM 6.3 war ファイル内の実行モードを変更する必要があります。変更するには、まず AEM 6.3 war を格納する一時フォルダーを作成します。次の例のフォルダー名は、**temp** です。war ファイルをコピーしたら、temp フォルダー内で次のコマンドを実行して、内容を抽出します。

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. 内容を抽出したら、**WEB-INF** フォルダーに移動して `web.xml` ファイルを編集し、実行モードを変更します。XML での実行モードの設定場所を探すには、`sling.run.modes` 文字列を検索します。見つかったら、コードの次の行で実行モードを変更します。デフォルトでは、author に設定されています。

   ```shell
   <param-value >author</param-value>
   ```

1. 上述の author という値を変更し、実行モードを author,crx3,crx3tar に設定します。最終的なコードブロックは次のようになります。

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 編集後の内容で jar を再作成します。

   ```shell
   jar cvf aem62.war
   ```

1. 最後に、新しい war ファイルをデプロイします。

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

