---
title: 初期サンドボックスコンテンツ
seo-title: Initial Sandbox Content
description: コンテンツを作成
seo-description: Create content
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 47%

---

# 初期サンドボックスコンテンツ {#initial-sandbox-content}

ここでは、次のページを作成します。これらのすべてのページで[ページテンプレート](initial-app.md#createthepagetemplate)を使用します。

* SCF Sandbox Site：メインページの英語バージョンにリダイレクトします。

   * SCF Sandbox — サイトの英語バージョンのメインページ。

   * SCF 再生 — 再生するメインページの子。

このチュートリアルでは[言語コピー](../../help/sites-administering/tc-prep.md)については詳しく説明しませんが、HTML ヘッダーによるユーザーの優先言語の検出をルートページに実装し、その言語の適切なメインページにリダイレクトできるように設計されています。ページのノード名に 2 文字の国コードを使用する規則です。例えば、英語の場合は「en」、フランス語の場合は「fr」などです。

## 最初のページの作成 {#create-first-pages}

[ページテンプレート](initial-app.md#createthepagetemplate)を作成したので、ここでは、/content ディレクトリで Web サイトのルートページを設定できます。

1. 標準 UI では現在、サイトを作成するためのブループリントが提供されます。このチュートリアルでは簡単なサイトを作成するので、クラシック UI が便利です。

   クラシック UI に切り替えるには、グローバルナビゲーションを選択し、「プロジェクト」アイコンの右側にマウスカーソルを合わせます。を選択します。 *クラシック UI に切り替え* 表示されるアイコン：

   ![classic-ui](assets/classic-ui.png)

   クラシック UI に切り替える機能は、[管理者が有効にする](../../help/sites-administering/enable-classic-ui.md)必要があります。

1. 次の [クラシック UI のようこそページ](http://localhost:4502/welcome.html)を選択します。 **[!UICONTROL Web サイト]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   または、[/siteadmin](http://localhost:4502/siteadmin) を参照して、Web サイトのクラシック UI に直接アクセスします。

1. エクスプローラウィンドウで、「 」を選択します。 **[!UICONTROL Web サイト]** 次に、ツールバーで **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**.

   **[!UICONTROL ページを作成]**&#x200B;ダイアログで、次のように入力します。

   * タイトル: `SCF Sandbox Site`
   * 名前：`an-scf-sandbox`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. エクスプローラーウィンドウで、作成したページを選択します。 `/Websites/SCF Sandbox Site`をクリックし、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**:

   * タイトル: `SCF Sandbox`
   * 名前：`en`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. エクスプローラーウィンドウで、作成したページを選択します。 `/Websites/SCF Sandbox Site/SCF Sandbox`をクリックし、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**

   * タイトル: `SCF Play`
   * 名前：`play`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. Web サイトコンソールに Web サイトが次のように表示されます。エクスプローラペインで選択した項目の子ページが、管理可能な右側のペインに表示されます。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   次に、Web サイトツールとテンプレートを使用して作成されたページのリポジトリビューを示します。

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## デザインパスの追加 {#add-the-design-path}

条件 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` は、ツールコンソールの designs セクション ( プロパティ「

* `cq:template="/libs/wcm/core/templates/designpage"`

が定義されました。このプロパティによって、`currentDesign.getPath()` () を使用してスクリプト内のデザインアセットを参照するオプション機能が提供されます。例：

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名前：`cq:designPath`
   * タイプ：`String`
   * 値：`/etc/designs/an-scf-sandbox`

* 緑をクリック `[+] Add`

リポジトリは次のようになります。

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* クリック **[!UICONTROL すべて保存]**

設定の保存で問題が発生した場合は、再度ログインし、再度設定してください。

>[!NOTE]
>
>の使用 `cq:designPath` はオプションで、とは無関係です。 [clientlib の使用](develop-app.md#includeclientlibsintemplate)（SCF コンポーネントが使用する際に基本的に必要） [clientlibs](client-customize.md#clientlibs-for-scf) を使用して、JS および CSS を管理できます。
