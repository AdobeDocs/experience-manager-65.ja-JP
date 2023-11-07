---
title: アプリの詳細な構造
description: このページでは、アプリ用に作成するページコンポーネントの説明を提供します。このコンポーネントは、 /libs/mobileapps/components/angular/ng-page コンポーネント ( ローカルサーバー上のCRXDE Lite) に基づいています。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '2681'
ht-degree: 0%

---

# アプリの詳細な構造{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

## モバイルアプリのページテンプレート {#page-templates-for-mobile-apps}

アプリ用に作成するページコンポーネントは、 /libs/mobileapps/components/angular/ng-page コンポーネント ([ローカルサーバーでCRXDE Liteで開く](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)) をクリックします。 このコンポーネントには、コンポーネントが継承または上書きする次の JSP スクリプトが含まれています。

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

を使用してアプリケーションの名前を決定します。 `applicationName` プロパティを使用して公開し、pageContext を使用して公開します。

head.jsp と body.jsp が含まれます。

### head.jsp {#head-jsp}

を書き出します。 `<head>` 要素に含める必要があります。

アプリの viewport メタプロパティを上書きする場合は、上書きするファイルがこのファイルになります。

ベストプラクティスに従い、デスクトップアプリケーションではクライアントライブラリの css 部分を head に含め、一方、JS は closing &lt; `body>` 要素を選択します。

### body.jsp {#body-jsp}

angularページの本文は、wcmMode が検出されたか (!= WCMMode.DISABLED) を使用して、ページをオーサリング用に開くか、公開ページとして開くかを判断します。

**オーサーモード**

オーサーモードでは、各ページが個別にレンダリングされます。 Angularは、ページ間のルーティングを処理しないほか、ページのコンポーネントを含む部分的なテンプレートの読み込みに使用される ng-view も使用しません。 代わりに、ページテンプレート (template.jsp) のコンテンツは、 `cq:include` タグを使用します。

この方法を使用すると、作成者機能 ( 段落システム、Sidekick、デザインモードなどのコンポーネントの追加や編集など ) を変更せずに使用できます。 アプリ用のページなど、クライアント側のレンダリングに依存するページは、AEMオーサーモードでは正常に動作しません。

template.jsp インクルードは、 `div` 要素 `ng-controller` ディレクティブ。 この構造により、DOM コンテンツをコントローラーにリンクできます。 したがって、クライアント側でレンダリングされるページは失敗しますが、個々のコンポーネントは正常に機能します（以下のコンポーネントの節を参照）。

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**公開モード**

