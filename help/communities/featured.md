---
title: おすすめコンテンツ機能
description: おすすめコンテンツ機能を使用すると、サインインしたサイト訪問者がコンテンツを強調表示できます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 7%

---

# おすすめコンテンツ機能 {#featured-content-feature}

## はじめに {#introduction}

おすすめコンテンツ機能を使用すると、パブリッシュ環境でサインインしたサイト訪問者（コミュニティメンバー）が次のコンテンツをハイライト表示できる領域が提供されます。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [フォーラム](forum.md)
* [アイデア](ideation-feature.md)
* [Q&amp;A](working-with-qna.md)

コンテンツにおすすめとしてフラグが設定されると、このコンポーネント内に一覧表示されます。このコンポーネントは、コミュニティメンバーの注意を引きやすい特定のランディングページや領域に配置できます。

コンテンツを特集する機能は、コンポーネントごとに許可または禁止できます。

ドキュメントのこの節では、以下について説明します。

* コミュニティサイトにおすすめコンテンツを追加する。
* の設定 `Featured Content` コンポーネント。

## ページへのおすすめコンテンツの追加 {#adding-featured-content-to-a-page}

を追加するには、以下を実行します。 `Featured Content` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Featured Content`

ページ上の特集コンテンツが表示される場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-featured.md#essentials-for-client-side) が含まれる場合、この方法で `Featured Content` コンポーネントが表示されます。

![featuredcontent](assets/featuredcontent.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

配置した `Featured Content` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 「設定」タブ {#settings-tab}

の下 **[!UICONTROL 設定]** 「 」タブで、機能するコンテンツを指定します。

* **[!UICONTROL 表示名]**

  おすすめコンテンツのリストのタイトル。 例： `Featured Questions` または `Featured Ideas`. デフォルトはです。 `Featured Content` 空のままの場合は。

* **[!UICONTROL おすすめコンテンツの場所]**

  *（必須）* 取り上げるコンテンツを含むページを参照します（そのページのコンポーネントは、「おすすめコンテンツを許可」に設定する必要があります）。 例：`/content/sites/engage/en/forum`

* **[!UICONTROL 最大表示数]**

  表示するおすすめコンテンツの最大数。 デフォルトは 5 です。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

コンテンツにおすすめコンテンツのフラグを設定する機能には、モデレーター権限が必要です。

モデレーターが投稿されたコンテンツを表示すると、コンテキスト内のモデレートフラグにアクセスできます。このフラグには、新しい `Feature` フラグ。

![site-visitor-experience](assets/site-visitor-experience.png)

機能としてフラグ付けされた後、モデレートフラグは `Unfeature`.

次を含むページ： `Featured Content` コンポーネントにこの投稿が含まれるようになりました。

![site-visitor-experience1](assets/site-visitor-experience1.png)

The `Read More` 実際の投稿へのリンク。

## 追加情報 {#additional-information}

詳しくは、 [おすすめコンテンツ](essentials-featured.md) 開発者向けのページ

コンテンツをおすすめとしてフラグ設定する方法については、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).
