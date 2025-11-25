---
title: 完全な機能を備えた web サイトの作成（JSP）
description: このチュートリアルでは、Adobe Experience Manager（AEM）で完全な機能を備えた web サイトを作成する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d7cf843c-c837-4b97-b6c5-0fbd6793bdd4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '4923'
ht-degree: 95%

---

# 完全な機能を備えた web サイトの作成（JSP）{#create-a-fully-featured-website-jsp}

>[!NOTE]
>
>この記事では、JSP を使用して、クラシック UI に基づいた web サイトを作成する方法について説明します。アドビでは、[AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)で詳しく説明しているように、web サイトに最新の Adobe Experience Manager（AEM）テクノロジーを利用することをお勧めします。

このチュートリアルでは、AEM で完全な機能を備えた web サイトを作成できます。Web サイトは汎用の web サイトに基づき、主に web 開発者をターゲットにしています。すべての開発は、1 つのオーサー環境内で行われます。

このチュートリアルでは、次の方法について説明します。

1. AEM をインストールします。
1. CRXDE Lite（開発環境）にアクセスします。
1. CRXDE Lite でプロジェクトの構造を設定します。
1. コンテンツページを作成する際の基礎として使用するテンプレート、コンポーネントおよびスクリプトを作成します。
1. Web サイトのルートページを作成し、次にコンテンツページを作成します。
1. ページで使用する以下のコンポーネントを作成します。

   * 上部ナビゲーション
   * リストの子
   * Logo（ロゴ）
   * 画像
   * テキスト画像
   * 検索

1. 様々な基盤コンポーネントを含めます。

すべての手順を実行すると、ページは次のようになります。

![chlimage_1-24](assets/chlimage_1-24.png)

**最終結果をダウンロード**

演習を実行する代わりにチュートリアルに従うには、website-1.0.zip をダウンロードします。このファイルは、このチュートリアルの結果を含む AEM コンテンツパッケージです。[パッケージマネージャー](/help/sites-administering/package-manager.md)を使用して、パッケージをオーサーインスタンスにインストールします。

**メモ：**&#x200B;このパッケージをインストールすると、このチュートリアルを使用して作成したオーサーインスタンス上のリソースがすべて上書きされます。

Web サイトコンテンツパッケージ

[ファイルを入手](assets/website-1_0.zip)

## Adobe Experience Manager のインストール {#installing-adobe-experience-manager}

