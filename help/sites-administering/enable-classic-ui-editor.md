---
title: 編集者
seo-title: 編集者
description: クラシック UI エディターへの切り替え方法について説明します。
seo-description: クラシック UI エディターへの切り替え方法について説明します。
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 90%

---


# 編集者{#editor}

エディターからクラシック UI に切り替える機能は、デフォルトで無効になっています。

**ページ情報**&#x200B;メニューのオプション「**クラシック UI で開く**」を再度有効にするには、次の手順に従います。

1. CRXDE Lite を使用して、次のノードを見つけます。

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例：

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Create an overlay using the **Overlay Node** option; for example:

   * **パス**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次の複数値テキストプロパティを追加します。

   `sling:hideProperties = ["granite:hidden"]`

1. ページの編集時に、「**クラシック UI で開く**」オプションが&#x200B;**ページ情報**&#x200B;メニューで再度使用可能になります。

   ![](assets/syui-03-2019-02-27-15-19-48.png)