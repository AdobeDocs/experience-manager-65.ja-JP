---
title: 初期サンドボックスコンテンツ
description: サンドボックスでページテンプレートを使用して、英語版の web サイトのメインページと、メインページの子ページを作成する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 4%

---

# 初期サンドボックスコンテンツ {#initial-sandbox-content}

このセクションでは、以下のページを作成します。これらはすべて、 [ページテンプレート](initial-app.md#createthepagetemplate):

* メインページの英語版にリダイレクトされる SCF サンドボックスサイト。

   * SCF サンドボックス – サイトの英語版のメインページ。

   * SCF プレイ – 再生するメインページの子。

このチュートリアルでは、詳しくは説明しません [言語コピー](../../help/sites-administering/tc-prep.md). 代わりに、ルートページがHTMLヘッダーを介して利用者の優先言語を検出し、その言語の適切なメインページにリダイレクトするように設計される。 慣例により、ページのノード名には 2 文字の国コードを使用します。例えば、英語は「en」、フランス語は「fr」です。

## 最初のページを作成 {#create-first-pages}

新たに [ページテンプレート](initial-app.md#createthepagetemplate)この場合、/content ディレクトリに web サイトのルートページを確立できます。

1. 標準 UI は現在、サイトを作成するためのブループリントを提供しています。 このチュートリアルではシンプルなサイトを作成するので、クラシック UI が役立ちます。

   クラシック UI に切り替えるには、グローバルナビゲーションを選択して、プロジェクト アイコンの右側にカーソルを置きます。 「」を選択します *クラシック UI に切り替え* 表示されるアイコン：

   ![classic-ui](assets/classic-ui.png)

   クラシック UI に切り替える機能は、 [管理者によって有効化されています](../../help/sites-administering/enable-classic-ui.md).

1. から [クラシック UI のようこそページ](http://localhost:4502/welcome.html)を選択 **[!UICONTROL Web サイト]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   または、を参照して、web サイトのクラシック UI に直接アクセスします。 [/siteadmin です。](http://localhost:4502/siteadmin)

1. エクスプローラーペインで、次の項目を選択します。 **[!UICONTROL Web サイト]** 次に、ツールバーでを選択します。 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**.

   が含まれる **[!UICONTROL ページを作成]** ダイアログで、以下を入力します。

   * タイトル: `SCF Sandbox Site`
   * 名前：`an-scf-sandbox`
   * を選択 **[!UICONTROL SCF サンドボックス再生テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. エクスプローラーペインで、作成したページを選択します。 `/Websites/SCF Sandbox Site`を選択し、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**:

   * タイトル: `SCF Sandbox`
   * 名前：`en`
   * を選択 **[!UICONTROL SCF サンドボックス再生テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします

1. エクスプローラーペインで、作成したページを選択します。 `/Websites/SCF Sandbox Site/SCF Sandbox`を選択し、 **[!UICONTROL 新規]** > **[!UICONTROL 新しいページ]**

   * タイトル: `SCF Play`
   * 名前：`play`
   * を選択 **[!UICONTROL SCF サンドボックス再生テンプレート]**
   * 「**[!UICONTROL 作成]**」をクリックします

1. Web サイトコンソールに、web サイトがこのように表示されるようになりました。 エクスプローラーペインで選択された項目の子ページが右側のペインに表示され、そこで管理できます。

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   これは、Web サイトツールとテンプレートを使用して作成された内容のリポジトリビューです。

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## デザインパスを追加 {#add-the-design-path}

条件 ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` は、ツール コンソールの designs セクション、プロパティ「」を使用して作成されました

* `cq:template="/libs/wcm/core/templates/designpage"`

を定義しました。これにより、を使用してスクリプトでデザインアセットを参照するオプション機能が提供されます。 `currentDesign.getPath()`. 例：

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名前：`cq:designPath`
   * タイプ：`String`
   * 値：`/etc/designs/an-scf-sandbox`

* 緑をクリックします `[+] Add`

リポジトリは次のように表示されます。

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* クリック **[!UICONTROL すべて保存]**

設定の保存で問題が発生した場合は、再度ログインして設定し直します。

>[!NOTE]
>
>の使用 `cq:designPath` ：オプションで、 [clientlibs の使用](develop-app.md#includeclientlibsintemplate)（SCF コンポーネントが使用する際に必要） [clientlibs](client-customize.md#clientlibs-for-scf) を使用して JS と CSS を管理します。
