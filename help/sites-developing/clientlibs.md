---
title: クライアントサイドライブラリの使用
description: AEMにはクライアントサイドライブラリフォルダーが用意されています。これを使用すると、クライアントサイドコードをリポジトリに保存し、カテゴリに整理し、コードの各カテゴリをクライアントに提供するタイミングと方法を定義できます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 91%

---

# クライアントサイドライブラリの使用{#using-client-side-libraries}

最近の web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題に対処するために、AEMでは次の機能を提供しています。 **クライアント側ライブラリフォルダー**：クライアント側コードをリポジトリに保存し、カテゴリに整理し、コードの各カテゴリをクライアントに提供するタイミングと方法を定義できます。 その後、クライアントサイドライブラリシステムは、正しいコードを読み込むための正しいリンクを最終的な Web ページに生成する処理をおこないます。

## AEMでのクライアント側ライブラリの仕組み {#how-client-side-libraries-work-in-aem}

クライアントサイドライブラリ（JS ファイルまたは CSS ファイル）をページの HTML に含めるための標準的な方法は、`<script>` タグまたは `<link>` タグを使用して、そのページの JSP に該当するファイルのパスを含めることです。例：

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

この方法は AEM で機能しますが、ページやそれに含まれるコンポーネントが複雑になると、問題につながる可能性があります。そのような場合、同じ JS ライブラリの複数のコピーが最終的な HTML 出力に含まれる危険性があります。これを回避してクライアントサイドライブラリを論理的に整理するために、AEM では&#x200B;**クライアントサイドライブラリフォルダー**&#x200B;を使用します。

