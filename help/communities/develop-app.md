---
title: サンドボックスアプリケーションの開発
description: 基盤スクリプトを使用し、コミュニティコンポーネントを使用したオーサリングを有効にする機能を含むサンドボックスアプリケーションを開発する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 8%

---

# サンドボックスアプリケーションの開発  {#develop-sandbox-application}

このセクションでは、テンプレートが [初期応用](initial-app.md) セクション、および [初期コンテンツ](initial-content.md) 「 」セクションでは、アプリケーションを開発できます。 これを行うには、コミュニティコンポーネントを使用したオーサリングを有効にする機能を含む基盤スクリプトを使用します。 この節の最後に、完全に機能する Web サイトがあります。

## Foundation ページスクリプトの使用 {#using-foundation-page-scripts}

playpage テンプレートをレンダリングするコンポーネントを追加したときに作成されたデフォルトのスクリプトは、基盤ページの head.jsp とローカルの body.jsp を含むように変更されます。

### スーパーリソースタイプ {#super-resource-type}

最初の手順は、リソースのスーパータイププロパティを `/apps/an-scf-sandbox/components/playpage` ノードを継承し、スーパータイプのスクリプトとプロパティを継承します。

CRXDE Lite の使用:

1. ノードを選択 `/apps/an-scf-sandbox/components/playpage`.
1. 「プロパティ」タブで、次の値を持つ新しいプロパティを入力します。

   名前：`sling:resourceSuperType`

   タイプ：`String`

   値：`foundation/components/page`

1. 緑をクリック **[!UICONTROL +追加]** 」ボタンをクリックします。
1. 「**[!UICONTROL すべて保存]**」をクリックします。

   ![page-script](assets/page-script.png)

### head および body スクリプト {#head-and-body-scripts}

1. In **CRXDE Lite** エクスプローラペイン：に移動します。 `/apps/an-scf-sandbox/components/playpage` をクリックし、ファイルをダブルクリックします。 `playpage.jsp` をクリックして、編集ウィンドウで開きます。

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

1. 開く/閉じるスクリプトタグに注意して、「 // TODO ...」を `includes` 頭部と体部の台本の &lt;html>.

   のスーパータイプで `foundation/components/page`の場合、この同じフォルダーに定義されていないスクリプトは、 `/apps/foundation/components/page` フォルダー（存在する場合）、または内のスクリプトに `/libs/foundation/components/page` フォルダー。

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

1. 基盤スクリプトのオーバーレイ `head.jsp` は必要ではありませんが、基盤スクリプトは不要です。 `body.jsp` が空である。

   オーサリング用にを設定するには、オーバーレイ `body.jsp` ローカルスクリプトを使用し、本文に段落システム (parsys) を含めます。

   1. `/apps/an-scf-sandbox/components` に移動します。
   1. `playpage` ノードを選択します。
   1. 右クリックして「 」を選択します。 `Create > Create File...`

      * 名前： **body.jsp**

   1. 「**[!UICONTROL すべて保存]**」をクリックします。

   開く `/apps/an-scf-sandbox/components/playpage/body.jsp` 次のテキストに貼り付けます。

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

**ページを編集モードでブラウザーに表示します。**

* 標準 UI: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

見出しだけが表示されるわけではありません **コミュニティの再生**&#x200B;をクリックします。また、ページコンテンツを編集するための UI も使用します。

アセット/コンポーネントのサイドパネルは、サイドパネルを開くように切り替えたときに表示され、ウィンドウの幅がサイドコンテンツとページコンテンツの両方に十分に広い場合に表示されます。

![view-page](assets/view-page.png)

* クラシック UI：`http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

クラシック UI での再生ページの表示方法を次に示します ( コンテンツファインダー (cf) を含む )。

![play-page-view](assets/play-page-view.png)

## コミュニティコンポーネント {#communities-components}

コミュニティコンポーネントのオーサリングを有効にするには、次の手順に従って開始します。

* [コミュニティコンポーネントへのアクセス](basics.md#accessing-communities-components)

このサンドボックスの目的では、次のものから始めます。 **Communities** コンポーネント（チェックボックスをオンにして有効にします）:

* コメント
* フォーラム
* レーティング
* レビュー
* レビューの概要 (表示)
* 投票

さらに、 **[!UICONTROL 一般]** コンポーネント（例： ）

* 画像
* テーブル
* テキスト
* タイトル (基盤)

>[!NOTE]
>
>ページパーツに対して有効なコンポーネントは、 `components` のプロパティ
>
>ノード `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## ランディングページ {#landing-page}

多言語環境では、ルートページには、クライアントからの要求を解析して優先言語を決定するスクリプトを含めます。

この例では、ルートページは英語のページにリダイレクトするように静的に設定されています。英語のページは、今後、再生ページへのリンクを持つメインランディングページとして開発される可能性があります。

ブラウザー URL をルートページに変更します。 `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* ページ情報アイコンを選択します。
* 選択 **[!UICONTROL プロパティを開く]**
* 「詳細」タブで、

   * リダイレクトエントリの場合は、 **[!UICONTROL Web サイト]** > **[!UICONTROL SCF サンドボックスサイト]** > **[!UICONTROL SCF サンドボックス]**
   * クリック **[!UICONTROL OK]**

* クリック **[!UICONTROL OK]**

サイトが公開された後、パブリッシュインスタンス上のルートページを参照すると、英語のページにリダイレクトされます。

コミュニティ SCF コンポーネントを再生する前の最後の手順は、クライアントライブラリフォルダー (clientlibs) を追加することです.... [clientlib の追加](add-clientlibs.md)
