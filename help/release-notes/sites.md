---
title: AEM Sites リリースノート
description: Adobe Experience Manager 6.4 Sites 固有のリリースノート
uuid: 676ead61-3d97-4f23-b616-c647d590bc8f
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: f82e9bd4-f7b6-492d-8e02-593e74fa1058
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# AEM Sites リリースノート{#aem-sites-release-notes}

AEM Sites 6.5 の機能強化について詳しくは、以下を参照してください。

## コンポーネントとテンプレートの開発 {#component-amp-template-development}

* 新規プロジェクト用の Maven プロジェクトアーキタイプ 18 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases) を参照）。
* 新規プロジェクト用の単一ページアプリ Maven プロジェクトアーキタイプ 1.0.6 以上（[リリースノートの GitHub](https://github.com/adobe/aem-spa-project-archetype/releases) を参照）。
* HTL バージョン 1.4（[リリースノートの GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4) を参照）。

   * 文字列、配列、オブジェクトの&quot;in&quot;演算子：

      ```
      ${'a' in 'abc’}
       ${100 in myArray}
       ${'a' in myObject}
      ```

   * 変数宣言のデータスリルセット：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 制御パラメーターのリストと繰り返し：begin, step, end:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * データに対する非ラップの識別子：

      ```
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
       text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
       </div>
      ```

   * 負の数のサポート

* コアコンポーネント 2.3.2 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照）。
* レイアウトコンテナのグリッドシステム（[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照）。
* Clientlibマネージャ：google Closure CompilerをデフォルトでJavaScript clientlibsの縮小（旧デフォルトはYahoo YUI）に設定し、Google Closure Compilerをバージョンv20190121に更新
* テンプレートエディターとポリシー

   * JS SDK（別名SPAエディター）を使用するシングルページアプリ用のテンプレートの作成と編集

* 参照サイト We.Retail 4.0（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照）。
* Toolkit to upgrade existing sites to leverage the latest editor capabilities, see [Github repository](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEMには、既存のカスタムコードとの互換性を最大限に保つために、jQueryライブラリのバージョン1.12.4が含まれています。 セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

## サイト管理 {#site-administration}

* [参照](/help/sites-authoring/author-environment-tools.md#references)レールには、選択したページを参照する内部リンクを一覧表示する新しいセクションがあります。これは、ページをオフラインで取得したり削除することが想定される場合や、オフラインで取得する前に調整する必要があるページを確認する場合に便利です。
* [リスト表示](/help/sites-authoring/basic-handling.md#list-view)には、ページが現在ワークフローに含まれている場合にステータスを表示する新しいワークフロー列があります。
* [ページのプロパティ](/help/sites-authoring/editing-page-properties.md)で、ページにサムネールを割り当てるときに既存のアセットを参照できるようになりました（「サムネール」タブ）。

## ページエディター {#page-editor}

* JS SDK を利用する React および Angular クライアント側コンポーネントで構築された単一ページアプリエクスペリエンスのコンテキスト内編集および作成が可能になりました（SPA エディターとも呼ばれます）。
* 基礎モードは、ページに基礎モードが設定されている場合にのみ表示されます。

## コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* 全般的なコメントを書き込んだり、テキスト内のコメントを表示（タイムラインレールにも表示）するための新しい[注釈](/help/assets/content-fragments-variations.md#viewing-editing-deleting-annotations)レールがコンテンツフラグメントエディターに追加されました。
* Ability to set the default content type of a multi-line text element in a [Content Fragment model](/help/assets/content-fragments-models.md) to simple text, rich text or markdown
* RTE（フルスクリーン表示）でテキストを選択して、[コメント／注釈](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)を追加できます。
* 参照レールでコンテンツフラグメント並列に表示して、[バージョンを比較](/help/assets/content-fragments-managing.md#comparing-fragment-versions)できるようになりました。
* アセットのダウンロードレポートにコンテンツフラグメントが適宜表示されるようになりました。
* /api.json を通じて、[Assets HTTP API でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになりました。コンテンツフラグメントの作成、更新、読み取りおよび削除のための API が用意されています。

## エクスペリエンスフラグメント {#experience-fragments}

* [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)のインデックス作成を改善して、フラグメントの使用ページの検索でコンテンツが見つかるようになりました。
* 「[Adobe Target に書き出し](/help/sites-administering/experience-fragments-target.md)」オプションで、エクスペリエンスフラグメントを JSON（デフォルトは HTML）またはその両方として送信できるようになりました。

## 翻訳 {#translation}

* プロジェクトマスターを使用して、翻訳プロジェクトを手軽に作成できます。
* 翻訳ジョブをデフォルトで承認済みステータスに設定することで、翻訳プロジェクトの実行を簡素化します。
* サードパーティ翻訳メモリの変更点に合わせて翻訳済みページを更新できます。
* 翻訳ジョブを JSON 形式で書き出すことができます。
* V3 APIを使用するようにMicrosoft Translation統合を更新

## Multi-Site Management (MSM) {#multi-site-management-msm}

* PushOnModifyを使用するロールアウト設定の場合、ページ移動操作の処理が改善され、状態の不整合を回避できます。
* ライブコピー構造内に新しいページを作成すると、デフォルトでスタンドアロンページが作成されるようになりました。
* JS SDK（別名SPAエディター）を使用するシングルページアプリでMSM機能を使用する

## ローンチ {#launches}

* ローンチの新しいレビューおよび承認ワークフローと、承認済みのローンチページのみ昇格させる機能が追加されました。
* [プロモーションステップの直後にローンチを削除するオプションが UI に追加](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)されました。

## コンテンツのターゲット設定とシミュレーション {#content-targeting-simulation}

* ContextHub データレイヤーおよびクライアント側ルールエンジンの JavaScript が更新され、jQuery 3 をデフォルトで使用するようになりました。

## AEMとAdobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>AEM 6.5 のリリース時点では、at.js 2.x は AEM でサポートされていません。at.js 1.x の最新バージョンを使用してください。

* Adobe Target との連携で Target Standard API を使用できるようになりました。AEMの以前のバージョンでは、非推奨となったTarget Classic HTTP APIを使用しています。
* Adobe Target `mbox.js` version 63 is included. Adobe strongly recommends to switch implementation to `at.js` v1.x.
* `at.js` バージョン1.5.0が含まれるようになりました。 Adobe recommends that you use [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) to provision `at.js` v1.x into the site.

## AEMとAdobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5が含まれます。 実装を `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0が含まれます。 Adobe recommends to use [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) to provision AppMeasurement.js into the site.

## AEMとコマース {#aem-commerce}

Improvements to the Commerce Integration Framework are on a faster release cycle since AEM 6.4. [Learn more here](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Communities アドオン {#communities-add-on}

[Communities のリリースノートページ](../release-notes/communities-release-notes.md)を参照してください。

## Screens アドオン {#screens-add-on}

* 起動を使用した署名コンテンツの将来のコンテンツ変更の計画
* シーケンスチャンネルでのメーター制再生が可能になりました。
* ソースファイル（Excel シートなど）を使用してプロジェクト構造を自動作成できるようになりました。

For more details on changes to AEM Screens - see the Release Notes in the [AEM Screens User Guide](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).
