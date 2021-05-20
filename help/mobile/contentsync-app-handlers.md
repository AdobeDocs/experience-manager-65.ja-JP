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
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 32%

---

# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

コンテンツ同期ハンドラーの開発については、以下のガイドラインを参照してください。

* ハンドラーは、*com.day.cq.contentsync.handler.ContentUpdateHandler*&#x200B;を実装する必要があります（直接実装するか、実装するクラスを拡張する）。
* ハンドラーは、*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler* を拡張できます。
* ハンドラーは、コンテンツ同期キャッシュを更新した場合にのみtrueを報告する必要があります。 誤って true を返すと、AEM で更新が作成されます。
* ハンドラーは、コンテンツが実際に変更された場合にのみ、キャッシュを更新する必要があります。ホワイトが不要な場合はキャッシュに書き込まず、不要な更新の作成を避けます。

## 既製のハンドラー {#out-of-the-box-handlers}

以下に、既製のアプリハンドラーのリストを示します。

**** mobileappagesRendersアプリページ。

* ***type - String***  - mobileapppages
* ***path - String***  — ページへのパス
* ***extension - String***  — リクエストで使用する拡張子。ページの場合、ほとんど常に&#x200B;*html*&#x200B;ですが、他のページも引き続き使用できます。

* ***selector - String***  — オプションのセレクター（ドット区切り）。一般的な例としては、ページのモバイルバージョンをレンダリングする場合の&#x200B;*touch*&#x200B;があります。

* ***deep - Boolean***  — 子ページも含める必要があるかどうかを指定する、オプションのブール型プロパティ。デフォルト値は *true* です。

* ***includeImages - Boolean***  — 画像を含める必要があるかどうかを指定する、オプションのブール型プロパティ。デフォルト値は *true* です。

   * デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントだけが追加の対象になります。

* ***includeVideos - Boolean***  — ビデオを含める必要があるかどうかを指定する、オプションのブール型プロパティです。デフォルト値は *true* です。

* ***includeModifiedPagesOnly — ブール値***  - falseまたは省略した場合、すべてのページをレンダリングし、レンダリング時に更新を確認します。true の場合、最後に変更されたページに対する変更に基づいて差異を処理します。
* ***+ rewrite（ノード）***
   ***- relativeParentPath - String***  — 他のすべての相対パスを書き込むパス。

>[!NOTE]
>
>このハンドラーの影響を受ける画像およびビデオコンポーネントのリソースタイプは、*com.adobe.cq.mobile.platform.impl.contentsync.handler*&#x200B;のプロパティを設定することで設定します。*MobilePagesUpdateHandler* OSGi サービスのプロパティによって設定します。

**** mobilepageassetsCollectsアプリページのアセットを収集します。

**** mobilecontentlistingContentSync zipのコンテンツをリストします。これは、デバイスのクライアント側 js によって使用され、AEM アプリで必要な最初のファイルコピーを実行します。

このハンドラーは、すべての AEM アプリコンテンツ同期設定に追加する必要があります。

* ***type - String - mobilecontentlisting***
* ***path***  - String — 空のままにする。有効なハンドラーとして表示するには存在する必要がありますが、パスは現在のContentSyncキャッシュと解釈されます。この値は無視されます。
* ***targetRootDirectory*  - **文字列 — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long*  - **ContentSyncがこのハンドラーを実行する順序。この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

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

**** mobilecontentpackageslisting特定のアプリ内のAEMコンテンツパッケージと、更新要求をおこなうserverURLをリストします。これは、デバイス上のクライアント側jsを使用して、コンテンツの更新をリクエストします

ハンドラーは、AEM App Shell ContentSync Config（pge-type=app-instanceのノード）で使用する必要があります

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String***  — アプリシェルのパス（pge-type=app-instanceのノード）。
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long*  - **コンテンツ同期でこのハンドラーを実行する順序。この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

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

**** widgetconfigコマンドセンターで行われた編集を提供されたconfig.xmlと結合する、更新されたconfig.xmlを含みます。このハンドラーがアプリに含まれていない場合、管理インターフェイスで変更された詳細はキャッシュに含まれません。

このハンドラーは、AEM App Shell ContentSync設定（pge-type=[app-instance]のノード）で使用する必要があります。

* ***type - String* - **widgetconfig
* ***path **-**String***  — 任意のアプリシェルの子ノード(pge-type=[app-instance]のノード)へのパス。
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String***  — アプリのアイコンを配置するディレクトリ

**** mobileADBMobileConfigJSONI:AMSクラウドサービスが設定されている場合、ADBMobileConfig.JSONファイルを含めます。

これは、解析をサポートするための AMS プラグインを設定するためにコンパイル時に使用されます。

ハンドラーは、AEM App Shell ContentSync Config（pge-type=app-instanceのノード）で使用する必要があります

* ***type - String***  - mobileADBMobileConfigJSON
* ***path - String***  — アプリシェルのパス（pge-type=app-instanceのノードまたは/libs/mobileapps/core/components/instanceを拡張するRT）
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス

**** notificationsconfigExcraptsデバイスで必要な通知設定を抽出します。プロパティは、アプリに関連付けられた各プッシュサービスクラウドサービス設定から抽出されます。

