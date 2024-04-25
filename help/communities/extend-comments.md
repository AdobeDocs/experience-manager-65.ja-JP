---
title: コメントコンポーネントの拡張
description: コメントコンポーネントを拡張して、特定の用途に合わせて外観や動作を変更する
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 7%

---

# コメントコンポーネントの拡張  {#extend-comments-component}

の目的 [の拡張](client-customize.md#extensions) デフォルトコンポーネントは、特定の用途に合わせてコンポーネントの外観や動作を変更するものです。

コンポーネントへのパスは一意で、デフォルトのコンポーネントをスーパーリソースタイプとして参照します。 コンポーネントオーバーレイのグローバルスコープに比べて範囲が制限されるので、リスクは低くなります。

>[!NOTE]
>
>の拡張 [オーバーレイ](client-customize.md#overlays) コンポーネントはサポートされていません。

## 例 {#example}

コメントコンポーネントのヘッダーが、AEM インスタンスの 1 つのサイトでは代替表示で表示され、別のサイトではデフォルト表示で表示される必要があるとします。 デフォルトのコメントをオーバーレイしてすべてのインスタンスのコメントコンポーネントを変更するのではなく、様々なサイトで複数のコメントコンポーネントを使用できるようにする方が良い解決策です。

このソリューションを実装するには、既存のコンポーネントを拡張（オーバーライド）するコンポーネントを作成し、Handlebars スクリプトを変更します。 新しいコメントを使用するサイトの領域には拡張コメントを使用できますが、既定の外観を使用するサイトには影響はありません。

コメントコンポーネントは、実際には、コメントシステムを構成する 2 つのコンポーネントの 1 つです。 したがって、拡張するコンポーネントは 2 つあります。 *コメント* および *コメント*. 編集するスクリプトは *コメント* コンポーネントの `header.hbs` ファイル、親 *コメント* コンポーネント（コメントシステム）は、作成者が実際にページに追加するものです。

コメントを拡張するには、次の操作を行う必要があります。

1. [コンポーネントの作成](extend-create-components.md)
1. [サンプルページへのコメントの追加](extend-sample-page.md)
1. [外観の変更](extend-alter-appearance.md)
