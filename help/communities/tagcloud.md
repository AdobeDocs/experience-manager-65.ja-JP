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
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Social タグクラウドの使用 {#using-social-tag-cloud}

## 概要 {#introduction}

The `Social Tag Cloud` component highlights tags applied by community members when posting content. これは、トレンドトピックを識別し、サイトの訪問者がタグ付きコンテンツをすばやく見つける手段です。

現在のトレンドを識別するもう 1 つの手段については、「[アクティビティのトレンド](trends.md)」を参照してください。

This page documents the `Social Tag Cloud` component dialog settings and describes the user experience.

開発者向けの詳細な情報は、[タグの重要事項](tag.md)を参照してください。

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Social タグクラウドの追加 {#adding-a-social-tag-cloud}

作成者モードでペ `Social Tag Cloud` ージにコンポーネントを追加するには、コンポーネントブラウザーを使用して、タグクラウドが表示さ `Communities / Social Tag Cloud` れるページ上の場所にコンポーネントを配置し、ドラッグします。

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](tag.md#essentials-for-client-side) are included, this is how the `Social Tag Cloud` component will appear:

![chlimage_1-303](assets/chlimage_1-303.png)

## Social タグクラウドの設定 {#configuring-social-tag-cloud}

Select the placed `Social Tag Cloud` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-304](assets/chlimage_1-304.png)

Under the **[!UICONTROL Social Tag Cloud]** tab, specify which tags to display and, if the tags are active links, the location of the page for search results:

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL 表示する Social タグ]**&#x200B;表示する UGC タグを指定します。プルダウン・オプションは次のとおりです。

   * `From page and child pages`
   * `All tags`
   デフォルトは `From page and child pages`で、「page」は下の「 **Page** 」設定を指します。

* **[!UICONTROL ページ]**

   (Required if not `All tags)` The path to the UGC for a page. 初期設定は、空白の場合は現在のページです。

* **[!UICONTROL タグにリンクがありません]**

   チェックすると、タグはプレーンテキストとしてタグクラウドに表示されます。 このチェックボックスをオフにすると、タグはアクティブなリンクとして表示され、タグが適用されるすべてのコンテンツを検索します。 Default is unchecked and requires the **[!UICONTROL Search Result Path]** to be set.

* **[!UICONTROL 検索結果のパス]**

   The path to a page on which a `Search Result` component has been placed, configured to reference UGC which includes the UGC path specified by the **Page** setting.

## Social タグクラウドの表示を変更する {#change-display-of-social-tag-cloud}

**Socialタグクラウドの表示を編集するには、** Design Modeに入り [、配置したコンポーネントを重複](../../help/sites-authoring/default-components-designmode.md)`Social Tag Cloud` がクリックして、追加のタブを含むダイアログを開きます。

Using the **[!UICONTROL Social Tag Cloud (Design)]** tab, specify how tags are displayed. タグは、単純なタグ、デフォルトの名前空間内の単一の単語、または階層的分類です。

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL タイトルの完全なパスを表示]**

   オンにすると、適用された各タグの親タグと名前空間のタイトルが表示されます。

   次に例を示します。

   * チェック: `Geometrixx Media: Gadgets / Cars`
   * 未チェック: `Cars`
   シンプルなタグの場合は、表示に違いは現れません。

   初期設定はオフです。

* **[!UICONTROL リーフタグのみを表示]**

   選択すると、他のタグを含まない、適用されたタグのみが表示されます。

   例えば、次のTagIDを指定したとします。

   `Geometrixx Media: Gadgets / Cars`

   次の3つのタグを適用できます。

   `Geometrixx Media (the namespace)`, `Gadgets`, および `Cars`

   * Checked: Only `Cars` will display, if applied.
   * Unchecked: `Geometrixx Media` and `Gadgets`as well as `Cars` will display, if applied.
   シンプルなタグはリーフタグです。

   初期設定はオフです。

* **[!UICONTROL リンクテンプレート]**

   コンポーネント編集ダイアログでリンクが有効になっている場合、タグクラウド内のリンクの表示に使用される、デフォルト以外のテンプレート。

* **[!UICONTROL すべてのタグに同じサイズ]**

   チェックすると、タグクラウド内のすべての単語が同じスタイルで表示されます。 このオプションをオフにすると、使用方法に応じて異なるスタイルが使用されます。 初期設定はオフです。

## 追加情報 {#additional-information}

More information may be found on the [Tag Essentials](tag.md) page for developers.

See [Tagging User Generated Content](tag-ugc.md) (UGC) for information about creating and managing tags.
