---
title: コミュニティコンポーネントのオーバーレイ
seo-title: コミュニティコンポーネントのオーバーレイ
description: コミュニティコンポーネントのオーバーレイ
seo-description: コミュニティコンポーネントのオーバーレイ
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 34%

---

# コミュニティコンポーネント{#overlay-communities-components}のオーバーレイ

デフォルトのコンポーネントを[オーバーレイ](/help/communities/client-customize.md#overlays)する目的は、コンポーネントのすべての相対参照について、コンポーネントの外観や動作をグローバルに変更することです。これには、/libs フォルダー内で検索する前に、/apps フォルダーに解決するという sling の特性が利用されます。つまり、コンポーネントへのパスは、/apps フォルダーにあり、/libs フォルダーにはない場合を除き、デフォルトのコンポーネントへのパスと同じです。

## 例 {#example}

**コメントコンポーネントのオーバーレイ**

コメント機能を変更してWebサイトのデザインに合わせ、コメントヘッダーを変更して、コメントのアバターが表示されないようにするとします。 アバターを非表示にするソリューションは、CSSを使用するか、ここで説明するように、アバターを含むHTMLがクライアントに送信されないように、appsフォルダー内のheader.jspをオーバーレイします。

コメントをオーバーレイするには、次の手順を実行する必要があります。

1. [コメントページ](/help/communities/overlay-create-comments-page.md)
1. [ノードの作成](/help/communities/overlay-create-nodes.md)
1. [外観の変更](/help/communities/overlay-alter-appearance.md)

**通知電子メールのオーバーレイ**

電子メール通知のメッセージをカスタマイズする場合は、**/libs/settings/community/templates/email/html**&#x200B;にあるテンプレートを[オーバーレイ](/help/communities/client-customize.md#overlays)してカスタマイズできます。

例えば、（ugcが作成される特定のコミュニティコンポーネントの）メンション電子メール通知を変更するには、**@mentions**&#x200B;サポートを有効にしたコンポーネントのテンプレートに、動詞&#x200B;**mention**&#x200B;の&#x200B;**if**&#x200B;条件を追加します。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

ブログコメント内の@mentionの電子メール通知テンプレートを変更するには、次の場所に標準テンプレートを配置します。`/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
