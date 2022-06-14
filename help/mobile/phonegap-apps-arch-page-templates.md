---
title: モバイルアプリのページテンプレート
seo-title: Page Templates for Mobile Apps
description: このページでは、モバイルアプリのページテンプレートについて説明します。
seo-description: Follow this page to learn about page templates for mobile apps.
uuid: ef469796-10f5-44f4-a5c7-25025ca192b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: f45d8a9b-14d6-468f-a44c-3933e962922c
exl-id: 7f00d426-4d28-41ee-8c54-636349e48669
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2649'
ht-degree: 67%

---

# モバイルアプリのページテンプレート {#page-templates-for-mobile-apps}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

## モバイルアプリのページテンプレート {#page-templates-for-mobile-apps-1}

アプリ用に作成するページコンポーネントは、 /libs/mobileapps/components/angular/ng-page コンポーネント ([ローカルサーバーでCRXDE Liteで開く](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)) をクリックします。 このコンポーネントには次の JSP スクリプトが含まれており、これらのスクリプトを自分のコンポーネントで継承またはオーバーライドします。

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

を `<head>` 要素に含めることができます。

アプリの viewport メタプロパティをオーバーライドする場合は、これがオーバーライド対象のファイルになります。

ベストプラクティスに従い、デスクトップアプリケーションではクライアントライブラリの css 部分を head に含め、一方、JS は closing &lt; `body>` 要素。

### body.jsp {#body-jsp}

Angular ページのボディは、wcm モードが検出されたかどうか（! = WCMMode.DISABLED）に応じてレンダリングが異なり、ページを作成用に開くか、公開済みページとして開くかが決まります。

**オーサーモード**

オーサーモードでは、各ページが個別にレンダリングされます。 Angularは、ページ間のルーティングを処理しないほか、ページのコンポーネントを含む部分的なテンプレートの読み込みに使用される ng-view も使用しません。 その代わり、ページテンプレート（template.jsp）のコンテンツが `cq:include` タグによってサーバー側にインクルードされます。

この方法により、何も変更を加えることなく、オーサー機能（段落システム、サイドキック、デザインモードでのコンポーネントの追加および編集など）を使用可能にすることができます。アプリ向けのページなどクライアント側のレンダリングを利用するページは、AEM オーサーモードではパフォーマンスがよくありません。

template.jsp インクルードは `div` 要素 `ng-controller` ディレクティブ。 この構造により、DOM コンテンツをコントローラーとリンクできます。このため、クライアント側で自身をレンダリングするページは失敗しますが、同じようにレンダリングする個々のコンポーネントは正常に機能します（下のコンポーネントに関する節を参照）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**パブリッシュモード**

