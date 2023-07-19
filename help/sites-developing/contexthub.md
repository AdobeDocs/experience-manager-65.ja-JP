---
title: ContextHub
seo-title: ContextHub
description: ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 61%

---

# ContextHub{#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。クライアント側 JavaScript API を使用してデータにアクセスし、コンテンツをパーソナライズできます。

>[!NOTE]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)は、ContextHub を実装しており、ContextHub をプロジェクトに組み込む際の参考になります。

>[!CAUTION]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)で使用される ContextHub 設定のサンプルを含むパス（`/libs/settings/cloudsettings/legacy`）は、独自の設定を作成する際の参考としてご利用ください。
>
>独自の ContextHub 設定としてプロジェクトで使用しないでください。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub JavaScript API を使用すると、ストアにアクセスして、必要に応じてデータを作成、更新および削除できます。 したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルストアタイプ](/help/sites-developing/ch-samplestores.md).
* AEMコンソールを使用して [ストアを作成](ch-configuring.md#creating-a-contexthub-store).
* デベロッパーは、[カスタムストアタイプを作成](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)できます。
* 開発者が実行できる操作 [ストアデータにアクセス](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) JavaScript を使用します。

## セグメント化 {#segmentation}

ContextHub には、セグメントの管理や、現在のコンテキストで解決されるセグメントを判断するセグメント化エンジンが含まれています。いくつかのセグメントが定義されています。JavaScript API を使用すると、 [解決されたセグメントを決定](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## プレゼンテーション {#presentation}

マーケターと作成者は、[ContextHub ツールバー](/help/sites-authoring/ch-previewing.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。ツールバーは、ContextHub ストアへのアクセスを提供する UI モジュールのグループで構成されます。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルモジュールタイプ](/help/sites-developing/ch-samplemodules.md).
* AEMコンソールを使用して [UI モジュールの追加](ch-configuring.md#adding-a-ui-module)、および [UI モードでグループ化](ch-configuring.md#adding-a-ui-mode).

* 開発者が実行できる操作 [カスタムモジュールタイプの作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

開発者は、 [ページに ContextHub コンポーネントを追加する](/help/sites-developing/ch-adding.md).
