---
title: IntelliJ IDEA を使用して AEM プロジェクトを開発する方法
description: IntelliJ IDEA を使用したAEMプロジェクトの開発
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 48%

---

# IntelliJ IDEA を使用して AEM プロジェクトを開発する方法{#how-to-develop-aem-projects-using-intellij-idea}

## 概要 {#overview}

IntelliJ でのAEM開発を開始するには、次の手順が必要です。

各手順について、このトピックの後半で詳しく説明します。

* IntelliJ のインストール
* Maven に基づいてAEMプロジェクトをセットアップする
* Maven POM での IntelliJ 用の JSP サポートの準備
* IntelliJ への Maven プロジェクトの読み込み

>[!NOTE]
>
>このガイドは、IntelliJ IDEA Ultimate Edition 12.1.4 およびAEM 5.6.1 に基づいています。

### IntelliJ IDEA のインストール {#install-intellij-idea}

次から IntelliJ IDEA をダウンロード： [JetBrains のダウンロードページ](https://www.jetbrains.com/idea/download/).

次に、このページのインストール手順に従います。

### Maven に基づいてAEMプロジェクトをセットアップする {#set-up-your-aem-project-based-on-maven}

次に、[Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)に記載されている手順に従って、Maven を使用してプロジェクトを設定します。

IntelliJ IDEA でAEMプロジェクトの操作を開始するには、 [5 分ではじめに](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) で十分です。

### IntelliJ IDEA 用の JSP サポートの準備 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA は、JSP での作業にも対応しています。次に例を示します。

* タグライブラリの自動補完
* `<cq:defineObjects />` と `<sling:defineObjects />` で定義されたオブジェクトの認知

サポートを有効にするには、[Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)の [JSP を使用する方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)に記載されている手順に従います。

### Maven プロジェクトの読み込み {#import-the-maven-project}

1. 次の手順を使用して、IntelliJ IDEA で&#x200B;**読み込み**&#x200B;ダイアログを開きます。

   * プロジェクトを開いていない場合は、ようこそ画面の「**プロジェクトを読み込む**」を選択します。
   * メインメニューから&#x200B;**ファイル／プロジェクトをインポート**&#x200B;を選択します。

1. 読み込みダイアログで、プロジェクトの POM ファイルを選択します。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 次のダイアログに示すデフォルト設定を使用して続行します。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 以降のダイアログで繰り返し「**次へ**」をクリックし、最後に「**終了**」をクリックします。
1. これで、IntelliJ IDEA を使用した AEM 開発用の設定は完了です。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### IntelliJ IDEA を使用した JSP のデバッグ {#debugging-jsps-with-intellij-idea}

IntelliJ IDEA で JSP をデバッグするには、次の手順が必要です

* プロジェクトでの Web ファセットの設定
* JSR45 サポートプラグインのインストール
* デバッグプロファイルの設定
* デバッグモード用のAEMの設定

#### プロジェクトでの Web ファセットの設定 {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA は、デバッグ用の JSP をどこで見つけるかを理解する必要があります。 IDEA は `content-package-maven-plugin` 設定を使用する場合は、手動で設定する必要があります。

1. **ファイル／プロジェクト構造**&#x200B;に移動します。
1. 「**コンテンツ**」モジュールを選択します。
1. モジュールのリストの上にある「**+**」をクリックして、「**Web**」を選択します。
1. 「Web リソースディレクトリ」として、 `content/src/main/content/jcr_root subdirectory` 以下のスクリーンショットに示すように、プロジェクトの。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### JSR45 サポートプラグインのインストール {#install-the-jsr-support-plugin}

1. IntelliJ IDEA 設定の&#x200B;**プラグイン**&#x200B;ウィンドウに移動します。
1. 「**JSR45 Integration**」プラグインに移動して、その横にあるチェックボックスをオンにします。
1. 「**適用**」をクリックします。
1. 再起動するよう要求されたら、IntelliJ IDEA を再起動します。

![chlimage_1-49](assets/chlimage_1-49a.png)

#### デバッグプロファイルの設定 {#configure-a-debug-profile}

1. **実行／設定を編集**&#x200B;に移動します。
1. 「**+**」をクリックして「**JSR45 Remote**」を選択します。
1. 設定ダイアログで、「**アプリケーションサーバー**」の横にある「**設定**」を選択して、Generic サーバーを設定します。
1. デバッグの開始時にブラウザーを開く場合は、開始ページを適切な URL に設定します。
1. vlt autosync を使用する場合は、「**起動前**」タスクをすべて削除します。使用しない場合は、適切な Maven タスクを設定します。
1. の **起動/接続** パネル、必要に応じてポートを調整
1. IntelliJ IDEA が提案するコマンドライン引数をコピーする

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### デバッグモード用のAEMの設定 {#configure-aem-for-debug-mode}

最後に必要な手順は、IntelliJ IDEA が提案する JVM オプションでAEMを起動することです。

AEM jar ファイルを直接起動し、次のコマンドラインなどを使用して、これらのオプションを追加します。

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

また、次に示すように、`crx-quickstart/bin/start` の起動スクリプトにこれらのオプションを追加することもできます。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### デバッグを開始 {#start-debugging}

これで、AEMでの JSP のデバッグ用に設定されました。

1. **実行／デバッグ／デバッグプロファイル**&#x200B;を選択します。
1. コンポーネントコードにブレークポイントを設定する
1. ブラウザーでページにアクセスする

![chlimage_1-52](assets/chlimage_1-52a.png)

### IntelliJ IDEA によるバンドルのデバッグ {#debugging-bundles-with-intellij-idea}

バンドル内のコードは、標準の汎用リモートデバッグ接続を使用してデバッグできます。 次の手順を実行できます。 [リモートデバッグに関する Jetbrain ドキュメント](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
