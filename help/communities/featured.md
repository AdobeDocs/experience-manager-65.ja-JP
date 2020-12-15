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
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 48%

---


# おすすめコンテンツ機能  {#featured-content-feature}

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
* `Featured Content`コンポーネントの構成設定です。

## おすすめコンテンツをページに追加 {#adding-featured-content-to-a-page}

作成者モードで`Featured Content`コンポーネントをページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Featured Content`

コンポーネントを探し、ページ上のおすすめコンテンツを表示する位置にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](essentials-featured.md#essentials-for-client-side)が含まれる場合、`Featured Content`コンポーネントは次のように表示されます。

![featuredcontent](assets/featuredcontent.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

アクセスする配置済みの`Featured Content`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブの下で、おすすめに設定するコンテンツを指定します。

* **[!UICONTROL 表示名]**

   重点コンテンツのリストのタイトル。 （例：`Featured Questions`、`Featured Ideas`）。 空白のままの場合の初期設定は`Featured Content`です。

* **[!UICONTROL おすすめコンテンツの場所]**

   *（必須）* 特集コンテンツを含むページを参照します（そのページのコンポーネントは、「特集コンテンツを許可」に設定する必要があります）。例： `/content/sites/engage/en/forum`

* **[!UICONTROL 最大表示数]**

   表示する重点コンテンツの最大数。 初期設定は 5 です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

コンテンツにおすすめコンテンツのフラグを設定する機能には、モデレーター権限が必要です。

モデレーター表示がコンテンツを投稿すると、新しい`Feature`フラグを含むコンテキスト内モデレートフラグにアクセスできます。

![サイト訪問者体験](assets/site-visitor-experience.png)

機能としてフラグ付けされると、モデレーションフラグは`Unfeature`になります。

`Featured Content`コンポーネントを含むページに、この投稿が含まれるようになります。

![site-訪問者-experience1](assets/site-visitor-experience1.png)

`Read More` は、実際の投稿へのリンクです。

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[おすすめコンテンツ](essentials-featured.md)ページを参照してください。

コンテンツへのおすすめフラグの設定について詳しくは、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。
