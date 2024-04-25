---
title: コミュニティの購読
description: コミュニティメンバーは、メールで他のメンバーとやり取りします
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# コミュニティの購読 {#communities-subscriptions}

## 概要 {#overview}

コミュニティの場合 [FP1](deploy-communities.md#latestfeaturepack)の場合、コミュニティメンバーは、購読と呼ばれる機能を使用して、メールでコミュニティとやり取りできます。

サブスクリプションは次に似ています [通知](notifications.md) 会員は、ブログ記事、フォーラムのトピック、または QnA の質問に従うときに購読することができます。

購読と通知の違いは次のとおりです。

* 会員は、他の会員をフォローする場合は購読できません。
* メンバーが行う唯一のアクションは、 `Email Subscriptions` フォローする場合。
* メール返信を設定した場合、受信したメールに返信するだけで、効果的にコンテンツを投稿できます。

### 要件 {#requirements}

**メールを設定**

購読が機能し、メンバーがメールで返信するには、メールを設定する必要があります。

メールの設定手順については、を参照してください。 [メールの設定](email.md).

**購読を有効にしてフォロー**

購読を有効にするには、コンポーネントを設定する必要があります *および* 次のとおりです。 購読を許可する機能は次のとおりです [ブログ](blog-feature.md), [フォーラム](forum.md) および [QnA](working-with-qna.md).

## 購読（フォローから） {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

この **フォロー** ボタンを使用すると、エントリをアクティビティ、購読、通知として追跡できます。 毎回 **フォロー** ボタンが選択されている場合、選択のオンとオフを切り替えることができます。

次のいずれかの方法を選択した場合、ボタンのテキストは **次の**. 便宜上、以下を選択できます。 `Unfollow All` すべてのメソッドの表示/非表示を切り替えます。

この **フォロー** ボタンには、 `Email Subscriptions` メール購読を有効にするようにフォーラム、QnA またはブログが設定されている場合にのみ選択します。 このボタンは次のように表示されます。

* 有効化されたフォーラムのメイン機能ページで、QnA またはブログは、その機能に基づくすべてのアクティビティについてメールを送信します。

* フォーラムのトピック、QnA の質問、ブログ記事など、特定のエントリに対してアクティビティがある場合、そのエントリに対してメールが送信されます。

## メールで返信 {#reply-by-email}

電子メールが [電子メールで返信するように設定](email.md#configure-polling-importer)を購読したメンバーには、投稿されたコンテンツとオンラインコンテンツへのリンクが記載されたメールが届きます。

ユーザーがメールに返信すると、返信に入力したコンテンツはオンラインのコンテンツとして表示されます。

![email-reply](assets/email-reply.png)

返信が投稿されるまでにかかる時間は、によって制御されます。 [ポーリングインポーターの更新間隔](email.md#configure-polling-importer).

![QA](assets/qa.png)
