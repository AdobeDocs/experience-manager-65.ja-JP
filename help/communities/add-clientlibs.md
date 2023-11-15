---
title: clientlib の追加
description: サイトのページをレンダリングするために使用する JavaScript およびカスケードスタイルシートを含めるために使用する ClientLibraryFolder(clientlibs) を追加する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# clientlib の追加 {#add-clientlibs}

## ClientLibraryFolder(clientlibs) の追加 {#add-a-clientlibraryfolder-clientlibs}

という名前の ClientLibraryFolder を作成します。 `clientlibs` サイトのページをレンダリングするために使用される JavaScript(JS) およびカスケーディングスタイルシート (CSS) を含む

The `categories` このクライアントライブラリに与えられるプロパティ値は、コンテンツページからこの clientlib を直接含めたり、他の clientlib に埋め込んだりするために使用される識別子です。

1. 使用 **CRXDE Lite**、展開 `/etc/designs`

1. 右クリック `an-scf-sandbox` を選択し、 `Create Node`

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. クリック **OK**

![add-client-library](assets/add-client-library.png)

Adobe Analytics の **プロパティ** 新しい `clientlibs` ノードに、 **カテゴリ** プロパティ：

* 名前：**categories**
* タイプ：**String**
* 値： **apps.an-scf-sandbox**
* クリック **追加**
* クリック **すべて保存**

注意： categories 値の前に「apps」を付けます。 は、「所有アプリケーション」が/libs ではなく/apps フォルダー内にあることを識別する規則です。 重要：プレースホルダーを追加 `js.tx`t および **`css.txt`** ファイル。 （正式には cq:ClientLibraryFolder ではありません。）

1. 右クリック **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選択 **ファイルを作成…**
1. 入力 **名前：** `css.txt`
1. 選択 **ファイルを作成…**
1. 入力 **名前：** `js.txt`
1. クリック **すべて保存**

![clientlibs-css](assets/clientlibs-css.png)

css.txt と js.txt の最初の行は、以下のファイルのリストを検索する基本の場所を示します。

css.txt の内容を次のように設定してみてください。

```
#base=.
 style.css
```

次に、clientlibs の下に style.css という名前のファイルを作成し、コンテンツを

`body {`

`background-color: #b0c4de;`

`}`

### SCF Clientlibs を埋め込む {#embed-scf-clientlibs}

Adobe Analytics の **プロパティ** タブ `clientlibs` ノードで、複数値の String プロパティを入力します。 **埋め込み**. これにより、必要な [SCF コンポーネントのクライアント側ライブラリ (clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf). このチュートリアルでは、コミュニティコンポーネントに必要なクライアントライブラリの多くが追加されています。

各ページにダウンロードされる clientlib の利便性とサイズ/速度に関する考慮事項があるので、実稼動サイトで使用する方法にはこの方法が望ましい場合とそうでない場合があります。

1 つのページで 1 つの機能のみを使用する場合、その機能の完全な clientlib をそのページに直接組み込むことができます（例： ）。

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

この場合は、すべてを含め、作成者の clientlib であるより基本的な SCF クライアントライブラリをお勧めします。

* 名前：**`embed`**
* 型：**`String`**
* Click **`Multi`**
* 値：**`cq.social.scf`**

   * ダイアログが表示され、 **`+`** 各エントリの後に、次の clientlib カテゴリを追加します。

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * クリック **OK**

* クリック **すべて保存**

![scf-clientlibs](assets/scf-clientlibs.png)

このように `/etc/designs/an-scf-sandbox/clientlibs` がリポジトリに表示されます。

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### PlayPage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

を含めずに、 `apps.an-scf-sandbox` 必要な JavaScript および CSS スタイルを使用できないので、ページの ClientLibraryFolder カテゴリ、SCF コンポーネントは機能しないか、スタイル設定されていません。

例えば、clientlibs を含めないと、SCF コメントコンポーネントはスタイル設定されていない状態で表示されます。

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs を含めると、 SCF コメントコンポーネントは次のスタイルで表示されます。

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include ステートメントは、 `head` のセクション `html` スクリプト。 デフォルト **`foundation head.jsp`** には、オーバーレイ可能なスクリプトが含まれています。 **`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. 使用 **CRXDE Lite**&#x200B;を選択します。 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右クリックして「 」を選択します。 **コピー** （または、ツールバーから「コピー」を選択します）。
1. **`/apps/an-scf-sandbox/components/playpage`** を選択します。
1. 右クリックして「 」を選択します。 **貼り付け** （または、ツールバーから「貼り付け」を選択します）。
1. ダブルクリック **`headlibs.jsp`** 開けるように
1. ファイルの末尾に次の行を追加します。
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. クリック **すべて保存**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

ブラウザーに Web サイトを読み込み、背景が青の影でないかどうかを確認します。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![コミュニティプレイ](assets/community-play.png)

### これまでの作業の保存 {#saving-your-work-so-far}

この時点で、最小限のサンドボックスが存在します。 再生中にリポジトリが破損し、再起動したい場合は、サーバーをオフにできるように、パッケージとして保存する価値がある場合があります。 次に、フォルダー crx-quickstart/の名前を変更または削除し、サーバーをオンにし、この保存済みパッケージをアップロードしてインストールします。これらの最も基本的な手順を繰り返す必要はありません。

このパッケージは、 [サンプルページの作成](/help/communities/create-sample-page.md) 飛び込んで遊び始めるのを待ちきれない人向けのチュートリアル！

パッケージを作成するには：

* CRXDE Liteで、 [パッケージアイコン](https://localhost:4502/crx/packmgr/)
* クリック **パッケージを作成**

   * パッケージ名： an-scf-sandbox-minimal-pkg
   * バージョン： 0.1
   * グループ：`leave as default`
   * クリック **OK**

* クリック **編集**

   * 選択 **フィルター** タブ

      * クリック **フィルターを追加**
      * ルートパス：参照先 `/apps/an-scf-sandbox`
      * クリック **完了**
      * クリック **フィルターを追加**
      * ルートパス：参照先 `/etc/designs/an-scf-sandbox`
      * クリック **完了**
      * クリック **フィルターを追加**
      * ルートパス：参照先 `/content/an-scf-sandbox**`
      * クリック **完了**

   * 「**保存**」をクリックします。

* クリック **ビルド**

これで、以下を選択できます。 **ダウンロード** ディスクに保存し **パッケージをアップロード** 別の場所に移動し、「 **その他/レプリケート** ：サンドボックスを localhost パブリッシュインスタンスにプッシュして、サンドボックスの領域を拡張します。
