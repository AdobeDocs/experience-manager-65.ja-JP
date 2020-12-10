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
source-git-commit: f696b1081f14ba379cde51a3542a5b1b5f9668e2
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 67%

---


# アプリケーションサーバーのインストール環境のアップグレード手順{#upgrade-steps-for-application-server-installations}

ここでは、アプリケーションサーバーインストール用の AEM を更新するために必要になる手順を説明します。

この手順の例では、アプリケーションサーバーとしてTomcatを使用し、AEMの稼働バージョンが既にデプロイされていることを示しています。 ここでは、**AEM バージョン 6.4 から 6.5** へのアップグレードについて説明します。

1. まず、開始のトムキャット。 ほとんどの場合、`./catalina.sh`開始の起動スクリプトを実行し、ターミナルから次のコマンドを実行することで、これを行うことができます。

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. AEM 6.4が既にデプロイされている場合は、次のリンクにアクセスして、バンドルが正しく機能していることを確認してください。

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 次に、AEM 6.4のデプロイを解除します。これはTomCat App Manager (`http://serveraddress:serverport/manager/html`)から実行できます。

1. 次に、crx2oak移行ツールを使用してリポジトリを移行します。 これを行うには、[この](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak)からcrx2oakの最新バージョンをダウンロードしてください。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 次の操作をおこなって、sling.properties ファイル内の必要なプロパティを削除します。

   1. `crx-quickstart/launchpad/sling.properties`にあるファイルを開きます
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

   * **base.jarファイル**:`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txtファイル**:`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * **sling.options.file**&#x200B;を次を実行して削除します。`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 次に、AEM 6.5 で使用されるノードストアとデータストアを作成します。そのためには、次の名前を持つ 2 つのファイルを `crx-quickstart\install` の下に作成します。

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   この 2 つのファイルにより、AEM が TarMK ノードストアとファイルデータストアを使用するように設定されます。

1. 設定ファイルを編集し、使用できる状態にします。具体的には、次のように編集します。

   * 追加`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`に次の行を追加します。

      ```customBlobStore=true```

   * 次に、`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`に次の行を追加します。

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

1. 上記の作成者値を変更し、実行モードを次のように設定します。`author,crx3,crx3tar`.コードの最後のブロックは次のようになります。

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

1. 最後に、新しいwarファイルをTomCatに展開します。
