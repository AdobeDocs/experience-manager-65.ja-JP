---
title: コミュニティコンポーネントのオーバーレイ
description: コンポーネントへのすべての相対参照に対して、コンポーネントの外観や動作をグローバルに変更できるように、デフォルトのコンポーネントをオーバーレイする方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---

# コミュニティコンポーネントのオーバーレイ {#overlay-communities-components}

次の目的 [重ね合わせ](/help/communities/client-customize.md#overlays) デフォルトのコンポーネントでは、コンポーネントに対するすべての相対参照に対して、コンポーネントの外観や動作をグローバルに変更します。 /libs フォルダーで検索する前に/apps フォルダーに解決する Sling の性質に依存します。 したがって、コンポーネントへのパスは、/libs フォルダーではなく/apps フォルダー内にある点を除き、デフォルトコンポーネントへのパスと同じになります。

## 例 {#example}

**コメントコンポーネントをオーバーレイ**

Web サイトのデザインに合わせてコメント機能を変更する場合は、コメントヘッダーを変更して、コメントのアバターを表示しないようにします。 アバターを非表示にするソリューションは、CSS を使用するか、ここで説明するように、アバターを含むHTMLがクライアントに送信されないように、apps フォルダー内の header.jsp をオーバーレイします。

コメントをオーバーレイするには、次の操作が必要です。

1. [コメントページの作成](/help/communities/overlay-create-comments-page.md)
1. [ノードの作成](/help/communities/overlay-create-nodes.md)
1. [外観の変更](/help/communities/overlay-alter-appearance.md)

**通知 E メールのオーバーレイ**

電子メール通知のメッセージをカスタマイズする場合は、次の方法でおこなうことができます。 [重ね合わせ](/help/communities/client-customize.md#overlays) テンプレートの場所： `/libs/settings/community/templates/email/html`.

例えば、（UGC が作成される特定のコミュニティコンポーネントの）メンションメール通知を編集するとします。 その場合は、 **if** 動詞の条件 **メンション** を有効にしたコンポーネントのテンプレートで、 **@mentions** サポート。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

ブログコメント内の@mentionの電子メール通知テンプレートを変更するには、次の場所にある標準のテンプレートを配置します。 `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
