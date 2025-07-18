---
title: SPA の動的モデルとコンポーネントのマッピング
description: Adobe Experience Manager 用 JavaScript SPA SDK で動的モデルとコンポーネントとのマッピングがどのように行われるかを説明します。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: ht
source-wordcount: '313'
ht-degree: 100%

---


# SPA の動的モデルとコンポーネントのマッピング{#dynamic-model-to-component-mapping-for-spas}

このドキュメントでは、Adobe Experience Manager（AEM）用 JavaScript SPA SDK で動的モデルとコンポーネントのマッピングがどのように行われるかを説明します。

{{ue-over-spa}}

## ComponentMapping モジュール {#componentmapping-module}

`ComponentMapping` モジュールは、プロントエンドプロジェクトに NPM パッケージとして提供されます。フロントエンドコンポーネントを格納し、単一ページアプリケーションがフロントエンドコンポーネントを AEM リソースタイプにマップする方法を提供します。これにより、アプリケーションの JSON モデルを構文解析する際に、コンポーネントの動的な解決が可能になります。

モデル内の各項目には、AEM リソースタイプを表示する `:type` フィールドが含まれます。フロントエンドコンポーネントは、マウントされると、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

モデル解析とモデルへのフロントエンドコンポーネントアクセスについて詳しくは、[SPA ブループリント](/help/sites-developing/spa-blueprint.md)を参照してください。

npm パッケージも参照してください。[https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## モデル駆動型単一ページアプリケーション {#model-driven-single-page-application}

AEM 用 JavaScript SPA SDK を使用する単一ページアプリケーションは、モデル主導です。

1. フロントエンドコンポーネントは、自らを[コンポーネントマッピングストア](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)に登録します。
1. [モデルプロバイダー](/help/sites-developing/spa-blueprint.md#the-model-provider)でモデルが提供されると、[コンテナ](/help/sites-developing/spa-blueprint.md#container)はそのモデルコンテンツ（`:items`）を反復します。

1. ページがある場合、そのページの子（`:children`）は、最初に[コンポーネントマッピング](/help/sites-developing/spa-blueprint.md#componentmapping)からコンポーネントクラスを取得してから、取得したクラスをインスタンス化します。

## アプリの初期化 {#app-initialization}

各コンポーネントは、[`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider) の機能で拡張されます。初期化は、次の一般的な形式をとります。

1. 各モデルプロバイダーは自身を初期化し、内部コンポーネントに対応するモデルの部分に対しておこなわれる変更をリッスンします。
1. [初期化フロー](/help/sites-developing/spa-blueprint.md)で示されるとおりに、[`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) は初期化される必要があります。

1. 保存されると、ページモデルマネージャーはアプリの完全なモデルを返します。
1. 次に、このモデルは、アプリケーションのフロントエンドルート[コンテナ](/help/sites-developing/spa-blueprint.md#container)コンポーネントに渡されます。
1. モデルの断片は、最後に個々の子コンポーネントに伝播されます。

![app_model_initialization](assets/app_model_initialization.png)
