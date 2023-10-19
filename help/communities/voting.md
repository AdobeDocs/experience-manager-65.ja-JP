---
title: 投票の使用
description: サインインしたコミュニティメンバーが回答などの特定のコンテンツを評価するためのページに投票コンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# 投票の使用 {#using-voting}

The `Voting` コンポーネントは、コミュニティメンバーが Q&amp;A コンポーネント内の回答など、特定のコンテンツを評価するのに便利なツールです。 を使用 `Voting` コンポーネント、メンバーは上向き矢印または下向き矢印を選択して、意見を示します。

## 投票をページに追加する {#adding-voting-to-a-page}

を追加するには、以下を実行します。 `Voting` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用します。 場所 `Communities / Voting` をドラッグして、ページ上の適切な位置（ユーザーが投票できる機能に対する相対位置など）に配置します。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-voting.md#essentials-for-client-side) が含まれる場合、この方法で `Voting` コンポーネントが表示されます。

![投票構成要素](assets/voting-component.png)

## 投票の設定 {#configuring-voting}

配置した `Voting` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

の下 **[!UICONTROL テキストとラベル]** 「 」タブで、投票の記録に使用するプロパティを指定します。

![投票ラベル](assets/voting-label.png)

* **[!UICONTROL 肯定的な返信ラベル]**

  (*必須*) 肯定的な応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

  (*必須*) 否定的な応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

  (*必須*) 投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは 1 回のみ投票できますが、いつでも投票を変更できます。

### 匿名 {#anonymous}

匿名投票はサポートされていません。 サイト訪問者が投票に 1 回参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [投票の基本事項](essentials-voting.md) 開発者向けのページ
