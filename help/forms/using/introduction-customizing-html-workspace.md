---
title: AEM Forms Workspace のカスタマイズの概要
description: 概念的および技術的情報を含む、プロセス管理のためにAEM Forms Workspace をカスタマイズするLiveCycleの概要です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 23%

---

# AEM Forms Workspace のカスタマイズの概要{#introduction-to-customizing-aem-form-workspace}

AEM Forms Workspace では、プレゼンテーションセマンティックおよびインターフェイスの機能を変更することが可能です。スタイル、レイアウト、書式設定、ブランド、およびコア機能を変更するカスタマイズのタイプについては、以下に説明します。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

カスタマイズされた Workspace の例

## カスタマイズのタイプ {#types-of-customizations}

AEM Forms workspace は、様々なカスタマイズをサポートし、ユーザーインターフェイスのレイアウト、外観、機能などを更新します。 カスタマイズには、次の 1 つ以上を更新する必要があります。

* ユーザーインターフェイスの外観
* セマンティックのカスタマイズを使用する機能
* 他のアプリケーションでのHTMLコンポーネントの再利用

### ユーザーインターフェイスの変更 {#user-interface-changes}

AEM Forms Workspace の外観、レイアウト、およびその他の表示セマンティクスを変更できます。 CSS、ワークスペーステンプレートおよび JavaScript™ファイルをカスタマイズして、HTMLを変更します。 すべてのデフォルトファイルは、デフォルトのインストール環境で提供されます。

最も一般的な手順については、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)を参照してください。詳細な手順など、このようなカスタマイズの具体的な例については、この記事の最後にある関連記事を参照してください。

#### スタイルシートについて {#understanding-the-style-sheet}

Workspace をカスタマイズする前に、AEM Forms(/libs/ws/css/style.css) に付属するデフォルトのスタイルシートについて理解しておいてください。

ワークスペースをカスタマイズするには、/libs/ws/css フォルダー内の既存のスタイルシート (style.css) に慣れておくことをお勧めします。 以下では、主なコンポーネントの一部を説明します。

<table>
 <tbody>
  <tr>
   <th><p>CSS 要素</p> </th>
   <th><p>ユーザインターフェイスコンポーネントが変更されました</p> </th>
  </tr>
  <tr>
   <td><p>#ヘッダー</p> </td>
   <td><p>AEM Forms Workspace のヘッダー</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>カテゴリリスト</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>カテゴリリストのヘッダー</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>カテゴリリストの下のスペース</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>カテゴリ</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>選択したカテゴリとカテゴリのスタイルにマウスを移動</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool、categoryListBar .content</p> </td>
   <td><p>プロセスページを開始（閉じたカテゴリリスト）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>To Do ページ（閉じたフィルターリスト）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>トラッキングページ（閉じられたプロセス名リスト）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>スタートポイントリストまたはタスクリスト</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>スタートポイントリストまたはタスクリストのヘッダー</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>選択した開始点またはタスク</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected .description</p> </td>
   <td><p>選択したスタートポイントまたはタスクの説明</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>「タスク」領域</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>ヘッダーのユーザードロップダウン</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>並べ替えタスクドロップダウン</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms Workspace の表示方法は、CSS の表示方法を使用しています。CSS をカスタマイズすることで、フォント、色、ブランディング、レイアウトなど、ワークスペースのプレゼンテーションセマンティクスを変更できます。

CSS カスタマイズの最上位の手順は次のとおりです。

* CSS ファイルを作成します。
* この CSS にスタイル項目を追加します。 詳しくは、 CSS スタイルについてを参照してください。
* `html.jsp` の参照を更新します。

これらのカスタマイズを行うための正確な手順については、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)を参照してください。AEM Forms Workspace に付属している CSS ファイルは、/libs/ws/css/ にあります。CSS 関連のカスタマイズの場合は、 [出荷パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). CSS 関連のカスタマイズの具体的な例については、この記事の最後にある関連するヘルプトピックを参照してください。

#### 画像 {#image}

AEM Forms Workspace をカスタマイズしてユーザーのアバターを追加したり、組織のロゴを追加することができます。これらのカスタマイズの場合は、 [出荷パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

画像をカスタマイズするための最上位の手順は次のとおりです。

* WebDAV をインストールして設定します。
* 新しい画像を追加します。
* 追加した画像に対応する新しいスタイルを追加します。
* `html.jsp` ファイル内の新しい CSS ファイルにリンクします。

AEM Forms Workspace の画像のカスタマイズを開始するには、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)に従います。画像関連のカスタマイズの具体的な例については、この記事の最後にある関連するヘルプトピックを参照してください。

#### HTMLテンプレート {#html-template}

HTML テンプレートは、Workspace ユーザーインターフェイスの表示方法とレイアウトを定義するのに役立ちます。デフォルトのHTMLテンプレートを更新することで、レイアウトのデフォルトのユーザインターフェイスをカスタマイズできます。

テンプレートをカスタマイズするための最上位の手順は、次のとおりです。HTML

