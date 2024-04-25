---
title: おすすめコンテンツ機能
description: おすすめコンテンツ機能を使用すると、ログインしたサイト訪問者がコンテンツをハイライト表示できます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 5%

---

# おすすめコンテンツ機能 {#featured-content-feature}

## はじめに {#introduction}

おすすめコンテンツ機能には、パブリッシュ環境でログインしたサイト訪問者（コミュニティメンバー）がコンテンツをハイライト表示する領域が用意されています。

* [ブログ](blog-feature.md)
* [カレンダー](calendar.md)
* [フォーラム](forum.md)
* [アイデア](ideation-feature.md)
* [Q&amp;A](working-with-qna.md)

おすすめコンテンツとしてフラグ付けされると、そのコンテンツはこのコンポーネント内にリストされます。特定のランディングページや、コミュニティメンバーが注目しやすい領域に配置できます。

コンテンツを機能させる機能は、コンポーネントごとに許可または禁止される場合があります。

ドキュメントのこの節では、以下について説明します。

* コミュニティサイトへのおすすめコンテンツの追加。
* の設定 `Featured Content` コンポーネント。

## ページへのおすすめコンテンツの追加 {#adding-featured-content-to-a-page}

を追加します `Featured Content` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます

* `Communities / Featured Content`

おすすめコンテンツが表示されるページの場所にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](essentials-featured.md#essentials-for-client-side) が含まれる場合、このようにして `Featured Content` コンポーネントが表示されます。

![featuredcontent](assets/featuredcontent.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

配置されたを選択します。 `Featured Content` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 「設定」タブ {#settings-tab}

の下 **[!UICONTROL 設定]** タブで、機能するコンテンツを特定します。

* **[!UICONTROL 表示名]**

  おすすめコンテンツのリストのタイトル。 例えば、`Featured Questions` や `Featured Ideas` です。 デフォルトは `Featured Content` 空のままにした場合。

* **[!UICONTROL おすすめコンテンツの場所]**

  *（必須）* おすすめコンテンツを含むページを参照します（そのページのコンポーネントは、おすすめコンテンツを許可するように設定されている必要があります）。 例えば、`/content/sites/engage/en/forum` のように指定します。

* **[!UICONTROL 表示の制限]**

  表示するおすすめコンテンツの最大数。 デフォルトは 5 です。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

おすすめコンテンツとしてコンテンツにフラグを付けるには、モデレーター権限が必要です。

モデレーターが投稿されたコンテンツを表示すると、新しいを含むコンテキスト内モデレートフラグにアクセスできます `Feature` フラグ。

![サイト訪問者エクスペリエンス](assets/site-visitor-experience.png)

機能としてフラグが設定されると、モデレートフラグはになります `Unfeature`.

を含むページ `Featured Content` コンポーネントに、この投稿が含まれるようになりました。

![site-visitor-experience1](assets/site-visitor-experience1.png)

この `Read More` 実際の投稿へのリンク。

## 追加情報 {#additional-information}

詳しくは、 [おすすめコンテンツ](essentials-featured.md) 開発者向けのページです。

おすすめコンテンツのフラグ設定については、を参照してください。 [ユーザー作成コンテンツのモデレート](moderate-ugc.md).
