---
title: イベント追跡の拡張
seo-title: Extending Event Tracking
description: AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 100%

---

# イベント追跡の拡張{#extending-event-tracking}

AEM Analytics では、Web サイトでのユーザーインタラクションを追跡できます。開発者は次の作業が必要になる場合があります。

* 訪問者がコンポーネントとどのようなやり取りをおこなっているかの追跡。これを行うには、[カスタムイベント](#custom-events)を使用します。
* [ContextHub の値へのアクセス](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。
* [レコードのコールバックの追加](#adding-record-callbacks)。

>[!NOTE]
>
>この情報は基本的には全体に適用されますが、一部の例では [Adobe Analytics](/help/sites-administering/adobeanalytics.md) が使用されています。
>
>コンポーネントとダイアログボックスの開発に関する一般的な情報については、[コンポーネントの開発](/help/sites-developing/components.md)を参照してください。

## カスタムイベント {#custom-events}

カスタムイベントはページ内の特定のコンポーネントの可用性に依存する要素を追跡します。これにはテンプレート特有のイベントも含まれます。ページコンポーネントは別のコンポーネントとして扱われています。

### ページの読み込み時のカスタムイベントの追跡 {#tracking-custom-events-on-page-load}

これを行うには、疑似属性 `data-tracking`（下位互換性のために、古いレコード属性がまだサポートされています）を使用します。これは任意の HTML タグに追加できます。

`data-tracking` の構文は次のとおりです。

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

2 番目のパラメーターとして、任意の数のキーと値のペアを渡すことができます。これをペイロードと呼びます。

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

ページの読み込み時に、すべての `data-tracking` 属性が収集されて ContextHub のイベントストアに追加され、Adobe Analytics イベントにマッピングできるようになります。マッピングされないイベントは Adobe Analytics では追跡されません。マッピングイベントについて詳しくは、[Adobe Analytics への接続](/help/sites-administering/adobeanalytics.md)を参照してください。

### ページの読み込み後のカスタムイベントの追跡 {#tracking-custom-events-after-page-load}

ページの読み込み後に発生するイベント（ユーザーインタラクションなど）を追跡するには、JavaScript 関数 `CQ_Analytics.record` を使用します。

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

ここで、

* `events`：文字列、または文字列の配列（イベントが複数の場合）。

* `values`：追跡するすべての値を格納します。
* `collect`：オプションで、イベントおよびデータオブジェクトを格納する配列を返します。
* `options`：オプションであり、HTML 要素 `obj` および ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)` などのリンク追跡オプションが含まれます。

* `componentPath`：必須の属性。`<%=resource.getResourceType()%>` に設定することを推奨します。

例えば、次のように定義した場合、「**Jump to top**」リンクをクリックすると `jumptop` と `headlineclick` の 2 つのイベントが実行されます。

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## ContextHub の値へのアクセス {#accessing-values-in-the-contexthub}

ContextHub JavaScript API には、指定したストアを返す `getStore(name)` 関数があります（使用可能な場合）。このストアには、指定したキーの値を返す `getItem(key)` 関数があります（使用可能な場合）。`getKeys()` 関数を使用すると、特定のストアに対して定義されたキーの配列を取得できます。

`ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` 関数を使用して関数をバインドすると、ストアの値が変更されたことを知らせる通知を受けることができます。

ContextHub の利用開始の通知を受けるには、`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` 関数を使用するのが最適です。

**ContextHub のその他のイベント：**

すべてのストアに対応：

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

ストア固有：

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>完全な [ContextHub API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/contexthub-api.html?lang=ja)も参照してください

## レコードコールバックの追加 {#adding-record-callbacks}

関数 `CQ_Analytics.registerBeforeCallback(callback,rank)` と `CQ_Analytics.registerAfterCallback(callback,rank)` を使用して、before コールバックと after コールバックを登録します。

どちらの関数も、先頭の引数では関数を、2 番目の引数ではランクを受け取ります。このランクによって、コールバックの実行順序が決定されます。

コールバックが false を返す場合、実行チェーンの後続のコールバックは実行されません。
