---
title: ClientContext JavaScript API
description: Adobe Experience Managerの ClientContext 用 JavaScript API について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 24%

---

# ClientContext JavaScript API{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

CQ_Analytics.ClientContextMgr オブジェクトは、自己登録されたセッションストアのセットを含むシングルトンで、セッションストアを登録、保持、管理するためのメソッドを提供します。

CQ_Analytics.PersistedSessionStore を拡張します。

### メソッド {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

指定された名前のセッションストアを返します。 関連トピック [セッションストアへのアクセス](/help/sites-developing/client-context.md#accessing-session-stores).

**パラメーター**

* name: String。 セッションストアの名前。

**戻り値**

指定した名前のセッションストアを表す CQ_Analytics.SessionStore オブジェクト。 指定された名前のストアが存在しない場合は、`null` を返します。

#### register(sessionstore) {#register-sessionstore}

セッションストアを ClientContext に登録します。 完了時に storeregister および storeupdate イベントを実行します。

**パラメーター**

* sessionstore: CQ_Analytics.SessionStore。 登録するセッションストアオブジェクト。

**戻り値**

戻り値はありません。

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

セッションストアのアクティベーションと登録をリッスンするためのメソッドを提供します。[セッションストアの定義および初期化の確認](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized)も参照してください。

### メソッド {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

セッションストアの初期化時に呼び出されるコールバック関数を登録します。 複数回初期化されたストアの場合は、コールバック関数が 1 回だけ呼び出されるように、コールバック遅延を指定します。

* 前回の初期化の遅延期間中にストアが初期化されると、以前の関数呼び出しがキャンセルされ、現在の初期化に対して関数が再び呼び出されます。
* 後続の初期化が発生する前に遅延期間が経過した場合、コールバック関数が 2 回実行されます。

例えば、セッションストアは JSON オブジェクトに基づいており、JSON リクエストで取得されます。 次の初期化シナリオが考えられます。

* リクエストが完了し、取得されたデータがストアに読み込まれます。 この場合、初期化は 1 回だけおこなわれます。
* リクエストが失敗しました（タイムアウト）。 この場合、初期化はおこなわれず、ストアにデータがありません。
* ストアには、デフォルト値（init プロパティ）が事前に設定されていますが、リクエストは失敗します（タイムアウト）。 デフォルト値を持つ初期化は 1 つだけです。
* ストアが事前に設定されています。

遅延が `true` または数ミリ秒の間、メソッドはコールバックメソッドを呼び出す前に待機します。 遅延が渡される前に別の初期化イベントがトリガーされた場合は、初期化イベントなしで遅延時間が経過するまで待ちます。 これにより、2 番目の初期化イベントがトリガーされるのを待機し、最適なケースでコールバック関数を呼び出すことができます。

**パラメーター**

* storeName: String。 リスナーを追加するセッションストアの名前。
* callback：関数。 ストアの初期化時に呼び出す関数。
* delay：ブール値または数値。 コールバック関数の呼び出しを遅延させる時間（ミリ秒）。 Boolean 値 `true` の場合、デフォルトの遅延 `200 ms` が使用されます。Boolean 値 `false` または負の数の場合、遅延は使用されません。

**戻り値**

戻り値はありません。

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

セッションストアが登録されたときに呼び出されるコールバック関数を登録します。ストアが [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr) に登録されると、登録イベントが発生します。

**パラメーター**

* storeName: String。 リスナーを追加するセッションストアの名前。
* callback：関数。 ストアの初期化時に呼び出す関数。

**戻り値**

戻り値はありません。

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

JSON データを含む、永続化されていないセッションストア。 データは外部の JSONP サービスから取得されます。 `getInstance` メソッドまたは `getRegisteredInstance` メソッドを使用して、このクラスのインスタンスを作成します。

CQ_Analytics.JSONStore を拡張します。

### プロパティ {#properties}

継承されたプロパティについては、 CQ_Analytics.JSONStore および CQ_Analytics.SessonStore を参照してください。

### メソッド {#methods-2}

継承されたメソッドについては、 CQ_Analytics.JSONStore および CQ_Analytics.SessonStore も参照してください。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

CQ_Analytics.JSONPStore オブジェクトを作成します。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。 storeName を指定しない場合、このメソッドは null を返します。
* serviceURL：文字列。 JSONP サービスの URL
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* deferLoading: （オプション）ブール値。 値が true の場合は、オブジェクト作成時に JSONP サービスが呼び出されなくなります。 値が false の場合、JSONP サービスが呼び出されます。
* loadingCallback：（オプション）文字列。JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

新しい CQ_Analytics.JSONPStore オブジェクト、または storeName が Null の場合は Null。

#### getServiceURL() {#getserviceurl}

このオブジェクトが JSON データの取得に使用する JSONP サービスの URL を取得します。

**パラメーター**

なし。

**戻り値**

サービス URL を表す String 値。サービス URL が設定されていない場合は null です。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

JSONP サービスを呼び出します。 JSONP の URL は、指定されたコールバック関数名が後ろに付いたサービス URL です。

**パラメーター**

* serviceURL: （オプション）文字列。 呼び出す JSONP サービス。 値 null を指定すると、既に設定されているサービス URL が使用されます。 null 以外の値は、このオブジェクトに使用する JSONP サービスを設定します。 （ setServiceURL を参照）。
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* callback: （オプション）String。 JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

CQ_Analytics.JSONPStore オブジェクトを作成し、ストアを ClientContext に登録します。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。 storeName を指定しない場合、このメソッドは null を返します。
* serviceURL: （オプション）文字列。 JSONP サービスの URL。
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* callback: （オプション）String。 JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

登録済みの CQ_Analytics.JSONPStore オブジェクト。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

JSON データの取得に使用する JSONP サービスの URL を設定します。

**パラメーター**

* serviceURL：文字列。 JSON データを提供する JSONP サービスの URL

**戻り値**

戻り値はありません。

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

JSON オブジェクトのコンテナ。JSON データを含む非永続セッションストアを作成するために、このクラスのインスタンスを作成します。

`myjsonstore = new CQ_Analytics.JSONStore`

初期化時にストアに入力されるデータのセットを定義できます。

CQ_Analytics.SessionStore を拡張します。

### プロパティ {#properties-1}

#### STOREKEY {#storekey}

ストアを識別するキー。 この値を取得するには、`getInstance` メソッドを使用します。

#### STORENAME {#storename}

ストアの名前。この値を取得するには、`getInstance` メソッドを使用します。

### メソッド {#methods-3}

継承されたメソッドについては、 CQ_Analytics.SessionStore も参照してください。

#### clear() {#clear}

セッションストアのデータを削除し、すべての初期化プロパティを削除します。

**パラメーター**

なし。

**戻り値**

戻り値はありません。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

指定された名前で CQ_Analytics.JSONStore オブジェクトを作成し、指定された JSON データで初期化します（ initJSON メソッドを呼び出します）。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData: Object. JSON データを格納したオブジェクト。

**戻り値**

CQ_Analytics.JSONStore オブジェクト。

#### getJSON() {#getjson}

セッションストアのデータを JSON 形式で取得します。

**パラメーター**

なし。

**戻り値**

JSON 形式のストアデータを表すオブジェクト。

#### init() {#init}

セッションストアをクリアし、初期化プロパティで初期化します。 初期化フラグを `true` に設定し、`initialize` イベントと `update` イベントを発生させます。

**パラメーター**

なし。

**戻り値**

返されたデータはありません。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

JSON オブジェクトのデータから初期化プロパティを作成します。 必要に応じて、既存のすべての初期化プロパティを削除できます。

プロパティの名前は、JSON オブジェクト内のデータの階層から派生します。 次のコード例は、JSON オブジェクトを表しています。

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

この例では、次のプロパティがストアに作成されます。

```xml
A: "valueA"
B/B1: "valueBB1"
```

**パラメーター**

* jsonData：保存するデータを格納する JSON オブジェクト。
* doNotClear：値が true の場合、既存の初期化プロパティが保持され、JSON オブジェクトから派生した初期化プロパティが追加されます。値が false の場合、既存の初期化プロパティを削除してから、JSON オブジェクトから得た初期化プロパティが追加されます。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

指定された名前で CQ_Analytics.JSONStore オブジェクトを作成し、指定された JSON データで初期化します（ initJSON メソッドを呼び出します）。 新しいオブジェクトは、Clickstream Cloud Manager に自動的に登録されます。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData: Object. JSON データを格納したオブジェクト。

**戻り値**

CQ_Analytics.JSONStore オブジェクト。

## CQ_Analytics.Observable {#cq-analytics-observable}

イベントを発生させ、他のオブジェクトがこれらのイベントと反応をリッスンできるようにします。 このクラスを拡張するクラスは、リスナーを呼び出すイベントを発生させることができます。

### メソッド {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

イベントのリスナーを登録します。 関連トピック [セッションストアの更新に反応するリスナーの作成](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**パラメーター**

* event:String。 リッスンするイベントの名前。
* fct：関数。 イベントの発生時に呼び出される関数。
* scope：（オプション）オブジェクト。ハンドラー関数を実行するスコープ。 ハンドラー関数の「this」コンテキスト。

**戻り値**

戻り値はありません。

#### removeListener(event, fct) {#removelistener-event-fct}

イベントに対して指定されたイベントハンドラを削除します。

**パラメーター**

* event:String。 イベントの名前。
* fct：関数。 イベントハンドラー。

**戻り値**

戻り値はありません。

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

リモート JSONP サービスから取得された JSON オブジェクトの永続コンテナです。

CQ_Analytics.PersistedJSONStore を拡張します。

### メソッド {#methods-5}

継承されたメソッドについては、 CQ_Analytics.PersistedJSONStore も参照してください。

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

CQ_Analytics.PersistedJSONPStore オブジェクトを作成します。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。 storeName を指定しない場合、このメソッドは null を返します。
* serviceURL：文字列。 JSONP サービスの URL
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* deferLoading: （オプション）ブール値。 値が true の場合は、オブジェクト作成時に JSONP サービスが呼び出されなくなります。 値が false の場合、JSONP サービスが呼び出されます。
* loadingCallback：（オプション）文字列。JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

新しい CQ_Analytics.PersistedJSONPStore オブジェクト、または storeName が Null の場合は Null。

#### getServiceURL() {#getserviceurl-1}

このオブジェクトが JSON データの取得に使用する JSONP サービスの URL を取得します。

**パラメーター**

なし。

**戻り値**

サービス URL を表す String 値。サービス URL が設定されていない場合は null です。

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

JSONP サービスを呼び出します。 JSONP の URL は、指定されたコールバック関数名が後ろに付いたサービス URL です。

**パラメーター**

* serviceURL: （オプション）文字列。 呼び出す JSONP サービス。 値 null を指定すると、既に設定されているサービス URL が使用されます。 null 以外の値は、このオブジェクトに使用する JSONP サービスを設定します。 （ setServiceURL を参照）。
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* callback: （オプション）String。 JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

CQ_Analytics.PersistedJSONPStore オブジェクトを作成し、ストアを ClientContext に登録します。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。 storeName を指定しない場合、このメソッドは null を返します。
* serviceURL: （オプション）文字列。 JSONP サービスの URL。
* dynamicData: （オプション）Object。 コールバック関数が呼び出される前に、ストアの初期化データに追加される JSON データ。
* callback: （オプション）String。 JSONP サービスが返す JSONP オブジェクトを処理するために呼び出す関数の名前。 コールバック関数は、CQ_Analytics.JSONPStore オブジェクトである 1 つのパラメーターを定義する必要があります。

**戻り値**

登録済みの CQ_Analytics.PersistedJSONPStore オブジェクト。

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

JSON データの取得に使用する JSONP サービスの URL を設定します。

**パラメーター**

* serviceURL：文字列。 JSON データを提供する JSONP サービスの URL

**戻り値**

戻り値はありません。

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

JSON オブジェクトの永続的なコンテナ。

`CQ_Analytics.PersistedSessionStore` を拡張します。

### プロパティ {#properties-2}

#### STOREKEY {#storekey-1}

ストアを識別するキー。 この値を取得するには、`getInstance` メソッドを使用します。

#### STORENAME {#storename-1}

ストアの名前。この値を取得するには、`getInstance` メソッドを使用します。

### メソッド {#methods-6}

継承されたメソッドについては、 CQ_Analytics.PersistedSessionStore も参照してください。

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

指定された名前で CQ_Analytics.PersistedJSONStore オブジェクトを作成し、指定された JSON データで初期化します（ initJSON メソッドを呼び出します）。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData: Object. JSON データを格納したオブジェクト。

**戻り値**

CQ_Analytics.PersistedJSONStore オブジェクト。

#### getJSON() {#getjson-1}

セッションストアのデータを JSON 形式で取得します。

**パラメーター**

なし。

**戻り値**

JSON 形式のストアデータを表すオブジェクト。

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

JSON オブジェクトのデータから初期化プロパティを作成します。 必要に応じて、既存のすべての初期化プロパティを削除できます。

プロパティの名前は、JSON オブジェクト内のデータの階層から派生します。 次のコード例は、JSON オブジェクトを表しています。

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

この例では、次のプロパティがストアに作成されます。

```xml
A: "valueA"
B/B1: "valueBB1"
```

**パラメーター**

* jsonData：保存するデータを格納する JSON オブジェクト。
* doNotClear：値が true の場合、既存の初期化プロパティが保持され、JSON オブジェクトから派生した初期化プロパティが追加されます。値が false の場合、既存の初期化プロパティを削除してから、JSON オブジェクトから得た初期化プロパティが追加されます。

**戻り値**

戻り値はありません。

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

指定された名前で CQ_Analytics.PersistedJSONStore オブジェクトを作成し、指定された JSON データで初期化します（ initJSON メソッドを呼び出します）。 新しいオブジェクトは、ClientContext Manager に自動的に登録されます。

**パラメーター**

* storeName: String。 STORENAME プロパティとして使用する名前です。 STOREKEY プロパティの値は、すべて大文字で storeName に設定されます。
* jsonData: Object. JSON データを格納したオブジェクト。

**戻り値**

CQ_Analytics.PersistedJSONStore オブジェクト。

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

プロパティと値のコンテナ。 データは CQ_Analytics.SessionPersistence を使用して永続化されます。永続セッションストアを作成するには、このクラスのインスタンスを作成します。

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

CQ_Analytics.SessionStore を拡張します。

### プロパティ {#properties-3}

#### STOREKEY {#storekey-2}

デフォルト値は `key` です。

### メソッド {#methods-7}

継承されたメソッドについては、 CQ_Analytics.SessionStore を参照してください。

継承されるメソッド `clear`、`setProperty`、`setProperties`、`removeProperty` を使用してストアデータを変更すると、変更されたプロパティに notPersisted というフラグが設定されない限り、変更内容が自動的に保持されます。

#### getStoreKey() {#getstorekey}

`STOREKEY` プロパティを取得します。

**パラメーター**

なし

**戻り値**

`STOREKEY` プロパティの値。

#### isPersisted(name) {#ispersisted-name}

データプロパティが永続化されるかどうかを指定します。

**パラメーター**

* name: String。 プロパティの名前。

**戻り値**

値が永続プロパティの場合は Boolean 値 `true`、永続プロパティではない場合は値 `false`。

#### persist() {#persist}

セッションストアを保持します。 デフォルトの永続モードでは、`ClientSidePersistence` を名前として使用するブラウザーの `localStorage` を使用します（`window.localStorage.set("ClientSidePersistance", store);`）。

localStorage が使用できない、または書き込めない場合、ストアはウィンドウのプロパティとして永続化されます。

完了時に `persist` イベントを発生させます。

**パラメーター**

なし

**戻り値**

戻り値はありません。

#### reset(deferEvent) {#reset-deferevent}

ストアからすべてのデータプロパティを削除し、ストアを保持します。 オプションで、完了時に `udpate` イベントを発生させません。

**パラメーター**

* deferEvent：値が true の場合は、`update` イベントを発生させないようにします。値が `false` の場合は、update イベントを発生させます。

**戻り値**

戻り値はありません。

#### setNonPersisted(name) {#setnonpersisted-name}

データプロパティに非永続的なフラグを設定します。

**パラメーター**

* name: String。 永続化しないプロパティの名前。

**戻り値**

戻り値はありません。

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore は、セッションストアを表します。 このクラスのインスタンスを作成して、セッションストアを作成します。

`mystore = new CQ_Analytics.SessionStore`

CQ_Analytics.Observable を拡張します。

### プロパティ {#properties-4}

#### STORENAME {#storename-2}

セッションストアの名前。 getName を使用して、このプロパティの値を取得します。

### メソッド {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

プロパティと値をセッションストア初期化データに追加します。

loadInitProperties を使用して、初期化値をセッションストアデータに設定します。

**パラメーター**

* name: String。 追加するプロパティの名前。
* value: String。 追加するプロパティの値。

**戻り値**

戻り値はありません。

#### clear() {#clear-1}

ストアからすべてのデータプロパティを削除します。

**パラメーター**

なし。

**戻り値**

戻り値はありません。

#### getData(excluded) {#getdata-excluded}

ストアデータを返します。 オプションで、名前プロパティをデータから除外します。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

excluded: （オプション）返されるデータから除外するプロパティ名の配列。

**戻り値**

プロパティとその値のオブジェクト。

#### getInitProperty(name) {#getinitproperty-name}

データプロパティの値を取得します。

**パラメーター**

* name: String。 取得するデータプロパティの名前。

**戻り値**

データプロパティの値。 指定された名前のプロパティがセッションストアに格納されていない場合は `null` を返します。

#### getName() {#getname}

セッションストアの名前を返します。

**パラメーター**

なし。

**戻り値**

ストア名を表す String 値です。

#### getProperty(name, raw) {#getproperty-name-raw}

プロパティの値を返します。 値は、未加工のプロパティまたは XSS フィルタリングされた値として返されます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name: String。 取得するデータプロパティの名前。
* raw：ブール値。 値が true の場合、生のプロパティ値が返されます。 値が false の場合、返される値を XSS フィルターします。

**戻り値**

データプロパティの値。

#### getPropertyNames(excluded) {#getpropertynames-excluded}

セッションストアに格納されているプロパティの名前を返します。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

excluded: （オプション）結果から除外するプロパティ名の配列。

**戻り値**

セッションプロパティ名を表す String 値の配列です。

#### getSessionStore() {#getsessionstore}

現在のオブジェクトに関連付けられたセッションストアを返します。

**パラメーター**

なし。

**戻り値**

この

#### init() {#init-1}

ストアを初期化済みとしてマークし、`initialize` イベントを発生させます。

**パラメーター**

なし。

**戻り値**

戻り値はありません。

#### isInitialized() {#isinitialized}

セッションストアが初期化されるかどうかを示します。

**パラメーター**

なし。

**戻り値**

ストアが初期化されている場合は値 `true`、ストアが初期化されていない場合は値 `false`。

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

特定のオブジェクトのプロパティをセッションストアの初期化データに追加します。 必要に応じて、オブジェクトデータもストアデータに追加されます。

**パラメーター**

* obj：可算プロパティを格納したオブジェクト。
* setValues: true の場合、ストアデータに同じ名前のプロパティがまだ含まれていない場合、obj プロパティがセッションストアデータに追加されます。 false の場合、データはセッションストアデータに追加されません。

**戻り値**

戻り値はありません。

#### removeProperty(name) {#removeproperty-name}

セッションストアからプロパティを削除します。 完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name: String。 削除するプロパティの名前。

**戻り値**

戻り値はありません。

#### reset() {#reset}

データストアの初期値を復元します。 デフォルトの実装では、すべてのデータが削除されるだけです。 完了時に `update` イベントを発生させます。

**パラメーター**

なし。

**戻り値**

戻り値はありません。

#### setProperties(properties) {#setproperties-properties}

複数のプロパティの値を設定します。完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* プロパティ：オブジェクト。 可算プロパティを含むオブジェクト。 各プロパティ名と値がストアに追加されます。

**戻り値**

戻り値はありません。

#### setProperty(name, value) {#setproperty-name-value}

プロパティの値を設定します。 完了時に `update` イベントを発生させます。ストアのデータプロパティが存在しない場合は、`init` メソッドを呼び出します。

**パラメーター**

* name: String。 プロパティの名前。
* value: String。 プロパティの値。

**戻り値**

戻り値はありません。
