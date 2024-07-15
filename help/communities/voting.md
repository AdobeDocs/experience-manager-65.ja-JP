---
title: 投票の使用
description: ログインコミュニティメンバーが回答などの特定のコンテンツを評価できるページに投票コンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---

# 投票の使用 {#using-voting}

`Voting` コンポーネントは、コミュニティメンバーが QnA コンポーネント内の回答など、特定のコンテンツを評価できるようにする便利なツールです。 `Voting` コンポーネントでは、メンバーは上矢印または下矢印を選択して自分の意見を示します。

## ページへの投票の追加 {#adding-voting-to-a-page}

オーサーモードで `Voting` コンポーネントをページに追加するには、コンポーネントブラウザーを使用します。 `Communities / Voting` を見つけて、ユーザーが投票できる機能に対する相対的な位置など、ページ上の場所にドラッグします。

必要な情報については、[Communities コンポーネントの基本 ](basics.md) を参照してください。

[ 必須のクライアントサイドライブラリ ](essentials-voting.md#essentials-for-client-side) が含まれると、`Voting` コンポーネントはこのように表示されます。

![voting-component](assets/voting-component.png)

## 投票の設定 {#configuring-voting}

配置された `Voting` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![ 設定 ](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、投票の記録に使用するプロパティを指定します。

![ 投票ラベル ](assets/voting-label.png)

* **[!UICONTROL 肯定的な応答ラベル]**

  （*必須*）正応答の内部プロパティ名。

* **[!UICONTROL 否定応答ラベル]**

  （*必須*）否定応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

  （*必須*）投票コンポーネントのこのインスタンスの、識別可能な内部プロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

会員は一度のみ投票できますが、いつでも投票を変更することができます。

### 匿名 {#anonymous}

匿名投票はサポートされていません。 サイト訪問者が一度投票に参加するには、登録（メンバーになる）とログインが必要です。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [ 投票の基本事項 ](essentials-voting.md) ページを参照してください。
