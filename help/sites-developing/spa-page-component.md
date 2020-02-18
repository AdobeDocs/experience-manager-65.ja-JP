---
title: SPAページコンポーネント
seo-title: SPAページコンポーネント
description: SPAでは、ページコンポーネントは子コンポーネントのHTML要素を提供せず、代わりにSPAフレームワークに委任します。 このドキュメントでは、SPAのページ・コンポーネントがどのように一意になるかを説明します。
seo-description: SPAでは、ページコンポーネントは子コンポーネントのHTML要素を提供せず、代わりにSPAフレームワークに委任します。 このドキュメントでは、SPAのページ・コンポーネントがどのように一意になるかを説明します。
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPAページコンポーネント{#spa-page-component}

SPAでは、ページコンポーネントは子コンポーネントのHTML要素を提供せず、代わりにSPAフレームワークに委任します。 このドキュメントでは、SPAのページ・コンポーネントがどのように一意になるかを説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

SPAのページコンポーネントは、JSPまたはHTLファイルとリソースオブジェクトを介して、子コンポーネントのHTML要素を提供しません。 この処理は SPA フレームワークに委任されます。子コンポーネントの表現は、JSONデータ構造（例：モデル）として取得されます。 次に、提供されたJSONモデルに従ってSPAコンポーネントがページに追加されます。 したがって、ページコンポーネントの初期ボディの構成は、レンダリング済みのHTMLの初期ボディの構成とは異なります。

## ページモデルの管理 {#page-model-management}

The resolution and the management of the page model is delegated to a provided [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) module. SPAは、初期化時にモジュールとやり取りし、モデル更新の登録を行う必要があります。主に、作成者がページエディターを使用してページを編集しているときに生成されます。 `PageModelManager` は、SPAプ `PageModelManager` ロジェクトによってnpmパッケージとしてアクセスできます。 AEMとSPAの間のインタープリターとして、はSPAに付き `PageModelManager` 添うことを意図しています。

ページの作成を許可するには、SPAとページエディター間の通信チャネルを提供するため `cq.authoring.pagemodel.messaging` に、という名前のクライアントライブラリを追加する必要があります。 SPAページコンポーネントがページwcm/coreコンポーネントから継承される場合は、クライアントライブラリカテゴリを使用可能にするための次のオ `cq.authoring.pagemodel.messaging` プションが用意されています。

* テンプレートが編集可能な場合は、クライアントライブラリカテゴリをページポリシーに追加します。
* ページコンポーネントのを使用して、クライアントラ `customfooterlibs.html` イブラリカテゴリを追加します。

カテゴリの組み込みをページエディターのコンテキ `cq.authoring.pagemodel.messaging` ストに制限するのを忘れないでください。

## 通信データタイプ {#communication-data-type}

通信データ型は、属性を使用してAEMページコンポーネント内にHTML要素を設定し `data-cq-datatype` ます。 通信データ型がJSONに設定されている場合、GET要求はコンポーネントのSlingモデルエンドポイントに到達します。 ページエディターで更新が実行されると、更新されたコンポーネントの JSON 表記がページモデルのライブラリに送信されます。次に、ページモデルライブラリはSPAに更新の警告を表示します。

**SPAページコンポーネント —`body.html`**

```
<div id="page"></div>
```

DOM生成を遅らせないことをお勧めするだけでなく、SPAフレームワークでは、本文の末尾にスクリプトを追加する必要があります。

**SPAページコンポーネント —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

SPAコンテンツを記述するメタリソースプロパティ。

**SPAページコンポーネント —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>デフォルトのモデルセレクターは、コンポーネントのSlingモデル表現を要求する際に静的に設定されます。

## メタプロパティ {#meta-properties}

* `cq:wcmmode`:エディターのWCMモード（ページ、テンプレートなど）
* `cq:pagemodel_root_url`:アプリのルートモデルのURL。 子ページモデルはアプリのルートモデルのフラグメントなので、子ページに直接アクセスする場合に重要です。 次に、ア ` [PageModelManager](/help/sites-developing/spa-page-component.md)` プリの初期モデルを、そのルートエントリポイントからアプリに入るとして体系的に再構成する。

* `cq:pagemodel_router`:ライブラリの有効化ま ` [ModelRouter](/help/sites-developing/spa-routing.md)` たは無効 `PageModelManager` 化

* `cq:pagemodel_route_filters`:無視する必要のあるルートを提供するコンマ区切りリストまたは ` [ModelRouter](/help/sites-developing/spa-routing.md)` 正規表現。

## ページエディターオーバーレイの同期 {#page-editor-overlay-synchronization}

オーバーレイの同期は、カテゴリが提供するのと同じ変異オブザーバーによって保証さ `cq.authoring.page` れます。

## SlingモデルJSONに書き出された構造の設定 {#sling-model-json-exported-structure-configuration}

ルーティング機能が有効な場合、AEMナビゲーションコンポーネントのJSONエクスポートにより、SPAのJSONエクスポートにアプリケーションの様々なルートが含まれることが前提となります。 AEM ナビゲーションコンポーネントの JSON 出力は、次の 2 つのプロパティを使用し、SPA のルートページのコンテンツポリシーで設定することができます。

* `structureDepth`：書き出されたツリーの深度に対応する数字。
* `structurePatterns`:書き出すページに対応する正規表現の配列

これは、のSPAサンプルコンテンツに表示できま `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`す。
