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
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 51%

---

# 単一ページアプリケーション{#single-page-applications}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

[シングルページアプリケーション](https://en.wikipedia.org/wiki/Single-page_application) (SPA)は、Webテクノロジーでシームレスなエクスペリエンスを構築するための最も効果的なパターンと見なされ、クリティカルマスに達しています。SPAのパターンに従うことで、デスクトップまたはモバイルアプリケーションと同じ動作をするが、オープンWeb標準での基盤が原因で多数のデバイスプラットフォームやフォームファクターに到達するアプリケーションを作成できます。

通常、SPAは、完全なHTMLページ&#x200B;**を1回**（CSS、JS、サポートフォントコンテンツを含む）だけ読み込み、アプリで状態の変更が発生するたびに必要なもののみを読み込むので、従来のページベースのWebサイトよりもパフォーマンスが高くなります。 状態の変更の発生に必要なものは、選択するテクノロジーのセットによって異なります。通常は、既存の「ビュー」を置き換える単一の HTML フラグメント、新規ビューを接続するための JS コードブロックの実行、必要に応じたクライアント側でのテンプレートのレンダリングが含まれます。状態の変更の速度は、テンプレートのキャッシュメカニズムをサポートすることで、または Adobe PhoneGap を使用する場合はテンプレートコンテンツへのオフラインアクセスによって、さらに改善することができます。

AEM 6.1 では、AEM アプリを利用して SPA をビルドおよび管理できます。この記事では、SPAの背後にある概念と、[AngularJS](https://angularjs.org/)を活用してApp StoreやGoogle Playにブランドを導き出す方法について説明します。

## AEM アプリでの SPA {#spa-in-aem-apps}

AEM アプリでシングルページアプリケーションフレームワークを使用すると、パフォーマンスの高い AngularJS アプリを実現できると同時に、作成者（または技術ユーザー以外のユーザー）は、タッチ操作用に最適化されたドラッグアンドドロップ編集環境でアプリのコンテンツを作成および管理できます（この環境は従来、Web サイト管理用でした）。AEM でビルドしたサイトが既に存在する場合があります。AEM アプリでは、コンテンツ、コンポーネント、ワークフロー、アセットおよび権限を簡単に再利用することができます。

## AngularJS アプリケーションモジュール {#angularjs-application-module}

AEM アプリでは、アプリのトップレベルのモジュールを取りまとめるなど、AngularJS 設定の多くが自動で処理されます。デフォルトでは、このモジュールの名前は「AEMAngularApp」で、このモジュールの生成を担当するスクリプトは/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jspで見つかります（また、オーバーレイされます）。

アプリの初期化の一部として、アプリが依存するAngularJSモジュールを指定する必要があります。 アプリが使用するモジュールのリストは、/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jspにあるスクリプトで指定され、アプリのページコンポーネントでオーバーレイして、アプリが必要とする追加のAngularJSモジュールを取り込むことができます。 一例として、上記のスクリプトを Geometrixx 実装（/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp にあります）と比較してみてください。

アプリ内の異なる状態間の移動をサポートするために、angular-app-module スクリプトはトップレベルアプリページのすべての下位のページを繰り返し処理して、一連の「ルート」を生成し、Angular の $routeProvider サービスに各パスを設定します。この動作が実際にどのように見えるかの例については、Geometrixx Outdoorsアプリのサンプルで生成されたangularアプリモジュールスクリプトを参照してください。（リンクにはローカルインスタンスが必要） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

生成された AEMAngularApp を詳細に見ると、一連のルートが次のように指定されています。

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

特に上記のサンプルは、パスの一部としてパラメーターを渡す例を示しています。この例では、指定されたパターンを満たすパス(/content/phonegap/geometrixx-outdoors/en/home/products/:id)が要求された場合、home/products.template.htmlテンプレートでそのパスを処理し、「contentphonegapgeometrixxoutdoorsenhomeproducts」コントローラーを使用する必要があることを示しています。

このルートが要求されたときに読み込むテンプレートは、templateUrl プロパティで指定されています。このテンプレートは、ページにインクルードされた AEM コンポーネントの HTML と、アプリケーションのクライアント側を接続するために必要な AngularJS ディレクティブが含まれたものになります。Geometrixxコンポーネント内のAngularJSディレクティブの例については、swipe-carouselのtemplate.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)の45行目を参照してください。

## ページコントローラー {#page-controllers}

Angular におけるコントローラーの説明は、「Angular スコープを補強するために使用される JavaScript コンストラクター関数です」というものです([source](https://docs.angularjs.org/guide/controller)) AEM Appの各ページは、`frameworkType`を`angular`と指定する任意のコントローラーで拡張できるコントローラーに自動的に接続されます。 一例として ng-text コンポーネント（/libs/mobileapps/components/angular/ng-text）および cq:template ノード（このコンポーネントがページに追加されるたびに、確実にこの重要な frameworkType プロパティを含めます）を参照してください。

より複雑なコントローラの例については、 ng-template-page controller.jspスクリプト（ /apps/geometrixx-outdoors-app/components/components/template/ng-template-pageにある）を開きます。 特に興味深いのは実行時に生成される JavaScript コードで、次のようにレンダリングされます。

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

上記の例では、`$routeParams`サービスからパラメーターを取得し、JSONデータが格納されるディレクトリ構造にマッサージすることに注意してください。 この方法でsku `id`を扱うことで、数千もの異なる製品の製品データをレンダリングできる単一の製品テンプレートを提供できます。 これは、（潜在的に）大規模な製品データベース内の項目ごとに個別のルートを必要とするよりも、拡大／縮小の可能性が非常に高いモデルです。

また、ここでは2つのコンポーネントが動作します。ng-productは、上記の`$http`呼び出しから抽出したデータで範囲を拡張します。 また、このページにはng-imageがあり、応答から取得した値でスコープを補強します。 angularの`$http`サービスにより、各コンポーネントは、リクエストが完了し、作成されたプロミスが満たされるまで、辛抱強く待ちます。

## 次の手順 {#the-next-steps}

シングルページアプリケーションについて学習したら、[PhoneGap CLI によるアプリの開発](/help/mobile/phonegap-apps-pg-cli.md)を参照してください。
