---
title: 必要なテスト環境の種類
description: テストの一部として考慮する必要がある環境はいくつかあります
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 100%
---
# 必要なテスト環境の種類{#which-test-environments-will-be-needed}

テストする設定を定義するには、次の点を考慮する必要があります。

**開発** — 単体テスト、特定の統合テストの場合。

**テスト** – ほとんどのテストの場合。

**ライブ** — 最終的なパフォーマンステストとストレステスト。 顧客の受け入れテスト用。

必要なインスタンスと場所を決定します（通常、すべてのレベルのテストで各インスタンスのうち少なくとも 1 つ）。

**作成者** — このインスタンスで、作成者がコンテンツを入力したり公開したりできます。

**公開** — このインスタンスは、訪問者がアクセスするための、公開済みの形式の Web サイトを表します。

Dispatcher を使用してテスト。

最後に、実際のハードウェアを考慮する必要があります。パフォーマンステストは、可能な限り最終的な実稼働環境に近い設定のシステム上で行う必要があります。 このため、プロジェクトのローンチは、次のように分割することをお勧めします。

**ソフトローンチ** - 可用性を制限。本番環境の現実的な条件下でパフォーマンステスト、チューニングおよび最適化を行う時間を確保できます。

**ハードローンチ** - 完全な可用性。
