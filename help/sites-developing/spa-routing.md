---
title: SPAモデルルーティング
seo-title: SPAモデルルーティング
description: AEMのシングルページアプリの場合、アプリはルーティングを担当します。 このドキュメントでは、ルーティングメカニズム、契約および使用可能なオプションについて説明します。
seo-description: AEMのシングルページアプリの場合、アプリはルーティングを担当します。 このドキュメントでは、ルーティングメカニズム、契約および使用可能なオプションについて説明します。
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
ht-degree: 4%

---


# SPAモデルルーティング{#spa-model-routing}

AEMのシングルページアプリの場合、アプリはルーティングを担当します。 このドキュメントでは、ルーティングメカニズム、契約および使用可能なオプションについて説明します。

>[!NOTE]
>
>SPAエディターは、SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトに推奨されるソリューションです。

## プロジェクトルーティング {#project-routing}

アプリはルーティングを所有し、プロジェクトのフロントエンド開発者によって実装されます。 このドキュメントでは、AEMサーバーから返されるモデルに固有のルーティングについて説明します。 ページモデルのデータ構造は、基になるリソースのURLを公開します。 フロントエンドプロジェクトでは、ルーティング機能を提供するカスタムライブラリまたはサードパーティライブラリを使用できます。 ルートでモデルのフラグメントが必要になると、関数の呼び出しを行うことができ `PageModelManager.getData()` ます。 モデルルートが変更された場合は、ページエディターなどのリスニングライブラリに警告するためにイベントをトリガーする必要があります。

## アーキテクチャ {#architecture}

詳細については、SPA BlueprintドキュメントのPageModelManager [の節を参照してください](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 。

## ModelRouter {#modelrouter}

有効な場合、 `ModelRouter` はHTML5履歴API関数をカプセル化し `pushState` 、特定のモデルフラグメントが事前に取得され、アクセス可能であ `replaceState` ることを保証します。 次に、モデルが変更されたことを登録されたフロントエンドコンポーネントに通知します。

## 手動と自動のモデルルーティング {#manual-vs-automatic-model-routing}

は、モデルのフラグメントの取得を `ModelRouter` 自動化します。 しかし、自動化されたツールには制限が伴います。 必要に応じて、メタプロパティを使用してパスを無効にしたり、無視するように設定する `ModelRouter` ことができます( [SPAページコンポーネント](/help/sites-developing/spa-page-component.md) ドキュメントの「メタプロパティ」セクションを参照)。 フロントエンド開発者は、関数を使用して特定のモデルのフラグメントを読み込むようにリクエストするこ `PageModelManager` とで、独自のモデルルーティングレイヤーを実装でき `getData()` ます。

>[!NOTE]
>
>現在、We.RetailジャーナルサンプルのReactプロジェクトは、自動アプローチを示し、Angularプロジェクトは手動アプローチを示します。 半自動化アプローチも有効な使用例です。

>[!CAUTION]
>
>現在のバージョンのみで、Sling Modelエントリポイントの実際のリソースパスを指すURLの使用がサポートされて `ModelRouter` います。 バニティURLやエイリアスの使用はサポートされていません。

## ルーティングのコントラクト {#routing-contract}

現在の実装は、SPAプロジェクトで、異なるアプリページへのルーティングにHTML5履歴APIを使用することを前提としています。

### 設定 {#configuration}

は、モデルルーティングのリスンと、モデルフラグメントのプリフェッチの呼び出しに関する概念を `ModelRouter` サポートし `pushState``replaceState` ています。 内部的に、指定されたURL `PageModelManager` に対応するモデルの読み込みがトリガーされ、他のモジュールがリッスンできる `cq-pagemodel-route-changed` イベントが発生します。

デフォルトではこの処理が自動的に有効になっています。無効にする場合は、SPA で次のメタプロパティをレンダリングする必要があります。

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Note that every route of the SPA should correspond to an accessible resource in AEM (e.g., &quot; `/content/mysite/mypage"`) since the `PageModelManager` will automatically try to load the corresponding page model once the route is selected. Though, if needed, the SPA can also define a &quot;block list&quot; of routes that should be ignored by the `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
