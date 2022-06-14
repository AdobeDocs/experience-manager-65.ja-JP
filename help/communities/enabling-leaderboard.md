---
title: リーダーボード機能
seo-title: Leaderboard Feature
description: ページへのリーダーボードコンポーネントの追加
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 47%

---

# リーダーボード機能 {#leaderboard-feature}

## はじめに {#introduction}

この `Leaderboard` コンポーネントを使用すると、獲得したポイント（基本スコア）や専門知識（高度なスコア）に従ってメンバーをランク付けすることで、コミュニティ内でのメンバーの関わり方を把握できます。

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)を設定する必要があります。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* の追加 `Leaderboard` コンポーネントを [コミュニティサイト](/help/communities/overview.md#community-sites).
* の設定 `Leaderboard` コンポーネント。

### リーダーボードをページに追加 {#adding-a-leaderboard-to-a-page}

を追加するには、以下を実行します。 `Leaderboard` コンポーネントをオーサリングモードでページに追加する場合は、

* `Communities / Leaderboard`

コンポーネントを探し、ページ上の位置にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](/help/communities/basics.md).

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![リーダーボード](assets/leaderboard.png)

### リーダーボードの設定 {#configuring-leaderboard}

配置された `Leaderboard` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 「設定」タブ {#settings-tab}

「**[!UICONTROL 設定]**」タブで、メンバーに関連して表示する情報を指定します。

* **表示名**

   ボードに表示するわかりやすい名前。バッジとスコアの表示に選択したルールが反映されます。
デフォルトはです。 `Leaderboard`（何も入力されていない場合）

* **バッジ**

   オンにすると、リーダーボードにバッジアイコンの列が表示されます。
初期設定はオフです。

* **バッジ名**

   オンにすると、リーダーボードにバッジ名の列が表示されます。
初期設定はオフです。

* **ユーザーアバター**

   オンにすると、メンバーのアバター画像がリーダーボードに含まれ、メンバーのプロファイルへの名前リンクの横に表示されます。
初期設定はオフです。

#### 「ルール」タブ {#rules-tab}

「**ルール**」タブで、コミュニティサイト、およびそのスコアルールとバッジルールを指定します。

* **ルールの場所**

   （必須）スコア/バッジルールを設定する場所。

* **スコアルール**

   （必須）表示するスコアを生成する特定のルール。

* **バッジルール**

   （必須）表示するバッジを生成する特定のルール。

* **最大表示数**

   1 ページに表示するメンバーの数。デフォルトは 10 です。

### 例：参加者のリーダーボード {#example-participants-leaderboard}

このリーダーボードには、基本スコアルールを適用した結果が報告されます。

リーダーボードコンポーネントの設定：

* 「設定」タブ：

   * 表示名 = `Participation Board`
   *  `checked`：

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
   *  `checked`：

      * バッジ
      * ユーザーアバター

* 「ルール」タブ：

   * ルールの場所 = `/content/sites/<site name>/jcr:content`
   * スコアルール = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * バッジルール = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 最大表示数 = `10`

![専門家のリーダーボード](assets/experts-leaderboard.png)

### 追加情報 {#additional-information}

詳しくは、 [リーダーボードの基本事項](/help/communities/leaderboard.md) 開発者向けのページ

ルールを作成する手順は、 [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md) 管理者向けのページ
