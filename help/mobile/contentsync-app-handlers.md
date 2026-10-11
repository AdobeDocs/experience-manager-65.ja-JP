---
title: 既製のアプリハンドラー
description: このページでは、Adobe PhoneGap EnterpriseとAEMの組み合わせですぐに使用できるハンドラーについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 1%
---
# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

コンテンツ同期ハンドラーの開発については、次のガイドラインを参照してください。

* ハンドラーは&#x200B;*com.day.cq.contentsync.handler.ContentUpdateHandler*&#x200B;を実装する必要があります（直接実装するか、実装するクラスを拡張する必要があります）
* ハンドラーは&#x200B;*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*&#x200B;を拡張できます
* ハンドラーは、ContentSync キャッシュを更新した場合にのみtrueを報告する必要があります。 誤ったレポートがtrueの場合、AEMは更新を作成できます。
* ハンドラーは、コンテンツが実際に変更された場合にのみキャッシュを更新する必要があります。 ホワイトが不要な場合はキャッシュに書き込まないでください。不要なアップデートの作成を避けてください。

## Out of the Box ハンドラー {#out-of-the-box-handlers}

次に、すぐに使えるアプリハンドラーの一覧を示します。

**mobileapppages** アプリページをレンダリングします。

* ***type - String*** - mobileapppages
* ***path - String*** - ページへのパス
* ***extension - String*** - リクエストで使用する拡張機能。 ページの場合は、ほとんどの場合&#x200B;*html*&#x200B;ですが、他のページでも可能です。

* ***selector - String*** - オプションのセレクターをドットで区切ります。 一般的な例は、ページのモバイルバージョンをレンダリングするための&#x200B;*touch*&#x200B;です。

* ***deep - Boolean*** – 子ページを含めるかどうかを決定するオプションのブール値プロパティです。 デフォルト値は&#x200B;*trueです。*

* ***includeImages - Boolean*** – 画像を含める必要があるかどうかを決定するオプションのブール値プロパティ。 デフォルト値は&#x200B;*true*&#x200B;です。

  * デフォルトでは、リソースタイプがfoundation/components/imageの画像コンポーネントのみが含まれると見なされます。

* ***includeVideos - Boolean*** - ビデオを含める必要があるかどうかを決定するオプションのブール値プロパティ。 デフォルト値は&#x200B;*true*&#x200B;です。

* ***includeModifiedPagesOnly - Boolean*** - falseまたは省略した場合は、すべてのページをレンダリングし、レンダリングで更新を確認します。 trueの場合は、lastModified ページへの変更に基づいて差分を生成します。
* ***+書き換え（ノード）***
  ***- relativeParentPath - String*** – 他のすべての相対パスを書き込むパス。

>[!NOTE]
>
>このハンドラーの影響を受ける画像およびビデオコンポーネントのリソースタイプは、*com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler OSGi サービス*&#x200B;のプロパティを設定することで設定されます。

**mobilepageassets**&#x200B;は、アプリページのアセットを収集します。

**mobilecontentlisting** ContentSync zipのコンテンツを一覧表示します。 これは、AEM アプリケーションに必要な初期ファイルコピーを実行するために、デバイス上のクライアントサイド jsで使用されます。

このハンドラーは、任意のAEM Apps ContentSync設定に追加する必要があります。

* ***type - String - mobilecontentlisting***
* ***path*** – 文字列 – 空のままにする。有効なハンドラーと見なすには存在する必要がありますが、パスは現在のContentSync キャッシュであると推測されます。 この値は無視されます。
* ***targetRootDirectory* -**文字列 – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ContentSyncがこのハンドラーを実行するための&#x200B;***注文 – Long* -**注文。 この数値は、100など、他のすべてのハンドラーよりも高く設定する必要があります。 従来のコンテンツハンドラーの後で実行する必要があります。

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

**mobilecontentpackageslisting**&#x200B;特定のアプリ内のAEM コンテンツパッケージと、更新リクエストを行うためのserverURLを一覧表示します。 これは、コンテンツの更新をリクエストするためにデバイス上のクライアントサイド jsで使用されます

ハンドラーは、AEM App Shell ContentSync Config （node with pge-type=app-instance）で使用する必要があります

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String*** - アプリシェルへのパス（pge-type=app-instanceを持つノード）。
* ***targetRootDirectory - String*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ContentSyncがこのハンドラーを実行するための&#x200B;***注文 – Long* -**注文。 この数値は、100など、他のすべてのハンドラーよりも高く設定する必要があります。 従来のコンテンツハンドラーの後で実行する必要があります。

>[!NOTE]
>
>次のコードブロックは完全な実装ではないので、参照例として使用する必要があります。

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

**widgetconfig** コマンドセンターを介して行われた編集を、指定されたconfig.xmlと結合する、更新されたconfig.xmlが含まれます。 このハンドラーが含まれていない場合、管理インターフェイスを介して変更されたアプリの詳細はキャッシュに含まれません。

このハンドラーは、AEM App Shell ContentSync設定（page-type=[app-instance]）で使用する必要があります。

* ***type - String* - **widgetconfig
* ***path **-**String*** - アプリシェルの任意の子ノード（pge-type=[app-instance]）へのパス。
* ***targetRootDirectory - String*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String*** - アプリのアイコンを配置するディレクトリ

**mobileADBMobileConfigJSON** AMS cloudserviceが設定されている場合は、ADBMobileConfig.JSON ファイルを含めます。

これは、分析サポート用にAMS プラグインを設定する際にコンパイル時に使用されます。

ハンドラーは、AEM App Shell ContentSync Config （node with pge-type=app-instance）で使用する必要があります

