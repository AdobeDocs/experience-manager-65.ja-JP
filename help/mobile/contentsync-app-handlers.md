---
title: 既製のアプリハンドラー
seo-title: 既製のアプリハンドラー
description: このページでは、AEM の Adobe PhoneGap Enterprise で使用できる既製のハンドラーについて説明します。
seo-description: このページでは、AEM の Adobe PhoneGap Enterprise で使用できる既製のハンドラーについて説明します。
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

コンテンツ同期ハンドラーの開発については、以下のガイドラインを参照してください。

* Handlers must implement *com.day.cq.contentsync.handler.ContentUpdateHandler* (either directly or extending a class that does)
* ハンドラーは、*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler* を拡張できます。
* ハンドラーは、ContentSyncキャッシュを更新した場合にのみtrueを報告する必要があります。 誤って true を返すと、AEM で更新が作成されます。
* ハンドラーは、コンテンツが実際に変更された場合にのみ、キャッシュを更新する必要があります。ホワイトが不要な場合はキャッシュに書き込まず、不要な更新の作成を避けます。

## 既製のハンドラー {#out-of-the-box-handlers}

以下に、既製のアプリハンドラーのリストを示します。

**mobileappagesアプリのページをレンダリングします。**

* ***type - String*** - mobileappages
* ***path - String*** — ページへのパス
* ***extension - String*** — リクエストで使用する拡張子。 For pages this is almost always *html*, but others are still possible.

* ***selector - String*** — オプションのセレクターをドットで区切ります。 Common examples are *touch* for rendering mobile versions of a page.

* ***deep - Boolean*** — 子ページも含める必要があるかどうかを決定するオプションのブール型プロパティ。 デフォルト値は *true* です。

* ***includeImages - Boolean*** — 画像を含めるかどうかを決定するオプションのブール型プロパティ。 デフォルト値は *true* です。

   * デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントだけが追加の対象になります。

* ***includeVideos - Boolean*** — ビデオを含める必要があるかどうかを決定するオプションのブール型プロパティ。 デフォルト値は *true* です。

* ***includeModifiedPagesOnly - Boolean*** - falseの場合、または省略した場合はすべてのページがレンダリングされ、レンダリング時に更新が確認されます。 true の場合、最後に変更されたページに対する変更に基づいて差異を処理します。
* ***+ rewrite (node)***
   ***- relativeParentPath - String*** — 他のすべてのパスを書き込む相対パス。

>[!NOTE]
>
>The resource type of the image and video components that are affected by this handler is set by configuring the properties of the *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler* OSGi サービスのプロパティによって設定します。

**mobilepageassetsアプリのページアセットを収集します。**

**mobilecontentlisting** ContentSync zipの内容を表示します。 これは、デバイスのクライアント側 js によって使用され、AEM アプリで必要な最初のファイルコピーを実行します。

このハンドラーは、すべての AEM アプリコンテンツ同期設定に追加する必要があります。

* ***type - String - mobilecontentlisting***
* ***path*** - String — 空白のままにしておく必要があり、有効なハンドラーとして表示するには空白のままにする必要がありますが、pathは現在のContentSyncキャッシュと推定されます。 この値は無視されます。
* ***targetRootDirectory *-**String — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long ***- ContentSyncがこのハンドラーを実行するための順序。 この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackageslisting** 特定のアプリ内のAEMコンテンツパッケージと、更新要求を行うサーバーURLを表示します。 これは、クライアント側のデバイス上のjsを使用して、コンテンツの更新をリクエストします

このハンドラーは、AEM App Shell ContentSync Config（page-type=app-instanceのノード）で使用する必要があります

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String*** — アプリケーションシェルのパス（page-type=app-instanceのノード）。
* ***targetRootDirectory - String*** — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long ***- ContentSyncがこのハンドラーを実行する順序。 この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

>[!NOTE]
>
>以下のコードブロックは厳密な実装ではなく、参考例として使用してください。

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** ：コマンドセンターで行った編集を提供されたconfig.xmlとマージする、更新されたconfig.xmlを含みます。 このハンドラーがアプリに含まれていない場合、管理インターフェイスで変更された詳細はキャッシュに含まれません。

