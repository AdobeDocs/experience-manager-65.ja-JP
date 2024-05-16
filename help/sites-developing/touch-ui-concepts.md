---
title: Adobe Experience Manager タッチ操作対応 UI の概念
description: アドビは、Adobe Experience Manager 5.6 で、レスポンシブデザインを採用した新しいタッチ操作対応 UI をオーサー環境に導入しました。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '2147'
ht-degree: 100%

---

# Adobe Experience Manager タッチ操作対応 UI の概念{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager（AEM）は、タッチデバイスとデスクトップデバイスの両方で動作するように設計されたオーサー環境向けに、[レスポンシブデザイン](/help/sites-authoring/responsive-layout.md)を採用したタッチ操作対応 UI を備えています。

>[!NOTE]
>
>タッチ対応 UI は AEM の標準 UI です。クラシック UI は AEM 6.4 で非推奨となりました。

タッチ対応 UI は以下で構成されます。

* スイートヘッダー：
   * ロゴを表示します
   * グローバルナビゲーションへのリンクを表示します
   * 検索、ヘルプ、Experience Cloud ソリューション、通知、ユーザー設定など、その他の汎用アクションへのリンクを表示します。
* 左側のレール（必要に応じて表示／非表示の切り替えが可能）には次を表示できます。
   * タイムライン
   * 参照
   * フィルター
* ナビゲーションヘッダー：コンテキストに応じて、次を表示できます。
   * 現在使用しているコンソールやそのコンソール内の場所、または両方
   * 左側のパネルの選択内容
   * パンくずリスト
   * 適切な&#x200B;**作成**&#x200B;アクションへのアクセス
   * 表示の選択状況
* 次の特長を持つコンテンツ領域：
   * コンテンツの項目（ページ、アセット、フォーラム投稿など）をリストします。
   * 必要に応じて形式（コラム、カードまたはリストなど）を指定できます。
   * レスポンシブデザインを使用します（デバイスやウィンドウのサイズに応じて自動的に表示サイズが変更されます）。
   * 無限スクロールを使用します（ページネーションがなく、すべての項目が 1 つのウィンドウに表示されます）。

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>ほとんどすべての AEM 機能がタッチ操作対応 UI に移植されています。ただし、一部の限られたケースでは、機能がクラシック UI に戻ります。詳しくは、[タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md)を参照してください。

タッチ操作対応 UI は、複数の製品間で一貫性のあるユーザーエクスペリエンスを提供するように設計されています。次をベースとしています。

* **Coral UI**（CUI）は、アドビのタッチ操作対応 UI 用のビジュアルスタイル実装です。Coral UI は、製品／プロジェクト／web アプリケーションで UI のビジュアルスタイルを採用するうえで必要となるすべてのものを備えています。
* **Granite UI** コンポーネントは、Coral UI を使用して作成されています。

タッチ操作対応 UI の基本原則は次のとおりです。

* モバイル優先（デスクトップを念頭に置きながら）
* レスポンシブデザイン
* コンテキストに適した表示
* 再利用可能
* 組み込みのリファレンスドキュメント
* 組み込みのテスト
* ボトムアップ設計（これらの原則がすべての要素およびコンポーネントに確実に適用されます）

タッチ操作対応 UI の構造の概要について詳しくは、[AEM タッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md)を参照してください。

## AEM テクノロジースタック {#aem-technology-stack}

AEM がベースとして使用する Granite プラットフォームには、特に Java™ コンテンツリポジトリが含まれます。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite は、アドビのオープン web スタックで、次のような様々なコンポーネントを提供します。

* アプリケーションランチャー
* すべてがデプロイされる OSGi フレームワーク
* アプリケーションの構築をサポートする複数の OSGi 簡易サービス
* 様々なログ API を提供する包括的なログフレームワーク
* JCR API 仕様の CRX リポジトリ実装
* Apache Sling web フレームワーク
* 現在の CRX 製品の追加要素

>[!NOTE]
>
>Granite は、アドビ内でオープンな開発プロジェクトとして進められています。コード、ディスカッションおよび問題に会社全体が関与しています。
>
>ただし、Granite はオープンソースプロジェクトでは&#x200B;**ありません**。いくつかのオープンソースプロジェクト（特に Apache Sling、Felix、Jackrabbit および Lucene）を重要なベースとしていますが、アドビは公開部分と非公開部分を明確に区別しています。

## Granite UI {#granite-ui}

Granite エンジニアリングプラットフォームには、基盤 UI フレームワークも用意されています。主な目的は次のとおりです。

