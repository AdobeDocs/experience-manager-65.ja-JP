---
title: ワークフローの操作
description: Adobe Experience Manager のワークフローでは、ページまたはアセットで実行される一連の手順を自動化できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 100%
---
# ワークフローの操作{#working-with-workflows}

AEM のワークフローでは、（1 つ以上の）ページまたはアセットで実行される一連の手順を自動化できます。

例えば、パブリッシュ時にエディターは、サイトの管理者がページをアクティベートする前にコンテンツをレビューする必要があります。 この例を自動化するワークフローでは、必要な作業を実行するときが来たことが各参加者に通知されます。

1. 作成者がワークフローをページに適用します。
1. 編集者は、ページの内容をレビューする必要があることを示す作業項目を受け取ります。 これが完了すると、作業項目が完了したことが示されます。
1. 次に、サイトの管理者は、ページのアクティベートをリクエストする作業項目を受け取ります。 これが完了すると、作業項目が完了したことが示されます。

一般的に、以下のようになります。

* コンテンツの作成者がワークフローをページに適用し、ワークフローに参加します。
* 使用するワークフローは、組織のビジネスプロセスに固有です。

参考資料：

* [ページへのワークフローの適用](/help/sites-authoring/workflows-applying.md)
* [ワークフローへの参加](/help/sites-authoring/workflows-participating.md)
