---
title: 単一ページアプリケーション
seo-title: 単一ページアプリケーション
description: このページでは、シングルページアプリケーションについて説明します。つまり、デスクトップでもモバイルアプリケーションでも同じように機能するアプリケーションを作成できます。
seo-description: このページでは、シングルページアプリケーションについて説明します。つまり、デスクトップでもモバイルアプリケーションでも同じように機能するアプリケーションを作成できます。
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 51%

---


# 単一ページアプリケーション{#single-page-applications}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

[シングルページアプリ](https://en.wikipedia.org/wiki/Single-page_application) (SPA)は、Webテクノロジーを使用したシームレスなエクスペリエンスを構築する上で最も効果的なパターンと広く受け取られている、重要な大量のアプリケーションに達しています。SPAパターンに従うと、デスクトップやモバイルアプリケーションと同じ動作をしながら、オープンWeb標準での基盤に起因する数多くのデバイスプラットフォームやフォームファクタに到達するアプリケーションを作成できます。

通常、SPAは従来のページベースのWebサイトよりもパフォーマンスが高く表示されます。これは、通常、**完全なHTMLページを読み込むのは**（CSS、JS、サポートフォントコンテンツを含む）1回だけで、状態の変更が発生するたびに必要なものだけです。 状態の変更の発生に必要なものは、選択するテクノロジーのセットによって異なります。通常は、既存の「ビュー」を置き換える単一の HTML フラグメント、新規ビューを接続するための JS コードブロックの実行、必要に応じたクライアント側でのテンプレートのレンダリングが含まれます。状態の変更の速度は、テンプレートのキャッシュメカニズムをサポートすることで、または Adobe PhoneGap を使用する場合はテンプレートコンテンツへのオフラインアクセスによって、さらに改善することができます。

AEM 6.1 では、AEM アプリを利用して SPA をビルドおよび管理できます。この記事では、SPAの概念と、が[AngularJS](https://angularjs.org/)をどのように利用してApp StoreやGoogle Playに自社ブランドを導入するかについて説明します。

## AEM アプリでの SPA {#spa-in-aem-apps}

AEM アプリでシングルページアプリケーションフレームワークを使用すると、パフォーマンスの高い AngularJS アプリを実現できると同時に、作成者（または技術ユーザー以外のユーザー）は、タッチ操作用に最適化されたドラッグアンドドロップ編集環境でアプリのコンテンツを作成および管理できます（この環境は従来、Web サイト管理用でした）。AEM でビルドしたサイトが既に存在する場合があります。AEM アプリでは、コンテンツ、コンポーネント、ワークフロー、アセットおよび権限を簡単に再利用することができます。

## AngularJS アプリケーションモジュール {#angularjs-application-module}

AEM アプリでは、アプリのトップレベルのモジュールを取りまとめるなど、AngularJS 設定の多くが自動で処理されます。デフォルトでは、このモジュールは&#39;AEMAngularApp&#39;という名前で、このモジュールの生成を担当するスクリプトは/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jspで見つかります（またオーバーレイされます）。

アプリの初期化の一部として、アプリが依存するAngularJSモジュールの指定が含まれます。 アプリで使用するモジュールのリストは、/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jspにあるスクリプトによって指定され、独自のアプリのページコンポーネントでオーバーレイして、アプリで必要な追加のAngularJSモジュールを引き込むことができます。 一例として、上記のスクリプトを Geometrixx 実装（/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp にあります）と比較してみてください。

アプリ内の異なる状態間の移動をサポートするために、angular-app-module スクリプトはトップレベルアプリページのすべての下位のページを繰り返し処理して、一連の「ルート」を生成し、Angular の $routeProvider サービスに各パスを設定します。実際の例として、Geometrixx Outdoors版アプリのサンプルで生成されたangular-app-moduleスクリプトを見てみましょう。（リンクにはローカルインスタンスが必要） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

生成された AEMAngularApp を詳細に見ると、一連のルートが次のように指定されています。

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

特に上記のサンプルは、パスの一部としてパラメーターを渡す例を示しています。この例では、指定したパターンを満たすパス(/content/phonegap/geometrixx-outdoors/en/home/products/:id)が要求された場合、そのパスはhome/products.template.htmlテンプレートで処理され、「contentphonegapgeometrixxoutdoorsenhomeproducts」コントローラーを使用する必要があることを示しています。

このルートが要求されたときに読み込むテンプレートは、templateUrl プロパティで指定されています。このテンプレートは、ページにインクルードされた AEM コンポーネントの HTML と、アプリケーションのクライアント側を接続するために必要な AngularJS ディレクティブが含まれたものになります。Geometrixxコンポーネント内のAngularJSディレクティブの例を見るには、swipe-carouselのtemplate.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)の45行目を参照してください。

## ページコントローラー {#page-controllers}

Angular におけるコントローラーの説明は、「Angular スコープを補強するために使用される JavaScript コンストラクター関数です」というものです([source](https://docs.angularjs.org/guide/controller)) AEMアプリの各ページは、`angular`の`frameworkType`を指定する任意のコントローラーで拡張可能なコントローラーに自動的に結線されます。 一例として ng-text コンポーネント（/libs/mobileapps/components/angular/ng-text）および cq:template ノード（このコンポーネントがページに追加されるたびに、確実にこの重要な frameworkType プロパティを含めます）を参照してください。

より複雑なコントローラーの例としては、ng-template-page controller.jspスクリプト（/apps/geometrixx-outdoors-app/components/angular/ng-template-pageにあります）を開きます。 特に興味深いのは実行時に生成される JavaScript コードで、次のようにレンダリングされます。

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

上記の例では、`$routeParams`サービスからパラメーターを取得し、JSONデータが格納されるディレクトリ構造にマッサージします。 この方法でSKU `id`を扱うことで、何千もの異なる製品の製品データをレンダリングできる単一の製品テンプレートを提供できます。 これは、（潜在的に）大規模な製品データベース内の項目ごとに個別のルートを必要とするよりも、拡大／縮小の可能性が非常に高いモデルです。

ここでは、2つのコンポーネントも使用できます。ng-productは、上記の`$http`呼び出しから抽出したデータで範囲を拡張します。 このページには、ng-imageもあり、応答から取得した値で範囲を補うこともできます。 Angularの`$http`サービスにより、各コンポーネントは、要求が完了し、作成された約束が果たされるまで待ちます。

## 次の手順 {#the-next-steps}

シングルページアプリケーションについて学習したら、[PhoneGap CLI によるアプリの開発](/help/mobile/phonegap-apps-pg-cli.md)を参照してください。
