---
title: 単一ページアプリケーション
description: このページでは、デスクトップまたはモバイルアプリケーションと同様に動作するアプリケーションを作成できる、単一ページアプリケーションについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 1%

---

# 単一ページアプリケーション{#single-page-applications}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

[シングルページアプリケーション](https://en.wikipedia.org/wiki/Single-page_application) (SPA) は、Web テクノロジーとのシームレスなエクスペリエンスを構築するための最も効果的なパターンと広く見なされ、重要な質量に達しています。 SPAのパターンに従うことで、デスクトップまたはモバイルアプリケーションと同じ動作を行うが、オープン Web 標準での基盤により、多数のデバイスプラットフォームやフォームファクタに達するアプリケーションを作成できます。

一般に、SPAは、通常、完全なHTMLページを読み込むので、従来のページベースの Web サイトよりもパフォーマンスが高く表示されます **1 回のみ** （CSS、JS、サポートフォントコンテンツを含む）を追加し、アプリで状態の変更が発生するたびに必要な内容のみを読み込みます。 この状態の変更に必要なものは、選択したHTMLのセットに応じて異なりますが、通常は、既存の「ビュー」に代わる単一のテクノロジーフラグメントと、新しいビューを結び付けて必要なクライアント側のテンプレートレンダリングを実行する JS コードのブロックの実行です。 この状態の変更は、テンプレートのキャッシュメカニズムをサポートすることで、さらに速くできます。また、Adobe PhoneGapを使用している場合は、テンプレートコンテンツへのオフラインアクセスもサポートします。

AEM 6.1 は、AEM Apps を介したSPAの構築と管理をサポートします。 この記事では、SPAの背後にある概念と、その使用方法について説明します [AngularJS](https://angularjs.org/) ブランドをApp StoreとGoogle Playに移動します。

## SPA in AEM Apps {#spa-in-aem-apps}

AEM Apps の単一ページアプリケーションフレームワークを使用すると、AngularJS アプリの高パフォーマンスを実現すると同時に、従来 Web サイト管理用に予約されていたタッチ操作向けのドラッグ&amp;ドロップエディター環境を使用して、作成者（または非技術者）がアプリのコンテンツを作成および管理できます。 AEMで作成したサイトは既にありますか？ AEM Apps では、コンテンツ、コンポーネント、ワークフロー、アセットおよび権限を簡単に再利用できます。

## AngularJS アプリケーションモジュール {#angularjs-application-module}

AEM Apps では、アプリのトップレベルモジュールを組み立てるなど、AngularJS の設定の多くをお客様が処理します。 デフォルトでは、このモジュールの名前は「AEMngularApp」で、その生成を担当するスクリプトは/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp で見つかります（また、オーバーレイされます）。

アプリの初期化の一部として、アプリが依存する AngularJS モジュールを指定する必要があります。 アプリが使用するモジュールのリストは、/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp にあるスクリプトで指定されます。また、アプリが必要とする追加の AngularJS モジュールを取り込むために、独自のアプリのページコンポーネントでオーバーレイできます。 例えば、上記のスクリプトをGeometrixx実装 (/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp にある ) と比較します。

アプリ内の個別の状態間のナビゲーションをサポートするために、angular-app-module スクリプトは、トップレベルのアプリページのすべての下位ページを反復して「routes」のセットを生成し、Angularの$routeProvider サービスの各パスを設定します。 この動作の実際の例については、Geometrixx Outdoorsアプリのサンプルで生成されたangular-app-module スクリプトを参照してください。（リンクにはローカルインスタンスが必要です） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

生成された AEMngularApp を掘り下げると、次のように指定された一連のルートが見つかります。

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

上記のサンプルは、パスの一部としてパラメーターを渡す例を示しています。 この例では、指定されたパターン (/content/phonegap/geometrixx-outdoors/en/home/products/:id) を満たすパスが要求された場合、home/products.template.html テンプレートで処理され、「contentphonegapgeometrixxoutdoorsenhomeproducts」コントローラーを使用する必要があることを示しています。

このルートが要求されたときに読み込むテンプレートは、 templateUrl プロパティで指定されます。 このテンプレートには、ページに含まれるAEMコンポーネントからのHTMLと、アプリケーションのクライアント側の配線に必要な AngularJS ディレクティブが含まれます。 Geometrixxコンポーネント内の AngularJS ディレクティブの例については、swipe-carousel の template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp) の 45 行目を参照してください。

## ページコントローラ {#page-controllers}

angular独自の言い方では、「コントローラは、Angular範囲を拡張するために使用される JavaScript コンストラクタ関数です」。 ([ソース](https://docs.angularjs.org/guide/controller)) AEM App 内の各ページは、 `frameworkType` / `angular`. 例として ng-text コンポーネント (/libs/mobileapps/components/template/ng-text) を見てみましょう。cq:templateangularは、このコンポーネントがページに追加されるたびに、この重要なプロパティを含むようにします。

より複雑なコントローラの例については、 ng-template-page controller.jsp スクリプトを開きます (/apps/geometrixx-outdoors-app/components/template/ng-template-page)。 特に重要なのは、実行時に生成される JavaScript コードです。このコードは次のようにレンダリングされます。

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

上記の例では、 `$routeParams` サービスが取得され、JSON データが格納されるディレクトリ構造にマッサージされます。 SKU を扱う `id` この方法で、潜在的に数千の個別の製品の製品データをレンダリングできる、単一の製品テンプレートを配信できます。 これは、（潜在的に）大規模な製品データベース内の各項目の個々のルートを必要とする、はるかにスケーラブルなモデルです。

また、ここでは 2 つのコンポーネントが動作します。ng-product は、上記から抽出したデータで範囲を増補します。 `$http` 呼び出し。 また、このページには ng-image があり、これにより、応答から取得した値でスコープが増補されます。 angularの `$http` サービスの場合、各コンポーネントは、リクエストが完了し、作成されたプロミスが満たされるまで待機します。

## 次の手順 {#the-next-steps}

シングルページアプリケーションについて学習したら、 [PhoneGap CLI を使用したアプリの開発](/help/mobile/phonegap-apps-pg-cli.md).
