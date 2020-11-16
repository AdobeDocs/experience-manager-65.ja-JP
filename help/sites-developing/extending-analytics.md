---
title: イベント追跡の拡張
seo-title: イベント追跡の拡張
description: AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます
seo-description: AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 49%

---


# イベント追跡の拡張{#extending-event-tracking}

AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます。開発者は次の作業が必要になる場合があります。

* 訪問者がコンポーネントとどのようなやり取りをおこなっているかの追跡。This can be done with [Custom events.](#custom-events)
* [ContextHubの値にアクセスします](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [レコードのコールバックの追加](#adding-record-callbacks)。

>[!NOTE]
>
>This information is basically generic, but it uses [Adobe Analytics](/help/sites-administering/adobeanalytics.md) for specific examples.
>
>コンポーネントとダイアログボックスの開発に関する一般的な情報については、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

## カスタムイベント {#custom-events}

カスタムイベントはページ内の特定のコンポーネントの可用性に依存する要素を追跡します。これにはテンプレート特有のイベントも含まれます。ページコンポーネントは別のコンポーネントとして扱われています。

### ページの読み込み時のカスタムイベントの追跡 {#tracking-custom-events-on-page-load}

This can be done using the pseudo-attribute `data-tracking` (the older record attribute is still supported for backwards compatibility). これは任意の HTML タグに追加できます。

The syntax for `data-tracking` is

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

キーと値のペアは、2番目のパラメーター（ペイロードと呼ばれる）として任意の数だけ渡すことができます。

次に例を示します。

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

At page load, all `data-tracking` attributes will be collected and added to the event store of the ContextHub, where they can be mapped to Adobe Analytics events. マッピングされていないイベントは、Adobe Analyticsでは追跡されません。 See [Connecting to Adobe Analytics](/help/sites-administering/adobeanalytics.md) for more details about mapping events.

### ページの読み込み後のカスタムイベントの追跡 {#tracking-custom-events-after-page-load}

ページの読み込み後に発生するイベント（ユーザーインタラクションなど）を追跡するには、JavaScript 関数 `CQ_Analytics.record` を使用します。

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

場所

* `events`：文字列、または文字列の配列（イベントが複数の場合）。

* `values`：追跡するすべての値を格納します。
* `collect`：オプションで、イベントおよびデータオブジェクトを格納する配列を返します。
* `options` はオプションで、HTML要素やなどのリンクトラッキングオプション `obj` が含まれ ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`ます。

* `componentPath` が必要な属性であり、 `<%=resource.getResourceType()%>`

例えば、次のように定義した場合、「**Jump to top**」リンクをクリックすると `jumptop` と `headlineclick` の 2 つのイベントが実行されます。

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHubでの値へのアクセス {#accessing-values-in-the-contexthub}

ContextHub JavaScript APIには、指定されたストア（存在する場合）を返す `getStore(name)` 関数があります。 ストアには、指定したキーがある場合にその値を返す `getItem(key)` 関数があります。 関数を使用すると、特定のストアに対して定義されたキーの配列を取得できます。 `getKeys()`

関数を使用して関数を連結すると、ストアで値の変化を通知でき `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` ます。

The best way to be notified of initial availability of the ContextHub is to use the `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` function.

**ContextHubの追加イベント:**

すべてのストアに対応：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

ストア固有：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>完全なContextHub APIリファレンスも参照して [ください](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## レコードコールバックの追加 {#adding-record-callbacks}

Before and after callbacks are registered using the functions `CQ_Analytics.registerBeforeCallback(callback,rank)` and `CQ_Analytics.registerAfterCallback(callback,rank)`.

どちらの関数も、先頭の引数では関数を、2 番目の引数ではランクを受け取ります。このランクによって、コールバックの実行順序が決定されます。

コールバックが false を返す場合、実行チェーンの後続のコールバックは実行されません。
