---
title: Oak-run Jar を使用したインデックス作成
description: Oak-run Jar を使用してインデックス作成を実行する方法を説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 40%

---

# Oak-run Jar を使用したインデックス作成 {#indexing-via-the-oak-run-jar}

Oak-run は、JMX レベルから操作する必要なく、コマンドラインですべてのインデックス作成の使用例をサポートします。 oak-run アプローチの利点は次のとおりです。

1. AEM 6.4 の新しいインデックス作成ツールセットです。
1. インデックス再作成時間を削減します。より大きいリポジトリでのインデックス再作成時間に有益な影響があります。
1. AEM でのインデックス再作成時のリソース消費を削減します。これにより、他の AEM アクティビティのシステムパフォーマンスが向上します。
1. Oak-run は、帯域外のサポートを提供します。実稼動環境で実稼動インスタンスに対してインデックス再作成を実行できない場合は、クローン環境を使用してインデックス再作成を行い、パフォーマンスに重大な影響を与えるのを防ぐことができます。

以下に、 `oak-run` ツール

## インデックスの整合性チェック {#indexconsistencychecks}

>[!NOTE]
>
>このシナリオについて詳しくは、 [使用例 1 — インデックスの整合性チェック](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`Lucene Oak インデックスが破損しているかどうかを迅速に判断します。
* 整合性チェックレベル 1 および 2 の場合は、使用中の AEM インスタンスで実行しても安全です。

![インデックスの整合性チェック](assets/screen_shot_2017-12-14at135758.png)

## インデックスの統計 {#indexstatistics}

>[!NOTE]
>
>このシナリオについて詳しくは、 [使用例 2 — インデックス統計](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` オフライン分析用に、すべてのインデックス定義、重要なインデックス統計、およびインデックスコンテンツをダンプします。
* 使用中の AEM インスタンスで実行しても安全です。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## インデックス再作成アプローチのデシジョンツリー {#reindexingapproachdecisiontree}

様々なインデックス再作成アプローチを使用すべき状況についてのデシジョンツリーを次の図に示します。

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## MongoMK / RDMBMK のインデックス再作成 {#reindexingmongomk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [使用例 3 — インデックスの再作成](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### SegmentNodeStore および DocumentNodeStore のテキスト事前抽出 {#textpre-extraction}

[テキストの事前抽出](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (AEM 6.3 で存在していた機能 ) を使用して、インデックス再作成の時間を短縮できます。 テキストの事前抽出は、すべてのインデックス再作成アプローチで使用できます。

に応じて `oak-run.jar` インデックス作成アプローチでは、以下の図の「再インデックスを実行」手順のどちらかの側で様々な手順を実行します。

![SegmentNodeStore および DocumentNodeStore のテキスト事前抽出](assets/4.png)

>[!NOTE]
>
>オレンジは、AEMがメンテナンスウィンドウに存在する必要があるアクティビティを示します。

### oak-run.jar を使用した MongoMK または RDBMK のオンラインインデックス再作成 {#onlinere-indexingformongomk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [インデックス再作成 — DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

これは、MongoMK（および RDBMK）AEM インストールのインデックスを再作成する場合にお勧めする方法です。他の方法は使用しないでください。

このプロセスは、クラスター内の 1 つのAEMインスタンスに対してのみ実行します。

![oak-run.jar を使用した MongoMK または RDBMK のオンラインインデックス再作成](assets/5.png)

## TarMK のインデックス再作成 {#re-indexingtarmk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [インデックス再作成 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **コールドスタンバイに関する考慮事項（TarMK）**

   * コールドスタンバイに関する特別な考慮事項はありません。コールドスタンバイインスタンスの同期は、通常どおり変更されます。

* **AEM パブリッシュファーム（AEM パブリッシュファームは常に TarMK にする必要があります）**

   * パブリッシュファームの場合は、すべての OR に対しておこなう必要があります。また、1 つのパブリッシュで手順を実行し、他のパブリッシュに対して設定をクローンする必要があります (AEMインスタンスのクローンを作成する場合は、通常の手順を実行します )。sling.id — ここで何かにリンクする必要がある )

### TarMK のオンラインインデックス再作成 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [オンラインインデックス再作成 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

これは、oak-run.jar の新しいインデックス作成機能の導入前に使用された方法です。これは、 `reindex=true` Oak インデックスのプロパティ。

このアプローチは、インデックス作成に対する時間効果とパフォーマンス効果がお客様に許容される場合に使用できます。 これは、多くの場合、中小のAEMインストールに該当します。

![TarMK のオンラインインデックス再作成](assets/6.png)

### oak-run.jar を使用した TarMK のオンラインインデックス再作成 {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、[オンラインのインデックス再作成 - SegmentNodeStore - AEM インスタンス実行中](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)を参照してください。

oak-run.jar を使用した TarMK のオンラインインデックス再作成は、上記の [TarMK のオンラインインデックス再作成](#onlinere-indexingfortarmk)より高速です。ただし、メンテナンスウィンドウ中に実行する必要があり、時間は短くなりますが、インデックス再作成の実行に必要な手順が増えます。

>[!NOTE]
>
>オレンジ色は、メンテナンス期間中に AEM を実行する必要がある操作を示します。

![oak-run.jar を使用した TarMK のオンラインインデックス再作成](assets/7.png)

### oak-run.jar を使用した TarMK のオフラインインデックス再作成 {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、 [オンラインインデックス再作成 — SegmentNodeStore - AEMインスタンスがシャットダウンされます](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

TarMK のオフラインインデックス再作成は、必要な `oak-run.jar` コメントが 1 つだけなので、`oak-run.jar` ベースの TarMK 用インデックス再作成アプローチとしては最も簡単です。ただし、AEMインスタンスをシャットダウンする必要があります。

>[!NOTE]
>
>赤は、AEMをシャットダウンする必要がある操作を示します。

![oak-run.jar を使用した TarMK のオフラインインデックス再作成](assets/8.png)

### oak-run.jar を使用した TarMK の Out-of-band インデックス再作成  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、 [帯域外再インデックス — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

アウトオブバンドでのインデックス再作成により、使用中のAEMインスタンスに対するインデックス再作成の影響を最小限に抑えます。

>[!NOTE]
>
>赤は、AEMがシャットダウンされる可能性がある操作を示します。

![oak-run.jar を使用した TarMK の Out-of-band インデックス再作成](assets/9.png)

## インデックス作成定義の更新 {#updatingindexingdefinitions}

>[!NOTE]
>
>このシナリオについて詳しくは、[ユースケース 4 - インデックス定義の更新](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)を参照してください。

### ACS Ensure Index を使用した TarMK でのインデックス定義の作成と更新 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index は、コミュニティでサポートされるプロジェクトで、Adobe・サポートではサポートされていません。

これにより、コンテンツパッケージを介したインデックス定義の送信が可能になり、reindex フラグを `true` に設定すれば、後でインデックスが再作成されることになります。これは、インデックス再作成に時間がかからない小規模なセットアップで機能します。

詳しくは、 [ACS Ensure Index ドキュメント](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 」を参照してください。

### oak-run.jar を使用した TarMK でのインデックス定義の作成と更新 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

非インデックスを使用した再インデックスによる時間またはパフォーマンスへの影響`oak-run.jar` メソッドが大きすぎます。次の操作を行います： `oak-run.jar` ベースアプローチは、TarMK ベースのAEMインストールで Lucene Index 定義の読み込みと再インデックスを行う場合に使用できます。

![oak-run.jar を使用した TarMK でのインデックス定義の作成と更新](assets/10.png)

### oak-run.jar を使用した MonogMK でのインデックス定義の作成と更新 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

非インデックスを使用した再インデックスによる時間またはパフォーマンスへの影響`oak-run.jar` メソッドが大きすぎます。次の操作を行います： `oak-run.jar` ベースアプローチは、MongoMK ベースのAEMインストールで Lucene Index 定義の読み込みと再インデックスをおこなう場合に使用できます。

![oak-run.jar を使用した MonogMK でのインデックス定義の作成と更新](assets/11.png)
