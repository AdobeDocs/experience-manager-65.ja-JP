---
title: Communities コンポーネントをオーバーレイ
description: コンポーネントに関連するすべての参照について、デフォルトのコンポーネントをオーバーレイして、コンポーネントの外観や動作をグローバルに変更する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---

# Communities コンポーネントをオーバーレイ {#overlay-communities-components}

デフォルトコンポーネントを [ オーバーレイ ](/help/communities/client-customize.md#overlays) して表示する目的は、コンポーネントに関連するすべての参照について、そのコンポーネントの外観や動作をグローバルに変更することです。 これは、/libs フォルダーで検索する前に/apps フォルダーに解決される sling の性質に依存します。 そのため、コンポーネントのパスは、/libs フォルダーではなく/apps フォルダーにあることを除いて、デフォルトコンポーネントへのパスと同一です。

## 例 {#example}

**コメントコンポーネントをオーバーレイ**

コメント機能を変更して web サイトのデザインと一致するようにする場合は、コメントのヘッダーを変更し、コメントのアバターが表示されないようにします。 アバターを非表示にするためのソリューションは、CSS を使用するか、後述のように、apps フォルダーの header.jsp をオーバーレイして、アバターを含むHTMLがクライアントに送信されないようにします。

コメントをオーバーレイするには、次の操作を行う必要があります。

1. [コメントページの作成](/help/communities/overlay-create-comments-page.md)
1. [ノードの作成](/help/communities/overlay-create-nodes.md)
1. [外観の変更](/help/communities/overlay-alter-appearance.md)

**通知メールをオーバーレイ**

例えば、メール通知のメッセージをカスタマイズする場合は、`/libs/settings/community/templates/email/html` のテンプレートを [ オーバーレイ ](/help/communities/client-customize.md#overlays) することで行うことができます。

例えば、（UGC が作成された特定の Communities コンポーネントの）メンションメール通知を編集するとします。 その場合、**@mentions** サポートを有効にしたコンポーネントのテンプレートに動詞 **メンション** の **if** 条件を追加します。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

ブログコメント内の@mention のメール通知テンプレートを変更するには、次の場所に標準テンプレートを配置します。`/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
