---
title: モバイルデバイス用サイトの作成
description: モバイルサイトの作成は、標準サイトの作成と似ていますが、テンプレートやコンポーネントの作成も含まれます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '3787'
ht-degree: 40%

---

# モバイルデバイス用サイトの作成{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

モバイルサイトの作成は、標準サイトの作成と似ています。また、テンプレートとコンポーネントの作成も含まれます。 テンプレートとコンポーネントの作成について詳しくは、次のページを参照してください。 [テンプレート](/help/sites-developing/templates.md), [コンポーネント](/help/sites-developing/components.md)、および [AEM Sitesの開発の手引き](/help/sites-developing/getting-started.md). 主な違いは、サイト内でのAdobe Experience Manager(AEM) 組み込みモバイル機能の有効化です。 そのためには、モバイルページコンポーネントを使用するテンプレートを作成します。

使用を検討 [レスポンシブデザイン](/help/sites-developing/responsive.md)：複数の画面サイズに対応する単一のサイトを作成します。

まず、 **We.Retail モバイルデモサイト** AEMで使用可能な

モバイルサイトを作成するには、次の手順に従います。

1. ページコンポーネントを作成します。

   * `sling:resourceSuperType` プロパティを `wcm/mobile/components/page` に設定します。
このようにすることで、コンポーネントはモバイルページコンポーネントに依存します。

   * を作成します。 `body.jsp` プロジェクト固有のロジックを使用します。

1. ページテンプレートを作成します。

   * `sling:resourceType` プロパティを新しく作成したページコンポーネントに設定します。
   * `allowedPaths` プロパティを設定します。

1. サイト用のデザインページを作成します。
1. `/content` ノードの下にサイトのルートページを作成します。

   * `cq:allowedTemplates` プロパティを設定します。
   * `cq:designPath` プロパティを設定します。

1. サイトのルートページのページプロパティの「**モバイル**」タブで、デバイスグループを設定します。
1. 新しいテンプレートを使用してサイトページを作成します。

モバイルページコンポーネント（`/libs/wcm/mobile/components/page`）：

* ページプロパティダイアログに「**モバイル**」タブを追加します。
* `head.jsp` を使用して、現在のモバイルデバイスグループを要求から取得します。デバイスグループが見つかった場合は、そのグループの `drawHead()` メソッドを使用して、デバイスグループの関連するエミュレーターの init コンポーネント（オーサーモードの場合のみ）とデバイスグループのレンダリング CSS をインクルードします。

>[!NOTE]
>
>モバイルサイトのルートページはノード階層のレベル 1 に位置する必要があります。また、このページを /content ノードの下に配置することをお勧めします。

## マルチサイトマネージャーによるモバイルサイトの作成 {#creating-a-mobile-site-with-the-multi-site-manager}

マルチサイトマネージャー (MSM) を使用して、標準サイトからモバイルライブコピーを作成します。 標準サイトは、モバイルサイトに自動的に変換されます。モバイルサイトには、モバイルサイトのすべての機能（エミュレーター内のエディションなど）があり、標準サイトと同期して管理できます。 の節を参照してください。 [様々なチャネル用のライブコピーの作成](/help/sites-administering/msm.md) をクリックします。

## サーバー側モバイル API {#server-side-mobile-api}

