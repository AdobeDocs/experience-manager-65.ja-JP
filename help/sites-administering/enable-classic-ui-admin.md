---
title: 管理コンソール
description: AEM で使用可能な管理コンソールの使用方法について説明します。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 75%

---


# 管理コンソール{#admin-consoles}

管理コンソールからクラシック UI に切り替える機能は、デフォルトで無効になっています。したがって、特定のコンソールアイコンにマウスを合わせると表示されるポップアップアイコン（クラシック UI にアクセスできる）は表示されなくなりました。

各コンソールのクラシック UI バージョンは `/libs/cq/core/content/nav` にあり、個別に再有効化できます。それぞれのクラシック UI を有効にすれば、コンソールアイコンの上にマウスを移動したときに、「**クラシック UI**」オプションが再度ポップアップするようになります。

以下の例では、サイトコンソールのクラシック UI を再有効化しています。

1. CRXDE Liteを使用して、クラシック UI を再度有効にするAdmin Consoleに対応するノードを探します。 目的のノードは次の場所にあります。

   `/libs/cq/core/content/nav`

   例：

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. クラシック UI を再有効化するコンソールのノードを選択します。この例では、Sites コンソールのクラシック UI を再有効化します。

   `/libs/cq/core/content/nav/sites`

1. 「**オーバーレイノード**」オプションを使用してオーバーレイを作成します。次に例を示します。

   * **パス**: `/apps/cq/core/content/nav/sites`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次のブールプロパティを追加します。

   `enableDesktopOnly = {Boolean}true`

1. The **クラシック UI** オプションは、Admin Consoleのポップオーバーオプションとして再び使用できます。

   ![クラシック UI ポップオーバーオプション](assets/syui-01-2019-02-27-15-16-55.png)

クラシック UI バージョンへのアクセスを再有効化する各コンソールに対して、これらの手順を繰り返します。
