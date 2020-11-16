---
title: モバイルアプリのページテンプレート
seo-title: モバイルアプリのページテンプレート
description: このページでは、ページテンプレートの詳細について説明します。アプリに作成するページコンポーネントは、/libs/mobileapps/components/angular/ng-page コンポーネントに基づいています。
seo-description: このページでは、ページテンプレートの詳細について説明します。アプリに作成するページコンポーネントは、/libs/mobileapps/components/angular/ng-page コンポーネントに基づいています。
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2698'
ht-degree: 66%

---


# モバイルアプリのページテンプレート {#page-templates-for-mobile-apps}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

## モバイルアプリのページテンプレート {#page-templates-for-mobile-apps-1}

Page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component ([open in CRXDE Lite on a local server](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). このコンポーネントには次の JSP スクリプトが含まれており、これらのスクリプトを自分のコンポーネントで継承またはオーバーライドします。

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

`applicationName` プロパティを使用してアプリケーションの名前を決定し、pageContext を使用して公開します。

head.jsp および body.jsp をインクルードしています。

### head.jsp {#head-jsp}

Writes out the `<head>` element of the app page.

アプリの viewport メタプロパティをオーバーライドする場合は、これがオーバーライド対象のファイルになります。

Following best practices, the app includes the css portion of the client libraries in the head, while the JS is included at the closing &lt; `body>` element.

### body.jsp {#body-jsp}

Angular ページのボディは、wcm モードが検出されたかどうか（! = WCMMode.DISABLED）に応じてレンダリングが異なり、ページを作成用に開くか、公開済みページとして開くかが決まります。

**オーサーモード**

オーサーモードでは、個々のページが個別にレンダリングされます。 Angularは、ページ間のルーティングを処理しません。また、ページのコンポーネントを含む部分的な表示の読み込みに使用されるngテンプレートもありません。 その代わり、ページテンプレート（template.jsp）のコンテンツが `cq:include` タグによってサーバー側にインクルードされます。

この方法により、何も変更を加えることなく、オーサー機能（段落システム、サイドキック、デザインモードでのコンポーネントの追加および編集など）を使用可能にすることができます。アプリ向けのページなどクライアント側のレンダリングを利用するページは、AEM オーサーモードではパフォーマンスがよくありません。

Note that the template.jsp include is wrapped in a `div` element that contains the `ng-controller` directive. この構造により、DOM コンテンツをコントローラーとリンクできます。このため、クライアント側で自身をレンダリングするページは失敗しますが、同じようにレンダリングする個々のコンポーネントは正常に機能します（下のコンポーネントに関する節を参照）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**パブリッシュモード**

公開モード（コンテンツの同期を使用してアプリを書き出す場合など）では、すべてのページが単一のページアプリ(SPA)になります。 (To learn about SPAs, use the Angular tutorial, specifically [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

There is only one HTML page in a SPA (a page that contains the `<html>` element). このページは、「レイアウトテンプレート」と呼ばれています。Angular 用語では、「アプリケーション内のすべてのビューに共通するテンプレート」となります。このページは、「トップレベルのアプリページ」と考えてください。By convention the top-level app page is the `cq:Page` node of your application that is closest to the root (and is not a redirect).

パブリッシュモードではアプリの実際の URI が変わらないので、このページから外部アセットを参照するには相対パスを使用する必要があります。したがって、書き出す画像をレンダリングする際に、この最上位レベルのページが考慮される特別な画像コンポーネントが用意されています。

SPA として、このレイアウトテンプレートページは単に ng-view ディレクティブとともに div 要素を生成します。

```xml
 <div ng-view ng-class="transition"></div>
```

Angularルートサービスはこの要素を使用して、現在のページ（template.jspに含まれる）の承認可能なコンテンツを含む、アプリ内のすべてのページのコンテンツを表示します。

body.jsp ファイルには、header.jsp および footer.jsp が空の状態でインクルードされています。どのページにも静的コンテンツを提供する場合には、アプリでこれらのスクリプトをオーバーライドできます。

Finally, javascript clientlibs are included at the bottom of the &lt;body> element including two special JS files that are generated on the server: *&lt;page name>*.angular-app-module.js and *&lt;page name>*.angular-app-controllers.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

このスクリプトでは、アプリケーションの Angular モジュールを定義します。このスクリプトの出力は、テンプレートのコンポーネントの残りの部分が `html` 要素を利用して ng-page.jsp に生成するマークアップにリンクされます。ng-page.jsp には、次の属性が含まれています。

```xml
ng-app="<c:out value='${applicationName}'/>"
```

この属性は Angular に対して、この DOM 要素のコンテンツを次のモジュールにリンクする必要があることを示します。このモジュールは、ビュー（AEM では cq:Page リソース）を対応するコントローラーとリンクします。

また、`AppController` 変数をスコープに公開するトップレベルのコントローラーを `wcmMode` という名前で定義し、コンテンツ同期更新ペイロードを取得する URI を設定します。

最後に、このモジュールは各子孫ページ（自身を含む）を反復し、各ページのルートフラグメントの内容を（angular-route-fragment.jsセレクターと拡張を介して）レンダリングします。この内容は、Angularの\$routeProviderへのconfigエントリとして含まれます。 つまり、\$routeProviderは、特定のパスがリクエストされた場合にどのコンテンツをレンダリングするかをアプリに指示します。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

このスクリプトは、次の形式を取る JavaScript フラグメントを生成します。

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

This code indicates to $routeProvider (defined in angular-app-module.js.jsp) that &#39;/&lt;path>&#39; is to be handled by the resource at `templateUrl`, and wired up by `controller` (which we&#39;ll get to next).

必要に応じて、変数があるものも含めさらに複雑なパスを処理するように、このスクリプトをオーバーライドできます。この一例を AEM とともにインストールされる /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp スクリプトで確認できます。

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Angularでは、コントローラは\$scope内の変数を配線し、表示に公開します。 angular-app-controllers.js.jspスクリプトは、angular-app-module.js.jspに示すパターンに従って、そのページ自体を含む各子孫ページを繰り返し処理し、各ページが定義したコントローラーフラグメントをcontroller.js.jsp経由で出力します。 このスクリプトが定義しているモジュールは、`cqAppControllers` という名前であり、ページコントローラーが使用可能になるようにトップレベルアプリモジュールの依存関係としてリストされる必要があります。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp スクリプトは、ページごとにコントローラーフラグメントを生成します。このコントローラーフラグメントは、次の形式を取ります。

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Note that the `data` variable is assigned the promise returned by the Angular `$http.get` method. このページにインクルードされている各コンポーネントでは、必要に応じて一部の .json コンテンツを（その angular.json.jsp スクリプトを利用して）使用可能にし、この要求を解決する際に要求のコンテンツに対して処理を実行できます。要求は、単にファイルシステムにアクセスするだけなので、モバイルデバイスでは非常に高速です。

このようにコンポーネントをコントローラーの一部にするには、コンポーネントを /libs/mobileapps/components/angular/ng-component コンポーネントで拡張し、コンポーネントに `frameworkType: angular`   プロパティを含める必要があります。

### template.jsp {#template-jsp}

body.jspセクションで最初に導入されたtemplate.jspには、ページのparsysが含まれています。 公開モードでは、このコンテンツは（&lt;page-path>.template.htmlで）直接参照され、\$routeProviderに設定されたtemplateUrlを介してSPAに読み込まれます。

このスクリプトの parsys は、任意のタイプのコンポーネントを受け入れるように設定できます。ただし、（SPA ではなく）従来の Web サイト向けにビルドされたコンポーネントを扱うときには注意が必要です。例えば、基盤画像コンポーネントは、アプリ内部にあるアセットを参照するように設計されていないため、トップレベルアプリページでのみ正しく機能します。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

このスクリプトは、単にトップレベルの Angular アプリモジュールの Angular 依存関係を出力します。angular-app-module.js.jspで参照されています。

### header.jsp {#header-jsp}

アプリの最上部に静的コンテンツを配置するスクリプト。このコンテンツは、トップレベルページによって ng-view のスコープ外にインクルードされます。

### footer.jsp {#footer-jsp}

アプリの最下部に静的コンテンツを配置するスクリプト。このコンテンツは、トップレベルページによって ng-view のスコープ外にインクルードされます。

### js_clientlibs.jsp {#js-clientlibs-jsp}

JavaScript clientlibs をインクルードするように、このスクリプトをオーバーライドしてください。

### css_clientlibs.jsp {#css-clientlibs-jsp}

CSS clientlibs をインクルードするように、このスクリプトをオーバーライドしてください。

## アプリコンポーネント {#app-components}

アプリコンポーネントは、AEM インスタンス（パブリッシュまたはオーサー）で機能するだけではなく、アプリコンテンツがコンテンツ同期によってファイルシステムにエクスポートされるときにも機能する必要があります。このため、コンポーネントは次の特性を備える必要があります。

* PhoneGap アプリケーション内のすべてのアセット、テンプレートおよびスクリプトが相対的に参照される必要があります。
* AEM インスタンスがオーサーモードまたはパブリッシュモードで動作している場合には、リンクの処理が異なります。

### 相対的なアセット {#relative-assets}

PhoneGap アプリケーション内の特定のアセットの URI は、プラットフォームごとに異なるだけでなく、アプリのインストールごとに一意になります。例えば、iOS シミュレーターで実行中のアプリの次の URI に注意してください。

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

パスの GUID が「24BA22ED-7D06-4330-B7EB-F6FC73251CA3」となっています。

PhoneGap 開発者に関係するコンテンツは、www ディレクトリの下にあります。アプリアセットにアクセスするには、相対パスを使用します。

問題が複雑なのは、PhoneGap アプリケーションではシングルページアプリ（SPA）パターンを使用しているので、基準 URI が（ハッシュを除いて）変更されないことです。Therefore, every asset, template, or script that you reference **must be relative to your top-level page.** トップレベルのページは、およびを使用してAngularルーティングとコントローラを初期化 `*<name>*.angular-app-module.js` し `*<name>*.angular-app-controllers.js`ます。 このページは、リポジトリのルートに最も近いページで、sling:redirectを*拡張しない。

次の複数のヘルパーメソッドで相対パスに対処できます。

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

使用例を確認するには、/libs/mobileapps/components/angularにあるmobileappsソースを開きます。

### リンク {#links}

Links must use the `ng-click="go('/path')"` function to support all WCM modes. この関数は、スコープ変数の値を利用して、リンクアクションを正しく判別します。

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

When `$scope.wcmMode == true` we handle each navigation event in the usual way, such that the result is a change to the path and/or page portion of the URL.

Alternatively, if `$scope.wcmMode == false`, each navigation event results in a change to the hash portion of the URL which is resolved internally by Angular&#39;s ngRoute module.

### コンポーネントスクリプトの詳細 {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

このスクリプトは、編集モードが検出されたときにコンポーネントコンテンツまたは適切なプレースホルダーを表示します。

#### template.jsp {#template-jsp-1}

template.jsp スクリプトは、コンポーネントのマークアップをレンダリングします。問題のコンポーネントがAEMから抽出されたJSONデータ（「ng-text」など）によって駆動される場合：/libs/mobileapps/components/angular/ng-text/template.jsp)の場合、このスクリプトは、ページのコントローラースコープによって公開されるデータを使用してマークアップを配線します。

ただし、パフォーマンス要件のために、クライアント側でテンプレート化（データ連結とも呼ばれます）を実行しないように指示されることがあります。この場合は、単にサーバー側でコンポーネントのマークアップをレンダリングし、それをページテンプレートコンテンツにインクルードします。

#### overhead.jsp {#overhead-jsp}

JSONデータによって駆動されるコンポーネント（「ng-text」など）の場合：/libs/mobileapps/components/angular/ng-text)、overhead.jspを使用して、template.jspからすべてのJavaコードを削除できます。 overhead.jsp は template.jsp から参照され、overhead.jsp が要求で公開している変数は使用可能です。この方法により、ロジックと表示を分離でき、既存のコンポーネントから新規のコンポーネントを生成する場合にコピーして貼り付ける必要があるコードの量を抑えることができます。

#### controller.js.jsp {#controller-js-jsp-1}

As described in AEM Page Templates, each component can output a JavaScript fragment to consume the JSON content exposed by the `data` promise. Angular の表記規則に従って、コントローラーはスコープに変数を割り当てる目的でのみ使用します。

#### angular.json.jsp {#angular-json-jsp}

このスクリプトは、ng-page を拡張するページごとにエクスポートされるページ全体の &lt;ページ名>.angular.json ファイルにフラグメントとしてインクルードされます。このファイルで、コンポーネント開発者はコンポーネントで必要な任意の JSON 構造を公開できます。「ng-text」の例の場合、この構造に含まれているのは、コンポーネントのテキストコンテンツと、コンポーネントにリッチテキストが含まれているかどうかを示すフラグだけです。

さらに複雑な例が Geometrixx Outdoors アプリ製品コンポーネントです（/apps/geometrixx-outdoors-app/components/angular/ng-product）。

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI アセットのダウンロードの内容 {#contents-of-the-cli-assets-download}

アプリコンソールから CLI アセットをダウンロードすると、CLI アセットを特定のプラットフォームに合わせて最適化したうえで、PhoneGap コマンドライン統合（CLI）API を使用してアプリをビルドできます。ローカルファイルシステムに保存している ZIP ファイルの内容は、次のような構造になっています。

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

これは、現在の OS 設定によっては表示されない隠しディレクトリです。OSに含まれるアプリケーションフックを変更する場合に、このディレクトリが表示されるようにOSを設定する必要があります。

#### .cordova/hooks/ {#cordova-hooks}

This directory contains the [CLI hooks](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). hooks ディレクトリ内のフォルダーには、ビルド中に正確な時点で実行される node.js スクリプトが含まれています。

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

The after-platform_add directory contains the `copy_AMS_Conifg.js` file. このスクリプトは、Adobe Mobile Services 分析を収集できるように設定ファイルをコピーします。

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

The after-prepare directory contains the `copy_resource_files.js` file. このスクリプトは、数多くのアイコンおよびスプラッシュスクリーンの画像をプラットフォーム固有の場所にコピーします。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

The before_platform_add directory contains the `install_plugins.js` file. このスクリプトは、Cordova プラグイン識別子のリストを繰り返し処理して、まだ使用可能でないことが検出されたプラグインをインストールします。

This strategy does not require that you bundle and install the plugins to AEM each time the Maven `content-package:install` command is executed. 別の方法で SCM システムにファイルをチェックインする場合には、バンドルとインストールの作業が繰り返し発生します。

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

必要に応じて他のフックがインクルードされます。次のフックを使用できます（PhoneGap サンプルの hello world アプリに用意されています）。

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### platforms/ {#platforms}

This directory is empty until you execute the `phonegap run <platform>` command on the project. 現在、 `<platform>` またはを使用でき `ios` ま `android`す。

特定のプラットフォーム向けのアプリをビルドすると、対応するディレクトリが作成され、プラットフォーム固有のアプリコードが含められます。

#### plugins/ {#plugins}

The plugins directory is populated by each plugin listed in the `.cordova/hooks/before_platform_add/install_plugins.js` file after you execute the `phonegap run <platform>` command. 初期状態では空になっています。

#### www/ {#www}

www ディレクトリには、アプリの外観および動作を実装するすべての Web コンテンツ（HTML、JS、CSS の各ファイル）が含まれています。次に説明する例外を除き、このコンテンツは AEM から発生し、コンテンツ同期によって静的フォームにエクスポートされます。

#### www/config.xml {#www-config-xml}

The [PhoneGap documentation](https://docs.phonegap.com) refers to this file as a &#39;global configuration file&#39;. The config.xml contains many app properties, such as the name of the app, the app &#39;preferences&#39; (for example whether or not an iOS webview allows overscroll), and plugin dependencies that are *only* consumed by PhoneGap build.

config.xml ファイルは、AEM の静的ファイルで、コンテンツ同期によってそのままエクスポートされます。

#### www/index.html {#www-index-html}

index.html ファイルは、アプリの開始ページにリダイレクトします。

config.xml ファイルには、`content` 要素が含まれています。

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

In [the PhoneGap documentation](https://docs.phonegap.com), this element is described as &quot;The optional &lt;content> element defines the app&#39;s starting page in the top-level web assets directory. デフォルト値は index.html です。これは、プロジェクトのトップレベルの www ディレクトリに配置されるのが通例です」と説明しています。

index.html ファイルが存在しない場合、PhoneGap Build は失敗します。したがって、このファイルは含まれます。

#### www/res {#www-res}

res ディレクトリには、スプラッシュスクリーンの画像およびアイコンが含まれています。The `copy_resource_files.js` script copies the files to their platform-specific locations during the `after_prepare` build phase.

#### www/etc {#www-etc}

慣例により、AEM では /etc ノードに静的 clientlib コンテンツが含まれています。etc ディレクトリには、Topcoat、AngularJS および Geometrixx ng-clientlibsall ライブラリが含まれています。

#### www/apps {#www-apps}

apps ディレクトリには、スプラッシュページに関連するコードが含まれています。AEM アプリのスプラッシュページが備える固有の特性は、ユーザーとの対話なしでアプリを初期化することです。このため、パフォーマンスを最大限に高めるために、アプリの clientlib コンテンツ（CSS と JS の両方）が最小化されます。

#### www/content {#www-content}

content ディレクトリには、アプリの残りの Web コンテンツが含まれています。主に次のファイルをインクルードできます。

* HTML ページコンテンツ（AEM に直接作成されます）
* AEM コンポーネントに関連付けられた画像アセット
* サーバー側スクリプトが生成する JavaScript コンテンツ
* ページまたはコンポーネントコンテンツを説明する JSON ファイル

#### www/package.json {#www-package-json}

The package.json file is a manifest file that lists the files that a **full** Content Sync download includes. このファイルには、コンテンツ同期ペイロードが生成されたタイムスタンプ（`lastModified`）も含まれています。このプロパティは、AEM にアプリの部分的更新を要求するときに使用されます。

#### www/package-update.json {#www-package-update-json}

If this payload is a download of the entire app, this manifest contains the exact listing of files as `package.json`.

However, if this payload is a partial update, `package-update.json` contains only the files that are included in this particular payload.