モバイルクラスを含む Java™パッケージは次のとおりです。

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - MobileConstants を定義します。
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - Device、DeviceGroup および DeviceGroupList を定義します。
* [com.day.cq.wcm.mobile.api.device.capability](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - DeviceCapability を定義します。
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - WurflQueryEngine を定義します。
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - WCM モバイルに関連するさまざまなユーティリティメソッドを提供する MobileUtil を定義します。

### モバイルコンポーネント {#mobile-components}

**We.Retail モバイルデモサイト** では、`/libs/foundation/components` にある以下のモバイルコンポーネントを使用します。

<table>
 <tbody>
  <tr>
   <td>名前</td>
   <td>グループ</td>
   <td>特徴</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>hidden</td>
   <td> — フッター</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>モバイル</td>
   <td> — 画像の基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>モバイル</td>
   <td> — リストの基盤コンポーネントに基づく<br /> - listitem_teaser.jsp （デバイスが対応している場合）は、画像をレンダリングします。<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>hidden</td>
   <td> — ロゴの基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>モバイル</td>
   <td><p>- reference 基盤コンポーネントと同様</p> <p>- textimage コンポーネントを mobiletextimage コンポーネントに、画像コンポーネントを mobileimage コンポーネントにマッピングします</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>モバイル</td>
   <td>- textimage 基盤コンポーネントに基づく<br />  — デバイスが対応している場合に画像をレンダリングします</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>hidden</td>
   <td><p>- topnav 基盤コンポーネントに基づく</p> <p> — テキストのみをレンダリングします</p> </td>
  </tr>
 </tbody>
</table>

#### モバイルコンポーネントの作成 {#creating-a-mobile-component}

AEM モバイルフレームワークを使用すると、要求を発行するデバイスを感知するコンポーネントを開発できます。以降の節のコード例は、コンポーネントの jsp で AEM モバイル API を使用する方法を示しています。具体的には、次に示す処理の方法を示します。

* リクエストからデバイスを取得します。
  `Device device = slingRequest.adaptTo(Device.class);`

* デバイスグループを取得します。
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* デバイスグループの機能を取得します。
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* デバイスの属性（WURFL データベースから生の機能のキーと値）を取得します。
  `Map<String,String> deviceAttributes = device.getAttributes();`

* デバイスのユーザーエージェントを取得します。
  `String userAgent = device.getUserAgent();`

* 現在のページからデバイスグループリスト（作成者によってサイトに割り当てられたデバイスグループ）を取得します。
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* デバイスグループが画像をサポートしているかどうかを確認
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
または
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>jsp では、`slingRequest` は `<sling:defineObjects>`タグ、`currentPage` は `<cq:defineObjects>` タグを通じて利用できます。

### エミュレーター {#emulators}

エミュレーターに基づくオーサリングを使用すると、作成者はモバイルクライアント向けのコンテンツページを作成できます。モバイルコンテンツのオーサリングは、インプレース WYSIWYG 編集の同じ原則に従います。作成者がモバイルデバイスでのページの外観を確認できるように、モバイルコンテンツページはデバイスエミュレーターを使用して編集されます。

モバイルデバイスエミュレーターは、汎用のエミュレーターフレームワークに基づいています。 詳しくは、 [エミュレーター](/help/sites-developing/emulators.md).

デバイスエミュレーターのページには、モバイルデバイスが表示されます。一方、通常の編集（parsys、コンポーネント）は、デバイスの画面内でおこなわれます。デバイスエミュレーターは、サイト用に設定されるデバイスグループに依存します。1 つのデバイスグループに複数のエミュレーターを割り当てることができます。これにより、すべてのエミュレーターをコンテンツページで使用できるようになります。デフォルトで表示されるのは、サイトに割り当てた最初のデバイスグループに割り当てられた最初のエミュレーターです。ページ上部にあるエミュレーターのカルーセルまたはサイドキックの編集ボタンを使用してエミュレーターを切り替えることができます。

**エミュレーターの作成**

エミュレーターを作成するには、 [カスタムモバイルエミュレーターの作成](/help/sites-developing/emulators.md) （汎用エミュレーターページ内）

**モバイルエミュレーターの主な特徴**

* デバイスグループは、次のエミュレーターの 1 つで構成されます。デバイスグループの設定ページ（例：/etc/mobile/groups/touch）には、 `emulators` 以下のプロパティ `jcr:content` ノード。
メモ：同じエミュレーターが複数のデバイスグループに属する可能性もありますが、あまり意味がありません。

* デバイスグループの設定ダイアログから、 `emulators` プロパティは、目的のエミュレーターのパスを使用して設定します。 （例：`/libs/wcm/mobile/components/emulators/iPhone4`）。

* エミュレーターコンポーネント ( 例： `/libs/wcm/mobile/components/emulators/iPhone4`) 基本モバイルエミュレーターコンポーネントを拡張する ( `/libs/wcm/mobile/components/emulators/base`) をクリックします。

* デバイスグループを設定する際は、基本のモバイルエミュレーターを拡張するすべてのコンポーネントを選択できます。 これにより、カスタムエミュレーターを簡単に作成または拡張できます。
* 編集モードの要求時に、エミュレーターの実装を使用してページがレンダリングされます。
* ページのテンプレートでモバイルページコンポーネントを使用する場合は、エミュレーターの機能が（モバイルページコンポーネントの `head.jsp` を使用して）自動的にページに統合されます。

### Device Groups {#device-groups}

モバイルデバイスグループは、デバイスの機能に基づいてモバイルデバイスをセグメント化します。 デバイスグループは、オーサーインスタンス上のエミュレーターベースのオーサリングと、パブリッシュインスタンス上での正しいコンテンツレンダリングに必要な情報を提供します。作成者がモバイルページにコンテンツを追加して公開したら、そのページをパブリッシュインスタンスでリクエストできます。 そこで、エミュレーターの編集ビューの代わりに、設定済みのデバイスグループの 1 つを使用してコンテンツページがレンダリングされます。 デバイスグループの選択は、 [モバイルデバイス検出](#devicedetection). 次に、対応するデバイスグループが、必要なスタイル設定情報を提供します。

デバイスグループは、`/etc/mobile/devices` の下のコンテンツページとして定義され、**モバイルデバイスグループ** テンプレートを使用します。デバイスグループテンプレートは、コンテンツページのフォームでデバイスグループ定義用の設定テンプレートとして機能します。このダイアログの主な特徴を次に示します。

* 場所: `/libs/wcm/mobile/templates/devicegroup`
* 許可されたパス： `/etc/mobile/groups/*`
* ページコンポーネント: `wcm/mobile/components/devicegroup`

#### サイトへのデバイスグループの割り当て {#assigning-device-groups-to-your-site}

モバイルサイトを作成する場合は、サイトにデバイスグループを割り当てる必要があります。 AEMは、デバイスのHTMLおよび JavaScript レンダリング機能に応じて、次の 3 つのデバイスグループを提供します。

* **機能** 携帯電話、Sony Ericsson W800 などの機能デバイス ( 基本HTMLはサポートされますが、画像や JavaScript はサポートされません )。
* **スマート** 携帯電話、BlackBerry®などのデバイス ( 基本的なHTMLと画像はサポートされますが、JavaScript はサポートされません )。

* **タッチ** 携帯電話、iPadなどのデバイス用。HTML、画像、JavaScript、デバイスの回転を完全にサポートします。

エミュレーターをデバイスグループに関連付けることができます（[デバイスグループの作成](#creating-a-device-group) を参照）。デバイスグループをサイトに割り当てると、作成者は、ページの編集用にデバイスグループに関連付けられている複数のエミュレーターの中から選択できます。

サイトにデバイスグループを割り当てるには：

1. ブラウザーで、**Siteadmin** コンソールに移動します。
1. 以下のモバイルサイトのルートページを開きます。 **Web サイト**.
1. ページのプロパティを開きます。
1. を選択します。 **モバイル** タブ：

   * デバイスグループを定義します。
   * 「**OK**」をクリックします。

>[!NOTE]
>
>デバイスグループがサイトに対して定義されている場合、それらはサイトのすべてのページに継承されます。

#### デバイスグループフィルター {#device-group-filters}

デバイスグループフィルターは、デバイスがグループに属するかどうかを指定するための、機能に基づく条件を定義します。デバイスグループの作成時には、デバイスの評価に使用するフィルターを選択できます。

AEMがデバイスから HTTP リクエストを受け取ると、実行時に、グループに関連付けられている各フィルターが、デバイスの機能と特定の条件を比較します。 フィルターが必要とするすべての機能を持つデバイスは、グループに属していると見なされます。 機能は WURFL™ データベースから取得されます。

デバイスグループは、機能検出に 0 個以上のフィルターを使用できます。 また、1 つのフィルターを複数のデバイスグループで使用することもできます。 AEMには、グループに対して選択された機能をデバイスに含めるかどうかを決定するデフォルトのフィルターが用意されています。

* CSS
* JPG 画像と PNG 画像
* JavaScript
* デバイスの回転

デバイスグループでフィルターを使用しない場合、デバイスが要求するのは、グループ用に設定された選択済みの機能のみです。

詳しくは、[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)を参照してください。

#### デバイスグループの作成 {#creating-a-device-group}

AEMがインストールするグループが要件を満たさない場合は、デバイスグループを作成します。

1. ブラウザーで、 **ツール** コンソール。
1. 以下にページを作成 **ツール** > **モバイル** > **デバイスグループ**. 内 **ページを作成** ダイアログ：

   * 形式 **タイトル**&#x200B;を入力して、 `Special Phones`.

   * 形式 **名前**&#x200B;を入力して、 `special`.

   * を選択します。 **モバイルデバイスグループテンプレート**.
   * 「**作成**」をクリックします。

1. CRXDE で、デバイスグループ用のスタイルを格納する **static.css** ファイルを `/etc/mobile/groups/special` ノードの下に追加します。

1. **Special Phones** ページを開きます。
1. デバイスグループを設定するには、「**設定**」の横にある「**編集**」ボタンをクリックします。「**一般**」タブで、次の設定をおこないます。

   * **タイトル**：モバイルデバイスグループの名前
   * **説明**:グループの説明。
   * **User-Agent**:デバイスを照合するユーザーエージェント文字列。 これはオプションで、正規表現にすることができます。 例：`BlackBerryZ10`
   * **機能**:グループが画像、CSS、JavaScript、デバイスの回転のいずれを処理できるかを定義します。
   * **画面の最小の幅**&#x200B;および&#x200B;**高さ**
   * **エミュレーターを無効にする**:：コンテンツ編集中にエミュレーターを有効/無効にします。

   の **エミュレーター** タブ：

   * **エミュレーター**：デバイスグループに割り当てられたエミュレーターを選択します。

   の **フィルター** タブ：

   * フィルターを追加するには、「項目を追加」をクリックし、ドロップダウンリストからフィルターを選択します。
   * フィルターは、表示順に評価されます。 デバイスがフィルターの条件を満たさない場合、リスト上の後続のフィルターは評価されません。

1. 「OK」をクリックします。

モバイルデバイスグループの設定ダイアログは、次のように表示されます。

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### デバイスグループごとのカスタム CSS {#custom-css-per-device-group}

前述のように、カスタム CSS をデバイスグループページに関連付けることができます。これは、デザインページの CSS と同様です。 この CSS は、オーサー環境およびパブリッシュ環境でのページコンテンツのデバイスグループ固有のレンダリングに影響を与えるために使用されます。 この CSS は自動的に含まれます。

* オーサーインスタンスのページで、このデバイスグループで使用されるすべてのエミュレーター用に。
* パブリッシュインスタンス上のページで、要求のユーザーエージェントがこの特定のデバイスグループ内のモバイルデバイスと一致する場合。

## サーバー側デバイス検出 {#server-side-device-detection}

HTTP 要求を実行するデバイスの機能を決定するには、フィルターとデバイス仕様のライブラリを使用します。

### デバイスグループフィルターの開発 {#develop-device-group-filters}

デバイスグループフィルターを作成して、一連のデバイス機能要件を定義します。 必要なデバイス機能のグループをターゲットにするために必要な数のフィルターを作成します。

組み合わせを使用して機能のグループを定義できるようにフィルターをデザインします。 通常、異なるデバイスグループの機能が重複します。 したがって、複数のデバイスグループ定義で一部のフィルターを使用する場合があります。

作成したフィルターは、グループ設定で使用できます。

詳しくは、を参照してください。 [デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md).

### WURFL™データベースの使用 {#using-the-wurfl-database}

AEMは、 [WURFL](https://wurfl.sourceforge.net/)™デバイスの User-Agent に基づいて、デバイスの機能（画面の解像度や JavaScript のサポートなど）を問い合わせるデータベース。

WURFL™ データベースの XML コードは、`wurfl.xml` ファイル（`/libs/wcm/mobile/devicespecs/wurfl.xml.`）を解析することによって、`/var/mobile/devicespecs` の下にあるノードとして表されます。ノードに対する拡張は `cq-mobile-core` バンドルの初回起動時に行われます。

デバイスの機能はノードのプロパティとして保存され、ノードはデバイスモデルを表します。 クエリを使用して、デバイスまたはユーザーエージェントの機能を取得できます。

WURFL™データベースが進化しているので、カスタマイズまたは置き換えが必要になる場合があります。 モバイルデバイスデータベースを更新するには、次のオプションがあります。

* この使用を許可するライセンスをお持ちの場合は、ファイルを最新バージョンに置き換えます。 「別の WURFL データベースのインストール」を参照してください。
* AEM で使用可能なバージョンを使用して、ユーザーエージェント文字列を照合し、既存の WURFL™ デバイスを指定する正規表現を設定します。[正規表現に基づくユーザーエージェント照合の追加](#adding-a-regexp-based-user-agent-matching)を参照してください。

#### WURFL™機能へのユーザーエージェントのマッピングのテスト {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

デバイスがモバイルサイトにアクセスすると、AEMはデバイスを検出し、その機能に従ってデバイスグループにマッピングし、デバイスグループに対応するページのビューを送信します。 対応するデバイスグループが、必要なスタイル設定情報を提供します。 このマッピングをモバイルのユーザーエージェントテストページでテストできます。

`https://localhost:4502/etc/mobile/useragent-test.html`

#### 別の WURFL™ データベースのインストール {#installing-a-different-wurfl-database}

AEMと共にインストールされる切り捨てられた WURFL™データベースは、2011 年 8 月 30 日より前のリリースです。 お使いのバージョンの WURFL が 2011 年 8 月 30 日以降にリリースされた場合は、使用状況がライセンスに準拠していることを確認してください。

WURFL™ データベースをインストールするには：

1. CRXDE Lite で、`/apps/wcm/mobile/devicespecs` フォルダーを参照します。
1. WURFL™ ファイルをそのフォルダーにコピーします。
1. ファイル名を `wurfl.xml` に変更します。

AEM は `wurfl.xml` ファイルを自動的に解析して、`/var/mobile/devicespecs` の下にあるノードを更新します。

>[!NOTE]
>
>WURFL™データベース全体が有効になっている場合、解析とアクティベーションに数分かかる場合があります。 ログで進行状況を確認できます。

#### 正規表現に基づくユーザーエージェントの照合の追加 {#adding-a-regexp-based-user-agent-matching}

ユーザーエージェントを /apps/wcm/mobile/devicespecs/wurfl/regexp に正規表現として追加して、既存の WURFL™ デバイスタイプを指定します。

1. In **CRXDE Lite**/apps/wcm/mobile/devicespecs/regexp の下にノードを作成します。例： `apple_ipad_ver1`.
1. ノードに次のプロパティを追加します。

   * **正規表現**:ユーザーエージェントを定義する正規表現。例：&#42;Mozilla.&#42;iPad.&#42;AppleWebKit。&#42;Safari.&#42;
   * **deviceId**:wurfl.xml で定義されたデバイス ID。例： `apple_ipad_ver1`

上記の設定によって、ユーザーエージェントが指定の正規表現に一致するデバイスが、WURFL™ デバイス ID である apple_ipad_ver1（存在する場合）にマップされます。

## クライアント側のデバイス検出 {#client-side-device-detection}

この節では、AEMのデバイスクライアント側検出を使用して、ページレンダリングを最適化する方法、またはクライアントに代替の Web サイトバージョンを提供する方法について説明します。

AEM は `BrowserMap` に基づくデバイスのクライアントサイド検出をサポートしています。`BrowserMap` は、`/etc/clientlibs/browsermap` 下のクライアントライブラリとして AEM に同梱されています。

`BrowserMap` では、次の 3 つの方法を使用して、代替 Web サイトをクライアントに提供できます。この方法は、次の順序で使用されます。

1. [代替リンク](#providing-alternate-links)
1. [デバイスグループ専用の URL](#definingdevicegroupspecificurl)
1. [セレクターベースの URL](#defining-selector-based-urls)

>[!NOTE]
>
クライアントライブラリの統合について詳しくは、 [クライアント側HTMLライブラリの使用](/help/sites-developing/clientlibs.md).

### 代替リンクの設定 {#providing-alternate-links}

`PageVariantsProvider` OSGi サービスは、同じファミリーに属するサイトに対して代替リンクを生成できます。サービスで考慮されるサイトを設定するには、 `cq:siteVariant` ノードを `jcr:content` ノードをサイトのルートから削除します。

この `cq:siteVariant` ノードには次のプロパティが必要です。

* `cq:childNodesMapTo`  — 子ノードをマッピングするリンク要素の属性を決定します。ルートノードの子がグローバル web サイトの言語バリアントのルートを表すように、web サイトのコンテンツを整理することをお勧めします ( 例： `/content/mysite/en`, `/content/mysite/de`) の場合、 `cq:childNodesMapTo` は、 `hreflang`;
* `cq:variantDomain` - ページバリアントの絶対 URL を生成するために使用する `Externalizer` ドメインを示します。この値が設定されていない場合は、相対リンクを使用してページバリアントが生成されます。
* `cq:variantFamily` - このサイトが属する Web サイトのファミリーを示します。同じ Web サイトのデバイス特有の複数の表現は同じファミリーに属している必要があります。
* `media` - リンク要素のメディア属性の値を格納します。`BrowserMap` が登録した `DeviceGroups` の名前を使用することをお勧めします。これにより、`BrowserMap` ライブラリは、クライアントを Web サイトの適切なバリアントに自動的に転送できます。

#### PageVariantsProvider と Externalizer {#pagevariantsprovider-and-externalizer}

When the value of `cq:variantDomain` プロパティ `cq:siteVariant` ノードが空でない場合、 `PageVariantsProvider` この値を `Externalizer` サービス。 使用する設定を反映させるために、`Externalizer`サービスの設定を確認します。

>[!NOTE]
>
AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### デバイスグループ固有の URL の定義 {#defining-a-device-group-specific-url}

代替リンクを使用しない場合は、各 `DeviceGroup` にグローバル URL を設定できます。Adobeでは、 `browsermap.standard` クライアントライブラリを作成しますが、デバイスグループは再定義されます。

BrowserMap は、同じ名前のデバイスグループを作成し、に追加することで、デバイスグループの定義を上書きできるように設計されています。 `BrowserMap` オブジェクトをカスタマイズしたクライアントライブラリから取得します。

>[!NOTE]
>
詳しくは、 [カスタマイズされた BrowserMap](#creatingacustomisedbrowsermap).

### セレクターベースの URL の定義 {#defining-selector-based-urls}

代替サイトを示すために以前のメカニズムが使用されていない場合 `BrowserMap`を選択した後、 `DeviceGroups` が `URL`の場合は、リクエストを処理する独自のサーブレットを提供する必要があります。

例えば、`www.example.com/index.html` を閲覧するデバイスが BrowserMap によって `smartphone` と識別された場合、そのデバイスは `www.example.com/index.smartphone.html.` に転送されます。

### ページでの BrowserMap の使用 {#using-browsermap-on-your-pages}

ページで標準の BrowserMap クライアントライブラリを使用するには、 `/libs/wcm/core/browsermap/browsermap.jsp` ファイルを `cq:include`タグをページの `head` 」セクションに入力します。

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

`JSP` ファイルで `BrowserMap` クライアントライブラリを追加する以外にも、`client-side` に設定した `cq:deviceIdentificationMode` 文字列プロパティを web サイトのルートの下にある `jcr:content` ノードに追加する必要があります。

### BrowserMap のデフォルト動作の上書き {#overriding-browsermap-s-default-behaviour}

をカスタマイズする場合 `BrowserMap`  — 上書きによる `DeviceGroups` プローブを追加する — 次に、埋め込む独自のクライアント側ライブラリを作成する必要があります。 `browsermap.standard`クライアントサイドライブラリ。

さらに、`JavaScript` コードで `BrowserMap.forwardRequest()` メソッドを手動で呼び出す必要があります。

>[!NOTE]
>
クライアントライブラリの統合について詳しくは、 [クライアント側HTMLライブラリの使用](/help/sites-developing/clientlibs.md).

カスタマイズした `BrowserMap` クライアントライブラリのAdobeでは、次の方法を推奨しています。

1. アプリケーションで `browsermap.jsp` ファイルを作成します。

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. head セクションに `broswermap.jsp` ファイルをインクルードします。

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### 特定のページからの BrowserMap の除外 {#excluding-browsermap-from-certain-pages}

クライアント検出を必要としない一部のページから BrowserMap ライブラリを除外する場合は、request 属性を追加できます。

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

これにより、`/libs/wcm/core/browsermap/browsermap.jsp` スクリプトは、`BrowserMap` が検出を行わないようにする meta タグをページに追加するようになります。

```xml
<meta name="browsermap.enabled" content="false">
```

### Web サイトの特定のバージョンのテスト {#testing-a-specific-version-of-a-web-site}

通常、BrowserMap スクリプトは常に最適なバージョンの Web サイトに訪問者をリダイレクトします。通常、必要に応じて、訪問者をデスクトップまたはモバイルサイトにリダイレクトします。

リクエストのデバイスに Web サイトの特定のバージョンをテストするように強制できます。その場合、 `device` パラメーターを URL に追加します。 次の URL は、モバイルバージョンのGeometrixx OutdoorsWeb サイトをレンダリングします。

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
この `wcmmode` パラメーターが `disabled` を使用して、パブリッシュインスタンスの動作をシミュレートします。

上書きするデバイス値は cookie に保存されるので、 `device` 各 `URL`.

そのため、同じ `URL` と `device` に設定 `browser` をクリックして、Web サイトのデスクトップバージョンに戻ります。

>[!NOTE]
>
BrowserMap は、上書きするデバイス値を、 `BMAP_device`. この cookie を削除すると、CQ は現在のデバイス（デスクトップやモバイルなど）に応じて適切なバージョンの Web サイトを提供するようになります。

## モバイルの要求の処理 {#mobile-request-processing}

AEM は、タッチデバイスグループに属するモバイルデバイスが発行した要求を次のように処理します。

1. iPadがAEMパブリッシュインスタンスにリクエストを送信します。例えば、 `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEMは、リクエストされたページのサイトがモバイルサイトかどうかを判断します（第 1 レベルのページかどうかを調べます）。 `/content/geometrixx_mobile` は、モバイルページコンポーネントを拡張したものです )。 モバイルサイトである場合は、次の処理が行われます。
1. AEM が要求ヘッダーのユーザーエージェントに基づいてデバイスの機能を検出します。
1. AEM がデバイスの機能をデバイスグループにマップし、デバイスグループセレクターとして`touch`を設定します。
1. AEM がリクエストを `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.` にリダイレクト 
1. AEM が応答を iPad に送信します。

   * `products.touch.html` は通常の方法でレンダリングされます。このページはキャッシュ可能です。
   * レンダリングコンポーネントでは、セレクターを使用してプレゼンテーションを変更します。
   * AEM では、ページ内のすべての内部リンクにモバイルセレクターを自動的に追加します。

### 統計 {#statistics}

モバイルデバイスから AEM サーバーに対して行われたリクエスト数に関する一部の統計を取得できます。リクエスト数は次のように分類できます。

* デバイスグループごと、およびデバイス
* 年、月、日

統計を表示するには：

1. 次に移動： **ツール** コンソール。
1. を開きます。 **デバイス統計** 下のページ **ツール** > **モバイル**.
1. リンクをクリックすると、特定の年、月または日の統計を表示できます。

この **統計** ページは次のようになります。

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
**統計**&#x200B;ページは、モバイルデバイスが初めて AEM にアクセスし、そのデバイスが検出されると作成されます。それ以前にこのページを使用することはできません。

統計内にエントリを生成する必要がある場合は、次の手順を実行できます。

1. モバイルデバイスまたはエミュレーター（例えば、Firefox の場合は https://chrispederick.com/work/user-agent-switcher/）を使用します。
1. オーサリングモードを無効にして、オーサーインスタンス上のモバイルページをリクエストします。次に例を示します。
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

これで、**統計**&#x200B;ページを使用できるようになります。

### 「友人にリンクを送信」リンク用のページキャッシュのサポート {#supporting-page-caching-for-send-link-to-a-friend-links}

モバイルページは Dispatcher 上でキャッシュ可能です。これは、デバイスグループ用にレンダリングされるページは、デバイスグループセレクターによってページ URL 内で識別されるからです。 `/content/mobilepage.touch.html`. セレクターのないモバイルページへのリクエストはキャッシュされないので、この場合、デバイス検出が動作し、最終的に一致するデバイスグループ（またはその件に関しては「一致しない」）にリダイレクトされます。 デバイスグループセレクターを使用してレンダリングされたモバイルページは、リンクリライターによって処理されます。このリンクは、ページ内のすべてのリンクを書き換え、デバイスグループセレクターも含みます。

したがって、次のシナリオが発生する可能性があります。

Alice というユーザーが `coolpage.feature.html` にリダイレクトされ、その URL を友人の Bob に送信します。Bob は `touch` デバイスグループに分類される別のクライアントを使用してその URL にアクセスします。

`coolpage.feature.html` がフロントエンドキャッシュから提供される場合、要求を分析して、モバイルセレクターが新しいユーザーエージェントに一致しないことを確認する機会が AEM にはありません。そのため、Bob は誤った表現を取得することになります。

この問題を解決するために、単純な選択の UI をページにインクルードできます。このようなページでは、AEM で選択されたデバイスグループをエンドユーザーが上書きできます。上記の例では、ページ上のリンク（またはアイコン）により、エンドユーザーは `coolpage.touch.html` もし彼らが自分のデバイスがそれに対して十分に良いと思うなら
