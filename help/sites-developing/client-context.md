---
title: ClientContext の詳細
description: ClientContext は、動的にアセンブルされたユーザーデータのコレクションを表します
uuid: 95b08fbd-4f50-44a1-80fb-46335fe04a40
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c881ad66-bcc3-4f99-b77f-0944c23e2d29
docset: aem65
feature: Context Hub
exl-id: 38b9a795-1c83-406c-ab13-b4456da938dd
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '3017'
ht-degree: 36%

---

# ClientContext の詳細{#client-context-in-detail}

>[!NOTE]
>
>Client Context は、ContextHub に変更されました。詳しくは、 [関連ドキュメント](/help/sites-developing/contexthub.md) 」を参照してください。

ClientContext は、動的に組み立てられたユーザーデータのコレクションを表します。 特定の状況（コンテンツのターゲット設定）で Web ページに表示するコンテンツを、データを使用して決定できます。 また、データは、Web サイトの分析や、ページ上の任意の JavaScript にも使用できます。

ClientContext は、主に次の側面で構成されます。

* ユーザーデータを格納するセッションストア。
* ユーザーデータを表示し、ユーザーエクスペリエンスをシミュレートするツールを提供する UI。
* A [JavaScript API](/help/sites-developing/ccjsapi.md) を参照してください。

スタンドアロンのセッションストアを作成して ClientContext に追加する場合、または Context Store コンポーネントに関連付けられたセッションストアを作成する場合。 AEMは、すぐに使用できる複数のコンテキストストアコンポーネントをインストールします。 これらのコンポーネントは、コンポーネントの基礎として使用できます。

ClientContext の起動、表示する情報の設定、ユーザーエクスペリエンスのシミュレーションについて詳しくは、[ClientContext](/help/sites-administering/client-context.md) を参照してください。

## セッションストア {#session-stores}

ClientContext には、ユーザーデータを含む様々なセッションストアが含まれます。 ストアデータは次のソースから取得されます。

