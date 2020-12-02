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
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 31%

---


# 「いいね!」設定の使用  {#using-liking}

`Liking`コンポーネントは、ユーザーがフォーラム内のコメントなど、特定のコンテンツに関する意見を表すのに役立つツールです。 `Liking`コンポーネントを使用して、メンバーは、ポジティブな意見を示すハートアイコンを選択します。

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

作成者モードで`Liking`コンポーネントをページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

必要な情報については、[Communities Components Basics](basics.md)を参照してください。

[必要なクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side)が含まれる場合、`Liking`コンポーネントは次のように表示されます。

![好み成分](assets/liking-component.png)

## 「いいね!」の設定{#configuring-liking}

アクセスする配置済みの`Liking`コンポーネントを選択し、編集ダイアログを開く`Configure`アイコンを選択します。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、「いいね！」の記録に使用するプロパティを指定します。

![設定に「いいね！」を付ける](assets/configure-liking.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   （*必須*）ポジティブな応答のプロパティ名です。

* **[!UICONTROL 否定的な返信ラベル]**

   （*必須*）否定的な応答のプロパティ名です。

* **[!UICONTROL 集計名]**

   （*必須*）投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名  {#anonymous}

匿名での「いいね!」はサポートされていません。サイト訪問者は、「いいね！」に参加するには、登録（会員になる）し、サインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[Linking Essentials](essentials-liking.md)ページを参照してください。
