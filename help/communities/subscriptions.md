---
title: コミュニティの購読
description: コミュニティメンバーは、メールを通じて他のメンバーとやり取りします
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%
---
# コミュニティの購読 {#communities-subscriptions}

## 概要 {#overview}

コミュニティ [FP1](deploy-communities.md#latestfeaturepack)の時点では、コミュニティ メンバーは、サブスクリプションと呼ばれる機能を使用して、メールを通じてコミュニティとやり取りできます。

購読は、[通知](notifications.md)と似ています。メンバーは、ブログ記事、フォーラムのトピック、QnAの質問をフォローする際に購読できます。

購読と通知の違いは次のとおりです。

* 会員は、他の会員にフォローする際に購読することはできません。
* メンバーが実行するアクションは、フォロー時に`Email Subscriptions`を選択することだけです。
* メール返信が設定されている場合、メンバーは受信したメールに返信するだけで、コンテンツを効果的に投稿できます。

### 要件 {#requirements}

**メールの設定**

購読が機能し、メンバーがメールで返信するには、メールを設定する必要があります。

電子メールの設定方法については、[電子メールの設定](email.md)を参照してください。

**サブスクリプションを有効にしてフォローする**

次のサブスクリプション *および*&#x200B;を有効にするには、コンポーネントを設定する必要があります。 サブスクリプションを許可する機能は、[ ブログ ](blog-feature.md)、[ フォーラム ](forum.md)、[QnA](working-with-qna.md)です。

## フォローからの購読 {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

「**フォロー**」ボタンは、アクティビティ、サブスクリプション、通知などのエントリをフォローするための手段を提供します。 「**フォロー**」ボタンを選択するたびに、選択範囲のオンとオフを切り替えることができます。

次のいずれかの方法を選択すると、ボタンのテキストが&#x200B;**次**&#x200B;に変わります。 便宜上、`Unfollow All`を選択してすべてのメソッドをオフにすることができます。

**フォロー** ボタンには、`Email Subscriptions` オプションが含まれます。これは、フォーラム、QnA、またはブログがメール購読を有効にするように設定されている場合に限られます。 このボタンは次のように表示されます。

* 有効になっているフォーラム、QnA、またはブログのメイン機能ページでは、その機能の下にあるすべてのアクティビティに関するメールが送信されます。

* フォーラムのトピック、QnAの質問、ブログ記事など、特定のエントリのアクティビティが発生すると、そのエントリに対してメールが送信されます。

## メールで返信 {#reply-by-email}

電子メールが[電子メールで返信するように設定されている場合](email.md#configure-polling-importer)、購読者は、投稿されたコンテンツとオンラインコンテンツへのリンクが記載された電子メールを受け取ります。

返信先が電子メールに返信した場合、返信先に入力したコンテンツがオンラインでコンテンツとして表示されます。

![email-reply](assets/email-reply.png)

返信が投稿されるまでの時間は、[ ポーリングインポーターの更新間隔](email.md#configure-polling-importer)によって制御されます。

![QA](assets/qa.png)
