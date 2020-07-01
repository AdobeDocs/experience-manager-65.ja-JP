---
title: サンプルページの作成
seo-title: サンプルページの作成
description: サンプルコミュニティサイトの作成
seo-description: サンプルコミュニティサイトの作成
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 56c2e6b55964ea5f3e180b17bd2a244882aa62ea
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 73%

---


# サンプルページの作成 {#create-a-sample-page}

AEM Communities 6.1 以降では、サンプルページを作成する最も簡単な方法は、1 つのページ機能のみで構成されるシンプルなコミュニティサイトを作成することです。

この場合、[オーサリング用にコンポーネントを有効](basics.md#accessing-communities-components)にできるように parsys コンポーネントが含まれます。

サンプルコンポーネントを調査するためのもう 1 つのオプションは、[コミュニティコンポーネントガイド](components-guide.md)で提示される機能を使用することです。

## コミュニティサイトの作成 {#create-a-community-site}

これは、[AEM Communities の使用の手引き](getting-started.md)に記載されている新しいサイトの作成とよく似ています。

主な違いは、このチュートリアルでは、[ページ機能](functions.md#page-function)のみを含む新しいコミュニティサイトテンプレートを作成して、他の機能がないシンプルなコミュニティサイトを作成する点です（ただし、すべてのコミュニティサイトの基礎となる、あらかじめ接続された機能は含まれます）。

### 新しいサイトテンプレートの作成 {#create-new-site-template}

初めに、シンプルな[コミュニティサイトテンプレート](sites.md)を作成します。

From global navigation on an author instance select **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Site Templates]**.

![chlimage_1-82](assets/chlimage_1-82.png)

*  `Create button`
* 基本情報

   * `Name`: 単一ページのテンプレート
   * `Description`: 単一のPage関数で構成されるテンプレートです。
   *  `Enabled`

![chlimage_1-83](assets/chlimage_1-83.png)

* 構造

   * Drag a `Page` function to the Template Builder
   * 「構成関数の詳細」に、

      * `Title`: 単一ページ
      * `URL`: page

![chlimage_1-84](assets/chlimage_1-84.png)

* Select **`Save`** for the configuration
* Select **`Save`** for the site template

### 新しいコミュニティサイトの作成 {#create-new-community-site}

次に、シンプルなサイトテンプレートに基づいて新しいコミュニティサイトを作成します。

After creating the site template, from global navigation select **[!UICONTROL Communities > Sites]**.

![chlimage_1-85](assets/chlimage_1-85.png)

* 選択 **`Create`** アイコン

* 手順 `1 - Site Template`

   * `Title`: シンプルコミュニティサイト
   * `Description`: 実験用の単一ページから成るコミュニティサイトです。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: sample

      * url = http://localhost:4502/content/sites/sample

      * `Template`: 選択 `Single Page Template`
      ![chlimage_1-86](assets/chlimage_1-86.png)


*  `Next`
* 手順 `2 - Design`

   * 任意のデザインを選択

*  `Next`
*  `Next`

   （すべてのデフォルト設定を受け入れる）

*  `Create`

   ![chlimage_1-87](assets/chlimage_1-87.png)

## サイトの公開 {#publish-the-site}

![chlimage_1-88](assets/chlimage_1-88.png)

[コミュニティサイトコンソール](sites-console.md)から、「発行」アイコンを選択して、サイトを http://localhost:4503（デフォルト）に公開します。

## オーサー環境でのサイトの編集モードでのオープン {#open-the-site-on-author-in-edit-mode}

![chlimage_1-89](assets/chlimage_1-89.png)

「サイトを開く」アイコンを選択して、編集モードでサイトを表示します。

The URL will be [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![chlimage_1-90](assets/chlimage_1-90.png)

シンプルなホームページでは、コミュニティ機能とテンプレートを介してあらかじめ接続された機能を確認し、コミュニティコンポーネントの追加や設定を試してみることができます。

## パブリッシュ環境でのサイトの表示 {#view-site-on-publish}

ページを公開したら、[パブリッシュインスタンス](http://localhost:4503/content/sites/sample/en.html)でページを開いて、匿名のサイト訪問者、サインインしたメンバーまたは管理者として機能を確認します。作成者環境に表示される「管理」リンクは、管理者がログインしない限り公開環境に表示されません。
