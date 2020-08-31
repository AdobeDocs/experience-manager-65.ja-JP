---
title: パターン検出を使用したアップグレードの複雑性の評価
seo-title: パターン検出を使用したアップグレードの複雑性の評価
description: パターン検出を使用してアップグレードの複雑性を評価する方法について説明します。
seo-description: パターン検出を使用してアップグレードの複雑性を評価する方法について説明します。
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 93%

---


# パターン検出を使用したアップグレードの複雑性の評価{#assessing-the-upgrade-complexity-with-the-pattern-detector}

## 概要 {#overview}

この機能を使用すると、次のパターンを検出することによって、既存の AEM インスタンスのアップグレード可能性をチェックできます。

1. 特定のルールへの違反があり、アップグレードにより影響を受けるか上書きされる領域でおこなわれている。
1. AEM 6.5 との後方互換性のない AEM 6.x の機能や API を使用しており、アップグレード後に動作しない可能性がある。

これにより、AEM 6.5 へのアップグレードに必要な開発の作業量を評価できます。

## 設定方法 {#how-to-set-up}

パターン検出は、AEM 6.5 のアップグレードを対象とした 6.1 から 6.5 のソース AEM バージョンで動作する [1 つのパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65)として個別にリリースされます。[パッケージマネージャー](/help/sites-administering/package-manager.md)を使用してインストールできます。

## 使用方法 {#how-to-use}

>[!NOTE]
>
>パターン検出は、ローカル開発インスタンスを含むあらゆる環境で実行できます。ただし、次の 2 つを同時に達成するには：
>
>* 検出率を上げる
>* ビジネスにとって重大なインスタンスの減速を避ける


>ユーザーアプリケーション、コンテンツ、設定の分野において、実稼働環境にできるだけ近い&#x200B;**ステージング環境で**&#x200B;実行することをお勧めします。
>
いくつかの方法を使用して、パターン検出の出力をチェックできます。

* **Felix Inventory コンソールを使用：** 

1. Go to the AEM Web Console by browsing to *https://serveraddress:serverport/system/console/configMgr*
1. 次の図に示すように、**ステータス - パターン検出**&#x200B;を選択します。

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **事後対応テキストベースまたは通常の JSON インターフェイスを使用**

* **無効なJSON行インターフェイスを使用して、各行に個別のJSONドキュメントを生成します。

これらの方法の詳細を次に示します。

## 事後対応インターフェイス {#reactive-interface}

事後対応インターフェイスを使用すると、疑義が検出された場合、すぐに違反レポートを処理できます。

現在、出力は次の 2 つの URL から取得できます。

1. プレーンテキストインターフェイス
1. JSON インターフェイス

## プレーンテキストインターフェイスの処理 {#handling-the-plain-text-interface}

出力の情報は、一連のイベントエントリとして書式設定されます。違反を公開するためのチャネルと、現在の進行状況を公開するためのチャネルがあります。

これらのチャネルは、次のコマンドを使用することで取得できます。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

出力は次のようになります。

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

進行状況は、`grep` コマンドを使用してフィルタリングできます。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

次の出力が得られます。

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## JSON インターフェイスの処理 {#handling-the-json-interface}

同様に、[jq ツール](https://stedolan.github.io/jq/)を使用すると、公開された JSON をすぐに処理できます。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

出力は以下のようになります。

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

進行状況は 5 分ごとに報告され、疑義ありとしてマークされたメッセージを除外することで取得できます。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

出力は以下のようになります。

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
curl からの出力全体をファイルに保存した後、`jq` または `grep` を使用して情報タイプをフィルタリングする方法をお勧めします。

## 検出範囲 {#scope}

現在、パターン検出では以下のことを確認できます。

* OSGi バンドルのエクスポートとインポートの不一致
* Sling リソースタイプとスーパータイプ（検索パスのコンテンツオーバーレイを含む）の過剰使用
* Oakインデックスの定義（互換性）
* VLT パッケージ（過剰使用）
* rep：ユーザーノードの互換性（OAuth 設定のコンテキストで）

>[!NOTE]
パターン検出はアップグレードに関する警告を正確に予測しようとします。ただし、シナリオによっては誤検知が発生する可能性があります。

