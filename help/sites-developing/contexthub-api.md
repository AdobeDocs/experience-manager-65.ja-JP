---
title: ContextHub JavaScript API リファレンス
seo-title: ContextHub JavaScript API リファレンス
description: ContextHub コンポーネントをページに追加すると、ContextHub JavaScript API がスクリプトで使用できるようになります
seo-description: ContextHub コンポーネントをページに追加すると、ContextHub JavaScript API がスクリプトで使用できるようになります
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '5029'
ht-degree: 80%

---


# ContextHub JavaScript API リファレンス{#contexthub-javascript-api-reference}

[ContextHub コンポーネントをページに追加](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component)すると、ContextHub JavaScript API がスクリプトで使用できるようになります。

## ContextHub 定数 {#contexthub-constants}

ContextHub JavaScript API によって定義される定数値です。

### イベント定数 {#event-constants}

ContextHub ストアに対して発生する名前付きイベントを次の表に示します。[ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) も参照してください。

| 定数 | 説明 | 値 |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | ContextHubのイベント名前空間 | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | 必要なすべてのストアが登録、初期化され、使用可能な状態であることを示す | 全店舗対応の |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | 指定されたタイムアウト内に一部のストアが初期化されなかったことを示す | 部分的に準備された |
| ContextHub.Constants.EVENT_STORE_REGISTERED | ストアの登録時に発生します | 店舗登録の |
| ContextHub.Constants.EVENT_STORE_READY | ストアが動作する準備ができていることを示します。 JSONP ストア（データが取得されると実行される）を除き、登録後すぐにトリガーされる。 | 店舗対応の |
| ContextHub.Constants.EVENT_STORE_UPDATED | ストアが永続性を更新した場合に発生します | 店舗で更新された |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | 永続性コンテナ名 | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | 生のJSON結果が保存される特定の永続性キー名を格納します | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | JSONデータがフェッチされた日時を示す特定のタイムスタンプを格納します | /_/response-time |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | 前回の呼び出しで使用されたJSONサービスの特定のURLを格納 | /_/URL |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | ContextHubのUIが展開されているかどうかを示します | /_/コンテナ拡張 |

### UI イベント定数 {#ui-event-constants}

次の表に、ContextHub UI に関して発生するイベントの名前を示します。

| **定数** | **説明** | **値** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | モードが登録されたときに発生します | ui-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | モードが未登録の場合に発生します | ui-mode-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | モードレンダラーが登録されたときに発生します | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | モードレンダラーの登録が解除されると発生します | ui-mode-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | 新しいモードが追加されたときに発生します | ui-modeが追加された |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | モードが削除されたときに発生します | ui-mode-removed |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | ユーザーがモードを選択した場合に呼び出されます | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | 新しいモジュールが登録されたときに発生します | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | モジュールの登録を解除すると発生します | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | モジュールレンダラーが登録されたときに発生します | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | モジュールレンダラーの登録が解除されたときに発生します | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | 新しいモジュールが追加されたときに発生します | ui-moduleが追加された |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | モジュールが削除されたときに発生します | ui-module-removed |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | UIコンテナがページに追加されたときに発生します | ui-コンテナが追加した |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | ContextHub UIが開かれたときに発生します | ui-コンテナが開いた |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | ContextHub UIが折りたたまれている場合に発生します | ui-コンテナ閉 |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | プロパティが変更された場合に発生します | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | ContextHub UIがレンダリングされるたび（例：プロパティの変更後）に実行されます | ui-rendered |
| ContextHub.Constants.EVENT_UI_INITIALIZED | UIコンテナが初期化されたときに発生します | ui-initialized |
| ContextHub.Constants.ACTIVE_UI_MODE | アクティブなUIモードを示します。 | /_/active-ui-mode |

## ContextHub JavaScript API リファレンス {#contexthub-javascript-api-reference-2}

ContextHub オブジェクトを使用して、すべてのストアにアクセスできます。

### 関数（ContextHub） {#functions-contexthub}

#### getAllStores() {#getallstores}

登録されている ContextHub ストアをすべて返します。

この関数にパラメーターはありません。

**戻り値**

すべての ContextHub ストアを格納したオブジェクト。各ストアは、ストアと同じ名前を使用するオブジェクトです。

**例**

次の例では、すべてのストアを取得してから、geolocation ストアを取得しています。

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

ストアを JavaScript オブジェクトとして取得します。

**パラメーター**

* **name：**&#x200B;ストアが登録された名前。

