---
title: ClientContext JavaScript API
seo-title: ClientContext JavaScript API
description: ClientContext 用 JavaScript API
seo-description: ClientContext 用 JavaScript API
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 90%

---


# ClientContext JavaScript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgrオブジェクトは、自己登録済みのセッションストアのセットを含むシングルトンで、セッションストアの登録、保存、管理のためのメソッドを提供します。

CQ_Analytics.PersistedSessionStore を拡張します。

### メソッド {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

指定された名前のセッションストアを返します。[セッションストアへのアクセス](/help/sites-developing/client-context.md#accessing-session-stores)も参照してください。

**パラメーター**

* name：String。セッションストアの名前。

**戻り値**

指定された名前のセッションストアを表す CQ_Analytics.SessionStore オブジェクト。指定された名前のストアが存在しない場合は、`null` を返します。

#### register(sessionstore) {#register-sessionstore}

セッションストアを ClientContext に登録します。完了時に storeregister イベントと storeupdate イベントを発生させます。

**パラメーター**

* sessionstore：CQ_Analytics.SessionStore。登録するセッションストアオブジェクト。

**戻り値**

戻り値はありません。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

セッションストアのアクティベートと登録をリッスンするためのメソッドを提供します。See also [Checking That a Session Store is Defined and Initialized](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### メソッド {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

セッションストアが初期化されたときに呼び出されるコールバック関数を登録します。複数回初期化されるストアの場合は、コールバック関数が一度だけ呼び出されるように、コールバック遅延を指定します。

* 前回の初期化の遅延期間中にストアが初期化されると、前回の関数呼び出しがキャンセルされ、現在の初期化に対して関数が再度呼び出されます。
* 次の初期化が発生する前に遅延期間が経過した場合、コールバック関数は 2 回実行されます。

例えば、JSON オブジェクトをベースとするセッションストアがあり、JSON 要求を使用して取得するものとします。次の初期化シナリオが考えられます。

* 要求が完了し、データが取得され、ストアに読み込まれます。この場合、初期化は一度だけおこなわれます。
* 要求が失敗します（タイムアウト）。この場合、初期化はおこなわれず、ストアにデータは読み込まれません。
* ストアにはデフォルト値（初期化プロパティ）が事前設定されていますが、要求は失敗します（タイムアウト）。デフォルト値を使用した初期化は一度だけおこなわれます。
* ストアは事前設定されています。

When the delay is set to `true` or a number of milliseconds, the method waits before calling the callback method. delay で設定した遅延時間が経過する前に別の初期化イベントが発生した場合は、初期化イベントを発生させないまま、遅延時間が経過するまで待機します。これにより、2 番目の初期化イベントが発生するまで待機して、最適な状況でコールバック関数を呼び出すことができます。

**パラメーター**

* storeName：String。リスナーに追加するセッションストアの名前。
* callback：Function。ストアの初期化時に呼び出す関数。
* delay：Boolean または Number。コールバック関数の呼び出しを遅延させる時間（ミリ秒単位）。A boolean value of `true` uses the default delay of `200 ms`. A boolean value of `false` or a negative number causes no delay to be used.

**戻り値**

戻り値はありません。

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

セッションストアが登録されたときに呼び出されるコールバック関数を登録します。The register event occurs when a store is registered to [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**パラメーター**

* storeName：String。リスナーに追加するセッションストアの名前。
* callback：Function。ストアの初期化時に呼び出す関数。

**戻り値**

戻り値はありません。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

JSON データを格納する非永続セッションストア。データは外部 JSONP サービスから取得されます。Use the `getInstance` or `getRegisteredInstance` method to create an instance of this class.

CQ_Analytics.JSONStore を拡張します。

### プロパティ {#properties}

継承されるプロパティについては、CQ_Analytics.JSONStore および CQ_Analytics.SessonStore を参照してください。

### メソッド {#methods-2}

継承されるメソッドについては、CQ_Analytics.JSONStore および CQ_Analytics.SessonStore も参照してください。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

CQ_Analytics.JSONPStore オブジェクトを作成します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。storeName が指定されていない場合、メソッドは null を返します。
* serviceURL：String。JSONP サービスの URL
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* deferLoading：（オプション）Boolean。値が true の場合は、オブジェクトの作成時に JSONP サービスが呼び出されません。値が false の場合は、JSONP サービスが呼び出されます。
* loadingCallback:（オプション）文字列。 JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

新しいCQ_Analytics.JSONPStoreオブジェクト。storeNameがnullの場合はnull。

#### getServiceURL() {#getserviceurl}

このオブジェクトが JSON データの所得に使用する JSONP サービスの URL を取得します。

**パラメーター**

なし.

**戻り値**

サービス URL を表す String、またはサービス URL が設定されていない場合は null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

JSONP サービスを呼び出します。JSONP の URL は、指定されたコールバック関数名が後ろに付いたサービス URL です。

**パラメーター**

* serviceURL：（オプション）String。呼び出す JSONP サービス。値が null の場合は、既に設定済みのサービス URL が使用されます。null 以外の値は、このオブジェクトに使用する JSONP サービスを設定します。（setServiceURL を参照）。
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* callback：（オプション）String。JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

CQ_Analytics.JSONPStoreオブジェクトを作成し、ストアをClient Contextに登録します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。storeName が指定されていない場合、メソッドは null を返します。
* serviceURL：（オプション）String。JSONP サービスの URL。
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* callback：（オプション）String。JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

登録された CQ_Analytics.JSONPStore オブジェクト。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

JSON データの取得に使用する JSONP サービスの URL を設定します。

**パラメーター**

* serviceURL：String。JSON データを提供する JSONP サービスの URL

**戻り値**

戻り値はありません。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON オブジェクトのコンテナ。このクラスのインスタンスを作成して、JSONデータを含む非永続的なセッションストアを作成します。

`myjsonstore = new CQ_Analytics.JSONStore`

初期化時にストアに設定される一連のデータを定義できます。

CQ_Analytics.SessionStore を拡張します。

### プロパティ {#properties-1}

#### STOREKEY {#storekey}

ストアを識別するキー。この値を取得するには、`getInstance` メソッドを使用します。

#### STORENAME {#storename}

ストアの名前。この値を取得するには、`getInstance` メソッドを使用します。

### メソッド {#methods-3}

継承されるメソッドについては、CQ_Analytics.SessionStore も参照してください。

#### clear() {#clear}

セッションストアのデータを削除し、すべての初期化プロパティを削除します。

**パラメーター**

なし.

**戻り値**

戻り値はありません。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

指定された名前で、指定された JSON データを使用して初期化される（initJSON メソッドを呼び出す）CQ_Analytics.JSONStore オブジェクトを作成します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData：Object。JSON データを格納するオブジェクト。

**戻り値**

CQ_Analytics.JSONStore オブジェクト。

#### getJSON() {#getjson}

セッションストアのデータを JSON 形式で取得します。

**パラメーター**

なし.

**戻り値**

JSON 形式のストアデータを表すオブジェクト。

#### init() {#init}

セッションストアをクリアし、初期化プロパティを使用して初期化します。Sets the initialization flag to `true` and then fires the `initialize` and `update` events.

**パラメーター**

なし.

**戻り値**

戻り値はありません。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

JSON オブジェクト内のデータから初期化プロパティを作成します。オプションで、既存の初期化プロパティをすべて削除できます。

プロパティの名前は、JSON オブジェクト内のデータの階層から得られます。次のサンプルのコードは、JSON オブジェクトを表しています。

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

この例では、次のプロパティがストア内に作成されます。

```xml
A: "valueA"
B/B1: "valueBB1"
```

**パラメーター**

* jsonData：保存するデータを格納する JSON オブジェクト。
* doNotClear:値をtrueに設定すると、既存の初期化プロパティが保持され、JSONオブジェクトから派生した初期化プロパティが追加されます。 値をfalseに設定した場合、既存の初期化プロパティが削除された後で、JSONオブジェクトから派生した初期化プロパティが追加されます。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

指定された名前で、指定された JSON データを使用して初期化される（initJSON メソッドを呼び出す）CQ_Analytics.JSONStore オブジェクトを作成します。新しいオブジェクトは、Clickstream Cloud Manager に自動的に登録されます。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData：Object。JSON データを格納するオブジェクト。

**戻り値**

CQ_Analytics.JSONStore オブジェクト。

## CQ_Analytics.Observable {#cq-analytics-observable}

イベントを発生させ、他のオブジェクトがこれらのイベントをリッスンして対処できるようにします。このクラスを拡張したクラスは、リスナーを呼び出すイベントを発生させることができます。

### メソッド {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

イベントのリスナーを登録します。[セッションストアの更新に対処するリスナーの作成](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update)も参照してください。

**パラメーター**

* event：String。リッスンするイベントの名前。
* fct：Function。イベント発生時に呼び出される関数。
* 範囲：（オプション）オブジェクト。 ハンドラー関数の実行範囲。ハンドラー関数の「this」コンテキストとなります。

**戻り値**

戻り値はありません。

#### removeListener(event, fct) {#removelistener-event-fct}

イベントに対して指定されたイベントハンドラーを削除します。

**パラメーター**

* event：String。イベントの名前。
* fct：Function。イベントハンドラー。

**戻り値**

戻り値はありません。

## CQ_Analyics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

リモート JSONP サービスから取得される JSON オブジェクトの永続コンテナ。

CQ_Analytics.PersistedJSONStore を拡張します。

### メソッド {#methods-5}

継承されるメソッドについては、CQ_Analytics.PersistedJSONStore も参照してください。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

CQ_Analytics.PersistedJSONPStore オブジェクトを作成します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。storeName が指定されていない場合、メソッドは null を返します。
* serviceURL：String。JSONP サービスの URL
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* deferLoading：（オプション）Boolean。値が true の場合は、オブジェクトの作成時に JSONP サービスが呼び出されません。値が false の場合は、JSONP サービスが呼び出されます。
* loadingCallback:（オプション）文字列。 JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

新しいCQ_Analytics.PersistedJSONPStoreオブジェクト。storeNameがnullの場合はnull。

#### getServiceURL() {#getserviceurl-1}

このオブジェクトが JSON データの所得に使用する JSONP サービスの URL を取得します。

**パラメーター**

なし.

**戻り値**

サービス URL を表す String、またはサービス URL が設定されていない場合は null。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

JSONP サービスを呼び出します。JSONP の URL は、指定されたコールバック関数名が後ろに付いたサービス URL です。

**パラメーター**

* serviceURL：（オプション）String。呼び出す JSONP サービス。値が null の場合は、既に設定済みのサービス URL が使用されます。null 以外の値は、このオブジェクトに使用する JSONP サービスを設定します。（setServiceURL を参照）。
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* callback：（オプション）String。JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

CQ_Analytics.PersistedJSONPStoreオブジェクトを作成し、ストアをクライアントコンテキストに登録します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。storeName が指定されていない場合、メソッドは null を返します。
* serviceURL：（オプション）String。JSONP サービスの URL。
* dynamicData：（オプション）Object。コールバック関数を呼び出す前に、ストアの初期化データに追加する JSON データ。
* callback：（オプション）String。JSONP サービスが返す JSONP オブジェクトの処理のために呼び出す関数の名前。コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである単一のパラメーターを定義する必要があります。

**戻り値**

登録された CQ_Analytics.PersistedJSONPStore オブジェクト。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

JSON データの取得に使用する JSONP サービスの URL を設定します。

**パラメーター**

* serviceURL：String。JSON データを提供する JSONP サービスの URL

**戻り値**

戻り値はありません。

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

JSON オブジェクトの永続コンテナ。

Extends `CQ_Analytics.PersistedSessionStore`.

### プロパティ {#properties-2}

#### STOREKEY {#storekey-1}

ストアを識別するキー。この値を取得するには、`getInstance` メソッドを使用します。

#### STORENAME {#storename-1}

ストアの名前。この値を取得するには、`getInstance` メソッドを使用します。

### メソッド {#methods-6}

継承されるメソッドについては、CQ_Analytics.PersistedSessionStore も参照してください。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

指定された名前で、指定された JSON データを使用して初期化される（initJSON メソッドを呼び出す）CQ_Analytics.PersistedJSONStore オブジェクトを作成します。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData：Object。JSON データを格納するオブジェクト。

**戻り値**

CQ_Analytics.PersistedJSONStore オブジェクト。

#### getJSON() {#getjson-1}

セッションストアのデータを JSON 形式で取得します。

**パラメーター**

なし.

**戻り値**

JSON 形式のストアデータを表すオブジェクト。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

JSON オブジェクト内のデータから初期化プロパティを作成します。オプションで、既存の初期化プロパティをすべて削除できます。

プロパティの名前は、JSON オブジェクト内のデータの階層から得られます。次のサンプルのコードは、JSON オブジェクトを表しています。

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

この例では、次のプロパティがストア内に作成されます。

```xml
A: "valueA"
B/B1: "valueBB1"
```

**パラメーター**

* jsonData：保存するデータを格納する JSON オブジェクト。
* doNotClear:値をtrueに設定すると、既存の初期化プロパティが保持され、JSONオブジェクトから派生した初期化プロパティが追加されます。 値をfalseに設定した場合、既存の初期化プロパティが削除された後で、JSONオブジェクトから派生した初期化プロパティが追加されます。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

指定された名前で、指定された JSON データを使用して初期化される（initJSON メソッドを呼び出す）CQ_Analytics.PersistedJSONStore オブジェクトを作成します。新しいオブジェクトは、ClientContext Manager に自動的に登録されます。

**パラメーター**

* storeName：String。STORENAME プロパティとして使用する名前。STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData：Object。JSON データを格納するオブジェクト。

**戻り値**

CQ_Analytics.PersistedJSONStore オブジェクト。

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

プロパティと値のコンテナ。データは CQ_Analytics.SessionPersistence を使用して保持されます。このクラスのインスタンスを作成して、永続化されたセッションストアを作成します。

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

CQ_Analytics.SessionStore を拡張します。

### プロパティ {#properties-3}

#### STOREKEY {#storekey-2}

デフォルト値は `key` です。

### メソッド {#methods-7}

継承されるメソッドについては、CQ_Analytics.SessionStore を参照してください。

When the inherited methods `clear`, `setProperty`, `setProperties`, `removeProperty` are used to change the store data, the changes are automatically persisted, unless the changed properties are flagged as notPersisted.

#### getStoreKey() {#getstorekey}

Retrieves the `STOREKEY` property.

**パラメーター**

なし

**戻り値**

プ `STOREKEY` ロパティの値。

#### isPersisted(name) {#ispersisted-name}

データプロパティが永続化されているかどうかを判断します。

**パラメーター**

* name：String。プロパティの名前。

**戻り値**

永続プロパティの場合は Boolean 値 `true`、値が永続プロパティではない場合は Boolean 値 `false` です。

#### persist() {#persist}

セッションストアを保持します。The default persistence mode uses browser `localStorage` using `ClientSidePersistence` as the name ( `window.localStorage.set("ClientSidePersistance", store);`)

localStorage が使用できないまたは書き込めない場合、ストアはウィンドウのプロパティとして保持されます。

完了時に `persist` イベントを発生させます。

**パラメーター**

なし

**戻り値**

戻り値はありません。

#### reset(deferEvent) {#reset-deferevent}

すべてのデータプロパティをストアから削除して、ストアを保持します。オプションで、完了時に `udpate` イベントを発生させません。

**パラメーター**

* deferEvent：値が true の場合は、`update` イベントを発生させないようにします。値が `false` の場合は、update イベントを発生させます。

**戻り値**

戻り値はありません。

#### setNonPersisted(name) {#setnonpersisted-name}

データプロパティに「非永続」というフラグを設定します。

**パラメーター**

* name：String。永続化しないプロパティの名前。

**戻り値**

戻り値はありません。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore はセッションストアを表します。セッションストアを作成するには、このクラスのインスタンスを次のように作成します。

`mystore = new CQ_Analytics.SessionStore`

CQ_Analytics.Observableを拡張します。

### プロパティ {#properties-4}

#### STORENAME {#storename-2}

セッションストアの名前。このプロパティの値を取得するには、getName を使用します。

### メソッド {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

プロパティと値をセッションストアの初期化データに追加します。

初期化の値をセッションストアデータに設定するには、loadInitProperties を使用します。

**パラメーター**

* name：String。追加するプロパティの名前。
* value：String。追加するプロパティの値。

**戻り値**

戻り値はありません。

#### clear() {#clear-1}

ストアからすべてのデータプロパティを削除します。

**パラメーター**

なし.

**戻り値**

戻り値はありません。

#### getData(excluded) {#getdata-excluded}

ストアデータを返します。オプションで、名前プロパティをデータから除外します。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

excluded：（オプション）返されるデータから除外するプロパティ名の配列。

**戻り値**

プロパティとその値からなるオブジェクト。

#### getInitProperty(name) {#getinitproperty-name}

データプロパティの値を取得します。

**パラメーター**

* name：String。取得するデータプロパティの名前。

**戻り値**

データプロパティの値。指定された名前のプロパティがセッションストアに格納されていない場合は `null` を返します。

#### getName() {#getname}

セッションストアの名前を返します。

**パラメーター**

なし.

**戻り値**

ストア名を表す String 値。

#### getProperty(name, raw) {#getproperty-name-raw}

プロパティの値を返します。値は未加工のプロパティまたは XSS フィルタリングされた値として返されます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name：String。取得するデータプロパティの名前。
* raw：Boolean。値が true の場合は、未加工のプロパティ値が返されます。値が false の場合は、返す値が XSS フィルタリングされます。

**戻り値**

データプロパティの値。

#### getPropertyNames(excluded) {#getpropertynames-excluded}

セッションストアに格納されているプロパティの名前を返します。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

excluded：（オプション）結果から除外するプロパティ名の配列。

**戻り値**

セッションプロパティ名を表す String 値の配列。

#### getSessionStore() {#getsessionstore}

現在のオブジェクトに結び付けられているセッションストアを返します。

**パラメーター**

なし.

**戻り値**

this

#### init() {#init-1}

ストアを「初期化済み」としてマークし、`initialize` イベントを発生させます。

**パラメーター**

なし.

**戻り値**

戻り値はありません。

#### isInitialized() {#isinitialized}

セッションストアが初期化されていることを示します。

**パラメーター**

なし.

**戻り値**

ストアが初期化されている場合は値 `true`、ストアが初期化されていない場合は値 `false`。

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

指定されたオブジェクトのプロパティをセッションストアの初期化データに追加します。オプションで、オブジェクトデータもストアデータに追加します。

**パラメーター**

* obj：可算プロパティを格納するオブジェクト。
* setValues：true の場合、ストアデータに同じ名前のプロパティがまだ含まれていなければ、obj のプロパティがセッションストアデータに追加されます。false の場合、セッションストアデータに追加されるデータはありません。

**戻り値**

戻り値はありません。

#### removeProperty(name) {#removeproperty-name}

セッションストアからプロパティを削除します。完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name：String。削除するプロパティの名前。

**戻り値**

戻り値はありません。

#### reset() {#reset}

データストアの初期値を復元します。デフォルトの実装では、すべてのデータが削除されるだけです。完了時に `update` イベントを発生させます。

**パラメーター**

なし.

**戻り値**

戻り値はありません。

#### setProperties(properties) {#setproperties-properties}

複数のプロパティの値を設定します。完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* Properties：Object。可算プロパティを格納するオブジェクト。各プロパティ名と値がストアに追加されます。

**戻り値**

戻り値はありません。

#### setProperty(name, value) {#setproperty-name-value}

プロパティの値を設定します。完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name：String。プロパティの名前。
* value：String。プロパティ値。

**戻り値**

戻り値はありません。
