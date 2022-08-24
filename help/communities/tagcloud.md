---
title: Social タグクラウドの使用
seo-title: Using Social Tag Cloud
description: Social タグクラウドコンポーネントをページに追加
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 24%

---

# Social タグクラウドの使用 {#using-social-tag-cloud}

## はじめに {#introduction}

この `Social Tag Cloud` コンポーネントは、コンテンツの投稿時にコミュニティメンバーが適用したタグをハイライトします。 これは、トレンドトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

このページでは、 `Social Tag Cloud` コンポーネントダイアログの設定およびユーザーエクスペリエンスについて説明します。

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

タグの作成および管理や、タグが適用されるコンテンツについては、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

を追加するには、以下を実行します。 `Social Tag Cloud` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Social Tag Cloud` をクリックし、ページ上のタグクラウドが表示される場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

次の場合に [必要なクライアント側ライブラリ](tag.md#essentials-for-client-side) が含まれる場合、この方法で `Social Tag Cloud` コンポーネントが表示されます。

![social-tag](assets/social-tag.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置された `Social Tag Cloud` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

以下 **[!UICONTROL Social タグクラウド]** タブで、表示するタグを指定し、タグがアクティブなリンクの場合は、検索結果のページの場所を指定します。

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

   デフォルトはです。 `From page and child pages`(「page」は **ページ** を設定します。

* **[!UICONTROL Page]**

   ( そうでない場合は必須 `All tags)` ページの UGC へのパス。 空白の場合、初期設定は現在のページです。

* **[!UICONTROL タグにリンクがありません]**

   オンにすると、タグはプレーンテキストとしてタグクラウドに表示されます。 オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 デフォルトはオフで、に必要な **[!UICONTROL 検索結果のパス]** を設定します。

* **[!UICONTROL 検索結果のパス]**

   ページのパス。 `Search Result` コンポーネントが配置され、 **ページ** 設定。

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

表示を編集するには **Social タグクラウド**&#x200B;を入力して、 [デザインモード](../../help/sites-authoring/default-components-designmode.md) そして、配置された `Social Tag Cloud` 追加のタブを含むダイアログを開くコンポーネント。

の使用 **[!UICONTROL Social タグクラウド（デザイン）]** タブで、タグの表示方法を指定します。 タグは、単純なタグ、デフォルト名前空間の単一の単語、階層的な分類のいずれかになります。

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL タイトルの完全なパスを表示]**

   オンにすると、適用された各タグの親タグと名前空間のタイトルが表示されます。

   次に例を示します。

   * チェック済み: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`

   シンプルなタグの場合は、表示に違いは現れません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**

   オンにすると、他のタグを含まない、適用されたタグのみが表示されます。

   例えば、次のタグ ID が指定されます。

   `Geometrixx Media: Gadgets / Cars`

   次の 3 つのタグを適用できます。

   `Geometrixx Media (the namespace)`, `Gadgets`, および `Cars`

   * チェック済み：のみ `Cars` が表示されます（適用されている場合）。
   * オフ： `Geometrixx Media` および `Gadgets`同様に `Cars` が表示されます（適用されている場合）。

   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**

   コンポーネント編集ダイアログでリンクを有効にした場合、タグクラウドにリンクを表示するために使用される、デフォルト以外のテンプレートです。

* **[!UICONTROL すべてのタグに同じサイズ]**

   オンにすると、タグクラウド内のすべての単語に同じスタイルが設定されます。 オフにすると、単語のスタイルは使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

詳しくは、 [タグの基本事項](tag.md) 開発者向けのページ

詳しくは、 [ユーザー生成コンテンツのタグ付け](tag-ugc.md) (UGC) を参照してください。
