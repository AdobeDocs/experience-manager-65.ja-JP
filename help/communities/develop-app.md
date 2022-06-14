---
title: サンドボックスアプリケーションの開発
seo-title: Develop Sandbox Application
description: 基盤スクリプトによるアプリケーションの開発
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 49%

---

# サンドボックスアプリケーションの開発  {#develop-sandbox-application}

[初期アプリケーション](initial-app.md)の節でテンプレートをセットアップし、[初期コンテンツ](initial-content.md)の節で初期ページを設定したので、ここでは、作成時にコミュニティコンポーネントを使用できるようにするとともに、基盤スクリプトを使用してアプリケーションを開発できます。この節の最後に、Web サイトが機能するようになります。

## 基盤ページスクリプトの使用 {#using-foundation-page-scripts}

デフォルトのスクリプトは、playpage テンプレートをレンダリングするコンポーネントを追加したときに作成されましたが、このスクリプトを変更して、基盤ページの head.jsp およびローカルの body.jsp を含めます。

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

1. スクリプトの開始／終了タグに注意して、「// TODO ...」の代わりに、&lt;html> のヘッダーと本文部分のスクリプトを含めます。

   スーパータイプが `foundation/components/page`を指定した場合、この同じフォルダーに定義されていないスクリプトは、 `/apps/foundation/components/page` フォルダー（存在する場合）、それ以外の場合は `/libs/foundation/components/page` フォルダー。

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

   オーサリング用に設定するには、オーバーレイ `body.jsp` ローカルスクリプトを使用し、本文に段落システム (parsys) を含めます。

   1. `/apps/an-scf-sandbox/components` に移動します。
   1. `playpage` ノードを選択します。
   1. 右クリックして「 」を選択します。 `Create > Create File...`

      * 名前：**body.jsp**
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

見出しだけが表示されるわけではありません **コミュニティプレイ**&#x200B;をクリックします。また、ページコンテンツを編集するための UI も使用します。

サイドパネルが開くように切り替え、ウィンドウがサイドコンテンツとページコンテンツの両方を表示するのに十分な大きさである場合、アセット／コンポーネントサイドパネルが表示されます。

![view-page](assets/view-page.png)

* クラシック UI：`http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

クラシック UI での再生ページの表示方法を次に示します ( コンテンツファインダー (cf) を含む )。

![play-page-view](assets/play-page-view.png)

## コミュニティコンポーネント {#communities-components}

オーサリング用にコミュニティコンポーネントを使用できるようにするには、まず、次の指示に従ってください。

* [コミュニティコンポーネントへのアクセス](basics.md#accessing-communities-components)

このサンドボックスでは、次の&#x200B;**コミュニティ**&#x200B;コンポーネントから開始します（チェックボックスをオンにして有効にします）。

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
>ページパーツに対して有効なコンポーネントは、 `components` プロパティ
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.

## ランディングページ {#landing-page}

多言語環境では、クライアントからの要求を解析して優先言語を特定するスクリプトがルートページに含まれます。

この簡単な例では、ルートページは英語のページにリダイレクトするように静的に設定されています。将来、英語は再生ページへのリンクを持つメインランディングページとして開発される可能性があります。

ブラウザー URL をルートページに変更します。 `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* ページ情報アイコンを選択します。
* 選択 **[!UICONTROL プロパティを開く]**
* 「詳細」タブで、

   * リダイレクトエントリの場合は、 **[!UICONTROL Web サイト]** > **[!UICONTROL SCF サンドボックスサイト]** > **[!UICONTROL SCF サンドボックス]**
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL OK]**」をクリックします。

サイトを公開した後、パブリッシュインスタンスでルートページを参照すると、英語のページにリダイレクトされます。

コミュニティの SCF コンポーネントを使用する前の最後の手順は、クライアントライブラリフォルダー (clientlibs) を追加することです。. [clientlibs を追加](add-clientlibs.md)
