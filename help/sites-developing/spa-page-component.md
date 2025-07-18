---
title: SPA ページコンポーネント
description: SPA では、ページコンポーネントは子コンポーネントの HTML 要素を提供せず、代わりに SPA フレームワークに委任します。このドキュメントでは、これにより SPA のページコンポーネントがどのように一意になるかを説明します。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: ht
source-wordcount: '707'
ht-degree: 100%

---


# SPA ページコンポーネント{#spa-page-component}

SPA では、ページコンポーネントは子コンポーネントの HTML 要素を提供せず、代わりに SPA フレームワークに委任します。このドキュメントでは、これにより SPA のページコンポーネントがどのように一意になるかを説明します。

{{ue-over-spa}}

## はじめに {#introduction}

SPA のページコンポーネントは、JSP ファイルまたは HTL のファイルやリソースオブジェクトを介して子コンポーネントの HTML 要素を提供しません。この処理は SPA フレームワークに委任されます。子コンポーネントの表現は、JSON データ構造（モデル）として取得されます。次に、指定された JSON モデルに従って SPA コンポーネントがページに追加されます。そのため、ページコンポーネントの初期本文の構成は、その対応するプリレンダリング HTML とは異なります。

## ページモデルの管理  {#page-model-management}

ページモデルの解決と管理は、指定の [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) モジュールに委任されます。SPA は、初期化時に `PageModelManager` モジュールとやり取りして、初期ページモデルを取得し、モデル更新の登録をおこなう必要があります。これは主に、作成者がページエディターを使用してページを編集しているときに生成されます。`PageModelManager` は、npm パッケージとして SPA プロジェクトからアクセスできます。`PageModelManager` は、AEMとSPAとの間のインタープリターなので、SPAに付随するものです。

ページを作成できるようにするには、`cq.authoring.pagemodel.messaging` という名前のクライアントライブラリを追加して、SPA とページエディターの間の通信チャネルを提供する必要があります。SPA ページコンポーネントがページ wcm/core コンポーネントから継承している場合は、次のオプションを使用して、`cq.authoring.pagemodel.messaging` クライアントライブラリカテゴリを使用可能にします。

* テンプレートが編集可能な場合は、クライアントライブラリカテゴリをページポリシーに追加します。
* ページコンポーネントの `customfooterlibs.html` を使用したクライアントライブラリカテゴリを追加します。

`cq.authoring.pagemodel.messaging` カテゴリの組み込みをページエディターのコンテキストに制限することを忘れないでください。

## 通信データタイプ {#communication-data-type}

通信データタイプは、`data-cq-datatype` 属性を使用して AEM ページコンポーネント内に HTML 要素を設定します。通信データタイプが JSON に設定されると、GET リクエストにより、コンポーネントの Sling Model エンドポイントにヒットします。ページエディターで更新が実行されると、更新されたコンポーネントの JSON 表現がページモデルのライブラリに送信されます。次に、ページモデルのライブラリから、SPA に更新が警告されます。

**SPA ページコンポーネント -`body.html`**

```
<div id="page"></div>
```

DOM の生成を遅延させないことは基本ですが、それに加えて、SPA フレームワークは本文の末尾にスクリプトを追加する必要があります。

**SPA ページコンポーネント -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

SPA コンテンツを記述するメタリソースプロパティです。

**SPA ページコンポーネント -`customheaderlibs.html`**

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
>コンポーネントの Sling Model 表現をリクエストする際、デフォルトのモデルセレクターは静的に設定されます。

## メタプロパティ {#meta-properties}

* `cq:wcmmode`：エディターの WCM モード（ページ、テンプレートなど）
* `cq:pagemodel_root_url`：アプリのルートモデルの URL。子ページモデルはアプリのルートモデルのフラグメントなので、子ページに直接アクセスする場合に重要です。次に、` [PageModelManager](/help/sites-developing/spa-page-component.md)` は、アプリケーションの初期モデルを、そのルートエントリポイントからアプリケーションに入るときに体系的に再構成します。

* `cq:pagemodel_router`：`PageModelManager` ライブラリの ` [ModelRouter](/help/sites-developing/spa-routing.md)` を有効化または無効化

* `cq:pagemodel_route_filters`：` [ModelRouter](/help/sites-developing/spa-routing.md)` が無視する必要があるルートを指定するための、カンマ区切りのリストまたは正規表現。

>[!CAUTION]
>
>このドキュメントでは、We.Retail ジャーナルアプリケーションをデモの目的でのみ使用します。どのプロジェクト作業にも使用しないでください。
>
>AEM プロジェクトでは、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を使用する必要があります。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を使用します。AEM 上のすべての SPA プロジェクトは Maven アーキタイプ SPA 向け スターターキットを基にしている必要があります。

## ページエディターオーバーレイの同期 {#page-editor-overlay-synchronization}

オーバーレイの同期は、`cq.authoring.page` カテゴリが提供するのと同じミューテーションオブザーバーが保証されます。

## Sling Model JSON が書き出した構造設定 {#sling-model-json-exported-structure-configuration}

ルーティング機能を有効にすると、AEM ナビゲーションコンポーネントの JSON 書き出しによって、SPA の JSON 書き出しにアプリケーションの複数のルートが含まれるという前提になります。AEM ナビゲーションコンポーネントの JSON 出力は、次の 2 つのプロパティを使用し、SPA のルートページのコンテンツポリシーで設定することができます。

* `structureDepth`：書き出されたツリーの深度に対応する数字。
* `structurePatterns`：書き出すページに対応する Regex の Regex 配列。

これは、`/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root` にある SPA サンプルコンテンツで確認できます。
