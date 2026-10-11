---
title: コメントコンポーネントの拡張
description: 「コメント」コンポーネントを拡張して、特定の用途に合わせて外観や動作を変更します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 7%
---
# コメントコンポーネントの拡張  {#extend-comments-component}

デフォルトコンポーネントを[拡張](client-customize.md#extensions)する目的は、特定の用途のためにコンポーネントの外観や動作を変更することです。

コンポーネントへのパスは一意であり、デフォルトのコンポーネントをスーパーリソースタイプとして参照します。 コンポーネントオーバーレイのグローバルスコープと比較して、スコープが制限されているため、リスクが少なくなります。

>[!NOTE]
>
>[&#x200B; オーバーレイ &#x200B;](client-customize.md#overlays) コンポーネントの拡張はサポートされていません。

## 例 {#example}

例えば、コメントコンポーネントのヘッダーは、AEM インスタンスの1つのサイトでは代替表示で表示され、別のサイトではデフォルト表示で表示される必要があるとします。 すべてのインスタンスのコメントコンポーネントを変更するデフォルトのコメントをオーバーレイする代わりに、さまざまなサイトで使用できる複数のコメントコンポーネントがあることを確認することをお勧めします。

このソリューションを実装するには、既存のコンポーネントを拡張（オーバーライド）するコンポーネントを作成し、Handlebars スクリプトを変更します。 新しいコメントを使用するサイトの領域では、拡張されたコメントを使用できますが、デフォルトのアピアランスを使用するサイトは影響を受けません。

コメントコンポーネントは、実際にはコメントシステムを構成する2つのコンポーネントのうちの1つです。 したがって、拡張する2つのコンポーネントがあります。*コメント*&#x200B;と&#x200B;*コメント*。 編集するスクリプトは、*コメント* コンポーネントの`header.hbs` ファイルにあります。一方、親&#x200B;*コメント* コンポーネント（コメントシステム）は、作成者が実際にページに追加するものです。

コメントを拡張するには、次の操作を行う必要があります。

1. [コンポーネントの作成](extend-create-components.md)
1. [サンプルページへのコメントの追加](extend-sample-page.md)
1. [外観の変更](extend-alter-appearance.md)
