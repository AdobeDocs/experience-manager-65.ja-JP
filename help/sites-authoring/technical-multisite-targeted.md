---
title: ターゲットコンテンツ用マルチサイト管理の構造
description: 図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 45%

---

# ターゲットコンテンツ用マルチサイト管理の構造 {#how-multisite-management-for-targeted-content-is-structured}

以下の図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています。

領域は **/content/campaigns/&lt;brand>** の下に表示され、デフォルトでは、ブランドごとに自動作成されるマスター領域が 1 つあります。各領域には、独自のアクティビティ、エクスペリエンスおよびオファーのセットが含まれます。

![chlimage_1-268](assets/chlimage_1-268.png)

ターゲットコンテンツを検索するために、ページまたはサイトを特定の領域にマッピングできます。 領域が設定されていない場合、AEMはこの特定のブランドのマスター領域にフォールバックします。

以下の図は、site1、site2、site3 という 3 つのサイトに対してロジックがどのように機能するかを示したものです。

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 は領域マッピングに基づいて、brand1 の myarea1 を検索し、brand2 の otherarea2 を検索します。
* site2 は、brand1 の領域マッピングのみが定義されているので、brand1 の myarea1 と brand2 のマスター領域を検索します。
* site3 では、このサイトの他の領域マッピングが定義されていないので、brand1 と brand2 のマスター領域を検索します。
