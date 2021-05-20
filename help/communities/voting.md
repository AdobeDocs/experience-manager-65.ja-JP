---
title: 投票の使用
seo-title: 投票の使用
description: 投票コンポーネントをページに追加
seo-description: 投票コンポーネントをページに追加
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 24%

---

# 投票の使用 {#using-voting}

`Voting`コンポーネントは、コミュニティメンバーがQ&amp;Aコンポーネント内の回答など、特定のコンテンツを評価するのに役立つツールです。 `Voting`コンポーネントを使用して、メンバーは上向き矢印または下向き矢印を選択して意見を示します。

## 投票をページに追加 {#adding-voting-to-a-page}

`Voting`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して`Communities / Voting`を探し、ページ上の位置（ユーザーが投票する機能に対する相対位置など）にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-voting.md#essentials-for-client-side)を含めると、`Voting`コンポーネントは次のように表示されます。

![投票要素](assets/voting-component.png)

## 投票の設定 {#configuring-voting}

配置済みの`Voting`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、投票の記録に使用するプロパティを指定します。

![投票ラベル](assets/voting-label.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   （*必須*）正の応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   （*必須*）負の応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

   （*必須*）投票コンポーネントのこのインスタンスの、識別可能な内部プロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーが投票できるのは 1 回だけですが、いつでも投票を変更できます。

### 匿名 {#anonymous}

匿名での投票はサポートされていません。サイト訪問者が1回投票に参加するには、登録（メンバーになる）し、サインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[投票の基本事項](essentials-voting.md)ページを参照してください。
