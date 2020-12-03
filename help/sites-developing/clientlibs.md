---
title: クライアントサイドライブラリの使用
seo-title: クライアントサイドライブラリの使用
description: AEM では、クライアント側ライブラリフォルダーが提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義できます。
seo-description: AEM では、クライアント側ライブラリフォルダーが提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのカテゴリのコードをクライアントに提供するタイミングと方法を定義できます。
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 5d33b48000cf607eb77c626ec539280cadab378e
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 73%

---


# クライアントサイドライブラリの使用{#using-client-side-libraries}

最近の Web サイトは、複雑な JavaScript や CSS コードを利用したクライアント側の処理に大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。

この問題への対処に役立つように、AEM では、**クライアント側ライブラリフォルダー**&#x200B;が提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのコードカテゴリをクライアントに保存するタイミングと方法を定義することができます。その後、クライアント側ライブラリシステムにより、最終的な Web ページで、正しいコードを読み込むための正しいリンクが作成されます。

## AEM でのクライアント側ライブラリの機能  {#how-client-side-libraries-work-in-aem}

ページのHTMLにクライアント側ライブラリ（JSまたはCSSファイル）を含める標準的な方法は、そのページのJSPに`<script>`または`<link>`タグを含め、該当するファイルへのパスを含めることです。 例：

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

この方法は AEM で機能しますが、ページやそれに含まれるコンポーネントが複雑になると、問題につながる可能性があります。そのような場合、同じ JS ライブラリの複数のコピーが最終的な HTML 出力に含まれる危険性があります。これを回避してクライアント側ライブラリを論理的に整理するために、AEM では&#x200B;**クライアント側ライブラリフォルダー**&#x200B;を使用します。