* ***type - String*** - mobileADBMobileConfigJSON
* ***パス – 文字列*** - アプリシェルへのパス（pge-type=app-instanceのノード、または/libs/mobileapps/core/components/instanceを拡張するRT）
* ***targetRootDirectory - String*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス

**notificationsconfig** デバイスで必要な通知設定を抽出します。 プロパティは、アプリに関連付けられている各プッシュサービスクラウドサービス設定から抽出されます。

クラウドサービスのjcr:content ノード内のAEM以外のプロパティが抽出され、**pge-notifications-config.json** JSON ファイルに追加され、アプリコンテンツのwww ルートに含まれます。

AEMのプロパティは、「cq」、「sling」または「jcr」で名前空間が指定されたプロパティです。 その他のプロパティは、content-sync config ノードの「excludeProperties」プロパティを使用して除外できます。

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** – 除外するプロパティ

**contentsyncconfigcontent**&#x200B;既存のContentSync設定からコンテンツを収集します。

* ***type - String*** - contentsyncconfigcontent
* ***パス – 文字列*** – 次のいずれかにパスします：

  * 別のContentSync設定
  * コンテンツパッケージに移動します（phonegap-exportTemplate プロパティを使用してContentSync設定を検索します）
  * モバイルリソースに移動します（app-contentは、そのリソースの下に見つかります。これらのコンテンツパッケージにpge-includeInBuild プロパティがtrueの場合、phonegap-exportTemplateがContentSync設定を検索するために使用されます）

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - trueの場合、1回限りのインポートがまだ存在しない場合は、インポートの前にターゲット設定で最初の&#x200B;**update**&#x200B;を作成します

* ***autoFillBeforeImport - Boolean*** - trueの場合、インポートする前にターゲット設定を更新/入力します
* ***configSuffix - String*** - app-contentの「phonegap-exportTemplate」プロパティに示されているパスに追加する文字列。 これは、様々な書き出しテンプレートを区別するために使用できます。 例えば、このプロパティを&#x200B;**&quot;-dev&quot;**&#x200B;に設定して、*&quot;/.././../appconfig-dev&quot;*&#x200B;を使用する必要があることを示すことができます（*&quot;/../././appconfig&quot;*&#x200B;ではなく）。

**app-assets** アプリインスタンスに関連付けられたすべてのアセットが含まれます。 このハンドラーには、指定されたパスの下にあるアセットと、アプリインスタンスのappAssetPath プロパティによって参照されるアセットが含まれます。

* ***type - String*** - app-assets

* ***パス&#x200B;**-**文字列*** - アプリアセットが保存されているアプリインスタンスの下の場所へのパス

**mobileappoffers** Personalizationのユースケースに、ターゲットコンテンツをレンダリングするための新しいコンテンツ同期ハンドラーが導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者が作成した関連するターゲットオファーのレンダリング方法を認識します。 mobileappoffers ハンドラーは抽象ページ更新ハンドラーを拡張するため、多くのプロパティは類似しています。 mobileappoffers ハンドラーの詳細には、次のプロパティがあります。

mobileappsoffers ハンドラーは、mobileappspages ハンドラーを拡張し、次のプロパティを追加します。

* ***locationRoot - String*** - モバイルアプリケーションの場所を指定します
* ***includePageTypes - String*** - cq/personalization/components/teaserpageおよびcq/personalization/components/offerproxyをサポートするための既定値
* ***selector - String*** – は標準に設定する必要があります
* ***path - String***- キャンペーンのブランドへのパス

**mobileappconfig** mobileappconfig コンテンツ同期ハンドラーは、JSON データをMobileAppsConfig.jsonに挿入する方法を提供します。 プロバイダークラスを登録するには、開発者はMobileAppsInfoProvider クラスをプロバイダーのリストに追加します。 ハンドラーはMobileAppsInfoProvidersのリストを繰り返し処理し、プロバイダーが結果のjson ファイルにデータを注入できるようにします。 このハンドラーがサポートするプロパティのリストは次のとおりです。

* ***path **-**String*** - pge-type=app-instanceまたは/libs/mobileapps/core/components/instanceを拡張するRTを含むアプリインスタンスノードへのパス
* ***providers - String*** `[]` – 完全修飾されたMobileAppsInfoProvidersのリスト
* ***targetRootDirectory - String*** - MobileAppsConfig.json ファイルの書き込み先ディレクトリ。
* **fileName - String** - JSONを書き込むファイルのオプション名。デフォルトはMobileAppsConfig.jsonです

複数のmobileappconfig ハンドラーを、それぞれ異なるJSON ファイルに書き込む一意のプロバイダーのセットで設定することができます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**整合性を確認する手順** キャッシュをクリア

* キャッシュのクリア
* ハンドラーを実行します（キャッシュ更新）
* ハンドラーを再度実行します（キャッシュは更新されません）

**デバッグの手順**

* 設定を実行
* 設定をエクスポートするか、デバイスでレビューします
* レンダリングが失敗した場合は、*styles/assets/libs*&#x200B;がないか確認するか、*styles/assets/libs*&#x200B;への不正なパスを確認してください

**ログ** ContentSyncを有効にするパッケージ `com.day.cq.contentsync`のOSGI ロガー設定を使用したログのデバッグこれにより、実行したハンドラーと、キャッシュを更新し、キャッシュを更新したかどうかを追跡できます。

## その他のリソース {#additional-resources}

管理者と開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [Adobe PhoneGap EnterpriseとAEMのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile アプリ開発を開始するには、[こちら](/help/mobile/getting-started-aem-mobile.md)をクリックしてください。