* クライアント web ブラウザー。
* サーバー（サードパーティソースからの情報の保存については [JSONP ストア](/help/sites-administering/client-context.md#main-pars-variable-8)を参照してください）

ClientContext フレームワークは、 [JavaScript API](/help/sites-developing/ccjsapi.md) を使用して、セッションストアとやり取りし、ユーザーデータの読み取りと書き込み、ストアイベントのリッスンと反応をおこなうことができます。 また、コンテンツのターゲティングやその他の目的で使用するユーザーデータ用のセッションストアを作成することもできます。

セッションストアのデータは、クライアントに残ります。 ClientContext は、データをサーバーに書き戻しません。 データをサーバーに送信するには、フォームを使用するか、カスタム JavaScript を開発します。

各セッションストアは、プロパティと値のペアのコレクションです。セッションストアは（あらゆる種類の）データのコレクションを表し、その概念的な意味はデザイナーや開発者が決定できます。次の JavaScript コードの例では、セッションストアに格納されるプロファイルデータを表すオブジェクトを定義しています。

```
{
  age: 20,
  authorizableId: "aparker@geometrixx.info",
  birthday: "27 Feb 1992",
  email: "aparker@geometrixx.info",
  formattedName: "Alison Parker",
  gender: "female",
  path: "/home/users/geometrixx/aparker@geometrixx.info/profile"
}
```

セッションストアは、ブラウザーセッションをまたがって保持することも、そのストアが作成されたブラウザーセッションでのみ保持することもできます。

>[!NOTE]
>
>ストアの保持には、ブラウザーストレージまたは cookie（`SessionPersistence` cookie）を使用します。ブラウザーストレージはより一般的です。
>
>ブラウザーを閉じて再び開くと、セッションストアは、永続化されたストアの値を使用して読み込むことができます。 古い値を削除するには、ブラウザーキャッシュのクリアが必要です。

### コンテキストストアコンポーネント {#context-store-components}

コンテキストストアコンポーネントは、ClientContext に追加できる CQ コンポーネントです。 通常、コンテキストストアコンポーネントは、関連付けられているセッションストアのデータを表示します。 ただし、コンテキストストアコンポーネントに表示される情報は、セッションストアデータに限定されません。

コンテキストストアコンポーネントには、次の項目を含めることができます。

* ClientContext での外観を定義する JSP スクリプト。
* コンポーネントをリストするためのSidekick。
* コンポーネントインスタンスを設定するための編集ダイアログ。
* セッションストアを初期化する JavaScript。

コンテキストストアに追加できる、インストール済みのコンテキストストアコンポーネントの説明については、 [使用可能な ClientContext コンポーネント](/help/sites-administering/client-context.md#available-client-context-components).

>[!NOTE]
>
>ページデータは、ClientContext のデフォルトのコンポーネントではなくなりました。必要に応じて、ページデータを追加するには、Client Context を編集し、**汎用ストアのプロパティ**&#x200B;コンポーネントを追加して、**ストア**&#x200B;を `pagedata` として定義するように設定します。

### ターゲット設定されたコンテンツの配信 {#targeted-content-delivery}

[ターゲット設定されたコンテンツ](/help/sites-authoring/content-targeting-touch.md)の配信にはプロファイル情報も使用します。

![clientcontext_targetedcontentdelivery](assets/clientcontext_targetedcontentdelivery.png) ![clientcontext_targetedcontentdeliverydetail](assets/clientcontext_targetedcontentdeliverydetail.png)

## ページへの ClientContext の追加 {#adding-client-context-to-a-page}

ClientContext を有効にするには、Web ページの body セクションに ClientContext コンポーネントを含めます。 ClientContext コンポーネントノードのパスは `/libs/cq/personalization/components/clientcontext` です。このコンポーネントを含めるには、次のコードをページコンポーネントの JSP ファイルに追加します。場所は、ページの `body` 要素のすぐ下です。

```java
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

clientcontext コンポーネントにより、ページは ClientContext を実装するクライアントライブラリを読み込みます。

* ClientContext JavaScript API です。
* セッションストア、イベント管理などをサポートする ClientContext フレームワーク
* 定義されたセグメント。
* ClientContext に追加された各コンテキストストアコンポーネント用に生成される init.js スクリプト。
* （オーサーインスタンスのみ）ClientContext UI。

ClientContext UI は、オーサーインスタンスでのみ使用できます。

## ClientContext の拡張 {#extending-client-context}

ClientContext を拡張するには、セッションストアを作成し、必要に応じてストアデータを表示します。

* コンテンツのターゲティングと Web 分析に必要なユーザーデータ用のセッションストアを作成します。
* コンテキストストアコンポーネントを作成して、管理者が関連するセッションストアを設定し、テスト用にストアデータを ClientContext に表示できるようにします。

>[!NOTE]
>
>データを提供できる `JSONP` サービスがある（または作成する）場合は、`JSONP` コンテキストストアコンポーネントを使用して、その JSONP サービスにマップするだけです。これはセッションストアを処理します。

### セッションストアの作成 {#creating-a-session-store}

ClientContext に追加し、ClientContext から取得する必要のあるデータのセッションストアを作成します。 通常は、次の手順を使用してセッションストアを作成します。

1. `categories` プロパティの値が `personalization.stores.kernel` のクライアントライブラリフォルダーを作成します。Client Context は、このカテゴリのクライアントライブラリを自動的に読み込みます。

1. `personalization.core.kernel` クライアントライブラリフォルダーに対して依存関係を持つように、クライアントライブラリフォルダーを設定します。この `personalization.core.kernel` クライアントライブラリは、ClientContext JavaScript API を提供します。

1. セッションストアを作成し、初期化する JavaScript を追加します。

personalization.stores.kernel クライアントライブラリに JavaScript を含めると、ClientContext フレームワークの読み込み時にストアが作成されます。

>[!NOTE]
>
>コンテキストストアコンポーネントの一部としてセッションストアを作成している場合は、代わりに、コンポーネントのinit.js.jsp ファイルに JavaScript を配置することもできます。 この場合、セッションストアは、コンポーネントが ClientContext に追加された場合にのみ作成されます。

#### セッションストアのタイプ {#types-of-session-stores}

セッションストアは、ブラウザーセッション中に作成されて使用可能になるか、ブラウザーストレージまたは cookie に保持されます。 ClientContext JavaScript API は、両方のタイプのデータストアを表す複数のクラスを定義します。

* ` [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore)`：これらのオブジェクトはページ DOM 内にのみ存在します。データが作成され、ページが存続する間保持されます。
* ` [CQ_Analytics.PerstistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore)`：これらのオブジェクトはページ DOM 内に存在し、ブラウザーストレージまたは cookie に保持されます。データは、ページやユーザーセッションをまたがって使用できます。

また、API は JSON データまたは JSONP データの格納に特化したこれらのクラスを拡張します。

* セッションのみのオブジェクト： [CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonstore) および [CQ_Analytics.JSONPStore](/help/sites-developing/ccjsapi.md#cq-analytics-jsonpstore).

* 永続化されたオブジェクト： [CQ_Analytics.PersistedJSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedjsonstore) および [CQ_Analytics.PersistedJSONPStore](/help/sites-developing/ccjsapi.md#cq-analyics-persistedjsonpstore).

#### セッションストアオブジェクトの作成 {#creating-the-session-store-object}

クライアントライブラリフォルダーの JavaScript は、セッションストアを作成し、初期化します。 その後、Context Store Manager を使用してセッションストアを登録する必要があります。 次の例では、[CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) オブジェクトを作成して登録します。

```
//Create the session store
if (!CQ_Analytics.MyStore) {
    CQ_Analytics.MyStore = new CQ_Analytics.SessionStore();
    CQ_Analytics.MyStore.STOREKEY = "MYSTORE";
    CQ_Analytics.MyStore.STORENAME = "mystore";
    CQ_Analytics.MyStore.data={};
}
//register the session store
if (CQ_Analytics.ClientContextMgr){
    CQ_Analytics.ClientContextMgr.register(CQ_Analytics.MyStore)
}
```

次の例では、JSON データを格納するために、[CQ_Analytics.JSONStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) オブジェクトを作成して登録します。

```
if (!CQ_Analytics.myJSONStore) {
    CQ_Analytics.myJSONStore = CQ_Analytics.JSONStore.registerNewInstance("myjsonstore",{});
}
```

### コンテキストストアコンポーネントの作成 {#creating-a-context-store-component}

コンテキストストアコンポーネントを作成して、セッションストアデータを ClientContext でレンダリングします。 作成したら、コンテキストストアコンポーネントを ClientContext にドラッグして、セッションストアからデータをレンダリングできます。 コンテキストストアコンポーネントは、次の項目で構成されます。

* データをレンダリングするための JSP スクリプト。
* 編集ダイアログ。
* セッションストアを初期化するための JSP スクリプト。
* （オプション）セッションストアを作成するクライアントライブラリフォルダー。 コンポーネントが既存のセッションストアを使用する場合、クライアントライブラリフォルダーを含める必要はありません。

#### 提供されるコンテキストストアコンポーネントの拡張 {#extending-the-provided-context-store-components}

AEMは、拡張可能な genericstore および genericstoreproperties コンテキストストアコンポーネントを提供します。 ストアデータの構造によって、拡張するコンポーネントが決まります。

* プロパティと値のペア：`GenericStoreProperties` コンポーネントを拡張します。このコンポーネントは、プロパティと値のペアのストアを自動的にレンダリングします。 複数のインタラクションポイントが提供されます。

   * `prolog.jsp` と `epilog.jsp`：コンポーネントをレンダリングする前または後にサーバー側ロジックを追加できるコンポーネントインタラクション。

* 複合データ：`GenericStore` コンポーネントを拡張します。次に、セッションストアには、コンポーネントをレンダリングする必要が生じるたびに呼び出される「レンダラー」メソッドが必要です。 レンダラー関数は、次の 2 つのパラメーターで呼び出されます。

   * `@param {String} store`
レンダリングするストア

   * `@param {String} divId`
ストアをレンダリングする必要がある div の ID。

>[!NOTE]
>
>すべての ClientContext コンポーネントは、汎用ストアコンポーネントまたは汎用ストアのプロパティコンポーネントの拡張です。いくつかのサンプルが `/libs/cq/personalization/components/contextstores` フォルダーにインストールされています。

#### Sidekickでの外観の設定 {#configuring-the-appearance-in-sidekick}

ClientContext の編集時に、コンテキストストアコンポーネントがサイドキックに表示されます。 すべてのコンポーネントと同様に、ClientContext コンポーネントの `componentGroup` プロパティと `jcr:title` プロパティによって、コンポーネントのグループと名前が決まります。

`componentGroup` プロパティの値が `Client Context` のすべてのコンポーネントが、デフォルトでサイドキックに表示されます。`componentGroup` プロパティに異なる値を使用する場合は、デザインモードを使用して、手動でコンポーネントをサイドキックに追加する必要があります。

#### コンテキストストアコンポーネントインスタンス {#context-store-component-instances}

コンテキストストアコンポーネントを ClientContext に追加すると、コンポーネントインスタンスを表すノードが `/etc/clientcontext/default/content/jcr:content/stores` の下に作成されます。このノードには、コンポーネントの編集ダイアログを使用して設定するプロパティ値が含まれます。

ClientContext が初期化されると、これらのノードが処理されます。

#### 関連するセッションストアの初期化 {#initializing-the-associated-session-store}

コンポーネントにinit.js.jsp ファイルを追加して、コンテキストストアコンポーネントが使用するセッションストアを初期化する JavaScript コードを生成します。 例えば、初期化スクリプトを使用してコンポーネントの設定プロパティを取得し、それらのプロパティを使用してセッションストアを設定します。

生成された JavaScript は、オーサーインスタンスとパブリッシュインスタンスの両方で、ページの読み込み時に ClientContext が初期化されると、ページに追加されます。 この JSP は、コンテキストストアコンポーネントインスタンスの読み込みとレンダリングの前に実行されます。

コードでは、ファイルの MIME タイプを `text/javascript` に設定する必要があります。それ以外の場合は実行されません。

>[!CAUTION]
>
>init.js.jsp スクリプトは、オーサーインスタンスとパブリッシュインスタンスで実行されますが、コンテキストストアコンポーネントが ClientContext に追加された場合にのみ実行されます。

次の手順では、init.js.jsp スクリプトファイルを作成し、正しい MIME タイプを設定するコードを追加します。 ストアの初期化を実行するコードは、それに従います。

1. コンテキストストアコンポーネントノードを右クリックし、作成/ファイルを作成をクリックします。
1. 「名前」フィールドに「`init.js.jsp`」と入力して「OK」をクリックします。
1. ページの上部に次のコードを追加し、「すべて保存」をクリックします。

   ```java
   <%@page contentType="text/javascript" %>
   ```

### genericstoreproperties コンポーネントのセッションストアデータのレンダリング {#rendering-session-store-data-for-genericstoreproperties-components}

一貫性のある形式を使用して、セッションストアデータを ClientContext に表示します。

#### プロパティデータの表示 {#displaying-property-data}

パーソナライズタグライブラリが、セッションストアのプロパティの値を表示する `personalization:storePropertyTag` タグを提供します。タグを使用するには、JSP ファイルに次のコード行を含めます。

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

タグのフォーマットは次のとおりです。

```xml
<personalization:storePropertyTag propertyName="property_name" store="session_store_name"/>
```

`propertyName` 属性は、表示するストアプロパティの名前です。`store` 属性は、登録されたストアの名前です。次のサンプルのタグでは、`profile` ストアの `authorizableId` プロパティの値が表示されます。

```xml
<personalization:storePropertyTag propertyName="authorizableId" store="profile"/>
```

#### HTML構造 {#html-structure}

personalization.ui クライアントライブラリフォルダー (/etc/clientlibs/foundation/personalization/ui/themes/default) には、ClientContext がHTMLコードの書式設定に使用する CSS スタイルが用意されています。 次のコードは、ストアデータの表示に使用する推奨構造を示しています。

```xml
<div class="cq-cc-store">
   <div class="cq-cc-thumbnail">
      <div class="cq-cc-store-property">
           <!-- personalization:storePropertyTag for the store thumbnail image goes here -->
      </div>
   </div>
   <div class="cq-cc-content">
       <div class="cq-cc-store-property cq-cc-store-property-level0">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level1">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level2">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
       <div class="cq-cc-store-property cq-cc-store-property-level3">
           <!-- personalization:storePropertyTag for a store property goes here -->
       </div>
   </div>
   <div class="cq-cc-clear"></div>
</div>
```

`/libs/cq/personalization/components/contextstores/profiledata` コンテキストストアコンポーネントは、この構造を使用してプロファイルセッションストアのデータを表示します。`cq-cc-thumbnail` クラスは、サムネール画像を配置します。`cq-cc-store-property-level*x*` クラスは、英数字データを次のようにフォーマットします。

* level0、level1、level2 は垂直方向に分布し、白のフォントを使用します。
* level3 およびその他のレベルは、水平方向に分布され、背景が暗い白のフォントを使用します。

![chlimage_1-4](assets/chlimage_1-4.png)

### genericstore コンポーネントのセッションストアデータのレンダリング {#rendering-session-store-data-for-genericstore-components}

genericstore コンポーネントを使用してストアデータをレンダリングするには、次の操作が必要です。

* セッションストアの名前を識別するために、personalization:storeRendererTag タグをコンポーネントの JSP スクリプトに追加します。
* セッションストアクラスにレンダラーメソッドを実装します。

#### genericstore セッションストアの識別 {#identifying-the-genericstore-session-store}

パーソナライズタグライブラリが、セッションストアのプロパティの値を表示する `personalization:storePropertyTag` タグを提供します。タグを使用するには、JSP ファイルに次のコード行を含めます。

```xml
<%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
```

タグのフォーマットは次のとおりです。

```java
<personalization:storeRendererTag store="store_name"/>
```

#### セッションストアレンダラーメソッドの実装 {#implementing-the-session-store-renderer-method}

次に、セッションストアには、コンポーネントをレンダリングする必要が生じるたびに呼び出される「レンダラー」メソッドが必要です。 レンダラー関数は、次の 2 つのパラメーターで呼び出されます。

* @param {String} store
レンダリングするストア
* @param {String} divId
ストアをレンダリングする必要がある div の ID。

## セッションストアとのやり取り {#interacting-with-session-stores}

JavaScript を使用してセッションストアを操作します。

### セッションストアへのアクセス {#accessing-session-stores}

ストアに対してデータの読み取りまたは書き込みを行うセッションストアオブジェクトを取得します。 [CQ_Analytics.ClientContextMgr](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextmgr) は、ストア名に基づいてストアへのアクセスを提供します。 取得したら、 [CQ_Analytics.SessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-sessionstore) または [CQ_Analytics.PersistedSessionStore](/help/sites-developing/ccjsapi.md#cq-analytics-persistedsessionstore) ストアデータとやり取りする場合。

次の例では、`profile` ストアを取得し、このストアから `formattedName` プロパティを取得しています。

```
function getName(){
   var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
   if(profilestore){
      return profilestore.getProperty("formattedName", false);
   } else {
      return null;
   }
}
```

### セッションストアの更新に反応するリスナーの作成 {#creating-a-listener-to-react-to-a-session-store-update}

セッションはイベントを保存するので、これらのイベントに基づいてリスナーとトリガーイベントを追加できます。

セッションストアは、`Observable` パターンを基盤として作成されています。セッションストアは [`CQ_Analytics.Observable`](/help/sites-developing/ccjsapi.md#cq-analytics-observable) メソッドを提供する ` [addListener](/help/sites-developing/ccjsapi.md#addlistener-event-fct-scope)`  を拡張します。

次の例では、`profile` セッションストアの `update` イベントにリスナーを追加しています。

```
var profileStore = ClientContextMgr.getRegisteredStore("profile");
if( profileStore ) {
  //callback execution context
  var executionContext = this;

  //add "update" event listener to store
  profileStore.addListener("update",function(store, property) {
    //do something on store update

  },executionContext);
}
```

### セッションストアが定義され、初期化されていることを確認する {#checking-that-a-session-store-is-defined-and-initialized}

セッションストアは、データが読み込まれて初期化されるまで使用できません。 セッションストアが利用可能になるタイミングには、次の要因が影響する場合があります。

* ページの読み込み
* JavaScript の読み込み
* JavaScript 実行時間
* XHR リクエストの応答時間
* セッションストアに対する動的な変更

以下を使用： [CQ_Analytics.ClientContextUtils](/help/sites-developing/ccjsapi.md#cq-analytics-clientcontextutils) オブジェクトの [onStoreRegistered](/help/sites-developing/ccjsapi.md#onstoreregistered-storename-callback) および [onStoreInitialized](/help/sites-developing/ccjsapi.md#onstoreinitialized-storename-callback-delay) 使用可能な場合にのみセッションストアにアクセスするメソッド。 これらのメソッドを使用すると、セッション登録および初期化イベントに反応するイベントリスナーを登録できます。

>[!CAUTION]
>
>別のストアを使用している場合は、ストアが登録されていない場合に備えて対応する必要があります。

次の例では、`profile` セッションストアの `onStoreRegistered` イベントを使用しています。ストアが登録されると、リスナーがセッションストアの `update` イベントに追加されます。ストアが更新されると、ページ上の `<div class="welcome">` 要素のコンテンツが `profile` ストアの名前で更新されます。

```
//listen for the store registration
CQ_Analytics.ClientContextUtils.onStoreRegistered("profile", listen);

//listen for the store's update event
function listen(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
    profilestore.addListener("update",insertName);
}

//insert the welcome message
function insertName(){
 $("div.welcome").text("Welcome "+getName());
}

//obtain the name from the profile store
function getName(){
 var profilestore = CQ_Analytics.ClientContextMgr.getRegisteredStore("profile");
 if(profilestore){
  return profilestore.getProperty("formattedName", false);
    } else {
        return null;
    }
}
```

### sessionpersistence Cookie からのプロパティの除外 {#excluding-a-property-from-the-sessionpersistence-cookie}

`PersistedSessionStore` プロパティを永続化しないようにする（つまり、`sessionpersistence` cookie から除外する）には、永続セッションストアの非永続プロパティリストにプロパティを追加します。

参照先 ` [CQ_Analytics.PersistedSessionStore.setNonPersisted(propertyName)](/help/sites-developing/ccjsapi.md#setnonpersisted-name)`

```
CQ_Analytics.ClientContextUtils.onStoreRegistered("surferinfo", function(store) {
  //this will exclude the browser, OS and resolution properties of the surferinfo session store from the
  store.setNonPersisted("browser");
  store.setNonPersisted("OS");
  store.setNonPersisted("resolution");
});
```

## デバイススライダーの設定 {#configuring-the-device-slider}

### 条件 {#conditions}

現在のページに対応するモバイルページがあることが必要です。この条件が満たされるのは、そのページに、モバイルロールアウト設定で設定されたライブコピーがある（`rolloutconfig.path.toLowerCase` に `mobile` が含まれる）場合のみです。

#### 設定 {#configuration}

デスクトップページからモバイルに相当するページに切り替える場合：

* モバイルページの DOM が読み込まれます。
* コンテンツを含むメインの `div`（必須）が抽出され、現在のデスクトップページに挿入されます。

* 読み込む必要がある CSS クラスと body クラスを手動で設定する必要があります。

次は例です。

```
window.CQMobileSlider["geometrixx-outdoors"] = {
  //CSS used by desktop that need to be removed when mobile
  DESKTOP_CSS: [
    "/etc/designs/${app}/clientlibs_desktop_v1.css"
  ],

  //CSS used by mobile that need to be removed when desktop
  MOBILE_CSS: [
    "/etc/designs/${app}/clientlibs_mobile_v1.css"
  ],

  //id of the content that needs to be removed when mobile
  DESKTOP_MAIN_ID: "main",

  //id of the content that needs to be removed when desktop
  MOBILE_MAIN_ID: "main",

  //body classes used by desktop that need to be removed when mobile
  DESKTOP_BODY_CLASS: [
    "page"
  ],

  //body classes used by mobile that need to be removed when desktop
  MOBILE_BODY_CLASS: [
    "page-mobile"
  ]
};
```

## 例：カスタムコンテキストストアコンポーネントの作成 {#example-creating-a-custom-context-store-component}

この例では、外部サービスからデータを取得してセッションストアに保存するコンテキストストアコンポーネントを作成します。

* genericstoreproperties コンポーネントを拡張します。
* CQ_Analytics.JSONPStore JavaScript オブジェクトを使用してストアを初期化します。
* JSONP サービスを呼び出してデータを取得し、ストアに追加します。
* データを ClientContext でレンダリングします。

### ジオロケーションコンポーネントを追加する {#add-the-geoloc-component}

CQ アプリケーションを作成し、ジオロケーションコンポーネントを追加します。

1. Web ブラウザーで CRXDE Lite を開きます（[https://localhost:4502/crx/de](https://localhost:4502/crx/de)）。
1. `/apps` フォルダーを右クリックして、作成／フォルダーを作成をクリックします。「`myapp`」の名前を指定して、「OK」をクリックします。
1. 同様に、`myapp` の下に `contextstores` というフォルダーを作成します。
1. `/apps/myapp/contextstores` フォルダーを右クリックして、作成／コンポーネントを作成をクリックします。次のプロパティ値を指定し、「次へ」をクリックします。

   * ラベル：geoloc
   * タイトル：ロケーションストア
   * スーパータイプ：cq/personalization/components/contextstores/genericstoreproperties
   * グループ：ClientContext

1. コンポーネントを作成ダイアログで、各ページの「次へ」をクリックして「OK」ボタンを有効にし、「OK」をクリックします。
1. 「すべて保存」をクリックします。

### ジオロケーション編集ダイアログを作成する {#create-the-geoloc-edit-dialog}

コンテキストストアコンポーネントには、編集ダイアログが必要です。 ジオロケーション編集ダイアログには、設定するプロパティがないことを示す静的メッセージが含まれます。

1. `/libs/cq/personalization/components/contextstores/genericstoreproperties/dialog` ノードを右クリックして、「コピー」をクリックします。
1. `/apps/myapp/contextstores/geoloc` ノードを右クリックして、ペーストをクリックします。
1. /apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items ノードの下にある子ノードをすべて削除します。

   * store
   * properties
   * thumbnail

1. `/apps/myapp/contextstores/geoloc/dialog/items/items/tab1/items` ノードを右クリックして、作成／ノードを作成をクリックします。次のプロパティ値を指定し、「OK」をクリックします。

   * 名前：静的
   * タイプ：cq:Widget

1. このノードに次のプロパティを追加します。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | cls | 文字列 | x-form-fieldset-description |
   | text | 文字列 | ジオロケーションコンポーネントを設定する必要はありません。 |
   | xtype | 文字列 | static |

1. 「すべて保存」をクリックします。

   ![chlimage_1-5](assets/chlimage_1-5.png)

### 初期化スクリプトの作成 {#create-the-initialization-script}

init.js.jsp ファイルをジオロケーションコンポーネントに追加し、それを使用してセッションストアを作成し、ロケーションデータを取得して、ストアに追加します。

init.js.jsp ファイルは、ClientContext がページによって読み込まれると実行されます。 この時点で、ClientContext JavaScript API が読み込まれ、スクリプトで使用できます。

1. /apps/myapp/contextstores/geoloc ノードを右クリックし、作成／ファイルを作成をクリックします。「名前」にinit.js.jsp を指定し、「OK」をクリックします。
1. 次のコードをページの上部に追加し、「すべて保存」をクリックします。

   ```java
   <%@page contentType="text/javascript;charset=utf-8" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   log.info("***** initializing geolocstore ****");
   String store = "locstore";
   String jsonpurl = "https://api.wipmania.com/jsonp?callback=${callback}";
   
   %>
   var locstore = CQ_Analytics.StoreRegistry.getStore("<%= store %>");
   if(!locstore){
    locstore = CQ_Analytics.JSONPStore.registerNewInstance("<%= store %>", "<%= jsonpurl %>",{});
   }
   <% log.info(" ***** done initializing geoloc ************"); %>
   ```

### ジオロケーションセッションストアデータをレンダリング {#render-the-geoloc-session-store-data}

ジオロケーションコンポーネントの JSP ファイルにコードを追加して、ストアデータを ClientContext でレンダリングします。

![chlimage_1-6](assets/chlimage_1-6.png)

1. CRXDE Lite で `/apps/myapp/contextstores/geoloc/geoloc.jsp` ファイルを開きます。
1. スタブコードの下に次のHTMLコードを追加します。

   ```xml
   <%@taglib prefix="personalization" uri="https://www.day.com/taglibs/cq/personalization/1.0" %>
   <div class="cq-cc-store">
      <div class="cq-cc-content">
          <div class="cq-cc-store-property cq-cc-store-property-level0">
              Continent: <personalization:storePropertyTag propertyName="address/continent" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level1">
              Country: <personalization:storePropertyTag propertyName="address/country" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level2">
              City: <personalization:storePropertyTag propertyName="address/city" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level3">
              Latitude: <personalization:storePropertyTag propertyName="latitude" store="locstore"/>
          </div>
          <div class="cq-cc-store-property cq-cc-store-property-level4">
              Longitude: <personalization:storePropertyTag propertyName="longitude" store="locstore"/>
          </div>
      </div>
       <div class="cq-cc-clear"></div>
   </div>
   ```

1. 「すべて保存」をクリックします。

### コンポーネントを ClientContext に追加する {#add-the-component-to-client-context}

ページの読み込み時に初期化されるように、ロケーションストアコンポーネントを ClientContext に追加します。

1. オーサーインスタンス上で Geometrixx Outdoors のホームページを開きます（[https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)）。
1. Ctrl + Alt + C キー（Windows）または Control + Option + C キー（Mac）を押して、ClientContext を開きます。
1. ClientContext の上部にある編集アイコンをクリックして、ClientContext Designer を開きます。

   ![四角形内に鉛筆で示される編集アイコン。](do-not-localize/chlimage_1.png)

1. ロケーションストアコンポーネントを ClientContext にドラッグします。

### ClientContext のロケーション情報を参照 {#see-the-location-information-in-client-context}

Geometrixx Outdoorsホームページを編集モードで開き、ClientContext を開いてロケーションストアコンポーネントのデータを確認します。

1. Geometrixx Outdoors サイトの英語ページを開きます。（[https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)）
1. ClientContext を開くには、Ctrl + Alt + C キー（Windows）または Control + Option + C キー（Mac）を押します。

## カスタマイズした ClientContext の作成 {#creating-a-customized-client-context}

2 つ目の ClientContext を作成するには、ブランチを複製する必要があります。

`/etc/clientcontext/default`

* サブフォルダー：
  `/content`
には、カスタマイズされた ClientContext のコンテンツが格納されます。

* フォルダー：
  `/contextstores`
を使用して、コンテキストストアの様々な設定を定義できます。

カスタマイズされた ClientContext を使用するには、ClientContext コンポーネントのデザインスタイルの
`path`
プロパティを、ページテンプレートに含まれているものと同じように編集します。例えば、標準的な場所は次のようになります。
`/libs/cq/personalization/components/clientcontext/design_dialog/items/path`
