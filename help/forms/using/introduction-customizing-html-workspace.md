---
title: AEM Forms Workspace のカスタマイズの概要
description: LiveCycle AEM Forms Workspace をカスタマイズしてプロセス管理を行う方法の概念と技術情報を簡単に紹介します。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 100%

---

# AEM Forms Workspace のカスタマイズの概要{#introduction-to-customizing-aem-form-workspace}

AEM Forms Workspace では、プレゼンテーションセマンティックおよびインターフェイスの機能を変更することが可能です。スタイル、レイアウト、書式設定、ブランド、およびコア機能を変更するカスタマイズのタイプについては、以下に説明します。

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

カスタマイズされた Workspace の例

## カスタマイズの種類 {#types-of-customizations}

AEM Forms Workspace では、幅広く様々なカスタマイズをサポートしてユーザーインターフェイスのレイアウト、その表示方法、機能などを更新します。カスタマイズでは次の 1 つ以上を更新します。

* ユーザーインターフェイスの表示方法
* セマンティックのカスタマイズを使用した機能
* 他のアプリケーションでの HTML コンポーネントの再利用

### ユーザーインターフェイスの変更 {#user-interface-changes}

AEM Forms Workspace の表示方法、レイアウトおよびその他のプレゼンテーションセマンティックを変更できます。CSS、HTML テンプレートおよび JavaScript™ ファイルをカスタマイズすることによって、Workspace を変更します。すべてのデフォルトファイルはデフォルトのインストールで提供されます。

最も一般的な手順については、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)を参照してください。詳細な手順を含む、カスタマイズの特殊な例については、この記事の最後にある関連項目を参照してください。

#### スタイルシートについて {#understanding-the-style-sheet}

Workspace をカスタマイズする前に、/libs/ws/css/style.css にある AEM Forms 付属のデフォルトスタイルシートを理解しておくことをお勧めします。

Workspace をカスタマイズするには、/libs/ws/css フォルダー内にある既存のスタイルシート style.css を理解しておくことをお勧めします。いくつかの主なコンポーネントを以下に説明します。

<table>
 <tbody>
  <tr>
   <th><p>CSS 要素</p> </th>
   <th><p>変更されたユーザーインターフェイスコンポーネント</p> </th>
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
   <td><p>.categories、.filters</p> </td>
   <td><p>カテゴリリストの下の空白</p> </td>
  </tr>
  <tr>
   <td><p>.category、.filter</p> </td>
   <td><p>カテゴリ</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover、.category.selected、.filter:hover、.filter.selected</p> </td>
   <td><p>選択されたカテゴリとカテゴリのマウスオーバースタイル</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool、categoryListBar .content</p> </td>
   <td><p>開始プロセスページ（終了したカテゴリリスト）</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool、filterListBar .content</p> </td>
   <td><p>To Do ページ（終了したフィルターリスト）</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool、processNameListBar .content</p> </td>
   <td><p>トラッキングページ（終了したプロセス名リスト）</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList、.tasklist</p> </td>
   <td><p>スタートポイントリストまたはタスクリスト</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header、.tasklist .header</p> </td>
   <td><p>スタートポイントリストまたはタスクリストのヘッダー</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected、.task.selected</p> </td>
   <td><p>選択されたスタートポイントまたはタスク</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description、.task.selected.description</p> </td>
   <td><p>選択されたスタートポイントまたはタスクの説明</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>タスク領域</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>ヘッダー内のユーザードロップダウン</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>タスクの並べ替えドロップダウン</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms Workspace の表示方法は、CSS の表示方法を使用しています。CSS をカスタマイズすることにより、フォント、カラー、ブランド、レイアウトなどの Workspace のプレゼンテーションセマンティックを変更できます。

CSS カスタマイズのためのトップレベルの手順を次に示します。

* CSS ファイルを作成します。
* この CSS にスタイルアイテムを追加します。詳しくは、CSS スタイルについてを参照してください。
* `html.jsp` の参照を更新します。