This handler should be used on a AEM App Shell ContentSync config (node with pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**String*** — 任意のアプリシェルの子ノードのパス(page-type=[app-instance])。
* ***targetRootDirectory - String*** — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String*** — アプリケーションのアイコンを配置するディレクトリ

**mobileADBMobileConfigJSON** ADBMobileConfig.JSONファイル（AMSクラウドサービスが設定されている場合）を含めます。

これは、解析をサポートするための AMS プラグインを設定するためにコンパイル時に使用されます。

このハンドラーは、AEM App Shell ContentSync Config（page-type=app-instanceのノード）で使用する必要があります

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** — アプリケーションシェルのパス（page-type=app-instanceを持つノードまたは/libs/mobileapps/core/components/instanceを拡張するRT）
* ***targetRootDirectory - String*** — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス

**notificationsconfig** ：デバイスに必要な通知設定を抽出します。 プロパティは、アプリに関連付けられた各プッシュサービスクラウドサービス設定から抽出されます。

Non-AEM properties in the cloud service&#39;s jcr:content node are extracted and added to the **pge-notifications-config.json** JSON  file for inclusion in the app content&#39;s www root.

AEM プロパティは、「cq」、「sling」または「jcr」のネームスペースが付いたプロパティです。他のプロパティは、コンテンツ同期設定ノードの「excludeProperties」プロパティを使用して除外できます。

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** — 除外するプロパティ

**contentsyncconfigcontent** ：既存のContentSync設定からコンテンツを収集します。

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** — 次のいずれかのパス：

   * 別のコンテンツ同期設定
   * をコンテンツパッケージに追加します（phonegap-exportTemplateプロパティを使用してContentSync設定を検索します）。
   * をモバイルリソースに追加します（アプリコンテンツはそのリソースの下にあり、それらのコンテンツパッケージにpage-includeInBuildプロパティがtrueの場合、phonegap-exportTemplateを使用してContentSync設定が見つかります）。

* ***autoCreateFirstUpdateBeforeImport — ブール値*** - trueの場合は、読み込む前に **** 、ターゲット設定に初期更新を作成します（まだ1回しか存在しない場合）

* ***autoFillBeforeImport - Boolean*** - trueの場合、読み込む前にターゲット設定を更新/入力します。
* ***configSuffix - String*** - app-contentの「phonegap-exportTemplate」プロパティに示されているパスに追加する文字列。 これは、異なる書き出しテンプレートを区別するために使用できます。 For example, this property can be set to **&quot;-dev&quot;** to indicate that *&quot;/../../../appconfig-dev&quot;* should be used (as opposed to *&quot;/../../../appconfig&quot;*).

**app-assets** ：アプリインスタンスに関連付けられているすべてのアセットを含めます。 このハンドラーには、指定されたパスに見つかったアセットと、アプリインスタンスのappAssetPathプロパティで参照されているアセットが含まれます。

* ***type - String*** - app-assets

* ***path **-**String*** — アプリアセットが保存されるアプリインスタンスの下の場所のパス

**mobileappoffers** パーソナライゼーションのユースケースに、ターゲットコンテンツをレンダリングするための新しいコンテンツ同期ハンドラーが導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者が作成した関連するターゲットオファーをレンダリングする方法を知っています。 mobileappofersハンドラーは抽象ページの更新ハンドラーを拡張するので、多くのプロパティは似ています。 mobileappoffersハンドラーの詳細には、次のプロパティがあります。

mobileappsoffers ハンドラーは mobileappspages ハンドラーを拡張し、以下のプロパティが追加されます。

* ***locationRoot - String*** — モバイルアプリケーションの場所を指定
* ***includePageTypes - String*** — デフォルトでcq/personalization/components/teaserpageおよびcq/personalization/components/offerproxyをサポート
* ***selector - String*** - tandtに設定する必要があります。
* ***path - String***— キャンペーンのブランドへのパス

**mobileappconfig** :mobileappconfigコンテンツ同期ハンドラーを使用して、MobileAppsConfig.jsonにJSONデータを挿入できます。 プロバイダークラスを登録するには、開発者のMobileAppsInfoProviderクラスをプロバイダーのリストに追加します。 ハンドラーはMobileAppsInfoProvidersのリストを繰り返し処理し、プロバイダーが結果のjsonファイルにデータを挿入できるようにします。 このハンドラーがサポートするプロパティのリストは以下のとおりです。

* ***path **-**String*** - page-type=app-instanceを持つアプリインスタンスノードへのパス、または/libs/mobileapps/core/components/instanceを拡張するRT
* ***providers - String***`[]` — 完全修飾MobileAppsInfoProvidersのリスト
* ***targetRootDirectory - String*** - mobileAppsConfig.jsonファイルを書き込むディレクトリ。
* **fileName - String** - JSONを書き込むファイルの名前（オプション）。デフォルトはMobileAppsConfig.jsonです。

それぞれが異なる JSON ファイルに書き出す固有のプロバイダーセットを持つ、複数の mobileappconfig ハンドラーを設定することもできます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**整合性消去キャッシュの確認** 手順

* キャッシュのクリア
* ハンドラーを実行（キャッシュが更新されます）
* ハンドラーを再実行（キャッシュは更新されません）

**デバッグの手順**

* 設定を実行
* 設定を書き出すか、デバイス上で確認
* レンダリングに失敗した場合は、*styles/assets/libs* があるかどうか、または *styles/assets/libs* へのパスが正しいかを確認

**Logging**`com.day.cq.contentsync` Enable ContentSync Debug logging via OSGI logger configurations on packageを使用すると、実行されたハンドラーと、それらのハンドラーがキャッシュを更新し、キャッシュを更新したかどうか、およびレポートされたキャッシュの更新を追跡できます。

## その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM での Adobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM での Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile アプリの開発の概要については、[こちら](/help/mobile/getting-started-aem-mobile.md)を参照してください。

