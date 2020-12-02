---
title: ソーシャルグラフの使用
seo-title: ソーシャルグラフの使用
description: コンポーネントをページに追加
seo-description: コンポーネントをページに追加
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 23%

---


# ソーシャルグラフの使用 {#using-social-graph}

## 概要 {#introduction}

コミュニティのメンバーが[アクティビティ](activities.md)に従う能力は、次の2つの要素を通して確立されます。`Follow`と`Following`。

`Follow`コンポーネントは別のリソースと関連付ける必要があり、この関連付けはコミュニティのメンバーと機能に対して既に確立されています。

`Following`コンポーネントは、現在のメンバーに続くメンバー、または現在のメンバーの後に続くメンバーをリストするだけです。 会員間の関係のこのソーシャルグラフは、[コミュニティサイト](overview.md#communitiessites)に対して確立されたユーザプロファイルに含まれる。

## フォロー中コンポーネントをページに追加 {#adding-following-to-a-page}

作成者モードでページに`Following`コンポーネントを追加する場合は、コンポーネント`Communities / Following`を見つけ、ソーシャルグラフを表示するページ上の場所にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](essentials-socialgraph.md#essentials-for-client-side)が含まれる場合、`Following`コンポーネントは次のように表示されます。

![次の](assets/following.png)

## フォロー中コンポーネントの設定 {#configuring-following}

現在、コンポーネントに`follows`関係を表示するか、`following`関係を表示するかを決定するために、プロパティを設定する必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[ソーシャルグラフの重要事項](essentials-socialgraph.md)ページを参照してください。
