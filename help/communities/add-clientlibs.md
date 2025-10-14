---
title: clientlib の追加
description: サイトのページのレンダリングに使用するJavaScriptおよびカスケーディングスタイルシート（CSS）を格納するための ClientLibraryFolder （clientlibs）を追加する方法について説明します。
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

サイトのページのレンダリングに使用するJavaScript（JS）およびカスケードスタイルシート（CSS）を含む、`clientlibs` という名前の ClientLibraryFolder を作成します。

このクライアントライブラリに指定される `categories` プロパティの値は、このクライアントライブラリをコンテンツページから直接含めるために、または他のクライアントライブラリに埋め込むために使用される識別子です。

1. **CRXDE Lite** を使用して、`/etc/designs` を展開します

1. `an-scf-sandbox` を右クリックし、「`Create Node`」を選択します。

   * 名前：`clientlibs`
   * タイプ : `cq:ClientLibraryFolder`

1. 「**OK**」をクリックします。

![add-client-library](assets/add-client-library.png)

新しい `clientlibs` ノードの **プロパティ** タブで、**categories** プロパティを入力します。

* 名前：**categories**
* タイプ : **String**
* 値：**apps.an-scf-sandbox**
* **追加** をクリックします
* **すべて保存** をクリックします。

メモ : カテゴリ値の前に「apps」を付けます。 「所有しているアプリケーション」を/libs ではなく/apps フォルダー内にあるものとして識別する規則です。 重要：プレースホルダー `js.tx`t ファイルと **`css.txt`** ファイルを追加します。 （公式には、これらを持たない cq:ClientLibraryFolder ではありません。）

1. **`/etc/designs/an-scf-sandbox/clientlibs`** を右クリック
1. 「**ファイルを作成…**」を選択します。
1. **名前：** `css.txt` と入力します
1. 「**ファイルを作成…**」を選択します。
1. **名前：** `js.txt` と入力します
1. **すべて保存** をクリックします。

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

`clientlibs` ノードの **プロパティ** タブで、複数値の文字列プロパティ **embed** を入力します。 これにより、必要な [SCF コンポーネントのクライアントサイドライブラリ（clientlibs） &#x200B;](/help/communities/client-customize.md#clientlibs-for-scf) が組み込まれます。 このチュートリアルでは、Communities コンポーネントに必要な clientlib の多くを追加します。

すべてのページにダウンロードされる clientlibs の利便性とサイズ/速度を考慮する必要があるので、実稼動サイトで使用する場合は、この方法が望ましい場合もあれば、そうでない場合もあります。

1 つのページで 1 つの機能のみを使用する場合、その機能の完全な clientlib をページに直接含めることができます。例：

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

この場合、それらをすべて含めることによって、オーサー clientlibs であるより基本的な SCF clientlibs が推奨されます。

* 名前：**`embed`**
* タイプ : **`String`**
* **`Multi`** をクリック
* 値：**`cq.social.scf`**

   * ダイアログがポップアップ表示され、
各エントリの後の **`+`** をクリックして、次の clientlib カテゴリを追加します。

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * 「**OK**」をクリックします。

* **すべて保存** をクリックします。

![scf-clientlibs](assets/scf-clientlibs.png)

リポジトリーでは、`/etc/designs/an-scf-sandbox/clientlibs` は次のように表示されます。

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### プレイページテンプレートにクライアントライブラリを含める {#include-clientlibs-in-playpage-template}

ページに `apps.an-scf-sandbox` ClientLibraryFolder カテゴリが含まれていない場合、必要なJavaScriptと CSS スタイルが使用できないため、SCF コンポーネントは機能せず、スタイルも設定されません。

例えば、clientlib を含めない場合、SCF コメントコンポーネントのスタイルは未設定になります。

![clientlibs-comment](assets/clientlibs-comment.png)

apps.an-scf-sandbox clientlibs が含まれると、SCF コメントコンポーネントのスタイルが次のように表示されます。

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

include ステートメントは、`html` スクリプトの `head` セクションに属しています。 デフォルトの **`foundation head.jsp`** には、オーバーレイ可能なスクリプトが含まれています：**`headlibs.jsp`**。

**headlibs.jsp をコピーして clientlibs を含める：**

1. **CRXDE Lite** を使用して、「**`/libs/foundation/components/page/headlibs.jsp`**」を選択します

1. 右クリックして「**コピー**」を選択します（または、ツールバーの「コピー」を選択します）。
1. **`/apps/an-scf-sandbox/components/playpage`** を選択します。
1. 右クリックして「**貼り付け**」を選択します（または、ツールバーの「貼り付け」を選択します）。
1. **`headlibs.jsp`** をダブルクリックして開きます
1. ファイルの末尾に次の行を追加します
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. **すべて保存** をクリックします。

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

![&#x200B; コミュニティプレイ &#x200B;](assets/community-play.png)

### 作業内容を保存しています {#saving-your-work-so-far}

この時点で、最小限のサンドボックスが存在します。 再生中にリポジトリが破損して最初からやり直したい場合は、サーバーの電源を切ることができるように、パッケージとして保存する価値があるかもしれません。 次に、crx-quickstart/フォルダーの名前を変更または削除し、サーバーをオンにして、この保存されたパッケージをアップロードしてインストールします。これらの最も基本的な手順を繰り返す必要はありません。

このパッケージは、すぐに作業に取りかかって再生を開始できないユーザー向けの [&#x200B; サンプルページの作成 &#x200B;](/help/communities/create-sample-page.md) チュートリアルに存在しています。

パッケージを作成するには：

* CRXDE Liteで [&#x200B; パッケージアイコン &#x200B;](https://localhost:4502/crx/packmgr/) をクリックします
* 「**パッケージを作成**」をクリックします

   * パッケージ名：an-scf-sandbox-minimal-pkg
   * バージョン：0.1
   * グループ：`leave as default`
   * 「**OK**」をクリックします。

* **編集** をクリックします。

   * 「**フィルター**」タブを選択します

      * 「**フィルターを追加**」をクリックします
      * ルートパス：`/apps/an-scf-sandbox` を参照します
      * 「**完了**」をクリックします。
      * 「**フィルターを追加**」をクリックします
      * ルートパス：`/etc/designs/an-scf-sandbox` を参照します
      * 「**完了**」をクリックします。
      * 「**フィルターを追加**」をクリックします
      * ルートパス：`/content/an-scf-sandbox**` を参照します
      * 「**完了**」をクリックします。

   * 「**保存**」をクリックします。

* **ビルド** をクリックします

これで、「**ダウンロード** **」を選択してディスクに保存し、「パッケージをアップロード** を別の場所に保存できます。そして、**詳細/レプリケート** を選択して、サンドボックスを localhost パブリッシュインスタンスにプッシュして、サンドボックスの領域を拡張できます。
