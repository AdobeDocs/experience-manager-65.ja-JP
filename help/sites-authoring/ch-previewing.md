---
title: ContextHub データを使用したページのプレビュー
seo-title: ContextHub データを使用したページのプレビュー
description: ContextHub ツールバーは、ContextHub ストアからのデータを表示し、ストアデータを変更することができ、コンテンツのプレビューに役立ちます。
seo-description: ContextHub ツールバーは、ContextHub ストアからのデータを表示し、ストアデータを変更することができ、コンテンツのプレビューに役立ちます。
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 96%

---


# ContextHub データを使用したページのプレビュー {#previewing-pages-using-contexthub-data}

[ContextHub](/help/sites-developing/contexthub.md) ツールバーには、ContextHub ストアのデータが表示され、このツールバーを使用してストアデータを変更することができます。ContextHub ツールバーは、ContextHub ストア内のデータによって決定されるコンテンツのプレビューに役立ちます。

このツールバーは、1 つ以上の UI モジュールを含む一連の UI モードで構成されます。

* UI モードは、ツールバーの左側に表示されるアイコンです。アイコンをクリックまたはタップすると、そのモードに含まれる UI モジュールがツールバーに表示されます。
* UI モジュールは、1 つ以上の ContextHub ストアのデータを表示します。一部の UI モジュールでは、ストアデータを操作することもできます。

ContextHub によって、いくつかの UI モードと UI モジュールがインストールされます。管理者によって、異なる UI モードと UI モジュールを表示するように [ContextHub が設定されている](/help/sites-developing/ch-configuring.md)場合もあります。

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## ContextHub ツールバーの表示 {#revealing-the-contexthub-toolbar}

ContextHub ツールバーはプレビューモードで使用できます。このツールバーは、オーサーインスタンス上で、管理者が有効にしている場合にのみ使用できます。

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. 編集用にページを開いた状態で、ツールバーの「プレビュー」をクリックまたはタップします。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. ツールバーを表示するには、ContextHub アイコンをクリックまたはタップします。

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## UI モジュールの機能 {#ui-module-features}

提供する機能セットは UI モジュールごとに異なりますが、以下のタイプの機能は共通です。UI モジュールは拡張可能なので、開発者は必要に応じて他の機能を実装できます。

### ツールバーコンテンツ {#toolbar-content}

UI モジュールは、1 つ以上の ContextHub ストアのデータをツールバーに表示できます。UI モジュールは、アイコンとタイトルで識別されます。

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### ポップアップコンテンツ {#popup-content}

一部の UI モジュールは、クリックまたはタップされるとポップアップオーバーレイを表示します。一般的に、ポップアップには、ツールバーに表示されている以外の追加情報が含まれています。

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### ポップアップフォーム {#popup-forms}

モジュールのポップアップオーバーレイには、ContextHub ストア内のデータを変更するためのフォーム要素を含めることができます。ページコンテンツがストアデータによって決定される場合は、このフォームを使用してページコンテンツの変更を監視できます。

### 全画面表示モード {#fullscreen-mode}

ポップアップオーバーレイには、クリックまたはタップするとポップアップコンテンツを拡張してブラウザーウィンドウまたは画面全体に表示するアイコンを含めることができます。

![](do-not-localize/chlimage_1-18.png)

