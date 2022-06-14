---
title: コミュニティの購読
seo-title: Communities Subscriptions
description: コミュニティメンバーは他のメンバーと電子メールでやり取りします
seo-description: Community members interact with other members through email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 46%

---

# コミュニティの購読 {#communities-subscriptions}

## 概要 {#overview}

コミュニティの時点 [FP1](deploy-communities.md#latestfeaturepack)コミュニティメンバーは、購読と呼ばれる機能を使用して、電子メールを通じてコミュニティとやり取りすることができます。

購読は、 [通知](notifications.md) ブログ記事、フォーラムトピック、Q&amp;A の質問に従う際に、メンバーが購読する場合があります。

購読が通知と異なるのは以下の点です。

* メンバーは、他のメンバーをフォローする際に購読できません。
* メンバーが実行するアクションは、選択するだけです `Email Subscriptions` 後に続く場合
* 電子メールの返信が設定されている場合、メンバーは受信した電子メールに返信するだけで、効果的にコンテンツを投稿できます。

### 要件 {#requirements}

**電子メールの設定**

購読を機能させ、メンバーが電子メールで返信できるようにするには、電子メールを設定する必要があります。

電子メールを設定する手順については、[電子メールの設定](email.md)を参照してください。

**購読とフォローの有効化**

購読とフォローの両方を有効にするようコンポーネントを設定する必要があります。**&#x200B;サブスクリプションを許可する機能は、 [ブログ](blog-feature.md), [フォーラム](forum.md) および [Q&amp;A](working-with-qna.md).

## フォローからの購読 {#subscriptions-from-following}

![購読フォロー](assets/subscription-following.png)

「**フォロー**」ボタンを使用すると、エントリをアクティビティや購読、通知としてフォローできます。毎回 **フォロー** ボタンが選択されている場合、選択のオン/オフを切り替えることができます。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、 `Unfollow All` をクリックして、すべてのメソッドをオフにします。

この **フォロー** ボタンに `Email Subscriptions` オプションは、フォーラム、Q&amp;A またはブログが電子メール購読を有効にするように設定されている場合にのみ有効です。 このボタンは次のように表示されます。

* 有効なフォーラム、Q&amp;A、またはブログのメイン機能ページで、その機能の下にあるすべてのアクティビティに関するメールを送信します。

* フォーラムトピック、Q&amp;A 質問、ブログ記事などの特定のエントリに対して、その特定のエントリに対するアクティビティがある場合にメールを送信します。

## 電子メールによる返信 {#reply-by-email}

[電子メールによる返信の設定](email.md#configure-polling-importer)が電子メールでおこなわれている場合、購読したメンバーは、投稿されたコンテンツとオンラインコンテンツへのリンクが含まれた電子メールを受け取ります。

これらのメンバーが電子メールに返信すると、返信に入力したコンテンツがオンラインコンテンツとして投稿されます。

![電子メールの返信](assets/email-reply.png)

返信の投稿にかかる時間は、[ポーリングインポーターの更新間隔](email.md#configure-polling-importer)で制御します。

![QA](assets/qa.png)