**戻り値**

ストアを表すオブジェクト。

**例**

次の例では、geolocation ストアを取得します。

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

ContextHub セグメントを表します。ContextHub.SegmentEngine.SegmentManager を使用して、セグメントを取得します。

### 関数（ContextHub.ContextEngine.Segment） {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

セグメント名を String 値として返します。

#### getPath() {#getpath}

セグメント定義のリポジトリパスを String 値として返します。

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

ContextHub セグメントへのアクセスを提供します。

### 関数（ContextHub.SegmentEngine.SegmentManager） {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

現在のコンテキストで解決されたセグメントを返します。この関数にパラメーターはありません。

**戻り値**

ContextHub.SegmentEngine.Segment オブジェクトの配列。

## ContextHub.Store.Core {#contexthub-store-core}

ContextHub ストアのベースクラス。

### Properties (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### eventing {#eventing}

[ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) オブジェクト。このオブジェクトを使用して、関数をストアイベントにバインドします。For information about the default value and initialization, see [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

ストアの名前。

#### persistence {#persistence}

ContextHub.Utils.Persistence オブジェクト。For information about the default value and initialization, see `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Functions (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

データオブジェクトまたは配列とストアデータを結合します。オブジェクトのキーと値の各ペアまたは配列が（`setItem` 関数を使用して）ストアに追加されます。

* **オブジェクト：** キーはプロパティ名です。
* **配列：** キーは配列インデックスです。

値にオブジェクトを使用できます。

**パラメーター**

* **tree：**（Object または Array）ストアに追加するデータ。
* **options：**（Object）setItem 関数に渡すオプションからなる任意のオブジェクト。詳しくは、`options`setItem(key,value,)[ の ](/help/sites-developing/contexthub-api.md#setitem-key-value-options)options パラメーターを参照してください。

**戻り値**

値 `boolean` :

* 値 `true` は、データオブジェクトが保存されたことを示します。
* 値 `false` は、データストアが変更されていないことを示します。

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

1 つのキーから別のキーへの参照を作成します。キーは自分自身を参照できません。

**パラメーター**

* **key：**`anotherKey` を参照するキー。

* **anotherkey：**`key` に参照されるキー。

**戻り値**

値 `boolean` :

* 値 `true` は、参照が追加されたことを示します。
* 値 `false` は、参照が追加されなかったことを示します。

#### announceReadiness() {#announcereadiness}

このストアに対する `ready` イベントを発生させます。この関数にパラメーターはなく、値を返しません。

#### clean() {#clean}

すべてのデータをストアから削除します。この関数にパラメーターおよび戻り値はありません。

#### getItem(key) {#getitem-key}

キーに関連付けられている値を返します。

**パラメーター**

* **key：**（String）値を返すキー。

**戻り値**

キーの値を表すオブジェクト。

#### getKeys(includeInternals) {#getkeys-includeinternals}

ストアからキーを取得します。オプションで、ContextHub フレームワークが内部的に使用するキーを取得できます。

**パラメーター**

* **includeInternals：**&#x200B;値 `true` は、内部的に使用されているキーを結果に含めます。このようなキーは、アンダースコア（&quot;_&quot;）文字で始まります。デフォルト値は `false` です。

**戻り値**

キー名（`string` 値）の配列。

#### getReferences() {#getreferences}

ストアから参照を取得します。

**戻り値**

参照キーを参照キーのインデックスとして使用する配列：

* Referencing keys correspond with the `key` parameter of the `addReference` function.

* Referenced keys correspond with the `anotherKey` parameter of the `addReference` function.

#### getTree(includeInternals) {#gettree-includeinternals}

データツリーをストアから取得します。オプションで、ContextHub フレームワークが内部的に使用しているキーと値のペアを含めることができます。

**パラメーター**

* `includeInternals:` の値は、内部的に使用されたキーと値のペアを結果に `true` 含めます。 このデータのキーは、アンダースコア（&quot;_&quot;）文字で始まります。デフォルト値は `false` です。

**戻り値**

データツリーを表すオブジェクト。キーは、オブジェクトのプロパティ名です。

#### init(name, config) {#init-name-config}

ストアを初期化します。

* ストアデータを空のオブジェクトに設定します。
* ストア参照を空のオブジェクトに設定します。
* The eventChannel is data:*name*, where *name* is the store name.

* storeDataKey は /store/*name* です。*name* はストア名です。

**パラメーター**

* **name：**&#x200B;ストアの名前。
* **config：**&#x200B;設定プロパティを格納したオブジェクト。

   * eventDeferring：デフォルト値は 32 です。
   * eventing：このストアの [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) オブジェクト。デフォルト値は ContextHub.eventing オブジェクトです。
   * persistence：このストアの ContextHub.Utils.Persistence オブジェクト。デフォルト値は ContextHub.persistence オブジェクトです。

#### isEventingPaused() {#iseventingpaused}

このストアに対するイベンティングが一時停止されているかどうかを判断します。

**戻り値**

次の boolean 値。

* `true`：イベンティングが一時停止されているので、このストアに対するイベントは発生しません。
* `false`：イベンティングが一時停止されていないので、このストアに対するイベントが発生します。

#### pauseEventing() {#pauseeventing}

このストアに対するイベンティングを一時停止して、イベントが発生しないようにします。この関数にパラメーターは必要なく、値を返しません。

#### removeItem(key, options) {#removeitem-key-options}

キーと値のペアをストアから削除します。

キーが削除されると、この関数が `data` イベントを発生させます。イベントデータには、ストア名、削除されたキーの名前、削除された値、キーの新しい値(null)、およびアクションタイプ「remove」が含まれます。

オプションで、`data` イベントを発生させないようにすることができます。

**パラメーター**

* **key：**（String）削除するキーの名前。
* **options：**（Object）オプションからなるオブジェクト。次のオブジェクトプロパティが有効です。

   * silent：値 `true` は、`data` イベントが発生しないようにします。デフォルト値は `false` です。

**戻り値**

値 `boolean` :

* A value of `true` indicates the key/value pair was removed.
* A value of `false` indicates that the data store is unchanged because the key was not found in the store.

#### removeReference(key) {#removereference-key}

参照をストアから削除します。

**パラメーター**

* **key：**&#x200B;削除するキー参照。This parameter corresponds with the `key` parameter of the `addReference` function.

**戻り値**

値 `boolean` :

* A value of `true` indicates the reference was removed.
* A value of `false` indicates that the key was not valid and the store is unchanged.

#### reset(keepRemainingData) {#reset-keepremainingdata}

ストアの永続データの初期値を再設定します。オプションで、その他すべてのデータをストアから削除できます。ストアが再設定されている間、このストアに対するイベンティングは一時停止されます。この関数は値を返しません。

初期値は、ストアオブジェクトのインスタンス化に使用される config オブジェクトの initialValues プロパティで提供されます。

**パラメーター**

* **keepRemainingData：**（Boolean）値が true の場合、初期値以外のデータは保持されます。値が false の場合、初期値以外のすべてのデータが削除されます。

ストアの永続データの初期値を再設定します。オプションで、その他すべてのデータをストアから削除できます。ストアが再設定されている間、このストアに対するイベンティングは一時停止されます。この関数は値を返しません。

初期値は、ストアオブジェクトのインスタンス化に使用される config オブジェクトの initialValues プロパティで提供されます。

**パラメーター**

* keepRemainingData：（Boolean）値が true の場合、初期値以外のデータは保持されます。値が false の場合、初期値以外のすべてのデータが削除されます。

#### resolveReference(key, retry) {#resolvereference-key-retry}

被参照キーを取得します。オプションで、最良一致の解決に使用する繰り返し回数を指定できます。

**パラメーター**

* **key：**（String）参照を解決するためのキー。This `key` parameter corresponds with the `key` parameter of the `addReference` function.

* **retry：**（Number）使用する繰り返し回数。

**戻り値**

被参照キーを表す `string` 値。参照が解決されない場合は、`key` パラメーターの値が返されます。

#### resumeEventing() {#resumeeventing}

このストアに対するイベンティングを再開し、イベントが発生するようにします。この関数はパラメーターを定義せず、値を返しません。

#### setItem(key, value, options) {#setitem-key-value-options}

キーと値のペアをストアに追加します。

キーの値がそのキーに対して現在保存されている値と異なる場合にのみ `data` イベントを発生させます。オプションで、`data` イベントを発生させないようにすることができます。

イベントデータには、ストア名、キー、前の値、新しい値およびアクションタイプ `set` が含まれます。

**パラメーター**

* **key：**（String）キーの名前。
* **options：**（Object）オプションからなるオブジェクト。次のオブジェクトプロパティが有効です。

   * silent：値 `true` は、`data` イベントが発生しないようにします。デフォルト値は `false` です。

* **value：**（Object）キーに関連付ける値。

**戻り値**

値 `boolean` :

* 値 `true` は、データオブジェクトが保存されたことを示します。
* 値 `false` は、データストアが変更されていないことを示します。

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

JSON データを格納するストア。データは外部の JSONP サービスから取得されるか、オプションで JSON データを返すサービスから取得されます。このクラスのインスタンスを作成する際に、[`init`](/help/sites-developing/contexthub-api.md#init-name-config) 関数を使用してサービスの詳細を指定します。

ストアは、インメモリパーシスタンス（JavaScript 変数）を使用します。ストアデータは、ページが持続している間のみ使用可能です。

ContextHub.Store.JSONPStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) and inherits the functions of that class.

### Functions (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

このオブジェクトが使用する JSONP サービスへの接続の詳細を設定します。既存の設定を更新または置換できます。この関数は値を返しません。

**パラメーター**

* **serviceConfig：**&#x200B;次のプロパティを格納したオブジェクト。

   * host：（String）サーバーの名前または IP アドレス。
   * jsonp：（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。true の場合、{callback: &quot;ContextHub.Callbacks.*Object.name*} オブジェクトが service.params オブジェクトに追加されます。
   * params:（オブジェクト）オブジェクトプロパティとして表されるURLパラメーター。 パラメーター名はプロパティ名で、パラメーター値はプロパティ値です。
   * path：（String）サービスへのパス。
   * port：（Number）サービスのポート番号。
   * secure：（String または Boolean）サービス URL に使用するプロトコルを決定します。

      * auto: //
      * true：https://
      * false:https://

* **override：**（Boolean）A value of `true` causes the existing service configuration to be replaced by the properties of `serviceConfig`. A value of `false` causes the existing service configuration properties to be merged with the properties of `serviceConfig`.

#### getRawResponse() {#getrawresponse}

JSONP サービスへの最後の呼び出し以降キャッシュされている未加工の応答を返します。この関数にパラメーターは必要ありません。

**戻り値**

未加工の応答を表すオブジェクト。

#### getServiceDetails() {#getservicedetails}

この ContextHub.Store.JSONPStore オブジェクトのサービスオブジェクトを取得します。サービスオブジェクトには、サービス URL を作成するのに必要なすべての情報が格納されています。

**戻り値**

次のプロパティを持つオブジェクト。

* **host：**（String）サーバーの名前または IP アドレス。
* **jsonp：**（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。true の場合、{callback: &quot;ContextHub.Callbacks.*Object.name*} オブジェクトが service.params オブジェクトに追加されます。

* **params:** （オブジェクト）オブジェクトプロパティとして表されるURLパラメーター。 パラメーター名はプロパティ名で、パラメーター値はプロパティ値です。
* **path：**（String）サービスへのパス。
* **port：**（Number）サービスのポート番号。
* **secure：**（String または Boolean）サービス URL に使用するプロトコルを決定します。

   * auto: //
   * true：https://
   * false:https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

JSONP サービスの URL を取得します。

**パラメーター**

* **resolve：**（Boolean）解決されたパラメーターを URL に含めるかどうかを判断します。A value of `true` resolves parameters, and `false` does not.

**戻り値**

サービス URL を表す `string` 値。

#### init(name, config) {#init-name-config-1}

ContextHub.Store.JSONPStore オブジェクトを初期化します。

**パラメーター**

* **name：**（String）ストアの名前。
* **config：**（Object）サービスプロパティを格納するオブジェクト。JSONPStore オブジェクトは、`service` オブジェクトのプロパティを使用して、JSONP サービスの URL を組み立てます。

   * eventDeferring：32
   * eventing：このストアの ContextHub.Utils.Eventing オブジェクト。デフォルト値は `ContextHub.eventing` オブジェクトです。
   * persistence：このストアの ContextHub.Utils.Persistence オブジェクト。デフォルトでは、メモリパーシスタンスが使用されます（JavaScript オブジェクト）。
   * サービス：（オブジェクト）

      * host：（String）サーバーの名前または IP アドレス。
      * jsonp：（Boolean）値 true はサービスが JSONP サービスであることを示します。それ以外は false です。trueの場合、 `{callback: "ContextHub.Callbacks.*Object.name*}`オブジェクトはに追加され `service.params`ます。
      * params:（オブジェクト）オブジェクトプロパティとして表されるURLパラメーター。 パラメーターの名前と値は、それぞれオブジェクトのプロパティの名前と値です。
      * path：（String）サービスへのパス。
      * port：（Number）サービスのポート番号。
      * secure：（String または Boolean）サービス URL に使用するプロトコルを決定します。

         * auto: //
         * true：https://
         * false:https://
      * timeout：（Number）タイムアウトまでに JSONP サービスの応答を待機する時間（ミリ秒単位）。
      * ttl：JSONP サービスの最小呼び出し間隔（ミリ秒単位）。（[queryService](/help/sites-developing/contexthub-api.md#queryservice-reload) 関数を参照）。


#### queryService(reload) {#queryservice-reload}

リモート JSONP サービスをクエリーし、応答をキャッシュします。If the amount of time since the previous call to this function is less than the value of `config.service.ttl`, the service is not called and the cached response is not changed. オプションで、サービスを強制的に呼び出すことができます。`config.service.ttl` プロパティは、ストアを初期化するために [init](/help/sites-developing/contexthub-api.md#init-name-config) 関数を呼び出すと設定されます。

クエリーが完了すると、ready イベントが発生します。JSONP サービス URL が設定されていない場合、この関数は何もしません。

**パラメーター**

* **reload：**（Boolean）値が true の場合、キャッシュされた応答を削除し、JSONP サービスを強制的に呼び出します。

#### reset {#reset}

ストアの永続データを初期値にリセットしてから、JSONP サービスを呼び出します。オプションで、その他すべてのデータをストアから削除できます。初期値が再設定されている間、このストアに対するイベンティングは一時停止されます。この関数は値を返しません。

初期値は、ストアオブジェクトのインスタンス化に使用される config オブジェクトの initialValues プロパティで提供されます。

**パラメーター**

* **keepRemainingData：**（Boolean）値が true の場合、初期値以外のデータは保持されます。値が false の場合、初期値以外のすべてのデータが削除されます。

#### resolveParameter(f) {#resolveparameter-f}

指定されたパラメーターを解決します。

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore は [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) を拡張したものなので、このクラスのすべての関数を継承しています。ただし、JSONP サービスから取得されるデータは、ContextHub の永続性に応じて保持されます(See [Persistence Modes](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) so it inherits all of the functions of that class. このストアのデータは、ContextHub の永続性の設定に応じて保持されます。

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) so it inherits all of the functions of that class. このストアのデータは、インメモリパーシスタンス（JavaScript オブジェクト）を使用して保持されます。

## ContextHub.UI {#contexthub-ui}

UI モジュールおよび UI モジュールレンダラーを管理します。

### 関数（ContextHub.UI） {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

UI モジュールレンダラーを ContextHub に登録します。登録後、レンダラーを使用して [UI モジュールを作成](/help/sites-administering/contexthub-config.md#adding-a-ui-module)できます。[ContextHub.UI.BaseModuleRenderer を拡張](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)してカスタム UI モジュールレンダラーを作成する場合は、この関数を使用します。

**パラメーター**

* **moduleType：**（String）UI モジュールレンダラーの識別子。レンダラーが指定された値を使用して既に登録されている場合、このレンダラーが登録される前に、既存のレンダラーは登録されません。
* **renderer:** （文字列） UIモジュールをレンダリングするクラスの名前。
* **dontRender：**（Boolean）レンダラーの登録後に ContextHub UI がレンダリングされないようにするには、`true` に設定します。デフォルト値は `false` です。

**例**

次の例では、レンダラーを contexthub.browserinfo モジュールタイプとして登録します。

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

cookie とやり取りするユーティリティクラス。

### 関数（ContextHub.Utils.Cookie） {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

cookie が存在するかどうかを判断します。

**パラメーター**

* **key：**&#x200B;テストする cookie のキーを格納した `String`。

**戻り値**

`boolean` 値 true は、cookie が存在することを示します。

**例**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

フィルターに一致するキーを持つすべての cookie を返します。

**パラメーター**

* （オプション）**filter：** cookie のキーを照合する条件。すべての cookie を返すには、値を指定しないでください。次のタイプがサポートされています。

   * String：文字列を cookie のキーと比較します。
   * Array：配列内の各項目はフィルターです。
   * 正規表現オブジェクト：オブジェクトのテスト関数を使用して cookie のキーを照合します。
   * 関数：cookie のキーが一致するかどうかをテストする関数。関数は、cookie のキーをパラメーターとして取り、テストによって一致が確認された場合は true を返す必要があります。

**戻り値**

cookie からなるオブジェクト。オブジェクトのプロパティは cookie のキーで、キー値は cookie の値です。

**例**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

cookie の値を返します。

**パラメーター**

* **key：**&#x200B;値を取得する cookie のキー。

**戻り値**

cookie の値、またはそのキーの cookie が見つからなかった場合は `null`。

**例**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

フィルターに一致する既存の cookie のキーからなる配列を返します。

**パラメーター**

* **filter：** cookie のキーを照合する条件。次のタイプがサポートされています。

   * String：文字列を cookie のキーと比較します。
   * Array：配列内の各項目はフィルターです。
   * 正規表現オブジェクト：オブジェクトのテスト関数を使用して cookie のキーを照合します。
   * 関数：cookie のキーが一致するかどうかをテストする関数。関数は、cookie のキーをパラメーターとして取り、テストによって一致が確認された場合は `true` を返す必要があります。

**戻り値**

それぞれがフィルターに一致する cookie のキーである文字列からなる配列。

**例**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

cookie を削除します。cookie を削除するには、値を空の文字列に設定し、有効期限を現在の日付より前の日に設定します。

**パラメーター**

* **key：**&#x200B;削除する cookie のキーを表す `String` 値。

* **options：** cookie の属性を設定するプロパティ値を格納したオブジェクト。詳しくは、` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` 関数を参照してください。`expires` プロパティは無効です。

**戻り値**

この関数は値を返しません。

**例**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

指定されたキーと値の cookie を作成し、その cookie を現在のドキュメントに追加します。オプションで、cookie の属性を設定するオプションを指定できます。

**パラメーター**

* **key：** cookie のキーを格納した String。
* **value：** cookie の値を格納した String。
* **options：**（オプション）cookie の属性を設定する、次のいずれかのプロパティを格納したオブジェクト。

   * expires：cookie の有効期限を指定する `date` 値または `number` 値。date 値は、有効期限の絶対時間を指定します。number（日数）は、有効期限を現在時刻 + その日数に設定します。デフォルト値は `undefined` です。
   * ：cookie の `boolean`Secure 属性を指定する `Secure` 値。デフォルト値は `false` です。
   * ：cookie の `String`Path 属性として使用する `Path` 値。デフォルト値は `undefined` です。

**戻り値**

値が設定された cookie。

**例**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

指定されたフィルターに一致するすべての cookie を削除します。cookie は、getKeys 関数を使用して照合され、removeItem 関数を使用して削除されます。

**パラメーター**

* **：**`filter` 関数への呼び出しに使用する `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)`filter 引数。

* **：**`options` 関数への呼び出しに使用する `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)`options 引数。

**戻り値**

この関数は値を返しません。

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

関数を ContextHub ストアイベントにバインドおよびバインド解除できます。ストアの [eventing](/help/sites-developing/contexthub-api.md#eventing) プロパティを使用して、ストアの ContextHub.Utils.Eventing オブジェクトにアクセスします。

### 関数（ContextHub.Utils.Eventing） {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

イベントから関数をバインド解除します。

**パラメーター**

* **name:** 関数のバインドを解除するイベント [](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) の名前。

* **selector：**&#x200B;バインドを識別するセレクター(See the `selector` parameter for the [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) and [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) functions).

**戻り値**

この関数は値を返しません。

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

関数をイベントにバインドします。この関数は、イベントが発生するたびに呼び出されます。オプションで、過去にバインドが確立される前に発生したイベントに対して関数を呼び出すことができます。

**パラメーター**

* **name：**（String）関数をバインドする[イベントの名前](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing)。

* **handler：**（Function）イベントにバインドする関数。
* **selector:** （文字列）バインドの一意の識別子。 `off` 関数を使用してバインドを削除する場合は、セレクターでバインドを識別する必要があります。

* **triggerForPastEvents：**（Boolean）過去に発生したイベントに対してハンドラーを実行するかどうかを示します。値 `true` は、過去のイベントに対してハンドラーを呼び出します。値 `false` は、未来のイベントに対してハンドラーを呼び出します。デフォルト値は `true` です。

**戻り値**

`triggerForPastEvents` 引数が `true` の場合、この関数はイベントが過去に発生したかどうかを示す `boolean` 値を返します。

* `true`：イベントが過去に発生しており、ハンドラーが呼び出されます。
* `false`：イベントが過去に発生していません。

If `triggerForPastEvents` is `false`, this function returns no value.

**例**

次の例は、関数を位置情報ストアのデータイベントに連結します。 この関数は、ページ上の要素にストアの緯度データ項目の値を入力します。

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

関数をイベントにバインドします。関数は、最初に発生したイベントに対して一度だけ呼び出されます。オプションで、過去にバインドが確立される前に発生したイベントに対して関数を呼び出すことができます。

**パラメーター**

* **name：**（String）関数をバインドする[イベントの名前](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing)。

* **handler：**（Function）イベントにバインドする関数。
* **selector:** （文字列）バインドの一意の識別子。 `off` 関数を使用してバインドを削除する場合は、セレクターでバインドを識別する必要があります。

* **triggerForPastEvents：**（Boolean）過去に発生したイベントに対してハンドラーを実行するかどうかを示します。値 `true` は、過去のイベントに対してハンドラーを呼び出します。値 `false` は、未来のイベントに対してハンドラーを呼び出します。デフォルト値は `true` です。

**戻り値**

`triggerForPastEvents` 引数が `true` の場合、この関数はイベントが過去に発生したかどうかを示す `boolean` 値を返します。

* `true`：イベントが過去に発生しており、ハンドラーが呼び出されます。
* `false`：イベントが過去に発生していません。

If `triggerForPastEvents` is `false`, this function returns no value.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

オブジェクトが別のオブジェクトのプロパティとメソッドを継承できるようにするユーティリティクラス。

### 関数（ContextHub.Utils.inheritance） {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

オブジェクトに別のオブジェクトのプロパティとメソッドを継承させます。

**パラメーター**

* **child：**（Object）継承するオブジェクト。
* **parent：**（Object）継承するプロパティとメソッドを定義するオブジェクト。

## ContextHub.Utils.JSON {#contexthub-utils-json}

オブジェクトを JSON 形式にシリアライズし、JSON 文字列をオブジェクトにデシリアライズするための関数を提供します。

### 関数（ContextHub.Utils.JSON） {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

文字列値を JSON として解析し、JavaScript オブジェクトに変換します。

**パラメーター**

* **data：** JSON 形式の文字列値。

**戻り値**

JavaScript オブジェクト。

**例**

The code `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` returns the following object:

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

JavaScript の値およびオブジェクトを JSON 形式の文字列値にシリアライズします。

**パラメーター**

* **data：**&#x200B;シリアライズする値またはオブジェクト。この関数は、boolean、array、number、string および date 値をサポートします。

**戻り値**

シリアライズされた文字列値。When `data` is a R `egExp` value, this function returns an empty object. When `data` is a function, returns `undefined`.

**例**

次のコードは、 `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

このクラスは、ContextHub ストアに保存または ContextHub ストアから取得するデータオブジェクトの操作を容易にします。

### 関数（ContextHub.Utils.JSON.tree） {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

データオブジェクトのコピーを作成し、2 つ目のオブジェクトのデータツリーに追加します。この関数はコピーを返し、元のオブジェクトはどちらも変更されません。2 つのオブジェクトのデータツリーに同一のキーが含まれる場合、2 つ目のオブジェクトの値によって最初のオブジェクトの値が上書きされます。

**パラメーター**

* **tree:** コピーされるオブジェクトです。
* **secondTree:** オブジェクトのコピーと結合されるオブジェクト `tree` です。

**戻り値**

結合されたデータを格納したオブジェクト。

#### cleanup() {#cleanup}

オブジェクトのコピーを作成し、値を含まないか、null 値または undefined 値を含むデータツリーの項目を探して削除し、コピーを返します。

**パラメーター**

* **tree：**&#x200B;クリーンアップするオブジェクト。

**戻り値**

クリーンアップされたツリーのコピー。

#### getItem() {#getitem}

キーに対する値をオブジェクトから取得します。

**パラメーター**

* **tree：**&#x200B;データオブジェクト。
* **key：**&#x200B;取得する値のキー。

**戻り値**

キーに対応する値。キーに子キーがある場合、この関数は複合オブジェクトを返します。When the type of the value for the key is `undefined`, `null` is returned.

**例**

次の JavaScript オブジェクトについて考えてみます。

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

次のサンプルコードは、値 `260` を返します。

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

次のサンプルコードは、子キーを持つキーの値を取得します。

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

この関数は次のオブジェクトを返します。

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

オブジェクトのデータツリーからすべてのキーを取得します。オプションで、特定のキーの子のキーのみを取得できます。オプションで、取得したキーのソート順を指定することもできます。

**パラメーター**

* **tree：**&#x200B;データツリーのキーの取得元となるオブジェクト。
* **parent：**（オプション）子項目のキーを取得するデータツリー内の項目のキー。
* **order：**（オプション）返されたキーのソート順を判断する関数（Mozilla Developer Network の [Array.prototype.sort](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) を参照）。

**戻り値**

キーからなる配列。

**例**

次のオブジェクトについて考えてみます。

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

The `ContextHub.Utils.JSON.tree.getKeys(myObject);` script returns the following array:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

指定されたオブジェクトのコピーを作成し、指定されたブランチをデータツリーから削除し、変更されたコピーを返します。

**パラメーター**

* tree：データオブジェクト。
* key：削除するキー。

**戻り値**

キーが削除された元のデータオブジェクトのコピー。

**例**

次のオブジェクトについて考えてみます。

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

次のサンプルスクリプトでは、データツリーから /one/two/three/four ブランチを削除しています。

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

この関数は次のオブジェクトを返します。

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

文字列値の不要部分を削除して、キーとして使用できるようにします。文字列の不要部分を削除するために、この関数は次のアクションを実行します。

* 複数の連続するフォワードスラッシュを 1 つのスラッシュにまとめます。
* 文字列の先頭および末尾から空白を削除します。
* 結果をスラッシュで区切られた文字列の配列に分割します。

作成された配列を使用して、使用可能なキーを作成します。**パラメーター**

* **key:** 消毒 `string` する。

**戻り値**

An array of `string` values where each string is the portion of the `key` that was demarcated by slashes. 不要部分が削除されたキーを表します。不要部分が削除された配列の長さがゼロの場合、この関数は `null` を返します。

**例**

The following code sanitizes a string to produce the array `["this", "is", "a", "path"]`, and then generates the key `"/this/is/a/path"` from the array:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

オブジェクトのコピーのデータツリーにキーと値のペアを追加します。For information about data trees, see [Persistence](/help/sites-developing/contexthub.md#persistence).

**パラメーター**

* tree：データオブジェクト。
* key：追加する値に関連付けるキー。キーは、データツリー内の項目へのパスです。この関数は、`ContextHub.Utils.JSON.tree.sanitize` を呼び出して、キーを追加する前に不要部分を削除します。
* value：データツリーに追加する値。

**戻り値**

`tree` / `key``value` ペアを含むオブジェクトのコピー。

**例**

次の JavaScript コードについて考えてみます。

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

myObject オブジェクトは次の値を持ちます。

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

ストア候補を登録したり、登録されたストア候補を取得したりできるようにします。

### 関数（ContextHub.Utils.storeCandidates） {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

ストア候補として登録されているストアタイプを返します。特定のストアタイプまたはすべてのストアタイプの登録されている候補を取得します。

**パラメーター**

* **storeType：**（String）ストアタイプの名前。See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) function.

**戻り値**

ストアタイプのオブジェクト。オブジェクトのプロパティはストアタイプ名で、プロパティ値は登録されているストア候補からなる配列です。

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

登録されている候補からストアタイプを返します。複数のストアタイプが同じ名前で登録されている場合、この関数は最も優先度が高いストアタイプを返します。

**パラメーター**

* storeType：（String）ストア候補の名前。See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) function.

**戻り値**

登録されているストア候補を表すオブジェクト。要求されたストアタイプが登録されていない場合は、エラーがスローされます。

#### getSupportedStoreTypes() {#getsupportedstoretypes}

ストア候補として登録されているストアタイプの名前を返します。この関数にパラメーターは必要ありません。

**戻り値**

文字列値からなる配列で、各文字列はストア候補と一緒に登録されたストアタイプです。See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) function.

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

名前と優先度を使用して、ストアオブジェクトをストア候補として登録します。

優先度は、同じ名前のストアの重要度を示す数字です。既に登録されているストア候補と同じ名前を使用してストア候補を登録した場合、優先度の高い候補が使用されます。ストア候補を登録する場合、同じ名前の登録済みストア候補より優先度が高い場合にのみストアが登録されます。

**パラメーター**

* **store：**（Object）ストア候補として登録するストアオブジェクト。
* **storeType：**（String）ストア候補の名前。この値は、ストア候補のインスタンスを作成する際に必要です。
* **priority:** （番号）ストア候補の優先順位。
* **applies：**（Function）現在の環境内でのストアの適用可能性を評価するために呼び出す関数。この関数は、ストアを適用できる場合は `true`、それ以外の場合は `false` を返す必要があります。The default value is a function that returns true: `function() {return true;}`

**例**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

