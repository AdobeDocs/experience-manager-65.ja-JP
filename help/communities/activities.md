---
title: アクティビティストリーム機能
description: ログインしたコミュニティメンバーのアクティビティを、アクティビティストリーム コンポーネントを通じてフィルタリングおよび表示できるストリームに収集する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# アクティビティストリーム機能 {#activity-streams-feature}

## はじめに {#introduction}

フォーラムやブログへの投稿など、ログインしたコミュニティメンバーのアクティビティは、`Activity Streams` コンポーネントの設定を通じて様々な方法でフィルタリングおよび表示されるストリームに収集されます。

フォローする機能により、コミュニティメンバーが興味のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしたりする場合の、アクティビティの別のビューが追加されます。

このドキュメントでは、次の内容について説明します。

* AEM サイトへのアクティビティストリーム コンポーネントの追加
* アクティビティストリームコンポーネントの設定

### ページへのアクティビティストリームの追加 {#adding-activity-streams-to-a-page}

オーサーモードで `Activity Streams` コンポーネントをページに追加する場合は、コンポーネントブラウザーを使用して以下を見つけます

* `Communities / Activity Streams`

そして、アクティビティストリームが表示されるページの上にドラッグします。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](/help/communities/basics.md) を参照してください。

[&#x200B; 必須のクライアントサイドライブラリ &#x200B;](/help/communities/essentials-activities.md#essentials-for-client-side) が含まれると、`Activity Streams` のコンポーネントは次のように表示されます。

![activity-streams](assets/activity-component.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

配置された `Activity Streams` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![&#x200B; 設定 &#x200B;](assets/configure-new.png)

「**ユーザーアクティビティ**」タブで、表示するアクティビティを指定します。

![user-activities](assets/user-activities.png)

* **アクティビティの最大数**

  表示するアクティビティ数

* **ストリームリソースパス**

  空白のままにすると、デフォルトでコミュニティサイトまたはコミュニティグループに設定されます。 ストリームリソースパスは、アクティビティのソースを識別します。 デフォルトは空白です。

* **ユーザーアクティビティビューを表示**

  オンにした場合、アクティビティ ページにはタブが含まれ、現在のメンバーによってコミュニティ内で生成されたアクティビティに基づいてアクティビティをフィルタリングします。 デフォルトではオンになっています。

* **すべてのアクティビティビューを表示**

  オンにすると、アクティビティページにはタブが含まれます。このタブには、現在のメンバーがアクセス権を持つ、コミュニティ内で生成されたすべてのアクティビティが含まれます。 デフォルトではオンになっています。

* **次のビューを表示**

  オンにすると、アクティビティページにはタブが含まれ、現在のメンバーがフォローしているものに基づいてアクティビティがフィルタリングされます。 デフォルトではオンになっています。

### 次のビュー {#following-view}

コンポーネントは、以下を有効にするように設定する必要があります。 次の機能を使用できます。[blog](/help/communities/blog-feature.md)、[forum](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[calendar](/help/communities/calendar.md)、[file library](/help/communities/file-library.md)、[comments](/help/communities/comments.md)。

![&#x200B; 次のビュー &#x200B;](assets/following-activities.png)

**フォロー** ボタンを使用すると、エントリをアクティビティ、[&#x200B; 通知 &#x200B;](/help/communities/notifications.md) または [&#x200B; 購読 &#x200B;](/help/communities/subscriptions.md) としてフォローできます。 「**フォロー**」ボタンを選択するたびに、選択のオンとオフを切り替えることができます。 `Email Subscriptions` の選択は、設定されている場合にのみ存在します。

次のメソッドのいずれかを選択すると、ボタンのテキストが **次** に変わります。 便宜上、`Unfollow All` を選択してすべてのメソッドをオフにすることができます。

**フォロー** ボタンが表示されます。

* 別のメンバーのプロファイルを表示する場合。
* フォーラム、QnA、ブログなどのメイン機能ページ

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムのトピック、QnA の質問、ブログ記事など、特定のエントリの場合。

   * その特定のエントリのすべてのアクティビティに従います。

### 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; アクティビティストリームの初期設定 &#x200B;](/help/communities/essentials-activities.md) ページを参照してください。
