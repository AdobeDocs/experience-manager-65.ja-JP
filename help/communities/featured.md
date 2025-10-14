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
* `Featured Content` コンポーネントの設定。

## ページへのおすすめコンテンツの追加 {#adding-featured-content-to-a-page}

オーサーモードで `Featured Content` コンポーネントをページに追加するには、コンポーネントブラウザーを使用して以下を見つけます

* `Communities / Featured Content`

おすすめコンテンツが表示されるページの場所にドラッグします。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

[&#x200B; 必須のクライアントサイドライブラリ &#x200B;](essentials-featured.md#essentials-for-client-side) が含まれると、`Featured Content` のコンポーネントは次のように表示されます。

![featuredcontent](assets/featuredcontent.png)

## おすすめコンテンツの設定 {#configuring-featured-content}

配置された `Featured Content` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### 「設定」タブ {#settings-tab}

「**[!UICONTROL 設定]**」タブで、機能させるコンテンツを指定します。

* **[!UICONTROL 表示名]**

  おすすめコンテンツのリストのタイトル。 例えば、`Featured Questions` や `Featured Ideas` です。 空のままにした場合、デフォルトは `Featured Content` です。

* **[!UICONTROL おすすめコンテンツの場所]**

  *（必須）* おすすめコンテンツを含むページを参照します（そのページのコンポーネントは、おすすめコンテンツを許可するように設定されている必要があります）。 例えば、`/content/sites/engage/en/forum` のように指定します。

* **[!UICONTROL 表示制限]**

  表示するおすすめコンテンツの最大数。 デフォルトは 5 です。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

おすすめコンテンツとしてコンテンツにフラグを付けるには、モデレーター権限が必要です。

モデレーターが投稿されたコンテンツを表示すると、新しい `Feature` フラグを含むコンテキスト内モデレートフラグにアクセスできます。

![site-visitor-experience](assets/site-visitor-experience.png)

機能としてフラグが設定されると、モデレーションフラグは `Unfeature` になります。

`Featured Content` コンポーネントを含むページに、この投稿が含まれるようになりました。

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` は、実際の投稿にリンクしています。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; おすすめコンテンツ &#x200B;](essentials-featured.md) ページをご覧ください。

特集としてコンテンツにフラグを設定するには、[&#x200B; ユーザー生成コンテンツのモデレート &#x200B;](moderate-ugc.md) を参照してください。