* ユーザーが作成したフォルダーで、必要なデフォルトファイルのコピーを作成します。
* ユーザー定義フォルダーに新しいテンプレートを追加します。
* コピーしたファイルに対して、新しいテンプレートのパスなど、関連する更新を行います。

このようなカスタマイズの具体的な例については、この記事の最後にあるヘルプトピックを参照してください。 次の中から選択： [出荷パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) または [開発パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)（カスタマイズするテンプレートに応じて）

### セマンティックの変更 {#semantic-changes}

AEM Forms Workspace の機能を変更するには、JavaScript ソースコードを変更します。コア機能の変更は、セマンティックの変更としてラベル付けされます。 AEM Forms Workspace のソースコードの一部として提供されているモデル、表示、テンプレートを変更します。

セマンティックの変更を行って AEM Forms Workspace の機能を変更するためのトップレベルの手順を次に示します。

* ユーザーが作成したフォルダーで、適切なデフォルトのファイルのコピーを作成します。
* ユーザー定義フォルダーに新しいモデルとビューを追加します。
* デフォルトの JavaScript ファイルで新しく追加されたモデルとビューのパスを更新するなど、関連する更新をおこないます。
* パッケージを縮小してパフォーマンスを最適化します。

ソースコードの一部であるコンポーネントの概念について詳しくは、 [再利用可能なコンポーネントの説明](/help/forms/using/description-reusable-components.md). これらのカスタマイズの場合は、開発パッケージを使用します。

### 再利用可能なコンポーネント {#reusable-components}

AEM Forms Workspace は容易にカスタマイズや再利用が可能なコンポーネントベースのソフトウェアです。Workspace コンポーネントを Web アプリケーションで容易に統合できます。

概念的な情報について詳しくは、[再利用可能なコンポーネントの詳細](/help/forms/using/description-reusable-components.md)を参照してください。コンポーネントを使用する手順について詳しくは、[Web アプリケーションでの AEM Forms Workspace コンポーネントの統合](/help/forms/using/description-reusable-components.md)を参照してください。

## AEM Forms Workspace コードの構築 {#building-html-workspace-code}

### SDK パッケージ {#sdk-package}

このパッケージには、AEM Forms Workspace のソースコードが含まれています。 パッケージは、`[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip` に格納されています。

これは主にカスタマイズを目的としており、次の機能を生成できます。

* Ship、Debug、および Dev プロファイル用の CRX パッケージ ( 以下で説明する [CRX パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)) をクリックします。
* カスタマイズされたコードの縮小バージョン（セマンティックの変更用）。

#### WS コンテンツ {#ws-content}

* client-pkg:

   * src - CRX ノードの作成に必要なアーティファクトが含まれます。
   * pom.xml — 様々なプロファイルのデプロイパッケージを構築するスクリプト WS-Deploy パッケージ

* client-html:

   * assembly - AEM Forms Workspace SDK を作成するスクリプトが使用する zip.xml を含みます。
   * src/main/webapp -

      * css - AEM Forms Workspace のスタイルシートを含みます。
      * images - AEM Forms Workspace で使用する画像を含みます。
      * js:

         * libs - AEM Forms Workspace で使用されるすべてのサードパーティライブラリを含みます。
         * licenses -HTMLファイルと JS ファイルのライセンス、およびこれらのライセンスの先頭に各ソースファイルを置くコードが含まれます。
         * minifier - カスタマイズされた JavaScript コードの結合、縮小および醜怪化に使用されます。
         * resourcejs_optimizer - JavaScript ソースの結合、縮小および醜怪化に使用されます。
         * resource_generator - register.js および modelcontrollerpath.js の生成に使用されます。
         * runtime:

            * initializer - AEM Forms Workspace で使用する Backbone ビューとモデルを初期化するために使用される initializer.js が含まれます。
            * models - AEM Forms Workspace に存在するすべてのコンポーネントのバックボーンモデルを含みます。
            * routes - AEM Forms Workspace に開始プロセス、todo、トラッキングおよび環境設定を読み込む JavaScript ファイルと HTML ファイルを含みます。
            * services - AEM Forms Workspace で使用される service.js が含まれます。 すべてのサーバー呼び出しは service.js を通じておこなわれます。
            * templates — すべてのテンプレート、つまりAEM Forms Workspace のすべてのビューのHTMLファイルを含みます。
            * util - AEM Forms Workspace で使用されるすべてのユーティリティファイル (javascript) を含みます。
            * views - AEM Forms workspace のすべてのコンポーネントのバックボーンビューを含みます。

         * main.js
         * router.js

      * libs/ws：pdf.html および pluginPing.pdf は、PDF フォームを AEM Forms Workspace に読み込むのに使用されます。WSNextAdapter.swf は、SWF フォームおよび Guide を AEM Forms Workspace に読み込むのに使用されます。
      * locales:

         * de-DE — ドイツ語の translation.json を含みます。
         * en-US — 英語の translation.json を含みます。
         * fr-FR — フランス語の translation.json を含みます。
         * ja-JP — 日本語の translation.json を含みます。
         * html.jsp — 現在のブラウザーのロケールを調べるコードを含みます。

      * html.jsp
      * GET.jsp

