---
title: Adobe Experience Managerタッチ操作対応 UI の概念
description: Adobe Experience Manager 5.6 では、Adobeは、オーサー環境向けのレスポンシブデザインを備えた新しいタッチ操作向け UI を導入しました
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '2147'
ht-degree: 21%

---

# Adobe Experience Managerタッチ操作対応 UI の概念{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager(AEM) には、 [レスポンシブデザイン](/help/sites-authoring/responsive-layout.md) タッチデバイスとデスクトップデバイスの両方で動作するように設計されたオーサー環境向け。

>[!NOTE]
>
>タッチ対応 UI は AEM の標準 UI です。クラシック UI は AEM 6.4 で非推奨となりました。

タッチ対応 UI は以下で構成されます。

* スイートヘッダー：
   * ロゴを表示します
   * グローバルナビゲーションへのリンクを表示します
   * 検索、ヘルプ、Experience Cloudソリューション、通知、ユーザー設定など、他の一般的なアクションへのリンクを提供します。
* 左側のレール（必要に応じて表示／非表示の切り替えが可能）には次を表示できます。
   * タイムライン
   * 参照
   * フィルター
* ナビゲーションヘッダー。コンテキストに応じて、次の情報を表示できます。
   * 現在使用しているコンソール、またはそのコンソール内の場所、またはその両方を示します
   * 左側のパネルの選択
   * パンくずリスト
   * 適切な&#x200B;**作成**&#x200B;アクションへのアクセス
   * 表示の選択状況
* 次のコンテンツ領域：
   * コンテンツの項目（ページ、アセット、フォーラムの投稿など）をリストします。
   * リクエストに応じてフォーマットできます（例：列、カード、リスト）。
   * レスポンシブデザインを使用します（デバイスやウィンドウのサイズに応じて自動的に表示サイズが変更されます）。
   * 無限スクロールを使用します（ページネーションがなくなり、すべての項目が 1 つのウィンドウに表示されます）。

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>ほとんどすべてのAEM機能が、タッチ操作対応 UI に移植されています。 ただし、一部のケースでは、機能がクラシック UI に戻ります。 詳しくは、 [タッチ操作対応 UI 機能のステータス](/help/release-notes/touch-ui-features-status.md) を参照してください。

タッチ操作対応 UI は、複数の製品間でユーザーエクスペリエンスの一貫性を保つために、Adobeが設計しました。 次の項目に基づいています。

* **Coral UI** (CUI) タッチ操作対応 UI 用のAdobeの表示スタイルの実装。 Coral UI は、UI の表示スタイルを採用するために必要な製品/プロジェクト/ Web アプリケーションのあらゆる機能を提供します。
* **Granite UI** コンポーネントは、Coral UI を使用して構築されます。

タッチ操作対応 UI の基本原則は次のとおりです。

* モバイル優先（デスクトップを考慮）
* レスポンシブデザイン
* コンテキスト関連の表示
* 再利用可能
* 埋め込まれたリファレンスドキュメントを含める
* 埋め込みテストを含める
* ボトムアップ設計により、これらの原則がすべての要素およびコンポーネントに確実に適用されます。

タッチ操作対応 UI の構造の詳しい概要については、 [AEMタッチ操作対応 UI の構造](/help/sites-developing/touch-ui-structure.md).

## AEM Technology Stack {#aem-technology-stack}

AEMは Granite プラットフォームをベースとして使用し、Granite プラットフォームには Java™コンテンツリポジトリが含まれます。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite は、Adobeのオープン Web スタックで、次のような様々なコンポーネントを提供します。

* アプリケーションランチャー
* すべてがデプロイされる OSGi フレームワーク
* アプリケーションの構築をサポートする複数の OSGi コンプレディアムサービス
* 様々なログ API を提供する包括的なログフレームワーク
* JCR API 仕様の CRX リポジトリ実装
* Apache Sling Web Framework
* 現在の CRX 製品の追加部分

