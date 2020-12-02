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

### IntelliJ IDEA のインストール  {#install-intellij-idea}

[JetBrains のダウンロードページ](https://www.jetbrains.com/idea/download/index.html)から IntelliJ IDEA をダウンロードします。

そのページのインストール手順に従ってください。

### Maven に基づく AEM プロジェクトの設定  {#set-up-your-aem-project-based-on-maven}

次に、[Apache Mavenを使用したAEMプロジェクトの構築方法](/help/sites-developing/ht-projects-maven.md)の説明に従って、Mavenを使用してプロジェクトを設定します。

IntelliJ IDEAでAEMプロジェクトを開始するには、[5分後のはじめに](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)の基本設定で十分です。

### IntelliJ IDEA 用の JSP サポートの準備 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA では JSP との連携もサポートされます。サポートされる項目の例を次に示します。

* タグライブラリのオートコンプリート
* `<cq:defineObjects />`と`<sling:defineObjects />`で定義されるオブジェクトの認識

この機能を動作させるには、[How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md)の[How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)の手順に従ってください。

### Maven プロジェクトの読み込み {#import-the-maven-project}

1. IntelliJ IDEAの&#x200B;**インポート**&#x200B;ダイアログを開く

   * まだプロジェクトを開いていない場合は、ようこそ画面で「**プロジェクトを読み込み**」を選択
   * メインメニューから&#x200B;**ファイル —>プロジェクト**&#x200B;を読み込むを選択

1. Import ダイアログで、プロジェクトの POM ファイルを選択します。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 次のダイアログに示すデフォルト設定を使用して続行します。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. **次へ**&#x200B;と&#x200B;**完了**&#x200B;をクリックして、次のダイアログを続けます。
1. これで、IntelliJ IDEA を使用した AEM 開発用の設定は完了です。

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### IntelliJ IDEA による JSP のデバッグ {#debugging-jsps-with-intellij-idea}

IntelliJ IDEA を使用して JSP をデバッグするには、次の手順をおこなう必要があります。

* プロジェクトでの Web ファセットの設定
* JSR45 サポートプラグインのインストール
* デバッグプロファイルの設定
* デバッグモード用の AEM の設定

#### プロジェクトでの Web ファセットの設定  {#set-up-a-web-facet-in-the-project}

デバッグ用の JSP を検索する場所を IntelliJ IDEA で認識する必要があります。IDEA では `content-package-maven-plugin` 設定を解釈できないので、これを手動で設定する必要があります。

1. **ファイル —>プロジェクト構造**&#x200B;に移動
1. **コンテンツ**&#x200B;モジュールを選択
1. モジュールのリストの上の&#x200B;**+**&#x200B;をクリックし、**Web**&#x200B;を選択します
1. Webリソースディレクトリとして、次のスクリーンショットに示すように、プロジェクトの`content/src/main/content/jcr_root subdirectory`を選択します。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### JSR45 サポートプラグインのインストール {#install-the-jsr-support-plugin}

1. IntelliJ IDEA設定の&#x200B;**プラグイン**&#x200B;ウィンドウに移動します
1. **JSR45統合**&#x200B;プラグインに移動し、その横のチェックボックスを選択します
1. 「**適用**」をクリックします
1. 再起動するよう要求されたら、IntelliJ IDEA を再起動します。

![chlimage_1-49](assets/chlimage_1-49a.png)

#### デバッグプロファイルの設定 {#configure-a-debug-profile}

1. **実行 —>設定の編集**&#x200B;に移動
1. **+**&#x200B;を押し、**JSR45 Remote**&#x200B;を選択します。
1. 設定ダイアログで、「**アプリケーションサーバー**」の横の「**設定**」を選択し、汎用サーバーを設定します
1. デバッグの開始時にブラウザーを開く場合は、開始ページを適切な URL に設定します。
1. vlt autosyncを使用する場合は、すべての&#x200B;**起動前**&#x200B;タスクを削除し、使用しない場合は適切なMavenタスクを設定します
1. **Startup/Connection**&#x200B;ペインで、必要に応じてポートを調整します
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

1. [**実行 —>デバッグ —>デバッグプロファイル**]を選択します。
1. コンポーネントのコードにブレークポイントを設定します。
1. ブラウザーでページにアクセスします。

![chlimage_1-52](assets/chlimage_1-52a.png)

### IntelliJ IDEA によるバンドルのデバッグ {#debugging-bundles-with-intellij-idea}

標準の汎用リモートデバッグ接続を使用して、バンドル内のコードをデバッグできます。[リモートデバッグに関する Jetbrain のドキュメント](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)の手順に従ってください。
