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
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# おすすめコンテンツ機能 {#featured-content-feature}

## 概要 {#introduction}

おすすめコンテンツ機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下のコンテンツに注目する領域を提供します。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [フォーラム](forum.md)
* [アイデア](ideation-feature.md)
* [Q&amp;A](working-with-qna.md)

コンテンツにおすすめとしてフラグを設定すると、このコンポーネント内に一覧表示されるようになります。特定のランディングページまたは領域にこのコンポーネントを配置し、コミュニティメンバーの注目を簡単に集めることができます。

コンテンツをおすすめに設定する機能は、コンポーネントごとに許可または禁止できます。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* コミュニティサイトへの特集コンテンツの追加
* Configuration settings for the `Featured Content` component

## おすすめコンテンツをページに追加 {#adding-featured-content-to-a-page}

To add a `Featured Content` component to a page in author mode, use the component browser to locate

* `Communities / Featured Content`

コンポーネントを探し、ページ上のおすすめコンテンツを表示する位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-featured.md#essentials-for-client-side) are included, this is how the `Featured Content` component will appear:

![chlimage_1-13](assets/chlimage_1-13.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

Select the placed `Featured Content` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-14](assets/chlimage_1-14.png)![chlimage_1-15](assets/chlimage_1-15.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブの下で、おすすめに設定するコンテンツを指定します。

* **[!UICONTROL 表示名]**&#x200B;おすすめコンテンツのリストのタイトル。For example `Featured Questions` or `Featured Ideas`. 初期設定は、空 `Featured Content` のままの場合です。

* **[!UICONTROL おすすめコンテンツの場所]**
   *（必須）* 、特集可能なコンテンツを含むページを参照します（そのページのコンポーネントは、「重点コンテンツを許可」に設定する必要があります）。 例：`/content/sites/engage/en/forum`

* **[!UICONTROL 最大表示数]**&#x200B;表示するおすすめコンテンツの最大数。初期設定は 5 です。

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