これらのカスタマイズを行うための正確な手順については、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)を参照してください。AEM Forms Workspace に付属している CSS ファイルは、/libs/ws/css/ にあります。CSS 関連のカスタマイズの場合は、[Ship パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を使用します。CSS 関連のカスタマイズの特殊な例について詳しくは、この記事の最後にある関連ヘルプトピックを参照してください。

#### 画像 {#image}

AEM Forms Workspace をカスタマイズしてユーザーのアバターを追加したり、組織のロゴを追加することができます。これらのカスタマイズの場合は、[Ship パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)を使用します。

画像をカスタマイズするためのトップレベルの手順を次に示します。

* WebDAV をインストールして設定します。
* 新しい画像を追加します。
* 追加した画像に対応する新しいスタイルを追加します。
* `html.jsp` ファイル内の新しい CSS ファイルにリンクします。

AEM Forms Workspace の画像のカスタマイズを開始するには、[AEM Forms Workspace カスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)に従います。画像に関係するカスタマイズの特殊な例について詳しくは、この記事の最後にある関連ヘルプトピックを参照してください。

#### HTML テンプレート {#html-template}

HTML テンプレートは、Workspace ユーザーインターフェイスの表示方法とレイアウトを定義するのに役立ちます。デフォルトの HTML テンプレートを更新することによって、デフォルトのユーザーインターフェイスのレイアウトをカスタマイズできます。

HTML テンプレートをカスタマイズするためのトップレベルの手順を次に示します。

* ユーザーが作成したフォルダーで、必要なデフォルトのファイルのコピーを作成します。
* 新しいテンプレートをユーザー定義フォルダーに追加します。
* 新しいテンプレートのパスなど、コピーしたファイルに関連する更新を行います。

このようなカスタマイズの特殊な例について詳しくは、この記事の最後にある関連ヘルプトピックを参照してください。カスタマイズするテンプレートに応じて、[Ship パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)または [Dev パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)のいずれかを選択します。

### セマンティックの変更 {#semantic-changes}

AEM Forms Workspace の機能を変更するには、JavaScript ソースコードを変更します。コア機能の変更は、セマンティックの変更としてラベル付けされます。AEM Forms Workspace のソースコードの一部として、モデル、ビューおよびテンプレートを変更します。

セマンティックの変更を行って AEM Forms Workspace の機能を変更するためのトップレベルの手順を次に示します。

* ユーザーが作成したフォルダーで、該当するデフォルトのファイルのコピーを作成します。
* ユーザー定義フォルダーに新しいモデルおよびビューを追加します。
* デフォルトの JavaScript ファイルで新しく追加したモデルおよびビューのパスを更新するなど、関連する更新を行います。
* パッケージを縮小してパフォーマンスを最適化します。

ソースコードの一部であるコンポーネントに関する概念情報について詳しくは、[再利用可能なコンポーネントの説明](/help/forms/using/description-reusable-components.md)を参照してください。これらのカスタマイズの場合は、Dev パッケージを使用します。

### 再利用可能なコンポーネント {#reusable-components}

AEM Forms Workspace は容易にカスタマイズや再利用が可能なコンポーネントベースのソフトウェアです。Workspace コンポーネントを Web アプリケーションで容易に統合できます。

概念的な情報について詳しくは、[再利用可能なコンポーネントの詳細](/help/forms/using/description-reusable-components.md)を参照してください。コンポーネントを使用する手順について詳しくは、[Web アプリケーションでの AEM Forms Workspace コンポーネントの統合](/help/forms/using/description-reusable-components.md)を参照してください。

## AEM Forms Workspace コードの構築 {#building-html-workspace-code}

### SDK パッケージ {#sdk-package}

パッケージには AEM Forms Workspace のソースコードが含まれます。パッケージは、`[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip` に格納されています。

これは主としてカスタマイズ向けで、次を生成する機能を提供します。

* Ship、Debug および Dev プロファイルの CRX パッケージ（下記の [CRX パッケージ](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)に記載しています）
* カスタマイズされたコードの縮小バージョン（セマンティックの変更用）

#### WS コンテンツ {#ws-content}

* client-pkg:

   * src - CRX ノードを作成するのに必要なアーティファクトを含みます。
   * pom.xml - 様々なプロファイルのデプロイパッケージを構築するスクリプト（WS - デプロイパッケージ）

* client-html:

   * assembly - AEM Forms Workspace SDK を作成するスクリプトが使用する zip.xml を含みます。
   * src/main/webapp -

      * css - AEM Forms Workspace のスタイルシートを含みます。
      * images - AEM Forms Workspace で使用する画像を含みます。
      * js:

         * libs - AEM Forms Workspace で使用されているすべてのサードパーティライブラリを含みます。
         * licenses - HTML と JS ファイルのライセンスおよびこれらのライセンスをそれぞれのソースファイルの前に置くコードを含みます。
         * minifier - カスタマイズされた JavaScript コードの結合、縮小および醜怪化に使用されます。
         * resourcejs_optimizer - JavaScript ソースの結合、縮小および醜怪化に使用されます。
         * resource_generator - register.js および modelcontrollerpath.js の生成に使用されます。
         * runtime:

            * initializer - AEM Forms Workspace で使用するバックボーンビューやモデルの初期化に使用する initializer.js を含みます。
            * models - AEM Forms Workspace にあるすべてのコンポーネントのバックボーンモデルを含みます。
            * routes - AEM Forms Workspace に開始プロセス、todo、トラッキングおよび環境設定を読み込む JavaScript ファイルと HTML ファイルを含みます。
            * services - AEM Forms Workspace 内で使用される service.js を含みます。すべてのサーバー呼び出しは service.js を介して行われます。
            * templates - AEM Forms Workspace 内にあるすべてのテンプレート、すなわちすべてのビューの HTML ファイルを含みます。
            * util - AEM Forms Workspace 内で使用されているすべてのユーティリティファイル（JavaScript）を含みます。
            * views - AEM Forms Workspace 内のすべてのコンポーネントのバックボーンビューを含みます。

         * main.js
         * router.js

      * libs/ws：pdf.html および pluginPing.pdf は、PDF フォームを AEM Forms Workspace に読み込むのに使用されます。WSNextAdapter.swf は、SWF フォームおよび Guide を AEM Forms Workspace に読み込むのに使用されます。
      * locales:

         * de-DE - ドイツ語の translation.json を含みます。
         * en-US - 英語の translation.json を含みます。
         * fr-FR - フランス語の translation.json を含みます。
         * ja-JP - 日本語の translation.json を含みます。
         * html.jsp - 現在のブラウザーのロケールを調べるコードを含みます。

      * html.jsp
      * GET.jsp

### CRX パッケージ {#crx-package}

CRX パッケージは CRX™ リポジトリにデプロイできます。これは、`[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip` に格納されています。

このパッケージは、以下の 3 つのプロフィルを使用して構築することができます。

| **プロファイル** | **説明** | **使用方法** |
|---|---|---|
| Ship プロファイル | このプロファイルは縮小を使用して最も小さい CRX パッケージを作成します。このパッケージが最も効率的です。すべての JavaScript™ ファイルは単一の JS ファイルに結合されて縮小されます。 | このプロファイルは、JS ファイルにこれ以上セマンティックの変更が必要でない場合に使用します。 |
| Debug プロファイル | このプロファイルは、適度に効率的な CRX パッケージを作成します。このパッケージのサイズは、Ship プロファイルを使用して作成したパッケージよりも若干大きくなります。このパッケージにはほとんどの JavaScript ファイルが単一の JS ファイルに結合されています。 | このプロファイルはデバッグに使用します。 |
| Dev プロファイル | このプロファイルは、最も大きなサイズの CRX パッケージを作成します。すべての JavaScript ファイルは SDK パッケージ内にあるため、別々に利用できます。 | セマンティックの変更を組み込む場合はこのプロファイルを使用します。 |

#### Ship プロファイル {#ship-profile}

#### コマンド {#command}

* クライアントに出荷されるソースパッケージの client-pkg フォルダーへの mvn clean -P Ship インストール
* Ship プロファイルコマンド実行は 64 ビット JVM でのみ 動作します。

#### WS コンテンツ {#ws-content-1}

* css - style.css、ie.css および jquery-ui.css を含みます。
* images - すべての画像を含みます。
* js:

   * libs:

      * require - require.js を含みます。
      * jqueryui - jquery.ui.datepicker.ja.js を含みます。

   * runtime:

      * templates - AEM Forms Workspace 内にあるすべてのテンプレート、すなわちすべてのコンポーネントの HTML ファイルを含みます。

   * main.js（combined、minified および uglified）。
   * registry.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf を含みます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE - ドイツ語の translation.json を含みます。
   * en-US - 英語の translation.json を含みます。
   * fr-FR - フランス語の translation.json を含みます。
   * ja-JP - 日本語の translation.json を含みます。
   * html.jsp - 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含みます。
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Debug プロファイル {#debug-profile}

#### コマンド {#command-1}

* client-pkg への mvn clean -P Debug インストール
* Debug プロファイルコマンド実行は 64 ビット JVM でのみ機能します。

#### WS コンテンツ {#ws-content-2}

* css - style.css、ie.css および jqueri-ui.css を含みます。
* images - すべての画像を含みます。
* js:

   * libs:

      * require - require.js を含みます。
      * jqueryui - jquery.ui.datepicker.ja.js を含みます。

   * runtime:

      * templates - AEM Forms Workspace 内にあるすべてのテンプレート、すなわちすべてのコンポーネントの HTML ファイルを含みます。

   * main.js（組み合わせ）
   * registry.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf を含みます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE - ドイツ語の translation.json を含みます。
   * en-US - 英語の translation.json を含みます。
   * fr-FR - フランス語の translation.json を含みます。
   * ja-JP - 日本語の translation.json を含みます。
   * html.jsp - 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含みます。
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Dev プロファイル {#dev-profile}

#### コマンド {#command-2}

client-pkg への mvn clean -P Dev インストール

#### WS コンテンツ {#ws-content-3}

* css - style.css、ie.css および jqueri-ui.css を含みます。
* images - すべての画像を含みます。
* js:

   * libs - AEM Forms Workspace で使用されるすべてのライブラリを含みます。
   * require - require.js を含みます。
   * jqueryui - jquery.ui.datepicker.ja.js を含みます。
   * runtime:

      * initializer - initializer.js と modelcontrollerpath.js を含みます。
      * models - AEM Forms Workspace 内のすべてのコンポーネントのモデルを含みます。
      * routes - AEM Forms Workspace に開始プロセス、todo、トラッキングおよび環境設定を読み込む JavaScript ファイルと HTML ファイルを含みます。
      * services - AEM Forms Workspace 内で使用される service.js を含みます。
      * templates - AEM Forms Workspace 内にあるすべてのテンプレート、すなわちすべてのコンポーネントの HTML ファイルを含みます。
      * util - AEM Forms Workspace 内で使用されているすべてのユーティリティファイル（JavaScript）を含みます。
      * views - AEM Forms Workspace 内のすべてのコンポーネントのビューを含みます。

   * main.js
   * registry.js
   * router.js

* libs:

   * ws - pluginPing.pdf、pdf.html および WSNextAdapter.swf を含みます。

* Locale - .content.xml を含みます。
* locales:

   * de-DE - ドイツ語の translation.json を含みます。
   * en-US - 英語の translation.json を含みます。
   * fr-FR - フランス語の translation.json を含みます。
   * ja-JP - 日本語の translation.json を含みます。
   * html.jsp - 現在のブラウザーのロケールを調べるコードを含みます。

* Index - .content.xml を含みます。
* profile - offline.jsp を含みます。
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
