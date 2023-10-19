---
title: アクティビティストリーム機能
description: サインインしているコミュニティメンバーのアクティビティを、アクティビティストリームコンポーネントを通じてフィルタリングおよび表示できるストリームに収集する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 5%

---

# アクティビティストリーム機能 {#activity-streams-feature}

## はじめに {#introduction}

サインインしたコミュニティメンバーのアクティビティ（フォーラムやブログへの投稿など）は、ストリームに収集され、フィルタリングされ、様々な方法で表示されます。 `Activity Streams` コンポーネント。

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしたりすると、フォロー機能によって、アクティビティの別のビューが追加されます。

このドキュメントでは、次の内容について説明します。

* アクティビティストリームコンポーネントのAEMサイトへの追加
* アクティビティストリームコンポーネントの設定

### ページへのアクティビティストリームの追加 {#adding-activity-streams-to-a-page}

必要に応じて、 `Activity Streams` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Activity Streams`

そして、ページ上のアクティビティストリームが表示される場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](/help/communities/basics.md).

次の場合に [必要なクライアント側ライブラリ](/help/communities/essentials-activities.md#essentials-for-client-side) が含まれる場合、この方法で `Activity Streams` コンポーネントが表示されます。

![activity-streams](assets/activity-component.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

配置した `Activity Streams` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

の下 **ユーザーアクティビティ** タブで、表示するアクティビティを指定します。

![user-activities](assets/user-activities.png)

* **アクティビティの最大数**

  表示するアクティビティの数

* **ストリームリソースパス**

  空白にすると、コミュニティサイトまたはコミュニティグループがデフォルトになります。 ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。

* **ユーザーアクティビティビューを表示**

  オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成したアクティビティに基づいてアクティビティをフィルタリングするタブが表示されます。 初期設定はオンです。

* **すべてのアクティビティビューを表示**

  オンにすると、アクティビティページにタブが表示され、現在のメンバーがアクセスできるコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。

* **次のビューを表示**

  オンにすると、アクティビティページに、現在のメンバーが従っているアクティビティに基づいてアクティビティをフィルタリングするタブが表示されます。 初期設定はオンです。

### フォロービュー {#following-view}

以下を有効にするには、コンポーネントを設定する必要があります。 次の機能を使用できます。 [ブログ](/help/communities/blog-feature.md), [フォーラム](/help/communities/forum.md), [Q&amp;A](/help/communities/working-with-qna.md), [カレンダー](/help/communities/calendar.md), [ファイルライブラリ](/help/communities/file-library.md)、および [コメント](/help/communities/comments.md).

![フォロービュー](assets/following-activities.png)

The **フォロー** ボタンは、エントリをアクティビティとしてフォローする手段を提供し、 [通知](/help/communities/notifications.md)または [購読](/help/communities/subscriptions.md). 毎回、 **フォロー** ボタンが選択されている場合、選択のオン/オフを切り替えることができます。 The `Email Subscriptions` 選択が存在するのは、設定時のみです。

次のいずれかの方法を選択した場合、ボタンのテキストは **フォロー中**. 便宜上、 `Unfollow All` をクリックして、すべてのメソッドをオフにします。

The **フォロー** ボタンが表示されます。

* 別のメンバーのプロファイルを表示するとき。
* フォーラム、Q&amp;A、ブログなどのメイン機能ページ上。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムトピック、Q&amp;A 質問、ブログ記事などの特定のエントリ用。

   * その特定のエントリのすべてのアクティビティに従います。

### 追加情報 {#additional-information}

詳しくは、 [アクティビティストリームの基本事項](/help/communities/essentials-activities.md) 開発者向けのページ
