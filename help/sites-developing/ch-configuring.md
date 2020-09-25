---
title: ContextHub の設定
seo-title: ContextHub の設定
description: Context Hub の設定方法について説明します。
seo-description: Context Hub の設定方法について説明します。
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 72%

---


# ContextHub の設定 {#configuring-contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。ContextHub について詳しくは、[開発者ドキュメント](/help/sites-developing/contexthub.md)を参照してください。ContextHub は、タッチ UI の [ClientContext](/help/sites-administering/client-context.md) に置き換わるものです。

[ContextHub](/help/sites-developing/contexthub.md) ツールバーを設定して、プレビューモードで表示する、ContextHub ストアを作成するおよびタッチ操作向け UI を使用して UI モジュールを追加するかどうかを制御します。

## ContextHub の無効化 {#disabling-contexthub}

ContextHub は、AEM のインストールで、デフォルトで有効になります。ContextHub を無効にすると、js/css の読み込みと初期化を回避できます。ContextHub を無効にする方法は 2 つあります。

* ContextHub の設定を編集し、「**ContextHub を無効にする**」チェックボックスをオンにします。

   1. レールで、**ツール／サイト／ContextHub** をクリックまたはタップします。
   1. デフォルトの「**設定コンテナ**」をクリックまたはタップします。
   1. 「**ContextHub 設定**」を選択し、「**選択した要素を編集**」をクリックまたはタップします。
   1. 「**ContextHub を無効にする**」をクリックまたはタップし、「**保存**」をクリックまたはタップします。

または

* Use CRXDE Lite to set the property `disabled` to **true** under `/libs/settings/cloudsettings`

>[!NOTE]
>
>[AEM 6.4でのリポジトリの再構築により](/help/sites-deploying/repository-restructuring.md) 、ContextHub設定の場所が `/etc/cloudsettings` 、次のように変更されました。
>
> * `/libs/settings/cloudsettings`
> * `/conf/global/settings/cloudsettings`
> * `/conf/<tenant>/settings/cloudsettings`


## ContextHub UI の表示と非表示 {#showing-and-hiding-the-contexthub-ui}

Adobe Granite ContextHub OSGi サービスを設定して、ページに [ContextHub UI](/help/sites-authoring/ch-previewing.md) を表示または非表示にします。The PID of this service is `com.adobe.granite.contexthub.impl.ContextHubImpl.`

