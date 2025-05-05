---
title: サンドボックスアプリケーションの開発
description: 基盤スクリプトを使用し、Communities コンポーネントでのオーサリングを有効にする機能を含む、サンドボックスアプリケーションの開発方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 6%

---

# サンドボックスアプリケーションの開発  {#develop-sandbox-application}

この節では、テンプレートを「初期アプリケーション [」セクションで設定し、「初期コンテンツ ](initial-app.md)」セクションで設定した初期ページで設定したので、アプリケーションを開発でき [&#128279;](initial-content.md) す。 それには、Communities コンポーネントでのオーサリングを有効にする機能を含む、基盤スクリプトを使用します。 この節の最後では、完全に機能する web サイトがあります。

## 基盤ページスクリプトの使用 {#using-foundation-page-scripts}

再生ページテンプレートをレンダリングするコンポーネントを追加すると作成されるデフォルトのスクリプトは、基盤ページの head.jsp とローカルの body.jsp を含むように変更されます。

### スーパーリソースタイプ {#super-resource-type}

最初の手順では、リソースのスーパータイプのプロパティを `/apps/an-scf-sandbox/components/playpage` ノードに追加して、スーパータイプのスクリプトとプロパティを継承するようにします。

CRXDE Liteの使用：

1. ノード `/apps/an-scf-sandbox/components/playpage` を選択します。
1. 「プロパティ」タブで、次の値を持つ新しいプロパティを入力します。

   名前：`sling:resourceSuperType`

   タイプ：`String`

   値：`foundation/components/page`

1. 緑の「**[!UICONTROL +追加]**」ボタンをクリックします。
1. 「**[!UICONTROL すべて保存]**」をクリックします。

   ![ ページスクリプト ](assets/page-script.png)

### head スクリプトと body スクリプト {#head-and-body-scripts}

1. **CRXDE Lite** エクスプローラーウィンドウで、`/apps/an-scf-sandbox/components/playpage` に移動し、ファイル `playpage.jsp` をダブルクリックして編集ウィンドウで開きます。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. スクリプトタグを開く/閉じることを考慮して、「// TODO ...」を &lt;html> の head 部分と body 部分のスクリプトの `includes` に置き換えます。

   スーパータイプが `foundation/components/page` の場合、この同じフォルダーで定義されていないスクリプトは、`/apps/foundation/components/page` のフォルダー内のスクリプト（存在する場合）、または `/libs/foundation/components/page` のフォルダー内のスクリプトに解決されます。

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. 基盤スクリプト `head.jsp` をオーバーレイする必要はありませんが、基盤スクリプト `body.jsp` は空です。

   オーサリング用にを設定するには、`body.jsp` をローカルスクリプトでオーバーレイし、本文に段落システム（parsys）を含めます。

   1. `/apps/an-scf-sandbox/components` に移動します。
   1. `playpage` ノードを選択します。
   1. 右クリックして「`Create > Create File...`」を選択します。

      * 名前：**body.jsp**

   1. 「**[!UICONTROL すべて保存]**」をクリックします。

   `/apps/an-scf-sandbox/components/playpage/body.jsp` を開いて、次のテキストを貼り付けます。

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. 「**[!UICONTROL すべて保存]**」をクリックします。

**ページをブラウザーで編集モードで表示します。**

* 標準 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

見出し **コミュニティプレイ** だけでなく、ページコンテンツを編集するための UI も表示されます。

Assets/コンポーネントのサイドパネルは、両方のサイドパネルが開き換えられ、サイドコンテンツとページコンテンツの両方が表示されるほどウィンドウの幅が広い場合に表示されます。

![view-page](assets/view-page.png)

* クラシック UI：`http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

コンテンツファインダー（cf）を含むクラシック UI での再生ページの表示方法を次に示します。

![play-page-view](assets/play-page-view.png)

## コミュニティコンポーネント {#communities-components}

Communities コンポーネントをオーサリング用に有効にするには、まず次の手順に従います。

* [Communities コンポーネントへのアクセス](basics.md#accessing-communities-components)

このサンドボックスでは、まず次の **Communities** コンポーネントを使用します（チェックボックスをオンにして有効にします）。

* コメント
* フォーラム
* レーティング
* レビュー
* レビューの概要 (表示)
* 投票

さらに、次のような **[!UICONTROL 一般]** コンポーネントを選択します

* 画像
* テーブル
* テキスト
* タイトル （基盤）

>[!NOTE]
>
>ページ par に対して有効なコンポーネントは、の `components` プロパティの値としてリポジトリに格納されます。
>
>ノード `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`。

## ランディングページ {#landing-page}

多言語環境では、ルートページには、クライアントからのリクエストを解析して優先言語を決定するスクリプトが含まれます。

この例では、ルートページは英語ページにリダイレクトするように静的に設定されています。英語ページは今後開発される可能性があり、再生ページへのリンクを含むメインランディングページになります。

ブラウザーの URL をルートページに変更します。`http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* 「ページ情報」アイコンを選択します
* 「**[!UICONTROL プロパティを開く]**」を選択します。
* 「詳細」タブで、次の設定を行います

   * リダイレクトエントリについては、**[!UICONTROL Web サイト]**/**[!UICONTROL SCF サンドボックスサイト]**/**[!UICONTROL SCF サンドボックス]** を参照します。
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL OK]**」をクリックします。

サイトが公開されると、パブリッシュインスタンス上のルートページを参照すると、英語のページにリダイレクトされます。

Communities SCF コンポーネントを使用する前の最後の手順は、クライアントライブラリフォルダー（clientlibs）....を追加することです [Clientlibs の追加 ](add-clientlibs.md)
