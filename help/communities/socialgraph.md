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

コミュニティメンバーが [&#x200B; アクティビティ &#x200B;](activities.md) をフォローし、従う能力は、`Follow` と `Following` の 2 つのコンポーネントを通じて確立されます。

`Follow` コンポーネントは別のリソースに関連付ける必要があり、この関連付けはコミュニティメンバーおよび機能用に既に確立されています。

`Following` コンポーネントは、現在のメンバーに続くメンバーまたは現在のメンバーの後に続くメンバーをリストするだけです。 メンバー間の関係のこのソーシャルグラフは、[&#x200B; コミュニティサイト &#x200B;](overview.md#communitiessites) 用に作成されたユーザープロファイルに含まれます。

## ページへのフォロワーの追加 {#adding-following-to-a-page}

オーサーモードでページにソーシ `Following` ルコンポーネントを追加する場合は、`Communities / Following` のコンポーネントを見つけて、ソーシャルグラフを表示するページ上の場所にドラッグします。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

[&#x200B; 必須のクライアントサイドライブラリ &#x200B;](essentials-socialgraph.md#essentials-for-client-side) が含まれると、`Following` のコンポーネントは次のように表示されます。

![&#x200B; フォロー &#x200B;](assets/following.png)

## 設定 {#configuring-following}

現在は、プロパティを設定して、コンポーネントに `follows` の関係と `following` の関係のどちらを表示するかを決定する必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; ソーシャルグラフの初期設定 &#x200B;](essentials-socialgraph.md) ページを参照してください。
