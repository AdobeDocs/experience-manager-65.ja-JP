---
title: 評価の使用
seo-title: 評価の使用
description: 評価コンポーネントをページに追加
seo-description: 評価コンポーネントをページに追加
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# 評価の使用 {#using-ratings}

The `Rating` component is used standalone or in conjunction with other Communities features. ここでは、ログインしたコミュニティのメンバーが、コンテンツを評価することで意見を表すことができます。

## 評価をページに追加 {#adding-a-rating-to-a-page}

作成者モード `Rating` でページにコンポーネントを追加するには、コンポーネントを見つけ、 `Communities / Rating` そのコンポーネントをページ上の位置（メンバーが評価するフィーチャに対する相対位置など）にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](rating-basics.md#essentials-for-client-side) are included, this is how the `Rating` component will appear.

![chlimage_1-493](assets/chlimage_1-493.png)

## 評価の設定 {#configuring-rating}

Select the placed `Rating` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-494](assets/chlimage_1-494.png)

「**[!UICONTROL テキストとラベル]**」タブでは、評価の内部識別子を指定できます。

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Tally Name]**(必&#x200B;*須*)このインスタ `Rating`ンスを一意に識別する単純な名前。 リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

1 人のメンバーが付けられる評価は 1 つだけです。メンバーは、いつでも評価を変更できます。

### 匿名 {#anonymous}

匿名での評価投稿はサポートされていません。サイト訪問者は登録（会員になる）し、サインインして参加する必要があります。

## 追加情報 {#additional-information}

More information may be found on the [Rating Essentials](rating-basics.md) page for developers.
