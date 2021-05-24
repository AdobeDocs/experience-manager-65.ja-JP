---
title: 管理コンソール
seo-title: 管理コンソール
description: AEM で使用可能な管理コンソールの使用方法について学習します。
seo-description: AEM で使用可能な管理コンソールの使用方法について学習します。
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 69%

---

# 管理コンソール{#admin-consoles}

管理コンソールからクラシック UI に切り替える機能は、デフォルトで無効になっています。以前は、コンソールアイコンの上にマウスを移動すると、クラシック UI にアクセスするためのポップアップアイコンが表示されていましたが、このアイコンは表示されなくなりました。

`/libs/cq/core/content/nav`にクラシックUIバージョンがあるすべてのコンソールを個別に有効にし直すと、コンソールアイコンにマウスオーバーすると、 **クラシックUI**&#x200B;オプションが再度ポップアップ表示されます。

以下の例では、サイトコンソールのクラシック UI を再有効化しています。

1. CRXDE Liteを使用して、クラシックUIを再有効化するAdmin Consoleに対応するノードを探します。 目的のノードは次の場所にあります。

   `/libs/cq/core/content/nav`

   例：

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. クラシック UI を再有効化するコンソールのノードを選択します。この例では、サイトコンソールのクラシック UI を再有効化します。

   `/libs/cq/core/content/nav/sites`

1. **Overlay Node**&#x200B;オプションを使用してオーバーレイを作成します。例：

   * **パス**: `/apps/cq/core/content/nav/sites`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次のブールプロパティを追加します。

   `enableDesktopOnly = {Boolean}true`

1. 「**クラシック UI**」オプションが、管理コンソールに再びポップアップされるようになります。

   ![](assets/syui-01-2019-02-27-15-16-55.png)

クラシック UI バージョンへのアクセスを再有効化する各コンソールに対して、これらの手順を繰り返します。
