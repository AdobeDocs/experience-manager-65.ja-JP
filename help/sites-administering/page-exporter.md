---
title: ページエクスポーター
description: Adobe Experience Manager(AEM) ページエクスポーターの使用方法を説明します。
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 66%

---

# ページエクスポーター{#the-page-exporter}

Adobe Experience Manager(AEM) では、画像を含む完全な Web ページとしてページを書き出すことができます。 `.js`、および `.css` ファイル。

設定した場合、 `html` 次を使用 `export.zip` 」と入力します。 これにより、HTML 形式でレンダリングされたページと参照元のアセットを含む、アーカイブ（zip）ファイルが生成されます。ページ内のすべてのパス（例えば、画像へのパス）は、アーカイブに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。アーカイブ（zip）ファイルは、ブラウザーからダウンロードできます。

>[!NOTE]
>
>ブラウザーと設定に応じて、ダウンロードは次のいずれかになります。
>
>* アーカイブファイル（`<page-name>.export.zip`）
>* フォルダー（`<page-name>`）（アーカイブファイルを実際に展開済み）

## ページのエクスポート {#exporting-a-page}

次の手順では、ページをエクスポートする方法を説明します。サイトにエクスポートテンプレートが存在すると仮定しています。書き出しテンプレートは、ページの書き出し方法を定義し、サイトに固有のものです。 エクスポートテンプレートを作成するには、 [サイト用のページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site).

ページをエクスポートするには：

1. **Sites** コンソールで、対象のページに移動します。

1. ページを選択して、「**プロパティ**」ダイアログを開きます。

1. 「**詳細**」タブを選択します。

1. 「**エクスポート**」フィールドを展開して、エクスポートテンプレートを選択します。
サイトに必要なテンプレートを選択し、「**OK**」で確定します。

1. 「**保存して閉じる**」を選択して、ページプロパティのダイアログを閉じます。

1. ページのエクスポートをリクエストし、URL のサフィックス `html` を `export.zip` に置き換えます。

   次は例です。
   * localhost:4502/content/we-retail/language-masters/en.html

   次の方法でアクセス：
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. アーカイブファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、必要に応じてそのファイルを解凍します。展開すると、選択したページと同じ名前のフォルダーが存在します。 このフォルダーには次が含まれます。

   * サブフォルダー `content`：リポジトリ内のページへのパスを反映した一連のサブフォルダーのルート。

      * この構造の中に、選択したページの html ファイルがあります（`<page-name>.html`）

   * その他のリソース (`.js` ファイル、 `.css` ファイルや画像など ) は、エクスポートテンプレートの設定に従って配置されます。

1. ページの HTML ファイル (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) をブラウザーで確認して、レンダリングを確認できるようにします。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、[コンテンツ同期フレームワーク](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)に基づいています。「**ページプロパティ**」ダイアログで利用できる設定は、ページに必要な依存関係を定義するエクスポートテンプレートです。

ページの書き出しがトリガーされると、書き出しテンプレートが参照されます。ページパスとデザインパスの両方が動的に適用されます。 その後、標準のコンテンツ同期機能を使用して、zip ファイルが作成されます。

標準インストールの AEM では、`/etc/contentsync/templates/default` の下にデフォルトテンプレートが含まれています。

* このテンプレートは、リポジトリ内にエクスポートテンプレートが見つからない場合のフォールバックテンプレートです。

* `default` テンプレートは、ページをエクスポートするための設定方法を示していて、新しいエクスポートテンプレートのベースとして使用できます。

* テンプレートのノード構造を JSON 形式でブラウザーに表示するには、次の URL をリクエストします。
  `http://localhost:4502/etc/contentsync/templates/default.json`

ページエクスポーターテンプレートを作成する最も簡単な方法は次のとおりです。

* `default` テンプレートをコピーします。

* サイトに適した新しい名前を割り当て、

* その上で、必要な更新を行います。

完全に新しいテンプレートを作成するには：

1. **CRXDE Lite** で、`/etc/contentsync/templates` の下にノードを作成します。

   * `Name`：サイトに適した名前（例：`<mysite>`）。ページエクスポーターテンプレートを選択すると、この名前がページプロパティのダイアログボックスに表示されます。

   * `Type`：`nt:unstructured`

2. テンプレートノード（ここでは `mysite`）の下に、次で説明する設定ノードを使用してノード構造を作成します。

## ページのページエクスポーターテンプレートのアクティブ化 {#activating-a-page-exporter-configuration-for-your-pages}

テンプレートを設定したら、使用可能にします。

1. CRXDE で `/content` の分岐の対象ページに移動します。個々のページ、またはサブツリーのルートページを指定できます。

1. 次の日： `jcr:content` ページのノードで、次のプロパティを作成します。
   * `Name`：`cq:exportTemplate`
   * `Type`：`String`
   * `Value`：テンプレートへのパス（例： `/etc/contentsync/templates/mysite`）

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

[コンテンツ同期フレームワーク](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html)を使用しているため、テンプレートはノード構造で構成されています。各ノードには、zip ファイルの作成プロセスで特定のアクションを定義する `type` プロパティが含まれています。

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

次のノードを使用してエクスポートテンプレートを作成することができます。

* `page`
page ノードを使用して、ページの HTML を zip ファイルにコピーします。次のような特徴があります。

   * 必須ノードです。
   * 次の場所にあります。 `/etc/contentsync/templates/<mysite>`.
   * プロパティで定義 `Name`に設定 `page`.
   * ノードタイプは `nt:unstructured`

  `page` ノードには以下のプロパティがあります。

   * 値 `pages` が設定された `type` プロパティ。

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
rewrite ノードでは、エクスポートしたページでリンクを書き換える方法を定義します。書き換え後のリンクは、zip ファイルに含まれるファイルを指すか、サーバー上のリソースを指します。
  <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
design ノードを使用して、エクスポートされるページに使用されているデザインをコピーします。次のような特徴があります。

   * オプション.
   * 次の場所にあります。 `/etc/contentsync/templates/<mysite>`.
   * プロパティで定義 `Name` に設定 `design`.
   * ノードタイプは `nt:unstructured`.

  `design` ノードには次のプロパティがあります。

   * 値 `copy` に設定された `type` プロパティ。

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* `generic`
汎用ノードを使用して、clientlibs などのリソースをコピーできます。`.js` ファイルまたは `.css` ファイルを zip ファイルへ。次のような特徴があります。

   * オプション.
   * 次の場所にあります。 `/etc/contentsync/templates/<mysite>`.
   * 特定の名前はありません。
   * ノードタイプは `nt:unstructured`.
   * `type` プロパティと `type` に関連したプロパティを持ちます。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  例えば、次の設定ノードは `mysite.clientlibs.js` ファイルを zip ファイルにコピーします。

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

特定の要件を満たすには、 [カスタム更新ハンドラー](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## プログラムによるページのエクスポート {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、 [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGi サービス。 このサービスを使用すると、次のことができます。

* ページを書き出し、HTTP サーブレット応答に書き込みます。
* ページを書き出し、zip ファイルを特定の場所に保存します。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

Zip ファイルのダウンロードで問題が発生した場合は、リポジトリで `/var/contentsync` ノードを削除して、エクスポートリクエストを再度送信できます。
