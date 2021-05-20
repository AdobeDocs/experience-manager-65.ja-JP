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
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 31%

---

# アクティビティストリーム機能 {#activity-streams-feature}

## はじめに {#introduction}

フォーラムやブログへの投稿など、サインインしたコミュニティメンバーのアクティビティは、ストリームに収集され、`Activity Streams`コンポーネントの設定を通じて様々な方法でフィルタリングおよび表示できます。

コミュニティメンバーが関心のある投稿をフォローしたり、他のコミュニティメンバーのアクティビティをフォローしているときは、フォロー機能によって、アクティビティを別の見方で捉えることができます。

このドキュメントでは、次の内容について説明します。

* アクティビティストリームコンポーネントのAEMサイトへの追加
* アクティビティストリームコンポーネントの設定

### アクティビティストリームをページに追加 {#adding-activity-streams-to-a-page}

`Activity Streams`コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Activity Streams`

コンポーネントを探し、ページ上のアクティビティストリームを表示したい位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](/help/communities/basics.md)を参照してください。

[必須のクライアント側ライブラリ](/help/communities/essentials-activities.md#essentials-for-client-side)を含めると、`Activity Streams`コンポーネントは次のように表示されます。

![activity-streams](assets/activity-component.png)

### アクティビティストリームの設定 {#configuring-activity-streams}

配置済みの`Activity Streams`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

「**ユーザーアクティビティ**」タブでは、表示するアクティビティを指定します。

![user-activities](assets/user-activities.png)

* **アクティビティの最大数**

   表示するアクティビティの数

* **ストリームリソースパス**

   コミュニティサイトまたはコミュニティグループをデフォルトにする場合は空のままにします。 ストリームリソースパスは、アクティビティのソースを識別します。 初期設定は空白です。

* **ユーザーアクティビティビューを表示**

   オンにすると、アクティビティページにタブが表示され、現在のメンバーがコミュニティ内で生成したアクティビティに基づいてアクティビティをフィルタリングできます。 初期設定はオンです。

* **すべてのアクティビティビューを表示**

   オンにすると、アクティビティページにタブが表示され、現在のメンバーがアクセス権を持つコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定はオンです。

* **次のビューを表示**

   オンにすると、アクティビティページに、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングするタブが表示されます。 初期設定はオンです。

### フォロービュー {#following-view}

フォローを有効にするようにコンポーネントを設定する必要があります。以下を可能にする機能には、[blog](/help/communities/blog-feature.md)、[forum](/help/communities/forum.md)、[Q&amp;A](/help/communities/working-with-qna.md)、[calendar](/help/communities/calendar.md)、[filelibrary](/help/communities/file-library.md)、[comments](/help/communities/comments.md)があります。

![フォロービュー](assets/following-activities.png)

**フォロー**&#x200B;ボタンは、エントリをアクティビティ、[通知](/help/communities/notifications.md)、[購読](/help/communities/subscriptions.md)としてフォローする手段を提供します。 「**フォロー**」ボタンを選択するたびに、選択のオン/オフを切り替えることができます。 `Email Subscriptions`は、設定時にのみ表示されます。

フォロー方法が選択されると、ボタンのテキストが「**フォロー中**」に変わります。 便宜上、`Unfollow All`を選択してすべてのメソッドをオフに切り替えることができます。

「**フォロー**」ボタンが表示されます。

* 別のメンバーのプロファイルを表示するとき。
* フォーラム、Q&amp;A、ブログなどのメイン機能ページで使用します。

   * その一般的な機能のすべてのアクティビティに従います。

* フォーラムトピック、Q&amp;A質問、ブログ記事などの特定のエントリ用。

   * その特定のエントリのすべてのアクティビティに従います。

### 追加情報 {#additional-information}

開発者向けの詳細情報は、[アクティビティストリームの基本事項](/help/communities/essentials-activities.md)ページを参照してください。
