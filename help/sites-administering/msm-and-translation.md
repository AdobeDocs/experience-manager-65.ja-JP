---
title: Web サイト管理
seo-title: Website Administration
description: AEMで多言語の Web サイトを管理する方法を説明します。
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 34%

---

# Web サイト管理{#website-administration}

Web サイトおよびページの管理には、次の管理ツールを使用できます。

* マルチサイトマネージャー（MSM）を使用すると、同じサイトコンテンツを複数の場所で使用できるだけでなく、場所によってバリエーションを持たせることができます。

   * [コンテンツの再利用：マルチサイトマネージャとライブコピー](/help/sites-administering/msm.md)

* 翻訳を使用すると、ページコンテンツ、アセットおよびユーザー生成コンテンツの翻訳を自動化して、多言語の Web サイトを作成および管理できます。

   * [多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)

* これら 2 つの機能を組み合わせて、両方の Web サイトに対応できます。 [多国籍で多言語の](#multinational-and-multilingual-sites).

## 多国籍な多言語サイト {#multinational-and-multilingual-sites}

マルチサイトマネージャと翻訳ワークフローを併せて使用することで、多国籍な多言語サイトのコンテンツを効率的に作成できます。特定の国に対して 1 つの言語でマスターサイトを作成し、必要に応じて翻訳を使用して、そのコンテンツを他のサイトの基礎として使用します。

* マスターサイトを別の言語に[翻訳](/help/sites-administering/translation.md)します。

* [マルチサイトマネージャ](/help/sites-administering/msm.md)を次の用途で使用します。

   * マスターサイトのコンテンツと翻訳を再利用して、他の国や文化のサイトを作成します。
   * マルチサイトマネージャーの使用を 1 つの言語内のコンテンツに制限してください。例えば、国サイトでは英語のマスター/英語のブランチ、国サイトではフランス語のマスター/フランス語のブランチです。
   * 必要に応じて、ライブコピーの要素を分離して、ローカリゼーションの詳細を追加します。

次の図に、主な概念がどのように関連するかを示します（関連するすべてのレベルと要素を網羅しているわけではありません）。

![MSM と翻訳の主な概念を示す図](assets/chlimage_1-71a.png)

>[!NOTE]
>
>このようなシナリオでは、MSM は異なる言語バージョンを管理することはありません。
>
>* [MSM](/help/sites-administering/msm.md) は、言語の境界内で、ブループリント（グローバルマスターなど）からライブコピー（ローカルサイトなど）への翻訳済みコンテンツのデプロイメントを管理します。
>* The [翻訳](/help/sites-administering/translation.md) AEMの統合機能は、サードパーティの翻訳管理サービスと連携して、言語を管理し、コンテンツをこれらの異なる言語に翻訳します。
>
>より高度な使用例では、MSM を複数の言語マスターで使用することもできます。

>[!NOTE]
>
>すべての使用例で、次のベストプラクティスをお読みになることをお勧めします。
>
>* [MSM のベストプラクティス](/help/sites-administering/msm-best-practices.md)；特に：
>
>   * [サイトの作成](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM と多言語の Web サイト](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)
