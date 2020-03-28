---
title: コメントコンポーネントの拡張
seo-title: コメントコンポーネントの拡張
description: コメントコンポーネントを拡張して、特定の用途についてコンポーネントの外観や動作を変更する
seo-description: コメントコンポーネントを拡張して、特定の用途についてコンポーネントの外観や動作を変更する
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# コメントコンポーネントの拡張  {#extend-comments-component}

The intention of [extending](client-customize.md#extensions) a default component is to alter the appearance or behavior of a component for specific uses.

コンポーネントへのパスは一意で、デフォルトのコンポーネントをスーパーリソースタイプとして参照します。 コンポーネントオーバーレイのグローバルスコープと比較して、スコープが制限されるため、リスクが少なくなります。

>[!NOTE]
>
>[オーバーレイ](client-customize.md#overlays)されるコンポーネントの拡張はサポートされていません。

## 例 {#example}

コメントコンポーネントのヘッダーが、AEMインスタンスの1つのサイトで別の外観で表示され、別のサイトではデフォルト表示で表示される必要があるとします。 すべてのインスタンスのコメントコンポーネントを変更するデフォルトのコメントをオーバーレイする代わりに、様々なサイトで使用できる複数のコメントコンポーネントを確実に作成する方がよい解決策です。

この解決策を実装するには、既存のコンポーネントを拡張（上書き）する新しいコンポーネントを作成し、Handlebars スクリプトを変更します。新しいコメントを使用するサイトの領域は拡張コメントを使用できますが、デフォルトの外観を使用するサイトは影響を受けません。

コメントコンポーネントは実際には、コメントシステムを構成する 2 つのコンポーネントのうちの 1 つです。Thus, there are two components to extend: *comments* and *comment*. The script to edit is in the *comment* component&#39;s `header.hbs` file, while the parent *comments* component (the comment system) is what an author actually adds to the page.

コメントを拡張するには、次の手順を実行する必要があります。

1. [コンポーネントの作成](extend-create-components.md)
1. [サンプルページへのコメントの追加](extend-sample-page.md)
1. [外観の変更](extend-alter-appearance.md)

