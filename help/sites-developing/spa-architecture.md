---
title: Adobe Experience Manager向けSPAの開発
description: この記事では、フロントエンド開発者がSPA for Adobe Experience Manager(AEM) を開発する際に考慮すべき重要な質問を紹介し、開発済みSPAをAEMにデプロイする際に念頭に置くべきSPAに関するAEMのアーキテクチャの概要を説明します。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 73%

---

# AEM 向け SPA の開発{#developing-spas-for-aem}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者はSPAフレームワークを使用してサイトを構築できるようにしたいと考え、作成者は、そのようなフレームワークを使用して構築されたサイトのAdobe Experience Manager(AEM) 内のコンテンツをシームレスに編集したいと考えています。

この記事では、フロントエンド開発者がAEM向けのSPAを開発する際に考慮すべき重要な質問を紹介し、AEMへのSPAのデプロイに関するAEMのアーキテクチャの概要を説明します。

>[!NOTE]
>
>SPA Editor は、SPAフレームワークベースのクライアントサイドレンダリング (React やAngularなど ) が必要なプロジェクトで推奨されるソリューションです。

## AEM 向け SPA 開発原則 {#spa-development-principles-for-aem}

AEM で単一ページアプリケーションを開発する場合、フロントエンド開発者は SPA を作成する際に標準的なベストプラクティスを順守するものと想定します。次の一般的なベストプラクティスとAEM固有の原則に従うことで、フロントエンド開発者はSPAを使用して機能できます。 [AEMとそのコンテンツオーサリング機能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[移植性](/help/sites-developing/spa-architecture.md#portability) -**&#x200B;通常のあらゆるコンポーネントと同様に、コンポーネントは、移植性を可能な限り維持しながら構築する必要があります。SPA は、移動可能で再利用可能なコンポーネントを使用して構築する必要があります。
* **[AEM を主軸にしたサイト構築](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、AEM に依存してサイトのコンテンツ構造を定義します。
* **[動的レンダリング](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - すべてのレンダリングは動的である必要があります。
* **[動的ルーティング](#dynamic-routing) -** SPA がルーティングを担い、AEM はリッスンしたその情報に基づいて取得します。どのルーティングも動的である必要があります。

SPA の開発時にこれらの原則を念頭に置いておけば、サポートされるすべての AEM オーサリング機能を有効にしつつ、柔軟性と将来性も可能な限り実現できます。

AEM オーサリング機能をサポートする必要がない場合は、別の [SPA 設計モデル](/help/sites-developing/spa-architecture.md#spa-design-models)を検討する必要が生じる場合があります。

### 移植性 {#portability}

その他のあらゆるコンポーネントを開発する場合と同様に、コンポーネントの移植性を最大限に高めるように設計する必要があります。互換性、柔軟性、保守性を今後も保証するために、コンポーネントの移植性や再利用性に反するパターンは避ける必要があります。

作成する SPA は、移植性が高く、再利用可能なコンポーネントを使用して構築する必要があります。

### AEM を主軸にしたサイト構築 {#aem-drives-site-structure}

フロントエンド開発者は、アプリの作成に使用される SPA コンポーネントのライブラリの作成を自分自身が担当していると考える必要があります。フロントエンド開発者は、コンポーネントの内部構造を完全に制御できます。[ただし、AEMは常にサイトの構造を所有しています。](/help/sites-developing/spa-overview.md)

つまり、フロントエンド開発者は、コンポーネントのエントリポイントの前後に顧客コンテンツを追加したり、コンポーネント内でサードパーティ呼び出しをおこなうこともできます。 ただし、フロントエンド開発者は、例えばコンポーネントのネスト方法を完全に制御するわけではありません。

### 動的レンダリング {#dynamic-rendering}

SPA では、コンテンツの動的レンダリングのみに依存する必要があります。AEM がコンテンツ構造のすべての子を取得してレンダリングすることは、デフォルトで期待されています。

特定のコンテンツを指す明示的なレンダリングは静的レンダリングと見なされ、サポートされているものの、AEM コンテンツオーサリング機能との互換性はありません。これは[移植性](/help/sites-developing/spa-architecture.md#portability)の原則に反するものでもあります。

### 動的ルーティング {#dynamic-routing}

レンダリングと同様に、すべてのルーティングも動的である必要があります。AEM では、[SPA が常にルーティングを所有](/help/sites-developing/spa-routing.md)し、AEM がリッスンしてそれに基づいてコンテンツを取得します。

静的なルーティングは[移植性の原則](/help/sites-developing/spa-architecture.md#portability)に反し、AEM のコンテンツオーサリング機能との互換性がないことから、作成者を制限することになります。例えば、静的ルーティングの場合、コンテンツ作成者がルートの変更やページの変更を希望する場合は、フロントエンド開発者に依頼する必要があります。

## AEM プロジェクトアーキタイプ {#aem-project-archetype}

AEM プロジェクトでは、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## SPA デザインモデル {#spa-design-models}

[AEM での SPA 開発の原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)に従えば、SPA はサポートされるすべての AEM コンテンツオーサリング機能と共に機能します。

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
   <td>このプロジェクトは SPA エディター SDK を十分に活用し、フロントエンドコンポーネントはライブラリとして開発され、アプリのコンテンツ構造は AEM にデリゲートされます。</td>
   <td><p>アプリは再利用可能で移動可能です。</p> <p>コンテンツ作成者は、AEM コンテンツオーサリングエクスペリエンスを使用してアプリを編集できます。<br /> </p> <p>SPA は、テンプレートエディターと互換性があります。</p> </td>
   <td><p>開発者は、アプリの構造と AEM に委任されたコンテンツを管理できません。</p> <p>ただし、開発者は、AEM で作成する予定ではないコンテンツ用にアプリの領域を予約できます。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEMではすべてのモデルがサポートされていますが、3 番目のモデルを実装することによってのみ ( したがって、推奨される [AEMでのSPA開発原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) を使用すると、コンテンツ作成者は、AEMでSPAのコンテンツをいつもどおりに操作および編集できます。

## 既存の SPA から AEM への移行 {#migrating-existing-spas-to-aem}

一般的に、SPA が [AEM の SPA 開発原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)に従う場合、SPA は AEM で動作し、AEM SPA エディターを使用して編集できます。

既存の SPA を AEM で動作する準備をするには、次の手順に従います。

1. **JS コンポーネントをモジュラー化します。**

   任意の順序、位置、サイズでレンダリングできるようにします。
1. **Adobeの SDK が提供するコンテナを使用して、コンポーネントを画面に配置します。**

    AEM を使用すると、ページと段落のシステムコンポーネントを使用できます。
1. **各 JS コンポーネントに AEM コンポーネントを作成します。**

   AEM コンポーネントは、ダイアログと JSON の出力を定義します。

## フロントエンド開発者向けの説明 {#instructions-for-front-end-developers}

フロントエンド開発者が AEM 用の SPA を作成する際に行う主なタスクは、コンポーネントとその JSON モデルについて合意することです。

SPA for AEMを開発する際に、フロントエンド開発者が従う必要のある手順の概要を次に示します。

1. **コンポーネントと JSON モデルに合意する**

   フロントエンド開発者とバックエンドAEM開発者は、必要なコンポーネントとモデルについて合意し、SPAコンポーネントからバックエンドコンポーネントに 1 対 1 で一致させる必要があります。

   AEM コンポーネントは、主に編集ダイアログを提供し、コンポーネントモデルを書き出すためにも必要です。

1. **React コンポーネントでは、`this.props.cqModel`** を介してアクセスする

   コンポーネントについて合意が取れ、JSON モデルが設定されると、フロントエンド開発者は SPA を自由に開発でき、`this.props.cqModel` を介して JSON モデルに簡単にアクセスできます。

1. **コンポーネントの `render()` メソッド**&#x200B;を実装する

   フロントエンド開発者は、自由に `render()` メソッドを実装し、`cqModel` プロパティのフィールドを使用できます。これにより、DOM と、ページに挿入されたHTMLフラグメントが出力されます。 これは、React でアプリを作成する標準的な方法です。

1. **`MapTo()`** を使用してコンポーネントを AEM リソースタイプにマッピングする

   マッピングはコンポーネントクラスを格納し、`Container` コンポーネントによって内部的に使用され、提供されたリソースタイプに基づいてコンポーネントを取得して動的にインスタンス化します。

   これはフロントエンドとバックエンドの間の「接着剤」の役割を果たすので、エディターは、どのコンポーネントが React コンポーネントに対応するのかがわかります。

   `Page` と `ResponsiveGrid` は、基本 `Container` を拡張するクラスの好例です。

1. **コンポーネントの `EditConfig` を`MapTo()`** へのパラメーターとして定義する

   このパラメーターは、コンポーネントがまだレンダリングされていないか、レンダリングするコンテンツがない場合に、コンポーネントの名前をどのように付けるかをエディターに指示するために必要です。

1. **ページとコンテナに提供されている `Container` クラスを拡張する**

   ページと段落システムは、内部コンポーネントへの委任が期待どおりに機能するように、このクラスを拡張する必要があります。

1. **HTML5 `History` API を使用したルーティングソリューションを実装する。**

   `ModelRouter` が有効な場合、`pushState` および `replaceState` 関数を呼び出すと、モデルの欠落したフラグメントを取得するためのリクエストが `PageModelManager` にトリガーされます。

   の現在のバージョン `ModelRouter` は、Sling Model エントリポイントの実際のリソースパスを指す URL のみを使用できます。 バニティ URL やエイリアスの使用はサポートされません。

   `ModelRouter` は、無効にしたり、正規表現のリストを無視するように設定したりできます。

## AEM 非依存 {#aem-agnostic}

これらのコードブロックは、React コンポーネントと Angular コンポーネントが、Adobe や AEM に固有のものを必要としていないことを示してします。

* JavaScript コンポーネント内にあるものはすべて、AEM 非依存です。
* ただし、AEMに特有の点は、JS コンポーネントを MapTo ヘルパーを使用してAEMコンポーネントにマッピングする必要がある点です。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo` ヘルパーは、バックエンドとフロントエンドのコンポーネントを一致させる「接着剤」です。

* これは、JS コンテナ（または JS 段落システム）に、JSON に存在する各コンポーネントのレンダリングは、どの JS コンポーネントが関与するのかを伝えるものです。
* JS コンポーネントでレンダリングされる HTML に HTML データ属性が追加されるので、SPA エディターは、コンポーネントの編集時に作成者に表示するダイアログボックスを把握できます。

`MapTo` の使用法と AEM 向け SPA の構築の概要について詳しくは、選択したフレームワークの概要を参照してください。

* [React を使用した AEM での SPA の概要](/help/sites-developing/spa-getting-started-react.md)
* [AEM での SPA の概要 - Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM のアーキテクチャと SPA {#aem-architecture-and-spas}

開発、オーサリング、公開環境を含む AEM の一般的なアーキテクチャは、SPA を使用する場合でも変更されません。ただし、SPA 開発がこのアーキテクチャにどのように適合しているかを理解することに役立ちます。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **ビルド環境**

  SPAアプリケーションソースとコンポーネントソースのソースは、ここでチェックアウトされます。

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

   * リクエストは、AEMオーサーでの処理と同様に処理されますが、ページ情報のリクエストはありません。ページ情報はエディターでのみ必要とされるからです。
   * JavaScript、CSS、JSON およびHTMLがキャッシュされ、配信が高速になるようにページが最適化されます。

>[!NOTE]
>
>AEM 内では、JavaScript のビルドメカニズムを実行したり、JavaScript 自体を実行したりする必要はありません。AEM は、SPA アプリケーションからコンパイルされたアーティファクトのみをホストします。

## 次の手順 {#next-steps}

AEM でのシンプルな SPA の構造と仕組みの概要については、[React](/help/sites-developing/spa-getting-started-react.md) および [Angular](/help/sites-developing/spa-getting-started-angular.md) 両方の入門ガイドを参照してください。

独自の SPA を作成する手順については、[AEM SPA Editor の使用の手引き - WKND イベントチュートリアル](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)を参照してください。

動的モデルとコンポーネントのマッピング、および AEM の SPA 内での動作について詳しくは、[SPA の動的モデルとコンポーネントのマッピング](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)の記事を参照してください。

AEMに React やAngular以外のフレームワーク用にSPAを実装する場合や、AEM用SPA SDK の仕組みを詳しく知りたい場合は、 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 記事。