### CRX パッケージ {#crx-package}

CRX パッケージは CRX™リポジトリにデプロイできます。 これは、`[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip` に格納されています。

このパッケージは、以下の 3 つのプロフィルを使用して構築することができます。

| **プロファイル** | **説明** | **使用方法** |
|---|---|---|
| 出荷プロファイル | このプロファイルは、縮小化を使用して、可能な限り小さいサイズの CRX パッケージを作成します。 このパッケージは最も効率的です。 すべての JavaScript™ファイルが結合され、縮小されて 1 つの JS ファイルになります。 | JS ファイルでさらにセマンティックの変更が必要ない場合は、このプロファイルを使用します。 |
| プロファイルをデバッグ | このプロファイルは、適度に効率的な CRX パッケージを作成します。 パッケージのサイズは、Ship プロファイルを使用して作成したパッケージより少し大きくなります。 このパッケージには、ほとんどの JavaScript ファイルが単一の JS ファイルに結合されています。 | このプロファイルをデバッグに使用します。 |
| 開発プロファイル | このプロファイルは、可能な限り大きいサイズの CRX パッケージを作成します。 すべての JavaScript ファイルは SDK パッケージ内にあるので、個別に使用できます。 | セマンティックの変更を組み込む場合は、このプロファイルを使用します。 |

#### 出荷プロファイル {#ship-profile}

#### コマンド {#command}

* クライアントに出荷されたソースパッケージの client-pkg フォルダに対する mvn clean -P Ship install。
* Ship プロファイルコマンド実行は 64 ビット JVM でのみ 動作します。

#### WS コンテンツ {#ws-content-1}

* css - style.css、ie.css および jquery-ui.css を含みます。
* images — すべての画像を含みます。
* js:

   * libs:

      * require - require.js を含みます。
      * jqueryui - jquery.ui.datepicker.ja.jsを含みます。

   * runtime:

      * templates — すべてのテンプレート、つまりAEM Forms Workspace 内のすべてのコンポーネントのHTMLファイルを含みます。

   * main.js （組み合わせ、縮小および醜怪化）。
   * registry.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf が含まれます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE — ドイツ語の translation.json を含みます。
   * en-US — 英語の translation.json を含みます。
   * fr-FR — フランス語の translation.json を含みます。
   * ja-JP — 日本語の translation.json を含みます。
   * html.jsp — 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含む
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Debug Profile {#debug-profile}

#### コマンド {#command-1}

* client-pkg への mvn clean -P Debug install
* Debug プロファイルコマンドの実行は、64 ビット JVM でのみ機能します。

#### WS コンテンツ {#ws-content-2}

* css - style.css、ie.css および jquery-ui.css を含みます。
* images — すべての画像を含みます。
* js:

   * libs:

      * require - require.js を含みます。
      * jqueryui - jquery.ui.datepicker.ja.jsを含みます。

   * runtime:

      * templates — すべてのテンプレート、つまりAEM Forms Workspace 内のすべてのコンポーネントのHTMLファイルを含みます。

   * main.js （組み合わせ）
   * registry.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf が含まれます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE — ドイツ語の translation.json を含みます。
   * en-US — 英語の translation.json を含みます。
   * fr-FR — フランス語の translation.json を含みます。
   * ja-JP — 日本語の translation.json を含みます。
   * html.jsp — 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含む
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 開発プロファイル {#dev-profile}

#### コマンド {#command-2}

client-pkg への mvn clean -P Dev install

#### WS コンテンツ {#ws-content-3}

* css - style.css、ie.css および jquery-ui.css を含みます。
* images — すべての画像を含みます。
* js:

   * libs - AEM Forms Workspace で使用されるすべてのライブラリを含みます。
   * require - require.js を含みます。
   * jqueryui - jquery.ui.datepicker.ja.jsを含む
   * runtime:

      * initializer - initializer.js と modelcontrollerpath.js が含まれます。
      * models - AEM Forms Workspace のすべてのコンポーネントのモデルが含まれます。
      * routes - AEM Forms Workspace に開始プロセス、todo、トラッキングおよび環境設定を読み込む JavaScript ファイルと HTML ファイルを含みます。
      * services - AEM Forms Workspace で使用される service.js が含まれます。
      * templates — すべてのテンプレート、つまりAEM Forms Workspace 内のすべてのコンポーネントのHTMLファイルを含みます。
      * util - AEM Forms Workspace で使用されるすべてのユーティリティファイル (JavaScript) が含まれます。
      * views - AEM Forms Workspace のすべてのコンポーネントのビューを含みます。

   * main.js
   * registry.js
   * router.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf が含まれます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE — ドイツ語の translation.json を含みます。
   * en-US — 英語の translation.json を含みます。
   * fr-FR — フランス語の translation.json を含みます。
   * ja-JP — 日本語の translation.json を含みます。
   * html.jsp — 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含む
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
