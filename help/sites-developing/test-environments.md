---
title: 必要なテスト環境の種類
seo-title: Which Test Environments are needed?
description: テストの一部として考慮する必要がある環境はいくつかあります
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

---

# 必要になるテスト環境の種類{#which-test-environments-will-be-needed}

テストする設定を定義するには、次の点を考慮する必要があります。

**開発** — 単体テスト、特定の統合テストの場合。

**テスト** - 大部分のテスト用。

**ライブ** — 最終的なパフォーマンステストとストレステスト。 顧客の受け入れテスト用。

また、必要なインスタンスを決定する必要があります（通常、すべてのレベルのテスト用に各インスタンスの少なくとも 1 つ）。

**作成者** — このインスタンスで、作成者がコンテンツを入力したり公開したりできます。

**公開** — このインスタンスは、訪問者がアクセスするための、公開済みの形式の Web サイトを表します。

Dispatcher と合わせてテストする必要があります。

最後に、実際のハードウェアを検討する必要があります。パフォーマンステストはすべて、最終的なライブ環境とできる限り類似した構成のシステムでおこなう必要があります。このため、プロジェクトの開始を次の 2 つに分けることをお勧めします。

**ソフトローンチ** — 可用性を制限。実稼動環境の現実的な条件下でパフォーマンステスト、チューニングおよび最適化をおこなうための時間を確保できます。

**ハードローンチ** — 完全な可用性。
