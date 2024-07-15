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

コミュニティ [FP1](deploy-communities.md#latestfeaturepack) の時点では、コミュニティメンバーは、サブスクリプションと呼ばれる機能を使用して、メールを通じてコミュニティとやり取りできます。

購読は、メンバーがブログ記事、フォーラムのトピック、QnA の質問に従うときに購読できるので、[ 通知 ](notifications.md) に似ています。

購読と通知の違いは次のとおりです。

* 会員は、他の会員をフォローする場合は購読できません。
* メンバーが実行する唯一のアクションは、次の場合に `Email Subscriptions` を選択することです。
* メール返信を設定した場合、受信したメールに返信するだけで、効果的にコンテンツを投稿できます。

### 要件 {#requirements}

**メールの設定**

購読が機能し、メンバーがメールで返信するには、メールを設定する必要があります。

メールの設定手順については、[ メールの設定 ](email.md) を参照してください。

**購読を有効にしてフォロー**

サブスクリプション *および* を有効にするには、コンポーネントを設定する必要があります。 購読できる機能は、[ ブログ ](blog-feature.md)、[ フォーラム ](forum.md) および [QnA](working-with-qna.md) です。

## 購読（フォローから） {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

**フォロー** ボタンは、エントリをアクティビティ、購読、通知としてフォローする手段を提供します。 「**フォロー**」ボタンを選択するたびに、選択のオンとオフを切り替えることができます。

次のメソッドのいずれかを選択すると、ボタンのテキストが **次** に変わります。 便宜上、`Unfollow All` を選択してすべてのメソッドをオフにすることができます。

「**フォロー**」ボタンには、フォーラム、QnA またはブログがメール購読を有効にするように設定されている場合にのみ、`Email Subscriptions` オプションが含まれます。 このボタンは次のように表示されます。

* 有効化されたフォーラムのメイン機能ページで、QnA またはブログは、その機能に基づくすべてのアクティビティについてメールを送信します。

* フォーラムのトピック、QnA の質問、ブログ記事など、特定のエントリに対してアクティビティがある場合、そのエントリに対してメールが送信されます。

## メールで返信 {#reply-by-email}

メールが [ メールで返信するように設定 ](email.md#configure-polling-importer) されると、購読したメンバーには、投稿されたコンテンツとオンラインコンテンツへのリンクが記載されたメールが届きます。

ユーザーがメールに返信すると、返信に入力したコンテンツはオンラインのコンテンツとして表示されます。

![ メール返信 ](assets/email-reply.png)

返信がポストされるまでにかかる時間は、[ ポーリングインポーターの更新間隔 ](email.md#configure-polling-importer) によって制御されます。

![QA](assets/qa.png)