>[!NOTE]
>
>Granite は、Adobe内でオープンな開発プロジェクトとして運営されています。コード、ディスカッションおよび問題に対する貢献は、会社全体からおこなわれます。
>
>ただし、Granite は **not** オープンソースプロジェクト。 これは、いくつかのオープンソースプロジェクト（特に Apache Sling、Felix、Jackrabbit、Lucene）に大きく基づいていますが、Adobeは、何が公開されているかと内部的なものの間に明確な線を引きます。

## Granite UI {#granite-ui}

Granite エンジニアリングプラットフォームには、基盤 UI フレームワークも用意されています。 主な目標は次のとおりです。

* 詳細な UI ウィジェットを提供します
* UI の概念を実装し、ベストプラクティス（長いリストのレンダリング、リストのフィルタリング、オブジェクト CRUD、CUD ウィザードなど）を説明します。
* 拡張可能なプラグインベースの管理 UI を提供する

これらは要件に従います。

* 「モバイル優先」を尊重
* 拡張可能
* 上書きが簡単

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[ファイルを取得](assets/graniteui.pdf)
Granite UI は次のようになります。

* Sling の RESTful アーキテクチャを使用
* コンテンツ中心の Web アプリケーションの構築を目的としたコンポーネントライブラリを実装します。
* 詳細な UI ウィジェットを提供します
* デフォルトの標準化された UI を提供します。
* 拡張可能
* モバイルとデスクトップの両方のデバイス向けに設計されています（モバイルが優先されます）
* Granite ベースの任意のプラットフォーム/製品/プロジェクト ( 例：AEM) で使用できます。

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI 基盤コンポーネント](#granite-ui-foundation-components)
この基盤コンポーネントライブラリは他のライブラリで使用または拡張できます。
* [Granite UI 管理コンポーネント](#granite-ui-administration-components)

### クライアント側とサーバー側 {#client-side-vs-server-side}

Granite UI のクライアントとサーバーの通信は、オブジェクトではなくハイパーテキストで構成されるので、クライアントがビジネスロジックを理解する必要はありません

* サーバーは、セマンティックデータを使用してHTMLをエンリッチメントします
* クライアントは、ハイパーテキストをハイパーメディア（インタラクション）でエンリッチメントします。

![chlimage_1-83](assets/chlimage_1-83.png)

#### クライアント側 {#client-side}

作成者がインタラクティブな WebHTMLを構築する意向を表現できるよう、アプリケーションの語彙の拡張を使用します。 これは、 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) および [microformats](https://microformats.org/).

主に、クライアント側で実行される JS および CSS コードで解釈されるインタラクションパターンのコレクション（例えば、フォームの非同期送信）で構成されます。 クライアント側の役割は、インタラクティビティのためにマークアップ（サーバーがハイパーメディアアフォーダンスとして提供）を拡張することです。

クライアント側は、どのサーバーテクノロジーとも独立しています。 サーバーが適切なマークアップを提供している限り、クライアント側はその役割を果たすことができます。

現在、JS および CSS コードは Granite として提供されています [clientlibs](/help/sites-developing/clientlibs.md) カテゴリの下：

`granite.ui.foundation and granite.ui.foundation.admin`

これらはコンテンツパッケージの一部として提供されています。

`granite.ui.content`

#### サーバーサイド {#server-side}

sling コンポーネントのコレクションによって形成され、作成者は Web アプリケーションを迅速に構成できるようになります&#x200B;*。*&#x200B;開発者はコンポーネントを開発し、作成者はコンポーネントを Web アプリにアセンブルします。 サーバーサイドの役割は、ハイパーメディアアフォーダンス（マークアップ）をクライアントに提供することです。

現在、コンポーネントは Granite リポジトリ ( ) の次の場所にあります。

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
   <td>状態遷移</td>
  </tr>
  <tr>
   <td>データ転送オブジェクト</td>
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>クライアントはサーバの内部を把握しています</td>
   <td>クライアントは内部を知りません</td>
  </tr>
  <tr>
   <td>"Fat client"</td>
   <td>"シンクライアント"</td>
  </tr>
  <tr>
   <td>専用のクライアントライブラリ</td>
   <td>ユニバーサルクライアントライブラリ</td>
  </tr>
 </tbody>
</table>

### Granite UI 基盤コンポーネント {#granite-ui-foundation-components}

The [Granite UI 基盤コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) は、UI の構築に必要な基本的な構成要素を提供します。 次のようなものが含まれます。

* ボタン
* ハイパーリンク
* ユーザーアバター

基盤コンポーネントは、次の場所にあります。

`/libs/granite/ui/components/foundation`

このライブラリには、各 Coral 要素の Granite UI コンポーネントが含まれています。 コンポーネントはコンテンツ主導で、その設定はリポジトリに配置されます。 これにより、手動でHTMLマークアップを書かずに、Granite UI アプリケーションを作成できます。

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

Granite UI を使用するために ExtJS コードをアップグレードする場合、以下のリストは、ExtJS xtype とノードタイプの、同等の Granite UI リソースタイプの便利な概要を示しています。

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

The [Granite UI 管理コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 基盤コンポーネント上に構築して、任意の管理アプリケーションで実装できる汎用の構築ブロックを提供します。 これには、次のようなものが含まれます。

* グローバルナビゲーションバー
* レール（スケルトン）
* 検索パネル

目的：

* 管理アプリケーションのルックアンドフィールを統合
* 管理アプリケーションのRad

実装：

* 基盤コンポーネントを使用した事前定義済みのコンポーネント
* コンポーネントはカスタマイズ可能

## Coral UI {#coral-ui}

CoralUI.pdf

[ダウンロード](assets/coralui.pdf)
Coral UI(CUI) は、複数の製品間でユーザーエクスペリエンスの一貫性を提供するように設計された、タッチ操作対応 UI 用のAdobeのビジュアルスタイルの実装です。 Coral UI は、オーサリング環境で使用されるビジュアルスタイルを採用するために必要なすべてのものを提供します。

>[!CAUTION]
>
>Coral UI は、AEM のお客様が製品ライセンスの許容範囲内でアプリケーションや web インターフェイスの構築に利用できる UI ライブラリです。
>
>Coral UI は次の場合にのみ使用できます。
>
>
>* AEMに出荷され、バンドルされている場合。
>* オーサリング環境の既存の UI を拡張する際に使用します。
>* アドビの販促品、広告、プレゼンテーション
>* Adobeブランドアプリケーションの UI（他の用途ですぐに使用できるフォントではない）。
>* 小さなカスタマイズがあります。
>
>次の場合は、Coral UI の使用を避ける必要があります。
>
>* Adobeに関係のない書類その他の事項
>* コンテンツ作成環境（前の項目が他のユーザーによって生成される場合があります）。
>* アドビと明確なつながりのないアプリケーション／コンポーネント／web ページ
>

Coral UI は、web アプリケーションを開発するための構成要素のコレクションです。

![chlimage_1-84](assets/chlimage_1-84.png)

最初からモジュール式に設計され、各モジュールは、主な役割に基づいて個別のレイヤーを形成します。 レイヤは互いにサポートするように設計されていますが、必要に応じて個別に使用することもできます。 これにより、あらゆるHTML対応環境に Coral のユーザーエクスペリエンスを実装できます。

Coral UI では、特定の開発モデルやプラットフォームを使用する必要はありません。 Coral の主な目的は、このマークアップの発行に使用される実際の方法とは無関係に、統合されたクリーンなHTML5 マークアップを提供することです。 これは、クライアント側またはサーバ側のレンダリング、テンプレート、JSP、PHP、またはAdobeFlashの RIA アプリケーションに使用されます。

### HTML要素 — マークアップレイヤー {#html-elements-the-markup-layer}

HTML要素は、すべての基本 UI 要素（ナビゲーションバー、ボタン、メニュー、レールなど）に共通のルックアンドフィールを提供します。

最も基本的なレベルでは、HTML要素は、専用のクラス名を持つHTMLタグです。 複数のタグを（特定の方法で）相互にネストし、より複雑な要素を構成することができます。 

CSS は、実際のルックアンドフィールを提供するために使用されます。 ルックアンドフィールを簡単にカスタマイズできるように（例えば、ブランディングの場合）、実際のスタイル値は、 [LESS](https://lesscss.org/) 実行時のプリプロセッサー。

目的：

* 基本的な UI 要素と共通のルックアンドフィールを提供
* デフォルトのグリッドシステムを指定

実装：

* HTMLタグと、 [Bootstrap](https://twitter.github.com/bootstrap/)
* クラスは LESS ファイルで定義されます
* アイコンはフォントスプライトとして定義されます。

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

多くのHTML要素は、ポップアップメニューを開いたり閉じたりするなど、何らかの動的な動作を示す必要があります。 これは要素プラグインの役割で、JavaScript を使用して DOM を操作することでこのようなタスクを実行します。

プラグインは次のいずれかです。

* 特定の DOM 要素を操作するように設計されています。 例えば、ダイアログプラグインは、次を見つける必要があります。 `DIV class=dialog`
* 汎用的なものです。例えば、レイアウトマネージャーは、`DIV` 要素または `LI` 要素のリスト用のレイアウトを提供します。

プラグインの動作は、次のいずれかの方法でパラメーターと共にカスタマイズできます。

* JavaScript 呼び出しでパラメーターを渡す
* HTML マークアップに関連付けられた専用の `data-*` 属性を使用します。

開発者はどのプラグインにも最適なアプローチを選択できますが、経験則では以下のように使用します。

* HTML レイアウトに関連するオプションの `data-*` 属性。例えば、列数を指定します
* データに関連する機能の API オプション/クラス。 例えば、表示する項目のリストを作成する場合などです。

フォームの検証を実装する場合も同じ概念を使用します。要素を検証する場合、必要な入力フォームをカスタムの `data-*` 属性として指定する必要があります。この属性は、検証プラグインのオプションとして使用されます。

>[!NOTE]
>
>HTML5 ネイティブフォームの検証は、可能な場合は常に使用し、拡張する必要があります。

目的：

* HTML要素に動的な動作を提供
* 純粋な CSS では不可能なカスタムレイアウトの提供
* フォームの検証を実行
* 高度な DOM 操作の実行

実装：

* 特定の DOM 要素に結び付けられた jQuery プラグイン
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

The `cardLayout` プラグインは、閉じた `UL` それぞれの高さに基づく要素と、親の幅も考慮に入れた要素。

### HTML 要素ウィジェット {#html-elements-widgets}

ウィジェットは、1 つ以上の基本要素を JavaScript プラグインと組み合わせて「上位」の UI 要素を形成します。 これらは、より複雑な動作を実装し、また、単一の要素が提供する以上に複雑なルックアンドフィールを実装できます。 好例は、タグピッカーやパネルウィジェットです。

ウィジェットは、トリガーとカスタムイベントをリッスンの両方を行って、ページ上の他のウィジェットと連携することができます。 一部のウィジェットは、Coral ウィジェット要素を使用するネイティブ jQueryHTMLです。

目的：

* 複雑な動作を示す高レベルの UI 要素の実装
* イベントのトリガーと処理

実装：

* jQuery プラグイン+HTMLマークアップ
* クライアント/サーバー側のテンプレートを使用できます。

マークアップの例を次に示します。

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

jQuery プラグインの呼び出し（オプションを含む）:

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

プラグインはHTMLマークアップを発行します（このマークアップは基本要素を使用し、内部で他のプラグインを使用する場合があります）。

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
* 完全な機能を備えた Web アプリケーションの構築にとって非常に重要です。

これには、XSS の処理やイベントバスが含まれます。

HTML要素のプラグインとウィジェットは、ユーティリティライブラリが提供する機能に依存する場合がありますが、ユーティリティライブラリは、要素やウィジェット自体に強く依存することはできません。

目的：

* 共通の機能を提供
* イベントバスの実装
* クライアント側テンプレート
* XSS

実装：

* jQuery プラグインまたは AMD 準拠の JavaScript モジュール
