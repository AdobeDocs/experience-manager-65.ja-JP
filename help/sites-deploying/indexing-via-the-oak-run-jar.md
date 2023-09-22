---
title: Oak-run Jar を介したインデックス作成
description: Oak-run Jar を使用してインデックス作成を実行する方法を説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 21%

---

# Oak-run Jar を介したインデックス作成 {#indexing-via-the-oak-run-jar}

Oak-run は、JMX レベルから操作する必要なく、コマンドラインですべてのインデックス作成の使用例をサポートします。 oak-run アプローチの利点は次のとおりです。

1. これはAEM 6.4 の新しいインデックス作成ツールセットです。
1. これにより、大規模なリポジトリでの再インデックス時間に影響を与える、再インデックスに要する時間を短縮できます。
1. AEMでのインデックス再作成中のリソース消費を削減し、他のAEMアクティビティのシステムパフォーマンスを向上させます。
1. Oak-run は、帯域外のサポートを提供します。実稼動環境で実稼動インスタンスに対してインデックス再作成を実行できない場合は、重大なパフォーマンスへの影響を避けるために、クローン環境を再インデックスに使用できます。

以下に、 `oak-run` ツールを使用します。

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

この図は、様々なインデックス再作成アプローチを使用するタイミングを示すデシジョンツリーです。

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## MongoMK / RDMBMK のインデックス再作成 {#reindexingmongomk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [使用例 3 — インデックスの再作成](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### SegmentNodeStore および DocumentNodeStore のテキスト事前抽出 {#textpre-extraction}

[テキストの事前抽出](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (AEM 6.3 で存在していた機能 ) を使用して、再インデックスにかかる時間を短縮できます。 テキストの事前抽出は、すべてのインデックス再作成アプローチで使用できます。

に応じて `oak-run.jar` インデックス作成アプローチでは、以下の図の「再インデックスを実行」手順のどちらかの側に様々な手順があります。

![SegmentNodeStore および DocumentNodeStore のテキスト事前抽出](assets/4.png)

>[!NOTE]
>
>オレンジは、AEMがメンテナンスウィンドウに存在する必要があるアクティビティを示します。

### oak-run.jar を使用した MongoMK または RDBMK のオンラインインデックス再作成 {#onlinere-indexingformongomk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [インデックス再作成 — DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

MongoMK（および RDBMK）AEMインストールのインデックス再作成には、この方法をお勧めします。 他の方法は使用しないでください。

このプロセスは、クラスター内の 1 つのAEMインスタンスに対してのみ実行します。

![oak-run.jar を使用した MongoMK または RDBMK のオンラインインデックス再作成](assets/5.png)

## TarMK のインデックス再作成 {#re-indexingtarmk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [インデックス再作成 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **コールドスタンバイに関する考慮事項（TarMK）**

   * コールドスタンバイに関しては特別な考慮事項はありません。コールドスタンバイインスタンスの同期は通常どおり変更されます。

* **AEMパブリッシュファーム（AEM パブリッシュファームは常に TarMK にする必要があります）**

   * パブリッシュファームの場合は、すべての OR で、単一のパブリッシュで手順を実行する必要があります。 次に、他のユーザー向けに設定を複製します (AEMインスタンスを複製する際の通常の手順をすべて取ります。sling.id — は、ここにリンクする必要があります )。

### TarMK のオンラインインデックス再作成 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>このシナリオについて詳しくは、 [オンラインインデックス再作成 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

これは、oak-run.jar の新しいインデックス作成機能の導入前に使用された方法です。これは、 `reindex=true` Oak インデックスのプロパティ。

このアプローチは、インデックス作成に対する時間効果とパフォーマンス効果がお客様にとって受け入れ可能な場合に使用できます。 これは、多くの場合、中小のAEMインストールに該当します。

![TarMK のオンラインインデックス再作成](assets/6.png)

### oak-run.jar を使用した TarMK のオンラインインデックス再作成 {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、[オンラインのインデックス再作成 - SegmentNodeStore - AEM インスタンス実行中](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)を参照してください。

oak-run.jar を使用した TarMK のオンラインインデックス再作成は、 [TarMK のオンラインインデックス再作成](#onlinere-indexingfortarmk) 上記の説明。 ただし、メンテナンス期間中の実行も必要です。ただし、ウィンドウが短くなり、インデックス再作成を実行するには、より多くの手順が必要です。

>[!NOTE]
>
>オレンジ色は、メンテナンス期間中に AEM を実行する必要がある操作を示します。

![oak-run.jar を使用した TarMK のオンラインインデックス再作成](assets/7.png)

### oak-run.jar を使用した TarMK のオフラインインデックス再作成 {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、 [オンラインインデックス再作成 — SegmentNodeStore - AEMインスタンスがシャットダウンされます](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

TarMK のオフラインインデックス再作成は最も簡単です `oak-run.jar` TarMK のインデックス再作成アプローチは、1 つの `oak-run.jar` コメント。 ただし、AEMインスタンスをシャットダウンする必要があります。

>[!NOTE]
>
>赤は、AEMをシャットダウンする必要がある操作を示します。

![oak-run.jar を使用した TarMK のオフラインインデックス再作成](assets/8.png)

### oak-run.jar を使用した TarMK の Out-of-band インデックス再作成  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>このシナリオについて詳しくは、 [帯域外再インデックス — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

帯域外再インデックスにより、使用中のAEMインスタンスに対する再インデックスの影響を最小限に抑えます。

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
>ACS Ensure Index は、コミュニティでサポートされるプロジェクトであり、Adobe・サポートではサポートされていません。

これにより、コンテンツパッケージを介した出荷インデックスの定義が可能になり、後で reindex フラグをに設定することでインデックスが再作成されます。 `true`. これは、インデックス再作成に時間がかからない小規模な設定で機能します。

詳しくは、 [ACS Ensure Index ドキュメント](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 」を参照してください。

### oak-run.jar を使用した TarMK でのインデックス定義の作成と更新 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

非インデックスを使用してインデックス再作成を行った場合に、時間またはパフォーマンスに影響が及ぶ場合`oak-run.jar` メソッドが大きすぎます。次の操作を行います： `oak-run.jar` ベースアプローチは、TarMK ベースのAEMインストールで Lucene インデックス定義の読み込みと再インデックスを行う場合に使用できます。

![oak-run.jar を使用した TarMK でのインデックス定義の作成と更新](assets/10.png)

### oak-run.jar を使用した MonogMK でのインデックス定義の作成と更新 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

非インデックスを使用してインデックス再作成を行った場合に、時間またはパフォーマンスに影響が及ぶ場合`oak-run.jar` メソッドが大きすぎます。次の操作を行います： `oak-run.jar` ベースアプローチは、MongoMK ベースのAEMインストールで Lucene Index 定義の読み込みと再インデックスを行う場合に使用できます。

![oak-run.jar を使用した MonogMK でのインデックス定義の作成と更新](assets/11.png)
