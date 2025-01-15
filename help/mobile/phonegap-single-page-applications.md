---
title: 単一ページアプリケーション
description: このページでは、単一ページアプリケーションについて説明します。つまり、デスクトップアプリケーションやモバイルアプリケーションと同じように動作するアプリケーションを作成できます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# 単一ページアプリケーション{#single-page-applications}

{{ue-over-mobile}}

[ シングルページアプリケーション ](https://en.wikipedia.org/wiki/Single-page_application) （SPA）は、web テクノロジーを使用してシームレスなエクスペリエンスを構築するための最も効果的なパターンと広く見なされている重要な塊に達しました。 SPA パターンに従うと、デスクトップアプリケーションやモバイルアプリケーションと同じように機能しながら、オープン web 標準を基盤とするために多数のデバイスプラットフォームやフォームファクターに対応するアプリケーションを作成できます。

一般に、SPAは従来のページベースの web サイトよりもパフォーマンスが高く表示されます。これは、通常、完全なHTMLページ **CSS、JS、サポートフォントコンテンツを含む** を読み込み、アプリでステートの変化が発生するたびに必要なもののみを読み込むためです。 このステートの変化に必要な処理は、選択したテクノロジーによって異なりますが、通常は、既存の「ビュー」を置き換える 1 つのHTMLフラグメントと、新しいビューをワイヤリングし、必要に応じてクライアント側でテンプレートレンダリングを実行する JS コードのブロックの実行が含まれます。 このステートの変化の速度は、テンプレートキャッシングのメカニズムをサポートすることで、またはAdobe PhoneGapを使用する場合はテンプレートコンテンツへのオフラインアクセスをサポートすることで、さらに向上させることができます。

AEM 6.1 は、AEM アプリを介したSPAの構築と管理をサポートしています。 この記事では、SPAの背後にある概念と、その概念が [AngularJS](https://angularjs.org/) を使用してブランドをApp StoreやGoogle Playに導入する方法を紹介します。

## AEM アプリでのSPA {#spa-in-aem-apps}

AEM Apps のシングルページアプリケーションフレームワークにより、AngularJS アプリの高パフォーマンスが可能になると同時に、作成者（またはその他の技術者以外の担当者）が、従来 web サイトの管理に予約されていたタッチ操作向けのドラッグ&amp;ドロップエディター環境を使用して、アプリのコンテンツを作成および管理できるようになります。 既にAEMでサイトを構築していますか？ AEM アプリを使用すると、コンテンツ、コンポーネント、ワークフロー、アセット、権限を簡単に再利用できます。

## AngularJS アプリケーションモジュール {#angularjs-application-module}

AEM アプリケーションは、アプリの最上位モジュールをまとめるなど、AngularJS 設定の多くを処理します。 デフォルトでは、このモジュールの名前は「AEMAngularApp」で、このモジュールを生成するスクリプトは/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp にあります（オーバーレイされます）。

アプリの初期化の一部には、アプリが依存する AngularJS モジュールを指定することが含まれます。 アプリで使用されるモジュールのリストは、/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp にあるスクリプトで指定され、独自のアプリのページコンポーネントでオーバーレイして、アプリで必要な追加の AngularJS モジュールを取り込むことができます。 例として、上記のスクリプトをGeometrixx実装（/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp にあります）と比較してください。

アプリ内の異なるステート間のangularをサポートするために、Path-app-module スクリプトは、最上位のアプリページのすべての下位ページを反復処理して「routes」のセットを生成し、Angularの$routeProvider サービスで各パスを設定します。 これが実際にどのように見えるかの例については、Geometrixx Outdoorsアプリのサンプルによって生成されたangularアプリモジュールスクリプトを参照してください：（リンクにはローカルインスタンスが必要です） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

生成された AEMAngularApp を調べると、次のように指定された一連のルートが見つかります。

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上記のサンプルは、特に、パスの一部としてパラメーターを渡す例を示しています。 この例では、指定されたパターン（/content/phonegap/geometrixx-outdoors/en/home/products/:id）を満たすパスが要求された際に、そのパスがhome/products.template.html テンプレートによって処理され、「contentphonegapgeometrixoutdoorsenhomeproducts」コントローラーを使用する必要があることを示しています。

このルートが要求されたときに読み込むテンプレートは、templateUrl プロパティで指定します。 このテンプレートには、ページに含まれているAEM コンポーネントからのHTMLと、アプリケーションのクライアント側をワイヤリングするために必要な AngularJS 指令が含まれています。 Geometrixxコンポーネントの AngularJS ディレクティブの例については、スワイプカルーセルの template.jsp （/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp）の 45 行目を確認してください。

## ページコントローラー {#page-controllers}

angular自身の言葉では、「Controller は、Angularスコープを拡張するために使用されるJavaScript コンストラクター関数です。」 （[source](https://docs.angularjs.org/guide/controller)）AEM アプリの各ページは、`angular` ータの `frameworkType` を指定する任意のコントローラーによって拡張できるコントローラーに自動的にワイヤリングされます。 ng-text コンポーネントを例として見てみましょう（/libs/mobileapps/components/component/ng-text）。cq:template angularを含めているので、このコンポーネントがページに追加されるたびに、この重要なプロパティが含まれるようにします。

より複雑なangularの例については、ng-template-page controller.jsp スクリプト（/apps/geometrixx-outdoors-app/components/controller/ng-template-page）を開きます。 特に興味深いのは、の実行時に生成されるJavaScript コードです。このコードは、次のようにレンダリングされます。

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

上記の例では、`$routeParams` サービスのパラメーターが取得され、JSON データが格納されているディレクトリ構造にマッサージされます。 この方法で SKU `id` を処理することで、単一の製品テンプレートを配信でき、何千もの異なる製品の可能性がある製品データをレンダリングできます。 これは、（潜在的に）大規模な製品データベース内の各項目に対して個別のルートを必要とする、はるかにスケーラブルなモデルです。

また、2 つのコンポーネントが現在動作しています。ng-product は、上記の `$http` 呼び出しから抽出したデータで範囲を拡張します。 また、このページには ng 画像があり、応答から取得した値で範囲を拡張します。 angularの `$http` サービスにより、各コンポーネントは、リクエストが完了し、作成した promise が満たされるまで辛抱強く待ちます。

## 次の手順 {#the-next-steps}

シングルページアプリケーションの詳細については、「[PhoneGap CLI を使用したアプリの開発 ](/help/mobile/phonegap-apps-pg-cli.md) を参照してください。
