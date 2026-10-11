---
title: Backbone インタラクション
description: AEM Forms Workspace における Backbone JavaScript モデルの使用についての概念情報。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 100%
---
# Backbone インタラクション{#backbone-interaction}

Backbone は、web アプリケーションで MVC アーキテクチャの作成および追随に役立つライブラリです。 Backbone の基本概念は、ユーザーのインターフェイスをモデルによって裏付けられたロジックビューに編成し、モデルを変更する場合はページを作り直すことなく、個々に更新できるようにすることです。 Backbone について詳しくは、[https://backbonejs.org](https://backbonejs.org/) を参照してください。

いくつかの主要な概念を次に示します。

**Backbone モデル**：データと、このデータに関連付けられたほとんどのロジックが含まれています。

**Backbone ビュー**：対応するモデルの状態を表示するために使用します。 Backbone ビューは実際にはコントローラと同じように動作します。ユーザーがクリックするなどのユーザーインターフェイスイベントやモデルイベント（データが変更されたなど）をリッスンし、ユーザーインターフェイスを適宜変更します。

**HTML テンプレート**：モデルによって生成されたプレースホルダーがある、ラッパーテンプレート。

**AEM Forms ワークスペース**：複数の個別コンポーネントが含まれます。 各コンポーネントは、

* 単一の論理ユーザーインターフェイス要素を表します。
* 類似のコンポーネントを集めてコレクションにすることができます。
* Backbone モデル、Backbone ビュー、および HTML テンプレートで構成されています。
* サービスへの参照が含まれています。
* 必要なユーティリティへの参照が含まれています。

コンポーネントが初期化された場合、次のオブジェクトが作成されます。

* コンポーネントに Backbone モデルの新しいインスタンスが作成されます。 モデルにサービスが挿入されます。
* Backbone ビューの新しいインスタンスが作成されます。
* 対応するモデルのインスタンス、HTML テンプレート、およびユーティリティがビューに挿入されます。

Backbone ビューには、対応するハンドラーとのユーザーインターフェイスインタラクションによって発生する様々なイベントをマッピングするイベントマップがあります。 このマッピングは、コンポーネントが初期化された場合に開始されます。

ビューが初期化された場合、ビューは対応するモデルを呼び出してサーバーからデータを取得します。 ビューによって要求されたすべてのデータが使用可能になると、ビューはデータを HTML テンプレートによって指定された形式にレンダリングします。 複数のビューで、通信用に同じモデルを共有することが可能です。

![AEM Forms Backbone ビュー](do-not-localize/aem_forms_workflow.png)

次に例を示します。

1. ユーザーはタスクリストでタスクテンプレートをクリックします。
1. タスクビューはクリックをリッスンし、タスクモデルでレンダリング関数を呼び出します。
1. その後タスクモデルは、AEM Forms サーバーとのすべての通信で共通のポイントであるサービスを呼び出します。
1. サービスクラスは、レンダリングメソッドの AEM Forms REST エンドポイントを Ajax 経由で呼び出します。
1. この Ajax 呼び出しの成功コールバックはタスクモデルに定義されています。
1. タスクモデルは Backbone イベントをレンダリング呼び出し完了通知として発生させます。
1. 別のビューであるタスクの詳細ビューは、タスクモデルからこのイベントをリッスンします。
1. タスクの詳細ビューはその後、タスクの詳細テンプレートを変更してレンダリングされたタスク（フォーム、詳細、添付ファイル、メモなど）をユーザーに表示します。
