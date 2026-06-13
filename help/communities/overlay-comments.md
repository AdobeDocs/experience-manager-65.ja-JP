---
title: コミュニティコンポーネントのオーバーレイ
description: コンポーネントに対するすべての相対参照について、グローバルにコンポーネントの外観や動作を変更できるように、デフォルトコンポーネントをオーバーレイする方法について説明します。
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

# コミュニティコンポーネントのオーバーレイ {#overlay-communities-components}

デフォルトのコンポーネントを[ オーバーレイ ](/help/communities/client-customize.md#overlays)する目的は、コンポーネントに対するすべての相対参照について、コンポーネントの外観や動作をグローバルに変更することです。 /libs フォルダーで検索する前に/apps フォルダーに解決するslingの性質に依存しています。 したがって、コンポーネントへのパスは、デフォルトコンポーネントへのパスと同じですが、/apps フォルダーにあり、/libs フォルダーにはありません。

## 例 {#example}

**コメント コンポーネントをオーバーレイ**

コメント機能を変更してweb サイトのデザインと一致させるには、コメントヘッダーを変更して、コメントのアバターを表示しないようにします。 アバターを非表示にするソリューションは、CSSを使用するか、ここで説明したように、apps フォルダー内のheader.jspをオーバーレイして、アバターを含むHTMLがクライアントに送信されないようにします。

コメントをオーバーレイするには、次の操作を行う必要があります。

1. [コメントページの作成](/help/communities/overlay-create-comments-page.md)
1. [ノードの作成](/help/communities/overlay-create-nodes.md)
1. [外観の変更](/help/communities/overlay-alter-appearance.md)

**通知メールをオーバーレイ**

電子メール通知のメッセージをカスタマイズする場合は、[ テンプレートを`/libs/settings/community/templates/email/html`に](/help/communities/client-customize.md#overlays) オーバーレイすることでカスタマイズできます。

例えば、メンションメール通知を編集するとします（UGCが作成される特定のコミュニティコンポーネントの場合）。 このような場合は、**@mentions** サポートを有効にしたコンポーネントのテンプレートに、動詞&#x200B;**メンション**&#x200B;の&#x200B;**if**&#x200B;条件を追加します。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

ブログコメントの@mention用メール通知テンプレートを変更するには、標準テンプレートを`/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`に配置します。
