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

これには parsys コンポーネントが含まれるので、次のことができます [オーサリング用コンポーネントを有効にする](basics.md#accessing-communities-components).

サンプルコンポーネントを使用した探索のもう 1 つのオプションは、 [コミュニティコンポーネントガイド](components-guide.md).

## コミュニティサイトの作成 {#create-a-community-site}

これは、で説明しているサイトの作成に似ています。 [AEM Communitiesの概要](getting-started.md).

主な違いは、このチュートリアルでは以下のみを含んだコミュニティサイトテンプレートを作成する点です [ページ関数](functions.md#page-function) 簡単なコミュニティサイトを作成します。 他の機能（すべてのコミュニティサイトに不可欠な有線機能を除く）は含まれません。

### 新しいサイトテンプレートの作成 {#create-new-site-template}

開始するには、シンプルなを作成します [コミュニティサイトテンプレート](sites.md).

オーサーインスタンスのグローバルナビゲーションで、次の項目を選択します **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL サイトテンプレート]**.

![create-site-template](assets/create-site-template1.png)

* `Create button` を選択します。
* 基本情報

   * `Name`：単一ページテンプレート
   * `Description`：単一のページ関数で構成されるテンプレート。
   * `Enabled` を選択します。

![site-template-editor](assets/site-template-editor.png)

* 構造

   * ドラッグ `Page` テンプレートビルダーに対する関数
   * 「構成機能の詳細」で、次のように入力します

      * `Title`：単一ページ
      * `URL`: ページ

![site-template-editor-structure](assets/site-template-editor1.png)

* を選択 **`Save`** 設定の
* を選択 **`Save`** サイトテンプレート用

### 新しいコミュニティサイトを作成 {#create-new-community-site}

次に、シンプルなサイトテンプレートに基づいてコミュニティサイトを作成します。

サイトテンプレートを作成したら、グローバルナビゲーションから「」を選択します。 **[!UICONTROL コミュニティ / サイト]**.

![create-community-site](assets/create-community-site1.png)

* を選択 **`Create`** アイコン

* ステップ `1 - Site Template`

   * `Title`：シンプルなコミュニティサイト
   * `Description`：実験のための単一のページで構成されるコミュニティサイト。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`：サンプル

      * url = http://localhost:4502/content/sites/sample

      * `Template`：を選択 `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* `Next` を選択します。
* ステップ `2 - Design`

   * 任意のデザインを選択

* `Next` を選択します。
* `Next` を選択します。

  （すべてのデフォルト設定を受け入れる）

* `Create` を選択します。

  ![create-community-site](assets/create-community-site.png)

## サイトの公開 {#publish-the-site}

![publish-site](assets/publish-site.png)

から [コミュニティサイトコンソール](sites-console.md)を選択します。デフォルトでは、「公開」アイコンでhttp://localhost:4503にサイトを公開します。

## オーサー環境で編集モードでサイトを開きます {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

「サイトを開く」アイコンを選択して、編集モードでサイトを表示します。

URL はです [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

シンプルなホームページでは、コミュニティの機能やテンプレートをあらかじめ組み込んでいるものを確認したり、コミュニティコンポーネントを追加したり設定したりすることができます。

## 公開時にサイトを表示 {#view-site-on-publish}

ページを公開した後、 [パブリッシュインスタンス](http://localhost:4503/content/sites/sample/en.html) 匿名サイト訪問者、ログインメンバー、管理者などの機能を試すことができます。 オーサー環境に表示される管理リンクは、管理者がログインしない限り、パブリッシュ環境には表示されません。
