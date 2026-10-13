---
title: ターゲットコンテンツ用マルチサイト管理の構造
description: ターゲットコンテンツ用マルチサイトサポートの構造図を示します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%
---
# ターゲットコンテンツ用マルチサイト管理の構造{#how-multisite-management-for-targeted-content-is-structured}

以下の図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています。

領域は **/content/campaigns/&lt;brand>** の下に表示され、デフォルトでは、ブランドごとに自動作成されるマスター領域が 1 つあります。 各領域には、独自のアクティビティ、エクスペリエンスおよびオファーのセットが含まれます。

![chlimage_1-268](assets/chlimage_1-268.png)

ターゲットコンテンツを参照するために、ページまたはサイトを領域にマッピングできます。 設定されている領域がない場合、AEM はこの特定のブランドのマスター領域にフォールバックします。

以下の図は、site1、site2、site3 という 3 つのサイトに対してロジックがどのように機能するかを示したものです。

![chlimage_1-269](assets/chlimage_1-269.png)

* 領域マッピングに基づいて、site1 は、brand1 用として myarea1 領域を、brand2 用として otherarea2 領域を参照します。
* brand1 用の領域マッピングのみが定義されているので、site2 は brand1 用として myarea1 領域を、brand2 用としてマスター領域を参照します。
* site3 に対してはマスター領域以外の領域マッピングがまったく定義されていないので、site3 は brand1 用と brand2 用としてマスター領域を参照します。
