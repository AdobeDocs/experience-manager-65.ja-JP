---
title: AEM用SPAの開発
seo-title: AEM用SPAの開発
description: この記事では、フロントエンド開発者がAEM用のSPAを開発する際に考慮すべき重要な質問と、開発済みのSPAをAEMにデプロイする際に考慮すべきSPAに関するAEMのアーキテクチャの概要を説明します。
seo-description: この記事では、フロントエンド開発者がAEM用のSPAを開発する際に考慮すべき重要な質問と、開発済みのSPAをAEMにデプロイする際に考慮すべきSPAに関するAEMのアーキテクチャの概要を説明します。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# AEM用SPAの開発{#developing-spas-for-aem}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

この記事では、フロントエンド開発者がAEM用のSPAを開発する際に考慮すべき重要な質問を紹介し、AEMへのSPAのデプロイに関するAEMのアーキテクチャの概要を説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## AEMのSPA開発原則 {#spa-development-principles-for-aem}

AEMでシングルページアプリケーションを開発する場合、フロントエンド開発者がSPAを作成する際に標準的なベストプラクティスを遵守することを前提としています。 フロントエンド開発者が、AEM固有の原則に加えて、これらの一般的なベストプラクティスに従う場合、SPAは [AEMとそのコンテンツオーサリング機能と連携します](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)。