公開モード（コンテンツ同期を使用してアプリを書き出す場合など）では、すべてのページが単一ページアプリ (SPA) になります。 ( 特にSPAについて学ぶには、Angularチュートリアルを使用します。 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

SPA( `<html>` 要素 ) を参照してください。 このページは、「レイアウトテンプレート」と呼ばれています。Angular 用語では、「アプリケーション内のすべてのビューに共通するテンプレート」となります。このページは、「トップレベルのアプリページ」と考えてください。慣例により、最上位のアプリページは `cq:Page` ルートに最も近い（リダイレクトではない）アプリケーションのノード。

パブリッシュモードではアプリの実際の URI が変わらないので、このページから外部アセットを参照するには相対パスを使用する必要があります。したがって、書き出し用に画像をレンダリングする際に、この最上位ページを考慮に入れる特別な画像コンポーネントが提供されます。

SPA として、このレイアウトテンプレートページは単に ng-view ディレクティブとともに div 要素を生成します。

```xml
 <div ng-view ng-class="transition"></div>
```

angularルートサービスは、この要素を使用して、現在のページ（template.jsp に含まれる）のオーサリング可能なコンテンツを含む、アプリ内の各ページのコンテンツを表示します。

body.jsp ファイルには、header.jsp および footer.jsp が空の状態でインクルードされています。どのページにも静的コンテンツを提供する場合には、アプリでこれらのスクリプトをオーバーライドできます。

最後に、JavaScript クライアントライブラリが &lt;body> 要素には、サーバー上で生成される 2 つの特別な JS ファイルが含まれます。 *&lt;page name=&quot;&quot;>*.angular-app-module.js および *&lt;page name=&quot;&quot;>*.angular — アプリ — コントローラ.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

このスクリプトでは、アプリケーションの Angular モジュールを定義します。このスクリプトの出力は、テンプレートのコンポーネントの残りの部分が `html` 要素を利用して ng-page.jsp に生成するマークアップにリンクされます。ng-page.jsp には、次の属性が含まれています。

```xml
ng-app="<c:out value='${applicationName}'/>"
```

この属性は Angular に対して、この DOM 要素のコンテンツを次のモジュールにリンクする必要があることを示します。このモジュールは、ビュー（AEM では cq:Page リソース）を対応するコントローラーとリンクします。

また、`AppController` 変数をスコープに公開するトップレベルのコントローラーを `wcmMode` という名前で定義し、コンテンツ同期更新ペイロードを取得する URI を設定します。

最後に、このモジュールは、Angularの$routeProvider への設定エントリとして含め、各ページのルートフラグメントの内容を (angular-route-fragment.js セレクターおよび拡張を介して ) 繰り返し処理し、レンダリングします。 つまり、$routeProvider は特定のパスが要求されたときにどのコンテンツをレンダリングするかをアプリに指示します。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

このスクリプトは、次の形式を取る JavaScript フラグメントを生成します。

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

このコードは、$routeProvider (angular-app-module.js.jsp で定義 ) に対して、&lt;path>&#39;は次の場所のリソースによって処理されます： `templateUrl`で、 `controller` （次に行く）

必要に応じて、変数があるものも含めさらに複雑なパスを処理するように、このスクリプトをオーバーライドできます。この一例を、AEM とともにインストールされる /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp スクリプトで確認できます。

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Angular では、コントローラーが変数を $scope にワイヤアップしてビューに公開します。angular-app-controllers.js.jsp スクリプトは、angular-app-module.js.jsp で示すパターンに従います。このスクリプトは、各子孫ページ（それ自体も含む）を繰り返し処理し、各ページが定義するコントローラフラグメントを (controller.js.jsp を介して ) 出力します。 このスクリプトが定義しているモジュールは、`cqAppControllers` という名前であり、ページコントローラーが使用可能になるようにトップレベルアプリモジュールの依存関係としてリストされる必要があります。

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

なお、 `data` 変数には、Angular `$http.get` メソッド。 このページにインクルードされている各コンポーネントでは、必要に応じて一部の .json コンテンツを（その angular.json.jsp スクリプトを利用して）使用可能にし、この要求を解決する際に要求のコンテンツに対して処理を実行できます。要求は、単にファイルシステムにアクセスするだけなので、モバイルデバイスでは非常に高速です。

このようにコンポーネントをコントローラーの一部にするには、コンポーネントを /libs/mobileapps/components/angular/ng-component コンポーネントで拡張し、コンポーネントに `frameworkType: angular`   プロパティを含める必要があります。

### template.jsp {#template-jsp}

最初に body.jsp の節で導入された、template.jsp には、ページの parsys が含まれています。 パブリッシュモードでは、このコンテンツは（&lt;ページパス>.template.html で）直接参照され、$routeProvider に設定された templateUrl によって SPA に読み込まれます。

このスクリプトの parsys は、任意のタイプのコンポーネントを受け入れるように設定できます。ただし、（SPA ではなく）従来の Web サイト向けにビルドされたコンポーネントを扱うときには注意が必要です。例えば、基盤画像コンポーネントは、アプリ内部にあるアセットを参照するように設計されていないため、トップレベルアプリページでのみ正しく機能します。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

このスクリプトは、単にトップレベルの Angular アプリモジュールの Angular 依存関係を出力します。angular-app-module.js.jsp で参照されています。

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

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

パスの GUID が「24BA22ED-7D06-4330-B7EB-F6FC73251CA3」となっています。

PhoneGap 開発者に関係するコンテンツは、www ディレクトリの下にあります。アプリアセットにアクセスするには、相対パスを使用します。

問題が複雑なのは、PhoneGap アプリケーションではシングルページアプリ（SPA）パターンを使用しているので、基準 URI が（ハッシュを除いて）変更されないことです。したがって、参照するすべてのアセット、テンプレートまたはスクリプトは、最上位のページを基準とし**なければなりません。 **トップレベルのページでは、次の理由により、Angularルーティングとコントローラを初期化します。 `<name>.angular-app-module.js` および `<name>.angular-app-controllers.js`. このページは、sling:redirect を拡張しないリポジトリのルートに最も近いページにする必要があります。

次の複数のヘルパーメソッドで相対パスに対処できます。

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

使用例を確認するには、/libs/mobileapps/components/components にある mobileapps ソースを開きます。angular

### リンク {#links}

リンクでは `ng-click="go('/path')"` 関数を使用して、すべての WCM モードをサポートします。 この関数は、スコープ変数の値を利用して、リンクアクションを正しく判別します。

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

条件 `$scope.wcmMode == true` 各ナビゲーションイベントは通常の方法で処理され、結果として URL のパスやページ部分に対する変更が生じます。

または、 `$scope.wcmMode == false`を指定した場合、各ナビゲーションイベントによって URL のハッシュ部分が変更され、Angularの ngRoute モジュールによって内部的に解決されます。

### コンポーネントスクリプトの詳細 {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

このスクリプトは、編集モードが検出されたときにコンポーネントコンテンツまたは適切なプレースホルダーを表示します。

### template.jsp {#template-jsp-1}

template.jsp スクリプトは、コンポーネントのマークアップをレンダリングします。問題のコンポーネントが、AEMから抽出された JSON データ（「ng-text」など）によって駆動される場合：/libs/mobileapps/components/angular/ng-text/template.jsp) の場合、このスクリプトは、ページのコントローラースコープで公開されるデータを使用してマークアップを配線します。

