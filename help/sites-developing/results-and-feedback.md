---
title: 結果の追跡とフィードバックの提供
description: テストケースとその結果に基づくテスト計画を定義する方法や場所は任意に選択できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 270e66d1-a3f2-457a-90d1-28b9f3c8c218
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 100%
---
# 結果の追跡とフィードバックの提供{#tracking-results-and-providing-feedback}

テストケースとその結果に基づくテスト計画を定義する方法や場所は任意に選択することができ、多数のツールが用意されています。

ただし、選択する方法やツールに関係なく、保存される情報は、

* 次のようにする必要があります。

  * テストケースとその結果のトラッキングに限定する。 これによって、メンテナンスが容易になり、テストの進捗についての明確な概要をドキュメント化できます。
  * 単一コピーとして維持され、プロジェクトチームの適切なメンバー全員が利用できます。
  * 中立で、テスト結果に限定する。 テスト結果に起因するすべてのアクションを決定するのは、プロジェクトマネージャーの責任です。

* 次のようには、しないようにします。

  * トラッキング情報を含めるように拡張する（バグ、新機能、後続のアクションも同様） この情報は他の場所で管理されます。繰り返しになりますが、使用できるツールは多数あります。
