---
title: 初期サンドボックスコンテンツ
description: コンテンツを作成
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 6%

---

# 初期サンドボックスコンテンツ {#initial-sandbox-content}

このセクションでは、次のページを作成します。これらはすべて [ページテンプレート](initial-app.md#createthepagetemplate):

* SCF Sandbox Site：メインページの英語バージョンにリダイレクトします。

   * SCF Sandbox — サイトの英語バージョンのメインページ。

   * SCF 再生 — 再生するメインページの子。

このチュートリアルでは詳しく説明しませんが、 [言語コピー](../../help/sites-administering/tc-prep.md)の場合、ルートページでHTMLヘッダーを使用してユーザーの優先言語の検出を実装し、その言語に適したメインページにリダイレクトできるように設計されています。 ページのノード名に 2 文字の国コードを使用する規則です。例えば、英語の場合は「en」、フランス語の場合は「fr」です。

## 最初のページを作成 {#create-first-pages}

これで、 [ページテンプレート](initial-app.md#createthepagetemplate)を使用すると、Web サイトのルートページを/content ディレクトリに設定できます。

1. 標準 UI には、現在、サイトを作成するためのブループリントが用意されています。 このチュートリアルでは簡単なサイトを作成するので、クラシック UI が便利です。

   クラシック UI に切り替えるには、グローバルナビゲーションを選択し、プロジェクトアイコンの右側にマウスポインターを置きます。 を選択します。 *クラシック UI に切り替え* 表示されるアイコン：

   ![classic-ui](assets/classic-ui.png)

   クラシック UI に切り替える機能は、次の条件を満たす必要があります。 [管理者が有効にした](../../help/sites-administering/enable-classic-ui.md).

1. 次の [クラシック UI のようこそページ](http://localhost:4502/welcome.html)を選択します。 **[!UICONTROL Web サイト]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   または、Web サイトのクラシック UI に直接アクセスするには、 [/siteadmin.](http://localhost:4502/siteadmin)

1. エクスプローラウィンドウで、「 」を選択します。 **[!UICONTROL Web サイト]** 次に、ツールバーで **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**.

   内 **[!UICONTROL ページを作成]** ダイアログで、次の情報を入力します。

   * タイトル: `SCF Sandbox Site`
   * 名前：`an-scf-sandbox`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. エクスプローラーペインで、作成したページを選択します。 `/Websites/SCF Sandbox Site`をクリックし、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**:

   * タイトル: `SCF Sandbox`
   * 名前：`en`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. エクスプローラーペインで、作成したページを選択します。 `/Websites/SCF Sandbox Site/SCF Sandbox`をクリックし、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**

   * タイトル: `SCF Play`
   * 名前：`play`
   * 選択 **[!UICONTROL SCF Sandbox Play テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. Web サイトが Web サイトコンソールに表示されます。 エクスプローラペインで選択した項目の子ページが、管理可能な右側のペインに表示されます。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   これは、Web サイトツールとテンプレートを使用して作成された内容のリポジトリ表示です。

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## デザインパスを追加 {#add-the-design-path}

条件 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` は、ツールコンソールの designs セクション ( プロパティ「

* `cq:template="/libs/wcm/core/templates/designpage"`

が定義されました。これは、を使用してスクリプト内のデザインアセットを参照するオプションの機能を提供します。 `currentDesign.getPath()`. 例：

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名前：`cq:designPath`
   * タイプ：`String`
   * 値：`/etc/designs/an-scf-sandbox`

* 緑をクリック `[+] Add`

リポジトリは次のように表示されます。

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* クリック **[!UICONTROL すべて保存]**

設定の保存で問題が発生した場合は、再ログインし、再度設定してください。

>[!NOTE]
>
>の使用 `cq:designPath` はオプションで、とは無関係です。 [clientlib の使用](develop-app.md#includeclientlibsintemplate)（SCF コンポーネントが使用する際に必要） [clientlibs](client-customize.md#clientlibs-for-scf) を使用して、JS および CSS を管理できます。
