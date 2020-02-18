---
title: アクティビティストリーム機能
seo-title: アクティビティストリーム機能
description: サインインしているコミュニティメンバーのアクティビティ
seo-description: サインインしているコミュニティメンバーのアクティビティ
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# アクティビティストリーム機能{#activity-streams-feature}

## 概要 {#introduction}

The activities of a signed in community member, such as posting to a forum or blog, are collected into a stream which may be filtered and displayed in various ways through configuration of the `Activity Streams` component.

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

本書では、以下の内容を説明しています。

* アクティビティストリームコンポーネントを AEM サイトに追加
* アクティビティストリームコンポーネントを設定

### アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

If it is desired to add an `Activity Streams` component to a page in author mode, use the component browser to locate

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-activities.md#essentials-for-client-side) are included, this is how the `Activity Streams` component will appear :

![chlimage_1-24](assets/chlimage_1-24.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

Select the placed `Activity Streams` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-25](assets/chlimage_1-25.png)

「**ユーザーアクティビティ**」タブでは、表示するアクティビティを指定します。

![chlimage_1-26](assets/chlimage_1-26.png)

* **アクティビティの最大数**&#x200B;表示するアクティビティの数

* **ストリームリソースパス**&#x200B;空白のままにすると、コミュニティサイトまたはコミュニティグループがデフォルトになります。ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。

* **ユーザーアクティビティビューを表示**&#x200B;オンにすると、アクティビティページに、現在のメンバーがコミュニティ内で生成するアクティビティに基づいてアクティビティをフィルタリングできるタブが表示されます。初期設定はオンです。

* **すべてのアクティビティビューを表示**&#x200B;オンにすると、アクティビティページに、現在のメンバーがアクセス権を持つコミュニティ内で生成された全アクティビティを含むタブが表示されます。初期設定はオンです。

* **次のビューを表示**&#x200B;オンにすると、アクティビティページに、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングできるタブが表示されます。初期設定はオンです。

### フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。Features that allow following are [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md), and [comments](/help/communities/comments.md).

![chlimage_1-27](assets/chlimage_1-27.png)

The **Follow **button provides a means to follow entries as activities, [notifications](/help/communities/notifications.md), or [subscriptions](/help/communities/subscriptions.md). 「**Follow **」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。 The `Email Subscriptions` selection is only present when configured.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

「**Follow **」ボタンが表示されます。

* 別のメンバーのプロファイルを表示したとき
* フォーラム、Q&amp;A およびブログなど、メイン機能のページ上で

   * その一般的な機能のすべてのアクティビティをフォローするとき

* フォーラムトピック、Q&amp;A、ブログ記事など、特定のエントリの場合

   * その特定のエントリのすべてのアクティビティをフォローするとき

### 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](/help/communities/essentials-activities.md)ページを参照してください。
