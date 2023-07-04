---
title: 管理コンソール
seo-title: Admin Consoles
description: AEMで使用可能なAdmin Consoleの使用方法を説明します。
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b4370d23c7b1bd43e1f02a862f11952d04892eb3
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 管理コンソール{#admin-consoles}

デフォルトでは、管理コンソールからクラシック UI に切り替える機能は無効になっています。 したがって、特定のコンソールアイコンにマウスを合わせると表示されるポップアップアイコン（クラシック UI にアクセスできる）は表示されなくなりました。

各コンソールのクラシック UI バージョンは `/libs/cq/core/content/nav` にあり、個別に再有効化できます。それぞれのクラシック UI を有効にすれば、コンソールアイコンの上にマウスを移動したときに、「**クラシック UI**」オプションが再度ポップアップするようになります。

以下の例では、サイトコンソールのクラシック UI を再有効化しています。

1. CRXDE Lite で、クラシック UI を再有効化する管理コンソールのノードを見つけます。目的のノードは次の場所にあります。

   `/libs/cq/core/content/nav`

   例：

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. クラシック UI を再度有効にする、コンソールに対応するノードを選択します。 この例では、サイトコンソールのクラシック UI を再度有効にします。

   `/libs/cq/core/content/nav/sites`

1. 「**オーバーレイノード**」オプションを使用してオーバーレイを作成します。次に例を示します。

   * **パス**: `/apps/cq/core/content/nav/sites`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**:アクティブ（チェックボックスを選択）

1. オーバーレイノードに次のブールプロパティを追加します。

   `enableDesktopOnly = {Boolean}true`

1. この **クラシック UI** オプションは、admin console で再びポップオーバーオプションとして使用できます。

   ![クラシック UI ポップオーバーオプション](assets/syui-01-2019-02-27-15-16-55.png)

クラシック UI バージョンへのアクセスを再度有効にする各コンソールに対して、これらの手順を繰り返します。
