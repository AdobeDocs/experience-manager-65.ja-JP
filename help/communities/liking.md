---
title: 「いいね!」設定の使用
seo-title: Using Liking
description: 「いいね!」設定コンポーネントの追加と設定
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 28%

---

# 「いいね!」設定の使用 {#using-liking}

この `Liking` コンポーネントは、フォーラム内のコメントなど、コンテンツの特定の部分に関する意見をユーザーが表現できる便利なツールです。 を使用 `Liking` コンポーネント、メンバーは、肯定的な意見を示す心アイコンを選択します。

## ページへの「いいね!」設定の追加 {#adding-liking-to-a-page}

を追加するには、以下を実行します。 `Liking` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Liking`

を探し、ページ上の適切な位置（ユーザーに「いいね!」してもらう機能の近くなど）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side) が含まれる場合、この方法で `Liking` コンポーネントが表示されます。

![liking-component](assets/liking-component.png)

## 「いいね!」の設定 {#configuring-liking}

配置された `Liking` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

以下 **[!UICONTROL テキストとラベル]** 「 」タブで、「いいね！」の記録に使用するプロパティを指定します。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 肯定的な返信ラベル]**

   (*必須*) 肯定的な応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

   (*必須*) 否定的な応答のプロパティ名。

* **[!UICONTROL 集計名]**

   (*必須*) 投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーは、いつでも「いいね!」を変更できます。

### 匿名 {#anonymous}

匿名での「いいね!」はサポートされていません。サイト訪問者が「いいね！」に参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [「いいね！」の設定の基本事項](essentials-liking.md) 開発者向けのページ
