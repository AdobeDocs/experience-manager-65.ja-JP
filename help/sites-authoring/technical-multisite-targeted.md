---
title: ターゲットコンテンツ用マルチサイト管理の構造
seo-title: How Multisite Management for Targeted Content is Structured
description: 図は、ターゲットコンテンツ用マルチサイトサポートの構造を示しています。
seo-description: A diagram shows how multisite support for targeted content is structured
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '177'
ht-degree: 100%

---

# ターゲットコンテンツ用マルチサイト管理の構造 {#how-multisite-management-for-targeted-content-is-structured}

以下の図は、ターゲットコンテンツ用マルチサイト管理の構造を示しています。

領域は **/content/campaigns/&lt;brand>** の下に表示され、デフォルトでは、ブランドごとに自動作成されるマスター領域が 1 つあります。各領域には、独自のアクティビティ、エクスペリエンスおよびオファーのセットが含まれます。

![chlimage_1-268](assets/chlimage_1-268.png)

ターゲットコンテンツを参照するために、ページまたはサイトを領域にマップできます。設定されている領域がない場合、AEM はこの特定のブランドのマスター領域にフォールバックします。

以下の図は、site1、site2、site3 という 3 つのサイトに対してロジックがどのように機能するかを示したものです。

![chlimage_1-269](assets/chlimage_1-269.png)

* 領域マッピングに基づいて、site1 は、brand1 用として myarea1 領域を、brand2 用として otherarea2 領域を参照します。
* brand1 用の領域マッピングのみが定義されているので、site2 は brand1 用として myarea1 領域を、brand2 用としてマスター領域を参照します。
* site3 に対してはマスター領域以外の領域マッピングがまったく定義されていないので、site3 は brand1 用と brand2 用としてマスター領域を参照します。
