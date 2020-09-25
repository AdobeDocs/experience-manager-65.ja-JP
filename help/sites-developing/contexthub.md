---
title: ContextHub
seo-title: ContextHub
description: ContextHubは、コンテキストデータの保存、操作、表示のためのフレームワークです
seo-description: ContextHubは、コンテキストデータの保存、操作、表示のためのフレームワークです
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 67%

---


# ContextHub{#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。クライアント側のJavaScript APIを使用すると、コンテンツのパーソナライズ用にデータにアクセスできます。

>[!NOTE]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)は、ContextHub を実装しており、ContextHub をプロジェクトに組み込む際の参考になります。

>[!CAUTION]
>
>The path containing the sample ContextHub configuration that is used by the [We.Retail reference implementation](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) should only be used as a reference for creating your own configuration.
>
>プロジェクトでは、独自のContextHub設定として使用しないでください。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub Javascript APIを使用すると、ストアにアクセスし、必要に応じてデータを作成、更新、削除できます。 したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、いくつかの[ストアタイプのサンプル](/help/sites-developing/ch-samplestores.md)が用意されています。
* AEM コンソールを使用して[ストアを作成](ch-configuring.md#creating-a-contexthub-store)します。
* Developers can [create custom store types](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* 開発者は、JavaScript を使用して[ストアデータにアクセス](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)できます。

## セグメント化 {#segmentation}

ContextHub には、セグメントの管理や、現在のコンテキストで解決されるセグメントの判断をするセグメント化エンジンが含まれています。いくつかのセグメントが定義されています。JavaScript API を使用して、[解決されたセグメントを判断](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)できます。

## プレゼンテーション {#presentation}

マーケティング担当者と作成者は、[ContextHub ツールバー](/help/sites-authoring/ch-previewing.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。このツールバーは、ContextHub ストアへのアクセスを提供する UI モジュールのグループで構成されています。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、いくつかの[モジュールタイプのサンプル](/help/sites-developing/ch-samplemodules.md)が用意されています。
* AEM コンソールを使用して [UI モジュールを追加](ch-configuring.md#adding-a-ui-module)し、[UI モードにグループ化](ch-configuring.md#adding-a-ui-mode)します。

* 開発者は、[カスタムモジュールタイプを作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)できます。

開発者は、[ContextHub コンポーネントをページに追加](/help/sites-developing/ch-adding.md)する必要があります。