クライアントサイドライブラリフォルダーは、タイプが `cq:ClientLibraryFolder` のリポジトリノードです。[CND 注釈](https://jackrabbit.apache.org/node-type-notation.html)での定義は次のとおりです。

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

デフォルトでは、`cq:ClientLibraryFolder` ノードは、リポジトリのサブツリーである `/apps`、`/libs` および `/etc` 内であればどこにでも配置できます（これらのデフォルト、およびその他の設定は、[システムコンソール](https://localhost:4502/system/console/configMgr)の **Adobe Granite HTML ライブラリマネージャー**&#x200B;パネルで制御できます）。

各 `cq:ClientLibraryFolder` には、JS ファイルや CSS ファイルのセットと、いくつかのサポートファイルが入力されます（以下を参照）。`cq:ClientLibraryFolder` の重要なプロパティは、次のように設定されます。

* `categories`：`cq:ClientLibraryFolder` に含まれる JS ファイルや CSS ファイルのセットのカテゴリを特定します。`categories` プロパティは複数の値を取るため、ライブラリフォルダーを複数のカテゴリの一部にすることができます（これがどのように役立つかについては以下を参照）。

* `dependencies`：これは、このライブラリカテゴリが依存する他のクライアントライブラリフォルダーのリストです。例えば、`F` と `G` の 2 つの `cq:ClientLibraryFolder` ノードを指定し、`F` のファイルが正しく機能するために、別の `G` にあるファイルが必要な場合、`G` のうち 1 つ以上の `categories` は、`F` の `dependencies` に含まれている必要があります。

* `embed`：他のライブラリからコードを埋め込むために使用します。ノード F がノード G および H を埋め込むと、結果として得られる HTML は、ノード G および H からのコンテンツの合成になります。
* `allowProxy`：クライアントライブラリが `/apps` の下にある場合、このプロパティを使用すると、プロキシサーブレット経由でクライアントライブラリにアクセスできます。後述の[クライアントライブラリのフォルダーの配置とプロキシクライアントライブラリのサーブレットの使用](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)を参照してください。

## クライアント側ライブラリの参照 {#referencing-client-side-libraries}

AEMサイトの開発には HTL が推奨されるテクノロジーなので、AEMにクライアント側ライブラリを含めるには HTL を使用する必要があります。 ただし、JSP を使用しておこなうこともできます。

### HTL の使用 {#using-htl}

HTL では、クライアントライブラリは AEM 提供のヘルパーテンプレートを介して読み込まれます。テンプレートには [`data-sly-use`](https://helpx.adobe.com/jp/experience-manager/htl/using/block-statements.html#use) を使用してアクセスできます。このファイルには 3 つのテンプレートが含まれ、[`data-sly-call`](https://helpx.adobe.com/jp/experience-manager/htl/using/block-statements.html#template-call) で呼び出すことができます。

* **css** - 参照されるクライアントライブラリの CSS ファイルのみを読み込みます。
* **js** - 参照されるクライアントライブラリの JavaScript ファイルのみを読み込みます.
* **all** - 参照されるクライアントライブラリのすべてのファイル（CSS と JavaScript の両方）を読み込みます。

各ヘルパーテンプレートには、必要なクライアントライブラリを参照するための `categories` オプションを指定できます。このオプションには、文字列値の配列またはコンマ区切り値のリストを含む文字列を指定できます。

詳細および使用例については、[HTML テンプレート言語の使用の手引き](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html?lang=ja#loading-client-libraries)ドキュメントを参照してください。

### JSP の使用 {#using-jsp}

`ui:includeClientLib` タグを JSP コードに追加して、生成した HTML ページにクライアントライブラリへのリンクを追加します。ライブラリを参照するには、`ui:includeClientLib` ノードの `categories` プロパティの値を使用します。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例えば、 `/etc/clientlibs/foundation/jquery` ノードのタイプは、`cq.jquery` 値の categories プロパティを持つ `cq:ClientLibraryFolder` です。JSP ファイル内の以下のコードは、ライブラリを参照します。

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成されたHTMLページには、次のコードが含まれます。

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

JS、CSS またはテーマライブラリをフィルタリングするための属性を含め、詳しくは、 [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>` は、以前はクライアントライブラリを含めるために一般的に使用されていましたが、AEM 5.6 から非推奨（廃止予定）となりました。したがって、上記のとおり [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib)  を代わりに使用する必要があります。

## クライアントライブラリフォルダーの作成 {#creating-client-library-folders}

`cq:ClientLibraryFolder` ノードを作成して、JavaScript およびカスケードスタイルシートライブラリを定義し、それらを HTML ページで使用できるようにします。ノードの `categories` プロパティを使用して、ノードが属するライブラリカテゴリを特定します。

ノードには、実行時に単一の JS ファイルや CSS ファイルに結合される 1 つ以上のソースファイルが含まれます。生成されるファイルの名前はノード名で、ファイル名の拡張子は `.js` または `.css` です。例えば、`cq.jquery` という名前のライブラリノードからは、 `cq.jquery.js` または `cq.jquery.css` という名前のファイルが生成されます。

クライアントライブラリフォルダーには次の項目が含まれます。

* JS／CSS ソースファイル（いずれかまたは両方）を結合します。
* 画像ファイルなど、CSS スタイルをサポートするリソース。

  **メモ：**&#x200B;サブフォルダーを使用してソースファイルを整理できます。
* 生成される JS／CSS ファイルに統合するソースファイルを識別する、1 つの `js.txt` ファイルと 1 つの `css.txt` ファイル（いずれかまたは両方）。

![clientlibarch](assets/clientlibarch.png)

ウィジェット用のクライアントライブラリ特有の要件について詳しくは、[ウィジェットの使用および拡張](/help/sites-developing/widgets.md)を参照してください。

Web クライアントには、`cq:ClientLibraryFolder` ノードにアクセスする許可が必要です。また、リポジトリの保護された領域からライブラリを公開することもできます（以下の「他のライブラリからのコードの埋め込み」を参照）。

### /lib でのライブラリの上書き {#overriding-libraries-in-lib}

`/apps` にあるクライアントライブラリフォルダーは、`/libs` にある同じ名前のフォルダーよりも優先されます。例えば、`/apps/cq/ui/widgets` は `/libs/cq/ui/widgets` よりも優先されます。これらのライブラリが同じカテゴリに属する場合、`/apps` の下にあるライブラリが使用されます。

### クライアントライブラリフォルダーの配置とプロキシクライアントライブラリサーブレットの使用 {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

以前のバージョンでは、クライアントライブラリフォルダーは、リポジトリの `/etc/clientlibs` の下にありました。これは引き続きサポートされますが、クライアントライブラリを `/apps` の下に配置することをお勧めします。これは、クライアントライブラリを他のスクリプトの近くに配置するためです。他のスクリプトは、通常、`/apps` と `/libs` の下にあります。

>[!NOTE]
>
>クライアントライブラリフォルダーの下にある静的リソースは、*resources* というフォルダーに配置する必要があります。*resources* フォルダーの下に画像などの静的リソースがない場合、公開インスタンスで参照することはできません。以下に例を示します。https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>コードをコンテンツと設定からより詳細に分離するには、以下の場所にクライアントライブラリを配置することをお勧めします。 `/apps` を介して公開します。 `/etc.clientlibs` ～を活用して `allowProxy` プロパティ。

`/apps` にあるクライアントライブラリにアクセスできるようにするために、プロキシサーブレットが使用されます。ACL は依然としてクライアントライブラリフォルダーで適用されますが、サーブレットを使用すると、`/etc.clientlibs/` プロパティが `allowProxy` に設定されている場合、`true` を介してコンテンツを読み取ることができます。

静的リソースは、クライアントライブラリフォルダーの下のリソースにある場合、プロキシ経由でのみアクセスできます。

次に例を示します。

* clientlib は `/apps/myproject/clientlibs/foo` にあります。
* 静的画像は `/apps/myprojects/clientlibs/foo/resources/icon.png` にあります。

次に、`foo` の `allowProxy` プロパティを true に設定します。

* `/etc.clientlibs/myprojects/clientlibs/foo.js` をリクエストできます
* `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png` から画像を参照できます

>[!CAUTION]
>
>プロキシを使用したクライアントライブラリを使用している場合、拡張子 clientlibs を含む URI を許可するように AEM Dispatcher 設定を更新する必要が生じる場合があります。

>[!CAUTION]
>
>アドビでは、クライアントライブラリを `/apps` の下に配置し、プロキシサーブレットを使用して利用できるようにすることをお勧めします。ただし、ベストプラクティスとしては、依然として、`/apps` または `/libs` パスから直接提供されたものを何も含まない公開サイトが必要です。

### クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

1. Web ブラウザーで CRXDE Lite を開きます（[https://localhost:4502/crx/de](https://localhost:4502/crx/de)）。
1. クライアントライブラリフォルダーの配置先のフォルダーを選択して、**作成／ノードを作成**&#x200B;をクリックします。
1. ライブラリファイルの名前を入力し、タイプリストで `cq:ClientLibraryFolder` を選択します。「**OK**」をクリックし、「**すべて保存**」をクリックします。
1. ライブラリが所属するカテゴリ（1 つまたは複数）を指定するには、`cq:ClientLibraryFolder` ノードを選択し、次のプロパティを追加して、「**すべて保存**」をクリックします。

   * 名前：categories
   * タイプ：String
   * 値：カテゴリ名
   * 複数：選択

1. 何らかの方法で、ソースファイルをライブラリフォルダーに追加します。例えば、WebDav クライアントを使用してファイルをコピーする、ファイルを作成してコンテンツを手動で作成する、などの方法があります。

   **メモ：**&#x200B;必要に応じて、サブフォルダーを使用してソースファイルを整理できます。

1. クライアントライブラリフォルダーを選択して、**作成／ファイルを作成**&#x200B;をクリックします。
1. ファイル名ボックスに、次のいずれかのファイル名を入力して、「OK」をクリックします。

   * **`js.txt`：** JavaScript ファイルを生成する場合はこのファイル名を使用します。
   * **`css.txt`：** カスケーディングスタイルシート（CSS）を生成する場合はこのファイル名を使用します。

1. ファイルを開き、ソースファイルのパスのルートを識別する次のテキストを入力します。

   `#base=*[root]*`

   *`[root]`* を、ソースファイルが格納されているフォルダーの TXT ファイルに対する相対パスに置き換えます。例えば、ソースファイルが TXT ファイルと同じフォルダーにある場合は、次のテキストを使用します。

   `#base=.`

   次のコードで、`cq:ClientLibraryFolder` ノードの下の mobile という名前のフォルダーをルートに設定します。

   `#base=mobile`

1. `#base=[root]` の下の行に、ソースファイルのルートに対する相対パスを入力します。各ファイル名を別々の行に配置します。
1. 「**すべて保存**」をクリックします。

### 依存関係へのリンク {#linking-to-dependencies}

クライアントライブラリフォルダーのコードが他のライブラリを参照する場合、他のライブラリを依存関係として識別します。JSP では、クライアントライブラリフォルダーを参照する `ui:includeClientLib` タグが原因で、HTML コードに生成したライブラリファイルへのリンクおよび依存関係が含まれます。

依存関係は別の `cq:ClientLibraryFolder` でなければなりません。依存関係を識別するには、次の属性を持つプロパティを `cq:ClientLibraryFolder` ノードに追加します。

* **名前：** dependencies
* **タイプ：** String[]
* **値：**&#x200B;現在のライブラリフォルダーの依存先である cq:ClientLibraryFolder ノードの categories プロパティの値。

例えば、/ `etc/clientlibs/myclientlibs/publicmain` は `cq.jquery` ライブラリに依存しています。メインのクライアントライブラリを参照する JSP は、以下のコードを含む HTML を生成します。

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 他のライブラリからのコードの埋め込み {#embedding-code-from-other-libraries}

あるクライアントライブラリから別のクライアントライブラリに、コードを埋め込むことができます。実行時に、埋め込み元のライブラリで生成される JS ファイルおよび CSS ファイルには、埋め込み先のライブラリのコードが含まれます。

コードの埋め込みは、リポジトリーのセキュリティ保護された領域に格納されているライブラリへのアクセスを提供する際に便利です。

#### アプリ固有のクライアントライブラリフォルダー {#app-specific-client-library-folders}

アプリケーション関連のすべてのファイルは、`/apps` 内のアプリケーションフォルダーに格納することをお勧めします。Web サイト訪問者の `/apps` フォルダーに対するアクセスを拒否することもお勧めします。両方のベスト プラクティスを満たすには、`/apps` の下にクライアントライブラリフォルダーを作成し、[クライアントライブラリフォルダーの配置とプロキシクライアントライブラリサーブレットの使用](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)で説明されているように、プロキシサーブレットを介してアクセスできるようにします。

埋め込むクライアントライブラリフォルダーを識別するには、categories プロパティを使用します。ライブラリを埋め込むには、次のプロパティ属性を使用して、埋め込み `cq:ClientLibraryFolder` ノードにプロパティを追加します。

* **名前：** embed
* **タイプ：** String[]
* **値：**&#x200B;埋め込む `cq:ClientLibraryFolder` ノードの categories プロパティの値。

#### 埋め込みを使用したリクエストの最小化 {#using-embedding-to-minimize-requests}

場合によっては（特にサイトでの分析およびターゲティングのために ClientContext 情報を使用している場合）、通常のページ用に公開インスタンスで生成した最終 HTML に、比較的多くの `<script>` 要素が含まれている場合があります。例えば、最適化されていないプロジェクトで、ページの HTML に以下の一連の `<script>` 要素がある可能性があります。

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

このような場合、必要なすべてのクライアントライブラリコードを 1 つのファイルに組み合わせて、ページ読み込み時のリクエストの行き来の数を減らすと便利です。これを行うには、`cq:ClientLibraryFolder` ノードの embed プロパティを使用して、必要なライブラリをアプリ固有のクライアントライブラリに `embed` します。

次のクライアントライブラリカテゴリが AEM に含まれています。特定のサイトを機能させるために必要なもののみを埋め込んでください。ただし、**このリストの順序は保持する必要があります**。

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS ファイル内のパス {#paths-in-css-files}

CSS ファイルを埋め込むと、生成される CSS コードは、埋め込みライブラリに対するリソースへの相対パスを使用します。例えば、公開アクセス可能な `/etc/client/libraries/myclientlibs/publicmain` ライブラリによって `/apps/myapp/clientlib` クライアントライブラリが埋め込まれるとします。

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

`main.css` ファイルには次のスタイルが含まれます。

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain` ノードが生成する CSS ファイルには、元の画像の URL を使用した、次のスタイルが含まれます。

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 特定のモバイルグループ用のライブラリの使用 {#using-a-library-for-specific-mobile-groups}

クライアントライブラリフォルダーの `channels` プロパティを使用して、ライブラリを使用するモバイルグループを識別します。`channels` プロパティは、同じカテゴリのライブラリが異なるデバイス機能向けに設計されている場合に役立ちます。

デバイスグループにクライアントライブラリフォルダーを関連付けるには、以下の属性を伴うプロパティを `cq:ClientLibraryFolder` ノードに追加します。

* **名前：**&#x200B;チャネル
* **タイプ：**&#x200B;文字列[]
* **値：**&#x200B;モバイルグループの名前。ライブラリフォルダーをグループから除外するには、名前の先頭に感嘆符（「!」）を付けます。

例えば、次の表は、`cq.widgets` カテゴリの各クライアントライブラリフォルダーの `channels` プロパティの値を示しています。

| クライアントライブラリフォルダー | チャネルプロパティの値 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## プリプロセッサーの使用 {#using-preprocessors}

AEM では、プラグ可能なプリプロセッサーを使用でき、AEM のデフォルトプリプロセッサーとして、CSS および JavaScript 用の [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) と YUI が定された JavaScript 用の [Google Closure Compiler（GCC）](https://developers.google.com/closure/compiler/)をサポートします。

プラガブルプリプロセッサーは、次のように柔軟に使用できます。

* スクリプトソースを処理できる ScriptProcessors を定義する
* プロセッサーはオプションを使用して設定できる
* プロセッサーは縮小用に使用できるが、縮小以外の場合にも使用できる
* clientlib はどのプロセッサーを使用するかを定義できる

>[!NOTE]
>
>デフォルトでは、AEM は YUI Compressor を使用します。既知の問題のリストについては、[YUI Compressor GitHub ドキュメント](https://github.com/yui/yuicompressor/issues)を参照してください。特定の clientlibs 用の GCC コンプレッサーに切り替えると、YUI を使用しているときに発生していたいくつかの問題が解決することがあります。

>[!CAUTION]
>
>縮小化したライブラリをクライアントライブラリに配置しないでください。代わりに、生のライブラリを提供し、縮小が必要な場合は、プリプロセッサーのオプションを使用します。

### 使用方法 {#usage}

クライアントライブラリごとに、またはシステム全体でプリプロセッサーを設定できます。

* クライアントライブラリノードで、複数値プロパティ `cssProcessor` および `jsProcessor` を追加します。

* または、**HTML ライブラリマネージャー**&#x200B;の OSGi 設定で、システムのデフォルト設定を定義します。

clientlib ノードのプリプロセッサー設定は、OSGI 設定よりも優先されます。

### 形式と例 {#format-and-examples}

#### 形式 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### CSS 縮小用の YUI Compressor と JS 用の GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 事前処理のための Typescript と縮小および不明化のための GCC {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 追加の GCC オプション {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

GCC オプションについて詳しくは、[GCC ドキュメント](https://developers.google.com/closure/compiler/docs/compilation_levels)を参照してください。

### システムのデフォルト縮小ツールの設定 {#set-system-default-minifier}

YUI は、AEM のデフォルト縮小ツールとして設定されています。これを GCC に変更するには、次の手順に従います。

1. Apache Felix Config Manager（[https://localhost:4502/system/console/configMgrr](https://localhost:4502/system/console/configMgr)）に移動します。
1. **Adobe Granite HTML ライブラリマネージャー**&#x200B;を検索して編集します。
1. 「**Minify**」オプションを有効にします（まだ有効でない場合）。
1. **JS Processor Default Configs** の値を `min:gcc` に設定します。

   セミコロンで区切られている場合、オプションを渡すことができます（例：`min:gcc;obfuscate=true`）。

1. 「**保存**」をクリックして、変更を保存します。

## デバッグツール {#debugging-tools}

AEM には、クライアントライブラリフォルダーをデバッグおよびテストするためのツールが用意されています。

### 埋め込みファイルを参照 {#see-embedded-files}

埋め込みコードの元をトレースする、または埋め込みクライアントライブラリが期待どおりの結果を得られるようにするには、実行時に埋め込まれているファイルの名前を確認できます。ファイル名を確認するには、Web ページの URL に `debugClientLibs=true` パラメーターを追加します。生成されるライブラリには、埋め込みコードの代わりに `@import` ステートメントが含まれています。

前の「[他のライブラリからのコードの埋め込み](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)」節の例では、クライアントライブラリフォルダーに`/etc/client/libraries/myclientlibs/publicmain`クライアントライブラリフォルダーが埋め込まれています`/apps/myapp/clientlib`。Web ページにパラメーターを追加すると、Web ページのソースコードに次のリンクが作成されます。

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

`publicmain.css` ファイルを開くと、次のコードが表示されます。

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Web ブラウザーのアドレスボックスで、HTML の URL に次のテキストを付加します。

   `?debugClientLibs=true`
1. ページが読み込まれたら、ページソースを表示します。
1. リンク要素の href として指定されているリンクをクリックしてファイルを開き、ソースコードを表示します。

### クライアントライブラリの確認 {#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs` コンポーネントは、システム上のすべてのクライアントライブラリフォルダーに関する情報のページを生成します。`/libs/granite/ui/content/dumplibs` ノードは、コンポーネントをリソースタイプとして持ちます。ページを開くには、次の URL を使用します（必要に応じてホストとポートを変更）。

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

情報には、ライブラリのパスおよびタイプ（CSS または JS）と、categories や dependencies などのライブラリ属性の値が含まれます。ページ上の後続のテーブルは、各カテゴリおよびチャネルに含まれるライブラリを示します。

### 生成される出力の確認 {#see-generated-output}

`dumplibs` コンポーネントには、`ui:includeClientLib` タグ用に生成されたソースコードを表示するテストセレクターが含まれています。このページには、js、css およびテーマの属性の異なる組み合わせのためのコードが含まれています。

1. 次のいずれかの方法で、テスト出力ページを開きます。

   * `dumplibs.html` ページから、「**こちらをクリックして出力テスト**」テキストのリンクをクリックします。

   * Web ブラウザーで次の URL を開きます（必要に応じて別のホストおよびポートを使用）。

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   デフォルトページに、categories 属性の値がないタグの出力が表示されます。

1. 特定のカテゴリの出力を確認するには、クライアントライブラリの `categories` プロパティの値を入力して、「**クエリを送信**」をクリックします。

## 開発および実稼働用のライブラリ処理の設定 {#configuring-library-handling-for-development-and-production}

HTML ライブラリマネージャーサービスは、実行時に `cq:ClientLibraryFolder` タグを処理してライブラリを生成します。環境、開発または実稼動のタイプによって、サービスの設定方法が決まります。

* セキュリティの向上：デバッグを無効にする
* パフォーマンスの向上：空白を削除し、ライブラリを圧縮します。
* 可読性の向上：空白を含め、圧縮しないでください。

サービスの設定について詳しくは、 [AEMHTMLライブラリマネージャー](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
