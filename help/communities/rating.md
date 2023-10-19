---
title: 評価の使用
description: サインインしたコミュニティメンバーがコンテンツを評価して意見を表明できるページに評価コンポーネントを追加する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# 評価の使用 {#using-ratings}

The `Rating` コンポーネントは、スタンドアロンで、または他のコミュニティ機能と共に使用されます。 このコンポーネントを使用すると、サインインしたコミュニティメンバーは、コンテンツを評価して意見を表明できます。

## ページへの評価の追加 {#adding-a-rating-to-a-page}

を追加するには、以下を実行します。 `Rating` コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Rating` をクリックし、ページ上の適切な位置（メンバーが評価する機能を基準とした位置など）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](rating-basics.md#essentials-for-client-side) が含まれる場合、この方法で `Rating` コンポーネントが表示されます。

![評価](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置した `Rating` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

の下 **[!UICONTROL テキストとラベル]** 」タブで、評価の内部識別子を指定します。

![tallyname](assets/tallyname.png)

**[!UICONTROL 集計名]**
(*必須*) `Rating` このインスタンスを一意に識別する リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーごとに 1 つの評価のみが許可されます。 会員は、いつでも評価を変更することができます。

### 匿名 {#anonymous}

匿名での評価の投稿はサポートされていません。 サイト訪問者が参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [評価の基本事項](rating-basics.md) 開発者向けのページ
