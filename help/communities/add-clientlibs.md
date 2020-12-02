---
title: clientlib の追加
seo-title: clientlib の追加
description: ClientLibraryFolder の追加
seo-description: ClientLibraryFolder の追加
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 41%

---


# clientlib の追加  {#add-clientlibs}

## 追加ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. **CRXDE Lite**&#x200B;を使用して`/etc/designs`を展開します

1. `an-scf-sandbox`を右クリックし、`Create Node`を選択します

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. 「**OK**」をクリックします。

![add-client-library](assets/add-client-library.png)

新しい **ノードの「**&#x200B;プロパティ`clientlibs`」タブで、**categories** プロパティを入力します。

* 名前：**categories**
* タイプ：**String**
* 値：**apps.an-scf-sandbox**
* **追加**&#x200B;をクリックします
* 「**すべて保存**」をクリックします

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。重要：プ追加レースホルダー`js.tx`tと&#x200B;**`css.txt`**&#x200B;ファイル （正式には、cq:ClientLibraryFolderが存在しない場合は除きます）。

1. **`/etc/designs/an-scf-sandbox/clientlibs`**&#x200B;を右クリック
1. **ファイルを作成を選択…**
1. **名前：** `css.txt`を入力
1. **ファイルを作成を選択…**
1. **名前：** `js.txt`を入力
1. 「**すべて保存**」をクリックします

![clientlibs-css](assets/clientlibs-css.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。

```
#base=.
 style.css
```

次に、clientlibsにstyle.cssという名前のファイルを作成し、内容を

`body {`

`background-color: #b0c4de;`

`}`

### SCF clientlib の埋め込み {#embed-scf-clientlibs}

**ノードの「**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **embed** を入力します。これにより、SCFコンポーネント](/help/communities/client-customize.md#clientlibs-for-scf)に必要な[クライアント側ライブラリ(clientlibs)が埋め込まれます。 このチュートリアルでは、Communitiesコンポーネントに必要なclientlibの多くが追加されます。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1つのページで1つの機能しか使用しない場合は、その機能の完全なclientlibを直接ページに含めることができます。例えば、

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

この場合は、すべてを含め、より基本的なSCFクライアントライブラリを作成者のclientlibとして扱うことをお勧めします。

* 名前：**`embed`**
* 型：**`String`**
* クリック **`Multi`**
* 値：**`cq.social.scf`**

   * ダイアログが表示されます。
各エントリの後に**`+`**&#x200B;をクリックして、次のclientlibカテゴリを追加します。

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 「**OK**」をクリックします。

* 「**すべて保存**」をクリックします

![scf-clientlibs](assets/scf-clientlibs.png)

`/etc/designs/an-scf-sandbox/clientlibs`は、次のようにリポジトリに表示されます。

![scf-clientlibs-表示](assets/scf-clientlibs1.png)

### playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

`apps.an-scf-sandbox` ClientLibraryFolderカテゴリをページに含めないと、SCFコンポーネントは機能しなくなり、必要なJavaScriptとスタイルが使用できなくなります。

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

includeステートメントは、`html`スクリプトの`head`セクションに属します。 デフォルトの&#x200B;**`foundation head.jsp`**&#x200B;には、オーバーレイ可能なスクリプトが含まれています。**`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. **CRXDE Lite**&#x200B;を使用して、**`/libs/foundation/components/page/headlibs.jsp`**&#x200B;を選択します

1. 右クリックし、「**コピー**」を選択します（または、ツールバーの「コピー」を選択します）。
1.  **`/apps/an-scf-sandbox/components/playpage`**
1. 右クリックし、「**貼り付け**」を選択します（または、ツールバーから「貼り付け」を選択します）。
1. **`headlibs.jsp`**&#x200B;を重複クリックして開きます
1. ファイルの末尾に次の行を追加します。
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. 「**すべて保存**」をクリックします

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Web サイトをブラウザーに読み込み、背景が青の網掛けでないかどうかを確認します。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![地域遊び](assets/community-play.png)

### これまでの作業内容の保存 {#saving-your-work-so-far}

この時点では、最小限のサンドボックスが存在し、再生中にリポジトリが破損し、開始し直したい場合に、サーバーのオフ、crx-quickstart/フォルダーの名前の変更や削除、サーバーのオン、アップロード、インストールを行う際に、最も基本的な手順を繰り返す必要がない。

すぐに操作してみたい場合は、[サンプルページの作成](/help/communities/create-sample-page.md)チュートリアルにこのパッケージがあります。

パッケージを作成するには：

* CRXDE Liteから[パッケージアイコン](https://localhost:4502/crx/packmgr/)をクリックします。
* 「**パッケージを作成**」をクリックします

   * パッケージ名：an-scf-sandbox-minimal-pkg
   * バージョン：0.1
   * グループ: `leave as default`
   * 「**OK**」をクリックします。

* 「**編集**」をクリックします。

   * 「**フィルター**」タブを選択

      * **追加フィルター**&#x200B;をクリック
      * ルートパス：`/apps/an-scf-sandbox`を参照
      * 「**完了**」をクリックします
      * **追加フィルター**&#x200B;をクリック
      * ルートパス：`/etc/designs/an-scf-sandbox`を参照
      * 「**完了**」をクリックします
      * **追加フィルター**&#x200B;をクリック
      * ルートパス：`/content/an-scf-sandbox**`を参照
      * 「**完了**」をクリックします
   * 「**保存**」をクリックします。


* 「**ビルド**」をクリックします

これで、「**ダウンロード**」を選択してディスクに保存し、**パッケージをアップロード**&#x200B;他に保存することができます。また、**詳細>複製**&#x200B;を選択して、サンドボックスの領域を拡張できます。