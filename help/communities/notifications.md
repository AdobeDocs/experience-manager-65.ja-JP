---
title: コミュニティの通知
description: AEM Communitiesには、ログインしたコミュニティメンバーが関心を持つイベントを表示する通知があります
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# コミュニティの通知 {#communities-notifications}

## 概要 {#overview}

AEM Communitiesには「通知」セクションがあり、ログインしたコミュニティメンバーが関心を持つイベントが表示されます。

通知は、以下に起因する可能性があるので、[&#x200B; アクティビティ &#x200B;](/help/communities/essentials-activities.md) および [&#x200B; 購読 &#x200B;](/help/communities/subscriptions.md) に似ています。

* コンテンツを投稿するメンバー。
* 別のメンバーのフォローを選択したメンバー。
* 特定のトピック、記事、その他のコンテンツスレッドをフォローすることを選択したメンバー。
* メンバーのタグ付け（@mention）は、ユーザーが生成したコンテンツ内の別のコミュニティメンバーです。

通知をアクティビティや購読と区別するのは次のとおりです。

* 通知セクションへのリンクは、常にコミュニティサイトのヘッダーに存在します。

   * アクティビティを使用するには、[&#x200B; アクティビティストリーム関数 &#x200B;](/help/communities/functions.md#activity-stream-function) をコミュニティサイトの構造に含める必要があります。
   * 購読には [&#x200B; メールの設定 &#x200B;](/help/communities/email.md) が必要です。

* 通知の実装は、スケーラブルでプラグ可能なチャネルを通じて行われます。

   * アクティビティは、web でのみ使用できます。
   * 購読は、メールでのみ利用できます。

Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack) では、次の通知チャネルを使用できます。

* Web チャネル。`Notifications` リンクを使用してアクセスします。
* E メールチャネル。E メールが適切に設定されている場合に使用できます。

今後のチャネルはモバイルとデスクトップです。

### 要件 {#requirements}

**メールの設定**

通知のメールチャネルを機能させるには、メールを設定する必要があります。

メールの設定手順については、[&#x200B; メールの設定 &#x200B;](/help/communities/analytics.md) を参照してください。

**フォローを有効にする**

コンポーネントは、以下を有効にするように設定する必要があります。 次の機能を使用できます。[blog](/help/communities/blog-feature.md)、[forum](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[calendar](/help/communities/calendar.md)、[filelibrary](/help/communities/file-library.md)、[comments](/help/communities/comments.md)。

**メモ**：

* コミュニティ [&#x200B; サイトテンプレート &#x200B;](/help/communities/sites.md) および [&#x200B; グループテンプレート &#x200B;](/help/communities/tools-groups.md) 内で使用するコンポーネントは、既にフォローするように設定されていることがあります。

* メンバープロファイルは、他のメンバーがフォローできるように既に設定されています。

## 以下からの通知 {#notifications-from-following}

![&#x200B; 通知 &#x200B;](assets/notifications.png)

**[!UICONTROL フォロー]** ボタンは、エントリをアクティビティ、購読、通知としてフォローする手段を提供します。 「**[!UICONTROL フォロー]**」ボタンを選択するたびに、選択のオンとオフを切り替えることができます。 `Email Subscriptions` の選択は、設定されている場合にのみ存在します。

次のメソッドのいずれかを選択すると、ボタンのテキストが **[!UICONTROL 次]** に変わります。 便宜上、`Unfollow All` を選択してすべてのメソッドをオフにすることができます。

**[!UICONTROL フォロー]** ボタンが表示されます。

* 別のメンバーのプロファイルを表示する場合。
* フォーラム、QnA、ブログなどのメインの機能ページで、次の操作を行います。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムのトピック、QnA の質問、ブログ記事など、特定のエントリの場合：

   * その特定のエントリのすべてのアクティビティに従います。

## 通知設定の管理 {#managing-notification-settings}

通知ページから「通知設定」リンクを選択すると、各メンバーで通知の受信方法を管理できます。

Web チャネルは常に有効です。

![notifications14](assets/notifications1.png)

メールチャネルは、適切な [&#x200B; メールの設定 &#x200B;](/help/communities/email.md) に依存し、web チャネルの場合と同じ設定を提供します。

メールチャネルはデフォルトでオフになっています。

![notifications2](assets/notifications2.png)

メンバーがオンにしている場合もありますが、メールの設定によっては変わりません。

![notifications3](assets/notifications3.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

[&#x200B; ウィザードで作成されたコミュニティサイト &#x200B;](/help/communities/sites-console.md) に、バナーの上にあるサイトのヘッダーバーに `Notifications` 機能へのリンクが含まれるようになりました。 メッセージとは異なり、通知はコミュニティサイトごとに作成されますが、サイト作成プロセス中はメッセージを有効にする必要があります。

公開済みサイトにアクセスして「`Notifications`」リンクを選択すると、メンバーに関するすべての通知が表示されます。

![notifications4](assets/notifications4.png)

### メール通知 {#email-notifications}

メールチャネルを有効にすると、メンバーは、web 上のコンテンツへのリンクを含むメールを受け取ります。

![notifications5](assets/notifications5.png)

## メール通知のカスタマイズ {#customize-email-notifications}

組織は、**/libs/settings/community/templates/email/html[&#x200B; にあるテンプレートを &#x200B;](/help/communities/client-customize.md#overlays) オーバーレイ** することで、メール通知をカスタマイズできます。

例えば、（コミュニティコンポーネントの）メンションメール通知を変更するには、**@mentions** サポートを有効にしたコンポーネントのテンプレートに動詞 **メンション** の **if** 条件を追加します。

ブログコメント内の@mention のメール通知テンプレートを変更するには、次の場所に標準テンプレートを配置します。**/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
