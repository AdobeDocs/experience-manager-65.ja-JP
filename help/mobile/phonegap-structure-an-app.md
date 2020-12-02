---
title: アプリの構造
seo-title: アプリの構造
description: このページでは、アプリの構造の作成方法について説明します。このページでは、テンプレートやコンポーネントを構造化する方法と、JavaScript および CSS のクライアントライブラリについて説明します。
seo-description: このページでは、アプリの構造の作成方法について説明します。このページでは、テンプレートやコンポーネントを構造化する方法と、JavaScript および CSS のクライアントライブラリについて説明します。
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 62%

---


# アプリの構造{#structure-an-app}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM Mobile プロジェクトには、ページ、JavaScript と CSS のクライアントライブラリ、再利用可能な AEM コンポーネント、コンテンツ同期設定、PhoneGap アプリシェルコンテンツなど、多様なコンテンツタイプセットが含まれます。新しいAEM Mobileアプリを[スターターキット](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)に基づいて作成すると、様々なタイプのコンテンツをアドビの推奨構造に入手し、携帯性と保守性を長期にわたって容易にするのに便利です。

## ページコンテンツ {#page-content}

アプリケーションのページが AEM Mobile コンソールで認識されるには、そのすべてのページが /content/mobileapps の下に配置されている必要があります。

![chlimage_1-52](assets/chlimage_1-52.png)

AEM の慣例により、アプリの最初のページは、アプリのデフォルト言語（Geometrixx とスターターキットのどちらの場合でも「en」）として機能するいずれかの子ページへのリダイレクトである必要があります。トップレベルのロケールページは通常、Over-the-air Content Syncアップデートのインストールをサポートするために必要な初期化を行う基礎となる「splash-page」コンポーネント(/libs/mobileapps/components/splash-page)から継承します(contentInitコードは/etc/clientlibs/mobile/content-sync/js/contentInit.jsにあります)。

## テンプレートおよびコンポーネント {#templates-and-components}

アプリのテンプレートおよびコンポーネントのコードは、/apps/&lt;ブランド名>/&lt;アプリ名> にあります。規則に従って、テンプレートとコンポーネントコードは/apps/&lt;brand name>/&lt;app name>に配置する必要があります。 このパターンは、AEM のサイトでの作業経験がある開発者にはよく知られています。このパターンに従うのは通常、パブリッシュインスタンスでは /apps/ への匿名アクセスがデフォルトでロックされるからです。その結果、生の JSP コードが潜在的な攻撃者に対して非表示になります。

アプリ固有のテンプレートは、テンプレート自体の`allowedPaths`プロパティノードを使用し、その値を&#39;/content/mobileapps(/.&amp;ast;?&#39; に設定することです。テンプレートを単一のアプリでのみ使用する場合には、さらに具体的な値に設定することもできます。また、`allowedParents`プロパティと`allowedChildren`プロパティを使用して、新しいページの作成場所に基づいて、作成者がどのテンプレートを使用できるかをきめ細かく制御することもできます。

新しいアプリページコンポーネントを最初から作成する場合は、`sling:resourceSuperType`プロパティを&#39;mobileapps/components/angular/ng-page&#39;に設定することをお勧めします。 これにより、シングルページアプリとして作成したりレンダリングしたりできるようにページが設定され、コンポーネントで .jsp ファイルを変更する必要がある場合にはそのファイルをオーバーレイできます。ng-page には UI フレームワークが一切含まれないので、開発者は通常最終的には（少なくとも）「template.jsp」（/libs/mobileapps/components/angular/ng-page/template.jsp からオーバーレイされたもの）をオーバーレイすることになります。

AngularJSを利用したい場合、承認可能なページコンポーネントは、同じ方法でオーバーレイおよびカスタマイズできる、同等の`sling:resourceSuperType`コンポーネントを/libs/mobileapps/components/angular/ng-componentに配置します。

## JavaScript およびCSS Clientlibs {#javascript-and-css-clientlibs}

クライアントライブラリに関して、開発者は、リポジトリ内のどこに配置するかについてのオプションがいくつかあります。次のパターンはガイダンスとして示したものであり、固定の要件ではありません。

clientside コードが単独で機能でき、アプリケーションの特定のコンポーネントに関連していない（つまり、他のアプリケーションで再利用できる）場合には、/etc/clientlibs/&lt;ブランド名>/&lt;ライブラリ名> に格納することをお勧めします。一方、clientlib が単一のアプリに固有のものである場合には、アプリのデザインノードの子としてネストできます（/etc/designs/phonegap/&lt;ブランド名>/&lt;アプリ名>/clientlibs）。この clientlib のカテゴリは、他のライブラリで使用しないでください。必要に応じて他のライブラリを埋め込むために使用してください。このパターンに従うと、開発者はクライアントライブラリをアプリに追加するたびに新規コンテンツ同期設定を追加する必要がなくなり、単にアプリの design clientlib の embeds プロパティを更新するだけでよくなります。例えば、/content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-allのGeometrixxclientlibs-allコンテンツ同期設定ノードを見てみましょう。

クライアント側コードが特定のコンポーネントに密接に結合されている場合は、そのコードを /apps/ 内のコンポーネントの場所の下にネストされたクライアントライブラリに配置し、そのカテゴリをアプリの「design」clientlib に埋め込みます。

## PhoneGap 設定  {#phonegap-configuration}

各AEM Mobileアプリには、PhoneGap [コマンドラインインターフェイス](https://github.com/phonegap/phonegap-cli)と[PhoneGap build](https://build.phonegap.com/)で使用される設定ファイルをホストするディレクトリが含まれ、Webコンテンツを実行可能なアプリケーションに変換します。 例えば、Geometrixx のサンプルでは、このディレクトリ（/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content）はシェルの一部として存在しますが、このようなデザイン上の決定となったのは、無線で更新できないコンテンツ（デバイス API やアプリ自体の設定を処理するプラグインなど）のみが含まれているからです。

このディレクトリには、プラグインのインストール、プラットフォーム固有の場所へのリソースファイルの配置、ビルドの一環として実行する必要のある他のアクションに使用できる[Cordovaフック](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide)も多数あります。 注意：ビルドの一部として各プラグインをダウンロードする代わりに、Kitchen Sinkアプリと[include plugin source code](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins)のパターンに従って、残りのアプリプロジェクトを実行できます。

## 次の手順 {#the-next-steps}

アプリの構造について詳しくは、[アプリコンソールを使用したアプリの作成と編集](/help/mobile/phonegap-apps-console.md)を参照してください。
