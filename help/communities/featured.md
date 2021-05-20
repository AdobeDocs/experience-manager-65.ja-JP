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
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 54%

---

# おすすめコンテンツ機能  {#featured-content-feature}

## 概要 {#introduction}

おすすめコンテンツ機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下のコンテンツに注目する領域を提供します。：

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [フォーラム](forum.md)
* [アイデア](ideation-feature.md)
* [Q&amp;A](working-with-qna.md)

コンテンツにおすすめとしてフラグを設定すると、このコンポーネント内に一覧表示されるようになります。特定のランディングページまたは領域にこのコンポーネントを配置し、コミュニティメンバーの注目を簡単に集めることができます。

コンテンツをおすすめに設定する機能は、コンポーネントごとに許可または禁止できます。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* コミュニティサイトにおすすめコンテンツを追加する。
* `Featured Content`コンポーネントの設定。

## おすすめコンテンツをページに追加 {#adding-featured-content-to-a-page}

`Featured Content`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Featured Content`

コンポーネントを探し、ページ上のおすすめコンテンツを表示する位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-featured.md#essentials-for-client-side)を含めると、`Featured Content`コンポーネントは次のように表示されます。

![featuredcontent](assets/featuredcontent.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

配置済みの`Featured Content`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブの下で、おすすめに設定するコンテンツを指定します。

* **[!UICONTROL 表示名]**

   おすすめコンテンツのリストのタイトル。 例えば、`Featured Questions`や`Featured Ideas`などです。 空のままの場合、初期設定は`Featured Content`です。

* **[!UICONTROL おすすめコンテンツの場所]**

   *（必須）* 機能する可能性のあるコンテンツが含まれているページを参照します（そのページのコンポーネントは、「おすすめコンテンツを許可」に設定する必要があります）。（例：`/content/sites/engage/en/forum`）。

* **[!UICONTROL 最大表示数]**

   表示するおすすめコンテンツの最大数。 初期設定は 5 です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

コンテンツにおすすめコンテンツのフラグを設定する機能には、モデレーター権限が必要です。

モデレーターが投稿されたコンテンツを表示すると、コンテキスト内モデレートフラグにアクセスできます。これには新しい`Feature`フラグが含まれます。

![site-visitor-experience](assets/site-visitor-experience.png)

機能としてフラグが設定されると、モデレートフラグは`Unfeature`になります。

`Featured Content`コンポーネントを含むページに、この投稿が含まれます。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` は、実際の投稿へのリンクです。

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[おすすめコンテンツ](essentials-featured.md)ページを参照してください。

コンテンツへのおすすめフラグの設定について詳しくは、[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。
