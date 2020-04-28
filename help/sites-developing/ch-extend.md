---
title: ContextHub の拡張
seo-title: ContextHub の拡張
description: 提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます
seo-description: 提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3

---


# ContextHub の拡張{#extending-contexthub}

提供されている ContextHub ストアやモジュールのタイプがソリューションの要件を満たさない場合は、新しいタイプを定義できます。

## カスタムストア候補の作成 {#creating-custom-store-candidates}

ContextHub ストアは、登録済みのストア候補から作成します。カスタムストアを作成するには、ストア候補を作成して登録する必要があります。

ストア候補を作成して登録するコードを含む JavaScript ファイルは、[クライアントライブラリフォルダー](/help/sites-developing/clientlibs.md#creating-client-library-folders)に含める必要があります。フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.store.[storeType]
```

The `[storeType]` part of the category is the `storeType` with which the store candidate is registered. （「[ContextHub ストア候補の登録](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)」を参照）。例えば、storeType が `contexthub.mystore` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.store.contexthub.mystore` でなければなりません。

### ContextHub ストア候補の作成 {#creating-a-contexthub-store-candidate}

To create a store candidate, you use the [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) function to extend one of the base stores:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Note that each base store extends the [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) store.

次の例では、`ContextHub.Store.PersistedStore` ストア候補の最もシンプルな拡張を作成しています。

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

実際には、カスタムストア候補は追加の関数を定義するか、ストアの初期設定を上書きします。Several [sample store candidates](/help/sites-developing/ch-samplestores.md) are installed in the repository below `/libs/granite/contexthub/components/stores`. これらのサンプルを参考にするには、CRXDE Lite を使用して JavaScript ファイルを開きます。

### ContextHub ストア候補の登録 {#registering-a-contexthub-store-candidate}

ストア候補を登録して ContextHub フレームワークに統合し、ストア候補からストアを作成できるようにします。ストア候補を登録するには、[`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) クラスの `ContextHub.Utils.storeCandidates` 関数を使用します。

ストアの候補を登録する際に、ストアの種類の名前を指定します。 候補からストアを作成するときは、ストアタイプを使用してベースとする候補を識別します。

ストア候補を登録する際に、優先度を指定します。既に登録されている店舗候補と同じ店舗タイプで店舗候補が登録された場合は、優先度の高い候補を用いる。 そのため、新しいストア候補を既存のストア候補に優先させることができます。

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

ほとんどの場合、1つの候補のみが必要で、優先度をに設定できますが、より高度な登録について知りたい場合は、 `0`JavaScript条件( [)と優先度に基づいて、数少ないストア実装の1つを選択できます](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies)`applies`。

## ContextHub UI モジュールタイプの作成 {#creating-contexthub-ui-module-types}

[ContextHub に付属してインストールされる](/help/sites-developing/ch-samplemodules.md) UI モジュールタイプが要件を満たさない場合は、カスタム UI モジュールタイプを作成できます。UI モジュールタイプを作成するには、`ContextHub.UI.BaseModuleRenderer` クラスを拡張して `ContextHub.UI` に登録し、新しい UI モジュールレンダラーを作成します。

UI モジュールレンダラーを作成するには、UI モジュールをレンダリングするロジックを格納する `Class` オブジェクトを作成します。少なくとも、このクラスは次のアクションを実行する必要があります。

* Extend the `ContextHub.UI.BaseModuleRenderer` class. このクラスは、すべての UI モジュールレンダラーのベースとなる実装です。`Class` オブジェクトは、このクラスが拡張されていることを示すために使用する `extend` というプロパティを定義します。

* デフォルトの設定を指定します。Create a `defaultConfig` property. このプロパティは、[`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI モジュール用に定義されているプロパティと、必要なその他すべてのプロパティを含むオブジェクトです。

The source for `ContextHub.UI.BaseModuleRenderer` is located at /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  レンダラーを登録するには、[`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) クラスの `ContextHub.UI` メソッドを使用します。モジュールタイプの名前を指定する必要があります。管理者がこのレンダラーをベースとして UI モジュールを作成する場合は、この名前を指定します。

レンダラークラスを作成し、自己実行型匿名関数に登録します。次の例は、contexthub.browserinfo UI モジュールのソースコードをベースとしています。この UI モジュールは、`ContextHub.UI.BaseModuleRenderer` クラスのシンプルな拡張です。

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

The javascript file that includes the code that creates and registers the renderer must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). フォルダーのカテゴリは、次のパターンに一致しなければなりません。

```xml
contexthub.module.[moduleType]
```

The `[moduleType]` part of the category is the `moduleType` with which the module renderer is registered. 例えば、`moduleType` が `contexthub.browserinfo` の場合、クライアントライブラリフォルダーのカテゴリは `contexthub.module.contexthub.browserinfo` でなければなりません。
