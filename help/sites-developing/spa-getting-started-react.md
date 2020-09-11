---
title: AEMでのSPAの使用の手引き — React
seo-title: AEMでのSPAの使用の手引き — React
description: この記事では、サンプルのSPAアプリケーションを紹介し、SPAの組み合わせ方法を説明し、Reactフレームワークを使用して独自のSPAを使用して迅速に運用を開始できます。
seo-description: この記事では、サンプルのSPAアプリケーションを紹介し、SPAの組み合わせ方法を説明し、Reactフレームワークを使用して独自のSPAを使用して迅速に運用を開始できます。
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 41%

---


# Getting Started with SPAs in AEM - React{#getting-started-with-spas-in-aem-react}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、ReactフレームワークのシンプルなSPAアプリケーションを紹介し、その組み合わせ方法を説明します。これにより、独自のSPAを使用してすばやく作業を開始できます。

>[!NOTE]
>
>この記事はReactフレームワークに基づいています。 Angularフレームワークの対応するドキュメントについては、AEMのSPAの [使用の手引き — Angularを参照してください](/help/sites-developing/spa-getting-started-angular.md)。

>[!NOTE]
>
>SPAエディターは、SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトに推奨されるソリューションです。

## 概要 {#introduction}

この記事では、シンプルな SPA の基本的な機能と、SPA を運用するための最低条件の概要を説明します。

AEMでのSPAの動作方法の詳細については、次のドキュメントを参照してください。

* [SPAの概要とチュートリアル](/help/sites-developing/spa-walkthrough.md)
* [SPA オーサリングの概要](/help/sites-developing/spa-overview.md)
* [SPA ブループリント](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 内のコンテンツを作成するには、コンテンツを AEM に格納し、コンテンツモデルによって公開する必要があります。
>
>AEM 以外で開発された SPA については、コンテンツモデルのコントラクトに準拠していない場合、オーサリングをおこなうことはできません。

このドキュメントでは、Reactフレームワークを使用して作成されたシンプルなSPAの構造を順を追って説明し、その仕組みを説明して、この理解を独自のSPAに適用します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルの SPA では、必要な React の依存関係以外に、追加のライブラリも利用して SPA の作成を効率化できます。

### 依存関係 {#dependencies}

この `package.json` ファイルは、SPAパッケージ全体の要件を定義します。 動作中のSPAに対するAEMの最小依存関係を以下に示します。

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
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
>必要なバージョンの最小値 `aem-clientlib-generator` は1.4.1です。

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

### AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEMプロジェクトでは、 [AEM Project Archetype](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)（ReactまたはAngularを使用するSPAプロジェクトをサポートし、SPA SDKを利用する）を活用する必要があります。

## アプリケーション構造 {#application-structure}

前述のように依存関係を含め、アプリを作成すると、AEMインスタンスにアップロードできる有効なSPAパッケージが表示されます。

このドキュメントの次のセクションでは、AEMのSPAの構造、アプリケーションを駆動する重要なファイル、およびそれらの連携方法について説明します。

例としてシンプル化された画像コンポーネントが使用されますが、アプリケーションのすべてのコンポーネントは同じ概念に基づいています。

### index.js {#index-js}

SPA のエントリポイントはもちろん `index.js` ファイルです。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

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

コンポーネントテンプレート（JSXなど）を使用して静的にコンポーネントをインスタンス化する場合は、モデルからコンポーネントのプロパティに値を渡す必要があります。

### App.js {#app-js}

アプリをレンダリングすることで、`index.js` は `App.js` を呼び出します。このファイルの内容を以下に示していますが、重要な部分のみに焦点を当てるために簡略化されています。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` の主な役目は、アプリを構成するルートコンポーネントをラップすることです。アプリのエントリポイントは、ページです。

### Page.js {#page-js}

このページをレンダリングすると、ここに示す `App.js` 呼び出しをシンプル版 `Page.js` で表示します。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

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
import {MapTo} from '@adobe/aem-react-editable-components';

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
import { MapTo } from '@adobe/aem-react-editable-components';

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

単一ページのアプリケーション内のコンポーネントが情報を共有する場合は、定期的に必要となります。 これを行う方法には、次に示すように、複雑さを増す順序でいくつか推奨されます。

* **オプション1:** 例えばReact Contextを使用して、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション2:** Reduxなどのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション3:** コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

独自のSPAを作成する手順ガイドについては、「AEM SPA Editor - WKNDイベントの [概要チュートリアル](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)」を参照してください。

AEM用のSPAを開発するための自身の編成方法の詳細については、AEM用のSPAの [開発を参照してください](/help/sites-developing/spa-architecture.md)。

動的モデルとコンポーネントのマッピングおよびAEMのSPA内での動作について詳しくは、「SPAのSPA間の [動的モデルとコンポーネントのマッピング](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)」を参照してください。

AEMでReactやAngular以外のフレームワーク用にSPAを実装する場合、またはAEM用のSPA SDKの仕組みを詳しく調べる場合は、 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) の記事を参照してください。
