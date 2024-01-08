---
title: リーダーボード機能
description: リーダーボードコンポーネントを使用して、獲得したポイントと専門知識に基づいてメンバーをランク付けすることで、コミュニティ内でのメンバーのやり取りを確認できる方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 3%

---

# リーダーボード機能 {#leaderboard-feature}

## はじめに {#introduction}

The `Leaderboard` コンポーネントを使用すると、獲得したポイント（基本スコア）や専門知識（高度なスコア）に従ってメンバーをランク付けすることで、コミュニティ内でのメンバーの関わり方を把握できます。

ページにリーダーボードコンポーネントを含める前に、 [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md).

ドキュメントのこの節では、以下について説明します。

* の追加 `Leaderboard` コンポーネントを [コミュニティサイト](/help/communities/overview.md#community-sites).
* の設定 `Leaderboard` コンポーネント。

### ページへのリーダーボードの追加 {#adding-a-leaderboard-to-a-page}

を追加するには、以下を実行します。 `Leaderboard` コンポーネントをオーサリングモードでページに追加する場合は、

* `Communities / Leaderboard`

ページ上の場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](/help/communities/basics.md).

コミュニティサイトのページに最初に配置したとき、コンポーネントは次のように表示されます。

![リーダーボード](assets/leaderboard.png)

### リーダーボードの設定 {#configuring-leaderboard}

配置した `Leaderboard` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 「設定」タブ {#settings-tab}

の下 **[!UICONTROL 設定]** 「 」タブで、メンバーに関する表示情報を指定します。

* **表示名**

  ボードに表示するわかりやすい名前。バッジとスコアの表示に選択したルールが反映されます。
デフォルトはです。 `Leaderboard` を指定します。

* **バッジ**

  オンにすると、リーダーボードにバッジアイコンの列が表示されます。
初期設定はオフです。

* **バッジ名**

  オンにすると、リーダーボードにバッジ名の列が表示されます。
初期設定はオフです。

* **アバターを使用**

  オンにすると、メンバーのアバター画像がリーダーボードに含まれ、メンバーのプロファイルへの名前リンクの横に表示されます。
初期設定はオフです。

#### 「ルール」タブ {#rules-tab}

の下 **ルール** タブ、コミュニティサイト、およびそのスコアとバッジのルール

* **ルールの場所**

  （必須）スコア/バッジルールを設定する場所。

* **スコアルール**

  （必須）表示するスコアを生成する特定のルール。

* **バッジルール**

  （必須）表示するバッジを生成する特定のルール。

* **表示の制限**

  1 ページに表示するメンバーの数。 初期設定は 10 です。

### 例：参加者のリーダーボード {#example-participants-leaderboard}

このリーダーボードは、基本的なスコア付けルールの適用結果を報告します。

リーダーボードコンポーネントの設定：

* 「設定」タブ

   * 表示名= `Participation Board`
   *  `checked`：

      * バッジ
      * バッジ名
      * アバターを使用

* 「ルール」タブ

   * ルールの場所= `/content/sites/<site name>/jcr:content`
   * スコアルール= `/libs/settings/community/scoring/rules/forums-scoring`
   * バッジルール= `/libs/settings/community/badging/rules//reference-badging`
   * 表示の制限= `10`

![参加者のリーダーボード](assets/participants-leaderboard.png)

### 例：エキスパートリーダーボード {#example-experts-leaderboard}

このリーダーボードは、高度なスコアルールの適用結果を報告します。

リーダーボードコンポーネントの設定：

* 「設定」タブ

   * 表示名= `Expertise Board`
   *  `checked`：

      * バッジ
      * アバターを使用

* 「ルール」タブ

   * ルールの場所= `/content/sites/<site name>/jcr:content`
   * スコアルール= `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * バッジルール= `/libs/settings/community/badging/rules/adv-forums-badging`
   * 表示の制限= `10`

![専門家のリーダーボード](assets/experts-leaderboard.png)

### 追加情報 {#additional-information}

詳しくは、 [リーダーボードの基本事項](/help/communities/leaderboard.md) 開発者向けのページ

ルールを作成する手順は、 [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md) 管理者向けのページ。
