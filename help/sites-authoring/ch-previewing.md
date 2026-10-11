---
title: ContextHub データを使用したページのプレビュー
description: ContextHub ツールバーは、ContextHub ストアからのデータを表示し、ストアデータを変更することができ、コンテンツのプレビューに立ちます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 78673609-8cbc-4b4b-953e-56c31ea1b4ea
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 100%
---
# ContextHub データを使用したページのプレビュー{#previewing-pages-using-contexthub-data}

[ContextHub](/help/sites-developing/contexthub.md) ツールバーを使用すると、ContextHub ストアからデータを表示して、ストアデータを変更できます。 ContextHub ツールバーは、ContextHub ストア内のデータに基づいて決定されるコンテンツのプレビューに役立ちます。

このツールバーは、1 つ以上の UI モジュールを含む一連の UI モードで構成されます。

* UI モードは、ツールバーの左側に表示されるアイコンです。 アイコンをクリックすると、そのモードに含まれる UI モジュールがツールバーに表示されます。
* UI モジュールは、1 つ以上の ContextHub ストアのデータを表示します。 また、一部の UI モジュールでは、ストアデータを操作することもできます。

ContextHub によって、いくつかの UI モードと UI モジュールがインストールされます。 管理者が、異なる UI モードと UI モジュールを表示するように [ContextHub を設定](/help/sites-developing/ch-configuring.md)している場合があります。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## ContextHub ツールバーの表示 {#revealing-the-contexthub-toolbar}

ContextHub ツールバーは、プレビューモードで使用できます。 このツールバーは、オーサーインスタンス上で、管理者が有効にしている場合にのみ使用できます。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 編集用にページを開いた状態で、ツールバーの「プレビュー」をクリックします。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. ツールバーを表示するには、ContextHub アイコンをクリックします。

   ![Context Hub](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI モジュールの機能 {#ui-module-features}

提供する機能セットは UI モジュールごとに異なりますが、次のタイプの機能は共通しています。 UI モジュールは拡張可能なので、開発者は必要に応じて他の機能を実装できます。

### ツールバーのコンテンツ {#toolbar-content}

UI モジュールは、1 つ以上の ContextHub ストアのデータをツールバーに表示できます。 UI モジュールは、アイコンとタイトルで識別されます。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### ポップアップコンテンツ {#popup-content}

一部の UI モジュールでは、クリックまたはタップするとポップアップオーバーレイが表示されます。 一般的に、ポップアップには、ツールバーに表示されている以外の追加情報が含まれています。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### ポップアップフォーム {#popup-forms}

モジュールのポップアップオーバーレイには、ContextHub ストア内のデータを変更するためのフォーム要素を含めることができます。 ページのコンテンツがストアデータによって決まる場合は、このフォームを使用してページコンテンツの変更を監視できます。

### 全画面表示モード {#fullscreen-mode}

ポップアップオーバーレイには、クリックするとポップアップコンテンツを拡張してブラウザーウィンドウまたは画面全体に表示するアイコンを含めることができます。

![全画面](do-not-localize/chlimage_1-18.png)
