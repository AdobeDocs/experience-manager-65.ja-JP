---
title: コメントコンポーネントの拡張
seo-title: Extend Comments Component
description: コメントコンポーネントを拡張して、特定の用途についてコンポーネントの外観や動作を変更する
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 30%

---

# コメントコンポーネントの拡張  {#extend-comments-component}

次の目的 [拡張](client-customize.md#extensions) デフォルトのコンポーネントは、特定の用途でのコンポーネントの外観や動作を変更することです。

コンポーネントへのパスは一意で、デフォルトのコンポーネントをスーパーリソースタイプとして参照します。 コンポーネントオーバーレイのグローバルスコープと比較して、スコープが制限されるので、リスクが少なくなります。

>[!NOTE]
>
>[オーバーレイ](client-customize.md#overlays)されるコンポーネントの拡張はサポートされていません。

## 例 {#example}

コメントコンポーネントのヘッダーが、AEMインスタンスの 1 つのサイトで別の外観で表示され、別のサイトではデフォルトの表示で表示される必要があるとします。 すべてのインスタンスのコメントコンポーネントを変更するデフォルトのコメントをオーバーレイする代わりに、様々なサイトで使用できる複数のコメントコンポーネントを確実に使用する方法をお勧めします。

この解決策を実装するには、既存のコンポーネントを拡張（上書き）する新しいコンポーネントを作成し、Handlebars スクリプトを変更します。新しいコメントを使用するサイトの領域は拡張されたものを使用できますが、デフォルトの外観を使用するサイトは影響を受けません。

コメントコンポーネントは実際には、コメントシステムを構成する 2 つのコンポーネントのうちの 1 つです。そのため、次の 2 つのコンポーネントを拡張できます。 *コメント* および *コメント*. 編集するスクリプトは、 *コメント* コンポーネントの `header.hbs` ファイルを、親 *コメント* コンポーネント（コメントシステム）は、作成者が実際にページに追加するものです。

コメントを拡張するには、次の手順を実行する必要があります。

1. [コンポーネントの作成](extend-create-components.md)
1. [サンプルページへのコメントの追加](extend-sample-page.md)
1. [外観の変更](extend-alter-appearance.md)