* 詳細な UI ウィジェットの提供
* UI の概念を実装し、ベストプラクティス（長いリストのレンダリング、リストのフィルタリング、オブジェクト CRUD、CUD ウィザードなど）を説明します。
* 拡張可能なプラグインベースの管理 UI の提供

これらは次の要件に準拠しています。

* 「モバイル優先」を重視
* 拡張可能
* 上書きが簡単

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[ファイルを取得](assets/graniteui.pdf)
Granite UI は次のようになります。

* Sling の RESTful アーキテクチャを使用
* コンテンツ中心の web アプリケーションの構築を目的としたコンポーネントライブラリを実装
* 詳細な UI ウィジェットの提供
* デフォルトの標準化された UI を提供
* 拡張可能
* モバイルデバイスとデスクトップデバイスの両方に対応（モバイル優先）
* Granite ベースのすべてのプラットフォーム／製品／プロジェクト（AEM など）で使用

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI 基盤コンポーネント](#granite-ui-foundation-components)
この基盤コンポーネントライブラリは他のライブラリで使用または拡張できます。
* [Granite UI 管理コンポーネント](#granite-ui-administration-components)

### クライアントサイドとサーバーサイド {#client-side-vs-server-side}

Granite UI でのクライアントとサーバーの通信は、オブジェクトではなく、ハイパーテキストで行われるので、クライアントでビジネスロジックを認識する必要はありません。

* サーバーは HTML をセマンティックデータで強化
* クライアントはハイパーテキストをハイパーメディア（インタラクション）で強化

![chlimage_1-83](assets/chlimage_1-83.png)

#### クライアント側 {#client-side}

HTML ボキャブラリの拡張が使用され、作成者はインタラクティブな web アプリケーションを構築するという意向を表明できるようになります。これは、[WAI-ARIA](https://www.w3.org/TR/wai-aria/) および [microformats](https://microformats.org/) と同様のアプローチです。

主に、クライアントサイドで実行される JS および CSS コードによって解釈されるインタラクションパターンのコレクション（例えば、フォームの非同期送信）で構成されます。クライアントサイドの役割は、（サーバーによってハイパーメディアアフォーダンスとして指定された）マークアップを拡張してインタラクティブ機能を持たせることです。

クライアントサイドは、どのサーバーテクノロジーとも無関係です。サーバーが適切なマークアップを提供している限り、クライアントサイドはその役割を果たすことができます。

現在、JS および CSS コードは、Granite [clientlibs](/help/sites-developing/clientlibs.md) として、次のカテゴリで提供されています。

`granite.ui.foundation and granite.ui.foundation.admin`

これらはコンテンツパッケージの一部として提供されています。

`granite.ui.content`

#### サーバーサイド {#server-side}

sling コンポーネントのコレクションによって形成され、作成者は Web アプリケーションを迅速に構成できるようになります&#x200B;*。*&#x200B;開発者はコンポーネントを開発し、作成者はコンポーネントを組み立てて web アプリを作成します。サーバーサイドの役割は、ハイパーメディアアフォーダンス（マークアップ）をクライアントに提供することです。

現在、コンポーネントは Granite リポジトリの次の場所にあります。

`/libs/granite/ui/components/foundation`

これはコンテンツパッケージの一部として提供されています。

`granite.ui.content`

### クラシック UI との違い {#differences-with-the-classic-ui}

Granite UI と ExtJS（クラシック UI に使用）の違いも重要です。

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>リモート手続き呼び出し<br /> </td>
   <td>ステートのトランジション</td>
  </tr>
  <tr>
   <td>データ移行オブジェクト</td>
   <td>ハイパーメディア</td>
  </tr>
  <tr>
   <td>クライアントはサーバの内部を把握しています</td>
   <td>クライアントは内部を把握していません</td>
  </tr>
  <tr>
   <td>「ファットクライアント」</td>
   <td>「シンクライアント」</td>
  </tr>
  <tr>
   <td>専用クライアントライブラリ</td>
   <td>ユニバーサルクライアントライブラリ</td>
  </tr>
 </tbody>
</table>

### Granite UI 基盤コンポーネント {#granite-ui-foundation-components}

[Granite UI 基盤コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)は、UI の構築に必要な基本的な構築ブロックを提供します。次に例を示します。

* ボタン
* ハイパーリンク
* ユーザーアバター

基盤コンポーネントは次の場所にあります。

`/libs/granite/ui/components/foundation`

このライブラリには、各 Coral 要素の Granite UI コンポーネントが含まれます。コンポーネントはコンテンツ主導で、その設定はリポジトリに保持されます。これにより、HTML マークアップを手動で記述しなくても、Granite UI アプリケーションを構成できます。

目的：

* HTML 要素のコンポーネントモデル
* コンポーネントの構成
* 自動単体および機能テスト

実装：

* リポジトリベースの構成と設定
* Granite プラットフォームが提供するテスト機能の使用
* JSP テンプレート

この基盤コンポーネントライブラリは他のライブラリで使用または拡張できます。

### ExtJS と対応する Granite UI コンポーネント {#extjs-and-corresponding-granite-ui-components}

Granite UI を使用するように ExtJS コードをアップグレードする際は、次のリストでは、ExtJS xtype およびノードタイプと、それぞれに対応する Granite UI のリソースタイプを確認できます。

| **ExtJS xtype** | **Granite UI のリソースタイプ** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **ノードタイプ** | **Granite UI のリソースタイプ** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Granite UI 管理コンポーネント {#granite-ui-administration-components}

[Granite UI 管理コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)は、基盤コンポーネントをベースに構築され、あらゆる管理アプリケーションが実装できる汎用構築ブロックを提供します。次に例を示します。

* グローバルナビゲーションバー
* パネル（スケルトン）
* 検索パネル

目的：

* 管理アプリケーションの統一されたルックアンドフィール
* 管理アプリケーション向けの Rad

実装：

* 基盤コンポーネントを使用した事前定義済みのコンポーネント
* カスタマイズ可能なコンポーネント

## Coral UI {#coral-ui}

CoralUI.pdf

[ファイルを取得](assets/coralui.pdf)
Coral UI（CUI）は、アドビのタッチ操作対応 UI 用のビジュアルスタイルを実装したものです。複数の製品間で一貫性のあるユーザーエクスペリエンスを提供するように設計されています。Coral UI は、オーサリング環境で使用されるビジュアルスタイルを採用するのに必要なものをすべて備えています。

>[!CAUTION]
>
>Coral UI は、AEM のお客様が製品ライセンスの許容範囲内でアプリケーションや web インターフェイスの構築に利用できる UI ライブラリです。
>
>Coral UI は次の場合にのみ使用できます。
>
>
>* AEM にバンドルされて出荷された場合。
>* オーサリング環境の既存の UI を拡張する際に使用する場合。
>* アドビの販促品、広告、プレゼンテーション
>* アドビブランドアプリケーションの UI（フォントは他の用途にすぐに利用できないようにする必要があります）。
>* わずかにカスタマイズされている場合。
>
>次の場合は、Coral UI の使用は避けてください。
>
>* アドビに関係しないドキュメントやその他の項目。
>* コンテンツ作成環境（前述の項目が他者によって生成される可能性がある場合）。
>* アドビと明確なつながりのないアプリケーション／コンポーネント／web ページ
>

Coral UI は、web アプリケーションを開発するための構成要素のコレクションです。

![chlimage_1-84](assets/chlimage_1-84.png)

最初からモジュール式に設計され、各モジュールは、主な役割に基づいて個別のレイヤーを形成します。レイヤーは相互にサポートするように設計されていますが、必要に応じて単独で使用することもできます。これにより、あらゆる HTML 対応環境で Coral のユーザーエクスペリエンスを実装できます。

Coral UI では、特定の開発モデルやプラットフォームを使用することは必須ではありません。Coral の主な目的は、統一されたクリーンな HTML5 マークアップを提供することにあり、このマークアップを実際に生成する方法は関係しません。これは、クライアントサイドまたはサーバサイドのレンダリング、テンプレート、JSP、PHP、さらには Adobe Flash RIA アプリケーションなどに使用される場合があります。

### HTML 要素 - マークアップレイヤー {#html-elements-the-markup-layer}

HTML 要素は、すべての基本 UI 要素（ナビゲーションバー、ボタン、メニュー、パネルなど）に共通のルックアンドフィールを提供します。

最も基本的なレベルの HTML 要素は、専用のクラス名を持つ HTML タグです。より複雑な要素は、（特定の方法で）相互にネストされた複数のタグで構成できます。

CSS を使用して、実際のルックアンドフィールを指定します。ルックアンドフィールを簡単にカスタマイズできるように（ブランド設定を行う場合など）、実際のスタイル値は、実行時に [LESS](https://lesscss.org/) プリプロセッサーによって展開される変数として宣言します。

目的：

* 共通のルックアンドフィールを備えた基本的な UI 要素を提供
* デフォルトのグリッドシステムを提供

実装：

* [Bootstrap](https://twitter.github.com/bootstrap/) からアイデアを得たスタイルの HTML タグ
* クラスは LESS ファイルで定義
* アイコンはフォントスプライトとして定義

例えば、マークアップは次のようになります。

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

このマークアップは次のように表示されます。

![chlimage_1-85](assets/chlimage_1-85.png)

ルックアンドフィールは LESS で定義し、専用のクラス名によって要素に関連付けます（次の抜粋は短縮され、簡潔に示されています）。

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

実際の値は LESS 変数ファイルで定義します（次の抜粋は短縮され、簡潔に示されています）。

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 要素プラグイン {#element-plugins}

HTML 要素の多くは、ポップアップメニューの表示／非表示など、何らかの動的動作を示す必要があります。要素プラグインがこの役割を担い、JavaScript を使用して DOM を操作することで、このようなタスクを実行します。

プラグインは次のいずれかです。

* 特定の DOM 要素を動作するように設計されています。例えば、ダイアログプラグインは、`DIV class=dialog` を見つけます。
* 汎用的なものです。例えば、レイアウトマネージャーは、`DIV` 要素または `LI` 要素のリスト用のレイアウトを提供します。

プラグインの動作は、次のいずれかの方法でパラメーターを使用してカスタマイズできます。

* JavaScript 呼び出しでパラメーターを渡す
* HTML マークアップに関連付けられた専用の `data-*` 属性を使用します。

開発者はどのプラグインにも最適なアプローチを選択できますが、経験則では以下のように使用します。

* HTML レイアウトに関連するオプションの `data-*` 属性。例えば、列数を指定します
* データに関連する機能の API オプション／クラス。例えば、表示する項目のリストを作成する場合などです。

フォームの検証を実装する場合も同じ概念を使用します。要素を検証する場合、必要な入力フォームをカスタムの `data-*` 属性として指定する必要があります。この属性は、検証プラグインのオプションとして使用されます。

>[!NOTE]
>
>HTML5 固有のフォーム検証をできるだけ使用するか、場合によってはそれを拡張する必要があります。

目的：

* HTML 要素の動的動作を提供
* 純粋な CSS では実現できないカスタムレイアウトを提供
* フォーム検証を実行
* 高度な DOM 操作を実行

実装：

* 特定の DOM 要素に関連付けられた jQuery プラグイン
* `data-*` 属性を使用した動作のカスタマイズ

次にマークアップの例の抜粋を示します（data-&#42; 属性として指定されたオプションに注意）。

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

次に jQuery プラグインの呼び出しを示します。

```
$('.cards').cardlayout ();
```

これは次のように表示されます。

![chlimage_1-86](assets/chlimage_1-86.png)

`cardLayout` プラグインでは、囲まれた `UL` 要素のレイアウトを決定する際、それぞれの高さを基準とし、さらに親の幅を考慮します。

### HTML 要素ウィジェット {#html-elements-widgets}

ウィジェットでは、1 つ以上の基本要素を JavaScript プラグインと組み合わせて「上位」の UI 要素を形成します。これにより、単一要素の場合と比較して、より複雑な動作と、より複雑なルックアンドフィールを実装できます。タグピッカーやパネルウィジェットがよい例です。

ウィジェットは、カスタムイベントのトリガーとリッスンの両方を行って、ページ上の他のウィジェットと連携できます。一部のウィジェットは、Coral HTML 要素を使用するネイティブ jQuery ウィジェットです。

目的：

* 複雑な動作を示す上位 UI 要素の実装
* イベントのトリガーと処理

実装：

* jQuery プラグイン + HTML マークアップ
* クライアント／サーバーサイドのテンプレートを使用可能

マークアップの例を次に示します。

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

jQuery プラグインの呼び出し（オプション指定あり）を次に示します。

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

プラグインは HTML マークアップを発行します（このマークアップでは、他のプラグインを内部で使用する基本要素を使用しています）。

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

これは次のように表示されます。

![chlimage_1-87](assets/chlimage_1-87.png)

### ユーティリティライブラリ {#utility-library}

このライブラリは、次のような JavaScript ヘルパープラグインや関数のコレクションです。

* UI に依存しない
* それでも、フル機能の web アプリケーションの構築に不可欠

これには、XSS の処理やイベントバスが含まれます。

HTML 要素のプラグインおよびウィジェットは、ユーティリティライブラリが提供する機能に依存する場合がありますが、ユーティリティライブラリは、要素やウィジェット自体に強く依存できません。

目的：

* 共通の機能を提供
* イベントバスの実装
* クライアントサイドテンプレート
* XSS

実装：

* jQuery プラグインまたは AMD 準拠の JavaScript モジュール
