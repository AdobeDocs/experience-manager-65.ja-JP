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
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 38%

---

# 評価の使用 {#using-ratings}

`Rating`コンポーネントは、スタンドアロンで、または他のコミュニティ機能と組み合わせて使用されます。 このコンポーネントを使用すると、サインインしたコミュニティメンバーは、コンテンツを評価して意見を表明できます。

## 評価をページに追加 {#adding-a-rating-to-a-page}

`Rating`コンポーネントをオーサリングモードでページに追加するには、コンポーネント`Communities / Rating`を選択し、ページ上の位置（メンバーが評価する機能に対する相対位置など）にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](rating-basics.md#essentials-for-client-side)を含めると、`Rating`コンポーネントは次のように表示されます。

![評価](assets/rating.png)

## 評価の設定 {#configuring-rating}

配置済みの`Rating`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブでは、評価の内部識別子を指定できます。

![tallname](assets/tallyname.png)

**[!UICONTROL 集計名]**
(*必須*)このインスタンスを一意に識別 `Rating` する、のシンプルな名前。リポジトリの有効なノード名を指定する必要があります。

## サイト訪問者のエクスペリエンス  {#site-visitor-experience}

### メンバー {#members}

1 人のメンバーが付けられる評価は 1 つだけです。メンバーは、いつでも評価を変更できます。

### 匿名 {#anonymous}

匿名での評価投稿はサポートされていません。サイト訪問者が参加するには、登録（メンバーになる）し、サインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[評価の基本事項](rating-basics.md)ページを参照してください。
