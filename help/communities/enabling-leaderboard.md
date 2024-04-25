---
title: リーダーボード機能
description: リーダーボードコンポーネントを使用して、獲得したポイントと専門知識に基づいてメンバーをランキングすることで、コミュニティ内のメンバーのインタラクションを確認する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 3%

---

# リーダーボード機能 {#leaderboard-feature}

## はじめに {#introduction}

この `Leaderboard` コンポーネントは、獲得したポイント（基本スコアリング）または専門知識（高度なスコアリング）に従ってメンバーをランキングすることで、メンバーがコミュニティ内でどのように相互作用しているかを把握するのに役立ちます。

ページにリーダーボードコンポーネントを含める前に、を設定する必要があります [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md).

ドキュメントのこの節では、以下について説明します。

* の追加 `Leaderboard` コンポーネントからへ [コミュニティサイト](/help/communities/overview.md#community-sites).
* の設定 `Leaderboard` コンポーネント。

### ページへのリーダーボードの追加 {#adding-a-leaderboard-to-a-page}

を追加します `Leaderboard` オーサーモードのページへのコンポーネントの移動

* `Communities / Leaderboard`

そして、ページ上の場所にドラッグします。

詳細については、 [Communities コンポーネントの基本](/help/communities/basics.md).

コミュニティサイトのページに初めて配置すると、コンポーネントは次のように表示されます。

![leaderboard](assets/leaderboard.png)

### リーダーボードの設定 {#configuring-leaderboard}

配置されたを選択します。 `Leaderboard` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### 「設定」タブ {#settings-tab}

の下 **[!UICONTROL 設定]** タブで、メンバーに関連する表示される情報を指定します。

* **表示名**

  バッジおよびスコアの表示に選択したルールを反映した、ボードに表示するわかりやすい名前。
デフォルトは `Leaderboard` 何も入力されていない場合。

* **バッジ**

  オンにすると、リーダーボードにバッジアイコンの列が含まれます。
デフォルトではオフになっています。

* **バッジ名**

  オンにすると、バッジ名の列がリーダーボードに含まれます。
デフォルトではオフになっています。

* **アバターを使用**

  オンにすると、メンバーのアバター画像がリーダーボードのメンバープロファイルへの名前リンクの横に表示されます。
デフォルトではオフになっています。

#### 「ルール」タブ {#rules-tab}

の下 **ルール** タブ、コミュニティサイト、およびそのスコアとバッジルール

* **ルールの場所**

  （必須） スコア / バッジルールが設定される場所。

* **スコアルール**

  （必須）表示するスコアを生成する特定のルール。

* **バッジルール**

  （必須）表示するバッジを生成する特定のルール。

* **表示の制限**

  ページごとに表示するメンバーの数。 初期設定は 10 です。

### 例：参加者リーダーボード {#example-participants-leaderboard}

このリーダーボードは、基本的なスコアルールの適用の結果をレポートします。

リーダーボードコンポーネント設定：

* 「設定」タブ：

   * 表示名= `Participation Board`
   *  `checked`：

      * バッジ
      * バッジ名
      * アバターを使用

* 「ルール」タブ：

   * ルールの場所= `/content/sites/<site name>/jcr:content`
   * スコアルール = `/libs/settings/community/scoring/rules/forums-scoring`
   * バッジルール = `/libs/settings/community/badging/rules//reference-badging`
   * 表示制限= `10`

![参加者リーダーボード](assets/participants-leaderboard.png)

### 例：エキスパートリーダーボード {#example-experts-leaderboard}

このリーダーボードは、高度なスコアルールを適用した結果をレポートします。

リーダーボードコンポーネント設定：

* 「設定」タブ：

   * 表示名= `Expertise Board`
   *  `checked`：

      * バッジ
      * アバターを使用

* 「ルール」タブ：

   * ルールの場所= `/content/sites/<site name>/jcr:content`
   * スコアルール = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * バッジルール = `/libs/settings/community/badging/rules/adv-forums-badging`
   * 表示制限= `10`

![エキスパートリーダーボード](assets/experts-leaderboard.png)

### 追加情報 {#additional-information}

詳しくは、 [リーダーボードの基本事項](/help/communities/leaderboard.md) 開発者向けのページです。

ルールを作成する手順は、次のとおりです [コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md) 管理者向けのページです。
