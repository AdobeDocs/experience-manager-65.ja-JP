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
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 49%

---

# イベント追跡の拡張{#extending-event-tracking}

AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます。開発者は次の作業が必要になる場合があります。

* 訪問者がコンポーネントとどのようなやり取りをおこなっているかの追跡。これは、[カスタムイベントで実行できます。](#custom-events)
* [ContextHubの値にアクセスします](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [レコードのコールバックの追加](#adding-record-callbacks)。

>[!NOTE]
>
>この情報は基本的に汎用的ですが、具体的な例には[Adobe Analytics](/help/sites-administering/adobeanalytics.md)を使用します。
>
>コンポーネントとダイアログボックスの開発に関する一般的な情報については、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

## カスタムイベント {#custom-events}

カスタムイベントはページ内の特定のコンポーネントの可用性に依存する要素を追跡します。これにはテンプレート特有のイベントも含まれます。ページコンポーネントは別のコンポーネントとして扱われています。

### ページの読み込み時のカスタムイベントの追跡  {#tracking-custom-events-on-page-load}

これは、擬似属性`data-tracking`を使用して実行できます（下位互換性を保つために、古いレコード属性も引き続きサポートされます）。 これは任意の HTML タグに追加できます。

`data-tracking`の構文は次のとおりです。

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

キーと値のペアは、任意の数を2番目のパラメーター（ペイロードと呼ばれる）として渡すことができます。

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

ページの読み込み時に、すべての`data-tracking`属性が収集され、ContextHubのイベントストアに追加され、Adobe Analyticsイベントにマッピングできます。 マッピングされていないイベントは、Adobe Analyticsでは追跡されません。 イベントのマッピングについて詳しくは、[Adobe Analytics](/help/sites-administering/adobeanalytics.md)への接続を参照してください。

### ページの読み込み後のカスタムイベントの追跡 {#tracking-custom-events-after-page-load}

ページの読み込み後に発生するイベント（ユーザーインタラクションなど）を追跡するには、JavaScript 関数 `CQ_Analytics.record` を使用します。

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

ここで、

* `events`：文字列、または文字列の配列（イベントが複数の場合）。

* `values`：追跡するすべての値を格納します。
* `collect`：オプションで、イベントおよびデータオブジェクトを格納する配列を返します。
* `options` はオプションで、HTML要素やなどのリンクトラッキングオプションが含 `obj` まれま ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`す。

* `componentPath` が必要な属性である場合は、  `<%=resource.getResourceType()%>`

例えば、次のように定義した場合、「**Jump to top**」リンクをクリックすると `jumptop` と `headlineclick` の 2 つのイベントが実行されます。

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHubの値へのアクセス{#accessing-values-in-the-contexthub}

ContextHub JavaScript APIには、指定されたストアがある場合、そのストアを返す`getStore(name)`関数があります。 ストアには、指定されたキーの値（ある場合）を返す`getItem(key)`関数があります。 `getKeys()`関数を使用して、特定のストアに対して定義されたキーの配列を取得できます。

`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`関数を使用して関数をバインドすると、ストアの値の変更を通知できます。

ContextHubが最初に使用可能になったことを通知する最適な方法は、`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`関数を使用することです。

**ContextHubの追加イベント：**

すべてのストアに対応：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

ストア固有：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>[ContextHub APIリファレンス](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)も参照してください。

## レコードコールバックの追加 {#adding-record-callbacks}

コールバックの登録前と登録後は、関数`CQ_Analytics.registerBeforeCallback(callback,rank)`と`CQ_Analytics.registerAfterCallback(callback,rank)`を使用して行います。

どちらの関数も、先頭の引数では関数を、2 番目の引数ではランクを受け取ります。このランクによって、コールバックの実行順序が決定されます。

コールバックが false を返す場合、実行チェーンの後続のコールバックは実行されません。
