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
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 31%

---

# 「いいね!」設定の使用  {#using-liking}

`Liking`コンポーネントは、フォーラム内のコメントなど、コンテンツの特定の部分に関する意見を伝えるのに役立つツールです。 `Liking`コンポーネントを使用して、メンバーは心アイコンを選択して肯定的な意見を示します。

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

`Liking`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side)を含めると、`Liking`コンポーネントは次のように表示されます。

![liking-component](assets/liking-component.png)

## 「いいね!」の設定{#configuring-liking}

配置済みの`Liking`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、「いいね！」の記録に使用するプロパティを指定します。

![設定のいいね！](assets/configure-liking.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   （*必須*）正の応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   （*必須*）負の応答のプロパティ名。

* **[!UICONTROL 集計名]**

   （*必須*）投票コンポーネントのこのインスタンスの、識別可能な内部プロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名 {#anonymous}

匿名での「いいね!」はサポートされていません。サイト訪問者が「いいね！」を設定するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[「いいね！」の基本事項](essentials-liking.md)ページを参照してください。