Web サイトを開発するための AEM インスタンスをインストールするには、[オーサーインスタンスとパブリッシュインスタンスを含むデプロイメント環境](/help/sites-deploying/deploy.md#author-and-publish-installs)の設定手順に従うか、または[汎用インストール](/help/sites-deploying/deploy.md#default-local-install)を実行します。汎用インストールでは、AEM クイックスタート JAR ファイルをダウンロードし、license.properties ファイルを JAR ファイルと同じディレクトリに配置して、JAR ファイルをダブルクリックします。

AEM をインストールしたら、ようこそページで CRXDE Lite のリンクをクリックして CRXDE Lite 開発環境にアクセスします。

![chlimage_1-25](assets/chlimage_1-25.png)

>[!NOTE]
>
>デフォルトポートを使用してローカルにインストールされたAEM オーサーインスタンスのCRXDE Liteの URL は [https://localhost:4502/crx/de/](https://localhost:4502/crx/de/) です。

### CRXDE Lite でプロジェクトの構造を設定します。 {#setting-up-the-project-structure-in-crxde-lite}

CRXDE Lite を使用して、リポジトリ内に mywebsite アプリケーション構造を作成します。

1. CRXDE Liteの左側のツリーで、**`/apps`** フォルダーを右クリックし、**作成**／**作成**／**フォルダー**&#x200B;をクリックします。**フォルダーを作成**&#x200B;ダイアログで、フォルダー名として `mywebsite` と入力し、「**OK**」をクリックします。
1. **`/apps/mywebsite`** フォルダーを右クリックして、**作成**／**フォルダーを作成**&#x200B;をクリックします。**フォルダーを作成**&#x200B;ダイアログで、フォルダー名として `components` と入力し、「**OK**」をクリックします。
1. **`/apps/mywebsite`** フォルダーを右クリックして、**作成**／**フォルダーを作成**&#x200B;をクリックします。**フォルダーを作成**&#x200B;ダイアログで、フォルダー名として `templates` と入力し、「**OK**」をクリックします。

   ツリー内の構造は次のようになります。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 「**すべて保存**」をクリックします。

### デザインの設定 {#setting-up-the-design}

この節では、Designer ツールを使用して、アプリケーションのデザインを作成します。デザインは、web サイトに CSS および画像リソースを提供します。

>[!NOTE]
>
>以下のリンクをクリックして mywebsite.zip をダウンロードします。アーカイブには、デザイン用の static.css および画像ファイルが含まれています。

サンプルの static.css ファイルおよび画像

[ファイルを入手](assets/mywebsite.zip)

1. AEM のようこそ画面で、「**ツール**」をクリックします。（[https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html)）

   ![chlimage_1-27](assets/chlimage_1-27.png)

1. フォルダーツリーで、**Designs** フォルダーを選択して、**新規**／**新しいページ**&#x200B;をクリックします。タイトルとして `mywebsite` と入力し、「**作成**」をクリックします。

1. mywebsite という項目がテーブルに表示されない場合は、ツリーまたはテーブルを更新します。

1. [WebDAV を使用 &#x200B;](/help/sites-administering/webdav-access.md)https://localhostの URL にアクセスします :4502。サンプル `static.css` ファイルと `images` フォルダーを、ダウンロードした mywebsite.zip ファイルから `/etc/designs/mywebsite` フォルダーにコピーします。

   ![chlimage_1-28](assets/chlimage_1-28.png)

### contentpage テンプレート、コンポーネントおよびスクリプトの作成 {#creating-the-contentpage-template-component-and-script}

この節では、次を作成します。

* サンプル web サイト内のコンテンツページの作成に使用される contentpage テンプレート
* コンテンツのページをレンダリングするために使用される contentpage コンポーネント
* contentpage スクリプト

#### contentpage テンプレートの作成 {#creating-the-contentpage-template}

サイトの web ページの基礎として使用するテンプレートを作成します。

テンプレートは、新しいページのデフォルトコンテンツを定義します。複雑な web サイトでは、サイト内の様々なタイプのページを作成するために、複数のテンプレートを使用する場合があります。この演習では、すべてのページを 1 つのシンプルなテンプレートに基づいて作成します。

1. CRXDE Lite のフォルダーツリーで、`/apps/mywebsite/templates` を右クリックして、**作成**／**テンプレートを作成**&#x200B;をクリックします。

1. テンプレートを作成ダイアログで、次の値を入力して「**次へ**」をクリックします。

   * **ラベル**：contentpage
   * **タイトル**：マイ web サイトのコンテンツページコンポーネント
   * **説明**：マイ web サイトのコンテンツページコンポーネントです。
   * **リソースタイプ：** mywebsite/components/contentpage

   「ランキング」プロパティにはデフォルト値を使用します。

   ![chlimage_1-29](assets/chlimage_1-29.png)

   リソースタイプは、ページをレンダリングするコンポーネントを識別します。この場合、contentpage テンプレートを使用して作成されたページはすべて `mywebsite/components/contentpage` コンポーネントによってレンダリングされます。

1. このテンプレートを使用できるページのパスを指定するには、プラス記号のボタンをクリックして、表示されるテキストボックスに `/content(/.*)?` と入力します。次に、「**次へ**」をクリックします。

   ![chlimage_1-30](assets/chlimage_1-30.png)

   許可されているパスプロパティの値は&#x200B;*正規表現です。*&#x200B;この正規表現に一致するパスを含むページがテンプレートを使用できます。この場合、正規表現は、**/content** フォルダーおよびすべてのサブページのパスと一致します。

   作成者が /content の下にページを作成すると、使用可能なテンプレートのリストに **contentpage** テンプレートが表示されます。

1. **許可された親**&#x200B;パネルおよび&#x200B;**許可されている子**&#x200B;パネルで「**次へ**」をクリックして、「**OK**」をクリックします。CRXDE Lite で、「**すべて保存**」をクリックします。

   ![chlimage_1-31](assets/chlimage_1-31.png)

#### contentpage コンポーネントの作成 {#creating-the-contentpage-component}

コンテンツを定義し、contentpage テンプレートを使用するコンポーネントを作成します&#x200B;*。*&#x200B;コンポーネントの場所は、contentpage テンプレートの「リソースタイプ」プロパティの値と一致する必要があります。

1. CRXDE Lite で、`/apps/mywebsite/components` を右クリックして、**作成**／**コンポーネント**&#x200B;をクリックします。
1. **コンポーネントを作成**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * **ラベル**：contentpage
   * **タイトル**：マイ web サイトのコンテンツページコンポーネント
   * **説明**：マイ web サイトのコンテンツページコンポーネントです

   ![chlimage_1-32](assets/chlimage_1-32.png)

   新しいコンポーネントの場所は `/apps/mywebsite/components/contentpage` です。このパスは、contentpage テンプレートのリソースタイプ（パスの最初の **`/apps/`** 部分を除く）に対応します。

   この一致は、テンプレートをコンポーネントと結び付けるものなので、Web サイトを正常に機能させるために重要です。

1. 「**次へ**」をクリックしてダイアログの許可されている子パネルを表示し、「**OK**」をクリックします。CRXDE Lite で、「**すべて保存**」をクリックします。

   この時点で構造は次のようになります。

   ![chlimage_1-33](assets/chlimage_1-33.png)

#### contentpage コンポーネントスクリプトの開発 {#developing-the-contentpage-component-script}

contentpage.jsp スクリプトにコードを追加して、ページのコンテンツを定義します。

1. CRXDE Liteで、`/apps/mywebsite/components/contentpage` にあるファイル `contentpage.jsp` を開きます。ファイルには、デフォルトで次のコードが含まれています。

   ```java
   <%--
   
     My Website Content Page Component component.
   
     This is My Website Content Page Component.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
       /* TODO add you code here */
   %>
   ```

1. 以下のコードをコピーして、contentpage.jsp のデフォルトコードの後に貼り付けます。

   ```java
   <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
       pageEncoding="ISO-8859-1"%>
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "https://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
   <title>My title</title>
   </head>
   <body>
   <div>My body</div>
   </body>
   </html>
   ```

1. 「**すべて保存**」をクリックして変更を保存します。

### Web サイトページおよびコンテンツページの作成 {#creating-your-website-page-and-content-pages}

ここでは、すべて contentpage テンプレートを使用する、My Website、English、Products、Services、Customers の各ページを作成します。

1. AEMのようこそページ （[https://localhost:4502/libs/cq/core/content/welcome.html](https://localhost:4502/libs/cq/core/content/welcome.html)）で、「Web サイト」をクリックします。

   ![chlimage_1-34](assets/chlimage_1-34.png)

1. フォルダーツリーで、**Websites** フォルダーを選択して、**新規**／**新しいページ**&#x200B;をクリックします。
1. **ページを作成**&#x200B;ウィンドウで、以下を入力します。

   * タイトル: `My Website`
   * 名前：`mywebsite`
   * `My Website Content Page Template`

   ![chlimage_1-35](assets/chlimage_1-35.png)

1. 「**作成**」をクリックします。フォルダーツリーで、**/Websites/My Website/** ページを選択して、**新規**／**新しいページ**&#x200B;をクリックします。
1. ページを作成ダイアログで、以下のプロパティ値を入力して「作成」をクリックします。

   * タイトル：English
   * 名前：en
   * 「My Website Content Page Template」を選択します。

1. フォルダーツリーで、**/Websites/My Website/English** ページを選択して、**新規**／**新しいページ**&#x200B;をクリックします。
1. **ページを作成**&#x200B;ダイアログで、以下のプロパティ値を入力して「**作成**」をクリックします。

   * タイトル：Products
   * 「My Website Content Page Template」を選択します。

1. フォルダーツリーで、**/Websites/My Website/English** ページを選択して、**新規**／**新しいページ**&#x200B;をクリックします。
1. **ページを作成**&#x200B;ダイアログで、以下のプロパティ値を入力して「**作成**」をクリックします。

   * タイトル：Services
   * 「My Website Content Page Template」を選択します。

1. フォルダーツリーで、**/Websites/My Website/English** ページを選択して、**新規**／**新しいページ**&#x200B;をクリックします。
1. **ページを作成**&#x200B;ダイアログで、以下のプロパティ値を入力して「**作成**」をクリックします。

   * タイトル：Customers
   * 「My Website Content Page Template」を選択します。

   構造は次のようになります。

   ![chlimage_1-36](assets/chlimage_1-36.png)

1. ページを mywebsite デザインにリンクさせるには、CRXDE Liteで、`/content/mywebsite/en/jcr:content` ノードを選択します。「プロパティ」タブで、新しいプロパティに次の値を入力し、「追加」をクリックします。

   * 名前：cq:designPath
   * タイプ：String
   * 値：/etc/designs/mywebsite

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. Web ブラウザーの新しいタブまたはウィンドウで、[https://localhost:4502/content/mywebsite/en/products.html](https://localhost:4502/content/mywebsite/en/products.html) を開いて Products ページを確認します。

   ![chlimage_1-38](assets/chlimage_1-38.png)

### contentpage スクリプトの拡張 {#enhancing-the-contentpage-script}

この節では、AEM 基盤コンポーネントスクリプトを使用し、独自のスクリプトを記述することで、contentpage スクリプトを拡張する方法について説明します。

完了したら、**製品**&#x200B;ページは次のようになります。

![chlimage_1](assets/chlimage_1.jpeg)

#### 基盤ページスクリプトの使用 {#using-the-foundation-page-scripts}

この演習では、スーパータイプが AEM のページコンポーネントとなるように pagecontent コンポーネントを設定します。コンポーネントはスーパータイプの機能を継承するので、pagecontent はページコンポーネントのスクリプトとプロパティを継承します。

例えば、自分のコンポーネントの JSP コード内で、スーパータイプコンポーネントによって提供されているスクリプトを、自分のコンポーネントに含まれているかのように参照できます。

1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` ノードにプロパティを追加します。

   1. `/apps/mywebsite/components/contentpage` ノードを選択します。
   1. 「プロパティ」タブの下部で、以下のプロパティ値を入力して「追加」をクリックします。

      * **名前：** sling:resourceSuperType
      * **タイプ：** String
      * **値：** foundation/components/page

   1. 「すべて保存」をクリックします。

1. `/apps/mywebsite/components/contentpage` の下の `contentpage.jsp` ファイルを開いて、既存のコードを以下のコードに置換します。

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" contentType="text/html; charset=utf-8" %><%
   %><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
   <html>
   <cq:include script="head.jsp"/>
   <cq:include script="body.jsp"/>
   </html>
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。次のようなコンソールが表示されます。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

   ページソースを開いて、head.jsp および body.jsp スクリプトで生成された JavaScript 要素と HTML 要素を確認します。次のスクリプトスニペットは、ページを開く際にサイドキックを開きます。

   ```java
   CQ.WCM.launchSidekick("/content/mywebsite/en/products",
               {propsDialog: "/libs/foundation/components/page/dialog",
                  locked: false locked: false
                });
   ```

#### 独自のスクリプトの使用 {#using-your-own-scripts}

この節では、ページ本文の一部を生成する複数のスクリプトを作成します。次に、pagecontent コンポーネントに body.jsp ファイルを作成して、AEM ページコンポーネントの body.jsp を上書きします。body.jsp ファイルに、ページ本文の様々な部分を生成するスクリプトを含めます。

**ヒント：**&#x200B;コンポーネントのスーパータイプ内のファイルと同じ名前で相対的な場所も同じファイルがコンポーネントに含まれている場合、これをオーバーレイと呼びます&#x200B;*。*

1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` の下に `left.jsp` ファイルを作成します。

   1. `/apps/mywebsite/components/contentpage` ノードを右クリックして、「**作成**」を選択し、「**ファイルを作成**」を選択します。

   1. ウィンドウで「**名前**」に `left.jsp` と入力して、「**OK**」をクリックします。

1. `left.jsp` ファイルを編集して、既存のコンテンツを削除し、以下のコードに置き換えます。

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="left">
   <div>logo</div>
   <div>newslist</div>
   <div>search</div>
   </div>
   ```

1. 変更内容を保存します。
1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` の下に `center.jsp` ファイルを作成します。

   1. `/apps/mywebsite/components/contentpage` ノードを右クリックして、**作成**／**ファイルを作成**&#x200B;を選択します。

   1. ダイアログボックスで、「`center.jsp`名前&#x200B;**」に** と入力して、「**OK**」をクリックします。

1. `center.jsp` ファイルを編集して、既存のコンテンツを削除し、以下のコードに置換します。

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="center">
   <div>trail</div>
   <div>title</div>
   <div>parsys</div>
   </div>
   ```

1. 変更内容を保存します。
1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` の下に `right.jsp` ファイルを作成します。

   1. `/apps/mywebsite/components/contentpage` ノードを右クリックして、**作成**／**ファイルを作成**&#x200B;を選択します。

   1. ダイアログボックスで、「`right.jsp`名前&#x200B;**」に** と入力して、「**OK**」をクリックします。

1. `right.jsp` ファイルを編集して、既存のコンテンツを削除し、以下のコードに置き換えます。

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><div class="right">
   <div>iparsys</div>
   </div>
   ```

1. 変更内容を保存します。
1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` の下に `body.jsp` ファイルを作成します。
1. `body.jsp` ファイルを編集して、既存のコンテンツを削除し、以下のコードに置き換えます。

   ```java
   <%@include file="/libs/foundation/global.jsp"%><%
   %><body>
   <div id="CQ">
   <div class="topnav">topnav</div>
   <div class="content">
   <cq:include script="left.jsp" />
   <cq:include script="center.jsp" />
   <cq:include script="right.jsp" />
   </div>
   <div class="footer">
   <div class="toolbar">toolbar</div>
   </div>
   </div>
   </body>
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。次のようなコンソールが表示されます。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 上部ナビゲーションコンポーネントの作成 {#creating-the-top-navigation-component}

この節では、ナビゲーションを容易にするために、web サイトのすべてのトップレベルページへのリンクを表示するコンポーネントを作成します。このコンポーネントのコンテンツは、contentpage テンプレートを使用して作成されるすべてのページの上部に表示されます。

上部ナビゲーションコンポーネント（topnav）の最初のバージョンでは、ナビゲーション項目はテキストリンクのみです。2 つ目のバージョンでは、画像ナビゲーションリンクを含む topnav を実装します。

完了したら、上部ナビゲーションは次のようになります。

![chlimage_1-39](assets/chlimage_1-39.png)

#### 上部ナビゲーションコンポーネントの作成 {#creating-the-top-navigation-component-1}

1. CRXDE Lite で `/apps/mywebsite/components` を右クリックして、**作成**／**コンポーネントを作成**&#x200B;をクリックします。
1. **コンポーネントを作成**&#x200B;ウィンドウで、以下を入力します。

   * **ラベル**： `topnav`

   * **タイトル**: `My Top Navigation Component`

   * **説明**: `This is My Top Navigation Component`

1. 最後のウィンドウまで「**次へ**」をクリックしたら、「**OK**」をクリックします。変更を保存します。

#### テキストリンクを含む上部ナビゲーションスクリプトの作成 {#creating-the-top-navigation-script-with-textual-links}

topnav にレンダリングスクリプトを追加して、子ページへのテキストリンクを生成します。

1. CRXDE Lite で、`/apps/mywebsite/components/topnav` の下の `topnav.jsp` ファイルを開きます。
1. 次のコードをコピーと貼り付けし、そこにあるコードを置き換えます。

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
           com.day.text.Text,
           com.day.cq.wcm.api.PageFilter, com.day.cq.wcm.api.Page" %><%
       /* get starting point of navigation */
       Page navRootPage = currentPage.getAbsoluteParent(2);
       if (navRootPage == null && currentPage != null) {
       navRootPage = currentPage;
       }
       if (navRootPage != null) {
           Iterator<Page> children = navRootPage.listChildren(new PageFilter(request));
           while (children.hasNext()) {
               Page child = children.next();
               %><a href="<%= child.getPath() %>.html"><%=child.getTitle() %></a><%
           }
       }
   %>
   ```

#### contentpage コンポーネントへの上部ナビゲーションの追加 {#including-top-navigation-in-the-contentpage-component}

topnav を contentpage コンポーネントに含めるには、次の操作を行います。

1. CRXDE Lite で、`/apps/mywebsite/components/contentpage` の下の `body.jsp` ファイルを開いて、

   ```xml
   <div class="topnav">topnav</div>
   ```

   以下に置き換えます。

   ```xml
   <cq:include path="topnav" resourceType="mywebsite/components/topnav" />
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。上部ナビゲーションは次のように表示されます。

   ![chlimage_1-40](assets/chlimage_1-40.png)

#### サブタイトル付きのページの強化 {#enhancing-pages-with-subtitles}

ページコンポーネントでは、ページのキャプションを指定できるプロパティを定義します。ページコンテンツに関する情報を提供するキャプションを追加します。

1. ブラウザーで、**製品**&#x200B;ページを開きます。
1. サイドキックの「**ページ**」タブで、「**ページのプロパティ**」をクリックします。
1. ダイアログの「基本」タブで「**他のタイトルと説明**」を展開して、「**サブタイトル**」プロパティに「**私たちの活動**」と入力します。「**OK**」をクリックします。
1. ここまでの手順を繰り返して、「**私たちのサービス**」というサブタイトルを&#x200B;**サービス**&#x200B;ページに追加します。
1. ここまでの手順を繰り返して、「**私たちが得た信頼**」というサブタイトルを&#x200B;**顧客**&#x200B;ページに追加します。

   **ヒント：** CRXDE Liteで、/content/mywebsite/en/products/jcr:content ノードを選択して、subtitle プロパティが追加されていることを確認します。

#### 画像リンクを使用して上部ナビゲーションを強化する {#enhance-top-navigation-by-using-image-links}

topnav コンポーネントのレンダリングスクリプトを強化して、ナビゲーションコントロールにハイパーテキストの代わりに画像リンクを使用します。画像には、リンクターゲットのタイトルとサブタイトルが含まれます。

この演習では、[Sling のリクエスト処理](/help/sites-developing/the-basics.md#sling-request-processing)を示します。topnav.jsp スクリプトを変更して、ページナビゲーションリンクに使用する画像を動的に生成するスクリプトを呼び出します。この演習では、Sling は画像ソースファイルの URL を解析し、画像のレンダリングに使用するスクリプトを決定します。

例えば、製品ページへの画像リンクのソースは、https://localhost:4502/content/mywebsite/en/products.navimage.png になります。 Sling は、この URL を解析して、リソースタイプと、リソースをレンダリングするために使用するスクリプトを決定します。

1. Sling がリソースのパスを `/content/mwebysite/en/products.png.` と特定します。
1. Sling がこのパスを `/content/mywebsite/en/products` ノードと照合します。
1. Sling がこのノードの `sling:resourceType` を `mywebsite/components/contentpage` と特定します。

1. Sling が、このコンポーネント内で、URL セレクター（`navimage`）およびファイル名拡張子（`png`）に最も一致するスクリプトを見つけます。

この演習では、Sling はこれらの URL を、ユーザーが作成する /apps/mywebsite/components/contentpage/navimage.png.java スクリプトと照合します。

1. CRXDE Lite で、`/apps/mywebsite/components/topnav.` の下の `topnav.jsp` を開きます。アンカー要素（14 行目）のコンテンツを見つけます。

   ```xml
   <%=child.getTitle() %>
   ```

1. アンカーコンテンツを次のコードに置き換えます。

   ```xml
   <img alt="<%= child.getTitle() %>" src="<%= child.getPath() %>.navimage.png">
   ```

1. 変更内容を保存します。
1. `/apps/mywebsite/components/contentpage` ノードを右クリックして、**作成**／**ファイルを作成**&#x200B;をクリックします。
1. **ファイルを作成**&#x200B;ウィンドウで、「**名前**」に `navimage.png.java` と入力します。

   .java というファイル名の拡張子は、Apache Sling Scripting Java™ Support を使用してスクリプトをコンパイルし、サーブレットを作成する必要があることを Sling に示しています。

1. 以下のコードを `navimage.png.java.` にコピーします。このコードによって、AbstractImageServlet クラスが拡張されます。

   * [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) は、現在のリソースのプロパティを格納する ImageContext オブジェクトを作成します。
   * リソースの親ページは、ImageContext オブジェクトから抽出されます。次に、ページタイトルとサブタイトルが取得されます。
   * [ImageHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/ImageHelper.html) は、サイトデザインの navimage_bg.jpg ファイル、ページタイトルおよびページサブタイトルから画像を生成するために使用されます。

   ```java
   package apps.mywebsite.components.contentpage;
   
   import java.awt.Color;
   import java.awt.Paint;
   import java.awt.geom.Rectangle2D;
   
   import java.io.IOException;
   import javax.jcr.RepositoryException;
   
   import com.day.cq.wcm.api.Page;
   import com.day.cq.wcm.api.PageManager;
   import com.day.cq.wcm.api.components.Component;
   import com.day.cq.wcm.api.designer.Designer;
   
   import com.day.cq.commons.SlingRepositoryException;
   import com.day.cq.wcm.commons.WCMUtils;
   import com.day.cq.wcm.commons.AbstractImageServlet;
   import com.day.cq.commons.ImageHelper;
   
   import com.day.image.Font;
   import com.day.image.Layer;
   
   import org.apache.sling.api.SlingHttpServletRequest;
   import org.apache.sling.api.SlingHttpServletResponse;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
   
   /**
     * Renders the navigation image
     */
   public class navimage_png extends AbstractImageServlet {
   
         protected Layer createLayer(ImageContext ctx)
                throws RepositoryException, IOException {
            PageManager pageManager = ctx.resolver.adaptTo(PageManager.class);
            Page currentPage = pageManager.getContainingPage(ctx.resource);
   
            /* constants for image appearance */
            int scale = 6;
            int paddingX = 24;
            int paddingY = 24;
            Color bgColor = new Color(0x004a565c, true);
   
            /* obtain the page title */
            String title = currentPage.getTitle();
            if (title == null) {
                title = currentPage.getName();
            }
   
            /* format the title text */
            title = title.toUpperCase();
            Paint titleColor = Color.WHITE;
            Font titleFont = new Font("Myriad Pro", 10 * scale, Font.BOLD);
            int titleBase = 10 * scale;
   
            /* obtain and format the page subtitle */
            String subtitle = currentPage.getProperties().get("subtitle", "");
            Paint subtitleColor = new Color(0xffa9afb1, true);
            Font subTitleFont = new Font("Tahoma", 7);
            int subTitleBase = 20;
   
            /* create a layer that contains the background image from the mywebsite design */
            Designer dg = ctx.resolver.adaptTo(Designer.class);
            String imgPath = new String(dg.getDesignPath(currentPage)+"/images/navimage_bg.jpg");
            Layer bg = ImageHelper.createLayer(ctx.resolver.resolve(imgPath));
   
            /* draw the title text (4 times bigger) */
            Rectangle2D titleExtent = titleFont.getTextExtent(0, 0, 0, 0, title, Font.ALIGN_LEFT, 0, 0);
            Rectangle2D subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
   
            /* ensure subtitleExtent is wide enough */
            if ( subtitle.length() > 0 ) {
                int titleWidth = (int)titleExtent.getWidth() / scale;
                if ( subtitleExtent.getWidth() > titleWidth && subtitleExtent.getWidth() + 2 * paddingX >
    bg.getWidth() ) {
                    int charWidth = (int)subtitleExtent.getWidth() / subtitle.length();
                    int maxWidth = (bg.getWidth() > titleWidth + 2  * paddingX ? bg.getWidth() - 2 * paddingX : titleWidth);
                    int len = (maxWidth - ( 2 * charWidth) ) / charWidth;
                    subtitle = subtitle.substring(0, len) + "...";
                    subtitleExtent = subTitleFont.getTextExtent(0, 0, 0, 0, subtitle, Font.ALIGN_LEFT, 0, 0);
                }
            }
            int width = Math.max((int) titleExtent.getWidth(), (int) subtitleExtent.getWidth());
           /* create the text layer */
            Layer text = new Layer(width, (int) titleExtent.getHeight() + 40, new Color(0x01ffffff, true));
            text.setPaint(titleColor);
            text.drawText(0, titleBase, 0, 0, title, titleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            text.resize(text.getWidth() / scale, text.getHeight() / scale);
            text.setX(0);
            text.setY(0);
   
            if (subtitle.length() > 0) {
                /* draw the subtitle normal sized */
                text.setPaint(subtitleColor);
                text.drawText(0, subTitleBase, 0, 0, subtitle, subTitleFont, Font.ALIGN_LEFT | Font.ALIGN_BASE, 0, 0);
            }
   
            /* merge the image and text layers */
            text.setY(paddingY);
            text.setX(paddingX);
            text.setBackgroundColor(bgColor);
   
            int bgWidth = bg.getWidth();
            if ( text.getWidth() + 2 * paddingX > bgWidth ) {
                bgWidth = text.getWidth() + 2 * paddingX;
                bg.resize(bgWidth, bg.getHeight());
            }
            bg.merge(text);
   
            return bg;
        }
    }
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。上部ナビゲーションは次のように表示されます。

   ![screen_shot_2012-03-07at10047pm](assets/screen_shot_2012-03-07at10047pm.png)

### リストの子コンポーネントの作成 {#creating-the-list-children-component}

ページのタイトル、説明、日付（製品ページなど）を含むページリンクのリストを生成する listchildren コンポーネントを作成します。リンクは、現在のページの子ページ、またはコンポーネントダイアログで指定されたルートページをターゲットとします。

![chlimage_1-41](assets/chlimage_1-41.png)

#### 製品ページの作成 {#creating-product-pages}

製品ページの下に 2 つのページを作成します。2 つの特定の製品について説明する各ページに、タイトル、説明および日付を設定します。

1. Web サイトページのフォルダーツリーで、Websites/My Website/English/Products 項目を選択し、新規／新しいページをクリックします。
1. ダイアログで、次のプロパティ値を入力して「作成」をクリックします。

   * タイトル：Product 1
   * 名前：product1
   * 「マイ web サイトコンテンツページテンプレート」を選択します。

1. 次のプロパティ値を使用して、Products の下に別のページを作成します。

   * タイトル：Product 2
   * 名前：product2
   * 「マイ web サイトコンテンツページテンプレート」を選択します。

1. CRXDE Lite で、Product 1 ページの説明と日付を設定します。

   1. `/content/mywebsite/en/products/product1/jcr:content` ノードを選択します。
   1. 「**プロパティ**」タブで、以下の値を入力します。

      * 名前：`jcr:description`
      * タイプ：`String`
      * 値：`This is a description of the Product 1!.`

   1. 「**追加**」をクリックします。
   1. 「**プロパティ**」タブで、次の値を使用して別のプロパティを作成します。

      * 名前：date
      * タイプ：String
      * 値：02/14/2008
      * 「追加」をクリックします。

   1. 「すべて保存」をクリックします。

1. CRXDE Lite で、Product 2 ページの説明と日付を設定します。

   1. /content/mywebsite/en/products/product2/jcr:content ノードを選択します。
   1. 「**プロパティ**」タブで、以下の値を入力します。

      * 名前：jcr:description
      * タイプ：String
      * 値：商品 2 の説明です。

   1. 「**追加**」をクリックします。
   1. 同じテキストボックスで、以前の値を次の値に置き換えます。

      * 名前：date
      * タイプ：String
      * 値：05/11/2012
      * 「追加」をクリックします。

   1. 「すべて保存」をクリックします。

#### リストの子コンポーネントの作成 {#creating-the-list-children-component-1}

listchildren コンポーネントを作成するには、次の操作を実行します。

1. CRXDE Lite で `/apps/mywebsite/components` を右クリックして、**作成**／**コンポーネントを作成**&#x200B;をクリックします。
1. ダイアログで、次のプロパティ値を入力して「次へ」をクリックします。

   * ラベル：listchildren
   * タイトル：自分の Listchildren コンポーネント
   * 説明：これは自分の Listchildren コンポーネントです。

1. 「次へ」を数回クリックして許可されている子パネルを表示し、「OK」をクリックします。

#### リストの子スクリプトの作成 {#creating-the-list-children-script}

listchildren コンポーネントのスクリプトを開発します。

1. CRXDE Lite で、`/apps/mywebsite/components/listchildren` の下の `listchildren.jsp` ファイルを開きます。
1. デフォルトのコードを次のコードに置き換えます。

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="java.util.Iterator,
            com.day.cq.wcm.api.PageFilter"%><%
        /* Create a Page object using the path of the current page */
         String listroot = properties.get("listroot", currentPage.getPath());
        Page rootPage = pageManager.getPage(listroot);
        /* iterate through the child pages and gather properties */
        if (rootPage != null) {
            Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
            while (children.hasNext()) {
                Page child = children.next();
                String title = child.getTitle() == null ? child.getName() : child.getTitle();
                String date = child.getProperties().get("date","");
                %><div class="item">
                <a href="<%= child.getPath() %>.html"><b><%= title %></b></a>
                <span><%= date %></code><br>
                <%= child.getProperties().get("jcr:description","") %><br>
                </div><%
            }
        }
    %>
   ```

1. 変更内容を保存します。

#### リストの子ダイアログの作成 {#creating-the-list-children-dialog}

listchildren コンポーネントのプロパティの設定に使用するダイアログを作成します。

1. listchildren コンポーネントの下に dialog ノードを作成します。

   1. CRXDE Lite で `/apps/mywebsite/components/listchildren` ノードを右クリックして、**作成**／**ダイアログを作成**&#x200B;をクリックします。

   1. ダイアログで、以下のプロパティ値を入力して「OK」をクリックします。

      * **ラベル**：`dialog`

      * **タイトル**：`Edit Component` を行い、「**OK**」をクリックします。

   ![screen_shot_2012-03-07at45818pm](assets/screen_shot_2012-03-07at45818pm.png)

   次のようにプロパティを定義します。

   ![screen_shot_2012-03-07at50415pm](assets/screen_shot_2012-03-07at50415pm.png)

1. `/apps/mywebsite/components/listchildren/dialog/items/items/tab1` ノードを選択します。
1. 「プロパティ」タブで、**タイトル**&#x200B;プロパティの値を `List Children` に変更します。

   ![chlimage_1-42](assets/chlimage_1-42.png)

1. tab1 ノードを選択し、作成／ノードを作成をクリックし、次のプロパティ値を入力して、「OK」をクリックします。

   * 名前：items
   * タイプ：cq:WidgetCollection

   ![screen_shot_2012-03-07at51018pm](assets/screen_shot_2012-03-07at51018pm.png)

1. 次のプロパティ値を使用して、items ノードの下にノードを作成します。

   * 名前：listroot
   * タイプ：cq:Widget

   ![screen_shot_2012-03-07at51031pm](assets/screen_shot_2012-03-07at51031pm.png)

1. listroot ノードのプロパティを追加して、テキストフィールドとして設定します。以下の表の行は、それぞれプロパティを表します。完了したら、「すべて保存」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | fieldLabel | 文字列 | リストルートのパス |
   | name | 文字列 | 。/listroot |
   | xtype | 文字列 | textfield |

   ![screen_shot_2012-03-07at51433pm](assets/screen_shot_2012-03-07at51433pm.png)

#### contentpage コンポーネントへのリストの子の追加 {#including-list-children-in-the-contentpage-component}

contentpage コンポーネントに listchildren コンポーネントを組み込むには、次の手順に従います。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` の下の `left.jsp` ファイルを開いて、以下のコードを見つけます（4 行目）。

   ```xml
   <div>newslist</div>
   ```

1. そのコードを次のコードに置き換えます。

   ```xml
   <cq:include path="newslist" resourceType="mywebsite/components/listchildren" />
   ```

1. 変更内容を保存します。

#### ページ内のリストの子の表示 {#viewing-list-children-in-a-page}

このコンポーネントの完全な操作を確認するには、製品ページを表示します。

* 親ページ（「リストルートのパス」）が定義されていない場合。
* 親ページ（「リストルートのパス」）が定義されている場合。

1. ブラウザーで製品ページをリロードします。listchildren コンポーネントは次のように表示されます。

   ![chlimage_1-43](assets/chlimage_1-43.png)

1. ![chlimage_1-44](assets/chlimage_1-44.png)

1. 「リストルートのパス」に、`/content/mywebsite/en` と入力します。「OK」をクリックします。ページ上の listchildren コンポーネントは次のようになります。

   ![chlimage_1-45](assets/chlimage_1-45.png)

### ロゴコンポーネントの作成 {#creating-the-logo-component}

会社のロゴを表示し、サイトのホームページへのリンクを提供するコンポーネントを作成します。コンポーネントにはデザインモードのダイアログが含まれ、プロパティの値はサイトデザイン（/etc/designs/mywebsite）に格納されます。

* プロパティの値は、デザインを使用するページに追加されるコンポーネントのすべてのインスタンスに適用されます。
* プロパティは、デザインを使用するページ上にある任意のコンポーネントのインスタンスを使用して設定できます。

デザインモードダイアログには、画像とリンクパスを設定するためのプロパティが含まれています。ロゴコンポーネントは、web サイトのすべてのページの左上に配置されます。

完了したら、次のようになります。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Adobe Experience Manager は、より充実した機能を持つロゴコンポーネント（`/libs/foundation/components/logo`）を提供します。

#### ロゴコンポーネントノードの作成 {#creating-the-logo-component-node}

ロゴコンポーネントを作成するには、次の手順に従います。

1. CRXDE Lite で、/apps/mywebsite/components を右クリックして、**作成**／**コンポーネントを作成**&#x200B;をクリックします。
1. コンポーネントを作成ダイアログで、以下のプロパティ値を入力して「次へ」をクリックします。

   * ラベル: `logo`.
   * タイトル: `My Logo Component`.
   * 説明: `This is My Logo Component`.

1. ダイアログの最後のパネルにまで「次へ」をクリックして、「**OK**」をクリックします。

#### ロゴスクリプトの作成 {#creating-the-logo-script}

この節では、ホームページへのリンクを含むロゴ画像を表示するスクリプトを作成する方法について説明します。

1. CRXDE Lite で、`/apps/mywebsite/components/logo` の下の `logo.jsp` ファイルを開きます。
1. 以下のコードでは、サイトのホームページへのリンクが作成され、ロゴイメージへの参照が追加されます。このコードを `logo.jsp` にコピーします。

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.text.Text,
                      com.day.cq.wcm.foundation.Image,
                      com.day.cq.commons.Doctype" %><%
       /* obtain the path for home */
       long absParent = currentStyle.get("absParent", 2L);
       String home = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);
       /* obtain the image */
       Resource res = currentStyle.getDefiningResource("imageReference");
       if (res == null) {
           res = currentStyle.getDefiningResource("image");
       }
       /* if no image use text link, otherwise draw the image */
       %>
   <a href="<%= home %>.html"><%
       if (res == null) {
           %>Home<%
       } else {
           Image img = new Image(res);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out);
       }
       %></a>
   ```

1. 変更内容を保存します。

#### ロゴデザインダイアログの作成 {#creating-the-logo-design-dialog}

デザインモードでロゴコンポーネントを設定するためのダイアログを作成します。デザインモードのダイアログには、`design_dialog` という名前を付ける必要があります。

1. logo コンポーネントの下に dialog ノードを作成します。

   1. `/apps/mywebsite/components/logo` ノードを右クリックして、**作成**／**ダイアログを作成**&#x200B;をクリックします。

   1. 以下のプロパティ値を入力して「OK」をクリックします。

      * **ラベル：** `design_dialog`

      * **タイトル:** `Logo (Design)`

1. design_dialog ブランチの tab1 ノードを右クリックして「削除」をクリックします。「すべて保存」をクリックします。
1. `design_dialog/items/items` ノードの下に、`cq:Widget` タイプの `img` という名前のノードを作成します。次のプロパティを追加し、「すべて保存」をクリックします。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | fileNameParameter | 文字列 | 。/imageName |
   | fileReferenceParameter | 文字列 | 。/imageReference |
   | name | 文字列 | 。/画像 |
   | title | String | 画像 |
   | xtype | 文字列 | html5smartimage |

   ![chlimage_1-47](assets/chlimage_1-47.png)

#### ロゴレンダリングスクリプトの作成 {#creating-the-logo-render-script}

ロゴイメージを取得してページに書き込むスクリプトを作成します。

1. ロゴコンポーネントノードを右クリックし、作成／ファイルを作成をクリックして、img.GET.java という名前のスクリプトファイルを作成します。
1. ファイルを開き、次のコードをファイルにコピーして、「すべて保存」をクリックします。

```java
package apps.mywebsite.components.logo;

import java.io.IOException;
import java.io.InputStream;

import javax.jcr.RepositoryException;
import javax.jcr.Property;
import javax.servlet.http.HttpServletResponse;

import com.day.cq.wcm.foundation.Image;
import com.day.cq.wcm.commons.RequestHelper;
import com.day.cq.wcm.commons.WCMUtils;
import com.day.cq.wcm.commons.AbstractImageServlet;
import com.day.cq.commons.SlingRepositoryException;
import com.day.image.Layer;
import org.apache.commons.io.IOUtils;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ValueMap;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

/**
 * Renders an image
 */
public class img_GET extends AbstractImageServlet {

    protected Layer createLayer(ImageContext c)
            throws RepositoryException, IOException {
        /* do not create the layer yet. handle everything later */
        return null;
    }

    protected void writeLayer(SlingHttpServletRequest req,
                              SlingHttpServletResponse resp,
                              ImageContext c, Layer layer)
            throws IOException, RepositoryException {

        Image image = new Image(c.resource);
        image.setItemName(Image.NN_FILE, "image");
        image.setItemName(Image.PN_REFERENCE, "imageReference");
        if (!image.hasContent()) {
            resp.sendError(HttpServletResponse.SC_NOT_FOUND);
            return;
        }
        /* get pure layer */
        layer = image.getLayer(false, false, false);

        /* do not re-encode layer, just spool */
        Property data = image.getData();
        InputStream in = data.getStream();
        resp.setContentLength((int) data.getLength());
        String contentType = image.getMimeType();
        if (contentType.equals("application/octet-stream")) {
            contentType=c.requestImageType;
        }
        resp.setContentType(contentType);
        IOUtils.copy(in, resp.getOutputStream());
        in.close();

        resp.flushBuffer();
    }
}
```

#### contentpage コンポーネントへのロゴコンポーネントの追加 {#adding-the-logo-component-to-the-contentpage-component}

1. CRXDE Liteで `/apps/mywebsite/components/contentpage file` の下にある `left.jsp` を開き、次のコード行を探します。

   ```xml
   <div>logo</div>
   ```

1. そのコードを次のコード行に置き換えます。

   ```xml
   <cq:include path="logo" resourceType="mywebsite/components/logo" />
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。ロゴは以下のようになりますが、現時点では基になるリンクのみが表示されます。

   ![chlimage_1-48](assets/chlimage_1-48.png)

#### ページ内でのロゴ画像の設定 {#setting-the-logo-image-in-a-page}

この節では、デザインモードダイアログを使用して画像をロゴとして設定する方法について説明します。

1. ブラウザーで製品ページを開き、サイドキックの下部にある「デザイン」ボタンをクリックして、デザインモードに入ります。

   ![正方形で示される「デザイン」ボタン。](do-not-localize/chlimage_1-1.png)

1. ロゴバーのデザインで、「編集」をクリックし、ダイアログを使用してロゴコンポーネントの設定を編集します。
1. ダイアログで、「画像」タブのパネル内をクリックし、mywebsite.zip ファイルから抽出した logo.png 画像を参照して「OK」をクリックします。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. サイドキックタイトルバーの三角形をクリックして編集モードに戻ります。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. CRXDE Lite で、以下のノードに移動して、格納されているプロパティ値を確認します。

   `/etc/designs/mywebsite/jcr:content/contentpage/logo`

### パンくずコンポーネントの取り込み {#including-the-breadcrumb-component}

この節では、基盤コンポーネントの 1 つであるパンくず（trail）コンポーネントを含めます。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` を参照し、`center.jsp` ファイルを開いて次と置換します。

   ```java
   <div>trail</div>
   ```

   以下に置き換えます。

   ```xml
   <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
   ```

1. 変更を保存します。
1. ブラウザーで **Products 1** ページをリロードします。trail コンポーネントは次のようになります。

   ![chlimage_1-50](assets/chlimage_1-50.png)

### タイトルコンポーネントの取り込み {#including-the-title-component}

この節では、基盤コンポーネントの 1 つであるタイトルコンポーネントを含めます。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` を参照し、`center.jsp` ファイルを開いて次と置換します。

   ```xml
   <div>title</div>
   ```

   以下に置き換えます。

   ```xml
   <cq:include path="title" resourceType="foundation/components/title" />
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。タイトルコンポーネントは次のようになります。

   ![chlimage_1-51](assets/chlimage_1-51.png)

   **注意**：編集モードで別のタイトルおよびタイプ／サイズを設定できます。

### 段落システムコンポーネントの取り込み {#including-the-paragraph-system-component}

段落システム（parsys）は、段落のリストを管理する web サイトの重要な部分です。作成者は、これを使用して、ページに段落コンポーネントを追加し、構造を提供できます。

parsys コンポーネント（基盤コンポーネントの 1 つ）を contentpage コンポーネントに追加します。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` を参照し、`center.jsp` ファイルを開いて以下のコード行を見つけます。

   ```xml
   <div>parsys</div>
   ```

1. このコード行を以下のコードに置き換えて、変更内容を保存します。

   ```xml
   <cq:include path="par" resourceType="foundation/components/parsys" />
   ```

1. ブラウザーで、Products ページを更新します。parsys コンポーネントが以下のように表示されます。

   ![chlimage_1-52](assets/chlimage_1-52.png)

### 画像コンポーネントの作成 {#creating-the-image-component}

段落システムに画像を表示するコンポーネントを作成します。時間を節約するために、画像コンポーネントはロゴコンポーネントのコピーとして作成され、いくつかのプロパティの変更が加えられます。

>[!NOTE]
>
>Adobe Experience Manager は、より充実した機能を持つ画像コンポーネント（`/libs/foundation/components/image`）を提供します。

#### 画像コンポーネントの作成 {#creating-the-image-component-1}

1. `/apps/mywebsite/components/logo` ノードを右クリックして、「コピー」をクリックします。
1. `/apps/mywebsite/components` ノードを右クリックして、「貼り付け」をクリックします。
1. `Copy of logo` ノードを右クリックし、「名前を変更」をクリックして既存のテキストを削除し、`image` と入力します。

1. `image` コンポーネントノードを選択して、以下のプロパティ値を変更します。

   * `jcr:title:`：自分の画像コンポーネント
   * `jcr:description`：これは自分の画像コンポーネントです。

1. 以下のプロパティ値を使用して、`image` ノードにプロパティを追加します。

   * 名前：componentGroup
   * タイプ：String
   * 値：MyWebsite

1. `image` ノードの下で、`design_dialog` ノードの名前を `dialog` に変更します。

1. `logo.jsp` を `image.jsp.` に名前を変更します。

1. img.GET.java を開いて、パッケージを `apps.mywebsite.components.image` に変更します。

![chlimage_1-53](assets/chlimage_1-53.png)

#### 画像スクリプトの作成 {#creating-the-image-script}

この節では、画像スクリプトを作成する方法について説明します。

1. 次を開きます： `/apps/mywebsite/components/image/` `image.jsp`
1. 既存のコードを次のコードに置き換えてから、変更内容を保存します。

   ```xml
   <%@include file="/libs/foundation/global.jsp"%><%
   %><%@ page import="com.day.cq.commons.Doctype,
                       com.day.cq.wcm.foundation.Image,
                       com.day.cq.wcm.api.components.DropTarget,
                       com.day.cq.wcm.api.components.EditConfig,
                       com.day.cq.wcm.commons.WCMUtils" %><%
    /* global.jsp provides access to the current resource through the resource object */
           Image img = new Image(resource);
           img.setItemName(Image.NN_FILE, "image");
           img.setItemName(Image.PN_REFERENCE, "imageReference");
           img.setSelector("img");
           img.setDoctype(Doctype.fromRequest(request));
           img.setAlt("Home");
           img.draw(out); %>
   ```

1. 変更内容を保存します。

#### 画像 cq:editConfig ノードの作成 {#creating-the-image-cq-editconfig-node}

`cq:editConfig` ノードタイプを使用すると、プロパティを編集するときに、コンポーネントの一定の動作を設定できます。

この節では、cq:editConfig ノードを使用して、コンテンツファインダーから画像コンポーネントにアセットをドラッグできます。

1. CRXDE Lite の /apps/mywebsite/components/image ノードの下に、次のようにノードを作成します。

   * 名前：cq:editConfig.
   * タイプ：cq:EditConfig.

1. cq:editConfig ノードの下に、次のようにノードを作成します。

   * 名前：cq:dropTargets.
   * タイプ：cq:DropTargetConfig.

1. cq:dropTargets ノードの下に、次のようにノードを作成します。

   * 名前：画像
   * 型：nt:unstructured.

1. CRXDE で、プロパティを次のように設定します。

| 名前 | タイプ | 値 |
|---|---|---|
| 同意 | 文字列 | image/（gif\|jpeg\|png） |
| グループ | 文字列 | media |
| propertyName | 文字列 | 。/imageReference |

![chlimage_1-54](assets/chlimage_1-54.png)

#### アイコンの追加 {#adding-the-icon}

この節では、画像コンポーネントがサイドキックに一覧表示される際に画像コンポーネントの横に表示されるアイコンを追加します。

1. CRXDE Lite で `/libs/foundation/components/image/icon.png` ファイルを右クリックして「**コピー**」を選択します。
1. `/apps/mywebsite/components/image` ノードを右クリックして「**貼り付け**」をクリックし、「**すべて保存**」をクリックします。

#### 画像コンポーネントの使用 {#using-the-image-component}

ここでは、**製品**&#x200B;ページを表示して、段落システムに画像コンポーネントを追加します。

1. ブラウザーで&#x200B;**製品**&#x200B;ページをリロードします。
1. サイドキックで、**デザインモード**&#x200B;アイコンをクリックします。
1. 「編集」ボタンをクリックして、par のデザインダイアログを編集します。
1. ダイアログで、**許可されたコンポーネント**&#x200B;のリストが表示されます。**MyWebsite**&#x200B;に移動して、「**マイ画像コンポーネント**」を選択し、「**OK**」をクリックします。
1. **編集モードに戻ります。**
1. parsys フレーム（**コンポーネントまたはアセットをここにドラッグ**）をダブルクリックします。**新規コンポーネントを挿入**&#x200B;および&#x200B;**サイドキック**&#x200B;セレクターは次のようになります。

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

### ツールバーコンポーネントを含める {#including-the-toolbar-component}

この節では、基盤コンポーネントの 1 つであるツールバーコンポーネントを含めます。

デザインモードに加えて、編集モードにも複数のオプションがあります。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` に移動し、`body.jsp` ファイルを開いて以下のコードを見つけます。

   ```java
   <div class="toolbar">toolbar</div>
   ```

1. このコードを以下のコードに置き換えて、変更内容を保存します。

   ```java
   <cq:include path="toolbar" resourceType="foundation/components/toolbar"/>
   ```

1. AEM web サイトページのフォルダーツリーで、Websites／My Website／English を選択し、新規／新しいページをクリックします。次のプロパティ値を指定し、「作成」をクリックします。

   * タイトル：ツールバー
   * 「マイ web サイトコンテンツページテンプレート」を選択します。

1. ページのリストで、ツールバーページを右クリックし、「プロパティ」をクリックします。「ナビゲーション内で非表示にする」を選択し、「OK」をクリックします。

   「ナビゲーション内で非表示にする」オプションを使用すると、topnav や listchildren などのナビゲーションコンポーネントにページが表示されなくなります。

1. ツールバーの下に、次のページを作成します。

   * 連絡先
   * フィードバック
   * ログイン
   * 検索

1. ブラウザーで製品ページをリロードします。次のようなコンソールが表示されます。

   ![chlimage_1-55](assets/chlimage_1-55.png)

### 検索コンポーネントの作成 {#creating-the-search-component}

この節では、web サイト上のコンテンツを検索するためのコンポーネントを作成します。この検索コンポーネントは、任意のページの段落システム（特殊な検索結果ページなど）に配置できます。

完了したら、検索入力ボックスは、**英語**&#x200B;のページに以下のように表示されます。

![chlimage_1-56](assets/chlimage_1-56.png)

#### 検索コンポーネントの作成 {#creating-the-search-component-1}

1. CRXDE Lite で `/apps/mywebsite/components` を右クリックして、**作成**／**コンポーネントを作成**&#x200B;をクリックします。
1. ダイアログを使用してコンポーネントを設定します。

   1. 最初のパネルで、次のプロパティ値を指定します。

      * ラベル：検索
      * タイトル：自分の検索コンポーネント
      * 説明：これは自分の検索コンポーネントです。
      * グループ：MyWebsite

   1. 「次へ」をクリックしてから、再度「次へ」をクリックします。
   1. 許可された親パネルで、「+」ボタンをクリックして `*/parsys` と入力します。
   1. 「次へ」をクリックして「OK」をクリックします。

1. 「すべて保存」をクリックします。
1. 次のノードをコピーし、apps/mywebsite/components/search ノードに貼り付けます。

   * `/libs/foundation/components/search/dialog`
   * &grave;&grave; `/libs/foundation/components/search/i18n`

   * `/libs/foundation/components/search/icon.png`

1. 「すべて保存」をクリックします。

#### 検索スクリプトの作成 {#creating-the-search-script}

ここでは、検索スクリプトを作成する方法について説明します。

1. `/apps/mywebsite/components/search/search.jsp` ファイルを開きます。
1. 以下のコードを `search.jsp` にコピーします。

   ```java
   <%@ page import="com.day.cq.wcm.foundation.Search,com.day.cq.tagging.TagManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   %><cq:setContentBundle/><%
       Search search = new Search(slingRequest);
   
       String searchIn = (String) properties.get("searchIn");
       String requestSearchPath = request.getParameter("path");
       if (searchIn != null) {
           /* only allow the "path" request parameter to be used if it
            is within the searchIn path configured */
           if (requestSearchPath != null && requestSearchPath.startsWith(searchIn)) {
               search.setSearchIn(requestSearchPath);
           } else {
               search.setSearchIn(searchIn);
           }
       } else if (requestSearchPath != null) {
           search.setSearchIn(requestSearchPath);
       }
   
       pageContext.setAttribute("search", search);
       TagManager tm = resourceResolver.adaptTo(TagManager.class);
   %><c:set var="trends" value="${search.trends}"/><%
   %><center>
     <form action="${currentPage.path}.html">
       <input size="41" maxlength="2048" name="q" value="${fn:escapeXml(search.query)}"/>
       <input value="<fmt:message key="searchButtonText"/>" type="submit" />
     </form>
   </center>
   <br/>
   <c:set var="result" value="${search.result}"/>
   <c:choose>
     <c:when test="${empty result && empty search.query}">
     </c:when>
     <c:when test="${empty result.hits}">
       <c:if test="${result.spellcheck != null}">
         <p><fmt:message key="spellcheckText"/> <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${result.spellcheck}"/></c:url>"><b><c:out value="${result.spellcheck}"/></b></a></p>
       </c:if>
       <fmt:message key="noResultsText">
         <fmt:param value="${fn:escapeXml(search.query)}"/>
       </fmt:message>
     </c:when>
     <c:otherwise>
       <p class="searchmeta">Results ${result.startIndex + 1} - ${result.startIndex + fn:length(result.hits)} of ${result.totalMatches} for <b>${fn:escapeXml(search.query)}</b>. (${result.executionTime} seconds)</p>
      <br/>
   
     <div class="searchresults">
       <div class="results">
         <c:forEach var="hit" items="${result.hits}" varStatus="status">
           <div class="hit">
           <a href="${hit.URL}">${hit.title}</a>
           <div class="excerpt">${hit.excerpt}</div>
          <div class="hiturl"> ${hit.URL}<c:if test="${!empty hit.properties['cq:lastModified']}"> - <c:catch><fmt:formatDate value="${hit.properties['cq:lastModified'].time}" dateStyle="medium"/></c:catch></c:if> - <a href="${hit.similarURL}"><fmt:message key="similarPagesText"/></a>
           </div></div>
         </c:forEach>
       </div>
         <br/>
   
        <div class="searchRight">
             <c:if test="${fn:length(trends.queries) > 0}">
                 <p><fmt:message key="searchTrendsText"/></p>
                 <div class="searchTrends">
                     <c:forEach var="query" items="${trends.queries}">
                         <a href="<c:url value="${currentPage.path}.html"><c:param name="q" value="${query.query}"/></c:url>"><span style="font-size:${query.size}px"><c:out value="${query.query}"/></code></a>
                     </c:forEach>
                 </div>
             </c:if>
             <c:if test="${result.facets.languages.containsHit}">
                 <p>Languages</p>
                 <c:forEach var="bucket" items="${result.facets.languages.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value='<%= new java.util.Locale((String) pageContext.getAttribute("bucketValue")).getDisplayLanguage(request.getLocale()) %>'/>
                     <c:choose>
                         <c:when test="${param.language != null}">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.tags.containsHit}">
                 <p>Tags</p>
                 <c:forEach var="bucket" items="${result.facets.tags.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="tag" value="<%= tm.resolve((String) pageContext.getAttribute("bucketValue")) %>"/>
                     <c:if test="${tag != null}">
                         <c:set var="label" value="${tag.title}"/>
                         <c:choose>
                             <c:when test="<%= request.getParameter("tag") != null && java.util.Arrays.asList(request.getParameterValues("tag")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="tag" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                             <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="tag" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                         </c:choose><br/>
                     </c:if>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.mimeTypes.containsHit}">
                 <jsp:useBean id="fileTypes" class="com.day.cq.wcm.foundation.FileTypes"/>
                 <p>File types</p>
                 <c:forEach var="bucket" items="${result.facets.mimeTypes.buckets}">
                     <c:set var="bucketValue" value="${bucket.value}"/>
                     <c:set var="label" value="${fileTypes[bucket.value]}"/>
                     <c:choose>
                         <c:when test="<%= request.getParameter("mimeType") != null && java.util.Arrays.asList(request.getParameterValues("mimeType")).contains(pageContext.getAttribute("bucketValue")) %>">${label} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:addParam name="mimeType" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
             <c:if test="${result.facets.lastModified.containsHit}">
                 <p>Last Modified</p>
                 <c:forEach var="bucket" items="${result.facets.lastModified.buckets}">
                     <c:choose>
                         <c:when test="${param.from == bucket.from && param.to == bucket.to}">${bucket.value} (${bucket.count}) - <a href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/></cq:requestURL>">remove filter</a></c:when>
                         <c:otherwise><a title="filter results" href="<cq:requestURL><cq:removeParam name="from"/><cq:removeParam name="to"/><c:if test="${bucket.from != null}"><cq:addParam name="from" value="${bucket.from}"/></c:if><c:if test="${bucket.to != null}"><cq:addParam name="to" value="${bucket.to}"/></c:if></cq:requestURL>">${bucket.value} (${bucket.count})</a></c:otherwise>
                     </c:choose><br/>
                 </c:forEach>
             </c:if>
   
         <c:if test="${fn:length(search.relatedQueries) > 0}">
   
          <br/><br/><div class="related">
           <fmt:message key="relatedSearchesText"/>
           <c:forEach var="rq" items="${search.relatedQueries}">
               <a href="${currentPage.path}.html?q=${rq}"><c:out value="${rq}"/></a>
           </c:forEach></div>
         </c:if>
         </div>
   
         <c:if test="${fn:length(result.resultPages) > 1}">
           <div class="pagination">
               <fmt:message key="resultPagesText"/>
           <c:if test="${result.previousPage != null}">
             <a href="${result.previousPage.URL}"><fmt:message key="previousText"/></a>
           </c:if>
           <c:forEach var="page" items="${result.resultPages}">
             <c:choose>
               <c:when test="${page.currentPage}">${page.index + 1}</c:when>
               <c:otherwise>
                 <a href="${page.URL}">${page.index + 1}</a>
               </c:otherwise>
             </c:choose>
           </c:forEach>
           <c:if test="${result.nextPage != null}">
             <a href="${result.nextPage.URL}"><fmt:message key="nextText"/></a>
           </c:if>
           </div>
         </c:if>
         </div>
   
     </c:otherwise>
   </c:choose>
   ```

1. 変更内容を保存します。

#### contentpage コンポーネントへの検索ボックスの追加 {#including-a-search-box-in-the-contentpage-component}

contentpage ページの左側のセクションに検索入力ボックスを含めるには、次の手順に従います。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` の下の `left.jsp` ファイルを開いて、以下のコードを見つけます（2 行目）。

   ```xml
   %><div class="left">
   ```

1. その行の&#x200B;**前**&#x200B;に、次のコードを挿入します。

   ```java
   %><%@ page import="com.day.text.Text"%><%
   %><% String docroot = currentDesign.getPath();
   String home = Text.getAbsoluteParent(currentPage.getPath(), 2);%><%
   ```

1. 次のコード行を探します。

   ```xml
   <div>search</div>
   ```

1. このコードを以下のコードに置き換えて、変更内容を保存します。

   ```java
   <div class="form_1">
        <form class="geo" action="<%= home %>/toolbar/search.html" id="form" >
             <p>
                  <input class="geo" type="text" name="q"><br>
                  <a href="<%= home %>/toolbar/search.html" class="link_1">advanced search</a>
             </p>
        </form>
   </div>
   ```

1. ブラウザーで、Products ページを再読み込みします。検索コンポーネントは次のようになります。

   ![chlimage_1-57](assets/chlimage_1-57.png)

#### 検索ページへの検索コンポーネントの追加 {#including-the-search-component-in-the-search-page}

この節では、段落システムに検索コンポーネントを追加します。

1. ブラウザーで検索ページを開きます。
1. サイドキックで、デザインモードアイコンをクリックします。
1. デザインの par ブロック（検索タイトルの下）で、「編集」をクリックします。
1. ダイアログで、下にスクロールして&#x200B;**自分の web サイト**&#x200B;グループを表示し、「**自分の検索コンポーネント**」を選択して「**OK**」をクリックします。
1. サイドキックで、三角形をクリックして編集モードに戻ります。
1. My Search コンポーネントをサイドキックから parsys フレームにドラッグします。次のようなコンソールが表示されます。

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. 製品ページに移動します。入力ボックスに customers と入力して Enter キーを押して検索します。検索ページにリダイレクトされます。プレビューモードに切り替わります。出力は以下のような形式です。

   ![chlimage_1-59](assets/chlimage_1-59.png)

### iparsys コンポーネントの取り込み {#including-the-iparsys-component}

この節では、基盤コンポーネントの 1 つである継承段落システム (iparsys) コンポーネントを含めます。このコンポーネントを使用すると、親ページ上に段落の構造を作成でき、子ページに段落を継承させることができます。

このコンポーネントでは、編集モードとデザインモードの両方で複数のパラメーターを設定できます。

1. CRXDE Lite で `/apps/mywebsite/components/contentpage` に移動し、`right.jsp` ファイルを開いて次と置き換えます。

   ```java
   <div>iparsys</div>
   ```

   以下に置き換えます。

   ```java
   <cq:include path="rightpar" resourceType="foundation/components/iparsys" />
   ```

1. 変更を保存します。
1. ブラウザーで製品ページをリロードします。ページ全体は次のようになります。

   ![chlimage_1-5](assets/chlimage_1-5.jpeg)
