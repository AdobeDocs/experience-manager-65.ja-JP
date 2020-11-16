---
title: 実行モード
seo-title: 実行モード
description: 実行モードを使用して、固有の目的に合わせて AEM インスタンスを調整する方法を学習します。
seo-description: 実行モードを使用して、固有の目的に合わせて AEM インスタンスを調整する方法を学習します。
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 73%

---


# 実行モード{#run-modes}

実行モードを使用すると、オーサーまたはパブリッシュ、テスト、開発、イントラネットなど、特定の目的に合わせて AEM インスタンスを調整できます。

以下の操作を実行できます。

* [各実行モードに対して設定パラメーターのコレクションを定義します](#defining-configuration-properties-for-a-run-mode)。

   すべての実行モードに対して基本的な設定パラメーターのセットが適用され、特定の環境の目的に合わせて追加のセットを調整できます。 これらは、必要に応じて適用されます。

* [特定のモード用にインストールする追加のバンドルを定義します](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

設定および定義はすべて 1 つのリポジトリに格納され、**実行モード**&#x200B;を設定することによってアクティベートされます。

## Installation Run Modes {#installation-run-modes}

インストール（固定）実行モードは、インストール時に使用され、インスタンスの全期間にわたって固定されます。変更はできません。

インストール実行モードは標準で提供されています。

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

これらは相互に排他的な実行モードの 2 つのペアです。例えば、次のことが可能です。

* define either `author` or `publish`, not both at the same time

* combine `author` with either `samplecontent` or `nosamplecontent` (but not both)

>[!CAUTION]
>
>上記のいずれかの実行モード（author、publish、samplecontent、nosamplecontent）を使用するときは、インストール時に使用する値が、そのインストールの全期間&#x200B;**&#x200B;の実行モードを定義します。
>
>これらの実行モードは、インストール後は変更できません&#x200B;**。

## カスタマイズされた実行モード {#customized-run-modes}

独自のカスタマイズされた実行モードも作成できます。これらを組み合わせて次のようなシナリオに対応できます。

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 必要に応じて使用

カスタマイズされた実行モードは、起動のたびに選択することもできます。

## samplecontent および nosamplecontent の使用 {#using-samplecontent-and-nosamplecontent}

これらのモードでは、サンプルコンテンツの使用を制御できます。サンプルコンテンツは、クイックスタートの構築前に定義され、パッケージや設定を含めることができます。

* `samplecontent` 実行モードでは、サンプルコンテンツがインストールされます（デフォルトモード）。

* `nosamplecontent` モードでは、サンプルコンテンツはインストールされません。

nosamplecontent 実行モードは、実稼働インストール用に設計されています。

## 実行モードの設定プロパティの定義 {#defining-configuration-properties-for-a-run-mode}

特定の実行モードに使用する設定プロパティの値をまとめてリポジトリに保存できます。

実行モードは、フォルダー名のサフィックスで示されます。これにより、すべての設定を 1 つのリポジトリに格納できます。次に例を示します。

* `config`

   すべての実行モードに適用可能

* `config.author`

   作成者の実行モードに使用

* `config.publish`

   公開実行モードに使用

* `config.<run-mode>`

   該当する実行モードで使用されます。例えば、config

これらのフォルダー内で個々の設定ノードを定義する方法、および複数の実行モードの組み合わせに関する設定を作成する方法について詳しくは、[リポジトリでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を参照してください。

>[!NOTE]
>
>[インストール実行モード](#installation-run-modes)（オーサーなど）に関しては、インストール後は実行モードを変更できません。ただし、個々の設定プロパティの変更は、再起動時に有効になります。

## 特定の実行モード用にインストールする追加のバンドルの定義 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

特定の実行モードに対してインストールする必要のある追加のバンドルも指定できます。 これらの定義では、バンドルの保持にインストールフォルダーが使用されます。 再び、実行モードは、プレフィックスで示されます。

* `install.author`
* `install.publish`

これらのフォルダーは、タイプが `nt:folder` であり、適切なバンドルを含む必要があります。

## 特定の実行モードでの CQ の起動 {#starting-cq-with-a-specific-run-mode}

複数の実行モードの設定を定義した場合は、起動時にどれを使用するかを定義する必要があります。使用する実行モードを指定する方法は複数あります。優先順位は次のとおりです。

1. [ `sling.properties` file](#using-the-sling-properties-file)
1. [ `-r` オプション](#using-the-r-option)
1. [システムのプロパティ(`-D`)](#using-a-system-property-in-the-start-script)

1. [ファイル名検出](#filename-detection-renaming-the-jar-file)

アプリケーションサーバーを使用している場合は、[web.xml](#defining-the-run-mode-in-web-xml-with-application-server) で実行モードを定義することもできます。

### sling.properties ファイルの使用 {#using-the-sling-properties-file}

`sling.properties` ファイルを使用して必要な実行モードを定義できます。

1. 設定ファイルを編集します。

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 追加次のプロパティ次に示すのは、authorの例です。

   `sling.run.modes=author`

### -r オプションの使用{#using-the-r-option}

カスタム実行モードは、quickstartの起動時に `-r` オプションを使用してアクティブ化できます。 例えば、実行モードがdevに設定されたAEMインスタンスを起動するには、次のコマンドを使用します。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 起動スクリプトのシステムプロパティを使用 {#using-a-system-property-in-the-start-script}

起動スクリプトのシステムプロパティを使用して実行モードを指定できます。

* 例えば、次の例を使用して、米国にある実稼働用発行インスタンスとしてインスタンスを起動します。

   `-Dsling.run.modes=publish,prod,us`

### ファイル名検出 - jar ファイルの名前変更 {#filename-detection-renaming-the-jar-file}

次の2つのインストール実行モードは、インストール前にインストールjarファイルの名前を変更することでアクティブ化できます。

* publish
* 作成者

jar ファイルでは、次の命名規則を使用する必要があります。

`cq5-<run-mode>-p<port-number>`

例えば、`publish` 実行モードを設定するには、jar ファイルの名前を次のように変更します。

`cq5-publish-p4503`

### Defining the run mode in web.xml (with Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

アプリケーションサーバーを使用している場合は、

`sling.run.modes`

プロパティを、次のファイル内で設定することもできます。

`WEB-INF/web.xml`

これは AEM の `war` ファイル内にあり、デプロイメントの前に更新する必要があります。

詳しくは、[AEM をアプリケーションサーバーと共にインストール](/help/sites-deploying/application-server-install.md)を参照してください。
