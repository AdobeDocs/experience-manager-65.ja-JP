---
title: サンプルページの作成
description: シンプルなコミュニティサイトの作成に役立つ、ページ関数のみを含んだコミュニティサイトテンプレートを作成する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# サンプルページの作成 {#create-a-sample-page}

AEM 6.1 Communities の場合、サンプルページを作成する最も簡単な方法は、Page 関数だけで構成されるシンプルなコミュニティサイトを作成することです。

これには parsys コンポーネントが含まれるので、このコンポーネントを [&#x200B; オーサリング用に有効にする &#x200B;](basics.md#accessing-communities-components) ことができます。

サンプルコンポーネントを使用した探索のもう 1 つのオプションは、[&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md) に記載されている機能を使用することです。

## コミュニティサイトの作成 {#create-a-community-site}

これは、[AEM Communitiesの基本を学ぶ &#x200B;](getting-started.md) で説明されているサイトの作成に似ています。

主な違いは、このチュートリアルでは、単純なコミュニティサイトを作成するための [&#x200B; ページ関数 &#x200B;](functions.md#page-function) のみを含むコミュニティサイトテンプレートを作成する点です。 他の機能（すべてのコミュニティサイトに不可欠な有線機能を除く）は含まれません。

### 新しいサイトテンプレートの作成 {#create-new-site-template}

開始するには、シンプルな [&#x200B; コミュニティサイトテンプレート &#x200B;](sites.md) を作成します。

オーサーインスタンスのグローバルナビゲーションで、**[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL サイトテンプレート]** を選択します。

![create-site-template](assets/create-site-template1.png)

* `Create button` を選択します。
* 基本情報

   * `Name`：単一ページテンプレート
   * `Description`：単一の Page 関数で構成されるテンプレート。
   * `Enabled` を選択します。

![site-template-editor](assets/site-template-editor.png)

* 構造

   * `Page` 関数をテンプレートビルダーにドラッグ
   * 「構成機能の詳細」で、次のように入力します

      * `Title`：単一ページ
      * `URL`: ページ

![site-template-editor-structure](assets/site-template-editor1.png)

* 設定する **`Save`** を選択します
* サイトテンプレートの **`Save`** を選択

### 新しいコミュニティサイトを作成 {#create-new-community-site}

次に、シンプルなサイトテンプレートに基づいてコミュニティサイトを作成します。

サイトテンプレートを作成したら、グローバルナビゲーションから **[!UICONTROL Communities/サイト]** を選択します。

![create-community-site](assets/create-community-site1.png)

* アイコン **`Create`** 選択

* ステップ `1 - Site Template`

   * `Title`：シンプルなコミュニティサイト
   * `Description`：実験のための単一ページで構成されるコミュニティサイト。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: サンプル

      * url = http://localhost:4502/content/sites/sample

      * `Template`: `Single Page Template` を選択

     ![create-community-site-template](assets/create-community-site-template.png)

* `Next` を選択します。
* ステップ `2 - Design`

   * 任意のデザインを選択

* `Next` を選択します。
* `Next` を選択します。

  （すべてのデフォルト設定を受け入れる）

* `Create` を選択します。

  ![create-community-site](assets/create-community-site.png)

## サイトのPublish {#publish-the-site}

![publish-site](assets/publish-site.png)

[&#x200B; コミュニティサイトコンソール &#x200B;](sites-console.md) から、公開アイコンを選択して、サイトを公開します（デフォルトではhttp://localhost:4503）。

## オーサー環境で編集モードでサイトを開きます {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

「サイトを開く」アイコンを選択して、編集モードでサイトを表示します。

URL は [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html) です

![author-site](assets/author-site.png)

シンプルなホームページでは、コミュニティの機能やテンプレートをあらかじめ組み込んでいるものを確認したり、コミュニティコンポーネントを追加したり設定したりすることができます。

## Publishでサイトを表示 {#view-site-on-publish}

ページを公開したら、[&#x200B; パブリッシュインスタンス &#x200B;](http://localhost:4503/content/sites/sample/en.html) 上のページを開いて、匿名サイト訪問者、ログインメンバー、管理者などの機能を試します。 オーサー環境に表示される管理リンクは、管理者がログインしない限り、パブリッシュ環境には表示されません。
