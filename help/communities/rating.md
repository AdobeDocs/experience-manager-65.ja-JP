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

この `Rating` コンポーネントは、スタンドアロンで使用するか、他の Communities 機能と共に使用します。 このコンポーネントを使用すると、ログインしたコミュニティメンバーが、コンテンツを評価して意見を表明できます。

## ページへの評価の追加 {#adding-a-rating-to-a-page}

を追加します `Rating` オーサーモードのページへのコンポーネントの移動 `Communities / Rating` そして、メンバーが評価するフィーチャーに対する相対的な位置など、ページ上の場所にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](rating-basics.md#essentials-for-client-side) が含まれる場合、このようにして `Rating` コンポーネントが表示されます。

![格付け](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置されたを選択します。 `Rating` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

の下 **[!UICONTROL テキストとラベル]** タブで、評価の内部識別子を指定します。

![tallyname](assets/tallyname.png)

**[!UICONTROL 集計名]**
（*必須*）の簡単な名前 `Rating` このインスタンスを一意に識別します。 リポジトリの有効なノード名である必要があります。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも格付けを変更することができる。

### 匿名 {#anonymous}

評価の匿名の投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）とログインが必要です。

## 追加情報 {#additional-information}

詳しくは、 [評価の基本事項](rating-basics.md) 開発者向けのページです。
