---
title: 実行モード
seo-title: Run Modes
description: 実行モードを使用して、固有の目的に合わせて AEM インスタンスを調整する方法を学習します。
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 100%

---

# 実行モード{#run-modes}

実行モードを使用すると、オーサーまたはパブリッシュ、テスト、開発、イントラネットなど、特定の目的に合わせて AEM インスタンスを調整できます。

以下の操作を実行できます。

* [各実行モードに対する設定パラメーターのコレクションを定義する](#defining-configuration-properties-for-a-run-mode)。

   すべての実行モードに対して基本的な設定パラメーターのセットが適用され、特定の環境の目的に合わせて追加のセットを調整できます。これらは必要に応じて適用されます。

* [特定のモード用にインストールする追加のバンドルを定義する](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

設定および定義はすべて 1 つのリポジトリに格納され、**実行モード**&#x200B;を設定することによってアクティベートされます。

## インストール実行モード {#installation-run-modes}

インストール（固定）実行モードは、インストール時に使用され、インスタンスの全期間にわたって固定されます。変更はできません。

インストール実行モードは標準で提供されています。

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

これらは相互に排他的な実行モードの 2 つのペアです。例えば、次のことが可能です。

* `author` または `publish` を定義できますが、両方を同時に定義することはできません。

* `author` を `samplecontent` または `nosamplecontent` と組み合わせることができますが、両方と組み合わせることはできません。

>[!CAUTION]
>
>上記のいずれかの実行モード（author、publish、samplecontent、nosamplecontent）を使用するときは、インストール時に使用する値が、そのインストールの全期間の実行モードを定義します&#x200B;*。*
>
>これらの実行モードは、インストール後は変更できません&#x200B;*。*

## カスタマイズされた実行モード {#customized-run-modes}

独自のカスタマイズされた実行モードも作成できます。これらを組み合わせて次のようなシナリオに対応できます。

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 必要に応じて

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

   すべての実行モードに適用される

* `config.author`

   オーサー実行モードに使用

* `config.publish`

   パブリッシュ実行モードに使用

* `config.<run-mode>`

   該当する実行モードに使用（config など）

これらのフォルダー内で個々の設定ノードを定義する方法、および複数の実行モードの組み合わせに関する設定を作成する方法について詳しくは、[リポジトリでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)を参照してください。

>[!NOTE]
>
>[インストール実行モード](#installation-run-modes)（オーサーなど）に関しては、インストール後は実行モードを変更できません。ただし、個々の設定プロパティの変更は、再起動時に有効になります。

## 特定の実行モード用にインストールする追加のバンドルの定義 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

特定の実行モード用にインストールする必要がある追加のバンドルも指定できます。これらの定義に関しては、インストールフォルダーを使用してバンドルが保持されます。繰り返しになりますが、実行モードはプレフィックスで示されます。

* `install.author`
* `install.publish`

これらのフォルダーは、タイプが `nt:folder` であり、適切なバンドルを含む必要があります。

## 特定の実行モードでの CQ の起動 {#starting-cq-with-a-specific-run-mode}

複数の実行モードの設定を定義した場合は、起動時にどれを使用するかを定義する必要があります。使用する実行モードを指定する方法は複数あります。優先順位は次のとおりです。

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [システムプロパティ (](#using-a-system-property-in-the-start-script)

1. [ファイル名検出](#filename-detection-renaming-the-jar-file)

アプリケーションサーバーを使用している場合は、[web.xml で実行モードを定義](#defining-the-run-mode-in-web-xml-with-application-server)することもできます。

### sling.properties ファイルの使用 {#using-the-sling-properties-file}

`sling.properties` ファイルを使用して必要な実行モードを定義できます。

1. 設定ファイルを編集します。

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 次のプロパティを追加します。この例は、オーサーの場合です。

   `sling.run.modes=author`

### -r オプションの使用 {#using-the-r-option}

カスタム実行モードは、クイックスタート起動時に`-r`オプションを使用することで起動することができます。例えば、次のコマンドを使用して、実行モードを dev `` に設定したAEMインスタンスを起動してください。

```shell
java -jar cq-56-p4545.jar -r dev
```

### 起動スクリプトのシステムプロパティを使用 {#using-a-system-property-in-the-start-script}

起動スクリプトのシステムプロパティを使用して実行モードを指定できます。

* 例えば、US にある実稼働のパブリッシュインスタンスとしてインスタンスを起動するには、以下を使用します。

   `-Dsling.run.modes=publish,prod,us`

### ファイル名検出 - jar ファイルの名前変更 {#filename-detection-renaming-the-jar-file}

インストール前にインストール jar ファイルの名前を変更することにより、次の 2 つのインストール実行モードをアクティベートできます。

* publish
* author

jar ファイルでは、次の命名規則を使用する必要があります。

`cq5-<run-mode>-p<port-number>`

例えば、`publish` 実行モードを設定するには、jar ファイルの名前を次のように変更します。

`cq5-publish-p4503`

### web.xml での実行モードの定義（アプリケーションサーバー使用時） {#defining-the-run-mode-in-web-xml-with-application-server}

アプリケーションサーバーを使用している場合は、

`sling.run.modes`

プロパティを、次のファイル内で設定することもできます。

`WEB-INF/web.xml`

これは AEM の `war` ファイル内にあり、デプロイメントの前に更新する必要があります。

詳しくは、[AEM をアプリケーションサーバーと共にインストール](/help/sites-deploying/application-server-install.md)を参照してください。
