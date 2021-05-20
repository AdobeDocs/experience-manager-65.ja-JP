---
title: AEM Commerceの開発
description: AEM プロジェクトアーキタイプを使用してコマース対応の AEM プロジェクトを生成する方法を説明します。プロジェクトを構築し、ローカル開発環境にデプロイする方法を説明します。
topics: Commerce, Development
feature: コマース統合フレームワーク
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 37%

---


# AEM Commerceの開発 {#develop}

AEM用のCommerce Integration Framework(CIF)に基づくAEM Commerceプロジェクトの開発は、他のAEMプロジェクトと同じルールとベストプラクティスに従います。 最初に以下を確認してください。

- [AEM 6.5 開発ユーザーガイド](/help/sites-developing/home.md)
- [AEM の中心概念](/help/sites-developing/the-basics.md)
- [AEM の開発 - ガイドラインとベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)

## AEM Commerceのローカル開発 {#local}

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。

>[!NOTE]
>
>以下の手順は、CIFを使用してAEM Commerce用のローカルAEM開発環境をAEM 6.5用に設定する場合に役立ちます)。 AEMをCloud Serviceとして使用している場合は、[AEM Commerce as aCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/home.html)のドキュメントを参照してください。

AEM 6.5用のAEM Commerceアドオンは、次のとおりです。 CIFアドオンは、ローカル開発にも使用でき、AEMパッケージとして提供されます。 [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)から機能パックとしてダウンロードできます。

### 必要なソフトウェア

以下をローカルにインストールしておく必要があります。

- ローカルAEM 6.5
- [AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7以降
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
- [ノードLTS](https://nodejs.org/ja/)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIFアドオンへのアクセス

CIFアドオンは、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードし、「AEM Commerce add-on」を検索します。

>[!TIP]
>
>常に最新バージョンの CIF アドオンを使用していることを確認してください。

### ローカル設定

AEMとCIFアドオンを使用するローカルCIFプロジェクト開発の場合は、次の手順に従います。

1. AEM 6.5リリースを入手し、AEM 6.5 Service Packをインストールします。 AEM 6.5 Service Pack 7が必要ですが、最新のサービスパックをインストールすることをお勧めします。

1. AEM.jar を解凍し、`crx-quickstart` フォルダーを作成します。次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーの作成

1. ソフトウェア配布ポータルからダウンロードしたCIFアドオンのすべてのパッケージを`crx-quickstart/install`フォルダーにコピーします。

>[!TIP]
>
>または、CIFアドオンパッケージをパッケージマネージャーからインストールすることもできます。

1. AEM Quickstartの起動

OSGI コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。このリストには、CIFアドオン関連バンドル、コンテンツパッケージ、OSGI設定が含まれている必要があります。 すべてのバンドルが開始されていることを確認します。

## プロジェクトのセットアップ {#project}

CIFを使用してAEM Commerceプロジェクトを開始する方法は2つあります。

### AEM プロジェクトアーキタイプの使用

CIF を使い始めるために事前に設定されたプロジェクトをブートストラップするには、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)が主なツールです。CIFコアコンポーネントと必要なすべての設定を、1つの追加オプションで生成されたプロジェクトに含めることができます。

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

CIFコアコンポーネントは、提供されている`all`パッケージを含めるか、CIFコンテンツパッケージと関連するOSGIバンドルを使用する個人を含めることで、任意のプロジェクトで使用できます。 CIF コアコンポーネントを手動でプロジェクトに追加するには、次の依存関係を使用します。

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

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティスの例と、独自の機能を開発するための潜在的な出発点として意図されています。

Venia参照用ストアを使い始めるには、[Gitリポジトリ](https://github.com/adobe/aem-cif-guides-venia)をコピーし、必要に応じてプロジェクトをカスタマイズします。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。AEM 6.5の場合は、`classic`プロファイルを使用します。

### AEMをCommerce Systemに接続する

プロジェクトをコマースシステムに接続するには、コマースシステムのGraphQLエンドポイントをAEMに設定する必要があります。

どちらの場合も、 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)または[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)で生成されるプロジェクトには、調整が必要な[デフォルト設定](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)が既に含まれています。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`の`url`の値を、プロジェクトで使用されるコマースシステムのGraphQLエンドポイントに置き換えます。

AEM CommerceアドオンおよびCIFコアコンポーネントは、AEMサーバーを介して、ブラウザーを介して直接コマースGraphQLエンドポイントに接続します。 クライアント側のCIFコアコンポーネントとCIFアドオンオーサリングツールは、デフォルトで`/api/graphql`に接続されます。 必要に応じて、CIFCloud Service設定（以下を参照）で調整できます。

CIFアドオンは、`/api/graphql`にGraphQLプロキシサーブレットを提供します。 ローカルのAEM Dispatcherを使用しない場合は、GraphQLプロキシサーブレットも設定することをお勧めします。

http://localhost:4502/system/console/configMgrに移動し、`Adobe CIF GraphQL Proxy Configuration`サービスのOSGI設定を作成します。 上記のGraphQLクライアントで使用したのと同じGraphQLエンドポイントをコマースシステムで使用します。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
