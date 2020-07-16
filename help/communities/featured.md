---
title: おすすめコンテンツ機能
seo-title: おすすめコンテンツ機能
description: おすすめコンテンツ機能を使用すると、サインインしているサイト訪問者がコンテンツに注目します
seo-description: おすすめコンテンツ機能を使用すると、サインインしているサイト訪問者がコンテンツに注目します
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: cbb5a6bac5e9932fd36abf20d4424890080d39bf
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 49%

---


# おすすめコンテンツ機能 {#featured-content-feature}

## 概要 {#introduction}

特集コンテンツ機能は、公開環境のログイン済みサイト訪問者（コミュニティのメンバー）がコンテンツを強調表示する領域を提供します。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [フォーラム](forum.md)
* [アイデア](ideation-feature.md)
* [Q&amp;A](working-with-qna.md)

コンテンツにおすすめとしてフラグを設定すると、このコンポーネント内に一覧表示されるようになります。特定のランディングページまたは領域にこのコンポーネントを配置し、コミュニティメンバーの注目を簡単に集めることができます。

コンテンツをおすすめに設定する機能は、コンポーネントごとに許可または禁止できます。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* コミュニティサイトへの重点コンテンツの追加
* Configuration settings for the `Featured Content` component.

## おすすめコンテンツをページに追加 {#adding-featured-content-to-a-page}

To add a `Featured Content` component to a page in author mode, use the component browser to locate

* `Communities / Featured Content`

コンポーネントを探し、ページ上のおすすめコンテンツを表示する位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

[必要なクライアント側ライブラリが含まれる場合](essentials-featured.md#essentials-for-client-side) 、次のようにコンポー `Featured Content` ネントが表示されます。

![chlimage_1-13](assets/chlimage_1-13.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

Select the placed `Featured Content` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-14](assets/chlimage_1-14.png)

![chlimage_1-15](assets/chlimage_1-15.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブの下で、おすすめに設定するコンテンツを指定します。

* **[!UICONTROL 表示名]**

   重点コンテンツのリストのタイトル。 For example `Featured Questions` or `Featured Ideas`. 初期設定は、空のままの `Featured Content` 場合です。

* **[!UICONTROL おすすめコンテンツの場所]**

   *（必須）* 特集対象のコンテンツを含むページを表示します（そのページのコンポーネントは、「重点コンテンツを許可」に設定する必要があります）。 例： `/content/sites/engage/en/forum`

* **[!UICONTROL 最大表示数]**

   表示する重点コンテンツの最大数。 初期設定は 5 です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

コンテンツにおすすめコンテンツのフラグを設定する機能には、モデレーター権限が必要です。

When a moderator views posted content, they have access to the in-context moderation flags, which includes the new `Feature` flag.

![chlimage_1-16](assets/chlimage_1-16.png)

Once flagged as feature, the modeartion flag becomes `Unfeature`.

The page containing the `Featured Content` component, will now include this post.

![chlimage_1-17](assets/chlimage_1-17.png)

`Read More` は、実際の投稿へのリンクです。

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[おすすめコンテンツ](essentials-featured.md)ページを参照してください。

コンテンツへのおすすめフラグの設定について詳しくは、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。