クラウドサービスのjcr:contentノード内のAEM以外のプロパティが抽出され、**pge-notifications-config.json** JSONファイルに追加されて、アプリコンテンツのwwwルートに含められます。

AEM プロパティは、「cq」、「sling」または「jcr」のネームスペースが付いたプロパティです。他のプロパティは、コンテンツ同期設定ノードの「excludeProperties」プロパティを使用して除外できます。

* ***type - String***  - notificationsconfig
* ***excludeProperties - String[]***  — 除外するプロパティ

**** contentsyncconfigcontentContentSyncの既存の設定からコンテンツを収集します。

* ***type - String***  - contentsyncconfigcontent
* ***path - String***  — 次のいずれかへのパス。

   * 別のコンテンツ同期設定
   * をコンテンツパッケージに追加します（phonegap-exportTemplateプロパティを使用してContentSync設定を検索します）。
   * をモバイルリソースに追加します（app-contentのはそのリソースの下に見つかり、これらのコンテンツパッケージにpge-includeInBuildプロパティがtrueの場合、phonegap-exportTemplateを使用してそのContentSync設定が見つかります）。

* ***autoCreateFirstUpdateBeforeImport — ブール値***  - trueの場合、1回だけ存在しない場合は、読み込む前 **** にターゲット設定で初期更新を作成します

* ***autoFillBeforeImport — ブール値***  - trueの場合、読み込む前にターゲット設定を更新/入力します
* ***configSuffix - String***  - app-contentの「phonegap-exportTemplate」プロパティで指定されたパスに追加する文字列。これは、異なる書き出しテンプレートを区別するために使用できます。 例えば、このプロパティを&#x200B;**&quot;-dev&quot;**&#x200B;に設定して、*&quot;/../../../appconfig-dev&quot;*&#x200B;を（*&quot;/../.../appconfig&quot;*&#x200B;ではなく）使用する必要があることを示すことができます。

**app-assets：アプリイ** ンスタンスに関連付けられているすべてのアセットが含まれます。このハンドラーには、指定されたパスの下に見つかったアセットと、アプリインスタンスのappAssetPathプロパティで参照されているアセットが含まれます。

* ***type - String***  - app-assets

* ***path **-**String***  — アプリアセットが格納されるアプリインスタンス下の場所のパス。

**** mobileappoffersターゲットコンテンツをレンダリングするための新しいコンテンツ同期ハンドラーが、パーソナライゼーションの使用例に導入されました。「mobileappoffers」ハンドラーは、コンテンツ作成者が作成した関連するターゲットオファーをレンダリングする方法を認識しています。 mobileappoffersハンドラーは抽象ページ更新ハンドラーを拡張するので、多くのプロパティは似ています。 mobileappoffersハンドラーの詳細には、次のプロパティがあります。

mobileappsoffers ハンドラーは mobileappspages ハンドラーを拡張し、以下のプロパティが追加されます。

* ***locationRoot - String***  — モバイルアプリケーションの場所を指定します
* ***includePageTypes - String***  — デフォルトでcq/personalization/components/teaserpageおよびcq/personalization/components/offerproxyをサポートします。
* ***selector - String***  - tandtに設定する必要があります。
* ***path - String*** — キャンペーンのブランドへのパス。

**** mobileappconfigmobileappconfigコンテンツ同期ハンドラーは、JSONデータをMobileAppsConfig.jsonに挿入する方法を提供します。プロバイダークラスを登録するには、開発者のMobileAppsInfoProviderクラスをプロバイダーのリストに追加します。 ハンドラーは、MobileAppsInfoProvidersのリストを反復し、プロバイダーが結果のjsonファイルにデータを挿入できるようにします。 このハンドラーがサポートするプロパティのリストは以下のとおりです。

* ***path **-**String***  - pge-type=app-instanceを持つアプリインスタンスノードへのパス、または/libs/mobileapps/core/components/instanceを拡張するRTへのパス。
* ***providers - String*** `[]`  — 完全修飾MobileAppsInfoProvidersのリスト
* ***targetRootDirectory - String***  - MobileAppsConfig.jsonファイルの書き込み先ディレクトリ。
* **fileName - String**  - JSONを書き込むファイルのオプション名。デフォルトはMobileAppsConfig.jsonです。

それぞれが異なる JSON ファイルに書き出す固有のプロバイダーセットを持つ、複数の mobileappconfig ハンドラーを設定することもできます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**IntegrityClearキャッシュを確認** する手順

* キャッシュのクリア
* ハンドラーを実行（キャッシュが更新されます）
* ハンドラーを再実行（キャッシュは更新されません）

**デバッグの手順**

* 設定を実行
* 設定を書き出すか、デバイス上で確認
* レンダリングに失敗した場合は、*styles/assets/libs* があるかどうか、または *styles/assets/libs* へのパスが正しいかを確認

**** パッケージのOSGIロガー設定を介したLoggingEnable ContentSync Debugログ。実行されたハンドラー `com.day.cq.contentsync` と、ハンドラーがキャッシュを更新し、キャッシュの更新を報告したかどうかを追跡できます。

## その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM での Adobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM での Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile アプリの開発の概要については、[こちら](/help/mobile/getting-started-aem-mobile.md)を参照してください。
