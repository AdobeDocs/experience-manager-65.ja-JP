---
title: 「いいね!」設定の使用
description: 「いいね！」設定コンポーネントを追加し、ユーザーがコメントなどの特定のコンテンツに関する意見を伝えられるように設定する方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 6%

---

# 「いいね!」設定の使用 {#using-liking}

The `Liking` コンポーネントは、フォーラム内のコメントなど、コンテンツの特定の部分に関する意見を表現できる便利なツールです。 を使用 `Liking` コンポーネント、メンバーは、肯定的な意見を示す心アイコンを選択します。

## ページへの「いいね！」の追加 {#adding-liking-to-a-page}

を追加するには、以下を実行します。 `Liking` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Liking`

そして、ページ上の適切な位置（ユーザーが好む機能に対する相対位置など）にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](essentials-liking.md#essentials-for-client-side) が含まれる場合、この方法で `Liking` コンポーネントが表示されます。

![liking-component](assets/liking-component.png)

## 「いいね！」の設定 {#configuring-liking}

配置した `Liking` コンポーネントを使用して、 `Configure` 編集ダイアログを開くアイコン。

![configure-new](assets/configure-new.png)

の下 **[!UICONTROL テキストとラベル]** 「 」タブで、「いいね！」の記録に使用するプロパティを指定します。

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL 肯定的な返信ラベル]**

  (*必須*) 肯定的な応答のプロパティ名。

* **[!UICONTROL 否定的な返信ラベル]**

  (*必須*) 否定的な応答のプロパティ名。

* **[!UICONTROL 集計名]**

  (*必須*) 投票コンポーネントのこのインスタンスの内部で識別可能なプロパティ名。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

### メンバー {#members}

メンバーはいつでも好みを変更できます。

### 匿名 {#anonymous}

匿名の「いいね！」の設定はサポートされていません。 サイト訪問者が「いいね！」に参加するには、登録（メンバーになる）してサインインする必要があります。

## 追加情報 {#additional-information}

詳しくは、 [「いいね！」の設定の基本事項](essentials-liking.md) 開発者向けのページ
