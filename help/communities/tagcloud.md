---
title: Social タグクラウドの使用
description: ログインしたコミュニティメンバーがトレンドのトピックをすばやく識別し、タグ付けされたコンテンツを見つけることができるようにするページにソーシャルタグクラウドコンポーネントを追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 6%

---

# Social タグクラウドの使用 {#using-social-tag-cloud}

## はじめに {#introduction}

この `Social Tag Cloud` コンポーネントは、コンテンツの投稿時にコミュニティメンバーによって適用されたタグをハイライト表示します。 これは、トレンドのトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにするための手段です。

現在のトレンドを特定するもう一つの方法は、次をご覧ください。 [アクティビティのトレンド](trends.md).

このページは、 `Social Tag Cloud` コンポーネントダイアログの設定と、ユーザーエクスペリエンスについての説明です。

開発者向けの詳細については、を参照してください。 [タグの基本事項](tag.md).

タグの作成および管理や、タグが適用されるコンテンツについては、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## ソーシャルタグクラウドの追加 {#adding-a-social-tag-cloud}

を追加します `Social Tag Cloud` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます `Communities / Social Tag Cloud` タグクラウドが表示されるページの場所にドラッグします。

詳細については、 [Communities コンポーネントの基本](basics.md).

いつ [必要なクライアントサイドライブラリ](tag.md#essentials-for-client-side) が含まれる場合、このようにして `Social Tag Cloud` コンポーネントが表示されます。

![social-tag](assets/social-tag.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置されたを選択します。 `Social Tag Cloud` にアクセスして選択できるコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

の下 **[!UICONTROL Social タグクラウド]** タブで、表示するタグを指定します。タグがアクティブなリンクの場合は、検索結果を表示するページの場所を指定します。

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 表示するソーシャルタグ]**
表示する UGC タグを特定します。 プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

  デフォルトはです `From page and child pages`（「ページ」はを指します） **ページ** を以下に設定します。

* **[!UICONTROL Page]**

  （必要ない場合） `All tags)` ページの UGC へのパス。 空白のままにした場合、デフォルトは現在のページです。

* **[!UICONTROL タグにリンクがありません]**

  オンにすると、タグはタグクラウドにプレーンテキストとして表示されます。 オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 デフォルトではオフで、次が必要です **[!UICONTROL 検索結果のパス]** を設定します。

* **[!UICONTROL 検索結果のパス]**

  が含まれているページへのパス `Search Result` コンポーネントが配置され、 **ページ** の設定値。

## ソーシャル タグ クラウドの表示を変更する {#change-display-of-social-tag-cloud}

の表示を編集するには **Social タグクラウド**、と入力します [デザインモード](../../help/sites-authoring/default-components-designmode.md) 配置されたをダブルクリックします。 `Social Tag Cloud` コンポーネント：追加のタブを持つダイアログを開きます。

使用， **[!UICONTROL Social タグクラウド（デザイン）]** タブで、タグの表示方法を指定します。 タグには、単純なタグ、デフォルトの名前空間に含まれる 1 つの単語、階層的な分類などがあります。

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL フルタイトルパスを表示]**

  オンにした場合、適用された各タグの親タグと名前空間のタイトルが表示されます。

  次に例を示します。

   * 確認済み： `Geometrixx Media: Gadgets / Cars`
   * オフ： `Cars`

  単純なタグに違いはありません。

  デフォルトではオフになっています。

* **[!UICONTROL リーフタグのみを表示]**

  オンにすると、他のタグを含まない、適用されたタグのみが表示されます。

  例えば、次のタグ ID の場合：

  `Geometrixx Media: Gadgets / Cars`

  次の 3 つのタグを適用できます。

  `Geometrixx Media (the namespace)`、`Gadgets` および `Cars`

   * オン：のみ `Cars` 適用されている場合は表示されます。
   * オフ： `Geometrixx Media`, `Gadgets`、および `Cars` 適用されている場合は表示されます。

  単純なタグはリーフタグです。

  デフォルトではオフになっています。

* **[!UICONTROL テンプレートをリンク]**

  コンポーネントの編集ダイアログでリンクを有効にした場合に、タグクラウドにリンクを表示するために使用されるテンプレート（デフォルト以外）。

* **[!UICONTROL すべてのタグで同じサイズ]**

  オンにすると、タグクラウド内のすべての単語のスタイルが同じになります。 オフにすると、単語のスタイルは使用法に応じて異なります。 デフォルトではオフになっています。

## 追加情報 {#additional-information}

詳しくは、 [タグの基本事項](tag.md) 開発者向けのページです。

参照： [ユーザー生成コンテンツのタグ付け](tag-ugc.md) タグの作成と管理については、（UGC）を参照してください。
