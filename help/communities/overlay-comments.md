---
title: コミュニティコンポーネントのオーバーレイ
seo-title: Overlay communities components
description: コミュニティコンポーネントのオーバーレイ
seo-description: Overlay communities components
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
source-wordcount: '246'
ht-degree: 34%

---

# コミュニティコンポーネントのオーバーレイ {#overlay-communities-components}

デフォルトのコンポーネントを[オーバーレイ](/help/communities/client-customize.md#overlays)する目的は、コンポーネントのすべての相対参照について、コンポーネントの外観や動作をグローバルに変更することです。これには、/libs フォルダー内で検索する前に、/apps フォルダーに解決するという sling の特性が利用されます。つまり、コンポーネントへのパスは、/apps フォルダーにあり、/libs フォルダーにはない場合を除き、デフォルトのコンポーネントへのパスと同じです。

## 例 {#example}

**コメントコンポーネントをオーバーレイ**

Web サイトのデザインに合わせてコメント機能を変更する場合は、コメントヘッダーを変更して、コメントのアバターを表示しないようにします。 アバターを非表示にするソリューションは、CSS を使用するか、ここで説明するように、アバターを含むHTMLがクライアントに送信されないように、apps フォルダー内の header.jsp をオーバーレイします。

コメントをオーバーレイするには、次の手順を実行する必要があります。

1. [コメントページ](/help/communities/overlay-create-comments-page.md)
1. [ノードの作成](/help/communities/overlay-create-nodes.md)
1. [外観の変更](/help/communities/overlay-alter-appearance.md)

**通知 E メールのオーバーレイ**

電子メール通知のメッセージをカスタマイズする場合は、次の方法でおこなうことができます。 [重ね](/help/communities/client-customize.md#overlays) テンプレートの場所： **/libs/settings/community/templates/email/html**.

例えば、（ugc が作成される特定のコミュニティコンポーネント用に）メンションメール通知を変更するには、 **if** 動詞の条件 **メンション** を有効にしたコンポーネントのテンプレートで **@mentions** サポート。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

ブログコメント内の@mentionの電子メール通知テンプレートを変更するには、次の場所にある標準のテンプレートを配置します。 `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
