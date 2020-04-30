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
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# 投票の使用 {#using-voting}

The `Voting` component is a useful tool that allows community members to rate a particular piece of content, such as an answer within a QnA component. With the `Voting` component, members select up or down arrows to indicate their opinion.

## 投票をページに追加 {#adding-voting-to-a-page}

作成者モード `Voting` でページにコンポーネントを追加するには、コンポーネントブラウザを使用してページを検索し、そのページ上の位置（ユーザが投票する機能に対する相対位置など）に `Communities / Voting` ドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-voting.md#essentials-for-client-side) are included, this is how the `Voting` component will appear.

![chlimage_1-307](assets/chlimage_1-307.png)

## 投票の設定 {#configuring-voting}

Select the placed `Voting` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-308](assets/chlimage_1-308.png)

Under the **[!UICONTROL Texts &amp; Labels]** tab, specify the properties used to record votes.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   (必&#x200B;*須*)肯定的な応答の内部プロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   (必&#x200B;*須*)否定応答の内部プロパティ名。

* **[!UICONTROL 集計名]**

   (*Required*) The internal, identifiable property name for this instance of a voting component.

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーが投票できるのは 1 回だけですが、いつでも投票を変更できます。

### 匿名 {#anonymous}

匿名での投票はサポートされていません。サイト訪問者は、一度投票に参加するには登録（会員になる）し、サインインする必要があります。

## 追加情報 {#additional-information}

More information may be found on the [Voting Essentials](essentials-voting.md) page for developers.
