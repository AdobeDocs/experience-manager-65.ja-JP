---
title: 「いいね!」設定の使用
description: ユーザーがコメントなどの特定のコンテンツに関する意見を表明できるように、「いいね」コンポーネントを追加および設定する方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 3%
---
# 「いいね!」設定の使用 {#using-liking}

`Liking` コンポーネントは、フォーラム内のコメントなど、特定のコンテンツに関する意見をユーザーが表明できる便利なツールです。 `Liking` コンポーネントでは、メンバーはハート アイコンを選択して肯定的な意見を示します。

## ページへの「いいね！」の追加 {#adding-liking-to-a-page}

作成者モードでページに`Liking` コンポーネントを追加するには、コンポーネントブラウザーを使用して

* `Communities / Liking`

ユーザーが好む機能に対する相対的な位置など、ページ上の場所にドラッグします。

必要な情報については、[&#x200B; コミュニティコンポーネントの基本](basics.md)を参照してください。

[必要なクライアントサイドライブラリ &#x200B;](essentials-liking.md#essentials-for-client-side)が含まれている場合、`Liking` コンポーネントはこのように表示されます。

![いいね – コンポーネント &#x200B;](assets/liking-component.png)

## 「いいね！」の設定 {#configuring-liking}

配置された`Liking` コンポーネントを選択して、編集ダイアログを開く`Configure` アイコンにアクセスして選択できるようにします。

![configure-new](assets/configure-new.png)

「**[!UICONTROL テキストとラベル]**」タブで、いいね！を記録するために使用するプロパティを指定します。

![configure-like](assets/configure-liking.png)

* **[!UICONTROL 肯定的な応答ラベル]**

  （*必須*）肯定的な応答のプロパティ名。

* **[!UICONTROL 否定的な応答ラベル]**

  （*必須*）否定的な応答のプロパティ名。

* **[!UICONTROL 合計名]**

  （*必須*）投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

会員は、いつでも「いいね！」を変更することができます。

### 匿名 {#anonymous}

匿名リンクはサポートされていません。 サイト訪問者は登録（会員になる）し、ログインして好みに参加する必要があります。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[Liking Essentials](essentials-liking.md) ページを参照してください。
