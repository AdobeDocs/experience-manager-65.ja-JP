---
title: IntelliJ IDEA を使用して AEM プロジェクトを開発する方法
seo-title: IntelliJ IDEA を使用して AEM プロジェクトを開発する方法
description: IntelliJ IDEA を使用した AEM プロジェクトの開発
seo-description: IntelliJ IDEA を使用した AEM プロジェクトの開発
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 64%

---


# IntelliJ IDEA を使用して AEM プロジェクトを開発する方法{#how-to-develop-aem-projects-using-intellij-idea}

## 概要 {#overview}

IntelliJ で AEM の開発を開始するには、次の手順を実行する必要があります。

各手順の詳細については、このページで後述します。

* IntelliJ のインストール
* Maven に基づく AEM プロジェクトの設定
* Maven POM での IntelliJ 用の JSP サポートの準備
* IntelliJ への Maven プロジェクトの読み込み

>[!NOTE]
>
>このガイドは IntelliJ IDEA Ultimate Edition 12.1.4 と AEM 5.6.1 を基に作成されています。

### IntelliJ IDEA のインストール {#install-intellij-idea}

[JetBrains のダウンロードページ](https://www.jetbrains.com/idea/download/index.html)から IntelliJ IDEA をダウンロードします。

そのページのインストール手順に従ってください。

### Maven に基づく AEM プロジェクトの設定 {#set-up-your-aem-project-based-on-maven}

Next, set up your project using Maven as described in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

To start working with AEM projects in IntelliJ IDEA, the basic setup in [Getting Started in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) is sufficient.

### IntelliJ IDEA 用の JSP サポートの準備 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA では JSP との連携もサポートされます。サポートされる項目の例を次に示します。

* タグライブラリのオートコンプリート
* awareness of objects defined by `<cq:defineObjects />` and `<sling:defineObjects />`

For that to work, follow the instructions on [How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Maven プロジェクトの読み込み {#import-the-maven-project}

1. Open the **Import** dialog in IntelliJ IDEA by

   * selecting **Import Project** on the welcome screen if you have no project open yet
   * selecting **File -> Import Project** from the main menu

1. Import ダイアログで、プロジェクトの POM ファイルを選択します。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 次のダイアログに示すデフォルト設定を使用して続行します。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continue through the following dialogs by clicking **Next** and **Finish**.
1. これで、IntelliJ IDEA を使用した AEM 開発用の設定は完了です。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### IntelliJ IDEA による JSP のデバッグ {#debugging-jsps-with-intellij-idea}

IntelliJ IDEA を使用して JSP をデバッグするには、次の手順をおこなう必要があります。

* プロジェクトでの Web ファセットの設定
* JSR45 サポートプラグインのインストール
* デバッグプロファイルの設定
* デバッグモード用の AEM の設定

#### プロジェクトでの Web ファセットの設定 {#set-up-a-web-facet-in-the-project}

デバッグ用の JSP を検索する場所を IntelliJ IDEA で認識する必要があります。IDEA では `content-package-maven-plugin` 設定を解釈できないので、これを手動で設定する必要があります。

1. Go to **File -> Project Structure**
1. Select the **Content** module
1. Click **+** above the list of modules and select **Web**
1. Webリソースディレクトリとして、下のスクリーンショットに示すように、プロジェクト `content/src/main/content/jcr_root subdirectory` の対象を選択します。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### JSR45 サポートプラグインのインストール {#install-the-jsr-support-plugin}

1. Go to the **Plugins** pane in the IntelliJ IDEA settings
1. Navigate to the **JSR45 Integration** Plugin and select the check box next to it
1. Click **Apply**
1. 再起動するよう要求されたら、IntelliJ IDEA を再起動します。

![chlimage_1-49](assets/chlimage_1-49a.png)

#### デバッグプロファイルの設定 {#configure-a-debug-profile}

1. Go to **Run -> Edit Configurations**
1. Hit the **+** and select **JSR45 Remote**
1. In the configuration dialog, select **Configure** next to **Application Server** and configure a Generic server
1. デバッグの開始時にブラウザーを開く場合は、開始ページを適切な URL に設定します。
1. Remove all **Before launch** tasks if you use vlt autosync, or configure appropriate Maven tasks if you don&#39;t
1. On the **Startup/Connection** pane, adjust the port if required
1. IntelliJ IDEA が処理するコマンドライン引数をコピーします。

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### デバッグモード用の AEM の設定 {#configure-aem-for-debug-mode}

必要な最後の手順は、IntelliJ IDEA が推奨する JVM オプションを指定して AEM を起動することです。

そのためには、AEM jar ファイルを直接起動して、これらのオプションを追加します。例えば、次のコマンドラインを使用します。

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

また、次に示すように、`crx-quickstart/bin/start` の起動スクリプトにこれらのオプションを追加することもできます。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### デバッグの開始 {#start-debugging}

これで、AEM における JSP のデバッグ用の設定はすべて完了です。

1. Select **Run -> Debug -> Your Debug Profile**
1. コンポーネントのコードにブレークポイントを設定します。
1. ブラウザーでページにアクセスします。

![chlimage_1-52](assets/chlimage_1-52a.png)

### IntelliJ IDEA によるバンドルのデバッグ {#debugging-bundles-with-intellij-idea}

標準の汎用リモートデバッグ接続を使用して、バンドル内のコードをデバッグできます。[リモートデバッグに関する Jetbrain のドキュメント](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)の手順に従ってください。
