---
title: ページエクスポーター
description: AEM ページエクスポーターの使用方法について説明します。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 25%

---

# ページエクスポーター{#the-page-exporter}

AEMでは、画像、`.js`および`.css`ファイルを含む完全なWebページとしてページを書き出すことができます。

設定が完了したら、URLの`html`を`export.zip`に置き換えて、ブラウザーからのページ書き出しを要求します。 これにより、HTML形式でレンダリングされたページと参照元のアセットが含まれるアーカイブ(zip)ファイルが生成されます。 ページ内のすべてのパス（例えば、画像へのパス）は、アーカイブに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。 アーカイブ(zip)ファイルは、ブラウザーからダウンロードできます。

>[!NOTE]
>
>ブラウザーと設定に応じて、ダウンロードは次のいずれかになります。
>* アーカイブファイル(`<page-name>.export.zip`)
>* フォルダー(`<page-name>`);事実上、アーカイブ・ファイルは既に拡張済


## ページの書き出し {#exporting-a-page}

次の手順は、ページを書き出す方法と、サイトに書き出しテンプレートが存在することを前提としています。 書き出しテンプレートは、ページの書き出し方法を定義し、サイトに固有です。 書き出しテンプレートを作成するには、「[サイトのページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site)」の節を参照してください。

ページを書き出すには：

1. **サイト**&#x200B;コンソールで必要なページに移動します。

1. ページを選択し、**プロパティ**&#x200B;ダイアログを開きます。

1. 「**詳細**」タブを選択します。

1. 「**エクスポート**」フィールドを展開して、エクスポートテンプレートを選択します。
サイトに必要なテンプレートを選択し、「**OK**」で確定します。

1. 「**保存して閉じる**」を選択して、ページプロパティダイアログを閉じます。

1. URLのサフィックス`html`を`export.zip`に置き換えて、ページの書き出しを要求します。

   次に例を示します。
   * localhost:4502/content/we-retail/language-masters/en.html

   次の場所からアクセスします。
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. アーカイブファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、必要に応じてファイルを解凍します。 展開すると、選択したページと同じ名前のフォルダーが作成されます。 このフォルダーには次が含まれます。

   * サブフォルダー`content`：リポジトリ内のページへのパスを反映する一連のサブフォルダーのルートです。

      * この構造内には、選択されたページのhtmlファイル(`<page-name>.html`)があります。
   * その他のリソース（`.js`ファイル、`.css`ファイル、画像など） は、書き出しテンプレートの設定に従って配置されます。


1. ブラウザーでページのhtmlファイル(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)を開き、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、[コンテンツ同期フレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)に基づいています。 **ページのプロパティ**&#x200B;ダイアログで使用できる設定は、ページに必要な依存関係を定義する書き出しテンプレートです。

ページの書き出しがトリガーされると、書き出しテンプレートが参照され、ページパスとデザインパスの両方が動的に適用されます。 zipファイルは、標準のコンテンツ同期機能を使用して作成されます。

標準インストールのAEMには、`/etc/contentsync/templates/default`の下にデフォルトのテンプレートが含まれています。

* このテンプレートは、リポジトリ内に書き出しテンプレートが見つからない場合のフォールバックテンプレートです。

* `default`テンプレートは、新しい書き出しテンプレートのベースとなるために、ページの書き出しを設定する方法を示します。

* テンプレートのノード構造をJSON形式でブラウザーに表示するには、次のURLを要求します。
   `http://localhost:4502/etc/contentsync/templates/default.json`

新しいページエクスポーターテンプレートを作成する最も簡単な方法は次のとおりです。

* `default`テンプレートをコピーします。

* サイトに適切な新しい名前を割り当てます。

* 次に、必要な更新を行います。

完全に新しいテンプレートを作成するには：

1. **CRXDE Lite**&#x200B;で、`/etc/contentsync/templates`の下にノードを作成します。

   * `Name`:サイトに適した名前例：  `<mysite>`。この名前は、ページエクスポーターテンプレートを選択する際に、ページプロパティダイアログに表示されます。

   * `Type`: `nt:unstructured`

2. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

## ページのページエクスポーターテンプレートのアクティブ化{#activating-a-page-exporter-configuration-for-your-pages}

テンプレートを設定したら、使用可能にする必要があります。

1. CRXDEで、`/content`ブランチ内の必要なページに移動します。 これは、個々のページまたはサブツリーのルートページにすることができます。

1. ページの`jcr:content`ノードで、次のプロパティを作成します。
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:テンプレートへのパス例：  `/etc/contentsync/templates/mysite`

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

テンプレートは、[コンテンツ同期フレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)を使用するノード構造で構成されます。  各ノードには`type`プロパティがあり、zipファイルの作成プロセスでの特定のアクションを定義します。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

書き出しテンプレートの作成には、次のノードを使用できます。

* `page`page ノードは、ページの HTML を zip ファイルにコピーする際に使用します。次のような特徴があります。

   * 必須ノードである。
   * `/etc/contentsync/templates/<mysite>`の下にあります。
   * プロパティ`Name`を`page`に設定して定義します。
   * ノードタイプは`nt:unstructured`です。

   `page` ノードには以下のプロパティがあります。

   * 値`pages`で設定された`type`プロパティ。

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`rewrite ノードでは、書き出したページでリンクを書き換える方法を定義します。書き換え後のリンクは、zip ファイルに含まれるファイルまたはサーバー上のリソースを指すことができます。
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`design ノードは、書き出されるページに使用されているデザインをコピーする際に使用します。次のような特徴があります。

   * オプションである。
   * `/etc/contentsync/templates/<mysite>`の下にあります。
   * プロパティ`Name`を`design`に設定して定義します。
   * ノードタイプは `nt:unstructured` です。

   `design` ノードには以下のプロパティがあります。

   * 値`copy`に設定された`type`プロパティ。

   * 現在のページパスは設定に動的にコピーされるので、`path`プロパティはありません。


* `generic`
汎用ノードは、clientlibsなどのリソースのコピーに使用されます 
`.js` または `.css` ファイルをzipファイルにコピーします。次の特性があります。

   * オプションである。
   * `/etc/contentsync/templates/<mysite>`の下にあります。
   * 特定の名前を持たない。
   * ノードタイプは `nt:unstructured` です。
   * `type`プロパティと`type`関連プロパティがある。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例えば、次の設定ノードでは、`mysite.clientlibs.js`ファイルをzipファイルにコピーします。

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
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

特定の要件を満たすには、場合によっては[カスタム更新ハンドラー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)を実装する必要があります。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

zipファイルのダウンロードで問題が発生した場合は、リポジトリ内の`/var/contentsync`ノードを削除し、書き出しリクエストを再度送信できます。
