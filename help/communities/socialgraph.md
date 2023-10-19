---
title: ソーシャルグラフの使用
description: サインインしたコミュニティメンバーがアクティビティをフォローしたりフォローしたりできるようにするページに、フォロー中コンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# ソーシャルグラフの使用 {#using-social-graph}

## はじめに {#introduction}

コミュニティメンバーがフォローする機能 [アクティビティ](activities.md) その後には、次の 2 つの要素を通じて確立されます。 `Follow` および `Following`.

The `Follow` コンポーネントは別のリソースに関連付ける必要があり、この関連付けはコミュニティのメンバーと機能に対して既に確立されています。

The `Following` コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーの後に続いているメンバーのみをリストします。 このメンバー間の関係のソーシャルグラフは、 [コミュニティサイト](overview.md#communitiessites).

## ページへのフォローの追加 {#adding-following-to-a-page}

必要に応じて `Following` コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Following` をドラッグし、ページ上のソーシャルグラフを表示する場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-socialgraph.md#essentials-for-client-side) が含まれる場合、この方法で `Following` コンポーネントが表示されます。

![次の](assets/following.png)

## フォローの設定 {#configuring-following}

現在、コンポーネントに `follows` 関係、または `following` 関係。

## 追加情報 {#additional-information}

詳しくは、 [ソーシャルグラフの基本事項](essentials-socialgraph.md) 開発者向けのページ
