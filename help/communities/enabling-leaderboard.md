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
source-git-commit: 6720d5a0fdf1facc0b10011ec306dffbb31f4ac5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 49%

---


# リーダーボード機能 {#leaderboard-feature}

## 概要 {#introduction}

The `Leaderboard` component provides the ability to obtain a sense of how members are interacting within the community by ranking members according to points earned (basic scoring) or their expertise (advanced scoring).

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](/help/communities/implementing-scoring.md)を設定する必要があります。

ドキュメントのこのセクションでは、以下の内容について説明します。：

* Adding the `Leaderboard` component to a [community site](/help/communities/overview.md#community-sites).
* Configuration settings for the `Leaderboard` component.

### リーダーボードをページに追加 {#adding-a-leaderboard-to-a-page}

To add a `Leaderboard` component to a page in author mode, locate the component

* `Communities / Leaderboard`

コンポーネントを探し、ページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-8](assets/chlimage_1-8.png)

### リーダーボードの設定 {#configuring-leaderboard}

Select the placed `Leaderboard` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-9](assets/chlimage_1-9.png)

![chlimage_1-10](assets/chlimage_1-10.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブで、メンバーに関連して表示する情報を指定します。

* **表示名**

   ボードに表示するわかりやすい名前。バッジとスコアの表示に選択したルールを反映します。
Default is `Leaderboard`, if nothing entered.

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

![chlimage_1-11](assets/chlimage_1-11.png)

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

![chlimage_1-12](assets/chlimage_1-12.png)

### 追加情報 {#additional-information}

More information may be found on the [Leaderboard Essentials](/help/communities/leaderboard.md) page for developers.

Instructions for creating rules are provided on the [Communities Scoring and Badges](/help/communities/implementing-scoring.md) page for administrators.
