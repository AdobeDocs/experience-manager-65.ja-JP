---
title: アプリの構造
description: このページでは、アプリの構造を作成する方法について説明します。 このページでは、テンプレートとコンポーネントを構造化する方法と、JavaScript および CSS Clientlib に関する情報について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# アプリの構造{#structure-an-app}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobileプロジェクトには、ページ、JavaScript および CSS クライアントライブラリ、再利用可能なAEMコンポーネント、コンテンツ同期設定、PhoneGap アプリシェルコンテンツなど、様々なコンテンツタイプのセットが含まれます。 次を基に新しいAEM Mobileアプリを作成する [スターターキット](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) は、すべての異なるタイプのコンテンツを推奨される構造に取り込み、長期的な移植性と保守性の両方を容易にする良い方法です。

## ページコンテンツ {#page-content}

アプリケーションのページがAEM Mobileコンソールで認識されるように、すべてのページが/content/mobileapps の下に配置されている必要があります。

![chlimage_1-52](assets/chlimage_1-52.png)

AEMの慣例により、アプリの最初のページは、アプリのデフォルト言語 (Geometrixxとスターターキットの両方のケースでは「en」) となる、アプリの子の 1 つへのリダイレクトにする必要があります。 トップレベルのロケールページは、通常、基盤の「splash-page」コンポーネント (/libs/mobileapps/components/splash-page) を継承します。このコンポーネントは、空中コンテンツ同期更新のインストールに必要な初期化を処理します (contentInit コードは/etc/clientlibs/mobile/content-sync/js/contentInit.jsにあります )。

## テンプレートとコンポーネント {#templates-and-components}

アプリのテンプレートとコンポーネントコードは、/apps/にある必要があります。&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. 慣例に従い、テンプレートとコンポーネントのコードは/apps/に配置する必要があります。&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>. このパターンは、AEMで Site を既に使用している開発者にとってよく知っている必要があります。 通常は、パブリッシュインスタンスで/apps/がデフォルトで匿名アクセスにロックされるので、これに従います。 したがって、生の JSP コードは潜在的な攻撃者から隠されます。

アプリ固有のテンプレートは、 `allowedPaths` プロパティノードを作成し、その値を&#39;/content/mobileapps(/.&amp;ast;)?&#39;  — またはテンプレートを単一のアプリに対してのみ使用できるようにする場合は、より具体的なもの。 The `allowedParents` および `allowedChildren` プロパティは、新しいページの作成場所に基づいて、作成者が使用できるテンプレートを詳細に制御する場合にも使用できます。

アプリページコンポーネントを最初から作成する場合は、新しく作成したコンポーネントに `sling:resourceSuperType` プロパティを「mobileapps/components/angular/ng-page」に設定します。 これにより、オーサリング用とレンダリング用のページが単一ページアプリとして設定され、コンポーネントで変更が必要な.jsp ファイルをオーバーレイできます。 ng-page には UI フレームワークがまったく含まれていないので、デベロッパーは通常、(/libs/mobileapps/components/angular/ng-page/template.jspからオーバーレイされた )「template.jsp」（少なくとも）をオーバーレイすることになります。

AngularJS を使用したいオーサリング可能なページコンポーネントには、同等の機能があります。 `sling:resourceSuperType` /libs/mobileapps/components/components/angular/ng-component のコンポーネント。同じ方法でオーバーレイおよびカスタマイズできます。

## JavaScript と CSS の clientlibs {#javascript-and-css-clientlibs}

クライアントライブラリには、開発者がリポジトリ内のどこに配置するかを選択できるオプションがいくつかあります。 次のパターンはガイダンス用に提供されていますが、難しい要件ではありません。

お使いのクライアントサイドコードが独立していて、アプリケーションの特定のコンポーネントに関連していない場合（つまり他のアプリケーションで再利用できる場合）は、Adobeは/etc/clientlibs/に保存することをお勧めします。&lt;brand name=&quot;&quot;>/&lt;lib name=&quot;&quot;>. 一方、clientlib が単一のアプリに固有の場合は、アプリのデザインノード (/etc/designs/phonegap/) の子としてネストできます。&lt;brand name=&quot;&quot;>/&lt;app name=&quot;&quot;>/clientlibs. この clientlib のカテゴリを他のライブラリと共に使用しないでください。代わりに、必要に応じて他のライブラリを埋め込みます。 このパターンに従うと、開発者はクライアントライブラリをアプリに追加するたびに新しいコンテンツ同期設定を追加する必要がなくなり、アプリのデザイン clientlib の「embeds」プロパティを更新するだけで済みます。 例えば、/content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all のGeometrixxclientlibs-all コンテンツ同期設定ノードを確認します。

クライアントサイドコードが特定のコンポーネントに緊密に結び付いている場合は、そのコードを/apps/内のコンポーネントの場所の下にネストされたクライアントライブラリに配置し、そのカテゴリをアプリの「デザイン」clientlib に埋め込みます。

## PhoneGap 設定 {#phonegap-configuration}

各AEM Mobileアプリには、PhoneGap で使用される設定ファイルをホストするディレクトリが含まれています [コマンドラインインターフェイス](https://github.com/phonegap/phonegap-cli) および PhoneGap Build は `https://build.phonegap.com/` web コンテンツを実行可能なアプリケーションに変換する場合。 例えば、このGeometrixxサンプルでは、このディレクトリ (/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content) は Shell の一部として配置されます。これは、デバイス API を扱うプラグインやアプリ自体の設定など、大切に更新できないコンテンツのみが含まれるためです。

このディレクトリには、 [Cordova フック](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) プラグインのインストールに使用できる、リソースファイルをプラットフォーム固有の場所に配置し、ビルドの一部として実行する必要があるその他のアクションを配置できます。 注意：ビルドの一部として各プラグインをダウンロードする代わりに、Kitchen Sink アプリのパターンに従って、プラグインのソースコードを含めることができます<!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> 残りのアプリプロジェクトと共に使用できます。

## 次の手順 {#the-next-steps}

アプリの構造について詳しくは、 [アプリコンソールを使用したアプリの作成と編集](/help/mobile/phonegap-apps-console.md).
