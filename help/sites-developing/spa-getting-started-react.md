---
title: AEMのSPA使用の手引き — React
seo-title: AEMのSPA使用の手引き — React
description: この記事では、サンプルのSPAアプリケーションを紹介し、その組み合わせ方法を説明します。また、Reactフレームワークを使用して、独自のSPAを迅速に使用して運用を開始できます。
seo-description: この記事では、サンプルのSPAアプリケーションを紹介し、その組み合わせ方法を説明します。また、Reactフレームワークを使用して、独自のSPAを迅速に使用して運用を開始できます。
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Getting Started with SPAs in AEM - React{#getting-started-with-spas-in-aem-react}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、Reactフレームワーク上のシンプル化されたSPAアプリケーションを紹介し、その組み合わせ方法を説明します。これにより、お客様自身のSPAを迅速に使用できるようになります。

>[!NOTE]
>
>この記事はReactフレームワークに基づいています。 Angularフレームワークの対応するドキュメントについては、「AEM - Angular [でのSPAの使用の手引き」を参照してください](/help/sites-developing/spa-getting-started-angular.md)。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

この記事では、シンプルな SPA の基本的な機能と、SPA を運用するための最低条件の概要を説明します。

AEMでのSPAの動作について詳しくは、次のドキュメントを参照してください。

* [SPAの概要とチュートリアル](/help/sites-developing/spa-walkthrough.md)
* [SPA オーサリングの概要](/help/sites-developing/spa-overview.md)
* [SPA ブループリント](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 内のコンテンツを作成するには、コンテンツを AEM に格納し、コンテンツモデルによって公開する必要があります。
>
>AEM 以外で開発された SPA については、コンテンツモデルのコントラクトに準拠していない場合、オーサリングをおこなうことはできません。

本書では、Reactフレームワークを使用して作成したシンプル化されたSPAの構造を紹介し、その仕組みを説明して、この理解を独自のSPAに適用します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルの SPA では、必要な React の依存関係以外に、追加のライブラリも利用して SPA の作成を効率化できます。

### 依存関係 {#dependencies}

このファ `package.json` イルは、SPAパッケージ全体の要件を定義します。 作業中のSPAに対するAEMの最小依存関係を以下に示します。

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

このサンプルは React フレームワークに基づいているので、`package.json` ファイルには必須となる React 固有の依存関係が 2 つあります。

```
react
 react-dom
```

The `aem-clientlib-generator` is leveraged to make the creation of client libraries automatic as part of the build process.

`"aem-clientlib-generator": "^1.4.1",`

詳しくは、[GitHub のこちらのページ](https://github.com/wcm-io-frontend/aem-clientlib-generator)を参照してください。

>[!CAUTION]
>
>必要なバージョンの `aem-clientlib-generator` 最小バージョンは1.4.1です。

The `aem-clientlib-generator` is configured in the `clientlib.config.js` file as follows.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### ビルド {#building}

アプリの実際のビルドでは、クライアントライブラリの自動作成用の aem-clientlib-generator 以外に、トランスパイル用に [Webpack](https://webpack.js.org/) も利用します。そのため、build コマンドは以下のようになります。

`"build": "webpack && clientlib --verbose"`

ビルドが完了したら、パッケージを AEM インスタンスにアップロードできます。

### SPAスターターキット用Mavenアーキタイプ {#maven-archetype-for-spa-starter-kit}

AEM用の独自のSPAプロジェクトを開始する際に役立つよう [](https://github.com/adobe/aem-spa-project-archetype) に、SPAスターターキット用のMavenアーキタイプの活用をお勧めします。

## アプリケーション構造 {#application-structure}

前述のように依存関係を含め、アプリを作成すると、AEMインスタンスにアップロードできる有効なSPAパッケージが提供されます。

このドキュメントの次のセクションでは、AEMのSPAの構造、アプリケーションを駆動する重要なファイル、および連携する方法について説明します。

シンプル化された画像コンポーネントを例として使用しますが、アプリケーションのすべてのコンポーネントは同じ概念に基づいています。

### index.js {#index-js}

SPA のエントリポイントはもちろん `index.js` ファイルです。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

`index.js` の主要機能は、`ReactDOM.render` 関数を使用して、DOM 内でアプリケーションをインジェクトする場所を決めることです。

これは、この関数の標準的な使用方法であり、この例のアプリに固有のものではありません。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレート（JSXなど）を使用して静的にコンポーネントをインスタンス化する場合、モデルからコンポーネントのプロパティに値を渡す必要があります。

### App.js {#app-js}

アプリをレンダリングすることで、`index.js` は `App.js` を呼び出します。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` の主な役目は、アプリを構成するルートコンポーネントをラップすることです。アプリのエントリポイントはページです。

### Page.js {#page-js}

ページをレンダリングすると、簡単なバ `App.js` ージョ `Page.js` ンでここに示す呼び出しが表示されます。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

In this example the `AppPage` class extends `Page`, which contains the inner-content methods that can then be used.

`Page` は、ページモデルの JSON 表現を取り込み、コンテンツを処理してページの各要素をラップ／デコレートします。`Page` のその他の詳細については、[SPA ブループリント](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)のドキュメントを参照してください。

### Image.js {#image-js}

ページがレンダリングされると、以下の `Image.js` などのコンポーネントがレンダリング可能になります。

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。See the document [SPA Editor Overview](/help/sites-developing/spa-overview.md) for an summary of this communication model.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

`MapTo` メソッドは、SPA コンポーネントを AEM コンポーネントにマッピングします。単一の文字列または文字列の配列の使用に対応しています。

`ImageEditConfig` は、エディターがプレースホルダーを生成するために必要なメタデータを提供することで、コンポーネントのオーサリング機能の有効化に関与する設定オブジェクトです。

コンテンツがない場合は、空のコンテンツを表すラベルがプレースホルダーとして提供されます。

#### 動的に渡されるプロパティ {#dynamically-passed-properties}

モデルからのデータは、コンポーネントのプロパティとして動的に渡されます。

## 編集可能コンテンツの書き出し {#exporting-editable-content}

コンポーネントをエクスポートして編集可能な状態を維持することができます。

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

The `MapTo` function returns a `Component` which is the result of a composition that extends the provided `PageClass` with the class names and attributes that enable the authoring. このコンポーネントは後でエクスポートし、アプリケーションのマークアップでインスタンス化できます。

When exported using the `MapTo` or `withModel` functions, the `Page` component, is wrapped with a `ModelProvider` component which provides standard components access to the latest version of the page model or a precise location in that page model.

詳しくは、[SPA ブループリントのドキュメント](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)を参照してください。

>[!NOTE]
>
>デフォルトでは、`withModel` 関数を使用するとコンポーネントのモデル全体を受け取ります。

## SPAコンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有する場合は、定期的に必要です。 これを行う場合は、次に示すように、複雑さの増加順に示すいくつかの推奨方法があります。

* **** オプション1:例えば、React Contextを使用して、ロジックを一元管理し、必要なコンポーネントにブロードキャストします。
* **** オプション2:Reduxなどのステートライブラリを使用して、コンポーネントの状態を共有します。
* **** オプション3:コンテナコンポーネントをカスタマイズして拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

独自のSPAを作成する手順ガイドについては、『AEM SPA Editor - WKND Events Tutorial [Getting Started with the AEM SPA Editor - WKND Events Tutorial』を参照してください](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

AEM用のSPAを開発するための組織化の詳細については、「AEM用のSPAの開発」の記事 [を参照してください](/help/sites-developing/spa-architecture.md)。

動的モデルとコンポーネントのマッピング、およびAEMのSPA内での動的モデルとコンポーネントのマッピングについて詳しくは、SPAの動的モデルとコンポ [ーネントのマッピングを参照してください](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

AEMにReactやAngular以外のフレームワーク用のSPAを実装する場合や、単にAEM用SPA SDKの仕組みを詳しく調べたい場合は、 [SPA Blueprintの記事を参照してください](/help/sites-developing/spa-blueprint.md) 。
