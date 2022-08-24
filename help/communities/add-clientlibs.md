---
title: clientlib の追加
seo-title: Add Clientlibs
description: ClientLibraryFolder の追加
seo-description: Add a ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 41%

---

# clientlib の追加 {#add-clientlibs}

## ClientLibraryFolder（clientlibs）の追加 {#add-a-clientlibraryfolder-clientlibs}

`clientlibs` という名前の ClientLibraryFolder を作成し、ここに、サイトのページをレンダリングするために使用される JS および CSS を格納します。

このクライアントライブラリに指定する `categories` プロパティの値は、clientlib をコンテンツページから直接含めたり、その他の clientlib に埋め込んだりする場合に使用される識別子です。

1. 使用 **CRXDE Lite**、展開 `/etc/designs`

1. 右クリック `an-scf-sandbox` を選択し、 `Create Node`

   * 名前：`clientlibs`
   * 型：`cq:ClientLibraryFolder`

1. 「**OK**」をクリックします。

![add-client-library](assets/add-client-library.png)

新しい **ノードの「**&#x200B;プロパティ`clientlibs`」タブで、**categories** プロパティを入力します。

* 名前：**categories**
* タイプ：**String**
* 値：**apps.an-scf-sandbox**
* クリック **追加**
* クリック **すべて保存**

注意：categories 値の前に「apps.」を付けるのは、「所有アプリケーション」が /libs ではなく、/apps フォルダー内にあることを示すための規則です。重要：プレースホルダーを追加 `js.tx`t および **`css.txt`** ファイル。 （正式には cq:ClientLibraryFolder ではありません。）

1. 右クリック **`/etc/designs/an-scf-sandbox/clientlibs`**
1. 選択 **ファイルを作成…**
1. 入力 **名前：** `css.txt`
1. 選択 **ファイルを作成…**
1. 入力 **名前：** `js.txt`
1. クリック **すべて保存**

![clientlibs-css](assets/clientlibs-css.png)

css.txt および js.txt の最初の行によって、後述のファイルのリストが見つかる基本の場所が特定されます。

css.txt の内容を次のように設定します。

```
#base=.
 style.css
```

次に、clientlibs の下に style.css という名前のファイルを作成し、コンテンツを

`body {`

`background-color: #b0c4de;`

`}`

### SCF clientlib の埋め込み {#embed-scf-clientlibs}

**ノードの「**&#x200B;プロパティ`clientlibs`」タブで、複数値の String プロパティ **embed** を入力します。これにより、必要な [SCF コンポーネントのクライアント側ライブラリ (clientlibs)](/help/communities/client-customize.md#clientlibs-for-scf). このチュートリアルでは、コミュニティコンポーネントに必要なクライアントライブラリの多くを追加します。

ページごとにダウンロードされる clientlib の利点とサイズ／スピードに関する考慮事項があるので、このアプローチが実稼動サイトでの使用に適している場合もあれば、そうでない場合もある点に&#x200B;**注意してください**。

1 つのページで 1 つの機能のみを使用する場合は、その機能の完全な clientlib をページに直接含めることができます ( 例：

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

この場合は、すべてを含めるなど、作成者の clientlib であるより基本的な SCF クライアントライブラリをお勧めします。

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
      * 「**OK**」をクリックします。

* クリック **すべて保存**

![scf-clientlibs](assets/scf-clientlibs.png)

このように `/etc/designs/an-scf-sandbox/clientlibs` がリポジトリに表示されます。

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### playpage テンプレートに clientlibs を含める {#include-clientlibs-in-playpage-template}

を含めずに、 `apps.an-scf-sandbox` 必要な JavaScript とスタイルが使用できないので、ページの ClientLibraryFolder カテゴリ、SCF コンポーネントは機能しないか、スタイル設定されません。

例えば、clientlibs を挿入しなかった場合、SCF コメントコンポーネントは、スタイルが設定されていない状態で表示されます。

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs を含めると、SCF コメントコンポーネントは、スタイルが設定された状態で表示されます。

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include ステートメントは、 `head` セクション `html` スクリプト デフォルト **`foundation head.jsp`** には、オーバーレイ可能なスクリプトが含まれています。 **`headlibs.jsp`**.

**headlibs.jsp をコピーし、clientlibs を含めます。**

1. 使用 **CRXDE Lite**&#x200B;を選択します。 **`/libs/foundation/components/page/headlibs.jsp`**

1. 右クリックして「 」を選択します。 **コピー** （または、ツールバーから「コピー」を選択します）。
1. 選択 **`/apps/an-scf-sandbox/components/playpage`**
1. 右クリックして「 」を選択します。 **貼り付け** （または、ツールバーから「貼り付け」を選択します）。
1. ダブルクリック **`headlibs.jsp`** 開ける
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

Web サイトをブラウザーに読み込み、背景が青の網掛けでないかどうかを確認します。

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![コミュニティプレイ](assets/community-play.png)

### これまでの作業内容の保存 {#saving-your-work-so-far}

この時点で、最小限のサンドボックスが存在し、再生中にリポジトリが破損し、再起動したい場合は、サーバーをオフにし、crx-quickstart/フォルダーの名前を変更または削除し、サーバーをオンにし、この保存済みパッケージをアップロードしてインストールできます。

すぐに操作してみたい場合は、[サンプルページの作成](/help/communities/create-sample-page.md)チュートリアルにこのパッケージがあります。

パッケージを作成するには：

* CRXDE Liteで、 [パッケージアイコン](https://localhost:4502/crx/packmgr/)
* クリック **パッケージを作成**

   * パッケージ名：an-scf-sandbox-minimal-pkg
   * バージョン：0.1
   * グループ：`leave as default`
   * 「**OK**」をクリックします。

* 「**編集**」をクリックします。

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

これで、 **ダウンロード** ディスクに保存し **パッケージをアップロード** 他の場所では、選択 **詳細 > レプリケート** サンドボックスを localhost パブリッシュインスタンスにプッシュしてサンドボックスの領域を拡張するために使用します。
