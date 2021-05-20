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
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 23%

---

# ソーシャルグラフの使用 {#using-social-graph}

## はじめに {#introduction}

コミュニティメンバーが[アクティビティ](activities.md)をフォローし、フォローする機能は、次の2つのコンポーネントを通じて確立されます。`Follow`と`Following`が含まれます。

`Follow`コンポーネントは、別のリソースに関連付ける必要があり、この関連付けはコミュニティのメンバーと機能に対して既に確立されています。

`Following`コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーをフォローしているメンバーを一覧表示します。 このメンバー間の関係のソーシャルグラフは、[コミュニティサイト](overview.md#communitiessites)用に確立されたユーザープロファイルに含まれます。

## フォロー中コンポーネントをページに追加 {#adding-following-to-a-page}

オーサリングモードでページに`Following`コンポーネントを追加する場合は、コンポーネント`Communities / Following`を選択し、ソーシャルグラフが表示されるページ上の位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-socialgraph.md#essentials-for-client-side)を含めると、`Following`コンポーネントは次のように表示されます。

![次の](assets/following.png)

## フォロー中コンポーネントの設定 {#configuring-following}

現在、コンポーネントに`follows`関係を表示するか`following`関係を表示するかを指定するプロパティを設定する必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[ソーシャルグラフの重要事項](essentials-socialgraph.md)ページを参照してください。
