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

通知は以下に似ています [activities](/help/communities/essentials-activities.md) および [subscriptions](/help/communities/subscriptions.md) その原因としては、以下が考えられます。

* コンテンツを投稿するメンバー。
* 別のメンバーのフォローを選択したメンバー。
* 特定のトピック、記事、その他のコンテンツスレッドをフォローすることを選択したメンバー。
* メンバーのタグ付け（@mention）は、ユーザーが生成したコンテンツ内の別のコミュニティメンバーです。

通知をアクティビティや購読と区別するのは次のとおりです。

* 通知セクションへのリンクは、常にコミュニティサイトのヘッダーに存在します。

   * アクティビティでは、以下が必要です [アクティビティストリーム関数](/help/communities/functions.md#activity-stream-function) コミュニティサイトの構造に含める必要があります。
   * 購読には次が必要です： [メールの設定](/help/communities/email.md).

* 通知の実装は、スケーラブルでプラグ可能なチャネルを通じて行われます。

   * アクティビティは、web でのみ使用できます。
   * 購読は、メールでのみ利用できます。

コミュニティの場合 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)使用できる通知チャネルは次のとおりです。

* Web チャネル（を使用してアクセス） `Notifications` リンク。
* E メールチャネル。E メールが適切に設定されている場合に使用できます。

今後のチャネルはモバイルとデスクトップです。

### 要件 {#requirements}

**メールを設定**

通知のメールチャネルを機能させるには、メールを設定する必要があります。

メールの設定手順については、を参照してください。 [メールの設定](/help/communities/analytics.md).

**フォローを有効にする**

コンポーネントは、以下を有効にするように設定する必要があります。 次の機能を使用できます [ブログ](/help/communities/blog-feature.md), [フォーラム](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [カレンダー](/help/communities/calendar.md), [ライブラリ](/help/communities/file-library.md)、および [コメント](/help/communities/comments.md).

**メモ**：

* コミュニティ内で使用されるコンポーネント [サイトテンプレート](/help/communities/sites.md) および [グループテンプレート](/help/communities/tools-groups.md) はフォローするように既に設定されている可能性があります。

* メンバープロファイルは、他のメンバーがフォローできるように既に設定されています。

## 以下からの通知 {#notifications-from-following}

![通知](assets/notifications.png)

この **[!UICONTROL フォロー]** ボタンを使用すると、エントリをアクティビティ、購読、通知として追跡できます。 毎回 **[!UICONTROL フォロー]** ボタンが選択されている場合、選択のオンとオフを切り替えることができます。 この `Email Subscriptions` 選択は、設定されている場合にのみ存在します。

次のいずれかの方法を選択した場合、ボタンのテキストは **[!UICONTROL 次の]**. 便宜上、以下を選択できます。 `Unfollow All` すべてのメソッドの表示/非表示を切り替えます。

この **[!UICONTROL フォロー]** ボタンが表示されます：

* 別のメンバーのプロファイルを表示する場合。
* フォーラム、QnA、ブログなどのメインの機能ページで、次の操作を行います。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムのトピック、QnA の質問、ブログ記事など、特定のエントリの場合：

   * その特定のエントリのすべてのアクティビティに従います。

## 通知設定の管理 {#managing-notification-settings}

通知ページから「通知設定」リンクを選択すると、各メンバーで通知の受信方法を管理できます。

Web チャネルは常に有効です。

![通知 14](assets/notifications1.png)

メールチャネル（適切なものに依存） [メールの設定](/help/communities/email.md)は、web チャネルと同じ設定を提供します。

メールチャネルはデフォルトでオフになっています。

![notifications2](assets/notifications2.png)

メンバーがオンにしている場合もありますが、メールの設定によっては変わりません。

![notifications3](assets/notifications3.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

A [ウィザードがコミュニティサイトを作成しました](/help/communities/sites-console.md) には、へのリンクが含まれるようになりました `Notifications` バナーの上にあるサイトのヘッダーバーの機能。 メッセージとは異なり、通知はコミュニティサイトごとに作成されますが、サイト作成プロセス中はメッセージを有効にする必要があります。

公開済みサイトにアクセスする際に、を選択する `Notifications` リンクは、メンバーのすべての通知を表示します。

![notifications4](assets/notifications4.png)

### メール通知 {#email-notifications}

メールチャネルを有効にすると、メンバーは、web 上のコンテンツへのリンクを含むメールを受け取ります。

![通知 5](assets/notifications5.png)

## メール通知のカスタマイズ {#customize-email-notifications}

組織は、次の方法でメール通知をカスタマイズできます [オーバーレイ](/help/communities/client-customize.md#overlays) のテンプレート **/libs/settings/community/templates/email/html**.

例えば、（コミュニティコンポーネントの）メンションメール通知を変更するには、 **もし** 動詞の条件 **メンション** を有効にしたコンポーネントのテンプレートで **@mentions** サポート。

ブログコメントに含まれる@mention のメール通知テンプレートを変更するには、標準テンプレートを次の場所に配置します。 **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
