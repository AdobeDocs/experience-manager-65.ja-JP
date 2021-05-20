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
role: Administrator
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 48%

---

# コミュニティの購読 {#communities-subscriptions}

## 概要 {#overview}

コミュニティ[FP1](deploy-communities.md#latestfeaturepack)の時点で、コミュニティメンバーは、購読と呼ばれる機能を使用して、Eメールでコミュニティとやり取りできます。

購読は[通知](notifications.md)に似ています。ブログ記事、フォーラムトピックまたはQ&amp;Aの質問をフォローする際に、メンバーが購読する可能性があります。

購読が通知と異なるのは以下の点です。

* メンバーは、他のメンバーをフォローする際に購読できません。
* メンバーが実行する唯一のアクションは、フォロー中に`Email Subscriptions`を選択することです。
* 電子メールの返信を設定すると、メンバーは受信した電子メールに返信するだけで、効果的にコンテンツを投稿できます。

### 要件 {#requirements}

**電子メールの設定**

購読を機能させ、メンバーが電子メールで返信できるようにするには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](email.md)を参照してください。

**購読とフォローの有効化**

購読とフォローの両方を有効にするようコンポーネントを設定する必要があります。**&#x200B;購読を許可する機能は、[blog](blog-feature.md)、[forum](forum.md)、[Q&amp;A](working-with-qna.md)です。

## フォローからの購読 {#subscriptions-from-following}

![購読フォロー](assets/subscription-following.png)

「**フォロー**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。「**フォロー**」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、`Unfollow All`を選択してすべてのメソッドをオフに切り替えることができます。

「**フォロー**」ボタンには、電子メール購読を有効にするようにフォーラム、Q&amp;Aまたはブログが設定されている場合にのみ、`Email Subscriptions`オプションが含まれます。 このボタンは、次のように表示されます。

* 有効なフォーラム、Q&amp;A、またはブログのメイン機能ページで、その機能の下にあるすべてのアクティビティに関する電子メールを送信します。

* フォーラムトピック、Q&amp;A質問、ブログ記事などの特定のエントリに対して、その特定のエントリのアクティビティがある場合に電子メールを送信します。

## 電子メールによる返信 {#reply-by-email}

[電子メールによる返信の設定](email.md#configure-polling-importer)が電子メールでおこなわれている場合、購読したメンバーは、投稿されたコンテンツとオンラインコンテンツへのリンクが含まれた電子メールを受け取ります。

これらのメンバーが電子メールに返信すると、返信に入力したコンテンツがオンラインコンテンツとして投稿されます。

![email-reply](assets/email-reply.png)

返信の投稿にかかる時間は、[ポーリングインポーターの更新間隔](email.md#configure-polling-importer)で制御します。

![QA](assets/qa.png)
