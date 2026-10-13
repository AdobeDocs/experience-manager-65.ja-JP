---
title: ヘッドレスをはじめる前に
description: このクイックスタートガイドでは、コンテンツモデル、コンテンツフラグメント、GraphQL API など、Adobe Experience Manager（AEM）6.5 の強力なヘッドレス機能の基本事項について説明します。
exl-id: 55ebd893-b3cc-47c5-ad84-46df984197fb
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%
---
# ヘッドレスをはじめる前に {#introduction}

ヘッドレス入門ガイドでは、AEM およびヘッドレステクノロジーを既に熟知しているユーザー向けに、Adobe Experience Manager（AEM）6.5 を使用したエクスペリエンスの作成、管理および配信の簡単な道筋を 5 つの手順に分けて示します。 各ガイドは前のガイドに基づいているので、じっくり順番に検討することをお勧めします。

1. [設定の作成](create-configuration.md)
1. [コンテンツフラグメントモデルの作成](create-content-model.md)
1. [アセットフォルダの作成](create-assets-folder.md)
1. [コンテンツフラグメントの作成](create-content-fragment.md)
1. [コンテンツフラグメントへのアクセスと配信](create-api-request.md)

>[!TIP]
>
>この入門ガイドでは、AEM とヘッドレステクノロジーの両方に関する知識を前提としています。
>
>AEM またはヘッドレスのいずれかを初めて使用する場合は、[ヘッドレスドキュメントジャーニー](/help/journey-headless/overview.md)を参照し、ヘッドレスについて、および AEM によるヘッドレスのサポートについての包括的な概要を理解してください。

## オーディエンス {#audience}

ヘッドレス入門ガイドで説明されているタスクは、AEM のヘッドレス機能の基本的な包括的デモに必要です。 テスト用 AEM インスタンスへの管理者アクセス権を持つユーザーは誰でも、これらのガイドに従って AEM でのヘッドレスな配信を理解できますが、開発者の経験を持つユーザーが最適です。

ただし、実稼動状況でこれらのタスクは通常、様々なペルソナによって実行され、実行回数も様々です。 例：

* **管理者**&#x200B;は、コンテンツの初期設定とフォルダー構造を、通常は 1 回のみまたは散発的にセットアップする必要があります。
* **情報アーキテクト**&#x200B;は、組織のニーズの変化に応じて新しいモデルを追加します。
* **コンテンツ作成者**&#x200B;は、アーキテクトが定義したモデルに基づいて、新しいコンテンツをコンテンツフラグメントとして継続的に作成します。

このヘッドレス入門ガイドでは、上記のタスクを一般に誰がどのような頻度で実行するかを説明します。

## 次の手順 {#next-step}

詳細に入る準備ができましたか？ それでは、まず、ヘッドレス入門ガイドの第 1 部[設定の作成](create-configuration.md)に目を通しましょう。
