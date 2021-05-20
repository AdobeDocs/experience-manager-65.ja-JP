---
title: ソーシャルタグクラウドの使用
seo-title: Social タグクラウドの使用
description: Social タグクラウドコンポーネントをページに追加
seo-description: Social タグクラウドコンポーネントをページに追加
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 22%

---

# Social タグクラウドの使用  {#using-social-tag-cloud}

## はじめに {#introduction}

`Social Tag Cloud`コンポーネントは、コンテンツの投稿時にコミュニティメンバーが適用したタグを強調表示します。 これは、トレンドトピックを識別し、サイト訪問者がタグ付きコンテンツをすばやく見つけられるようにする手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

このページでは、`Social Tag Cloud`コンポーネントダイアログの設定と、ユーザーエクスペリエンスについて説明します。

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

タグの作成と管理、およびタグが適用されるコンテンツについて詳しくは、[タグの管理](../../help/sites-administering/tags.md)を参照してください。

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

`Social Tag Cloud`コンポーネントをオーサリングモードでページに追加するには、コンポーネントブラウザーを使用して`Communities / Social Tag Cloud`を探し、タグクラウドが表示されるページ上の位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](basics.md)を参照してください。

[必須のクライアント側ライブラリ](tag.md#essentials-for-client-side)を含めると、`Social Tag Cloud`コンポーネントは次のように表示されます。

![socialタグ](assets/social-tag.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

配置済みの`Social Tag Cloud`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

「**[!UICONTROL Socialタグクラウド]**」タブで、表示するタグを指定し、タグがアクティブなリンクの場合は検索結果のページの場所を指定します。

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウンオプションは次のとおりです。

   * `From page and child pages`
   * `All tags`

   デフォルト値は`From page and child pages`です。「page」は、以下の&#x200B;**Page**&#x200B;設定を参照します。

* **[!UICONTROL ページ]**

   (`All tags)`でない場合は必須。ページのUGCへのパス。 空白の場合、初期設定は現在のページです。

* **[!UICONTROL タグにリンクがありません]**

   オンにすると、タグはプレーンテキストとしてタグクラウドに表示されます。 オフにすると、タグは、そのタグが適用されるすべてのコンテンツを検索するアクティブなリンクとして表示されます。 初期設定はオフで、**[!UICONTROL 検索結果のパス]**&#x200B;を設定する必要があります。

* **[!UICONTROL 検索結果のパス]**

   `Search Result`コンポーネントが配置されたページへのパス。**Page**&#x200B;設定で指定されたUGCパスを含むUGCを参照するように設定されます。

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

**Socialタグクラウド**&#x200B;の表示を編集するには、[デザインモード](../../help/sites-authoring/default-components-designmode.md)に入り、配置された`Social Tag Cloud`コンポーネントをダブルクリックして、追加のタブを含むダイアログを開きます。

「**[!UICONTROL Socialタグクラウド（デザイン）]**」タブを使用して、タグの表示方法を指定します。 タグは、単純なタグ、デフォルトの名前空間内の単一の単語、または階層的な分類です。

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL タイトルの完全なパスを表示]**

   オンにすると、適用された各タグの親タグと名前空間のタイトルが表示されます。

   以下に例を示します。

   * チェック: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`

   シンプルなタグの場合は、表示に違いは現れません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**

   オンにすると、他のタグを含まない、適用されたタグのみが表示されます。

   例えば、タグIDが次のように指定すると、

   `Geometrixx Media: Gadgets / Cars`

   次の3つのタグを適用できます。

   `Geometrixx Media (the namespace)`, `Gadgets`, および `Cars`

   * オン：`Cars`のみが表示されます（適用される場合）。
   * オフ：`Geometrixx Media`と`Gadgets`、および`Cars`が表示されます（適用される場合）。

   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**

   コンポーネントの編集ダイアログでリンクが有効になっている場合、タグクラウド内にリンクを表示するために使用される、デフォルト以外のテンプレート。

* **[!UICONTROL すべてのタグに同じサイズ]**

   オンにすると、タグクラウド内のすべての単語に同じスタイルが設定されます。 オフにすると、単語のスタイルが使用方法に応じて異なります。 初期設定はオフです。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[タグの基本事項](tag.md)ページを参照してください。

タグの作成と管理について詳しくは、[ユーザー生成コンテンツのタグ付け](tag-ugc.md)(UGC)を参照してください。
