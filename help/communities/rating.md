---
title: 評価の使用
description: ログインしているコミュニティメンバーがコンテンツを評価して意見を表明できるページに評価コンポーネントを追加する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 3%
---
# 評価の使用 {#using-ratings}

`Rating` コンポーネントは、スタンドアロンまたは他のコミュニティ機能と共に使用されます。 このコンポーネントを使用すると、サインインしているコミュニティメンバーは、コンテンツを評価して意見を表明できます。

## ページへの評価の追加 {#adding-a-rating-to-a-page}

作成者モードのページに`Rating` コンポーネントを追加するには、コンポーネント `Communities / Rating`を見つけて、メンバーが評価する機能に対する相対的な位置など、ページ上の場所にドラッグします。

必要な情報については、[ コミュニティコンポーネントの基本](basics.md)を参照してください。

[必要なクライアントサイドライブラリ ](rating-basics.md#essentials-for-client-side)が含まれている場合、`Rating` コンポーネントはこのように表示されます。

![評価](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置された`Rating` コンポーネントを選択して、編集ダイアログを開く`Configure` アイコンにアクセスして選択できるようにします。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、評価の内部識別子を指定します。

![tallyname](assets/tallyname.png)

**[!UICONTROL 合計名]**
（*必須*）このインスタンスを一意に識別する`Rating`の簡単な名前。 リポジトリの有効なノード名である必要があります。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーごとに1つの評価のみが許可されます。 会員は、いつでも評価を変更することができます。

### 匿名 {#anonymous}

評価の匿名での投稿はサポートされていません。 サイト訪問者は登録（会員になる）し、ログインして参加する必要があります。

## 追加情報 {#additional-information}

詳細については、開発者向けの[Rating Essentials](rating-basics.md) ページを参照してください。