ただし、パフォーマンス要件のために、クライアント側でテンプレート化（データ連結とも呼ばれます）を実行しないように指示されることがあります。この場合は、単にサーバー側でコンポーネントのマークアップをレンダリングし、それをページテンプレートコンテンツにインクルードします。

### overhead.jsp {#overhead-jsp}

JSON データ（「ng-text」など）によって駆動されるコンポーネントでは、次のようになります。/libs/mobileapps/components/text) では、overhead.jsp を使用して、template.jsp からすべての Java コードを削除できます。 overhead.jsp は template.jsp から参照され、overhead.jsp が要求で公開している変数は使用可能です。この方法により、ロジックと表示を分離でき、既存のコンポーネントから新規のコンポーネントを生成する場合にコピーして貼り付ける必要があるコードの量を抑えることができます。

### controller.js.jsp {#controller-js-jsp-1}

詳しくは、 [AEM Page Templates](/help/mobile/apps-architecture.md)の場合、各コンポーネントは JavaScript フラグメントを出力し、 `data` 約束。 Angular の表記規則に従って、コントローラーはスコープに変数を割り当てる目的でのみ使用します。

### angular.json.jsp {#angular-json-jsp}

このスクリプトは、ng-page を拡張するページごとにエクスポートされるページ全体の &lt;ページ名>.angular.json ファイルにフラグメントとしてインクルードされます。このファイルで、コンポーネント開発者はコンポーネントで必要な任意の JSON 構造を公開できます。「ng-text」の例の場合、この構造に含まれているのは、コンポーネントのテキストコンテンツと、コンポーネントにリッチテキストが含まれているかどうかを示すフラグだけです。

さらに複雑な例が We.Retail アプリ製品コンポーネントです（/apps/weretail-app/components/angular/ng-product）。

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

これは、現在の OS 設定によっては表示されない隠しディレクトリです。このディレクトリが含まれるアプリフックを変更する予定がある場合に、このディレクトリが表示されるように OS を設定する必要があります。

### .cordova/hooks/ {#cordova-hooks}

このディレクトリには、 [CLI フック](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). hooks ディレクトリ内のフォルダーには、ビルド中に正確な時点で実行される node.js スクリプトが含まれています。

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add ディレクトリには、 `copy_AMS_Conifg.js` ファイル。 このスクリプトは、Adobe Mobile Services 分析を収集できるように設定ファイルをコピーします。

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

after-prepare ディレクトリには、 `copy_resource_files.js` ファイル。 このスクリプトは、数多くのアイコンおよびスプラッシュスクリーンの画像をプラットフォーム固有の場所にコピーします。

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add ディレクトリには、 `install_plugins.js` ファイル。 このスクリプトは、Cordova プラグイン識別子のリストを繰り返し処理して、まだ使用可能でないことが検出されたプラグインをインストールします。

