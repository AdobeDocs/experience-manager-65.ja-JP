---
title: AEM Commerce の開発
description: AEM プロジェクトアーキタイプを使用してコマース対応の AEM プロジェクトを生成する方法を説明します。プロジェクトを構築し、ローカル開発環境にデプロイする方法を説明します。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 48479725-8b52-4ff2-a599-d20958b26ee6
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: ht
source-wordcount: '871'
ht-degree: 100%

---

# AEM Commerce の開発 {#develop}

AEM 向けコマース統合フレームワーク（CIF）に基づく AEM Commerce プロジェクトの開発でも、他の AEM プロジェクトと同じルールとベストプラクティスに従います。 最初に以下を確認してください。

- [AEM 6.5 開発ユーザーガイド](/help/sites-developing/home.md)
- [AEM の中心概念](/help/sites-developing/the-basics.md)
- [AEM の開発 - ガイドラインとベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)

## AEM Commerce のローカル開発 {#local}

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。

>[!NOTE]
>
>以下の手順は、CIF を使用して AEM Commerce 用のローカル AEM 開発環境を AEM 6.5 用に設定する場合に役立ちます。 AEM as a Cloud Service を使用している場合は、 [AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html?lang=ja) ドキュメントを参照してください。

AEM 6.5 用の AEM Commerce アドオンCIF アドオンは、ローカル開発にも使用でき、AEM パッケージとしても提供されます。 これは、 [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)から機能パックとしてダウンロードできます。

### 必要なソフトウェア

以下をローカルにインストールしておく必要があります。

- ローカル AEM 6.5
- [AEM 6.5 サービスパック](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 以降
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
- [Node LTS](https://nodejs.org/ja/)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF アドオンへのアクセス

CIF アドオンは、 [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。「AEM Commerce add-on」を検索してください。

>[!TIP]
>
>常に最新バージョンの CIF アドオンを使用していることを確認してください。

### ローカル設定

AEM と CIF アドオンを使用するローカル CIF プロジェクト開発の場合は、次の手順に従います。

1. AEM 6.5 リリースを入手し、AEM 6.5 サービスパックをインストールします。 AEM 6.5 サービスパック 7 が必要ですが、入手可能な最新のサービスパックをインストールすることをお勧めします。

1. AEM.jar を解凍し、`crx-quickstart` フォルダーを作成します。次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーの作成

1. ソフトウェア配布ポータルからダウンロードした CIF アドオンのすべてのパッケージを `crx-quickstart/install` フォルダーにコピーします。

>[!TIP]
>
>または、パッケージマネージャーから CIF アドオンパッケージをインストールすることもできます。

1. AEM クイックスタートを起動します。

OSGI コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。このリストには、CIF アドオン関連バンドル、コンテンツパッケージ、OSGI 設定が含まれている必要があります。すべてのバンドルが起動されていることを確認します。

## プロジェクトのセットアップ {#project}

CIF を使用して AEM Commerce プロジェクトを開始する方法は 2 とおりあります。

### AEM プロジェクトアーキタイプの使用

CIF を使い始めるために事前に設定されたプロジェクトをブートストラップするには、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)が主なツールです。CIF コアコンポーネントと必要なすべての設定を、生成されたプロジェクトに 1 つの追加オプションで含めることができます。

>[!TIP]
>
>プロジェクトを生成するには、[AEM プロジェクトアーキタイプ 25 以降](https://github.com/adobe/aem-project-archetype/releases)を使用します。

AEM プロジェクトの生成方法については、AEM プロジェクトのアーキタイプの「[使用手順](https://github.com/adobe/aem-project-archetype#usage)」を参照してください。プロジェクトに CIF を含めるには、`includeCommerce` オプションを使用します。

次に例を示します。

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

提供されている `all` パッケージを含めるか、CIF コンテンツパッケージと関連する OSGI バンドルを個別に使用することで、CIF コアコンポーネントを任意のプロジェクトで使用できます。CIF コアコンポーネントを手動でプロジェクトに追加するには、次の依存関係を使用します。

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### AEM Venia 参照用ストアの使用

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティス例として意図されていて、独自機能を開発するための有望な出発点としての役割も果たします。

Venia 参照用ストアの使用を開始するには、[Git リポジトリー](https://github.com/adobe/aem-cif-guides-venia)をコピーし、必要に応じてプロジェクトをカスタマイズします。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。AEM 6.5 の場合は、 `classic` プロファイルを使用します。

### コマースシステムへの AEM の接続

プロジェクトをコマースシステムに接続するには、コマースシステムの GraphQL エンドポイントを AEM に設定する必要があります。

[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)で生成されたプロジェクトにも、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)で生成されたプロジェクトにも、[デフォルト設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)が既に含まれており、これを調整する必要があります。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` の `url` の値を、プロジェクトで使用されるコマースシステムの GraphQL エンドポイントに置き換えます。

AEM Commerce アドオンと CIF コアコンポーネントは、AEM サーバーを介して、またはブラウザーを介して直接、コマース GraphQL エンドポイントに接続します。 クライアントサイドの CIF コアコンポーネントと CIF アドオンのオーサリングツールは、デフォルトで `/api/graphql` に接続します。 必要に応じて、 CIF Cloud Service 設定で調整できます（以下を参照）。

CIF アドオンは、`/api/graphql` で GraphQL プロキシサーブレットを提供します。 ローカルの AEM Dispatcher を使用しない場合は、GraphQL プロキシサーブレットも設定することをお勧めします。

http://localhost:4502/system/console/configMgr に移動し、`Adobe CIF GraphQL Proxy Configuration` サービスの OSGI 設定を作成します。上記の GraphQL クライアントで使用したのと同じ GraphQL エンドポイントを、コマースシステムで使用します。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
