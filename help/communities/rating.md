---
title: 評価の使用
seo-title: Using Ratings
description: 評価コンポーネントをページに追加
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 35%

---

# 評価の使用 {#using-ratings}

この `Rating` コンポーネントは、スタンドアロンで、または他のコミュニティ機能と組み合わせて使用されます。 このコンポーネントを使用すると、サインインしたコミュニティメンバーは、コンテンツを評価して意見を表明できます。

## 評価をページに追加 {#adding-a-rating-to-a-page}

を追加するには、以下を実行します。 `Rating` コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Rating` をクリックし、ページ上の適切な位置（メンバーが評価する機能を基準とした位置など）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](rating-basics.md#essentials-for-client-side) が含まれる場合、この方法で `Rating` コンポーネントが表示されます。

![評価](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置された `Rating` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブでは、評価の内部識別子を指定できます。

![tallyname](assets/tallyname.png)

**[!UICONTROL 集計名]**
(*必須*) `Rating` このインスタンスを一意に識別する リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

1 人のメンバーが付けられる評価は 1 つだけです。メンバーは、いつでも評価を変更できます。

### 匿名 {#anonymous}

匿名での評価投稿はサポートされていません。サイト訪問者が参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [評価の基本事項](rating-basics.md) 開発者向けのページ