公開モード（コンテンツ同期を使用してアプリを書き出す場合など）では、すべてのページが単一ページアプリ (SPA) になります。 ( 特にSPAについて学ぶには、Angularチュートリアルを使用します。 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

SPA( `<html>` 要素 ) を参照してください。 このページは、「レイアウトテンプレート」と呼ばれます。 angularの用語では、「。..アプリケーションのすべてのビューで共通のテンプレート」です。 このページを「トップレベルのアプリページ」と見なします。 慣例により、最上位のアプリページは `cq:Page` ルートに最も近い（リダイレクトではない）アプリケーションのノード。

アプリの実際の URI は公開モードでは変更されないので、このページからの外部アセットへの参照には相対パスを使用する必要があります。 したがって、書き出し用に画像をレンダリングする際に、この最上位ページを考慮に入れる特別な画像コンポーネントが提供されます。

SPAの場合、このレイアウトテンプレートページでは、ng-view ディレクティブを持つ div 要素を生成するだけです。

```xml
 <div ng-view ng-class="transition"></div>
```

angularルートサービスは、この要素を使用して、現在のページ（template.jsp に含まれる）のオーサリング可能なコンテンツを含む、アプリ内の各ページのコンテンツを表示します。

body.jsp ファイルには、空の header.jsp と footer.jsp が含まれます。 すべてのページに静的コンテンツを提供する場合は、アプリでこれらのスクリプトを上書きできます。

最後に、JavaScript クライアントライブラリが &lt;body> 要素には、サーバー上で生成される 2 つの特別な JS ファイルが含まれます。 *&lt;page name=&quot;&quot;>*.angular-app-module.js および *&lt;page name=&quot;&quot;>*.angular — アプリ — コントローラ.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

このスクリプトは、アプリケーションのAngularモジュールを定義します。 このスクリプトの出力は、テンプレートのコンポーネントの残りの部分でが `html` ng-page.jsp の要素。次の属性が含まれます。

```xml
ng-app="<c:out value='${applicationName}'/>"
```

この属性は、この DOM 要素のコンテンツが次のモジュールにリンクされている必要があることをAngularに示します。 このモジュールは、ビュー (AEM内のリソースは cq:Page です ) を対応するコントローラとリンクします。

また、このモジュールは、 `AppController` それが公開する `wcmMode` 変数をスコープに設定し、コンテンツ同期更新ペイロードの取得元となる URI を設定します。

最後に、このモジュールは、Angularの$routeProvider への設定エントリとして含め、各ページのルートフラグメントの内容を (angular-route-fragment.js セレクターおよび拡張を介して ) 繰り返し処理し、レンダリングします。 つまり、 $routeProvider は、特定のパスが要求されたときにレンダリングするコンテンツをアプリに伝えます。

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

このスクリプトは、次の形式を取る必要がある JavaScript フラグメントを生成します。

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

このコードは、$routeProvider (angular-app-module.js.jsp で定義 ) に対して、&lt;path>&#39;は次の場所のリソースによって処理されます： `templateUrl`そして、次の方法で配線されています。 `controller` （次に行く）。

必要に応じて、このスクリプトを上書きして、変数を持つパスを含む、より複雑なパスを処理できます。 この例は、AEMと共にインストールされる/apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp スクリプトで確認できます。

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

angularでは、コントローラは$scope 内の変数をワイヤアップし、ビューに公開します。 angular-app-controllers.js.jsp スクリプトは、angular-app-module.js.jsp で示すパターンに従います。このスクリプトは、各子孫ページ（それ自体も含む）を繰り返し処理し、各ページが定義するコントローラフラグメントを (controller.js.jsp を介して ) 出力します。 定義するモジュールは、と呼ばれます。 `cqAppControllers` およびをトップレベルのアプリモジュールの依存関係としてリストし、ページコントローラーを使用可能にする必要があります。

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp スクリプトは、各ページのコントローラーフラグメントを生成します。 このコントローラフラグメントは、次の形式を取ります。

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

The `data` 変数には、Angular `$http.get` メソッド。 このページに含まれる各コンポーネントでは、必要に応じて、一部の.json コンテンツを (angular.json.jsp スクリプトを介して ) 使用可能にし、解決時にこのリクエストのコンテンツに基づいて動作させることができます。 要求は、単にファイルシステムにアクセスするので、モバイルデバイスでは非常に高速です。

この方法でコンポーネントをコントローラーの一部にするには、 /libs/mobileapps/components/angular/ng-component コンポーネントを拡張し、 `frameworkType: angular` プロパティ。

### template.jsp {#template-jsp}

最初に body.jsp の節で導入された、template.jsp には、ページの parsys が含まれています。 公開モードでは、このコンテンツは直接参照されます ( &lt;page-path>.template.html) と共に使用され、$routeProvider に設定された templateUrl を介してSPAに読み込まれます。

このスクリプトの parsys は、任意の種類のコンポーネントを受け入れるように設定できます。 ただし、(SPAとは異なり、) 従来の Web サイト用に構築されたコンポーネントを扱う場合は、注意が必要です。 例えば、基盤画像コンポーネントは、アプリ内のアセットを参照するように設計されていないので、トップレベルのアプリページでのみ正しく機能します。

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

このスクリプトは、トップレベルのAngularアプリモジュールのAngular依存関係を出力するだけです。 angular-app-module.js.jsp で参照されています。

### header.jsp {#header-jsp}

静的コンテンツをアプリの上部に配置するスクリプトです。 このコンテンツは、ng-view の範囲外で、トップレベルのページに含まれます。

### footer.jsp {#footer-jsp}

静的コンテンツをアプリの下部に配置するスクリプトです。 このコンテンツは、ng-view の範囲外で、トップレベルのページに含まれます。

### js_clientlibs.jsp {#js-clientlibs-jsp}

JavaScript clientlibs を含めるには、このスクリプトをオーバーライドします。

### css_clientlibs.jsp {#css-clientlibs-jsp}

CSS clientlibs を含めるには、このスクリプトをオーバーライドします。

## アプリコンポーネント {#app-components}

アプリケーションコンポーネントは、AEMインスタンス（パブリッシュまたはオーサー）上で動作するだけでなく、コンテンツ同期を介してアプリケーションコンテンツをファイルシステムに書き出す場合にも動作する必要があります。 したがって、コンポーネントには次の特性が含まれている必要があります。

* PhoneGap アプリケーション内のすべてのアセット、テンプレートおよびスクリプトは、相対的に参照する必要があります。
* AEMインスタンスがオーサーモードまたはパブリッシュモードで動作している場合、リンクの処理は異なります。

### 相対的なアセット {#relative-assets}

PhoneGap アプリケーション内の特定のアセットの URI は、プラットフォームごとに異なるだけでなく、アプリのインストールごとに一意です。 例えば、iOSシミュレーターで実行されているアプリの次の URI に注意してください。

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

パスの GUID「24BA22ED-7D06-4330-B7EB-F6FC73251CA3」をメモします。

PhoneGap 開発者は、関心のあるコンテンツは www ディレクトリの下に配置されます。 アプリアセットにアクセスするには、相対パスを使用します。

この問題を組み合わせるために、PhoneGap アプリケーションでは単一ページアプリ (SPA) パターンを使用し、ベース URI（ハッシュを除く）が変更されないようにします。 したがって、参照するすべてのアセット、テンプレートまたはスクリプトは、最上位のページを基準とし**なければなりません。 **トップレベルのページでは、次の理由により、Angularルーティングとコントローラを初期化します。 `*<name>*.angular-app-module.js` および `*<name>*.angular-app-controllers.js`. このページは、sling:redirect を拡張しないリポジトリのルートに最も近いページにする必要があります。

相対パスの処理には、次のいくつかのヘルパーメソッドを使用できます。

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

使用例を確認するには、/libs/mobileapps/components/components にある mobileapps ソースを開きます。angular

### リンク {#links}

リンクは、 `ng-click="go('/path')"` 関数を使用して、すべての WCM モードをサポートします。 この関数は、スコープ変数の値に応じて、リンクアクションを正しく決定します。

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

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

このスクリプトは、編集モードが検出されたときに、コンポーネントのコンテンツまたは適切なプレースホルダーを表示します。

#### template.jsp {#template-jsp-1}

template.jsp スクリプトは、コンポーネントのマークアップをレンダリングします。 問題のコンポーネントがAEMから抽出された JSON データ (「ng-text」: /libs/mobileapps/components/angular/ng-text/template.jspなど ) によって駆動される場合、このスクリプトは、ページのコントローラースコープで公開されるデータを使用してマークアップを配線します。

ただし、パフォーマンス要件によっては、クライアント側のテンプレート（データ連結）を実行しないことが求められる場合があります。 この場合は、サーバー側でコンポーネントのマークアップをレンダリングし、ページテンプレートコンテンツに含めます。

#### overhead.jsp {#overhead-jsp}

JSON データによって駆動されるコンポーネント（「ng-text」など）では、overhead.jsp を使用して template.jsp からすべての Java コードを削除できます（例： /libs/mobileapps/components/text）。 その後、template.jsp から参照され、リクエストで公開されるすべての変数を使用できます。 この方法では、ロジックをプレゼンテーションから分離し、新しいコンポーネントを既存のコンポーネントから派生させる場合にコピー&amp;貼り付ける必要があるコードの量を制限します。

#### controller.js.jsp {#controller-js-jsp-1}

「AEMページテンプレート」で説明したように、各コンポーネントは JavaScript フラグメントを出力し、 `data` 約束。 angular規則に従い、コントローラはスコープに変数を割り当てる場合にのみ使用する必要があります。

#### angular.json.jsp {#angular-json-jsp}

このスクリプトはフラグメントとしてページ全体に含まれます。&lt;page-name>ng-page を拡張する各ページ用に書き出される。angular.json&#39;ファイル。 このファイルでは、コンポーネント開発者は、コンポーネントで必要な JSON 構造を公開できます。 「ng-text」の例では、この構造には、コンポーネントのテキストコンテンツと、コンポーネントにリッチテキストが含まれているかどうかを示すフラグが含まれます。

Geometrixxアウトドアアプリ製品コンポーネントは、より複雑な例です (/apps/geometrixx-outdoors-app/components/angular/ng-product)。

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

## CLI Assets ダウンロードの内容 {#contents-of-the-cli-assets-download}

アプリコンソールから CLI アセットをダウンロードして、特定のプラットフォームに合わせて最適化し、PhoneGap コマンドライン統合 (CLI)API を使用してアプリを構築します。 ローカルファイルシステムに保存する ZIP ファイルの内容は、次の構造を持ちます。

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

これは隠しディレクトリで、現在の OS の設定によっては表示されない場合があります。 このディレクトリが含まれるアプリフックを変更する予定がある場合に、このディレクトリが表示されるように OS を設定する必要があります。

#### .cordova/hooks/ {#cordova-hooks}

このディレクトリには、 [CLI フック](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). hooks ディレクトリ内のフォルダーには、ビルド中の正確な時点で実行される node.js スクリプトが含まれます。

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add ディレクトリには、 `copy_AMS_Conifg.js` ファイル。 次のスクリプトは、Mobile Services 分析のコレクションをサポートするAdobeファイルをコピーします。

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

after-prepare ディレクトリには、 `copy_resource_files.js` ファイル。 次のスクリプトは、複数のアイコンとスプラッシュ画面の画像をプラットフォーム固有の場所にコピーします。

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add ディレクトリには、 `install_plugins.js` ファイル。 このスクリプトは、Cordova プラグイン識別子のリストを繰り返し処理し、まだ使用できないことを検出した識別子をインストールします。

この方法では、Maven を呼び出すたびに、プラグインをバンドルしてAEMにインストールする必要はありません。 `content-package:install` コマンドが実行されます。 ファイルを SCM システムにチェックインする別の方法では、バンドルとインストールの作業を繰り返し行う必要があります。

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

必要に応じて、他のフックを含めます。 次のフックを使用できます（Phonegap サンプルの hello world アプリで提供されています）。

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

このディレクトリは、 `phonegap run <platform>` コマンドを使用して、プロジェクトに対して実行します。 現在、 `<platform>` 次のいずれかを指定できます。 `ios` または `android`.

特定のプラットフォーム向けにアプリを構築すると、対応するディレクトリが作成され、プラットフォーム固有のアプリコードが含まれます。

#### plugins/ {#plugins}

plugins ディレクトリには、 `.cordova/hooks/before_platform_add/install_plugins.js` ファイルを削除します。 `phonegap run <platform>` コマンドを使用します。 ディレクトリは最初は空です。

#### www/ {#www}

www ディレクトリには、アプリの外観と動作を実装するすべての Web コンテンツ (HTML、JS、CSS ファイル ) が含まれています。 以下に説明する例外を除き、このコンテンツはAEMから生成され、コンテンツ同期を介して静的フォームに書き出されます。

#### www/config.xml {#www-config-xml}

PhoneGap ドキュメント (`https://docs.phonegap.com`) は、このファイルを「グローバル設定ファイル」と呼びます。 config.xml には、アプリの名前、アプリの「環境設定」( 例えば、iOS Web ビューでオーバースクロールが許可されているかどうか )、次のようなプラグインの依存関係など、多くのアプリのプロパティが含まれます。 *のみ* PhoneGap Build で使用されます。

config.xml ファイルはAEMの静的ファイルで、コンテンツ同期を介してそのまま書き出されます。

#### www/index.html {#www-index-html}

index.html ファイルは、アプリの開始ページにリダイレクトします。

config.xml ファイルには、 `content` 要素：

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

PhoneGap ドキュメント (`https://docs.phonegap.com`) の場合、この要素は、「 &lt;content> 要素は、トップレベルの web assets ディレクトリにアプリの開始ページを定義します。 デフォルト値は index.html で、これは通常、プロジェクトの最上位の www ディレクトリに表示されます。

index.html ファイルが存在しない場合、PhoneGap Build は失敗します。 したがって、このファイルが含まれます。

#### www/res {#www-res}

res ディレクトリには、スプラッシュスクリーンの画像とアイコンが含まれています。 The `copy_resource_files.js` スクリプトは、 `after_prepare` ビルドフェーズ。

#### www/etc {#www-etc}

慣例により、 AEMでは、 /etc ノードに静的 clientlib コンテンツが含まれます。 etc ディレクトリには、Topcoat、AngularJS、およびGeometrixxng-clientlibsall ライブラリが含まれます。

#### www/apps {#www-apps}

apps ディレクトリには、スプラッシュページに関連するコードが含まれます。 AEMアプリのスプラッシュページの独自の特徴は、ユーザーの操作なしでアプリを初期化する点です。 したがって、アプリの clientlib コンテンツ（CSS と JS の両方）は、パフォーマンスを最大限に高めるために最小限に抑えられます。

#### www/content {#www-content}

コンテンツディレクトリには、アプリの残りの Web コンテンツが含まれます。 次のファイルを含めることができますが、これらに限定されません。

* HTMLページコンテンツ (AEMで直接作成 )
* AEMコンポーネントに関連付けられた画像アセット
* サーバーサイドスクリプトが生成する JavaScript コンテンツ
* ページまたはコンポーネントのコンテンツを記述する JSON ファイル

#### www/package.json {#www-package-json}

package.json ファイルは、 **完全** コンテンツ同期のダウンロードにはが含まれます。 このファイルには、コンテンツ同期ペイロードが生成されたタイムスタンプ ( `lastModified`) をクリックします。 このプロパティは、AEMからアプリの部分的な更新を要求する場合に使用されます。

#### www/package-update.json {#www-package-update-json}

このペイロードがアプリ全体のダウンロードである場合、このマニフェストには、ファイルの正確なリストが次のように含まれます。 `package.json`.

ただし、このペイロードが部分的な更新の場合、 `package-update.json` には、この特定のペイロードに含まれるファイルのみが含まれます。

### 次の手順 {#the-next-steps}

アプリの分析について学習したら、 [単一ページアプリケーション](/help/mobile/phonegap-single-page-applications.md).