この方法では、Maven を呼び出すたびに、プラグインをバンドルしてAEMにインストールする必要はありません `content-package:install` コマンドが実行されます。 別の方法で SCM システムにファイルをチェックインする場合には、バンドルとインストールの作業が繰り返し発生します。

### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

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

### platforms/ {#platforms}

このディレクトリは、 `phonegap run *<platform>*` コマンドを使用して、プロジェクトに対して実行します。 現在、 `*<platform>*` 次のいずれかを指定できます。 `ios` または `android`.

特定のプラットフォーム向けのアプリをビルドすると、対応するディレクトリが作成され、プラットフォーム固有のアプリコードが含められます。

### plugins/ {#plugins}

plugins ディレクトリには、 `.cordova/hooks/before_platform_add/install_plugins.js` ファイルを削除します。 `phonegap run *<platform>*` コマンドを使用します。 初期状態では空になっています。

### www/ {#www}

www ディレクトリには、アプリの外観および動作を実装するすべての Web コンテンツ（HTML、JS、CSS の各ファイル）が含まれています。次に説明する例外を除き、このコンテンツは AEM から発生し、コンテンツ同期によって静的フォームにエクスポートされます。

### www/config.xml {#www-config-xml}

この [PhoneGap ドキュメント](https://docs.phonegap.com) は、このファイルを「グローバル設定ファイル」として参照します。 config.xml には、アプリの名前、アプリの「環境設定」( 例えば、iOS Web ビューでオーバースクロールが可能かどうか )、および次のようなプラグインの依存関係が含まれます。 *のみ* PhoneGap Build で使用されます。

config.xml ファイルは、AEM の静的ファイルで、コンテンツ同期によってそのままエクスポートされます。

### www/index.html {#www-index-html}

index.html ファイルは、アプリの開始ページにリダイレクトします。

config.xml ファイルには、`content` 要素が含まれています。

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

In [PhoneGap ドキュメント](https://docs.phonegap.com)の場合、この要素は、「 &lt;content> 要素は、トップレベルの web assets ディレクトリにアプリの開始ページを定義します。 デフォルト値は index.html です。これは、プロジェクトのトップレベルの www ディレクトリに配置されるのが通例です」と説明しています。

index.html ファイルが存在しない場合、PhoneGap Build は失敗します。したがって、このファイルが含まれます。

### www/res {#www-res}

res ディレクトリには、スプラッシュスクリーンの画像およびアイコンが含まれています。この `copy_resource_files.js` スクリプトは、 `after_prepare` 構築フェーズ。

### www/etc {#www-etc}

慣例により、AEM では /etc ノードに静的 clientlib コンテンツが含まれています。etc ディレクトリには、Topcoat、AngularJS および We.Retail ng-clientlibsall ライブラリが含まれています。

### www/apps {#www-apps}

apps ディレクトリには、スプラッシュページに関連するコードが含まれています。AEM アプリのスプラッシュページが備える固有の特性は、ユーザーとの対話なしでアプリを初期化することです。このため、パフォーマンスを最大限に高めるために、アプリの clientlib コンテンツ（CSS と JS の両方）が最小化されます。

### www/content {#www-content}

content ディレクトリには、アプリの残りの Web コンテンツが含まれています。主に次のファイルをインクルードできます。

* HTML ページコンテンツ（AEM に直接作成されます）
* AEM コンポーネントに関連付けられた画像アセット
* サーバー側スクリプトが生成する JavaScript コンテンツ
* ページまたはコンポーネントコンテンツを説明する JSON ファイル

### www/package.json {#www-package-json}

package.json ファイルは、 **完全** コンテンツ同期のダウンロードにはが含まれます。 このファイルには、コンテンツ同期ペイロードが生成されたタイムスタンプ（`lastModified`）も含まれています。このプロパティは、AEM にアプリの部分的更新を要求するときに使用されます。

### www/package-update.json {#www-package-update-json}

このペイロードがアプリ全体のダウンロードである場合、このマニフェストには、ファイルの正確なリストが `package.json`.

ただし、このペイロードが部分的な更新の場合、 `package-update.json` には、この特定のペイロードに含まれるファイルのみが含まれます。
