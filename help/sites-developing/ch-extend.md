---
title: ContextHub の拡張
description: 提供される ContextHub ストアやモジュールがソリューションの要件を満たさない場合は、新しいタイプの ContextHub ストアやモジュールを定義する
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 59%

---

# ContextHub の拡張{#extending-contexthub}

提供される ContextHub ストアやモジュールがソリューションの要件を満たさない場合は、新しいタイプの ContextHub ストアやモジュールを定義します。

## カスタムストア候補の作成 {#creating-custom-store-candidates}

ContextHub ストアは、登録されたストア候補から作成されます。 カスタムストアを作成するには、ストア候補を作成して登録します。

ストア候補を作成して登録するコードを含む JavaScript ファイルは、 [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#creating-client-library-folders). フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.store.[storeType]
```

カテゴリの `[storeType]` 部分は、ストア候補と一緒に登録されている `storeType` です（「[ContextHub ストア候補の登録](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)」を参照）。例えば、storeType が `contexthub.mystore` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.store.contexthub.mystore` でなければなりません。

### ContextHub ストア候補の作成 {#creating-a-contexthub-store-candidate}

ストア候補を作成するには、[`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) 関数を使用して、次のいずれかのベースストアを拡張します。

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

各ベースストアは、 [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) ストア。

次の例では、`ContextHub.Store.PersistedStore` ストア候補の最もシンプルな拡張を作成しています。

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

実際には、カスタムストア候補は追加の関数を定義するか、ストアの初期設定を上書きします。 いくつかの[サンプルストア候補](/help/sites-developing/ch-samplestores.md)が、`/libs/granite/contexthub/components/stores` の下にあるリポジトリにインストールされています。これらのサンプルから学ぶには、CRXDE Liteを使用して JavaScript ファイルを開きます。

### ContextHub ストア候補の登録 {#registering-a-contexthub-store-candidate}

ストア候補を登録して ContextHub フレームワークに統合し、ストア候補からストアを作成できるようにします。ストア候補を登録するには、[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) クラスの `ContextHub.Utils.storeCandidates` 関数を使用します。

ストア候補を登録する際に、ストアタイプの名前を指定します。候補からストアを作成するときは、ストアタイプを使用してベースとする候補を識別します。

ストア候補を登録する際に、優先度を指定します。既に登録済みのストア候補と同じストアタイプを使用してストア候補を登録した場合、優先度の高い候補が使用されます。そのため、新しいストア候補を既存のストア候補に優先させることができます。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

通常、1 つの候補のみが必要で、優先度をに設定できます。 `0`. しかし、興味があれば、 [より高度な登録](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) :JavaScript 条件 (`applies`) および候補の優先度。

## ContextHub UI モジュールタイプの作成 {#creating-contexthub-ui-module-types}

[ContextHub に付属してインストールされる](/help/sites-developing/ch-samplemodules.md) UI モジュールタイプが要件を満たさない場合は、カスタム UI モジュールタイプを作成できます。UI モジュールタイプを作成するには、 `ContextHub.UI.BaseModuleRenderer` クラスとその後の登録 `ContextHub.UI`.

UI モジュールレンダラーを作成するには、UI モジュールをレンダリングするロジックを格納する `Class` オブジェクトを作成します。少なくとも、このクラスは次のアクションを実行する必要があります。

* `ContextHub.UI.BaseModuleRenderer` クラスを拡張します。このクラスは、すべての UI モジュールレンダラーのベースとなる実装です。`Class` オブジェクトは、このクラスが拡張されていることを示すために使用する `extend` というプロパティを定義します。

* デフォルトの設定を指定します。`defaultConfig` プロパティを作成します。このプロパティは、[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI モジュール用に定義されているプロパティと、必要なその他すべてのプロパティを含むオブジェクトです。

のソース `ContextHub.UI.BaseModuleRenderer` は/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js にあります。 レンダラーを登録するには、[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) クラスの `ContextHub.UI` メソッドを使用します。モジュールタイプの名前を指定します。 管理者がこのレンダラーに基づいて UI モジュールを作成する場合は、この名前を指定します。

レンダラークラスを作成し、自己実行する匿名関数に登録します。 次の例は、contexthub.browserinfo UI モジュールのソースコードをベースとしています。 この UI モジュールは、`ContextHub.UI.BaseModuleRenderer` クラスのシンプルな拡張です。

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

レンダラーを作成して登録するコードを含む JavaScript ファイルは、 [クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#creating-client-library-folders). フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.module.[moduleType]
```

カテゴリの `[moduleType]` 部分は、モジュールレンダラーの登録に使用されている `moduleType` です。例えば、`moduleType` が `contexthub.browserinfo` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.module.contexthub.browserinfo` でなければなりません。
