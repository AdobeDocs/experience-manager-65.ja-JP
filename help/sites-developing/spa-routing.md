---
title: SPA モデルルーティング
seo-title: SPA モデルルーティング
description: AEM の単一ページアプリケーションの場合、アプリはルーティングを担当します。このドキュメントでは、ルーティングメカニズム、契約、使用可能なオプションについて説明します。
seo-description: AEM の単一ページアプリケーションの場合、アプリはルーティングを担当します。このドキュメントでは、ルーティングメカニズム、契約、使用可能なオプションについて説明します。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 90%

---


# SPA モデルルーティング{#spa-model-routing}

AEM の単一ページアプリケーションの場合、アプリはルーティングを担当します。このドキュメントでは、ルーティングメカニズム、契約、使用可能なオプションについて説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## プロジェクトルーティング {#project-routing}

アプリはルーティングを所有し、プロジェクトのフロントエンド開発者によって実装されます。このドキュメントでは、AEM サーバーから返されるモデルに固有のルーティングについて説明します。ページモデルのデータ構造は、基になるリソースの URL を反映します。フロントエンドプロジェクトでは、ルーティング機能を提供する任意のカスタムライブラリまたはサードパーティ製ライブラリを使用できます。ルートでモデルのフラグメントが予想されたら、`PageModelManager.getData()` 関数の呼び出しをおこなうことができます。モデルルートが変更された場合は、イベントをトリガーして、ページエディターなどのリッスンしているライブラリに警告する必要があります。

## アーキテクチャ {#architecture}

詳しくは、SPA ブループリントドキュメントの [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) の節を参照してください。

## ModelRouter {#modelrouter}

`ModelRouter` は、有効な場合、HTML5 の History API 関数 `pushState` および `replaceState` をカプセル化して、特定のモデルフラグメントが事前に取得されアクセス可能になることを保証します。次に、モデルが変更されたことを登録済みのフロントエンドコンポーネントに通知します。

## 手動と自動のモデルルーティング {#manual-vs-automatic-model-routing}

`ModelRouter` は、モデルフラグメントの取得を自動化します。ただし、自動化された処理の常として、制限を伴います。必要に応じて、`ModelRouter` を無効にしたり、パスを無視するようにメタプロパティで設定したりできます（[SPA ページコンポーネント](/help/sites-developing/spa-page-component.md)のドキュメントでメタプロパティに関する節を参照）。フロントエンド開発者は、`getData()` 関数を使用して特定のモデルフラグメントを読み込むように `PageModelManager` に要求することで、独自のモデルルーティングレイヤーを実装することができます。

>[!NOTE]
>
>現在、We.RetailジャーナルサンプルのReactプロジェクトは、自動アプローチを示し、Angularプロジェクトは手動アプローチを示します。 半自動化アプローチも有効な使用例です。

>[!CAUTION]
>
>`ModelRouter` の現在のバージョンでは、Sling Model エントリポイントの実際のリソースパスを指す URL のみ使用できます。バニティ URL やエイリアスの使用はサポートしていません。

## ルーティングのコントラクト {#routing-contract}

現在の実装では、SPA プロジェクトで様々なアプリケーションページへのルーティングに HTML5 の History API を使用することを前提としています。

### 設定 {#configuration}

`ModelRouter` では、`pushState` 呼び出しと `replaceState` 呼び出しをリッスンしてモデルフラグメントをプリフェッチするので、モデルルーティングの概念をサポートしています。内部では、`PageModelManager` をトリガーして指定の URL に対応するモデルを読み込み、他のモジュールがリッスンできる `cq-pagemodel-route-changed` イベントを発生させます。

デフォルトではこの処理が自動的に有効になっています。無効にする場合は、SPA で次のメタプロパティをレンダリングする必要があります。

```
<meta property="cq:pagemodel_router" content="disable"\>
```

なお、ルートが選択されると、対応するページモデルの読み込みが `PageModelManager` で自動的に試行されるので、SPA のすべてのルートを AEM 内のアクセス可能なリソース（`/content/mysite/mypage"` など）に対応させる必要があります。ただし、SPA では、必要に応じて、`PageModelManager` で無視する必要があるルートの「ブロックリスト」を定義することもできます。

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
