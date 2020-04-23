---
title: 「いいね!」設定の使用
seo-title: 「いいね!」設定の使用
description: 「いいね!」設定コンポーネントの追加と設定
seo-description: 「いいね!」設定コンポーネントの追加と設定
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# 「いいね!」設定の使用 {#using-liking}

The `Liking` component is a useful tool that allows users to express an opinion about a particular piece of content, such as an comment within a forum. With the `Liking` component, members select the heart icon to indicate a positive opinion.

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

To add a `Liking` component to a page in author mode, use the component browser to locate:

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-liking.md#essentials-for-client-side) are included, this is how the `Liking` component will appear.

![chlimage_1-93](assets/chlimage_1-93.png)

## 「いいね!」の設定{#configuring-liking}

Select the placed `Liking` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-94](assets/chlimage_1-94.png)

Under the **[!UICONTROL Texts &amp; Labels]** tab, specify the properties used to record likes.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   (必&#x200B;*須*)ポジティブな応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   (必&#x200B;*須*)否定応答のプロパティ名。

* **[!UICONTROL 集計名]**

   (*Required*) The internal, identifiable property name for this instance of a voting component.

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名 {#anonymous}

匿名での「いいね!」はサポートされていません。サイト訪問者は登録（会員になる）し、サインインして「いいね！」に参加する必要があります。

## 追加情報 {#additional-information}

More information may be found on the [Liking Essentials](essentials-liking.md) page for developers.
