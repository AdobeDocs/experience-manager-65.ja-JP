---
title: アクティビティストリーム機能
description: サインインしたコミュニティメンバーのアクティビティをストリームに収集し、アクティビティストリームコンポーネントを通じてフィルタリングして表示する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
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
source-wordcount: '477'
ht-degree: 1%
---
# アクティビティストリーム機能 {#activity-streams-feature}

## はじめに {#introduction}

フォーラムやブログへの投稿など、サインインしたコミュニティメンバーのアクティビティは、ストリームに収集され、`Activity Streams` コンポーネントの設定を通じて様々な方法でフィルタリングおよび表示されます。

フォロー機能は、コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしたりすると、アクティビティの別のビューを追加します。

このドキュメントには、次の内容が記載されています。

* AEM サイトへのActivity Streams コンポーネントの追加
* Activity Streams コンポーネントの設定設定

### ページへのアクティビティストリームの追加 {#adding-activity-streams-to-a-page}

作成者モードでページに`Activity Streams` コンポーネントを追加する場合は、コンポーネントブラウザーを使用して検索します

* `Communities / Activity Streams`

アクティビティストリームが表示されるページ上にドラッグします。

必要な情報については、[ コミュニティコンポーネントの基本](/help/communities/basics.md)を参照してください。

[必要なクライアントサイドライブラリ ](/help/communities/essentials-activities.md#essentials-for-client-side)が含まれている場合、`Activity Streams` コンポーネントは次のように表示されます。

![activity-streams](assets/activity-component.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

配置された`Activity Streams` コンポーネントを選択して、編集ダイアログを開く`Configure` アイコンにアクセスして選択できるようにします。

![configure](assets/configure-new.png)

「**ユーザーアクティビティ**」タブで、表示するアクティビティを指定します。

![ ユーザー活動](assets/user-activities.png)

* **アクティビティの最大数**

  表示するアクティビティの数

* **ストリームリソースパス**

  コミュニティサイトまたはコミュニティグループをデフォルトにする場合は、空白のままにします。 ストリームリソースパスは、アクティビティのソースを識別します。 デフォルトは空白です。

* **ユーザーアクティビティ ビューの表示**

  オンにした場合、アクティビティページには、現在のメンバーによってコミュニティ内で生成されたアクティビティに基づいてアクティビティをフィルタリングするタブが含まれます。 デフォルトはオンです。

* **すべてのアクティビティの表示**

  オンにすると、アクティビティページには、現在のメンバーがアクセスできるコミュニティ内で生成されたすべてのアクティビティが含まれるタブが含まれます。 デフォルトはオンです。

* **次のビューを表示**

  オンにした場合、アクティビティページには、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングするタブが含まれます。 デフォルトはオンです。

### 次のビュー {#following-view}

以下を有効にするには、コンポーネントを設定する必要があります。 次の機能を許可するのは、[ ブログ ](/help/communities/blog-feature.md)、[ フォーラム ](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[ カレンダー](/help/communities/calendar.md)、[ ファイルライブラリ ](/help/communities/file-library.md)、および[ コメント ](/help/communities/comments.md)です。

![following-view](assets/following-activities.png)

「**フォロー**」ボタンは、エントリをアクティビティ、[通知](/help/communities/notifications.md)、または[ サブスクリプション ](/help/communities/subscriptions.md)としてフォローする手段を提供します。 「**フォロー**」ボタンを選択するたびに、選択範囲のオンとオフを切り替えることができます。 `Email Subscriptions`の選択は、設定時にのみ存在します。

次のいずれかの方法を選択すると、ボタンのテキストが&#x200B;**次**&#x200B;に変わります。 便宜上、`Unfollow All`を選択してすべてのメソッドをオフにすることができます。

「**フォロー**」ボタンが表示されます。

* オーディエンスの詳細を表示できます。
* フォーラム、QnA、ブログなどの主要機能ページ。

  * その一般的な機能のすべてのアクティビティに従います。

* 特定のエントリ（フォーラムのトピック、QnAの質問、ブログ記事など）。

  * その特定のエントリのすべてのアクティビティに従います。

### 追加情報 {#additional-information}

詳しくは、開発者向けの[Activity Streams Essentials](/help/communities/essentials-activities.md) ページを参照してください。
