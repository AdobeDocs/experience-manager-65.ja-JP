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

`Social Tag Cloud` コンポーネントは、コンテンツの投稿時にコミュニティメンバーによって適用されたタグをハイライト表示します。 これは、トレンドのトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにするための手段です。

現在のトレンドを特定するもう 1 つの方法については、[&#x200B; アクティビティのトレンド &#x200B;](trends.md) を参照してください。

このページでは、`Social Tag Cloud` コンポーネントダイアログの設定について説明し、ユーザーエクスペリエンスについて説明します。

開発者向けの詳細については、[&#x200B; タグの基本事項 &#x200B;](tag.md) を参照してください。

タグの作成および管理や、タグが適用されるコンテンツについては、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## ソーシャルタグクラウドの追加 {#adding-a-social-tag-cloud}

オーサーモードでページに `Social Tag Cloud` コンポーネントを追加するには、コンポーネントブラウザーを使用して `Communities / Social Tag Cloud` のコンポーネントを探し、タグクラウドが表示されるページの上にドラッグします。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

[&#x200B; 必須のクライアントサイドライブラリ &#x200B;](tag.md#essentials-for-client-side) が含まれると、`Social Tag Cloud` のコンポーネントは次のように表示されます。

![&#x200B; ソーシャルタグ &#x200B;](assets/social-tag.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置された `Social Tag Cloud` コンポーネントを選択して、編集ダイアログを開く `Configure` アイコンにアクセスして選択できるようにします。

![&#x200B; 設定 &#x200B;](assets/configure-new.png)

「**[!UICONTROL ソーシャルタグクラウド]**」タブで、表示するタグと、タグがアクティブなリンクの場合は検索結果を表示するページの場所を指定します。

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 表示するソーシャルタグ]**
表示する UGC タグを特定します。 プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

  デフォルトは `From page and child pages` です。「page」は以下の **Page** 設定を表します。

* **[!UICONTROL Page]**

  （ない場合は必須 `All tags)` ページの UGC へのパス。 空白のままにした場合、デフォルトは現在のページです。

* **[!UICONTROL タグにリンクがありません]**

  オンにすると、タグはタグクラウドにプレーンテキストとして表示されます。 オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 デフォルトではオフになっており、**[!UICONTROL 検索結果のパス]** を設定する必要があります。

* **[!UICONTROL 検索結果のパス]**

  **Page** 設定で指定された UGC パスを含む UGC を参照するように設定された、`Search Result` コンポーネントが配置されているページへのパス。

## ソーシャル タグ クラウドの表示を変更する {#change-display-of-social-tag-cloud}

**ソーシャルタグクラウド** の表示を編集するには、[&#x200B; デザインモード &#x200B;](../../help/sites-authoring/default-components-designmode.md) と入力し、配置した `Social Tag Cloud` コンポーネントをダブルクリックして、追加のタブを含むダイアログを開きます。

**[!UICONTROL ソーシャルタグクラウド（デザイン）]** タブを使用して、タグの表示方法を指定します。 タグには、単純なタグ、デフォルトの名前空間に含まれる 1 つの単語、階層的な分類などがあります。

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL フルタイトルパスの表示]**

  オンにした場合、適用された各タグの親タグと名前空間のタイトルが表示されます。

  次に例を示します。

   * 確認済み：`Geometrixx Media: Gadgets / Cars`
   * 未チェック：`Cars`

  単純なタグに違いはありません。

  デフォルトではオフになっています。

* **[!UICONTROL リーフタグのみを表示]**

  オンにすると、他のタグを含まない、適用されたタグのみが表示されます。

  例えば、次のタグ ID の場合：

  `Geometrixx Media: Gadgets / Cars`

  次の 3 つのタグを適用できます。

  `Geometrixx Media (the namespace)`、`Gadgets` および `Cars`

   * オン：適用されている場合、`Cars` のみ表示されます。
   * オフ：`Geometrixx Media`、`Gadgets`、および `Cars` が適用されている場合は表示されます。

  単純なタグはリーフタグです。

  デフォルトではオフになっています。

* **[!UICONTROL リンク テンプレート]**

  コンポーネントの編集ダイアログでリンクを有効にした場合に、タグクラウドにリンクを表示するために使用されるテンプレート（デフォルト以外）。

* **[!UICONTROL すべてのタグで同じサイズ]**

  オンにすると、タグクラウド内のすべての単語のスタイルが同じになります。 オフにすると、単語のスタイルは使用法に応じて異なります。 デフォルトではオフになっています。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; タグの初期設定 &#x200B;](tag.md) ページを参照してください。

タグの作成と管理については、[&#x200B; ユーザー生成コンテンツのタグ付け &#x200B;](tag-ugc.md) （UGC）を参照してください。
