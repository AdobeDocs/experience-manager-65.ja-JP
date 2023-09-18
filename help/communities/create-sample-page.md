---
title: サンプルページの作成
description: サンプルコミュニティサイトの作成
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 4%

---

# サンプルページの作成 {#create-a-sample-page}

AEM 6.1 Communities 以降、サンプルページを作成する最も簡単な方法は、単に Page 機能で構成されるシンプルなコミュニティサイトを作成することです。

これには parsys コンポーネントが含まれ、次の操作が可能です。 [オーサリング用コンポーネントの有効化](basics.md#accessing-communities-components).

サンプルコンポーネントを使用した調査のもう 1 つの方法は、 [コミュニティコンポーネントガイド](components-guide.md).

## コミュニティサイトを作成する {#create-a-community-site}

これは、 [AEM Communitiesの概要](getting-started.md).

主な違いは、このチュートリアルでは、 [ページ関数](functions.md#page-function) をクリックして、簡単なコミュニティサイトを作成します。 他の機能（すべてのコミュニティサイトに基本的な配線済みの機能以外）が無料で使用できます。

### 新しいサイトテンプレートの作成 {#create-new-site-template}

作業を開始するには、シンプルな [コミュニティサイトテンプレート](sites.md).

オーサーインスタンスのグローバルナビゲーションから、「 」を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL Communities]** > **[!UICONTROL サイトテンプレート]**.

![create-site-template](assets/create-site-template1.png)

* `Create button` を選択します。
* 基本情報

   * `Name`：単一ページテンプレート
   * `Description`：単一のページ関数で構成されるテンプレート。
   * `Enabled` を選択します。

![site-template-editor](assets/site-template-editor.png)

* 構造

   * ドラッグして `Page` 関数をテンプレートビルダーに追加します。
   * 「構成関数の詳細」に、次のように入力します。

      * `Title`：単一ページ
      * `URL`: ページ

![site-template-editor-structure](assets/site-template-editor1.png)

* 選択 **`Save`** （設定用）
* 選択 **`Save`** （サイトテンプレート用）

### 新しいコミュニティサイトを作成 {#create-new-community-site}

次に、シンプルなサイトテンプレートに基づいてコミュニティサイトを作成します。

サイトテンプレートの作成後、グローバルナビゲーションからを選択します。 **[!UICONTROL コミュニティ/サイト]**.

![create-community-site](assets/create-community-site1.png)

* 選択 **`Create`** アイコン

* 手順 `1 - Site Template`

   * `Title`：シンプルなコミュニティサイト
   * `Description`：実験用の単一のページで構成されるコミュニティサイト。
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`：サンプル

      * url = http://localhost:4502/content/sites/sample

      * `Template`：選択 `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* `Next` を選択します。
* 手順 `2 - Design`

   * 任意のデザインを選択

* `Next` を選択します。
* `Next` を選択します。

  （すべてのデフォルト設定を受け入れる）

* `Create` を選択します。

  ![create-community-site](assets/create-community-site.png)

## サイトの公開 {#publish-the-site}

![publish-site](assets/publish-site.png)

次から： [コミュニティサイトコンソール](sites-console.md)で、サイトを公開する公開アイコンを選択します ( デフォルトではhttp://localhost:4503に設定されています )。

## オーサー環境で編集モードでサイトを開く {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

サイトを編集モードで表示できるように、サイトを開くアイコンを選択します。

URL は [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

簡単なホームページでは、コミュニティの機能やテンプレートを通じて事前に接続されている内容を確認し、コミュニティコンポーネントの追加や設定を行うことができます。

## 公開時にサイトを表示 {#view-site-on-publish}

ページを公開したら、 [発行インスタンス](http://localhost:4503/content/sites/sample/en.html) を使用して、匿名のサイト訪問者、サインインしているメンバー、または管理者としての機能を試すことができます。 オーサー環境に表示される「管理」リンクは、管理者がログインしない限り、パブリッシュ環境には表示されません。
