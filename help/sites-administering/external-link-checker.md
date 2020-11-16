---
title: 外部リンクチェック
seo-title: 外部リンクチェック
description: AEM の外部リンクチェックについて説明します。
seo-description: AEM の外部リンクチェックについて説明します。
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 100%

---


# 外部リンクチェック{#the-external-link-checker}

AEM には、外部リンクチェッカーが用意されています。リンクチェッカー

* すべてのコンテンツページをスキャンします。
* すべての有効なリンクおよび無効なリンクのリストを生成します。
* 個々のコンテンツページで、無効なリンクをその場で壊れているとマークします。

## 外部リンクを検証する方法 {#how-to-validate-external-links}

外部リンクチェックを使用するには：

1. **ナビゲーション**&#x200B;を使用して、**ツール**／**サイト**&#x200B;を選択します。
1. **外部リンクチェック**&#x200B;を選択すると、すべての外部リンクのリストが生成されます。
1. 特定のリンクをリスト内で選択し、「**チェック**」をクリックして検証します。

   ![](assets/telc-01.png)

   情報が表示されます。

   * リンクの&#x200B;**ステータス**
   * **URL**
   * **リファラー**
   * リンクが&#x200B;**前回チェック**（検証）されてからの経過時間
   * 返された&#x200B;**最終ステータス**

   * リンクが&#x200B;**前回使用可能**&#x200B;になってからの経過時間
   * リンクが&#x200B;**最後アクセス**&#x200B;されからの経過時間

1. 個々のコンテンツページで、無効なリンクは壊れていると表示されます。

   ![](assets/chlimage_1-143.png)