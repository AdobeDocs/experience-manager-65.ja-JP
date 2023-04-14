---
title: SEO と URL 管理のベストプラクティス
description: AEM実装の SEO のベストプラクティスと推奨事項について説明します。
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '3678'
ht-degree: 50%

---

# SEO と URL 管理のベストプラクティス{#seo-and-url-management-best-practices}

SEO（検索エンジン最適化）は、多くのマーケターにとって重要な懸念事項となっています。 その結果、多くのAEM Projects で SEO の懸念に対処する必要があります。

このドキュメントでは、まず、 [SEO のベストプラクティス](#seo-best-practices) AEM実装に関する推奨事項。 その次に、最初の節で提示するより[複雑な実装手順](#aem-configurations)のいくつかについて詳しく説明していきます。

## SEO のベストプラクティス {#seo-best-practices}

この節では、一般的な SEO のベストプラクティスをいくつか説明します。

### URL {#urls}

URL に関する一部の受け入れ済みのベストプラクティスがあります。

AEM プロジェクトで URL を評価するときには、次のことを確認してください。

「ユーザーがこの URL を見たが、ページ上のコンテンツを見なかった場合、このページの説明はできますか。」

答えが「はい」であれば、その URL は検索エンジンに効果があります。

SEO 用の URL を作成する方法に関する一般的なヒントを以下に示します。

* ハイフンを使用して単語を区切ります。

   * ページにハイフン (-) を区切り文字として使用する名前を付けます。
   * キャメルケース、アンダースコアおよびスペースの使用は避けます。

* 可能な場合、クエリパラメーターの使用は避けます。必要に応じて、2 つ以下に制限します。

   * ディレクトリ構造を使用して、情報アーキテクチャを示します（使用可能な場合）。
   * ディレクトリ構造を使用できない場合は、クエリ文字列の代わりに、Sling セレクターを URL で使用します。Sling セレクターを使用すると、提供される SEO 値に加えて、Dispatcher でページをキャッシュできるようになります。

* 人間が読み取りやすい URL のほうが、より良いものです。URL にキーワードが存在すると、値がブーストされます。

   * ページでセレクターを使用する場合は、セマンティックな値を提供するセレクターをお勧めします。
   * 人が URL を読み取れない場合、検索エンジンも読み取れません。
   * 次に例を示します。
      `mybrand.com/products/product-detail.product-category.product-name.html`
の方が より望ましい 
`mybrand.com/products/product-detail.1234.html`

* 検索エンジンではサブドメインが異なるエンティティとして扱われ、サイトの SEO 値がフラグメント化されるので、可能な限りサブドメインを避けます。

   * 代わりに、第 1 レベルのサブパスを使用します。例えば、`es.mybrand.com/home.html` の代わりに、`www.mybrand.com/es/home.html` を使用します。

   * このガイドラインに従って、コンテンツの表示方法に合わせてコンテンツ階層を計画します。

* URL の長さとキーワードの位置が増えると、URL でのキーワードの有効性が低下します。 つまり、短い方が良いのです。

   * 不要な URL を削除するには、AEMが提供する URL 短縮手法と機能を使用します。
   * 例えば、`mybrand.com/content/my-brand/en/myPage.html` より `mybrand.com/en/myPage.html` を選択します。

* 正規 URL を使用します。

   * 複数のパスから、または複数のパラメーターやセレクターで 1 つの URL を提供できない場合は必ず、ページで `rel=canonical` タグを使用します。

   * AEMテンプレートのコードに正規 URL を含めます。

* 可能な限り、URL をページタイトルに一致させます。

   * コンテンツ作成者は、この方法に従うことをお勧めします。

* URL リクエストで大文字と小文字を区別しないようサポートします。

   * すべての受信要求を小文字として書き換えるように Dispatcher を設定します。
   * 小文字を使用してすべてのページを作成するようにコンテンツ作成者をトレーニングします。

* 各ページが 1 つのプロトコルからのみ提供されていることを確認します。

   * サイトが `http` 経由で提供され、ユーザーがチェックアウトまたはログインフォームを使用してページに到達した時点で、`https` に切り替わることがあります。このページからリンクする際に、ユーザーが `http` ページと `https`を使用する場合、検索エンジンは、2 つの異なるページとして追跡します。

   * Google では現在、`https` ページの方が `http` ページよりも推奨されています。サイト全体を通じてサイト全体を提供しやすくするのに役立ちます。 `https`.

### サーバーの設定 {#server-configuration}

サーバーの設定に関しては、次の手段を講じることで、適切なコンテンツのみがクロールされるようにすることができます。

* `robots.txt` ファイルを使用して、インデックスを作成する必要がないコンテンツのクローリングをブロックします。

   * ブロック **すべて** テスト環境でのクロール。

* 更新された URL を持つ新しいサイトを開始する際には、301 リダイレクトを実装して、既存の SEO ランキングが失われないようにします。
* サイトの favicon を含めます。
* 検索エンジンでのコンテンツのクロールを容易にするには、XML サイトマップを実装します。 モバイルサイトやレスポンシブサイト用のモバイルサイトマップを必ず含めてください。

## AEM の設定 {#aem-configurations}

この節では、次の SEO 推奨事項を使用してAEMを設定するための実装手順について説明します。

### Sling セレクターの使用 {#using-sling-selectors}

これまで、エンタープライズ web アプリケーションを構築する場合、クエリパラメーターを使用するのが認められた手法でした。

近年のトレンドでは、URL を読みやすくするためにパラメーターを削除するようになりました。 多くのプラットフォームでは、この削除プロセスでは Web サーバーまたはコンテンツ配信ネットワーク (CDN) にリダイレクトを実装しますが、Sling を使用すると簡単に処理できます。 Sling セレクター：

* URL の読みやすさを向上させます。
* Dispatcher でページをキャッシュし、セキュリティを強化できます。
* コンテンツを取得する汎用サーブレットを持つ代わりに、コンテンツを直接アドレス指定できます。 これにより、リポジトリに適用する ACL や、Dispatcher に適用するフィルターを活用できます。

#### サーブレット用のセレクターの使用 {#using-selectors-for-servlets}

AEMでは、サーブレットを記述する際に 2 つのオプションが用意されています。

* **bin** サーブレット
* **Sling** サーブレット

次に示す各例では、この両方のパターンに準拠したサーブレットを登録する方法とともに、Sling サーブレットを使用することによって得られる利点を説明します。

#### bin サーブレット（1 レベル下） {#bin-servlets-one-level-down}

**bin** サーブレットは、多くの開発者が使い慣れている J2EE プログラミングのパターンに準拠しています。このサーブレットは、通常、AEMの以下にある特定のパスに登録されます。 `/bin`をクリックし、必要なリクエストパラメーターをクエリ文字列から抽出します。

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

続いて、`SlingHttpServletRequest` メソッドに含まれる `doGet` オブジェクトを使用して、クエリ文字列からパラメーターを抽出します。次に例を示します。

```
String myParam = req.getParameter("myParam");
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

この方法では、次の点に注意してください。

* URL 自体が SEO 値を失います。 検索エンジンを含むサイトにアクセスするユーザーは、URL はコンテンツ階層ではなくプログラム的パスを表すので、URL からセマンティック値を受け取りません。
* URL にクエリパラメーターが含まれている場合、Dispatcher は応答をキャッシュできません。
* このサーブレットを保護する場合は、独自のカスタムセキュリティロジックをサーブレットに実装します。
* `/bin/myApp/myServlet` を公開するように Dispatcher を（慎重に）設定する必要があります。単に `/bin` を公開すると、サイト訪問者に公開してはいけない特定のサーブレットへのアクセスが許可されます。

#### Sling サーブレット（1 レベル下） {#sling-servlets-one-level-down}

**Sling** サーブレットを使用すると、サーブレットを逆の方法で登録できます。 サーブレットを指定し、クエリーパラメーターに基づいてサーブレットでレンダリングするコンテンツを指定するのではなく、必要なコンテンツを指定します。 また、Sling セレクターに基づいてコンテンツをレンダリングするサーブレットを指定します。

このタイプのサーブレットの SCR 注釈は、次のようになります。

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

この場合、URL がアドレスするリソース — `myPageType` resource — サーブレットで自動的にアクセスできます。 これにアクセスするには、次の呼び出しをおこないます。

```
Resource myPage = req.getResource();
```

使用される結果の URL は次のようになります。

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

このアプローチの利点は次のとおりです。

* サイト階層とページ名に存在するセマンティクスで取得した SEO 値でベイク処理できます。
* クエリパラメーターがないので、Dispatcher で応答をキャッシュできます。また、アドレス指定されたページが更新されていると、ページがアクティブ化されたときにこのキャッシュが無効になります。
* ユーザーがこのサーブレットにアクセスしようとすると、`/content/my-brand/my-page` に適用されているすべての ACL が有効になります。
* Dispatcher は、Web サイトを提供する機能としてこのコンテンツを提供するように既に設定されています。 追加の設定は必要ありません。

### URL の書き換え {#url-rewriting}

AEM では、すべての Web ページが `/content/my-brand/my-content` に保存されます。この場所は、リポジトリデータ管理の観点から見ると便利ですが、必ずしも顧客にサイトを表示する方法とは限りません。 また、URL をできるだけ短く保つための SEO ガイダンスと競合する場合があります。 また、同じ AEM インスタンスや異なるドメイン名から複数の web サイトを提供している場合もあります。

この節では、AEMでこれらの URL を管理し、より読みやすく SEO に適した方法でユーザーに提示するために使用できるオプションについて説明します。

#### バニティ URL {#vanity-urls}

作成者が、プロモーション目的で別の場所からアクセス可能なページを作成する場合、ページごとに定義される AEM のバニティー URL が役立つことがあります。ページのバニティー URL を追加するには、 **Sites** コンソールで該当するページに移動し、ページのプロパティを編集します。「**基本**」タブの下部に、バニティー URL を追加できるセクションが表示されます。複数の URL を使用してページにアクセスできるようにすると、ページの SEO 値が分断されるので、正規 URL タグをページに追加して、この問題を回避する必要があることに留意してください。

#### ページ名のローカライズ {#localized-page-names}

翻訳されたコンテンツのユーザーには、ローカライズされたページ名を表示した方がよい場合があります。次に例を示します。

* スペイン語を話すユーザーが次のページにアクセスするとします。
   `www.mydomain.com/es/home.html`

* この場合、URL を次のように表示した方が効果的です。
   `www.mydomain.com/es/casa.html`

ページ名のローカライズに伴う課題は、AEMプラットフォームで使用可能なローカリゼーションツールの多くでは、コンテンツを同期しておくために、ロケール間でページ名を一致させる必要がある点です。

この `sling:alias` プロパティを使用すると、Adobeケーキを食べることもできます。 次の項目を追加できます。 `sling:alias` を任意のリソースのプロパティとして使用して、リソースのエイリアス名を許可します。 前の例では、次のようになります。

* JCR の次の場所にページがあるとします。
   `…/es/home`

* プロパティを追加します。
   `sling:alias` = `casa`

このフローにより、マルチサイトマネージャーなどのAEM翻訳ツールで、次の間の関係を引き続き維持できます。

* `/en/home`

* `/es/home`

また、エンドユーザーもページ名を母国語で操作できます。

>[!NOTE]
>
>`sling:alias` プロパティは、[ページプロパティ編集時のエイリアスプロパティ](/help/sites-authoring/editing-page-properties.md#advanced)を使用して設定できます。

#### /etc/map {#etc-map}

標準 AEM インストールでは、

* OSGi 設定には
   **Apache Sling Resource Resolver Factory**
（ 
`org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`）

* プロパティ
   **マッピング場所**（`resource.resolver.map.location`）

* デフォルト `/etc/map` に設定。

AEM で受信要求のマッピングまたはページ上の URL の書き換え、あるいはその両方を行うために、この場所にマッピング定義を追加できます。

マッピングを作成するには、この場所の `/http` または `/https` の下に新しい `sling:Mapping` ノードを作成します。このノードで設定された `sling:match` および `sling:internalRedirect` プロパティに基づいて、AEM は、一致した URL のすべてのトラフィックを `internalRedirect` プロパティで指定された値にリダイレクトします。

この方法はAEMおよび Sling の公式ドキュメントに記載されていますが、この実装で提供される正規表現のサポートは、 `SlingResourceResolver` 直接 また、この方法でマッピングを実装すると、Dispatcher のキャッシュの無効化に関する問題が生じることがあります。

次に、この問題がどのように生じるかについて例を示します。

1. ユーザーが Web サイトを訪問し、`https://www.mydomain.com/my-page.html` を要求します。
1. Dispatcher が、このリクエストを公開サーバーに転送します。
1. 公開サーバーが `/etc/map` を使用して、このリクエストを `/content/my-brand/my-page` に解決し、ページをレンダリングします。

1. Dispatcher が `/my-page.html` に応答をキャッシュし、応答をユーザーに返します。
1. コンテンツ作成者がこのページを変更し、アクティブ化します。
1. Dispatcher フラッシュエージェントが `/content/my-brand/my-page`**の無効化リクエストを送信します。** Dispatcher はこのパスにページをキャッシュしていないので、古いコンテンツがキャッシュされたままになり、古くなります。

キャッシュの無効化のために、短い URL を長い URL にマッピングするカスタムのディスパッチフラッシュルールを設定する方法があります。

ただし、この問題をより簡単に管理する方法もあります。

1. **SlingResourceResolver ルール**

   Web コンソール（例えば、localhost:4502/system/console/configMgr）を使用して、Sling Resource Resolver を設定できます。

   * **Apache Sling Resource Resolver Factory**

      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`
   Adobeでは、URL を短縮するために必要なマッピングを正規表現として構築し、OsgiConfignode でこれらの設定を定義することをお勧めします。 `config.publish` ビルドに含まれる

   `/etc/map`マッピングを定義する代わりに、プロパティ **URL Mappings**（`resource.resolver.mapping`）に直接割り当てることができます。

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   この簡単な例では、URL に `/content/my-brand/` が存在する場合、URL の先頭から削除されます。

   URL が変換されます。

   * `/content/my-brand/my-page.html` から
   * ただの `/my-page.html`

   この変換は、URL をできるだけ短く保つことをお勧めする方法に従っておこなわれます。

1. **ページへの URL 出力のマッピング**

   Apache Sling Resource Resolver でマッピングを定義したら、コンポーネントでこれらのマッピングを使用して、ページに出力する URL が短く、適切になるようにします。 このハウスキーピングは、 `ResourceResolver`.

   例えば、現在のページの子をリストアウトするカスタムナビゲーションコンポーネントを実装している場合、次のようなマッピングメソッドを使用できます。

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP サーバ mod_rewrite {#apache-http-server-mod-rewrite}

これまで、URL をページに出力する際に、マッピングをロジックと共にコンポーネントに実装し、これらのマッピングを使用しています。

最後の手順は、短縮された URL の Dispatcher での処理です。ここでは、`mod_rewrite` を使用します。`mod_rewrite` を使用する最大の利点は、URL が、Dispatcher モジュールに送信される&#x200B;*前*&#x200B;に長い形式に再びマッピングされる点です。このフローは、Dispatcher がパブリッシュサーバーに長い URL を要求し、それに応じて URL をキャッシュすることを意味します。 したがって、パブリッシュサーバーからの Dispatcher フラッシュ要求では、このコンテンツを正常に無効にすることができます。

このようなルールを実装するには、Apache HTTP Server の設定で仮想ホストに `RewriteRule` 要素を追加します。前の例の短縮 URL を展開する場合は、次のようなルールを実装できます。

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### 正規 URL タグ {#canonical-url-tags}

正規 URL タグは、コンテンツのインデックス作成時に検索エンジンでページがどのように処理されるかを明確にするために、HTMLドキュメントの先頭に配置されるリンクタグです。 このタグを使用すると、ページの URL に異なる部分が含まれていても、同じものとしてページ（の様々なバージョン）のインデックスが作成されるという利点があります。

例えば、ページのプリンターフレンドリーなバージョンをサイトで提供する場合、検索エンジンでは、通常のバージョンのページとは別に、このページのインデックスが作成される可能性があります。正規タグを使用すると、同じページであることが検索エンジンで認識されます。

例：

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

両方について、ページの先頭に次のタグを適用します。

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

`href` は、相対パスとして指定することも、絶対パスとして指定することもできます。ページの正規 URL を確認し、このタグを出力するには、このコードをページマークアップに挿入する必要があります。

### 大文字と小文字を区別しないための Dispatcher の設定 {#configuring-the-dispatcher-for-case-insensitivity}

すべてのページに小文字を使用して表示することをお勧めします。 ただし、URL に大文字を使用して Web サイトにアクセスする際に、ユーザーに 404 を返さないようにする必要があります。 こうした理由から、すべての受信 URL を小文字にマッピングするように、Apache HTTP Server の設定に書き換えルールを追加することをお勧めします。また、小文字の名前を使用してページを作成するようコンテンツの作成者をトレーニングする必要があります。

すべての受信トラフィックを強制的に小文字に変換するように Apache を設定するには、次のコードを `vhost` の設定に追加します。

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

また、次のコードを `htaccess` ファイルの最上部に追加します。

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### 開発環境を保護するための robots.txt の実装 {#implementing-robots-txt-to-protect-development-environments}

検索エンジンは、サイトをクロールする前に、サイトのルートに *ファイルがあるかどうかをチェック*&#x200B;するはずです`robots.txt`。Google、Yahoo、Bing などの主要な検索エンジンではこのファイルがすべて考慮されますが、一部の外部の検索エンジンではこのファイルが考慮されません。

サイト全体へのアクセスをブロックするための最も簡単な方法は、`robots.txt` というファイルに次の内容を指定して、サイトのルートに配置することです。

```xml
User-agent: *
Disallow: /
```

また、実稼働環境では、インデックスが作成されないように特定のパスを禁止することもできます。

を `robots.txt` ファイルがサイトルートにある場合、Dispatcher のフラッシュ要求によってこのファイルがクリアされます。 また、URL マッピングによって、サイトのルートが `DOCROOT` Apache HTTP Server 設定で定義されたとおりです。 このため、このファイルをオーサーインスタンスのサイトルートに配置し、パブリッシュインスタンスにレプリケートするのが一般的です。

### AEMでの XML サイトマップの作成 {#building-an-xml-sitemap-on-aem}

クローラーは、Web サイトの構造をより深く理解するために XML サイトマップを使用します。 サイトマップを提供すれば SEO ランキングが上がるという保証はありませんが、ベストプラクティスの 1 つとして認められています。Web サーバー上で XML ファイルを手動で維持し、サイトマップとして使用できます。 ただし、Adobeでは、作成者がコンテンツを作成する際にサイトマップが自動的に変更を反映するように、サイトマップをプログラムで生成することをお勧めします。

AEM では、[Apache Sling Sitemap モジュール](https://github.com/apache/sling-org-apache-sling-sitemap)を使用して XML サイトマップを生成し、開発者と編集担当者がサイトの XML サイトマップを最新の状態に保つための様々なオプションを提供します。

>[!NOTE]
>
>Adobe Experience Managerバージョン 6.5.11.0以降の製品機能として使用できます。
> 
>古いバージョンの場合は、自身で Sling サーブレットを登録し、 `sitemap.xml` 呼び出し。 サーブレット API を介して提供されるリソースを使用して、現在のページとその子孫を検索し、 `sitemap.xml` ファイル。

Apache Sling Sitemap モジュールは、最上位のサイトマップとネストされたサイトマップを区別します。どちらも、`sling:sitemapRoot` プロパティが `true` に設定されているリソースについて生成されます。一般に、サイトマップは、ツリーの最上位のサイトマップ（他にサイトマップの上位要素を持たないリソース）のパスにあるセレクターを使用してレンダリングされます。また、この最上位のサイトマップルートはサイトマップのインデックスも公開します。このインデックスは通常、サイト所有者が検索エンジンの設定ポータルで設定したり、サイトの `robots.txt` に追加したりするものです。

例えば、最上位のサイトマップルートを `my-page` に定義し、ネストされたサイトマップルートを `my-page/news` に定義するサイトで、ニュースサブツリーのページ専用のサイトマップを生成するとします。これに、関連する URL は次のようになります。

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>セレクター `sitemap` および `sitemap-index` は、カスタム実装と干渉する可能性があります。製品機能を使用しない場合は、これらのセレクターを提供する独自のサーブレットを 0 より大きい `service.ranking` で設定します。

デフォルトの設定では、ページのプロパティダイアログには、ページをサイトマップルートとしてマークオプションがあり、前述したように、ページ自体とその下位要素のサイトマップを生成します。この動作は `SitemapGenerator` インターフェイスの実装によって実装されており、代替実装を追加することで拡張することができます。ただし、XML サイトマップを再生成する頻度はコンテンツオーサリングワークフローとワークロードに依存するので、製品には何も付属していません `SitemapScheduler` 設定。 したがって、機能は効果的にオプトインします。

XML サイトマップを生成するバックグラウンドジョブを有効にするには、 `SitemapScheduler` を設定する必要があります。 それには、PID `org.apache.sling.sitemap.impl.SitemapScheduler` の OSGi 設定を作成します。スケジューラー式 `0 0 0 * * ?` は、1 日 1 回午前 0 時にすべての XML サイトマップを再生成するための開始点として使用できます。

![Apache Sling Sitemap - スケジューラー](assets/sling-sitemap-scheduler.png)

サイトマップ生成ジョブは、オーサー層インスタンスとパブリッシュ層インスタンスの両方で実行できます。 適切な正規 URL はそこでのみ生成できるので、通常はパブリッシュ層インスタンスで生成を実行することをお勧めします（通常、Sling リソースマッピングルールはパブリッシュ層インスタンスでのみ存在するので）。 ただし、 [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) インターフェイス。 カスタム実装で、オーサー層インスタンス上にサイトマップの正規 URL を生成できる場合、 `SitemapScheduler` は、オーサー実行モード用に設定できます。 また、XML サイトマップ生成ワークロードをオーサーサービスクラスターのインスタンス全体に分散させることができます。 このシナリオでは、まだ公開されていない、変更されている、または制限されたユーザーグループにのみ表示されるコンテンツの処理には、注意が必要です。

AEM Sites には、ページのツリーをトラバースしてサイトマップを生成する `SitemapGenerator` のデフォルトの実装が含まれています。サイトの正規 URL と（使用可能な場合は）代替言語のみを出力するように事前設定されています。また、必要に応じて、ページの最終変更日を含めるように設定することもできます。これをおこなうには、 _最終変更日を追加_ オプション _AdobeAEM SEO - Page Tree Sitemap Generator_ 設定および _最終変更ソース_. サイトマップがパブリッシュ層で生成される場合は、`cq:lastModified` の日付を使用することをお勧めします。

![Adobe AEM SEO - Page Tree Sitemap Generator 設定](assets/sling-sitemap-pagetreegenerator.png)

サイトマップのコンテンツを制限するには、必要に応じて次のサービスインターフェイスを実装します。

* [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) を実装することで、AEM Sites 固有のサイトマップジェネレーターで生成された XML サイトマップからページを非表示にすることができます。
* [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) または [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) を実装して、[Commerce Integration Frameworks](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=ja) 固有のサイトマップジェネレーターで生成される XML サイトマップから製品やカテゴリをフィルタリングできます。

特定の使用例でデフォルトの実装が機能しない場合、または拡張機能が十分に柔軟性を持たない場合は、カスタムを実装します `SitemapGenerator` 生成されたサイトマップのコンテンツを完全に制御する。 次の例では、AEM Sitesのデフォルトの実装ロジックを使用しています。 [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) を開始点として使用して、ページのツリーをトラバースします。

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, etc
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

さらに、XML サイトマップ用に実装された機能は、例えば、正規リンクや代替言語をページの先頭に追加する場合など、様々なユースケースにも使用できます。詳しくは、 [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) インターフェイスを参照してください。

### レガシー URL の 301 リダイレクトの作成 {#creating-redirects-for-legacy-urls}

新しい構造でサイトの運用を開始するときには、次の 2 つの理由から、Apache HTTP Server で 301 リダイレクトを実装し、テストすることが重要です。

* レガシー URL は、時間の経過と共に SEO 値を構築しています。 リダイレクトを実装することで、検索エンジンはこの値を新しい URL に適用できます。
* サイトのユーザーが、これらのページにブックマークを作成している場合があります。 リダイレクトを実装すると、古いサイトでの取得を試みていた場所に最も近い新しいサイトのページに、ユーザーを確実に誘導できます。

301 リダイレクトの実装に関する説明や、リダイレクトが正しく機能していることをテストするためのツールについては、その他のリソースの節を参照してください。

## その他のリソース {#additional-resources}

詳しくは、以下のその他のリソースを参照してください。

* [リソースマッピング](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
