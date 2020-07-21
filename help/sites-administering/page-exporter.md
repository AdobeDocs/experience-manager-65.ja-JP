---
title: ページエクスポーター
description: AEM ページエクスポーターの使用方法について説明します。
translation-type: tm+mt
source-git-commit: 000666e0c3f05635a9469d3571a10c67b3b21613
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 28%

---


# ページエクスポーター{#the-page-exporter}

AEM allows you to export a page as a complete web page including images, `.js` and `.css` files.

設定が完了したら、URLのをに置き換えて、ブラウザーからページの書き出し `html` を要求 `export.zip` します。 これにより、HTML形式でレンダリングされたページと参照先のアセットが含まれたアーカイブ(zip)ファイルが生成されます。 ページ内のすべてのパス（例えば、画像へのパス）が、アーカイブに含まれるファイルまたはサーバー上のリソースを指すように書き直されます。 アーカイブ(zip)ファイルをブラウザーからダウンロードできます。

>!![NOTE]
ブラウザーと設定に応じて、ダウンロードは次のいずれかになります。
* アーカイブファイル(`<page-name>.export.zip`)
* フォルダ(`<page-name>`); 効果的にアーカイブ・ファイルは既に拡張済み


## ページの書き出し {#exporting-a-page}

The following steps describe how to export a page, and assume that an export configuration template exists for your site. A configuration template defines the way a page is exported and is specific to your site. To create a configuration template refer to the [Creating a Page Exporter Configuration for your Site](#creating-a-page-exporter-configuration-for-your-site) section.

ページを書き出すには：

1. 目的のページに移動し、ページを選択して、 **プロパティ** ダイアログを開きます。

1. 「**詳細**」タブを選択します。

1. 「 **書き出し** 」フィールドを展開し、設定テンプレートを選択します。
サイトに必要なテンプレートを選択し、「 **OK**」をクリックして確認します。

1. 「 **保存して閉じる** 」を選択して、ページプロパティダイアログを閉じます。

1. ページの書き出しを要求し、サフィックス `html` をURLの `export.zip` に置き換えます。

   次に例を示します。
   * localhost:4502/content/we-retail/language-masters/en.html

   次を介してアクセス：
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. アーカイブファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、必要に応じてファイルを解凍します。 展開すると、選択したページと同じ名前のフォルダーが作成されます。 このフォルダーには次が含まれます。

   * サブフォルダー `content`。リポジトリ内のページへのパスを反映した一連のサブフォルダーのルートです。

   * この構造内には、選択したページのhtmlファイルがあります(`<page-name>.html`)

   * その他のリソース(`.js` ファイル、 `.css` ファイル、画像など) は、書き出しテンプレートの設定に従って配置されます。

1. Open the page html file (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) in your browser to check the rendering.

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、コンテンツ同期フレームワークに基づいています。 「 **ページプロパティ** 」ダイアログで使用できる設定は、ページに必要な依存関係を定義する書き出しテンプレートです。

ページの書き出しがトリガーされると、書き出しテンプレートが参照され、ページパスとデザインパスの両方が動的に適用されます。 その後、標準のコンテンツ同期機能を使用してzipファイルを作成します。

AEMは、の下にデフォルトのテンプレートを埋め込み `/etc/contentsync/templates/default`ます。

* このテンプレートは、リポジトリに設定テンプレートが見つからない場合のフォールバックテンプレートです。

* この `default` テンプレートは、ページエクスポートの設定方法を示し、新しい設定テンプレートのベースとして機能します。

* テンプレートのノード構造をJSON形式で表示するには、次のURLを要求します。
   `http://localhost:4502/etc/contentsync/templates/default.json`

新しいページエクスポーターテンプレートを作成する最も簡単な方法は次のとおりです。

* テン `default` プレートのコピー、

* サイトに適した新しい名前を割り当て、

* 次に、必要な更新を行います。

完全に新しいテンプレートを作成するには：

1. In **CRXDE Lite**, create a node below `/etc/contentsync/templates`:

   * `Name`: サイトに適した名前 例えば、 `<mysite>`。 ページエクスポーターテンプレートを選択すると、ページプロパティダイアログに名前が表示されます。

   * `Type`: `nt:unstructured`

1. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

## ページのページエクスポータテンプレートのアクティブ化 {#activating-a-page-exporter-configuration-for-your-pages}

テンプレートを設定したら、使用可能にする必要があります。

1. CRXDEで、必要なページに移動します。

1. `jcr:content` ノードで、以下のプロパティを作成します。
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: テンプレートのパス 例： `/etc/contentsync/templates/mysite`

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

テンプレートはノード構造で構成されます。 各ノードには、zipファイルの作成プロセスでの特定のアクションを定義する `type` プロパティがあります。 typeプロパティの詳細については、コンテンツ同期フレームワークページの「設定タイプの概要」の節を参照してください。

書き出し設定テンプレートを作成するには、以下のノードを使用できます。

* `page`page ノードは、ページの HTML を zip ファイルにコピーする際に使用します。次のような特徴があります。

   * 必須ノードである。
   * は下にあり `/etc/contentsync/templates/<sitename>`ます。
   * Its name is `page`.
   * Its node type is `nt:unstructured`

   `page` ノードには以下のプロパティがあります。

   * A `type` property set with the value `pages`.

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

   * その他のプロパティは、コンテンツ同期フレームワークの「設定の種類の概要」セクションに説明されています。


* `rewrite`rewrite ノードでは、書き出したページでリンクを書き換える方法を定義します。書き換え後のリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すことができます。

   `rewrite` ノードについて詳しくは、コンテンツ同期ページを参照してください。

* `design`design ノードは、書き出されるページに使用されているデザインをコピーする際に使用します。次のような特徴があります。

   * オプションである。
   * は下にあり `/etc/contentsync/templates/<sitename>`ます。
   * Its name is `design`.
   * Its node type is `nt:unstructured`.

   `design` ノードには以下のプロパティがあります。

   * A `type` property set to the value `copy`.

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。


* `generic`汎用ノードは、クライアントライブラリの .js ファイルや .css ファイルのようなリソースを zip ファイルにコピーする際に使用します。次のような特徴があります。

   * オプションである。

   * は下にあり `/etc/contentsync/templates/<sitename>`ます。

   * 特定の名前を持たない。

   * Its node type is `nt:unstructured`.

   * Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.

   For example the following configuration node copies the `mysite.clientlibs.js` files to the zip file:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**カスタム設定の実装**

カスタム設定も可能です。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export configuration template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

特定の要件を満たすには、カスタム `type` プロパティの実装が必要になる場合があります。 これを行うには、コンテンツの同期ページの「カスタム更新ハンドラーの実装」の節を参照してください。

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

If you experience a problem with the download of the zip file, you may delete the `/var/contentsync` node in the repository and send the export request again.

