---
title: 評価の使用
description: ログインしたコミュニティメンバーがコンテンツを評価して意見を表明できるページに評価コンポーネントを追加する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 3%

---

# 評価の使用 {#using-ratings}

`Rating` コンポーネントは、スタンドアロンで使用するか、他の Communities 機能と共に使用します。 このコンポーネントを使用すると、ログインしたコミュニティメンバーが、コンテンツを評価して意見を表明できます。

## ページへの評価の追加 {#adding-a-rating-to-a-page}

オーサーモードで `Rating` コンポーネントをページに追加するには、コンポーネントを `Communities / Rating` に配置して、メンバーが評価するフィーチャーに対する相対的な位置など、ページ上の場所にドラッグします。

必要な情報については、[Communities コンポーネントの基本 ](basics.md) を参照してください。

[ 必須のクライアントサイドライブラリ ](rating-basics.md#essentials-for-client-side) が含まれると、`Rating` コンポーネントはこのように表示されます。

![ レーティング ](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置された `Rating` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![configure-new](assets/configure-new.png)

**[!UICONTROL テキストとラベル]** タブで、評価の内部識別子を指定します。

![tallyname](assets/tallyname.png)

**[!UICONTROL 集計名]**
（*必須*）このインスタンスを一意に識別する `Rating` のシンプルな名前。 リポジトリの有効なノード名である必要があります。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも格付けを変更することができる。

### 匿名 {#anonymous}

評価の匿名の投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）とログインが必要です。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [ 評価の基本事項 ](rating-basics.md) ページを参照してください。
