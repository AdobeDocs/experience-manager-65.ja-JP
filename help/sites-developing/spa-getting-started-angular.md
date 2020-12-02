---
title: AEMのSPA使用の手引き — Angular
seo-title: AEMのSPA使用の手引き — Angular
description: この記事では、サンプルの SPA アプリケーションを紹介し、その設定方法を説明するほか、Angular フレームワークを使用して独自の SPA の運用をすぐに開始する方法についても説明します。
seo-description: この記事では、サンプルの SPA アプリケーションを紹介し、その設定方法を説明するほか、Angular フレームワークを使用して独自の SPA の運用をすぐに開始する方法についても説明します。
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 84%

---


# AEMでのSPAの使用の手引き — Angular{#getting-started-with-spas-in-aem-angular}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、Angular フレームワーク上のシンプルな SPA アプリケーションを紹介し、その組み合わせ方法を説明します。これにより、独自の SPA をすぐに使い始めることができます。

>[!NOTE]
>
>この記事は Angular フレームワークに基づいています。対応する React フレームワークのドキュメントについては、「 [AEM での SPA の使用 - React](/help/sites-developing/spa-getting-started-react.md)」を参照してください。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

この記事では、シンプルな SPA の基本的な機能と、SPA を運用するための最低条件の概要を説明します。

AEM での SPA の動作について詳しくは、次のドキュメントを参照してください。

* [SPA の概要およびガイド](/help/sites-developing/spa-walkthrough.md)
* [SPA オーサリングの概要](/help/sites-developing/spa-overview.md)
* [SPA ブループリント](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>SPA 内のコンテンツを作成するには、コンテンツを AEM に格納し、コンテンツモデルによって公開する必要があります。
>
>AEM 以外で開発された SPA については、コンテンツモデルのコントラクトに準拠していない場合、オーサリングをおこなうことはできません。

このドキュメントでは、簡略化された SPA の構造と仕組みを説明します。お客様の SPA にも応用できる内容になっています。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルの SPA では、必要な Angular の依存関係以外に、追加のライブラリも利用して SPA の作成を効率化できます。

### 依存関係 {#dependencies}

`package.json` ファイルは、SPA パッケージ全体の要件を定義します。必要最小限の AEM 依存関係を以下に示します。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator` は、クライアントライブラリの作成をビルドプロセスの一部として自動化しています。

`"aem-clientlib-generator": "^1.4.1",`

詳しくは、[GitHub のこちらのページ](https://github.com/wcm-io-frontend/aem-clientlib-generator)を参照してください。

>[!CAUTION]
>
>必要な`aem-clientlib-generator`の最小バージョンは1.4.1です。

`aem-clientlib-generator` は、`clientlib.config.js` ファイルで次のように設定されています。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

ビルドが完了したら、パッケージを AEM インスタンスにアップロードできます。

### AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## アプリケーション構造 {#application-structure}

依存関係を追加して以前に説明したようにアプリをビルドすると、AEM インスタンスにアップロードできる SPA パッケージが作成されます。

このドキュメントの次の節では、AEM での SPA の構造と、アプリケーションの動作にかかわる重要なファイルのほか、それらのファイルがどのように連携するのかについて説明します。

簡潔化された画像コンポーネントを例として使用していますが、このアプリケーションのコンポーネントはすべて同じ概念に基づいています。

### app.module.ts {#app-module-ts}

SPA のエントリポイントは `app.module.ts` ファイルです。このファイルの内容を以下に示しますが、重要な部分のみに焦点を当てるために簡略化されています。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

`app.module.ts` ファイルはアプリの開始点で、初期プロジェクト設定が含まれ、`AppComponent` を使用してアプリをブートストラップします。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレートを使用して静的にコンポーネントをインスタンス化する場合、値はモデルからコンポーネントのプロパティに渡す必要があります。モデルの値は属性として渡され、後でコンポーネントプロパティとして使用できます。

### app.component.ts {#app-component-ts}

`app.module.ts` が `AppComponent` をブートストラップすると、アプリを初期化することができます。ここでは、重要なコンテンツに焦点を当てるための簡略化されたバージョンを示します。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

`app.component.ts`は、この単純化されたバージョンの`main-content.component.ts`を呼び出します。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` は、ページモデルの JSON 表現を取り込み、コンテンツを処理してページの各要素をラップ／デコレートします。`Page` のその他の詳細については、[SPA ブループリント](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)のドキュメントを参照してください。

### image.component.ts {#image-component-ts}

`Page` は、コンポーネントで構成されています。JSON を取得すると、`Page` は次に示すように `image.component.ts` のようなコンポーネントを処理できます。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。この通信モデルの概要については、[SPA エディターの概要](/help/sites-developing/spa-overview.md)のドキュメントを参照してください。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo` メソッドは、SPA コンポーネントを AEM コンポーネントにマッピングします。単一の文字列または文字列の配列の使用に対応しています。

`ImageEditConfig` は、エディターがプレースホルダーを生成するために必要なメタデータを提供することで、コンポーネントのオーサリング機能の有効化に関与する設定オブジェクトです。

コンテンツがない場合は、空のコンテンツを表すラベルがプレースホルダーとして提供されます。

#### 動的に渡されるプロパティ {#dynamically-passed-properties}

モデルからのデータは、コンポーネントのプロパティとして動的に渡されます。

### image.component.html {#image-component-html}

最後に、`image.component.html` でイメージをレンダリングできます。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPA コンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有することは定期的に必要です。これをおこなう推奨方法にはいくつかあり、以下に簡単なものから順に示します。

* **オプション 1**：util クラスを純粋なオブジェクト指向のソリューションとして使用するなど、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション 2**：NgRx などのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション 3**：コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

独自のSPAを作成する手順を説明したガイドについては、『AEM SPA Editor - WKNDイベントの使い始めに — チュートリアル[』を参照してください。](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)

AEM向けSPAを開発するための組織編成の詳細については、「 AEM用SPAの開発[](/help/sites-developing/spa-architecture.md)」を参照してください。

動的モデルとコンポーネントのマッピングおよびAEMのSPA内での動作について詳しくは、「SPA[の動的モデルとコンポーネントのマッピング」を参照してください。](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

ReactやAngular以外のフレームワーク用にSPAをAEMに実装する場合、またはAEM用のSPA SDKの仕組みを簡単に詳しく調べたい場合は、[SPA Blueprint](/help/sites-developing/spa-blueprint.md)の記事を参照してください。
