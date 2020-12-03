---
title: AEM 向け SPA の開発
seo-title: AEM 向け SPA の開発
description: この記事では、フロントエンド開発者が AEM 向けの SPA を開発する際に考慮すべき重要な問題と、開発済み SPA を AEM にデプロイする際に念頭に置くべきな SPA に関する AEM のアーキテクチャの概要を説明します。
seo-description: この記事では、フロントエンド開発者が AEM 向けの SPA を開発する際に考慮すべき重要な問題と、開発済み SPA を AEM にデプロイする際に念頭に置くべきな SPA に関する AEM のアーキテクチャの概要を説明します。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 86%

---


# AEM 向け SPA の開発{#developing-spas-for-aem}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

この記事では、フロントエンド開発者が AEM 向けの SPA を開発する際に考慮すべき重要な問題を紹介し、SPA を AEM にデプロイする際に関する AEM のアーキテクチャの概要を説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## AEM 向け SPA 開発原則 {#spa-development-principles-for-aem}

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。次の一般的なベストプラクティスには AEM 固有の原則はほぼなく、フロントエンド開発者がそれに従うことで、SPA は [AEM とコンテンツオーサリング機能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)と共に機能します。

* **[移植性](/help/sites-developing/spa-architecture.md#portability)**  — 任意のコンポーネントと同様に、コンポーネントは可能な限り持ち運び可能な状態で構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **[AEM を主軸にしたサイト構築](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEM に依存してサイトのコンテンツ構造を定義します。
* **[動的レンダリング](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - すべてのレンダリングは動的である必要があります。
* **[動的ルーティング](#dynamic-routing) - SPA** は、ルーティングを処理し、AEMはそれをリッスンし、それに基づいて取得します。どのルーティングも動的である必要があります。

SPA の開発時にこれらの原則を念頭に置いておけば、サポートされるすべての AEM オーサリング機能を有効にしつつ、柔軟性と将来性も可能な限り実現できます。

AEM オーサリング機能をサポートする必要がない場合は、別の [SPA 設計モデル](/help/sites-developing/spa-architecture.md#spa-design-models)を検討する必要が生じる場合があります。

### 移植性 {#portability}

その他のあらゆるコンポーネントを開発する場合と同様に、コンポーネントの移植性を最大限に高めるように設計する必要があります。互換性、柔軟性、保守性を今後も保証するために、コンポーネントの移植性や再利用性に反するパターンは避ける必要があります。

作成する SPA は、移植性が高く、再利用可能なコンポーネントを使用して構築する必要があります。

### AEM を主軸にしたサイト構築 {#aem-drives-site-structure}

フロントエンド開発者は、アプリの作成に使用される SPA コンポーネントのライブラリの作成を自分自身が担当していると考える必要があります。フロントエンド開発者は、コンポーネントの内部構造を完全に制御できます。[ただし、AEM は常にサイトの構造を所有しています。](/help/sites-developing/spa-overview.md)

つまり、フロントエンド開発者は、コンポーネントのエントリポイントの前後に顧客コンテンツを追加でき、コンポーネント内でサードパーティの呼び出しをおこなうこともできます。ただし、フロントエンド開発者は、例えばコンポーネントのネスト方法を完全に制御するわけではありません。

### 動的レンダリング {#dynamic-rendering}

SPA では、コンテンツの動的レンダリングのみに依存する必要があります。AEM がコンテンツ構造のすべての子を取得してレンダリングすることは、デフォルトで期待されています。  [](/help/sites-developing/spa-architecture.md#portability)

特定のコンテンツを指す明示的なレンダリングは静的レンダリングと見なされ、サポートされているものの、AEM コンテンツオーサリング機能との互換性はありません。これは[移植性](/help/sites-developing/spa-architecture.md#portability)の原則に反するものでもあります。

### 動的ルーティング {#dynamic-routing}

レンダリングと同様に、すべてのルーティングも動的である必要があります。AEM では、[SPA が常にルーティングを所有](/help/sites-developing/spa-routing.md)し、AEM がリッスンしてそれに基づいてコンテンツを取得します。

静的なルーティングは[移植性の原則](/help/sites-developing/spa-architecture.md#portability)に反し、AEM のコンテンツオーサリング機能との互換性がないことから、作成者を制限することになります。例えば、静的ルーティングの場合、コンテンツ作成者はルートの変更やページの変更を希望する場合は、フロントエンド開発者に依頼する必要があります。

## AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## SPA デザインモデル {#spa-design-models}

[AEM での SPA 開発の原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)に従えば、SPA はサポートされるすべての AEM コンテンツオーサリング機能と共に機能します。  [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

ただし、これが全く必要でない場合もあります。次の表に、様々なデザインモデルの長所と短所の概要を示します。

<table>
 <tbody>
  <tr>
   <th><strong>設計モデル<br /> </strong></th>
   <th><strong>メリット</strong></th>
   <th><strong>デメリット</strong></th>
  </tr>
  <tr>
   <td>AEM は、<a href="/help/sites-developing/spa-reference-materials.md">SPA エディター SDK フレームワークを使用せずにヘッドレスな CMS として使用されます。</a></td>
   <td>フロントエンド開発者は、アプリを完全に制御できます。</td>
   <td><p>コンテンツ作成者は、AEM のコンテンツオーサリングエクスペリエンスを活用できません。</p> <p>コードに静的参照またはルーティングが含まれる場合、コードは移動も再利用もできません。</p> <p>テンプレートエディターの使用を許可しないので、フロントエンド開発者は JCR を介して編集可能なテンプレートを維持する必要があります。</p> </td>
  </tr>
  <tr>
   <td>フロントエンド開発者は SPA エディター SDK フレームワークを使用しますが、コンテンツ作成者に対して一部の領域のみを開きます。</td>
   <td>開発者は、アプリの制限された領域でのみオーサリングを有効にすることで、アプリを管理し続けます。</td>
   <td><p>コンテンツ作成者は、AEM コンテンツオーサリングエクスペリエンスの限られたセットに制限されます。</p> <p>コードに静的参照またはルーティングが含まれる場合、移動や再利用性できない問題が発生する可能性があります。</p> <p>テンプレートエディターの使用を許可しないので、フロントエンド開発者は JCR を介して編集可能なテンプレートを維持する必要があります。</p> </td>
  </tr>
  <tr>
   <td>このプロジェクトは SPA エディター SDK を十二分に活用し、フロントエンドコンポーネントはライブラリとして開発され、アプリのコンテンツ構造は AEM に委任されます。</td>
   <td><p>アプリは再利用可能で移動可能です。</p> <p>コンテンツ作成者は、AEM コンテンツオーサリングエクスペリエンスを使用してアプリを編集できます。<br /> </p> <p>SPA は、テンプレートエディターと互換性があります。</p> </td>
   <td><p>開発者は、アプリの構造と AEM に委任されたコンテンツを管理できません。</p> <p>ただし、開発者は、AEM で作成する予定ではないコンテンツ用にアプリの領域を予約できます。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM ではすべてのモデルがサポートされていますが、3 番目のモデルを実装することでのみ（つまり AEM で推奨される [SPA 開発原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)に従うことで）、コンテンツ作成者は SPA のコンテンツをいつもどおりに操作、編集できます。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 既存の SPA から AEM への移行 {#migrating-existing-spas-to-aem}

一般的に、SPA が [AEM の SPA 開発原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)に従う場合、SPA は AEM で動作し、AEM SPA エディターを使用して編集できます。

既存の SPA を AEM で動作する準備をするには、次の手順に従います。

1. **JS コンポーネントをモジュラー化します。**

   任意の順序、位置、サイズでレンダリングできるようにします。
1. **SDK が提供するコンテナを使用して、コンポーネントを画面に配置します。**

   AEMでは、ページと段落のシステムコンポーネントを使用できます。
1. **各 JS コンポーネントに AEM コンポーネントを作成します。**

   AEMコンポーネントは、ダイアログとJSON出力を定義します。

## フロントエンド開発者向けの説明 {#instructions-for-front-end-developers}

フロントエンド開発者にAEM用のSPAを作成するように命じる主なタスクは、コンポーネントとそのJSONモデルについて同意することです。

AEM 用の SPA を開発する際に、フロントエンド開発者が実行する必要のある手順の概要を次に示します。

1. **コンポーネントと JSON モデルに合意する**

   フロントエンド開発者とバックエンド AEM 開発者は、必要なコンポーネントとモデルについて合意し、SPA コンポーネントからバックエンドコンポーネントに 1 対 1 で一致させる必要があります。

   AEM コンポーネントは、主に編集ダイアログを提供し、コンポーネントモデルを書き出すためにも必要です。

1. **React コンポーネントでは、`this.props.cqModel`** を介してアクセスする

   コンポーネントについて合意が取れ、JSON モデルが設定されると、フロントエンド開発者は SPA を自由に開発でき、`this.props.cqModel` を介して JSON モデルに簡単にアクセスできます。

1. **コンポーネントの `render()` メソッドを実装する**

   フロントエンド開発者は、適切に表示されると`render()`メソッドを実装し、`cqModel`プロパティのフィールドを使用できます。 これにより、DOM と、ページに挿入される HTML フラグメントが出力されます。これは、React でアプリを作成する標準的な方法です。

1. **`MapTo()`** を使用してコンポーネントを AEM リソースタイプにマッピングする

   マッピングはコンポーネントクラスを格納し、`Container` コンポーネントによって内部的に使用され、提供されたリソースタイプに基づいてコンポーネントを取得して動的にインスタンス化します。

   これはフロントエンドとバックエンドの間の「接着剤」の役割を果たすので、エディターは、どのコンポーネントが React コンポーネントに対応するのかがわかります。

   `Page` と `ResponsiveGrid` は、基本 `Container` を拡張するクラスの好例です。

1. **コンポーネントの `EditConfig` を`MapTo()`** へのパラメーターとして定義する

   このパラメーターは、コンポーネントがまだレンダリングされていないか、レンダリングするコンテンツがない場合に、コンポーネントの名前をどのように付けるかをエディターに指示するために必要です。

1. **ページとコンテナに提供されている `Container` クラスを拡張する**

   ページと段落システムは、内部コンポーネントへの委任が期待どおりに機能するように、このクラスを拡張する必要があります。

1. **HTML5 `History` API を使用したルーティングソリューションを実装する。**

   `ModelRouter` が有効な場合、`pushState` および `replaceState` 関数を呼び出すと、モデルの欠落したフラグメントを取得するための要求が `PageModelManager` にトリガーされます。

   `ModelRouter` の現在のバージョンでは、Sling Model エントリポイントの実際のリソースパスを指す URL のみ使用できます。バニティ URL やエイリアスの使用はサポートされません。

   `ModelRouter` は、無効にしたり、正規表現のリストを無視するように設定したりできます。

## AEM 非依存 {#aem-agnostic}

これらのコードブロックは、ReactコンポーネントとAngularコンポーネントが、AdobeやAEM固有の何も必要としないことを示します。

* JavaScript コンポーネント内にあるものはすべて、AEM 非依存です。
* AEM に固有なことは、JS コンポーネントを MapTo ヘルパーを使用して AEM コンポーネントにマッピングする必要がある点です。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo` ヘルパーは、バックエンドとフロントエンドのコンポーネントを一致させる「接着剤」です。

* これは、JS コンテナ（または JS 段落システム）に、JSON に存在する各コンポーネントのレンダリングは、どの JS コンポーネントが関与するのかを伝えるものです。
* JS コンポーネントでレンダリングされる HTML に HTML データ属性が追加されるので、SPA エディターは、コンポーネントの編集時に作成者に表示するダイアログボックスを把握できます。

`MapTo` の使用法と AEM 向け SPA の構築の概要について詳しくは、選択したフレームワークの概要を参照してください。

* [AEMのSPAを使い始める — React](/help/sites-developing/spa-getting-started-react.md)
* [AEMのSPA使用の手引き — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM のアーキテクチャと SPA {#aem-architecture-and-spas}

開発、オーサリング、公開環境を含む AEM の一般的なアーキテクチャは、SPA を使用する場合でも変更されません。ただし、SPA 開発がこのアーキテクチャにどのように適合しているかを理解することに役立ちます。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **ビルド環境**

   SPA のアプリケーションとコンポーネントのソースは、ここでチェックアウトされます。

   * NPM clientlib ジェネレーターは、SPA プロジェクトからクライアントライブラリを作成します。
   * ライブラリは Maven によって取得され、AEM オーサーのコンポーネントと共に、Maven Build プラグインによってデプロイされます。

* **AEM オーサー**

   コンテンツは、AEM オーサー（オーサリング SPA を含む）で作成されます。

   オーサリング環境で SPA エディターを使用して SPA を編集する場合の流れは次の通りです。

   1. SPA は外部の HTML をリクエストします。
   1. CSS が読み込まれます。
   1. SPA アプリケーションの JavaScript が読み込まれます。
   1. SPA アプリケーションを実行すると、JSON がリクエストされ、アプリが `cq-data` 属性を含むページの DOM を構築できるようになります。
   1. この `cq-data` 属性を使用すると、エディターが追加のページ情報を読み込んで、コンポーネントで使用する編集設定を把握できるようになります。

* **AEM パブリッシュ**

   SPA アプリケーションアーティファクト、クライアントライブラリ、コンポーネントなどのオーサリング済みコンテンツおよびコンパイル済みライブラリが、一般向けに公開される場所です。

* **Dispatcher／CDN**

   Dispatcher は、サイト訪問者に対する AEM のキャッシュ層の役割を果たします。

   * リクエストは、AEM オーサーでの処理と同様に処理されますが、ページ情報のリクエストはありません。ページ情報はエディターのみに必要とされる情報だからです。
   * JavaScript、CSS、JSON および HTML がキャッシュされ、配信が高速になるようにページが最適化されます。

>[!NOTE]
>
>AEM 内では、JavaScript のビルドメカニズムを実行したり、JavaScript 自体を実行したりする必要はありません。AEM は、SPA アプリケーションからコンパイルされたアーティファクトのみをホストします。

## 次の手順 {#next-steps}

AEMの単純なSPAの構造とその仕組みの概要については、[React](/help/sites-developing/spa-getting-started-react.md)と[Angular](/help/sites-developing/spa-getting-started-angular.md)の両方の入門ガイドを参照してください。

独自のSPAを作成する手順を説明したガイドについては、『AEM SPA Editor - WKNDイベントの使い始めに — チュートリアル[』を参照してください。](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)

動的モデルとコンポーネントのマッピングおよびAEMのSPA内での動作について詳しくは、「SPA[の動的モデルとコンポーネントのマッピング」を参照してください。](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)

ReactやAngular以外のフレームワーク用にSPAをAEMに実装する場合、またはAEM用のSPA SDKの仕組みを簡単に詳しく調べたい場合は、[SPA Blueprint](/help/sites-developing/spa-blueprint.md)の記事を参照してください。
