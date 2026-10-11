---
title: 単一ページアプリケーション
description: このページでは、シングルページアプリケーションについて説明します。つまり、デスクトップまたはモバイルアプリケーションと同じように動作するアプリケーションを作成できます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%
---
# 単一ページアプリケーション{#single-page-applications}

{{ue-over-mobile}}

[&#x200B; シングルページアプリケーション &#x200B;](https://en.wikipedia.org/wiki/Single-page_application) （SPA）はクリティカルマスに達しており、web テクノロジーでシームレスなエクスペリエンスを構築するための最も効果的なパターンとして広く認められています。 SPA パターンに従うことで、デスクトップまたはモバイルアプリケーションと同じように動作するアプリケーションを作成できますが、オープン web標準の基盤により、多数のデバイスプラットフォームやフォームファクターにリーチできます。

一般的に、SPAは従来のページベースのweb サイトよりもパフォーマンスが高く表示されます。通常は、HTMLのページ **を1回だけ読み込み（CSS、JS、およびサポートするフォントコンテンツを含む）、アプリで状態の変更が発生するたびに必要なページのみを読み込むからです。**&#x200B;この状態の変化に必要なものは、選択したテクノロジーセットによって異なりますが、通常は、既存の「ビュー」を置き換える1つのHTML フラグメントと、新しいビューを接続し、必要に応じてクライアントサイドのテンプレートレンダリングを実行するJS コードのブロックが含まれます。 この状態の変更の速度は、テンプレートキャッシュのメカニズムをサポートすることによってさらに向上できます。また、Adobe PhoneGapを使用している場合は、テンプレートコンテンツへのオフラインアクセスも可能になります。

AEM 6.1は、AEM Appsを介したSPAの構築と管理をサポートしています。 この記事では、SPAの背後にある概念と、それらが[AngularJS](https://angularjs.org/)を使用してブランドをApp StoreとGoogle Playに取り込む方法について説明します。

## AEM アプリのSPA {#spa-in-aem-apps}

AEM Appsのシングルページアプリケーションフレームワークは、AngularJS アプリの高いパフォーマンスを実現すると同時に、従来はweb サイトの管理のために予約されていた、タッチ操作向けのドラッグ&amp;ドロップ操作のエディター環境を使用して、制作者（またはその他の技術者）がアプリのコンテンツを作成および管理できるようにします。 AEMでサイトを構築したことがありますか？ AEMを利用すれば、コンテンツ、コンポーネント、ワークフロー、アセット、権限を容易に再利用できます。

## AngularJS アプリケーションモジュール {#angularjs-application-module}

AEM Appsは、アプリのトップレベルモジュールの作成など、AngularJSの設定の多くを処理します。 デフォルトでは、このモジュールの名前は「AEMAngularApp」で、その生成を担当するスクリプトは/libs/mobileapps/components/angular/ng-page/angular-app-module.js.jspにあります（およびオーバーレイされています）。

アプリの初期化の一環として、アプリが依存するAngularJS モジュールを指定する必要があります。 アプリで使用されるモジュールのリストは、/libs/mobileapps/components/angular/ng-page/angular-module-list.js.jspにあるスクリプトによって指定され、アプリに必要な追加のAngularJS モジュールを取り込むために、独自のアプリのページコンポーネントでオーバーレイできます。 例として、上記のスクリプトとGeometrixxの実装（/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jspにある）を比較します。

アプリ内の異なるステート間のナビゲーションをサポートするために、angular-app-module スクリプトは、トップレベルのアプリページのすべての下位ページを反復処理して「ルート」のセットを生成し、Angularの$routeProvider サービスで各パスを設定します。 これが実際にどのように見えるか例として、Geometrixx Outdoors アプリのサンプルで生成されたangular-app-module スクリプトを見てみましょう。（リンクにはローカルインスタンスが必要です） [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

生成されたAEMAngularAppを掘り下げると、次のように指定された一連のルートが見つかります。

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

特に上記のサンプルは、パスの一部としてパラメーターを渡す例を示しています。 この例では、指定されたパターン（/content/phonegap/geometrixx-outdoors/en/home/products/:id）を満たすパスが要求された場合は、home/products.template.html テンプレートで処理し、「contentphonegapgeometrixxoutdoorsenhomeproducts」コントローラを使用する必要があることを示しています。

このルートが要求されたときに読み込むテンプレートは、templateUrl プロパティで指定します。 このテンプレートには、ページに含まれているAEMのHTML コンポーネントと、アプリケーションのクライアントサイドをワイヤリングするために必要なAngularJS ディレクティブが含まれています。 Geometrixx コンポーネントのAngularJS ディレクティブの例については、スワイプカルーセルのtemplate.jsp （/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp）の45行目を参照してください。

## ページコントローラー {#page-controllers}

Angular自身の言葉では、「Controllerは、Angular Scopeを拡張するために使用されるJavaScript コンストラクタ関数です。」 （[source](https://docs.angularjs.org/guide/controller)） AEM アプリの各ページは、自動的に`angular`の`frameworkType`を指定する任意のコントローラーで強化できるコントローラーに接続されます。 ng-text コンポーネントを例（/libs/mobileapps/components/angular/ng-text）として見てください。このコンポーネントがページに追加されるたびに、この重要なプロパティが含まれていることを確認するcq:template ノードを含みます。

より複雑なコントローラの例では、ng-template-page controller.jsp スクリプト（/apps/geometrixx-outdoors-app/components/angular/ng-template-page）を開きます。 特に興味深いのは、実行時に生成されるJavaScript コードで、次のようにレンダリングされます。

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

上記の例では、`$routeParams` サービスのパラメーターが取得され、JSON データが格納されるディレクトリ構造にマッピングされます。 この方法でSKU `id`を処理すると、潜在的に何千もの異なる製品の製品データをレンダリングできる単一の製品テンプレートを配信できます。 これは、（潜在的に）大規模な製品データベースの各項目に対して個別のルートを必要とする、はるかにスケーラブルなモデルです。

ここには2つのコンポーネントもあります。ng-productは、上記の`$http`呼び出しから抽出したデータでスコープを拡張します。 また、このページにはng-imageがあり、その結果、応答から取得した値でスコープが補強されます。 Angularの`$http` サービスを利用することで、各コンポーネントは、リクエストが完了し、作成されたプロミスが満たされるまで辛抱強く待ちます。

## 次の手順 {#the-next-steps}

シングルページアプリケーションについて理解できたら、[PhoneGap CLIを使用したアプリケーションの開発](/help/mobile/phonegap-apps-pg-cli.md)を参照してください。
