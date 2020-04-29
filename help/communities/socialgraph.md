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
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# ソーシャルグラフの使用 {#using-social-graph}

## 概要 {#introduction}

The ability for a community member to follow [activities](activities.md) as well as be followed is established through two components: `Follow` and `Following`.

The `Follow` component must be associated with another resource, and this association is already established for community members and features.

The `Following` component simply lists the members that are either following the current member or are being followed by the current member. This social graph of the relationships between members is included in the user profile established for a [community site](overview.md#communitiessites).

## フォロー中コンポーネントをページに追加 {#adding-following-to-a-page}

作成者モードでページにコンポーネ `Following` ントを追加する場合は、コンポーネントを見つけて、ソーシャルグ `Communities / Following` ラフを表示するページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-socialgraph.md#essentials-for-client-side) are included, this is how the `Following` component will appear:

![chlimage_1-447](assets/chlimage_1-447.png)

## フォロー中コンポーネントの設定 {#configuring-following}

Currently, it is necessary to set the property to determine whether the component displays the `follows` relationship, or the `following` relationship.

## 追加情報 {#additional-information}

詳しくは、開発者向けの[ソーシャルグラフの重要事項](essentials-socialgraph.md)ページを参照してください。
