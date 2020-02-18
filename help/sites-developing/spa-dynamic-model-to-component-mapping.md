---
title: SPAの動的モデルとコンポーネントのマッピング
seo-title: SPAの動的モデルとコンポーネントのマッピング
description: この記事では、AEM用のJavaScript SPA SDKで動的モデルとコンポーネントのマッピングがどのように行われるかを説明します。
seo-description: この記事では、AEM用のJavaScript SPA SDKで動的モデルとコンポーネントのマッピングがどのように行われるかを説明します。
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPAの動的モデルとコンポーネントのマッピング{#dynamic-model-to-component-mapping-for-spas}

このドキュメントでは、AEM用のJavaScript SPA SDKで動的モデルとコンポーネントのマッピングがどのように行われるかを説明します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## ComponentMapping モジュール {#componentmapping-module}

The `ComponentMapping` module is provided as an NPM package to the front-end project. フロントエンドコンポーネントが格納され、シングルページアプリケーションがフロントエンドコンポーネントをAEMリソースタイプにマップする方法を提供します。 これにより、アプリケーションのJSONモデルを解析する際に、コンポーネントの動的な解決が可能になります。

モデル内に存在する各項目には、AEMリソースタ `:type` イプを公開するフィールドが含まれています。 マウントすると、フロントエンドコンポーネントは、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

モデル解析とモデルへのフロントエンドコンポーネントアクセスの詳細については、 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) (SPA Blueprint)ドキュメントを参照してください。

npmパッケージも参照してください。https://www.npmjs.com/package/@adobe/cq-spa-component-mapping [](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

## モデル駆動型シングルページアプリ {#model-driven-single-page-application}

AEM向けJavaScript SPA SDKを利用するシングルページアプリケーションは、モデル主導型です。

1. フロントエンドコンポーネントは、それ自体を [Component Mapping storeに登録します](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 次に、 [Container](/help/sites-developing/spa-blueprint.md#container)（コンテナ）は、モデルプロバイダーによってモデルが提供され [ると、そのモデルのコンテンツ](/help/sites-developing/spa-blueprint.md#the-model-provider)( `:items`)を繰り返し処理します。

1. ページの場合、その子( `:children`)は、最初にコンポーネントマッピングからコンポーネントクラスを取得し [、インスタンス化します](/help/sites-developing/spa-blueprint.md#componentmapping) 。

## アプリの初期化 {#app-initialization}

各コンポーネントは、の機能を使用して拡張されま [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)す。 したがって、初期化は次の一般的な形式をとります。

1. 各モデルプロバイダーは、自身を初期化し、その内部コンポーネントに対応するモデルに対して行われた変更をリッスンします。
1. 初期化フ [ ローで表されるとおりに初期化する `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 必要があります [](/help/sites-developing/spa-blueprint.md)。

1. 保存すると、ページモデルマネージャーはアプリの完全なモデルを返します。
1. 次に、このモデルはアプリケーションのフロントエンドルート [Container](/help/sites-developing/spa-blueprint.md#container) コンポーネントに渡されます。
1. モデルの断片は、最終的に各子コンポーネントに伝達されます。

![app_model_initialization](assets/app_model_initialization.png)

