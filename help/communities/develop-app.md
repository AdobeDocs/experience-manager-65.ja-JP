---
title: サンドボックスアプリケーションの開発
seo-title: サンドボックスアプリケーションの開発
description: 基盤スクリプトによるアプリケーションの開発
seo-description: 基盤スクリプトによるアプリケーションの開発
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: d0b333ffa6cad4841e70e652328e92554fb2a7a1
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 51%

---


# サンドボックスアプリケーションの開発  {#develop-sandbox-application}

[初期アプリケーション](initial-app.md)の節でテンプレートをセットアップし、[初期コンテンツ](initial-content.md)の節で初期ページを設定したので、ここでは、作成時にコミュニティコンポーネントを使用できるようにするとともに、基盤スクリプトを使用してアプリケーションを開発できます。この節の最後に、Webサイトが機能するようになります。

## 基盤ページスクリプトの使用 {#using-foundation-page-scripts}

デフォルトのスクリプトは、playpage テンプレートをレンダリングするコンポーネントを追加したときに作成されましたが、このスクリプトを変更して、基盤ページの head.jsp およびローカルの body.jsp を含めます。

### スーパーリソースタイプ {#super-resource-type}

The first step is to add a resource super type property to the `/apps/an-scf-sandbox/components/playpage` node so that it inherits the scripts and properties of the super type.

CRXDE Lite を使用して、次の手順を実行します。

1. ノードを選択 `/apps/an-scf-sandbox/components/playpage`します。
1. 「プロパティ」タブで、次の値を持つ新しいプロパティを入力します。

   名前：`sling:resourceSuperType`

   型：`String`

   値：`foundation/components/page`

1. Click the green **[!UICONTROL +Add]** button.
1. 「**[!UICONTROL すべて保存]**」をクリックします。

   ![chlimage_1-231](assets/chlimage_1-231.png)

### Head and body scripts {#head-and-body-scripts}

1. **CRXDE Lite** Explorerウィンドウで、ファイルに移動し `/apps/an-scf-sandbox/components/playpage` 、重複を押しながらクリックして、編集ウィンドウ `playpage.jsp` で開きます。

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

   With a super type of `foundation/components/page`, any script not defined in this same folder will resolve to a script in `/apps/foundation/components/page` folder (if it exists), else to a script in `/libs/foundation/components/page` folder.

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

   To setup for authoring, overlay `body.jsp` with a local script and include a paragraph system (parsys) in the body:

   1. `/apps/an-scf-sandbox/components` に移動します。
   1. Select the `playpage` node.
   1. Right-click and select `Create > Create File...`

      * 名前：**body.jsp**
   1. 「**[!UICONTROL すべて保存]**」をクリックします。

   Open `/apps/an-scf-sandbox/components/playpage/body.jsp` and paste in the following text:

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

* 標準 UI：[http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

You should not only see the heading **Community Play**, but also the UI for editing page content.

サイドパネルが開くように切り替え、ウィンドウがサイドコンテンツとページコンテンツの両方を表示するのに十分な大きさである場合、アセット／コンポーネントサイドパネルが表示されます。

![chlimage_1-232](assets/chlimage_1-232.png)

* Classic UI: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

以下に、コンテンツファインダー(cf)を含むクラシックUIでの再生ページの表示方法を示します。

![chlimage_1-233](assets/chlimage_1-233.png)

## コミュニティコンポーネント {#communities-components}

オーサリング用にコミュニティコンポーネントを使用できるようにするには、まず、次の指示に従ってください。

* [コミュニティコンポーネントへのアクセス](basics.md#accessing-communities-components)

このサンドボックスでは、次の&#x200B;**コミュニティ**&#x200B;コンポーネントから開始します（チェックボックスをオンにして有効にします）。

* コメント
* フォーラム
* 評価
* レビュー
* レビューの概要 (表示)
* 投票

In addition, choose **[!UICONTROL General]** components, such as

* 画像
* テーブル
* テキスト
* タイトル（基盤）

>[!NOTE]
>
>The components enabled for the page par are stored in the repository as the value of the `components` property of the
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` ノードの実際の値を表します。


## ランディングページ {#landing-page}

多言語環境では、クライアントからの要求を解析して優先言語を特定するスクリプトがルートページに含まれます。

この単純な例では、ルートページは英語のページにリダイレクトするように静的に設定されています。英語は、今後、再生ページへのリンクを持つメインランディングページとして開発される可能性があります。

ブラウザーの URL をルートページ [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html) に変更します。

* ページ情報アイコンを選択します。
* Select **[!UICONTROL Open Properties]**
* 「詳細」タブ

   * For the Redirect entry, browse to **[!UICONTROL Websites]** > **[!UICONTROL SCF Sandbox Site]** > **[!UICONTROL SCF Sandbox]**
   * 「**[!UICONTROL OK]**」をクリックします。

* 「**[!UICONTROL OK]**」をクリックします。

サイトを公開した後、パブリッシュインスタンスでルートページを参照すると、英語のページにリダイレクトされます。

コミュニティのSCFコンポーネントを再生する前の最後の手順は、クライアントライブラリフォルダー(clientlibs)を追加することです。. [追加クライアンリブ](add-clientlibs.md)