クライアント側ライブラリフォルダーは、タイプが `cq:ClientLibraryFolder` のリポジトリノードです。[CND 注釈](https://jackrabbit.apache.org/node-type-notation.html)での定義は次のとおりです。

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

デフォルトでは、`cq:ClientLibraryFolder`ノードはリポジトリの`/apps`、`/libs`、`/etc`サブツリー内の任意の場所に配置できます(これらのデフォルトと他の設定は、[System Console](https://localhost:4502/system/console/configMgr)の&#x200B;**AdobeGranite HTML Library Manager**&#x200B;パネルで制御できます)。

各 `cq:ClientLibraryFolder` には、JS ファイルや CSS ファイルのセットと、いくつかのサポートファイルが入力されます（以下を参照）。`cq:ClientLibraryFolder`のプロパティは、次のように設定します。

* `categories`：`cq:ClientLibraryFolder` に含まれる JS ファイルや CSS ファイルのセットのカテゴリを特定します。`categories` プロパティは複数の値を取るため、ライブラリフォルダーを複数のカテゴリーの一部にすることができます（これがどのように役立つかについては以下を参照）。

* `dependencies`：これは、このライブラリカテゴリが依存する他のクライアントライブラリフォルダーのリストです。例えば、`F` と `G` の 2 つの `cq:ClientLibraryFolder` ノードを指定し、`F` のファイルが正しく機能するために別の `G` のファイルを必要とする場合、`G` の中の少なくとも 1 つの `categories` は、`F` の `dependencies` でなければなりません。

* `embed`：他のライブラリからコードを埋め込むために使用します。ノードFがノードGとHを埋め込むと、結果のHTMLはノードGとHからのコンテンツの集合になります。
* `allowProxy`:クライアントライブラリがの下にある場合、 `/apps`このプロパティを使用すると、プロキシサーブレット経由でアクセスできます。後述の「[クライアントライブラリフォルダーの配置とプロキシクライアントライブラリサーブレットの使用](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)」を参照してください。

## クライアント側ライブラリの参照 {#referencing-client-side-libraries}

HTL は、AEM のサイト開発での推奨テクノロジーなので、HTL を使用して AEM にクライアント側ライブラリを含める必要があります。ただし、JSP を使用しておこなうこともできます。

### HTL の使用  {#using-htl}

HTL では、クライアントライブラリは AEM 提供のヘルパーテンプレートを介して読み込まれます。テンプレートには [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use) を使用してアクセスできます。このファイルには 3 つのテンプレートが含まれ、[`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call) で呼び出すことができます。

* **css**  — 参照されるクライアントライブラリのCSSファイルのみを読み込みます。
* **js**  — 参照されるクライアントライブラリのJavaScriptファイルのみを読み込みます。
* **all**  — 参照されるクライアントライブラリ（CSSとJavaScriptの両方）のすべてのファイルを読み込みます。

各ヘルパーテンプレートには、必要なクライアントライブラリを参照するための `categories` オプションを指定できます。このオプションには、文字列値の配列またはコンマ区切り値のリストを含む文字列を指定できます。

使用方法の詳細と例については、「[HTML Template Languageの使い始めに](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)」のドキュメントを参照してください。

### JSP の使用 {#using-jsp}

JSPコードに追加`ui:includeClientLib`タグを付け、生成されたHTMLページのクライアントライブラリにリンクを追加します。 ライブラリを参照するには、`ui:includeClientLib`ノードの`categories`プロパティの値を使用します。

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

例えば、`/etc/clientlibs/foundation/jquery`ノードのタイプが`cq:ClientLibraryFolder`で、カテゴリのプロパティが値`cq.jquery`です。 JSPファイル内の次のコードは、ライブラリを参照します。

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

生成される HTML ページには次のコードが含まれます。

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

JS、CSS またはテーマライブラリをフィルタリングするための属性を含めた詳細は、[ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib) を参照してください。

>[!CAUTION]
>
>`<cq:includeClientLib>`は、以前はクライアントライブラリを含めるためによく使用されていたもので、AEM 5.6以降では廃止されています。 [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 上記の説明の代わりに使用する必要があります。

## クライアントライブラリフォルダーの作成 {#creating-client-library-folders}

`cq:ClientLibraryFolder`ノードを作成して、JavaScriptライブラリとカスケーディングスタイルシートライブラリを定義し、それらをHTMLページで使用できるようにします。 ノードの `categories` プロパティを使用して、ノードが属するライブラリカテゴリを特定します。

ノードには、実行時に単一のJSファイルやCSSファイルに結合される1つ以上のソースファイルが含まれます。 生成されるファイルの名前はノード名で、ファイル名の拡張子は `.js` または `.css` です。例えば、`cq.jquery` という名前のライブラリノードからは、 `cq.jquery.js` または `cq.jquery.css` という名前のファイルが生成されます。

クライアントライブラリフォルダーには次の項目が含まれます。

* JS／CSS ソースファイル（いずれかまたは両方） 結合します。
* 画像ファイルなど、CSS スタイルをサポートするリソース。

   **注意：**&#x200B;サブフォルダーを使用してソースファイルを整理できます。
* 生成される JS／CSS ファイルに統合するソースファイルを識別する 1 つの `js.txt` ファイルと 1 つの `css.txt` ファイル（いずれかまたは両方）。

![clientlibarch](assets/clientlibarch.png)

ウィジェット用のクライアントライブラリ特有の要件について詳しくは、[ウィジェットの使用および拡張](/help/sites-developing/widgets.md)を参照してください。

Webクライアントは`cq:ClientLibraryFolder`ノードにアクセスする権限を持っている必要があります。 また、リポジトリの保護された領域からライブラリを公開することもできます（後述の「他のライブラリからのコードの埋め込み」を参照）。

### /lib でのライブラリの上書き{#overriding-libraries-in-lib}

`/apps`の下にあるクライアントライブラリフォルダーは、`/libs`と同じように配置されている同じ名前のフォルダーよりも優先されます。 例えば、`/apps/cq/ui/widgets`は`/libs/cq/ui/widgets`よりも優先されます。 これらのライブラリが同じカテゴリに属する場合は、`/apps`の下のライブラリが使用されます。

### クライアントライブラリフォルダーの配置とプロキシクライアントライブラリサーブレットの使用 {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

以前のバージョンでは、クライアントライブラリフォルダーはリポジトリの`/etc/clientlibs`の下に配置されていました。 これは引き続きサポートされますが、クライアントライブラリを`/apps`の下に置くことをお勧めします。 これは、他のスクリプトの近くにクライアントライブラリを配置するためのものです。通常は`/apps`と`/libs`の下にあります。

>[!NOTE]
>
>クライアントライブラリフォルダーの下の静的リソースは、*resources*&#x200B;というフォルダーに存在する必要があります。 フォルダー&#x200B;*resources*&#x200B;の下に画像などの静的リソースがない場合、その静的リソースは発行インスタンスで参照できません。 次に例を示します。https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>コードをコンテンツと設定からより詳細に分離するには、`/apps`の下にクライアントライブラリを配置し、`allowProxy`プロパティを活用して`/etc.clientlibs`を介してそれらを公開することをお勧めします。

`/apps` にあるクライアントライブラリにアクセスできるようにするために、プロキシサーブレットが使用されます。ACL は依然としてクライアントライブラリフォルダーで適用されますが、サーブレットを使用すると、`/etc.clientlibs/` プロパティが `allowProxy` に設定されている場合、`true` を介してコンテンツを読み取ることができます。

静的リソースは、クライアントライブラリフォルダーの下のリソースにある場合、プロキシ経由でのみアクセスできます。

次に例を示します。

* clientlib は `/apps/myproject/clientlibs/foo` にあります。
* 静的画像は `/apps/myprojects/clientlibs/foo/resources/icon.png` にあります。

次に、`foo`の`allowProxy`プロパティをtrueに設定します。

* その後、`/etc.clientlibs/myprojects/clientlibs/foo.js`をリクエストできます
* 次に、`/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`を介して画像を参照します

>[!CAUTION]
>
>プロキシ化されたクライアントライブラリを使用する場合、AEMディスパッチャーの設定で、拡張clientlibを持つURIが許可されるように更新する必要がある場合があります。

>[!CAUTION]
>
>Adobeでは、`/apps`の下にクライアントライブラリを探し、プロキシサーブレットを使用して使用することをお勧めします。 ただし、ベストプラクティスとしては、パブリックサイトには`/apps`または`/libs`パスを介して直接提供されるものは一切含めないことが必要です。

### クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

1. Webブラウザー([https://localhost:4502/crx/de](https://localhost:4502/crx/de))でCRXDE Liteを開きます。
1. クライアントライブラリフォルダーの配置先のフォルダーを選択して、**作成／ノードを作成**&#x200B;をクリックします。
1. ライブラリファイルの名前を入力し、タイプリストで `cq:ClientLibraryFolder` を選択します。「**OK**」をクリックし、「**すべて保存**」をクリックします。
1. ライブラリが所属するカテゴリ（1 つまたは複数）を指定するには、`cq:ClientLibraryFolder` ノードを選択し、次のプロパティを追加して、「**すべて保存**」をクリックします。

   * 名前：categories
   * タイプ：String
   * 値：カテゴリ名
   * 複数：選択

1. 何らかの方法で、ソースファイルをライブラリフォルダーに追加します。例えば、WebDav クライアントを使用してファイルをコピーする、ファイルを作成してコンテンツを手動で作成する、などの方法があります。

   **注意：**&#x200B;必要に応じて、サブフォルダーを使用してソースファイルを整理できます。

1. クライアントライブラリフォルダーを選択して、**作成／ファイルを作成**&#x200B;をクリックします。
1. ファイル名ボックスに、次のいずれかのファイル名を入力して、「OK」をクリックします。

   * **`js.txt`：** JavaScript ファイルを生成する場合はこのファイル名を使用します。
   * **`css.txt`：** カスケーディングスタイルシート（CSS）を生成する場合はこのファイル名を使用します。

1. ファイルを開き、ソースファイルのパスのルートを識別する次のテキストを入力します。

   `#base=*[root]*`

   「* `[root]`*」は、TXTファイルを基準とした、ソースファイルを含むフォルダーのパスに置き換えます。 例えば、ソースファイルが TXT ファイルと同じフォルダーにある場合は、次のテキストを使用します。

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

例えば、/ `etc/clientlibs/myclientlibs/publicmain`は`cq.jquery`ライブラリに依存しています。 メインのクライアントライブラリを参照するJSPは、次のコードを含むHTMLを生成します。

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 他のライブラリからのコードの埋め込み {#embedding-code-from-other-libraries}

あるクライアントライブラリから別のクライアントライブラリに、コードを埋め込むことができます。実行時に、埋め込み元のライブラリで生成される JS ファイルおよび CSS ファイルには、埋め込み先のライブラリのコードが含まれます。

コードの埋め込みは、リポジトリのセキュリティ保護された領域に格納されているライブラリへのアクセスを提供する際に便利です。

#### アプリケーション専用のクライアントライブラリフォルダー  {#app-specific-client-library-folders}

アプリケーション関連のすべてのファイルは、`/app` 内のアプリケーションフォルダーに格納することをお勧めします。Web サイト訪問者の `/app` フォルダーに対するアクセスを拒否することもお勧めします。両方のベストプラクティスを満たすには、`/etc` にクライアントライブラリフォルダーを作成して、 `/app` 内のクライアントライブラリを埋め込みます。

埋め込むクライアントライブラリフォルダーを識別するには、categories プロパティを使用します。ライブラリを埋め込むには、次のプロパティ属性を使用して、埋め込み `cq:ClientLibraryFolder` ノードにプロパティを追加します。

* **名前：** embed
* **タイプ：** String[]
* **値：**&#x200B;埋め込む `cq:ClientLibraryFolder` ノードの categories プロパティの値。

#### 埋め込みを使用したリクエストの最小化 {#using-embedding-to-minimize-requests}

発行インスタンスによって一般的なページ用に生成される最終的なHTMLに、比較的多数の`<script>`要素が含まれている場合があります。特に、サイトで分析やターゲット設定にクライアントコンテキスト情報を使用している場合に便利です。 例えば、最適化されていないプロジェクトでは、ページのHTMLに次の`<script>`要素のシリーズが含まれているとします。

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

このような場合、必要なすべてのクライアントライブラリコードを 1 つのファイルに組み合わせて、ページ読み込み時のリクエストの行き来の数を減らすと便利です。これをおこなうには、`cq:ClientLibraryFolder` ノードの embed プロパティを使用して、必要なライブラリをアプリ固有のクライアントライブラリに `embed` します。

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

クライアントライブラリフォルダーの`channels`プロパティを使用して、ライブラリを使用するモバイルグループを特定します。 `channels`プロパティは、同じカテゴリのライブラリが異なるデバイス機能用に設計されている場合に便利です。

クライアントライブラリフォルダーをデバイスグループに関連付けるには、次の属性を持つ`cq:ClientLibraryFolder`ノードにプロパティを追加します。

* **名前：** チャネル
* **タイプ：** String[]
* **値：モバ** イルグループの名前。ライブラリフォルダーをグループから除外するには、名前の前に感嘆符(&quot;!&quot;)を付けます。

例えば、次の表は、`channels` カテゴリの各クライアントライブラリフォルダーの `cq.widgets` プロパティの値を示しています。

| クライアントライブラリフォルダー | channels プロパティの値 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[値なし]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## プリプロセッサーの使用 {#using-preprocessors}

AEM では、プラグ可能なプリプロセッサーを使用でき、AEM のデフォルトプリプロセッサーとして、CSS および JavaScript 用の [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) と YUI が定された JavaScript 用の [Google Closure Compiler（GCC）](https://developers.google.com/closure/compiler/)をサポートします。

プラグ可能なプリプロセッサーは、次のように柔軟な使用が可能です。

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

### システムのデフォルト縮小ツールの設定  {#set-system-default-minifier}

YUI は、AEM のデフォルト縮小ツールとして設定されています。これを GCC に変更するには、次の手順に従います。

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)のApache Felix Config Managerに移動します。
1. **Adobe Granite HTML ライブラリマネージャー**&#x200B;を検索して編集します。
1. 「**Minify**」オプションを有効にします（まだ有効でない場合）。
1. **JS Processor Default Configs** の値を `min:gcc` に設定します。

   セミコロンで区切られている場合、オプションを渡すことができます（例：`min:gcc;obfuscate=true`）。

1. 「**保存**」をクリックして、変更を保存します。

## デバッグツール {#debugging-tools}

AEM には、クライアントライブラリフォルダーをデバッグおよびテストするためのツールが用意されています。

### 埋め込みファイルの確認  {#see-embedded-files}

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

## 開発および本番用のライブラリ処理の設定 {#configuring-library-handling-for-development-and-production}

HTML ライブラリマネージャーサービスは、実行時に `cq:ClientLibraryFolder` タグを処理し、ライブラリを生成します。環境、開発または本番のタイプが、サービスの設定方法を決定します。

* セキュリティを強化：デバッグを無効化
* パフォーマンスを向上：空白を削除してライブラリを圧縮
* 読みやすさを改善：空白を含めて圧縮しない

サービスの設定について詳しくは、[AEM HTML ライブラリマネージャー](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)を参照してください。
