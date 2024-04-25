---
title: ソーシャルグラフの使用
description: ログインしたコミュニティメンバーがアクティビティをたどったりフォローしたりできるページに、次のコンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# ソーシャルグラフの使用 {#using-social-graph}

## はじめに {#introduction}

コミュニティメンバーがフォローする機能 [activities](activities.md) そして、次の 2 つのコンポーネントを通じて従う必要があります。 `Follow` および `Following`.

この `Follow` コンポーネントは別のリソースに関連付ける必要があり、この関連付けはコミュニティメンバーおよび機能用に既に確立されています。

この `Following` コンポーネントは、現在のメンバーに続くメンバーまたは現在のメンバーの後に続くメンバーのリストを表示するだけです。 メンバー間の関係のこのソーシャルグラフは、用に作成されたユーザープロファイルに含まれます。 [コミュニティサイト](overview.md#communitiessites).

## ページへのフォロワーの追加 {#adding-following-to-a-page}

を追加する場合 `Following` オーサーモードのページへのコンポーネントの移動 `Communities / Following` ソーシャルグラフを表示するページの上にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](essentials-socialgraph.md#essentials-for-client-side) が含まれる場合、このようにして `Following` コンポーネントが表示されます。

![次の](assets/following.png)

## 設定 {#configuring-following}

現在は、プロパティを設定して、コンポーネントがを表示するかどうかを判断する必要があります `follows` relationship、または `following` 関係。

## 追加情報 {#additional-information}

詳しくは、 [ソーシャルグラフの基本事項](essentials-socialgraph.md) 開発者向けのページです。
