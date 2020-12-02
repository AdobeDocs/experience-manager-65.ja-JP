---
title: ページエクスポーター
description: AEM ページエクスポーターの使用方法について説明します。
translation-type: tm+mt
source-git-commit: 6aee1506b54a932bae8f2521fce4488de7d2a52a
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 24%

---


# ページエクスポーター{#the-page-exporter}

AEMでは、画像、`.js`、`.css`ファイルを含む完全なWebページとしてページを書き出すことができます。

設定が完了したら、URLの`html`を`export.zip`に置き換えて、ブラウザーからページエクスポートを要求します。 これにより、HTML形式でレンダリングされたページと参照先のアセットが含まれたアーカイブ(zip)ファイルが生成されます。 ページ内のすべてのパス（例えば、画像へのパス）が、アーカイブに含まれるファイルまたはサーバー上のリソースを指すように書き直されます。 アーカイブ(zip)ファイルをブラウザーからダウンロードできます。

>[!NOTE]
>
>ブラウザーと設定に応じて、ダウンロードは次のいずれかになります。
>* アーカイブファイル(`<page-name>.export.zip`)
>* フォルダー(`<page-name>`);効果的にアーカイブ・ファイルは既に拡張済み


## ページの書き出し {#exporting-a-page}

次の手順では、ページを書き出す方法、およびサイトに書き出しテンプレートが存在すると仮定します。 書き出しテンプレートは、ページの書き出し方法を定義し、サイトに固有のものです。 書き出しテンプレートを作成する方法については、「[サイト](#creating-a-page-exporter-configuration-for-your-site)のページエクスポーター設定の作成」を参照してください。

ページを書き出すには：

1. **サイト**&#x200B;コンソールの必要なページに移動します。

1. ページを選択し、**プロパティ**&#x200B;ダイアログを開きます。

1. 「**詳細**」タブを選択します。

1. 「**エクスポート**」フィールドを展開して、エクスポートテンプレートを選択します。
サイトに必要なテンプレートを選択し、**OK**&#x200B;で確認します。

1. 「**保存して閉じる**」を選択して、ページのプロパティダイアログを閉じます。

1. ページの書き出しを要求し、URLのサフィックス`html`を`export.zip`に置き換えます。

   次に例を示します。
   * localhost:4502/content/we-retail/language-masters/en.html

   次を介してアクセス：
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. アーカイブファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、必要に応じてファイルを解凍します。 展開すると、選択したページと同じ名前のフォルダーが作成されます。 このフォルダーには次が含まれます。

   * サブフォルダー`content`。リポジトリ内のページへのパスを反映した一連のサブフォルダーのルートです

      * この構造内には、選択されたページ(`<page-name>.html`)のhtmlファイルがあります
   * その他のリソース（`.js`ファイル、`.css`ファイル、画像など） は、書き出しテンプレートの設定に従って配置されます。


1. ブラウザーでページhtmlファイル(`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`)を開き、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、[コンテンツ同期フレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)に基づいています。 **ページプロパティ**&#x200B;ダイアログで使用できる設定は、ページに必要な依存関係を定義する書き出しテンプレートです。

ページの書き出しがトリガーされると、書き出しテンプレートが参照され、ページパスとデザインパスの両方が動的に適用されます。 その後、標準のコンテンツ同期機能を使用してzipファイルを作成します。

標準搭載のAEMインストールには、`/etc/contentsync/templates/default`の下にデフォルトのテンプレートが含まれています。

* このテンプレートは、リポジトリにエクスポートテンプレートが見つからない場合のフォールバックテンプレートです。

* `default`テンプレートは、ページエクスポートの設定方法を示し、新しい書き出しテンプレートのベースとして機能します。

* テンプレートのノード構造をJSON形式で表示するには、次のURLを要求します。
   `http://localhost:4502/etc/contentsync/templates/default.json`

新しいページエクスポーターテンプレートを作成する最も簡単な方法は次のとおりです。

* `default`テンプレートをコピーし、

* サイトに適した新しい名前を割り当て、

* 次に、必要な更新を行います。

完全に新しいテンプレートを作成するには：

1. **CRXDE Lite**&#x200B;に、`/etc/contentsync/templates`の下にノードを作成します。

   * `Name`:サイトに適した名前例えば、 `<mysite>`。ページエクスポーターテンプレートを選択すると、ページプロパティダイアログに名前が表示されます。

   * `Type`: `nt:unstructured`

2. テンプレートノード（ここでは `mysite`）の下に、以下で説明する設定ノードを使用してノード構造を作成します。

## ページのページエクスポータテンプレートのアクティブ化{#activating-a-page-exporter-configuration-for-your-pages}

テンプレートを設定したら、使用可能にする必要があります。

1. CRXDEで、`/content`ブランチの必要なページに移動します。 これは、個々のページ、またはサブツリーのルートページにすることができます。

1. ページの`jcr:content`ノードで、プロパティを作成します。
   * `Name`:  `cq:exportTemplate`
   * `Type`:  `String`
   * `Value`:テンプレートのパス例：  `/etc/contentsync/templates/mysite`

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

テンプレートは、[コンテンツ同期フレームワーク](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)を使用するノード構造で構成されます。  各ノードには`type`プロパティがあり、zipファイルの作成プロセスでの特定のアクションを定義します。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

書き出しテンプレートの作成には、次のノードを使用できます。

* `page`page ノードは、ページの HTML を zip ファイルにコピーする際に使用します。次のような特徴があります。

   * 必須ノードである。
   * `/etc/contentsync/templates/<mysite>`の下に配置されています。
   * `Name`プロパティを`page`に設定して定義します。
   * ノードタイプは`nt:unstructured`です

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
   * `/etc/contentsync/templates/<mysite>`の下に配置されています。
   * `Name`プロパティを`design`に設定して定義します。
   * ノードタイプは`nt:unstructured`です。

   `design` ノードには以下のプロパティがあります。

   * 値`copy`に設定された`type`プロパティ。

   * 現在のページパスは設定に動的にコピーされるので、`path`プロパティはありません。


* `generic`
汎用ノードは、clientlibsのようなリソースのコピーに使用されます。 
`.js` または `.css` ファイルをzipファイルに保存します。次の特性を持ちます。

   * オプションである。
   * `/etc/contentsync/templates/<mysite>`の下に配置されています。
   * 特定の名前を持たない。
   * ノードタイプは`nt:unstructured`です。
   * `type`プロパティと`type`関連するプロパティがあります。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   例えば、次の設定ノードは`mysite.clientlibs.js`ファイルをzipファイルにコピーします。

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

特定の要件を満たすには、[カスタム更新ハンドラ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)を実装する必要がある場合があります。

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことが可能です。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

zipファイルのダウンロードに問題が発生した場合は、リポジトリの`/var/contentsync`ノードを削除して、再度エクスポートリクエストを送信できます。
