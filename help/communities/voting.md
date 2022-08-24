---
title: 投票の使用
seo-title: Using Voting
description: 投票コンポーネントをページに追加
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 21%

---

# 投票の使用 {#using-voting}

この `Voting` コンポーネントは、コミュニティメンバーが Q&amp;A コンポーネント内の回答など、特定のコンテンツを評価するのに便利なツールです。 を使用 `Voting` コンポーネント、メンバーは上向き矢印または下向き矢印を選択して、意見を示します。

## 投票をページに追加 {#adding-voting-to-a-page}

を追加するには、以下を実行します。 `Voting` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Voting` をドラッグして、ページ上の適切な位置（ユーザーが投票する機能に対する相対位置など）に配置します。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-voting.md#essentials-for-client-side) が含まれる場合、この方法で `Voting` コンポーネントが表示されます。

![投票構成要素](assets/voting-component.png)

## 投票の設定 {#configuring-voting}

配置された `Voting` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

以下 **[!UICONTROL テキストとラベル]** タブで、投票の記録に使用するプロパティを指定します。

![投票ラベル](assets/voting-label.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   (*必須*) 肯定的な応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   (*必須*) 否定的な応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

   (*必須*) 投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーが投票できるのは 1 回だけですが、いつでも投票を変更できます。

### 匿名 {#anonymous}

匿名での投票はサポートされていません。サイト訪問者が投票に 1 回参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [投票の基本事項](essentials-voting.md) 開発者向けのページ
