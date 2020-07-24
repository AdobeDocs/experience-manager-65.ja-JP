---
title: 初期サンドボックスコンテンツ
seo-title: 初期サンドボックスコンテンツ
description: コンテンツを作成
seo-description: コンテンツを作成
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 49%

---


# 初期サンドボックスコンテンツ {#initial-sandbox-content}

ここでは、次のページを作成します。これらのすべてのページで[ページテンプレート](initial-app.md#createthepagetemplate)を使用します。

* SCF Sandboxサイト。メインページの英語版にリダイレクトされます。

   * SCF Sandbox — サイトの英語版のメインページです。

   * SCF再生 — 再生するメインページの子。

このチュートリアルでは[言語コピー](../../help/sites-administering/tc-prep.md)については詳しく説明しませんが、HTML ヘッダーによるユーザーの優先言語の検出をルートページに実装し、その言語の適切なメインページにリダイレクトできるように設計されています。規則では、ページのノード名に2文字の国コードを使用します（例：英語は「en」、フランス語は「fr」）。

## 最初のページの作成 {#create-first-pages}

[ページテンプレート](initial-app.md#createthepagetemplate)を作成したので、ここでは、/content ディレクトリで Web サイトのルートページを設定できます。

1. 標準 UI では現在、サイトを作成するためのブループリントが提供されます。このチュートリアルではシンプルなサイトを作成するので、クラシックUIが役に立ちます。

   クラシック UI に切り替えるには、グローバルナビゲーションを選択し、「プロジェクト」アイコンの右側にマウスカーソルを合わせます。Select the *Switch to Classic UI* icon which appears:

   ![chlimage_1-36](assets/chlimage_1-36.png)

   クラシック UI に切り替える機能は、[管理者が有効にする](../../help/sites-administering/enable-classic-ui.md)必要があります。

1. From the [classic UI Welcome page](http://localhost:4502/welcome.html), select **[!UICONTROL Websites]**.

   ![chlimage_1-37](assets/chlimage_1-37.png)

   または、[/siteadmin](http://localhost:4502/siteadmin) を参照して、Web サイトのクラシック UI に直接アクセスします。

1. In the explorer pane, select **[!UICONTROL Websites]** and then in the toolbar select **[!UICONTROL New]** > **[!UICONTROL New Page]**.

   **[!UICONTROL ページを作成]**&#x200B;ダイアログで、次のように入力します。

   * タイトル: `SCF Sandbox Site`
   * 名前：`an-scf-sandbox`
   * Select **[!UICONTROL An SCF Sandbox Play Template]**
   * 「**[!UICONTROL 作成]**」をクリックします。

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. In the explorer pane, select the page you just created, `/Websites/SCF Sandbox Site`, and click **[!UICONTROL New]** > **[!UICONTROL New Page]**:

   * タイトル: `SCF Sandbox`
   * 名前：`en`
   * Select **[!UICONTROL An SCF Sandbox Play Template]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. In the explorer pane, select the page you just created, `/Websites/SCF Sandbox Site/SCF Sandbox`, and click **[!UICONTROL New]** > **[!UICONTROL New Page]**

   * タイトル: `SCF Play`
   * 名前：`play`
   * Select **[!UICONTROL An SCF Sandbox Play Template]**
   * 「**[!UICONTROL 作成]**」をクリックします。

1. Web サイトコンソールに Web サイトが次のように表示されます。エクスプローラペインで選択した項目の子ページが、管理可能な右側のペインに表示されます。

   ![chlimage_1-39](assets/chlimage_1-39.png)

   次に、Web サイトツールとテンプレートを使用して作成されたページのリポジトリビューを示します。

   ![chlimage_1-40](assets/chlimage_1-40.png)

## デザインパスの追加 {#add-the-design-path}

When ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` was created using the designs section of the Tools console, the property ``

* `cq:template="/libs/wcm/core/templates/designpage"`

が定義されました。このプロパティによって、`currentDesign.getPath()` () を使用してスクリプト内のデザインアセットを参照するオプション機能が提供されます。例：

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * 名前：`cq:designPath`
   * 型：`String`
   * 値：`/etc/designs/an-scf-sandbox`

* Click the green `[+] Add`

リポジトリは次のようになります。

![chlimage_1-41](assets/chlimage_1-41.png)

* Click **[!UICONTROL Save All]**

設定の保存で問題が発生した場合は、再ログインして設定を再度行ってください。

>[!NOTE]
>
>The use of `cq:designPath` is optional and is unrelated to the [use of clientlibs](develop-app.md#includeclientlibsintemplate), which are essentially required as the SCF components use [clientlibs](client-customize.md#clientlibs-for-scf) to manage their JS and CSS.


