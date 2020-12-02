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
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 24%

---


# 投票の使用 {#using-voting}

`Voting`コンポーネントは、コミュニティのメンバーがQnAコンポーネント内の回答など、特定のコンテンツの部分を評価するのに役立つツールです。 `Voting`コンポーネントを使用して、メンバーは上向きまたは下向きの矢印を選択し、その意見を示します。

## 投票をページに追加 {#adding-voting-to-a-page}

作成者モードで`Voting`コンポーネントをページに追加するには、コンポーネントブラウザーを使用して`Communities / Voting`を検索し、ページ上にドラッグして配置します。例えば、ユーザーが投票できる機能に対する相対位置です。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](essentials-voting.md#essentials-for-client-side)が含まれる場合、`Voting`コンポーネントは次のように表示されます。

![投票構成要素](assets/voting-component.png)

## 投票の設定 {#configuring-voting}

アクセスする配置済みの`Voting`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![設定](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、投票の記録に使用するプロパティを指定します。

![投票ラベル](assets/voting-label.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   （*必須*）ポジティブな応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   （*必須*）否定的な応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

   （*必須*）投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーが投票できるのは 1 回だけですが、いつでも投票を変更できます。

### 匿名  {#anonymous}

匿名での投票はサポートされていません。サイト訪問者は、一度投票に参加するには、登録（会員になる）し、サインインする必要があります。

## 追加情報 {#additional-information}

詳しい情報は、開発者向けの[投票の必須事項](essentials-voting.md)ページにあります。
