---
title: アプリの構造
description: このページでは、アプリの構造を作成する方法について説明します。 ここでは、JavaScriptと CSS Clientlib に関する情報と共に、テンプレートとコンポーネントを構築する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 1%

---

# アプリの構造{#structure-an-app}

{{ue-over-mobile}}

AEM Mobile プロジェクトには、ページ、JavaScriptと CSS クライアントライブラリ、再利用可能なAEM コンポーネント、コンテンツ同期設定、PhoneGap アプリシェルコンテンツなど、様々なコンテンツタイプが含まれます。 新しいAEM Mobile アプリを [ スターターキット ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) に基づくと、あらゆる種類のコンテンツをお勧めの構造に取り込んで、長期にわたって移植性と保守性の両方を容易にすることができます。

## ページコンテンツ {#page-content}

AEM Mobile コンソールで認識されるようにするには、アプリケーションのページがすべて/content/mobileapps の下にある必要があります。

![chlimage_1-52](assets/chlimage_1-52.png)

AEMの慣例により、アプリの最初のページは、アプリのデフォルト言語として機能する子の 1 つにリダイレクトする必要があります（Geometrixxとスターターキットの両方の場合は「en」）。 最上位のロケールページは通常、基盤の「スプラッシュページ」コンポーネント （/libs/mobileapps/components/splash-page）から継承されます。このコンポーネントは、OTC コンテンツ同期アップデートのインストールをサポートするために必要な初期化を行います（contentInit コードは/etc/clientlibs/mobile/content-sync/js/contentInit.jsで入手できます）。

## テンプレートとコンポーネント {#templates-and-components}

アプリのテンプレートとコンポーネントコードは、/apps/&lt;brand name>/&lt;app name> 内にある必要があります。 規則に従って、テンプレートとコンポーネントコードは/apps/&lt;brand name>/&lt;app name> に配置する必要があります。 このパターンは、AEMのサイトを既に使用している開発者によく知られている必要があります。 通常、このアドレスに従います。パブリッシュインスタンスでは、デフォルトで/apps/が匿名アクセスに対してロックダウンされています。 そのため、生の JSP コードは、潜在的な攻撃者から隠されています。

アプリ固有のテンプレートは、テンプレート自体の `allowedPaths` プロパティノードを使用し、その値を「/content/mobileapps （/&amp;ast;）?&#39; - テンプレートを 1 つのアプリでのみ使用できるようにする場合は、より具体的なものを使用することもできます。 `allowedParents` プロパティと `allowedChildren` プロパティを使用すると、新しいページが作成される場所に基づいて、作成者が使用できるテンプレートを詳細に制御することもできます。

angular アプリページコンポーネントを新規に作成する場合は、`sling:resourceSuperType` プロパティを「mobileapps/components/mobile/ng-page」に設定することをお勧めします。 これにより、オーサリングとレンダリングの両方に対応するページが単一ページアプリとして設定され、コンポーネントの変更が必要になる可能性のある.jsp ファイルをオーバーレイできるようになります。 ng-page には UI フレームワークがまったく含まれていないので、開発者は通常、「template.jsp」（/libs/mobileapps/components/angular/ng-page/template.jspからオーバーレイ）をオーバーレイすることになります。

angular オーサリング可能なページコンポーネントは AngularJS を使用するものであり、/libs/mobileapps/components/authoring/ng-component に同等の `sling:resourceSuperType` コンポーネントがあります。このコンポーネントは、同じ方法でオーバーレイおよびカスタマイズできます。

## JavaScriptと CSS Clientlibs {#javascript-and-css-clientlibs}

クライアントライブラリには、リポジトリー内の配置場所に関する開発者が使用できるオプションがいくつかあります。 以下のパターンがガイダンスとして提供されていますが、これは難しい要件ではありません。

クライアントサイドコードが独立しており、アプリケーションの特定のコンポーネントに関連していない場合（つまり、他のアプリケーションで再利用できる場合）は、Adobeが/etc/clientlibs/&lt;brand name>/&lt;lib name> に格納することをお勧めします。 一方、clientlib が 1 つのアプリに固有の場合は、アプリのデザインノード（/etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs）の子としてネストできます。 この clientlib のカテゴリを他の libs と使用しないでください。代わりに、必要に応じて他の libs を埋め込みます。 このパターンに従うと、開発者は、アプリのデザイン clientlib の「embed」プロパティを更新するだけで、クライアントライブラリをアプリに追加するたびに新しいコンテンツ同期設定を追加する必要がなくなります。 例えば、/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all にあるGeometrixx clientlibs-all コンテンツ同期設定ノードを確認します。

クライアントサイドのコードが特定のコンポーネントに緊密に結び付けられている場合は、そのコードを、/apps/内のコンポーネントの場所の下にネストされたクライアントライブラリに配置し、そのカテゴリをアプリの「デザイン」 clientlib に埋め込みます。

## PhoneGap 設定 {#phonegap-configuration}

各AEM Mobile アプリケーションには、PhoneGap [ コマンドラインインターフェイス ](https://github.com/phonegap/phonegap-cli) および PhoneGap ビルドで使用される設定ファイルをホストし、Web コンテンツを実行可能なアプリケーションに変 `https://build.phonegap.com/` するディレクトリが含まれています。 例えば、Geometrixxサンプルでは、このディレクトリ（/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content）はシェルの一部として配置されています。これは、デバイス API やアプリ自体の設定を扱うプラグインなど、無線で更新できないコンテンツのみが含まれているために設計が決定されるためです。

このディレクトリには、[Cordova フック ](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) もあり、プラグインのインストール、プラットフォーム固有の場所へのリソースファイルの配置、ビルドの一部として実行されるその他のアクションに使用できます。 注：ビルドの一部として各プラグインをダウンロードする代わりに、Kitchen Sink アプリのパターンに従い、残りのアプリプロジェクトと共に <!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> プラグインのソースコードを含めることができます。

## 次の手順 {#the-next-steps}

アプリの構造については、[App Console を使用したアプリの作成と編集 ](/help/mobile/phonegap-apps-console.md) を参照してください。
