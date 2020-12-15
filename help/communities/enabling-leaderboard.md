---
title: リーダーボード機能
seo-title: リーダーボード機能
description: ページへのリーダーボードコンポーネントの追加
seo-description: ページへのリーダーボードコンポーネントの追加
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 48%

---


# リーダーボード機能  {#leaderboard-feature}

## 概要 {#introduction}

`Leaderboard`コンポーネントは、獲得点（基本スコア）またはその専門知識（高度スコア）に従ってメンバーをランク付けすることで、コミュニティ内でのメンバーの関わり方を把握できます。

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)を設定する必要があります。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* `Leaderboard`コンポーネントを[コミュニティサイト](/help/communities/overview.md#community-sites)に追加します。
* `Leaderboard`コンポーネントの構成設定です。

### リーダーボードをページに追加 {#adding-a-leaderboard-to-a-page}

作成者モードで`Leaderboard`コンポーネントをページに追加するには、コンポーネントを見つけます

* `Communities / Leaderboard`

コンポーネントを探し、ページ上の位置にドラッグします。

必要な情報については、[Communities Components Basics](/help/communities/basics.md)を参照してください。

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![先頭板](assets/leaderboard.png)

### リーダーボードの設定 {#configuring-leaderboard}

アクセスする配置済みの`Leaderboard`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブで、メンバーに関連して表示する情報を指定します。

* **表示名**

   ボードに表示するわかりやすい名前。バッジとスコアの表示に選択したルールを反映します。
何も入力しなかった場合の初期設定は`Leaderboard`です。

* **バッジ**

   選択すると、バッジアイコンの列がリーダーボードに含まれます。
初期設定はオフです。

* **バッジ名**

   オンの場合、バッジ名の列がリーダーボードに含まれます。
初期設定はオフです。

* **ユーザーアバター**

   オンの場合、メンバーのアバター画像はリーダーボードに含まれ、メンバープロファイルへの名前リンクの隣に表示されます。
初期設定はオフです。

#### 「ルール」タブ{#rules-tab}

「**ルール**」タブで、コミュニティサイト、およびそのスコアルールとバッジルールを指定します。

* **ルールの場所**

   （必須）スコアリング/バッジングルールが設定されている場所。

* **スコアルール**

   （必須）表示するスコアを生成する特定のルール。

* **バッジルール**

   （必須）表示するバッジを生成する特定のルール。

* **最大表示数**

   1ページに表示するメンバーの数。デフォルトは10です。

### 例：参加者のリーダーボード {#example-participants-leaderboard}

このリーダーボードには、基本スコアルールを適用した結果が報告されます。

リーダーボードコンポーネントの設定：

* 「設定」タブ：

   * 表示名 = `Participation Board`
   *  `checked` の下）で、次の手順をおこないます。

      * バッジ
      * バッジ名
      * ユーザーアバター

* 「ルール」タブ：

   * ルールの場所 = `/content/sites/<site name>/jcr:content`
   * スコアルール = `/libs/settings/community/scoring/rules/forums-scoring`
   * バッジルール = `/libs/settings/community/badging/rules//reference-badging`
   * 最大表示数 = `10`

![参加者のリーダーボード](assets/participants-leaderboard.png)

### 例：エキスパートのリーダーボード {#example-experts-leaderboard}

このリーダーボードには、高度なスコアルールを適用した結果が報告されます。

リーダーボードコンポーネントの設定：

* 「設定」タブ：

   * 表示名 = `Expertise Board`
   *  `checked` の下）で、次の手順をおこないます。

      * バッジ
      * ユーザーアバター

* 「ルール」タブ：

   * ルールの場所 = `/content/sites/<site name>/jcr:content`
   * スコアルール = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * バッジルール = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 最大表示数 = `10`

![専門家委員会](assets/experts-leaderboard.png)

### 追加情報 {#additional-information}

詳しい情報は[Leaderboard Essentials](/help/communities/leaderboard.md)ページの開発者向けページにあります。

ルールの作成手順は、管理者向けの[コミュニティスコアリングとバッジ](/help/communities/implementing-scoring.md)ページに記載されています。
