---
title: コミュニティの購読
seo-title: コミュニティの購読
description: コミュニティメンバーは他のメンバーと電子メールでやり取りします
seo-description: コミュニティメンバーは他のメンバーと電子メールでやり取りします
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# コミュニティの購読 {#communities-subscriptions}

## 概要 {#overview}

As of Communities [FP1](deploy-communities.md#latestfeaturepack), community members may interact with the community through email using a feature referrred to as subscriptions.

Subscriptions are similar to [notifications](notifications.md) as members may subscribe when following blog articles, forum topics or QnA questions.

購読が通知と異なるのは以下の点です。

* 会員は、他の会員をフォローする場合は、引き受けることができない。
* The only action for members to take is to select `Email Subscriptions` when following.
* 電子メールの返信が設定されている場合、受信した電子メールに返信するだけで、メンバーは効果的にコンテンツを投稿できます。

### 要件 {#requirements}

**電子メールの設定**

購読を機能させ、メンバーが電子メールで返信できるようにするには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](email.md)を参照してください。

**購読とフォローの有効化**

購読とフォローの両方を有効にするようコンポーネントを設定する必要があります。** Features that allow subscriptions are [blog](blog-feature.md), [forum](forum.md) and [QnA](working-with-qna.md).

## フォローからの購読 {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

「**フォロー**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。Each time the **Follow** button is selected, it is possible to toggle on or off a selection.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

The **Follow** button will include the `Email Subscriptions` option only when a forum, QnA, or blog is configured to enable email subscriptions. 次のボタンが表示されます。

* 有効になっているフォーラム、QnAまたはブログのメイン機能ページで、その機能を使用するすべてのアクティビティに関する電子メールを送信します。

* フォーラムトピック、QnA質問、ブログ記事など、特定の参加者に関するアクティビティがある場合は、その参加者に対して電子メールが送信されます。

## 電子メールによる返信 {#reply-by-email}

[電子メールによる返信の設定](email.md#configure-polling-importer)が電子メールでおこなわれている場合、購読したメンバーは、投稿されたコンテンツとオンラインコンテンツへのリンクが含まれた電子メールを受け取ります。

これらのメンバーが電子メールに返信すると、返信に入力したコンテンツがオンラインコンテンツとして投稿されます。

![chlimage_1-6](assets/chlimage_1-6.png)

返信の投稿にかかる時間は、[ポーリングインポーターの更新間隔](email.md#configure-polling-importer)で制御します。

![chlimage_1-7](assets/chlimage_1-7.png)

