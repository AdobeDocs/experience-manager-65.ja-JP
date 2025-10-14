---
title: 「いいね!」設定の使用
description: コメントなどの特定のコンテンツに関する意見をユーザーが表現できるように、好みのコンポーネントを追加および設定する方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---

# 「いいね!」設定の使用 {#using-liking}

`Liking` コンポーネントは、フォーラム内のコメントなど、特定のコンテンツに関する意見をユーザーが表現できるようにする便利なツールです。 `Liking` コンポーネントを使用して、メンバーは肯定的な意見を示すハートアイコンを選択します。

## ページへのリンクの追加 {#adding-liking-to-a-page}

オーサーモードで `Liking` コンポーネントをページに追加するには、コンポーネントブラウザーを使用して以下を見つけます

* `Communities / Liking`

そして、ユーザーが好きなように、ページ上の場所（機能に対する相対的な位置など）にドラッグします。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

[&#x200B; 必須のクライアントサイドライブラリ &#x200B;](essentials-liking.md#essentials-for-client-side) が含まれると、`Liking` コンポーネントはこのように表示されます。

![liking-component](assets/liking-component.png)

## Liking の設定 {#configuring-liking}

配置された `Liking` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![configure-new](assets/configure-new.png)

**[!UICONTROL テキストとラベル]** タブの下で、いいね！の記録に使用するプロパティを指定します。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 肯定的な応答ラベル]**

  （*必須*）肯定的な応答のプロパティ名。

* **[!UICONTROL 否定応答ラベル]**

  （*必須*）否定応答のプロパティ名。

* **[!UICONTROL 集計名]**

  （*必須*）投票コンポーネントのこのインスタンスの、識別可能な内部プロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーはいつでも「いいね！」を変更できます。

### 匿名 {#anonymous}

匿名の好みはサポートされていません。 サイト訪問者が好みに参加するには、登録（メンバーになる）とログインが必要です。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [Liking Essentials](essentials-liking.md) ページを参照してください。
