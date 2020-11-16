---
title: 必要なテスト環境
seo-title: 必要なテスト環境
description: いくつかの環境はテストの一部と見なす必要があります。
seo-description: いくつかの環境はテストの一部と見なす必要があります。
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 32%

---


# 必要になるテスト環境の種類{#which-test-environments-will-be-needed}

テストの設定を定義するには、次の点を考慮する必要があります。

**開発** — ユニット用、および特定の統合テスト用。

**テスト** — テストの大部分に対して使用します。

**ライブ** — 最終的なパフォーマンスとストレステスト用。 顧客の受け入れテスト用。

また、必要となるインスタンスを決定する必要があります（通常、すべてのレベルのテストに対して各インスタンスの少なくとも1つ）。

**作成者** — このインスタンスを使用すると、作成者はコンテンツを入力および発行できます。

**発行** — このインスタンスは、訪問者がアクセスできるように、発行済みの形式でWebサイトを表示します。

Dispatcher と合わせてテストする必要があります。

最後に、実際のハードウェアを検討する必要があります。パフォーマンステストはすべて、最終的なライブ環境とできる限り類似した構成のシステムでおこなう必要があります。このため、プロジェクトの開始を次の 2 つに分けることをお勧めします。

**ソフト起動** — 可用性の低下これにより、実稼働環境上で実際の状況下でのパフォーマンス・テスト、調整、最適化に要する時間を確保できます。

**ハード起動** — 完全な可用性。