* **[移植性](/help/sites-developing/spa-architecture.md#portability)-**任意のコンポーネントと同様に、コンポーネントは可搬性を可能な限り高めるように構築する必要があります。 SPAは、ポータブルで再利用可能なコンポーネントを使用して構築する必要があります。
* **[AEM Drivesサイト構造](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**— フロントエンド開発者はコンポーネントを作成し、内部構造を所有しますが、サイトのコンテンツ構造の定義はAEMに依存しています。
* **[ダイナミックレンダリング](/help/sites-developing/spa-architecture.md#dynamic-rendering)**— すべてのレンダリングはダイナミックである必要があります。
* **[動的ルーティング](#dynamic-routing)-**SPAがルーティングを担当し、AEMはルーティングをリッスンし、それに基づいて取得します。 ルーティングも動的に行う必要があります。

SPAの開発時にこれらの原則を念頭に置いておくと、サポートされるすべてのAEMオーサリング機能を有効にしながら、できる限り柔軟で将来の証拠となります。

AEMオーサリング機能をサポートする必要がない場合は、別の [SPAデザインモデルを検討する必要がある場合があります](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 移植性 {#portability}

コンポーネントを開発する場合と同様に、コンポーネントは移植性を最大限に高めるように設計する必要があります。 コンポーネントの移植性や再利用性に反して機能するパターンは、互換性、柔軟性、保守性を確保するために避ける必要があります。

作成されるSPAは、高度にポータブルで再利用可能なコンポーネントを使用して構築する必要があります。

### AEMドライブのサイト構造 {#aem-drives-site-structure}

フロントエンド開発者は、自分自身が、アプリの作成に使用されるSPAコンポーネントのライブラリの作成を担当していると考える必要があります。 フロントエンド開発者は、コンポーネントの内部構造を完全に制御できます。 [ただし、AEMは常にサイトの構造を所有しています。](/help/sites-developing/spa-overview.md)

つまり、フロントエンド開発者は、コンポーネントのエントリポイントの前後に顧客コンテンツを追加でき、また、コンポーネント内でサードパーティの呼び出しを行うこともできます。 ただし、フロントエンド開発者は、例えばコンポーネントのネストの方法を完全に制御するわけではありません。

### ダイナミックレンダリング {#dynamic-rendering}

SPAは、コンテンツの動的レンダリングのみに依存する必要があります。 これは、AEMがコンテンツ構造のすべての子を取得してレンダリングするデフォルトの期待値です。 [](/help/sites-developing/spa-architecture.md#portability)

特定のコンテンツを指す明示的なレンダリングは静的レンダリングと見なされ、サポートされていますが、AEMのコンテンツオーサリング機能との互換性はありません。 これは移植性の原則にも反 [する](/help/sites-developing/spa-architecture.md#portability)。

### 動的ルーティング {#dynamic-routing}

レンダリングと同様に、すべてのルーティングも動的である必要があります。 AEMでは、SPAが常にル [ーティングを所有し、AEMは](/help/sites-developing/spa-routing.md) SPAをリッスンし、それに基づいてコンテンツを取得します。

スタティックルーティングは移植性の原 [則に反し](/help/sites-developing/spa-architecture.md#portability) 、AEMのコンテンツオーサリング機能と互換性がないので作成者が制限されます。 例えば、静的ルーティングの場合、コンテンツ作成者がルートを変更したりページを変更したりする場合は、フロントエンド開発者に依頼する必要があります。

## SPAスターターキット用Mavenアーキタイプ {#maven-archetype-for-spa-starter-kit}

AEM用の独自のSPAプロジェクトを開始する際に役立つよう [](https://github.com/adobe/aem-spa-project-archetype) に、SPAスターターキット用のMavenアーキタイプの活用をお勧めします。

## SPA設計モデル {#spa-design-models}

AEMでのSPAの開 [発の原則に従うと、AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) SPAは、サポートされるすべてのAEMコンテンツオーサリング機能で機能します。 [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

しかし、これが完全に必要でない場合もある。 次の表に、様々なデザインモデル、その利点および欠点の概要を示します。

<table>
 <tbody>
  <tr>
   <th><strong>デザインモデル<br /> </strong></th>
   <th><strong>メリット</strong></th>
   <th><strong>デメリット</strong></th>
  </tr>
  <tr>
   <td>AEMは、 <a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDKフレームワークを使用せずに、ヘッドレスCMSとして使用されます。</a></td>
   <td>フロントエンド開発者は、アプリを完全に制御できます。</td>
   <td><p>コンテンツ作成者はAEMのコンテンツオーサリングエクスペリエンスを活用できません。</p> <p>コードに静的参照またはルーティングが含まれる場合、コードはポータブルでも再利用でもありません。</p> <p>テンプレートエディターの使用を許可しないので、フロントエンド開発者はJCRを使用して編集可能なテンプレートを維持する必要があります。</p> </td>
  </tr>
  <tr>
   <td>フロントエンド開発者はSPA Editor SDKフレームワークを使用しますが、コンテンツ作成者が開く領域は一部のみです。</td>
   <td>開発者は、アプリの制限された領域でのみオーサリングを有効にすることで、アプリを管理し続けます。</td>
   <td><p>コンテンツ作成者は、AEMのコンテンツオーサリングエクスペリエンスの制限を受けます。</p> <p>コードに静的参照またはルーティングが含まれる場合、コードは移植性も再利用性も損なわれる可能性があります。</p> <p>テンプレートエディターの使用を許可しないので、フロントエンド開発者はJCRを使用して編集可能なテンプレートを維持する必要があります。</p> </td>
  </tr>
  <tr>
   <td>このプロジェクトはSPAエディターSDKを完全に活用し、フロントエンドコンポーネントはライブラリとして開発され、アプリのコンテンツ構造はAEMに委任されます。</td>
   <td><p>アプリは再利用可能でポータブルです。</p> <p>コンテンツ作成者は、AEMのコンテンツオーサリングエクスペリエンスを使用してアプリを編集できます。<br /> </p> <p>SPAはテンプレートエディターと互換性があります。</p> </td>
   <td><p>開発者は、アプリの構造とAEMに委任されたコンテンツの一部を管理していません。</p> <p>開発者は、AEMを使用して作成する予定ではないコンテンツ用にアプリの領域を予約できます。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>すべてのモデルがAEMでサポートされていますが、3番目の実装(その結果、AEM [で推奨される](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)SPA開発原則に従う)によってのみ、コンテンツ作成者は、AEM内のSPAのコンテンツを慣れ親しんだとおりに操作し、編集できます。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 既存のSPAのAEMへの移行 {#migrating-existing-spas-to-aem}

一般に、SPAがAEMの [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)SPA開発原則に従う場合、SPAはAEMで動作し、AEM SPAエディターを使用して編集できます。

既存のSPAをAEMで使用する準備を整えるには、次の手順に従います。

1. **JSコンポーネントをモジュール化します。**

   任意の順序、位置、サイズでレンダリングできるようにします。
1. **SDKが提供するコンテナを使用して、コンポーネントを画面に配置します。**

   AEMは、使用するページと段落のシステムコンポーネントを提供します。
1. **JSコンポーネントごとにAEMコンポーネントを作成します。**

   AEMコンポーネントは、ダイアログとJSON出力を定義します。

## フロントエンド開発者向けの手順 {#instructions-for-front-end-developers}

フロントエンド開発者にAEM用のSPAを作成するように促す主な作業は、コンポーネントとそのJSONモデルに同意することです。

AEM用のSPAを開発する際にフロントエンド開発者が実行する必要がある手順の概要を以下に示します。

1. **コンポーネントとそのJSONモデルに同意する**

   フロントエンド開発者とバックエンドAEM開発者は、必要なコンポーネントとモデルについて合意し、SPAコンポーネントからバックエンドコンポーネントに1対1の一致を持たせる必要があります。

   AEMコンポーネントは、編集ダイアログを提供し、コンポーネントモデルを書き出すためには、ほとんど必要です。

1. **Reactコンポーネントで、`this.props.cqModel`**

   コンポーネントが合意され、JSONモデルが導入されると、フロントエンド開発者はSPAを自由に開発でき、JSONモデルにはを介してアクセスできま `this.props.cqModel`す。

1. **コンポーネントのメソッドの実`render()`装**

   フロントエンド開発者は、このメソッド `render()` を適切に実装し、プロパティのフィールドを使用で `cqModel` きます。 これにより、ページに挿入されるDOMとHTMLフラグメントが出力されます。 これは、Reactでアプリを作成する標準的な方法です。

1. **コンポーネントをAEMリソースタイプにマップするには、`MapTo()`**

   マッピングはコンポーネントクラスを格納し、指定されたコンポーネントによって内部的に使用さ `Container` れ、指定されたリソースタイプに基づいてコンポーネントを取得し、動的にインスタンス化します。

   これはフロントエンドとバックエンドの間の「接着」の役割を果たすので、エディタは、コンポーネントがどのコンポーネントに対応するかを知ることができます。

   とは、 `Page` ベー `ResponsiveGrid` スを拡張するクラスの良い例で `Container`す。

1. **コンポーネントのパラメー`EditConfig`ターを`MapTo()`**

   このパラメーターは、レンダリングが行われないか、レンダリングするコンテンツがない場合に、コンポーネントに名前を付ける必要がある方法をエディターに伝えるために必要です。

1. **提供されたページおよび`Container`コンテナのクラスの拡張**

   ページと段落システムは、内部コンポーネントへの委任が期待どおりに機能するように、このクラスを拡張する必要があります。

1. **HTML5`History`APIを使用するルーティングソリューションを実装します。**

   が有効な場 `ModelRouter` 合、および関数を呼び出 `pushState` すと、モデ `replaceState` ルの見つからないフラグメントを取 `PageModelManager` 得する要求がにトリガされます。

   現在のバージョンのみ `ModelRouter` で、Sling modelエントリポイントの実際のリソースパスを指すURLの使用がサポートされています。 バニティURLやエイリアスの使用はサポートされません。

   を無 `ModelRouter` 効にしたり、正規表現のリストを無視するように設定したりできます。

## AEMにとらわれない {#aem-agnostic}

これらのコードブロックは、ReactコンポーネントとAngularコンポーネントがAdobeやAEMに固有の何も必要としないことを示します。

* JavaScriptコンポーネント内にあるものはすべてAEMに依存しません。
* ただし、AEMに固有の点は、JSコンポーネントをMapToヘルパーを使用してAEMコンポーネントにマップする必要があることです。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

ヘルパー `MapTo` とは、バックエンドとフロントエンドのコンポーネントを一致させる「接着剤」です。

* JSコンテナ（またはJS段落システム）に、JSONに存在する各コンポーネントのレンダリングを担当するJSコンポーネントを伝えます。
* JSコンポーネントがレンダリングするHTMLにHTMLデータ属性が追加され、SPAエディターは、コンポーネントの編集時に作成者に表示するダイアログを知ることができます。

AEM用SPAの一般的な使用と構 `MapTo` 築について詳しくは、選択したフレームワークの「はじめに」ガイドを参照してください。

* [AEMのSPA使用の手引き — React](/help/sites-developing/spa-getting-started-react.md)
* [AEMのSPA使用の手引き — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEMアーキテクチャとSPA {#aem-architecture-and-spas}

SPAを使用する場合、開発環境、オーサリング環境、パブリッシング環境を含むAEMの一般的なアーキテクチャは変更されません。 ただし、SPA開発がこのアーキテクチャにどのように適合するかを理解すると役立ちます。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **ビルド環境**

   ここで、SPAアプリケーションソースとコンポーネントソースのソースがチェックアウトされます。

   * NPM clientlibジェネレーターは、SPAプロジェクトからクライアントライブラリを作成します。
   * このライブラリはMavenによって取得され、Maven BuildプラグインによってAEM Authorのコンポーネントと共にデプロイされます。

* **AEM 作成者**

   コンテンツは、オーサリングSPAを含め、AEM作成者によって作成されます。

   オーサリング環境でSPAエディタを使用してSPAを編集する場合：

   1. SPAは外部HTMLを要求します。
   1. CSSが読み込まれます。
   1. SPAアプリケーションのJavaScriptが読み込まれます。
   1. SPAアプリケーションが実行されると、JSONが要求され、アプリケーションは属性を含むページのDOMを構築でき `cq-data` ます。
   1. この属 `cq-data` 性を使用すると、エディターで追加のページ情報を読み込んで、コンポーネントで使用できる編集設定を把握できます。

* **AEM Publish**

   ここで、SPAアプリケーションアーティファクト、clientlib、コンポーネントを含むオーサリング済みのコンテンツとコンパイル済みのライブラリが、一般消費用に公開されます。

* **ディスパッチャー/CDN**

   ディスパッチャーは、サイトへの訪問者のAEMのキャッシュ層の役割を果たします。

   * リクエストはAEM Authorでの処理と同様に処理されますが、ページ情報のリクエストはありません。これは、エディターが必要とするのはこの操作のみです。
   * JavaScript、CSS、JSONおよびHTMLがキャッシュされ、高速配信のためにページが最適化されます。

>[!NOTE]
>
>AEM内でJavaScriptビルドメカニズムを実行したり、JavaScript自体を実行したりする必要はありません。 AEMは、SPAアプリケーションからコンパイルされたアーティファクトのみをホストします。

## 次の手順 {#next-steps}

AEMのシンプルなSPAの構造とその仕組みの概要については、 [React](/help/sites-developing/spa-getting-started-react.md) と [Angularの両方の使用の手引きガイドを参照してください](/help/sites-developing/spa-getting-started-angular.md)。

独自のSPAを作成する手順ガイドについては、『AEM SPA Editor - WKND Events Tutorial [Getting Started with the AEM SPA Editor - WKND Events Tutorial』を参照してください](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

動的モデルとコンポーネントのマッピング、およびAEMのSPA内での動的モデルとコンポーネントのマッピングについて詳しくは、SPAの動的モデルとコンポ [ーネントのマッピングを参照してください](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

AEMにReactやAngular以外のフレームワーク用のSPAを実装する場合や、単にAEM用SPA SDKの仕組みを詳しく調べたい場合は、 [SPA Blueprintの記事を参照してください](/help/sites-developing/spa-blueprint.md) 。
