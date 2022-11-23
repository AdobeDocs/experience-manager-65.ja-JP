---
title: React を使用した AEM での SPA の概要
seo-title: Getting Started with SPAs in AEM - React
description: この記事では、サンプルの SPA アプリケーションを紹介し、その設定方法を説明するほか、React を使用して独自の SPA の運用を速やかに開始する方法についても説明します。
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the React framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: ht
source-wordcount: '1166'
ht-degree: 100%

---

# React を使用した AEM での SPA の概要{#getting-started-with-spas-in-aem-react}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、React フレームワーク上のシンプルな SPA アプリケーションを紹介し、その設定方法を説明するほか、独自の SPA の運用をすぐに開始する方法についても説明します。

>[!NOTE]
>
>この記事は React フレームワークに基づいています。対応する Angular フレームワークのドキュメントについては、「[Angular を使用した AEM での SPA の概要](/help/sites-developing/spa-getting-started-angular.md)」を参照してください。

>[!NOTE]
>
>SPA エディターは、SPA フレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトで有効なソリューションです。

## はじめに {#introduction}

この記事では、シンプルな SPA の基本的な機能と、SPA を運用するための最低条件の概要を説明します。

AEM での SPA の動作について詳しくは、次のドキュメントを参照してください。

* [SPA の概要およびガイド](/help/sites-developing/spa-walkthrough.md)
* [SPA オーサリングの概要](/help/sites-developing/spa-overview.md)
* [SPA ブループリント](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 内のコンテンツを作成するには、コンテンツを AEM に格納し、コンテンツモデルによって公開する必要があります。
>
>AEM 以外で開発された SPA については、コンテンツモデルのコントラクトに準拠していない場合、オーサリングを行うことはできません。

このドキュメントでは、React フレームワークを使用して作成されたシンプルな SPA の構造を順を追って解説し、その仕組みを理解した上で独自の SPA に適用する方法を説明します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルの SPA では、必要な React の依存関係以外に、追加のライブラリも利用して SPA の作成を効率化できます。

### 依存関係 {#dependencies}

`package.json` ファイルは、SPA パッケージ全体の要件を定義します。SPA の動作に対する AEM の最小依存関係を以下に示します。

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

クライアントライブラリの作成をビルドプロセスの一部として自動化するために、`aem-clientlib-generator` が活用されています。

`"aem-clientlib-generator": "^1.4.1",`

詳しくは、[GitHub のこちらのページ](https://github.com/wcm-io-frontend/aem-clientlib-generator)を参照してください。

>[!CAUTION]
>
>必要な `aem-clientlib-generator` の最小バージョンは 1.4.1 です。

`aem-clientlib-generator` は、`clientlib.config.js` ファイルで次のように設定されています。

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

AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## アプリケーション構造 {#application-structure}

以前に説明したように依存関係を追加してアプリをビルドすると、AEM インスタンスにアップロードできる SPA パッケージが作成されます。

このドキュメントの次の節では、AEM での SPA 自体の構造と、アプリケーションの動作にかかわる重要なファイルのほか、それらのファイルがどのように連携するのかについて説明します。

シンプルな画像コンポーネントを例として使用していますが、このアプリケーションのコンポーネントはすべて同じ概念に基づいています。

### index.js {#index-js}

SPA のエントリポイントはもちろん `index.js` ファイルです。このファイルの内容を以下に示しますが、重要な部分のみに焦点を当てるために簡略化しています。

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

`index.js` の主要機能は、`ReactDOM.render` 関数を活用して、DOM 内でアプリケーションをインジェクトする場所を決めることです。

これはこの関数の標準的な使用方法です。このアプリ例に独自の使用方法ではありません。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレート（JSX など）を使用して静的にコンポーネントをインスタンス化する場合は、モデルからコンポーネントのプロパティに値を渡す必要があります。

### App.js {#app-js}

アプリをレンダリングすることで、`index.js` は `App.js` を呼び出します。このファイルの内容を以下に示しています（重要な部分のみに焦点を当てるために簡略化されています）。

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` の主な役目は、アプリを構成するルートコンポーネントをラップすることです。アプリのエントリポイントはページです。

### Page.js {#page-js}

ページをレンダリングすると、`App.js` は以下の `Page.js`（簡易表示）を呼び出します。

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

この例の `AppPage` クラスでは、インナーコンテンツメソッドを含む `Page` を拡張して使用します。

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

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。この通信モデルの概要については、[SPA エディターの概要](/help/sites-developing/spa-overview.md)のドキュメントを参照してください。

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

`MapTo` 関数は、指定された `Component` を、オーサリング可能にするクラス名と属性で拡張した構成結果の `PageClass` を返します。このコンポーネントは後でエクスポートし、アプリケーションのマークアップでインスタンス化できます。

`MapTo` または `withModel` 関数を使用してエクスポートされた `Page` コンポーネントは、`ModelProvider` コンポーネントによってラップされます。このコンポーネントは、標準コンポーネントに、ページモデルの最新バージョンに対するアクセス権またはそのページモデル内の詳細な位置を提供します。

詳しくは、[SPA ブループリントのドキュメント](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)を参照してください。

>[!NOTE]
>
>デフォルトでは、`withModel` 関数を使用するとコンポーネントのモデル全体を受け取ります。

## SPA コンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有することは定期的に必要です。これをおこなう推奨方法にはいくつかあり、以下に簡単なものから順に示します。

* **オプション 1：** React Context などを使用して、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション 2：** Redux などのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション 3：**&#x200B;コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

独自の SPA を作成する手順については、[AEM SPA Editor 使用の手引き — WKND イベントチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=ja)を参照してください。

効率的に AEM 向け SPA を開発する方法について詳しくは、記事 [AEM 向け SPA の開発](/help/sites-developing/spa-architecture.md)を参照してください。

動的モデルからコンポーネントへのマッピング、および　AEM の SPA 内での動作について詳しくは、[SPA の動的モデルからコンポーネントへのマッピング](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)の記事を参照してください。

React や Angular 以外のフレームワーク用に AEM の SPA を実装する場合や、AEM 用 SPA SDK の仕組みを詳しく知りたい場合は、[SPA ブループリント](/help/sites-developing/spa-blueprint.md)の記事を参照してください。
