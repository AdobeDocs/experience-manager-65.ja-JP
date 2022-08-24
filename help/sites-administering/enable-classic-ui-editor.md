---
title: エディター
seo-title: Editor
description: クラシック UI エディターへの切り替え方法について説明します。
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# エディター{#editor}

エディターからクラシック UI に切り替える機能は、デフォルトで無効になっています。

**ページ情報**&#x200B;メニューのオプション「**クラシック UI で開く**」を再度有効にするには、次の手順に従います。

1. CRXDE Lite を使用して、次のノードを見つけます。

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   次に例を示します。

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 「**オーバーレイノード**」オプションを使用してオーバーレイを作成します。次に例を示します。

   * **パス**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次の複数値テキストプロパティを追加します。

   `sling:hideProperties = ["granite:hidden"]`

1. ページの編集時に、「**クラシック UI で開く**」オプションが&#x200B;**ページ情報**&#x200B;メニューで再度使用可能になります。

   ![](assets/syui-03-2019-02-27-15-19-48.png)
