---
title: コミュニティの通知
seo-title: コミュニティの通知
description: AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知が用意されています
seo-description: AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知が用意されています
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# コミュニティの通知{#communities-notifications}

## 概要 {#overview}

AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知セクションが用意されています。

通知は[アクティビティ](/help/communities/essentials-activities.md)や[購読](/help/communities/subscriptions.md)と同様に、以下に基づいて生成されます。

* コンテンツを投稿するメンバー
* 別のメンバーのフォローを選択しているメンバー
* 特定のトピックや記事などのコンテンツのスレッドのフォローを選択しているメンバー
* ユーザーが生成したコンテンツ内の別のコミュニティメンバーにタグ付け(@mention)する

通知は以下の点でアクティビティや購読と異なります。

* 通知セクションへのリンクは、常にコミュニティサイトのヘッダーに表示されています。

   * activities require the [activity stream function](/help/communities/functions.md#activity-stream-function) to be included in the community site&#39;s structure
   * subscriptions require [configuration of email](/help/communities/email.md)

* 通知は、スケーラブルでプラガブルなチャネルを介して実装されます。

   * アクティビティは Web 上のみで使用できます。
   * 購読は、電子メールを使用した場合のみ使用できます。

Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack) 以降、使用可能な通知チャネルは以下のとおりです。

* the web channel, accessed using the `Notifications` link
* 電子メールチャネル（電子メールが適切に設定されている場合に使用可能）

今後のチャネルとしてモバイルおよびデスクトップがあります。

### 要件 {#requirements}

**電子メールの設定**

通知の電子メールチャネルを機能させるには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](/help/communities/analytics.md)を参照してください。

**フォローの有効化**

フォローを有効にするようにコンポーネントを設定する必要があります。Features that allow following are [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md), and [comments](/help/communities/comments.md).

以下の点に注意してください。

* components used within community [site templates](/help/communities/sites.md) and [group templates](/help/communities/tools-groups.md) may already be configured to allow following

* メンバーのプロファイルは、既に他のメンバーがフォローできるように設定されています。

## フォローによる通知 {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

「**フォロー**」ボタンは、アクティビティ、購読、通知としてエントリをフォローする手段を提供します。 「**Follow **」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。 The `Email Subscriptions` selection is only present when configured.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

「**Follow **」ボタンが表示されます。

* 別のメンバーのプロファイルを表示したとき
* フォーラム、Q&amp;A およびブログなど、メイン機能のページ上で

   * その一般的な機能のすべてのアクティビティをフォローするとき

* フォーラムトピック、Q&amp;A、ブログ記事など、特定のエントリの場合

   * その特定のエントリのすべてのアクティビティをフォローするとき

## 通知設定の管理 {#managing-notification-settings}

通知ページから通知設定リンクを選択すると、各メンバーは通知の受信方法を管理することができます。

Web チャネルは常に有効になっています。

![chlimage_1-244](assets/chlimage_1-244.png)

電子メールチャネルでは、Web チャネルの場合と同様の設定が用意されていますが、別途適切な[電子メールの設定](/help/communities/email.md)が必要です。

電子メールチャネルは、デフォルトでオフになっています。

![chlimage_1-245](assets/chlimage_1-245.png)

これはメンバーがオンにすることもできますが、それでも電子メールの設定によって決まります。

![chlimage_1-246](assets/chlimage_1-246.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

A [wizard created community site](/help/communities/sites-console.md) now includes a link to the `Notifications` feature in the site&#39;s header bar above the banner. メッセージとは異なり、通知は各コミュニティサイトに対して作成され、メッセージはサイトの作成プロセス中に有効にする必要があります。

When visiting the published site, selecting the `Notifications` link will display all notifications for the member.

![chlimage_1-247](assets/chlimage_1-247.png)

### 電子メール通知 {#email-notifications}

電子メールチャネルを有効にすると、メンバーは、Web 上のコンテンツへのリンクが記載されている電子メールを受信します。

![chlimage_1-248](assets/chlimage_1-248.png)

## 電子メール通知のカスタマイズ {#customize-email-notifications}

組織は、/libs/settings/community/templates [/email/htmlにあるテンプレートをオー](/help/communities/client-customize.md#overlays) バーレイすることで、電子メール通知をカスタマイズできます ****。

例えば、（コミュニティコンポーネントの）メンション電子メール通知を変更するには、@mentionsのサポートを有効にしたコンポーネントのテンプレートで、Verbメンションの* ******** *条件を追加します。

ブログコメント内の@mentionの電子メール通知テンプレートを変更するには、次の場所にテンプレートを配置します。 **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/jp**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

