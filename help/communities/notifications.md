---
title: コミュニティの通知
seo-title: Communities Notifications
description: AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知が用意されています
seo-description: AEM Communities has notifications that display events of interest to the signed-in community member
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 37%

---

# コミュニティの通知 {#communities-notifications}

## 概要 {#overview}

AEM Communities には、サインインしているコミュニティメンバーにとって興味深いイベントを表示する通知セクションが用意されています。

通知は[アクティビティ](/help/communities/essentials-activities.md)や[購読](/help/communities/subscriptions.md)と同様に、以下に基づいて生成されます。：

* コンテンツを投稿するメンバー。
* 別のメンバーに従うことを選択したメンバー。
* 特定のトピック、記事、およびコンテンツの他のスレッドに従うことを選択したメンバー。
* メンバーが、ユーザーが生成したコンテンツ内の別のコミュニティメンバーにタグ付け (@mention) します。

通知とアクティビティおよびサブスクリプションの違いは次のとおりです。

* 通知セクションへのリンクは、コミュニティサイトのヘッダーに常に存在します。

   * アクティビティには [アクティビティストリーム機能](/help/communities/functions.md#activity-stream-function) コミュニティサイトの構造に含める必要があります。
   * 購読にはが必要です [電子メールの設定](/help/communities/email.md).

* 通知の実装は、拡張性とプラグ可能な次のチャネルを通じておこなわれます。

   * アクティビティは、Web 上でのみ使用できます。
   * 購読は E メールでのみ利用できます。

コミュニティの時点 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)に設定できる通知チャネルは次のとおりです。

* Web チャネル ( `Notifications` リンク。
* E メールチャネル（E メールが正しく設定されている場合に使用できます）。

今後のチャネルとしてモバイルおよびデスクトップがあります。

### 要件 {#requirements}

**電子メールの設定**

通知の電子メールチャネルを機能させるには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](/help/communities/analytics.md)を参照してください。

**フォローの有効化**

フォローを有効にするようにコンポーネントを設定する必要があります。次の機能を使用できます。 [ブログ](/help/communities/blog-feature.md), [フォーラム](/help/communities/forum.md), [Q&amp;A](/help/communities/working-with-qna.md), [カレンダー](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md)、および [コメント](/help/communities/comments.md).

**メモ**：

* コミュニティ内で使用されるコンポーネント [サイトテンプレート](/help/communities/sites.md) および [グループテンプレート](/help/communities/tools-groups.md) は、既に従うように設定されている可能性があります。

* メンバープロファイルは、他のメンバーがフォローできるように既に設定されています。

## フォローによる通知 {#notifications-from-following}

![通知](assets/notifications.png)

「**[!UICONTROL フォロー]**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。毎回 **[!UICONTROL フォロー]** ボタンが選択されている場合、選択のオン/オフを切り替えることができます。 この `Email Subscriptions` 選択が存在するのは、設定時のみです。

フォロー方法が選択されると、ボタンのテキストが「**[!UICONTROL フォロー中]**」に変わります。 便宜上、 `Unfollow All` をクリックして、すべてのメソッドをオフにします。

この **[!UICONTROL フォロー]** ボタンが表示されます。

* 別のメンバーのプロファイルを表示する場合。
* フォーラム、Q&amp;A、ブログなどのメイン機能ページでは、次の操作を実行できます。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムトピック、Q&amp;A の質問、ブログ記事などの特定のエントリの場合：

   * その特定のエントリのすべてのアクティビティに従います。

## 通知設定の管理 {#managing-notification-settings}

通知ページから通知設定リンクを選択すると、各メンバーは通知の受信方法を管理することができます。

Web チャネルは常に有効になっています。

![notifications14](assets/notifications1.png)

電子メールチャネルでは、Web チャネルの場合と同様の設定が用意されていますが、別途適切な[電子メールの設定](/help/communities/email.md)が必要です。

電子メールチャネルは、デフォルトでオフになっています。

![notifications2](assets/notifications2.png)

これはメンバーがオンにすることもできますが、それでも電子メールの設定によって決まります。

![notifications3](assets/notifications3.png)

## 通知の表示 {#viewing-notifications}

### Web 通知 {#web-notifications}

A [ウィザードが作成したコミュニティサイト](/help/communities/sites-console.md) に、 `Notifications` 機能を使用します。 メッセージとは異なり、通知はすべてのコミュニティサイトに対して作成されますが、メッセージはサイト作成プロセス中に有効にする必要があります。

公開されたサイトにアクセスする際に、 `Notifications` リンクは、メンバーのすべての通知を表示します。

![notifications4](assets/notifications4.png)

### メール通知 {#email-notifications}

電子メールチャネルを有効にすると、メンバーは、Web 上のコンテンツへのリンクが記載されている電子メールを受信します。

![notifications5](assets/notifications5.png)

## 電子メール通知のカスタマイズ {#customize-email-notifications}

組織は、 [重ね](/help/communities/client-customize.md#overlays) テンプレートの場所： **/libs/settings/community/templates/email/html**.

例えば、（コミュニティコンポーネントの）メンションメール通知を変更するには、 **if** 動詞の条件 **メンション** を有効にしたコンポーネントのテンプレートで **@mentions** サポート。

ブログコメント内の@mentionの電子メール通知テンプレートを変更するには、次の場所にある標準のテンプレートを配置します。 **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
