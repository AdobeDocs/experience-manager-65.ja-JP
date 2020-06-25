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
source-git-commit: 10c17fc199c476ec66059cc6bf4cbb4a0ff1af40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 31%

---


# アクティビティストリーム機能 {#activity-streams-feature}

## 概要 {#introduction}

The activities of a signed in community member, such as posting to a forum or blog, are collected into a stream which may be filtered and displayed in various ways through configuration of the `Activity Streams` component.

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

このドキュメントでは、次の内容を説明します。

* AEMサイトへのアクティビティストリームコンポーネントの追加
* アクティビティストリームコンポーネントの構成設定

### アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

If it is desired to add an `Activity Streams` component to a page in author mode, use the component browser to locate

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

[必要なクライアント側ライブラリが含まれる場合](/help/communities/essentials-activities.md#essentials-for-client-side) 、次のようにコンポー `Activity Streams` ネントが表示されます。

![chlimage_1-195](assets/chlimage_1-195.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

Select the placed `Activity Streams` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-494](assets/chlimage_1-494.png)

「**ユーザーアクティビティ**」タブでは、表示するアクティビティを指定します。

![ユーザーアクティビティ](assets/user-activities.png)

* **アクティビティの最大数**

   表示するアクティビティ数

* **ストリームリソースパス**

   コミュニティサイトまたはコミュニティグループをデフォルトにする場合は、空白のままにします。 ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。

* **ユーザーアクティビティビューを表示**

   このオプションを選択すると、アクティビティページに、現在のメンバーによってコミュニティ内で生成されたアクティビティに基づいてフィルターがするタブが含まれます。 初期設定はオンです。

* **すべてのアクティビティビューを表示**

   このオプションを選択すると、アクティビティページにタブが含まれ、現在のアクティビティがアクセス権を持つコミュニティ内で生成されたすべてのメンバーが含まれます。 初期設定はオンです。

* **次のビューを表示**

   オンにすると、アクティビティページに、現在のメンバーに基づくフィルターアクティビティがたどっているタブが含まれます。 初期設定はオンです。

### フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。Features that allow following are [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md), and [comments](/help/communities/comments.md).

![chlimage_1-5](assets/chlimage_1-5.png)

The **Follow** button provides a means to follow entries as activities, [notifications](/help/communities/notifications.md), or [subscriptions](/help/communities/subscriptions.md). Each time the **Follow** button is selected, it is possible to toggle on or off a selection. The `Email Subscriptions` selection is only present when configured.

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 For convenience, it is possible to select `Unfollow All` to toggle off all methods.

The **Follow** button will appear:

* 別のメンバーのプロファイルを表示するとき。
* フォーラム、QnA、ブログなど、メイン機能ページ。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムトピック、QnA質問、ブログ記事など、特定のエントリに対して使用します。

   * 特定のエントリのすべてのアクティビティに従います。

### 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](/help/communities/essentials-activities.md)ページを参照してください。
