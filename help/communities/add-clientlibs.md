---
title: clientlib の追加
description: サイトのページのレンダリングに使用する JavaScript およびカスケードスタイルシートを含めるために使用される ClientLibraryFolder （clientlibs）を追加する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 2%

---

# clientlib の追加 {#add-clientlibs}

## ClientLibraryFolder （clientlibs）の追加 {#add-a-clientlibraryfolder-clientlibs}

という名前の ClientLibraryFolder を作成します。 `clientlibs` には、サイトのページのレンダリングに使用する JavaScript （JS）とカスケードスタイルシート（CSS）が含まれています。

この `categories` このクライアントライブラリに指定されるプロパティ値は、このクライアントライブラリをコンテンツページから直接含めるために、または他のクライアントライブラリに埋め込むために使用される識別子です。

1. 使用 **CRXDE Lite**、を展開 `/etc/designs`

1. 右クリック `an-scf-sandbox` を選択して、 `Create Node`

   * 名前： `clientlibs`
   * タイプ : `cq:ClientLibraryFolder`

1. クリック **OK**

![add-client-library](assets/add-client-library.png)

が含まれる **プロパティ** 新しいのタブ `clientlibs` ノードに、と入力します **カテゴリ** プロパティ：

* 名前： **カテゴリ**
* タイプ : **文字列**
* 値： **apps.an-scf-sandbox**
* クリック **追加**
* クリック **すべて保存**

メモ : カテゴリ値の前に「apps」を付けます。 「所有しているアプリケーション」を/libs ではなく/apps フォルダー内にあるものとして識別する規則です。 重要：プレースホルダーを追加 `js.tx`t および **`css.txt`** ファイル。 （公式には、これらを持たない cq:ClientLibraryFolder ではありません。）

1. 右クリック **`/etc/designs/an-scf-sandbox/clientlibs`**
1. を選択 **ファイルの作成…**
1. Enter **名前：** `css.txt`
1. を選択 **ファイルの作成…**
1. Enter **名前：** `js.txt`
1. クリック **すべて保存**

![clientlibs-css](assets/clientlibs-css.png)

css.txt と js.txt の最初の行は、次のファイルのリストが見つかるベースの場所を示しています。

css.txt のコンテンツをに設定してみてください

```
#base=.
 style.css
```

次に、clientlibs の下に style.css という名前のファイルを作成し、そのコンテンツをに設定します

`body {`

`background-color: #b0c4de;`

`}`

### SCF Clientlibs の埋め込み {#embed-scf-clientlibs}

が含まれる **プロパティ** タブ： `clientlibs` ノードで、複数値の文字列プロパティを入力します **embed**. これにより、必要なが埋め込まれます [scf コンポーネントのクライアントサイドライブラリ（clientlib）](/help/communities/client-customize.md#clientlibs-for-scf). このチュートリアルでは、Communities コンポーネントに必要な clientlib の多くを追加します。

すべてのページにダウンロードされる clientlibs の利便性とサイズ/速度を考慮する必要があるので、実稼動サイトで使用する場合は、この方法が望ましい場合もあれば、そうでない場合もあります。

1 つのページで 1 つの機能のみを使用する場合、その機能の完全な clientlib をページに直接含めることができます。例：

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

この場合、それらをすべて含めることによって、オーサー clientlibs であるより基本的な SCF clientlibs が推奨されます。

* 名前： **`embed`**
* タイプ : **`String`**
* クリック **`Multi`**
* 値：**`cq.social.scf`**

   * ダイアログがポップアップ表示されるので、クリックします **`+`** 各エントリの後に、次の clientlib カテゴリを追加します。

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * クリック **OK**

* クリック **すべて保存**

![scf-clientlibs](assets/scf-clientlibs.png)

方法は次のとおりです `/etc/designs/an-scf-sandbox/clientlibs` これで、リポジトリにが表示されます。

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### プレイページテンプレートにクライアントライブラリを含める {#include-clientlibs-in-playpage-template}

を含まない `apps.an-scf-sandbox` ClientLibraryFolder カテゴリ ページ上で、必要な JavaScript および CSS スタイルが使用できないため、SCF コンポーネントは機能せず、スタイルも設定されません。

例えば、clientlib を含めない場合、SCF コメントコンポーネントのスタイルは未設定になります。

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs が含まれると、SCF コメントコンポーネントのスタイルが次のように表示されます。

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include ステートメントは、 `head` の節 `html` スクリプト。 デフォルト **`foundation head.jsp`** オーバーレイ可能なスクリプトを含みます。 **`headlibs.jsp`**.

**headlibs.jsp をコピーして clientlibs を含めます。**

1. 使用 **CRXDE Lite**&#x200B;を選択 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右クリックして選択 **コピー** （または、ツールバーの「コピー」を選択します）
1. **`/apps/an-scf-sandbox/components/playpage`** を選択します。
1. 右クリックして選択 **ペースト** （または、ツールバーの「貼り付け」を選択します）
1. ダブルクリック **`headlibs.jsp`** だからあなたはそれを開くことができます
1. ファイルの末尾に次の行を追加します
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

ブラウザーで web サイトを読み込んで、背景が青の網掛けになっていないかどうかを確認します。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![コミュニティプレイ](assets/community-play.png)

### 作業内容を保存しています {#saving-your-work-so-far}

この時点で、最小限のサンドボックスが存在します。 再生中にリポジトリが破損して最初からやり直したい場合は、サーバーの電源を切ることができるように、パッケージとして保存する価値があるかもしれません。 次に、crx-quickstart/フォルダーの名前を変更または削除し、サーバーをオンにして、この保存されたパッケージをアップロードしてインストールします。これらの最も基本的な手順を繰り返す必要はありません。

このパッケージはに存在します [サンプルページの作成](/help/communities/create-sample-page.md) ジャンプして再生を開始するのを待つことができない人のためのチュートリアル。

パッケージを作成するには：

* CRXDE Liteで、 [パッケージアイコン](https://localhost:4502/crx/packmgr/)
* クリック **パッケージを作成**

   * パッケージ名：an-scf-sandbox-minimal-pkg
   * バージョン：0.1
   * グループ：`leave as default`
   * クリック **OK**

* クリック **編集**

   * を選択 **フィルター** タブ

      * クリック **フィルターを追加**
      * ルートパス：を参照します。 `/apps/an-scf-sandbox`
      * 「**完了**」をクリックします。
      * クリック **フィルターを追加**
      * ルートパス：を参照します。 `/etc/designs/an-scf-sandbox`
      * 「**完了**」をクリックします。
      * クリック **フィルターを追加**
      * ルートパス：を参照します。 `/content/an-scf-sandbox**`
      * 「**完了**」をクリックします。

   * 「**保存**」をクリックします。

* クリック **ビルド**

次を選択できます **Download** ディスクに保存するには、および **パッケージをアップロード** 他の場所で、を選択します。 **詳細/ レプリケート** サンドボックスを localhost パブリッシュインスタンスにプッシュしてサンドボックスの領域を拡張するには、次の手順を実行します。
