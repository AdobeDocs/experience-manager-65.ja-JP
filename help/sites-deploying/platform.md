---
title: AEM プラットフォームの概要
seo-title: Introduction to the AEM Platform
description: この記事では、AEM プラットフォームとその最も重要なコンポーネントの概要を説明します。
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: ht
source-wordcount: '754'
ht-degree: 100%

---

# AEM プラットフォームの概要{#introduction-to-the-aem-platform}

AEM 6 の AEM プラットフォームは、Apache Jackrabbit Oak に基づいています。

Apache Jackrabbit Oak は、昨今の世界規模の web サイトや、要求の厳しいその他のコンテンツアプリケーションの基盤として使用する、スケーラビリティとパフォーマンスに優れた階層構造のコンテンツリポジトリを実装するための取り組みです。

これは Jackrabbit 2 の後継であり、コンテンツリポジトリである CRX のデフォルトのバックエンドとして AEM 6 で使用しています。

## 設計の原則と目的 {#design-principles-and-goals}

Oak は [JSR-283](https://jcp.org/en/jsr/detail?id=283)（JCR 2.0）仕様を実装しています。その主な設計目標は次のとおりです。

* 大規模なリポジトリのサポートの強化
* 高可用性を確保するための複数の分散クラスターノード
* パフォーマンスの向上
* 多数の子ノードおよびアクセス制御レベルのサポート

## アーキテクチャの概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### ストレージ {#storage}

ストレージレイヤーの目的は次のとおりです。

* ツリーモデルの実装
* ストレージのプラグイン化
* クラスタリングメカニズムの提供

### Oak Core {#oak-core}

Oak Core は、ストレージレイヤーに複数のレイヤーを追加します。

* アクセスレベル制御
* 検索およびインデックス作成
* 監視

### Oak JCR {#oak-jcr}

Oak JCR の主な目的は、JCR セマンティクスをツリー操作に変換することです。また、次の役割も果たします。

* JCR API の実装
* JCR の制約を実装するコミットフックの格納

また、Oak JCR の概念の一環として、Java 以外の実装も可能になりました。

## ストレージの概要 {#storage-overview}

Oak ストレージレイヤーは、コンテンツの実際のストレージの抽象化レイヤーとなります。

現在、AEM6 では 2 つのストレージ実装（**Tar ストレージ**&#x200B;と **MongoDB ストレージ**）を使用できます。

### Tar ストレージ {#tar-storage}

Tar ストレージでは tar ファイルを使用します。大きなセグメント内の様々なタイプのレコードとしてコンテンツが格納されます。リポジトリの最新の状態を追跡するために、ジャーナルが使用されます。

設計の中心となるいくつかの基本原則を次に示します。

* **不変セグメント**

コンテンツは、最大 256 KB のセグメントに格納されます。このセグメントは不変であり、そのため、頻繁にアクセスされるセグメントを簡単にキャッシュして、リポジトリの破損につながるシステムエラーを削減できます。

各セグメントは、一意の識別子（UUID）で識別され、コンテンツツリーの連続したサブセットを含んでいます。また、セグメントは他のコンテンツを参照できます。各セグメントには、参照先の他のセグメントの UUID のリストが保持されます。

* **ローカル性**

関連するレコード（ノードやその直下の子など）は同じセグメントに格納されます。これにより、リポジトリの検索が高速になり、セッションごとに複数の関連ノードにアクセスする一般的なクライアントのキャッシュミスのほとんどが回避されます。

* **コンパクト性**

I/O コストを削減しコンテンツが可能な限りキャッシュに収まるように、レコードの形式がサイズに合わせて最適化されます。

### Mongo ストレージ {#mongo-storage}

MongoDB ストレージは、MongoDB を使用してシャーディングおよびクラスタリングを行います。リポジトリツリーは、1 つの MongoDB データベースに保存され、各ノードが個別のドキュメントとなります。

次に示すいくつかの特徴があります。

* リビジョン

コンテンツの更新（コミット）ごとに、新しいリビジョンが作成されます。リビジョンは、基本的に次の 3 つの要素で構成される文字列です。

1. 生成されたマシンのシステム時刻から得られるタイムスタンプ
1. 同じタイムスタンプで作成されたリビジョンを区別するためのカウンター
1. リビジョンが作成されたクラスターノード ID

* ブランチ

ブランチがサポートされ、クライアントは複数の変更をステージングし、1 回の結合の呼び出しで表示できます。

* 前のドキュメント

MongoDB ストレージは、変更のたびにドキュメントにデータを追加します。ただし、クリーンアップが明示的にトリガーされた場合にのみ、データが削除されます。特定のしきい値に達すると、古いデータが移動されます。以前のドキュメントには不変データのみが含まれています。つまり、コミットおよび結合されたリビジョンのみが含まれています。

* クラスターノードのメタデータ

クラスター操作を容易にするために、アクティブおよび非アクティブなクラスターノードに関するデータは、データベースに保持されます。

MongoDB ストレージを使用した一般的な AEM クラスターのセットアップは次のようになります。

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2 との違いは何ですか。 {#what-is-different-from-jackrabbit}

Oak は JCR 1.0 標準と後方互換性があるので、ユーザーレベルではほとんど変更はありません。ただし、Oak ベースの AEM インストールを設定する際には、次のような顕著な違いがあり、注意する必要があります。

* Oak はインデックスを自動的に作成しません。そのため、必要に応じてカスタムインデックスを作成する必要があります。
* Jackrabbit 2 では、セッションは常にリポジトリの最新の状態を反映しますが、Oak の場合、セッションは、セッションが取得された時点からのリポジトリの安定した表示を反映します。この原因は、Oak が基にしている MVCC モデルによるものです。
* 同じ名前の兄弟（SNS）は Oak ではサポートしていません。

## その他のプラットフォーム関連ドキュメント {#other-platform-related-documentation}

AEM プラットフォームについて詳しくは、次の記事も確認してください。

* [AEM 6 でのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)
* [Oak クエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6 のストレージ要素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [MongoDB を備えた AEM](/help/sites-deploying/aem-with-mongodb.md)
