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
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 48%

---

# リーダーボード機能  {#leaderboard-feature}

## はじめに {#introduction}

`Leaderboard`コンポーネントは、獲得したポイント（基本スコア）や専門知識（高度なスコア）に基づいてメンバーをランク付けすることで、コミュニティ内でのメンバーの関わり方を把握できます。

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)を設定する必要があります。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* `Leaderboard`コンポーネントを[コミュニティサイト](/help/communities/overview.md#community-sites)に追加します。
* `Leaderboard`コンポーネントの設定。

### リーダーボードをページに追加 {#adding-a-leaderboard-to-a-page}

`Leaderboard`コンポーネントをオーサリングモードでページに追加するには、

* `Communities / Leaderboard`

コンポーネントを探し、ページ上の位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](/help/communities/basics.md)を参照してください。

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![リーダーボード](assets/leaderboard.png)

### リーダーボードの設定 {#configuring-leaderboard}

配置済みの`Leaderboard`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

![設定リーダーボード](assets/configure-leaderboard.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブで、メンバーに関連して表示する情報を指定します。

* **表示名**

   ボードに表示するわかりやすい名前。バッジとスコアの表示用に選択したルールを反映します。
何も入力しない場合の初期設定は`Leaderboard`です。

* **バッジ**

   オンにすると、リーダーボードにバッジアイコンの列が表示されます。
初期設定はオフです。

* **バッジ名**

   オンにすると、リーダーボードにバッジ名の列が表示されます。
初期設定はオフです。

* **ユーザーアバター**

   オンにすると、リーダーボードのメンバープロファイルへの名前リンクの横に、メンバーのアバター画像が表示されます。
初期設定はオフです。

#### 「ルール」タブ{#rules-tab}

「**ルール**」タブで、コミュニティサイト、およびそのスコアルールとバッジルールを指定します。

* **ルールの場所**

   （必須）スコア/バッジルールを設定する場所。

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

![専門家のリーダーボード](assets/experts-leaderboard.png)

### 追加情報 {#additional-information}

詳しくは、開発者向けの[リーダーボードの基本事項](/help/communities/leaderboard.md)ページを参照してください。

ルールの作成手順は、管理者向けの[コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)ページで説明しています。
