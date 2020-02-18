---
title: SPAモデルのルーティング
seo-title: SPAモデルのルーティング
description: AEMのシングルページアプリの場合、アプリはルーティングを行います。 本書では、使用可能なルーティング・メカニズム、契約およびオプションについて説明します。
seo-description: AEMのシングルページアプリの場合、アプリはルーティングを行います。 本書では、使用可能なルーティング・メカニズム、契約およびオプションについて説明します。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPAモデルのルーティング{#spa-model-routing}

AEMのシングルページアプリの場合、アプリはルーティングを行います。 本書では、使用可能なルーティング・メカニズム、契約およびオプションについて説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## プロジェクト経路 {#project-routing}

アプリはルーティングを所有し、プロジェクトのフロントエンド開発者によって実装されます。 このドキュメントでは、AEMサーバーから返されるモデルに固有のルーティングについて説明します。 ページモデルのデータ構造は、基になるリソースのURLを公開します。 フロントエンドプロジェクトは、ルーティング機能を提供するカスタムライブラリまたはサードパーティライブラリを使用できます。 ルートでモデルのフラグメントが必要になったら、関数を呼び出す `PageModelManager.getData()` ことができます。 モデルルートが変更された場合、ページエディターなどのリスニングライブラリに警告を出すためにイベントをトリガーする必要があります。

## アーキテクチャ {#architecture}

詳細な説明については、SPA Blueprintドキュメントの [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) （ページモデルマネージャ）の節を参照してください。

## ModelRouter {#modelrouter}

有効 `ModelRouter` な場合、HTML5履歴API関数をカプセル化し、特定のモデ `pushState` ルのフ `replaceState` ラグメントが事前にフェッチされ、アクセス可能であることを保証します。 次に、モデルが変更されたことを登録されたフロントエンドコンポーネントに通知します。

## 手動ルーティングと自動モデルルーティング {#manual-vs-automatic-model-routing}

は、モ `ModelRouter` デルのフラグメントの取得を自動化します。 しかし、自動化されたツールには制限が伴います。 必要に応じて、メタ `ModelRouter` プロパティを使用してパスを無効にしたり、無視するように設定したりできます( [SPA Page Componentドキュメントの「Meta Properties](/help/sites-developing/spa-page-component.md) 」セクションを参照)。 フロントエンド開発者は、関数を使用して特定のモデルのフラグメントを読み込むように要求することで、独自 `PageModelManager` のモデルルーティングレイヤーを実装することがで `getData()` きます。

>[!NOTE]
>
>現在、We.Retail JournalサンプルReactプロジェクトは自動アプローチを示し、Angularプロジェクトは手動アプローチを示します。 半自動アプローチも有効です。

>[!CAUTION]
>
>現在のバージョンのみ `ModelRouter` で、Sling modelエントリポイントの実際のリソースパスを指すURLの使用がサポートされています。 バニティURLやエイリアスの使用はサポートされていません。

## ルーティングのコントラクト {#routing-contract}

現在の実装は、SPAプロジェクトでHTML5 History APIを使用して異なるアプリケーションページにルーティングすることを前提としています。

### 設定 {#configuration}

は、モデ `ModelRouter` ルフラグメントをリッスンし、モデルフラグメントをプリフェッチする呼び出しを `pushState` サポート `replaceState` しています。 内部的には、特定のURL `PageModelManager` に対応するモデルの読み込みをトリガーし、他のモジュールがリス `cq-pagemodel-route-changed` ンできるイベントを実行します。

デフォルトではこの処理が自動的に有効になっています。無効にする場合は、SPA で次のメタプロパティをレンダリングする必要があります。

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Note that every route of the SPA should correspond to an accessible resource in AEM (e.g., &quot; `/content/mysite/mypage"`) since the `PageModelManager` will automatically try to load the corresponding page model once the route is selected. Though, if needed, the SPA can also define a &quot;black list&quot; of routes that should be ignored by the `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