To configure the service you can either use the [Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) or use a [JCR node in the repository](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Web コンソール：** UI を表示するには、Show UI プロパティを選択します。UI を非表示にするには、Hide UI プロパティを消去します。
* **JCRノード：** UIを表示するには、boolean `com.adobe.granite.contexthub.show_ui` プロパティをに設定し `true`ます。 To hide the UI, set the property to `false`.

ContextHub UI を表示に設定すると、AEM オーサーインスタンスのページにのみ表示されます。UI はパブリッシュインスタンスのページには表示されません。

## ContextHub UI モードとモジュールの追加 {#adding-contexthub-ui-modes-and-modules}

ContextHub ツールバーに表示される UI のモードとモジュールをプレビューモードで設定します。

* UI モード：関連モジュールのグループ。
* モジュール：ストアからのコンテキストデータを公開し、作成者がそのコンテキストを操作できるようにするウィジェット。

UI モードはツールバーの左側に一連のアイコンとして表示されます。選択すると、UI モードのモジュールが右側に表示されます。

![chlimage_1-319](assets/chlimage_1-319.png)

アイコンは、[Coral UI ライブラリ](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons)からの参照です。

### UI モードの追加 {#adding-a-ui-mode}

UI モードをグループ関連の ContextHub モジュールに追加します。UI モードを作成する際に、ContextHub ツールバーに表示されるタイトルとアイコンを指定します。

1. Experience Manager レールで、ツール／サイト／Context Hub をクリックまたはタップします。
1. デフォルトの設定コンテナをクリックまたはタップします。
1. 「ContextHub 設定」をクリックまたはタップします。
1. 「作成」ボタンをクリックまたはタップして、「ContextHub UI モード」をクリックまたはタップします。

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. 次のプロパティの値を指定します。

   * UIモードのタイトル：UIモードを識別するタイトル
   * Mode Icon: The selector for the [Coral UI icon](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) to use, for example `coral-Icon--user`
   * 有効：オンにすると ContextHub ツールバーに UI モードが表示されます。

1. 「保存」をクリックまたはタップします。

### UI モジュールの追加 {#adding-a-ui-module}

ContextHub UI モジュールを UI モードに追加し、それを ContextHub ツールバーに表示して、ページコンテンツをプレビューできるようにします。UI モジュールを追加するときは、ContextHub に登録されるモジュールタイプのインスタンスを作成します。UI モジュールを追加するには、関連するモジュールタイプの名前が必要です。

AEM には、基本の UI モジュールタイプと、UI モジュールのベースにできる複数のサンプル UI モジュールタイプが用意されています。次の表で、各モジュールタイプについて簡単に説明します。カスタム UI モジュールの開発について詳しくは、[ContextHub UI モジュールの作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)を参照してください。

UI モジュールのプロパティには、モジュール固有のプロパティの値を指定できる詳細設定が含まれています。詳細設定は JSON 形式で指定します。表の「モジュールタイプ」列は、各 UI モジュールタイプに必要な JSON コードに関する情報へのリンクを示します。

| モジュールの種類 | 説明 | ストア |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | 汎用UIモジュールタイプ | UIモジュールのプロパティで設定 |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | ブラウザーに関する情報を表示します | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | 日付と時刻の情報を表示します | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | クライアントデバイスの表示 | emulators |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | クライアントの緯度と経度、およびマップ上の位置が表示されます。位置は変更できます。 | geolocation |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | デバイスの画面の向き（横置きまたは縦置き）を表示します。 | emulators |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | ページタグに関する統計を表示します。 | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | authorizableID、displayName、familyName など、現在のユーザーのプロファイル情報が表示されます。displayName と familyName の値は変更できます。 | プロファイル |

1. Experience Manager レールで、ツール／サイト／ContextHub をクリックまたはタップします。
1. UI モジュールを追加する設定コンテナをクリックまたはタップします。
1. UI モジュールを追加する ContextHub 設定コンテナをクリックまたはタップします。
1. UI モジュールを追加する UI モードをクリックまたはタップします。
1. 「作成」ボタンをクリックまたはタップして、「ContextHub UI モジュール (汎用)」をクリックまたはタップします。

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. 次のプロパティの値を指定します。

   * UI モジュールのタイトル：UI モジュールを識別するタイトル。
   * モジュールタイプ：そのモジュールのタイプ。
   * 有効：オンにすると ContextHub ツールバーに UI モジュールが表示されます。

1. （オプション）デフォルトのストアの設定をオーバーライドするには、UI モジュールを設定する JSON オブジェクトを入力します。
1. 「保存」をクリックまたはタップします。

## ContextHub ストアの作成 {#creating-a-contexthub-store}

ContextHub ストアを作成してユーザーデータを保持し、必要に応じてそのデータにアクセスします。ContextHub ストアは、登録済みのストア候補に基づきます。ストアを作成する際には、ストア候補が登録された storeType の値が必要です（[カスタムストア候補の作成](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)を参照してください）。

### ストアの詳細設定 {#detailed-store-configuration}

ストアを設定すると、詳細設定プロパティによりストア固有のプロパティの値を指定できます。値は、ストアの `config` 関数の `init` パラメーターに基づきます。このため、この値を指定する必要があるかどうかと、指定する値の形式はストアによって変わります。

詳細設定プロパティの値は、JSON 形式の `config` オブジェクトです。

### サンプルのストア候補 {#sample-store-candidates}

AEM には、ストアのベースにできる次のサンプルのストア候補が用意されています。

| ストアの種類 | 説明 |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | 解決済みおよび未解決の ContextHub セグメントを格納します。ContextHub SegmentManagerからセグメントを自動的に取得します |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | 現在までに解決済みのセグメントを格納します。ContextHub SegmentManagerサービスをリッスンしてストアを自動的に更新します |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | ブラウザーの場所の緯度と経度を格納します。 |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | ブラウザーの場所の現在の日付、時刻、季節が格納されます |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | 多数のデバイスのプロパティと機能を定義し、現在のクライアントデバイスを検出します |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | JSONPサービスからデータを取得し、保存します |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | 現在のユーザーのプロファイルデータを格納します |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | デバイス情報、ブラウザーの種類、ウィンドウの向きなど、クライアントに関する情報を格納します |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | ページタグとタグ数を格納します。 |

1. Experience Manager レールで、ツール／サイト／ContextHub をクリックまたはタップします。
1. デフォルトの設定コンテナをクリックまたはタップします。
1. 「Contexthub 設定」をクリックまたはタップします。
1. ストアを追加するには、「作成」アイコンをクリックまたはタップして、「ContextHub ストア設定」をクリックまたはタップします。

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. 次の基本設定のプロパティの値を指定して「次へ」をクリックまたはタップします。

   * **設定のタイトル：**&#x200B;ストアを識別するタイトル。
   * **ストアの種類：**&#x200B;ストアのベースとなるストア候補の storeType プロパティの値。
   * **必須：**&#x200B;オン。
   * **有効：**&#x200B;オンにするとストアが有効になります。

1. （オプション）デフォルトのストアの設定をオーバーライドするには、「詳細設定（JSON）」ボックスに JSON オブジェクトを入力します。
1. 「保存」をクリックまたはタップします。

## JSONP サービスの使用例  {#example-using-a-jsonp-service}

この例は、ストアを設定して UI モジュールにデータを表示する方法を示します。この例では、jsontest.comサイトのMD5サービスがストアのデータソースとして使用されています。 サービスが指定の文字列の MD5 ハッシュコードを JSON 形式で返します。

A contexthub.generic-jsonp store is configured so that it stores data for the service call `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. サービスが UI モジュールに表示される次のデータを返します。

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### contexthub.generic-jsonp ストアの作成 {#creating-a-contexthub-generic-jsonp-store}

contexthub.generic-jsonp のサンプルのストア候補を使用すると、JSON データを返す JSONP サービスや Web サービスからデータを取得できます。このストア候補では、そのストア設定を使用して、使用する JSONP サービスに関する詳細を指定します。

[JavaScriptクラスの](/help/sites-developing/contexthub-api.md#init-name-config) init `ContextHub.Store.JSONPStore` 関数は、このストア候補を初期化する `config` オブジェクトを定義します。 `config` オブジェクトには JSONP サービスに関する情報が含まれる `service` オブジェクトが含まれています。ストアを設定するには、詳細設定プロパティの値として `service` オブジェクトを JSON 形式で指定します。

jsontest.com サイトの MD5 サービスからのデータを保存するには、次のプロパティを使用して [ContextHub ストアの作成](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store)の手順に従います。

* **設定のタイトル：** md5
* **ストアの種類：** contexthub.generic-jsonp
* **必須：**&#x200B;オン。
* **有効：** 選択
* **詳細設定 (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### md5 データの UI モジュールの追加 {#adding-a-ui-module-for-the-md-data}

ContextHub ツールバーに UI モジュールを追加して、サンプルの md5 ストアに格納されているデータを表示します。この例では、contexthub.baseモジュールを使用して次のUIモジュールが生成されます。

![chlimage_1-323](assets/chlimage_1-323.png)

Use the procedure in [Adding a UI Module](#adding-a-ui-module) to add the UI module to an existing UI Mode, such as the sample Perona UI Mode. UI モジュールには、次のプロパティ値を使用します。

* **UI モジュールのタイトル：** MD5
* **モジュールタイプ：** contexthub.base
* **詳細設定 (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## ContextHub のデバッグ {#debugging-contexthub}

ContextHub のデバッグモードを有効にして、トラブルシューティングに対応できます。デバッグモードは、ContextHub 設定または CRXDE のいずれかを利用して有効にできます。

### 設定による有効化 {#via-the-configuration}

Edit the ContextHub&#39;s configuration and check the option **Debug**

1. レールで、**ツール／サイト／ContextHub** をクリックまたはタップします。
1. デフォルトの「**設定コンテナ**」をクリックまたはタップします。
1. 「**ContextHub 設定**」を選択し、「**選択した要素を編集**」をクリックまたはタップします。
1. Click or tap **Debug** and click or tap **Save**

### CRXDE による有効化 {#via-crxde}

Use CRXDE Lite to set the property `debug` to **true** under:

* `/conf/global/settings/cloudsettings` または
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>ContextHub設定が従来のパスの下にまだ存在する場合、設定する場所 `debug property` は次のとおりで `/libs/settings/cloudsettings/legacy/contexthub`す。

### サイレントモード {#silent-mode}

サイレントモードでは、すべてのデバッグ情報が無効になります。通常のデバッグオプションはContextHub設定ごとに個別に設定できますが、サイレントモードはグローバル設定で、ContextHub設定レベルの任意のデバッグ設定よりも優先されます。

これは、デバッグ情報をまったく必要としないパブリッシュインスタンスで役立ちます。 これはグローバル設定なので、OSGi を介して有効にします。

1. Open the **Adobe Experience Manager Web Console Configuration** at `http://<host>:<port>/system/console/configMgr`
1. Search for **Adobe Granite ContextHub**
1. Click the configuration **Adobe Granite ContextHub** to edit its properties
1. 「**サイレントモード**」チェックボックスをオンにし、「**保存**」をクリックします。

## アップグレード後の ContextHub の設定の復元 {#recovering-contexthub-configurations-after-upgrading}

[AEM へのアップグレード](/help/sites-deploying/upgrade.md)が実行されると、ContextHub の設定がバックアップされて安全な場所に格納されます。アップグレード中、デフォルトの ContextHub の設定がインストールされ、既存の設定が置換されます。加えられた変更や追加を保持するにはバックアップが必要です。

ContextHub設定は、次のノードの下にある名前のフォルダー `contexthub` に保存されます。

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

アップグレード後、バックアップは次の名前のノードの下にあるフォルダー `contexthub` に保存されます。

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` か `/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` のどちらかにする必要があります。

The `yyyymmdd` portion of the node name is the date when the upgrade was performed.

To recover your ContextHub configurations, use CRXDE Lite to copy the nodes that represent your stores, UI modes, and UI modules from below the `default-pre-upgrade_yyyymmdd_xxxxxx` node to below:

* `/conf/global/settings/cloudsettings` または
* `/conf/<tenant>/settings/cloudsettings`
