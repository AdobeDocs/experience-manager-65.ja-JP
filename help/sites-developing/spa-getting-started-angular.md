---
title: AEMでのSPAの使用の手引き — Angular
seo-title: AEMでのSPAの使用の手引き — Angular
description: この記事では、サンプルのSPAアプリケーションを紹介し、その組み合わせ方法を説明し、Angularフレームワークを使用して独自のSPAをすばやく習得できます。
seo-description: この記事では、サンプルのSPAアプリケーションを紹介し、その組み合わせ方法を説明し、Angularフレームワークを使用して独自のSPAをすばやく習得できます。
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# Getting Started with SPAs in AEM - Angular{#getting-started-with-spas-in-aem-angular}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AngularフレームワークのシンプルなSPAアプリケーションを紹介し、その組み合わせ方法を説明します。これにより、独自のSPAをすばやく使い始めることができます。

>[!NOTE]
>
>この記事はAngularフレームワークに基づいています。 対応するReactフレームワークのドキュメントについては、AEM - Reactの「SPAを使用する前に [」を参照してください](/help/sites-developing/spa-getting-started-react.md)。

>[!NOTE]
>
>SPAエディターは、SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトに推奨されるソリューションです。

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

このドキュメントでは、シンプル化されたSPAの構造を順を追って説明し、その仕組みを説明して、独自のSPAに適用します。

## 依存関係、設定、ビルド {#dependencies-configuration-and-building}

サンプルSPAは、期待されるAngularディペンデンシーに加えて、追加のライブラリを利用してSPAの作成をより効率的にできます。

### 依存関係 {#dependencies}

この `package.json` ファイルは、SPAパッケージ全体の要件を定義します。 必要最小限のAEM依存関係を以下に示します。

```
"dependencies": {
  "@adobe/cq-angular-editable-components": "~1.0.3",
  "@adobe/cq-spa-component-mapping": "~1.0.3",
  "@adobe/cq-spa-page-model-manager": "~1.0.4"
}
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

AEMプロジェクトは、ReactまたはAngularを使用してSPAプロジェクトをサポートし、SPA SDKを利用する [AEMプロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用する必要があります。

## アプリケーション構造 {#application-structure}

前述の依存関係を含め、アプリを作成すると、AEMインスタンスにアップロードできる作業中のSPAパッケージが表示されます。

このドキュメントの次の節では、AEMのSPAの構造、アプリケーションを駆動する重要なファイル、およびそれらの連携方法について説明します。

例としてシンプル化された画像コンポーネントが使用されますが、アプリケーションのすべてのコンポーネントは同じ概念に基づいています。

### app.module.ts {#app-module-ts}

The entry point into the SPA is the `app.module.ts` file shown here simplified to focus on the important content.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/cq-angular-editable-components';
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

この `app.module.ts` ファイルはアプリの開始点で、初期プロジェクト設定が含まれ、を使用してアプリをブートストラップ `AppComponent` します。

#### 静的インスタンス化 {#static-instantiation}

コンポーネントテンプレートを使用して静的にコンポーネントをインスタンス化する場合、値はモデルからコンポーネントのプロパティに渡す必要があります。 モデルの値は属性として渡され、後でコンポーネントプロパティとして使用できます。

### app.component.ts {#app-component-ts}

ブ `app.module.ts` ートストラップが完了 `AppComponent`すると、アプリを初期化できます。ここでは、重要なコンテンツに焦点を当てるためのシンプル版を示します。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/cq-spa-page-model-manager';
import { Constants } from "@adobe/cq-angular-editable-components";

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

ページを処理することで、簡単なバージョンでここに示す `app.component.ts` 呼び出し `main-content.component.ts` を実行できます。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/cq-angular-editable-components";

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

は、コンポ `Page` ーネントで構成されています。 JSONを取り込むと、は次に示すようなコンポーネントを処理 `Page` で `image.component.ts` きます。

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

AEM の SPA の中核概念は、SPA コンポーネントを AEM コンポーネントにマッピングし、コンテンツが変更されたときにコンポーネントも更新する（またはその逆も含む）というものです。See the document [SPA Editor Overview](/help/sites-developing/spa-overview.md) for an summary of this communication model.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo` メソッドは、SPA コンポーネントを AEM コンポーネントにマッピングします。単一の文字列または文字列の配列の使用に対応しています。

`ImageEditConfig` は、エディターがプレースホルダーを生成するために必要なメタデータを提供することで、コンポーネントのオーサリング機能の有効化に関与する設定オブジェクトです。

コンテンツがない場合は、空のコンテンツを表すラベルがプレースホルダーとして提供されます。

#### 動的に渡されるプロパティ {#dynamically-passed-properties}

モデルからのデータは、コンポーネントのプロパティとして動的に渡されます。

### image.component.html {#image-component-html}

最後に、でイメージをレンダリングでき `image.component.html`ます。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPAコンポーネント間での情報の共有 {#sharing-information-between-spa-components}

単一ページのアプリケーション内のコンポーネントが情報を共有する場合は、定期的に必要となります。 これを行う方法には、次に示すように、複雑さを増す順序でいくつか推奨されます。

* **オプション1:** utilクラスを純粋なオブジェクト指向のソリューションとして使用するなど、ロジックを一元化し、必要なコンポーネントにブロードキャストします。
* **オプション2:** NgRxなどのステートライブラリを使用して、コンポーネントの状態を共有します。
* **オプション3:** コンテナコンポーネントをカスタマイズおよび拡張することで、オブジェクト階層を活用します。

## 次の手順 {#next-steps}

独自のSPAを作成する手順ガイドについては、「AEM SPA Editor - WKNDイベントの [手引きチュートリアル](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)」を参照してください。

AEM用のSPAを開発するための自社統計の詳細については、「AEM用のSPAの [開発](/help/sites-developing/spa-architecture.md)」を参照してください。

動的モデルとコンポーネントのマッピングおよびAEMのSPA内での動作について詳しくは、「SPAのSPA間の [動的モデルとコンポーネントのマッピング](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)」を参照してください。

ReactやAngular以外のフレームワーク用にAEMにSPAを実装する場合、または単にSPA SDK for AEMの仕組みを詳しく調べたい場合は、 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) の記事を参照してください。
