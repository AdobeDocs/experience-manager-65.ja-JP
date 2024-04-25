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

この `Liking` コンポーネントは、フォーラム内のコメントなど、ユーザーが特定のコンテンツについて意見を表明できるようにする便利なツールです。 （を使用） `Liking` コンポーネントを使用して、メンバーは肯定的な意見を示すハートアイコンを選択します。

## ページへのリンクの追加 {#adding-liking-to-a-page}

を追加します `Liking` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます

* `Communities / Liking`

そして、ユーザーが好きなように、ページ上の場所（機能に対する相対的な位置など）にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](essentials-liking.md#essentials-for-client-side) が含まれる場合、このようにして `Liking` コンポーネントが表示されます。

![liking-component](assets/liking-component.png)

## Liking の設定 {#configuring-liking}

配置されたを選択します。 `Liking` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![configure-new](assets/configure-new.png)

の下 **[!UICONTROL テキストとラベル]** 「いいね」の記録に使用するプロパティを指定します。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 肯定的な応答ラベル]**

  （*必須*）肯定的な応答のプロパティ名。

* **[!UICONTROL 否定応答ラベル]**

  （*必須*）負の応答のプロパティ名。

* **[!UICONTROL 集計名]**

  （*必須*）投票コンポーネントのこのインスタンスの識別可能な内部プロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーはいつでも「いいね！」を変更できます。

### 匿名 {#anonymous}

匿名の好みはサポートされていません。 サイト訪問者が好みに参加するには、登録（メンバーになる）とログインが必要です。

## 追加情報 {#additional-information}

詳しくは、 [Liking Essentials](essentials-liking.md) 開発者向けのページです。
