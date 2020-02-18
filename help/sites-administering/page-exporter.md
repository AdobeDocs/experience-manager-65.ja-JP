---
title: ページエクスポーター
seo-title: ページエクスポーター
description: AEM ページエクスポーターの使用方法について説明します。
seo-description: AEM ページエクスポーターの使用方法について説明します。
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# ページエクスポーター{#the-page-exporter}

AEM では、画像、.js ファイルおよび .css ファイルを含む完全な Web ページとしてページを書き出すことができます。

書き出しを設定したら、URLのをに置き換えてブラウザーでページを要求し、レンダリングされたページをHTML形式で含み、参照アセットを含むzipファイルダウンロードを取得します。 `html``export.zip` ページ内のパス（画像へのパスなど）は、zipファイルに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。

## ページの書き出し {#exporting-a-page}

The following steps describe how to export a page, and assume that an export configuration template exists for your site. A configuration template defines the way a page is exported and is specific to your site. To create a configuration template refer to the [Creating a Page Exporter Configuration for your Site](#creating-a-page-exporter-configuration-for-your-site) section.

ページを書き出すには：

1. ブラウザーで、ページを開きます。次に例を示します。
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. ページのプロパティダイアログを開き、「**詳細**」タブを選択して、「**書き出し**」フィールドセットを展開します。

1. 虫眼鏡のアイコンをクリックして設定テンプレートを選択します。Geometrixx サイトのデフォルトである **geometrixx** テンプレートを選択します。「**OK**」をクリックします。

1. 「**OK**」をクリックしてページのプロパティダイアログを閉じます。
1. Request the page by replacing `html` with `export.zip` in the URL.

1. Download the `<page-name>.export.zip` file to your file system.

1. ファイルシステムで、ファイルを解凍します。

   * the page html file ( `<page-name>.html`) is available below `<unzip-dir>/<page-path>`
   * その他のリソース（.jsファイル、.cssファイル、画像など）は、書き出しテンプレートの設定に従って配置されます。 この例では、以下のリソースと、次のリソ `<unzip-dir>/etc`ースのいくつかを示しま `<unzip-dir>/<page-path>`す。

1. Open the page html file ( `<unzip-dir>/<page-path>.html`) in your browser to check the rendering.

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、コンテンツ同期フレームワークに基づいています。ページプロパティダイアログで使用できる設定は、設定テンプレートです。ページに必要な依存関係をすべて定義します。ページの書き出しがトリガーされると、設定テンプレートが使用され、ページパスとデザインパスの両方が設定に動的に適用されます。その後、標準のコンテンツ同期機能を使用してzipファイルを作成します。

AEM では、以下を含むいくつかのテンプレートが埋め込まれます。

* A default one at `/etc/contentsync/templates/default`. This template:

   * リポジトリ内に設定テンプレートが見つからない場合のフォールバックテンプレートです。
   * 新しい設定テンプレートのベースとして機能します。

* One that is dedicated to the **Geometrixx** site, at `/etc/contentsync/templates/geometrixx`. This template can be used as an example to create a new one.

ページエクスポーター設定テンプレートを作成するには：

1. In **CRXDE Lite**, create a node below `/etc/contentsync/templates`:

   * Name: e.g. `mysite`. The name appears in the page properties dialog when choosing the page exporter template.
   * タイプ: `nt:unstructured`

1. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

設定テンプレートはノード構造で構成されます。 各ノードには、zipフ `type` ァイルの作成プロセスでの特定のアクションを定義するプロパティがあります。 typeプロパティについて詳しくは、コンテンツ同期フレームワークページの「設定タイプの概要」を参照してください。

書き出し設定テンプレートを作成するには、以下のノードを使用できます。

**page node** ：ページノードは、ページhtmlをzipファイルにコピーするために使用します。 次の特徴があります。

* 必須ノードである。
* は下にあります `/etc/contentsync/templates/<sitename>`。
* Its name is `page`.
* Its node type is `nt:unstructured`

`page` ノードには以下のプロパティがあります。

* A `type` property set with the value `pages`.

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* その他のプロパティは、コンテンツ同期フレームワークの「設定タイプの概要」セクションで説明されています。

**rewrite node** ：書き出したページでリンクを書き換える方法はrewriteノードで定義します。 書き換え後のリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すことができます。

`rewrite` ノードについて詳しくは、コンテンツ同期ページを参照してください。

**デザインノード** ：デザインノードは、書き出したページで使用するデザインをコピーするために使用されます。 次の特徴があります。

* オプションである。
* は下にあります `/etc/contentsync/templates/<sitename>`。
* Its name is `design`.
* Its node type is `nt:unstructured`.

`design` ノードには以下のプロパティがあります。

* A `type` property set to the value `copy`.

* `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

**汎用ノード** :clientlibs .jsや.cssファイルなどのリソースをzipファイルにコピーするために使用される汎用ノードです。 次の特徴があります。

* オプションである。
* は下にあります `/etc/contentsync/templates/<sitename>`。
* 特定の名前を持たない。
* Its node type is `nt:unstructured`.
* Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.

例えば、以下の設定ノードでは、geometrixx クライアントライブラリの .js ファイルを zip ファイルにコピーします。

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

**Geometrixx** ページ書き出し設定テンプレートを見ると、ページ書き出しの設定方法がわかります。テンプレートのノード構造をブラウザーで json 形式で表示するには、以下の URL を要求します。

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**カスタム設定の実装**

ノード構造に気付いたかもしれませんが、 **Geometrixx** ページ書き出し設定テンプレートには、「」というプ `logo` ロパティが設定され `type` たノードがありま `image`す。 これは、画像のロゴをzipファイルにコピーするために作成された特別な設定タイプです。 特定の要件を満たすには、カスタムプロパティの実装が必要になる場合があ `type` ります。これを行うには、コンテンツの同期ページの「カスタムアップデートハンドラーの実装」の節を参照してください。

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

If you experience a problem with the download of the zip file, you may delete the `/var/contentsync` node in the repository and send the export request again.

