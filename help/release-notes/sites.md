---
title: AEM Sites リリースノート
description: Adobe Experience Manager 6.5 Sites 固有のリリースノート
exl-id: 0bd0933c-f14d-4be2-9ad0-3f8207d7fa5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 60%

---

# AEM Sites リリースノート {#aem-sites-release-notes}

AEM Sites 6.5 の機能強化について詳しくは、以下を参照してください。

## コンポーネントとテンプレートの開発 {#component-amp-template-development}

* 新規プロジェクト用の Maven プロジェクトアーキタイプ 18 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases) を参照）。
* 新規プロジェクト用の単一ページアプリ Maven プロジェクトアーキタイプ 1.0.6 以上（[リリースノートの GitHub](https://github.com/adobe/aem-spa-project-archetype/releases) を参照）。
* HTL バージョン 1.4（[リリースノートの GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4) を参照）。

   * 文字列、配列およびオブジェクトの「in」演算子

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * data-sly-setを使用した変数宣言：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 制御パラメーターのリストおよび繰り返し：開始、ステップ、終了：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrapの識別子：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 負の数のサポート

* コアコンポーネント 2.3.2 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照）。
* レイアウトコンテナのグリッドシステム（[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照）。
* Clientlib Manager:Google Closure CompilerをデフォルトでJavaScript clientlibsの縮小（古いデフォルトはYahoo YUI）に設定し、Google Closure Compilerをバージョンv20190121に更新しました。
* テンプレートエディターとポリシー

   * JS SDK(SPA Editorとも呼ばれます)を使用するシングルページアプリ用のテンプレートの作成と編集

* 参照サイト We.Retail 4.0（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照）。
* 既存のサイトをアップグレードして最新のエディター機能を活用するためのツールキット（[Githubリポジトリ](https://github.com/adobe/aem-modernize-tools)を参照）

>[!CAUTION]
>
>AEMには、既存のカスタムコードとの互換性を最大限に高めるために、jQueryライブラリのバージョン1.12.4が含まれています。 セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

## サイト管理  {#site-administration}

* [参照](/help/sites-authoring/author-environment-tools.md#references)レールには、選択したページを参照する内部リンクを一覧表示する新しいセクションがあります。これは、ページをオフラインで取得したり削除することが想定される場合や、オフラインで取得する前に調整する必要があるページを確認する場合に便利です。
* [リスト表示](/help/sites-authoring/basic-handling.md#list-view)には、ページが現在ワークフローに含まれている場合にステータスを表示する新しいワークフロー列があります。
* [ページのプロパティ](/help/sites-authoring/editing-page-properties.md)で、ページにサムネールを割り当てるときに既存のアセットを参照できるようになりました（「サムネール」タブ）。

## ページエディター {#page-editor}

* JS SDK を利用する React および Angular クライアント側コンポーネントで構築された単一ページアプリエクスペリエンスのコンテキスト内編集および作成が可能になりました（SPA エディターとも呼ばれます）。
* 基礎モードは、ページに基礎モードが設定されている場合にのみ表示されます。

## コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* 全般的なコメントを書き込んだり、テキスト内のコメントを表示（タイムラインレールにも表示）するための新しい[注釈](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)レールがコンテンツフラグメントエディターに追加されました。
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)の複数行テキスト要素のデフォルトのコンテンツタイプを、シンプルテキスト、リッチテキストまたはMarkdownに設定できます。
* RTE（フルスクリーン表示）でテキストを選択して、[コメント／注釈](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)を追加できます。
* 参照レールでコンテンツフラグメント並列に表示して、[バージョンを比較](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)できるようになりました。
* アセットのダウンロードレポートにコンテンツフラグメントが適宜表示されるようになりました。
* /api.json を通じて、[Assets HTTP API でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになりました。コンテンツフラグメントの作成、更新、読み取りおよび削除のための API が用意されています。

## エクスペリエンスフラグメント {#experience-fragments}

* [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)のインデックス作成を改善して、フラグメントの使用ページの検索でコンテンツが見つかるようになりました。
* 「[Adobe Target に書き出し](/help/sites-administering/experience-fragments-target.md)」オプションで、エクスペリエンスフラグメントを JSON（デフォルトは HTML）またはその両方として送信できるようになりました。

## 翻訳 {#translation}

* プロジェクトマスターを使用して、翻訳プロジェクトを手軽に作成できます。
* 翻訳ジョブをデフォルトで承認ステータスに設定することで、翻訳プロジェクトの実行を簡略化できます。
* サードパーティ翻訳メモリの変更点に合わせて翻訳済みページを更新できます。
* 翻訳ジョブを JSON 形式で書き出すことができます。
* V3 APIを使用するためのMicrosoft Translation統合の更新

## マルチサイト管理(MSM) {#multi-site-management-msm}

* PushOnModifyを使用するロールアウト設定の場合、ページ移動操作の処理を改善し、状態の不整合を回避
* ライブコピー構造内に新しいページを作成すると、デフォルトでスタンドアロンページが作成されるようになりました。
* JS SDKを使用するシングルページアプリでMSM機能を使用する(SPA Editorとも呼ばれます)

## ローンチ {#launches}

* ローンチの新しいレビューおよび承認ワークフローと、承認済みのローンチページのみ昇格させる機能が追加されました。
* [プロモーションステップの直後にローンチを削除するオプションが UI に追加](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)されました。

## コンテンツのターゲット設定とシミュレーション  {#content-targeting-simulation}

* ContextHub データレイヤーおよびクライアント側ルールエンジンの JavaScript が更新され、jQuery 3 をデフォルトで使用するようになりました。

## AEMとAdobe Target{#aem-amp-adobe-target}

>[!CAUTION]
>
>現在：
>
>* AEMアクティビティコンソール内でAdobe Targetをターゲティングエンジンとして使用している場合は、`at.js 1.x`のみがサポートされます。
   >
   >
* Targetへのエクスペリエンスフラグメントの書き出しを使用し、Targetのコンソール内でアクティビティを実行している場合、`at.js. 1.x`と`at.js 2.x`の両方がサポートされます。


* Adobe Target との連携で Target Standard API を使用できるようになりました。以前のバージョンのAEMでは、現在は非推奨（廃止予定）となっていたTarget Classic HTTP APIを使用していました。
* Adobe Target `mbox.js`バージョン63が含まれています。 Adobeでは、実装を`at.js` v1.xに切り替えることを強くお勧めします。
* `at.js` バージョン1.5.0が含まれるようになりました。Adobeでは、[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)を使用して`at.js` v1.xをサイトにプロビジョニングすることをお勧めします。

## AEMとAdobe Analytics{#aem-amp-adobe-analytics}

* `s_code.js` H.27.5が含まれています。Adobeでは、実装を`AppMeasurement.js`に切り替えることをお勧めします。
* `AppMeasurement.js` v1.8.0が含まれます。Adobeは、[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)を使用してAppMeasurement.jsをサイトにプロビジョニングすることをお勧めします。

## AEMとコマース{#aem-commerce}

AEM 6.4以降、Commerce Integration Frameworkの改善は、より高速なリリースサイクルに進んでいます。[詳細はこちら](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

## Communities アドオン {#communities-add-on}

[Communities のリリースノートページ](../release-notes/communities-release-notes.md)を参照してください。

## Screens アドオン  {#screens-add-on}

* ローンチを使用したサイネージコンテンツの将来のコンテンツ変更の計画
* シーケンスチャンネルでのメーター制再生が可能になりました。
* ソースファイル（Excel シートなど）を使用してプロジェクト構造を自動作成できるようになりました。

AEM Screensの変更点について詳しくは、『[AEM Screensユーザーガイド](https://docs.adobe.com/content/help/ja/experience-manager-screens/user-guide/aem-screens-introduction.html)』のリリースノートを参照してください。
