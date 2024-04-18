---
title: エディター
description: クラシック UI エディターへの切り替え方法を説明します。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '108'
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

   ![ページ情報からクラシック UI オプションで開く](assets/syui-03-2019-02-27-15-19-48.png)
