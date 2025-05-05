---
title: 既製のアプリハンドラー
description: ここでは、AEMを使用したAdobe PhoneGap Enterprise の標準提供ハンドラーについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 1%

---

# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

コンテンツ同期ハンドラーの開発については、次のガイドラインを参照してください。

* ハンドラーは、*com.day.cq.contentsync.handler.ContentUpdateHandler* （直接または実行するクラスの拡張）を実装する必要があります
* ハンドラーは、*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler* を拡張できます
* ハンドラーは、ContentSync キャッシュが更新された場合にのみ true をレポートする必要があります。 誤って true とレポートすると、AEMは更新を作成できます。
* ハンドラーは、コンテンツが実際に変更された場合にのみ、キャッシュを更新する必要があります。 白が不要な場合はキャッシュに書き込まず、不要な更新の作成を避けてください。

## 標準のハンドラー {#out-of-the-box-handlers}

以下に、すぐに使用できるアプリハンドラーの一覧を示します。

**mobileapppages** アプリのページをレンダリングします。

* ***type – 文字列*** - mobileapppages
* ***path – 文字列*** - ページへのパス
* ***extension – 文字列*** - リクエストで使用する必要がある拡張機能。 ページの場合は、ほとんどの場合 *html* ですが、それ以外の場合も可能です。

* ***selector – 文字列*** - ドットで区切られたオプションのセレクター。 一般的な例としては、ページのモバイルバージョンをレンダリングする *タッチ* があります。

* ***deep - Boolean*** – 子ページを含めるかどうかを決定するオプションのブール値プロパティ。 デフォルト値は *true* です。

* ***includeImages - Boolean*** – 画像を含めるかどうかを決定するオプションのブール値プロパティ。 デフォルト値は *true* です。

   * デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントのみが組み込み対象と見なされます。

* ***includeVideos - Boolean*** - オプションの boolean プロパティは、ビデオを含めるかどうかを決定します。 デフォルト値は *true* です。

* ***includeModifiedPagesOnly - ブール値*** - false または省略された場合、すべてのページがレンダリングされ、レンダリングで更新が確認されます。 true の場合、ページ lastModified に対する変更に基づいて異なります。
* ***+書き換え（ノード）***
  ***- relativeParentPath – 文字列*** – 他のすべてのパスを書き込む相対パス。

>[!NOTE]
>
>このハンドラーによって影響を受ける画像およびビデオコンポーネントのリソースタイプは、*com.adobe.cq.mobile.platform.impl.contentsync.handler* のプロパティを設定することで設定されます。*MobilePagesUpdateHandler OSGi サービス*。

**mobilepageassets** アプリのページアセットを収集します。

**mobilecontentlisting** ContentSync zip のコンテンツを一覧表示します。 これは、AEM アプリに必要な初期ファイルコピーを行うために、デバイス上のクライアントサイド js で使用されます。

このハンドラーはすべてのAEM アプリのコンテンツ同期設定に追加する必要があります。

* ***type – 文字列 – mobilecontentlisting***
* ***path*** – 文字列 – 空のままにします。有効なハンドラーとして見なされるには存在する必要がありますが、パスは現在の ContentSync キャッシュと推論されます。 この値は無視されます。
* ***targetRootDirectory*-**&#x200B;文字列 – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long* -**&#x200B;ContentSync がこのハンドラーを実行する順序。 この数は、100 などのその他すべてのハンドラーよりも高く設定する必要があります。 従来のコンテンツハンドラーの後に実行する必要があります。

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

**mobilecontentpackageslisting** 特定のアプリ内のAEM コンテンツパッケージと、更新リクエストを行う serverURL を一覧表示します。 コンテンツの更新をリクエストするために、デバイス上のクライアントサイド js に使用されます

ハンドラーは、AEM アプリシェルのコンテンツ同期設定（page-type=app-instance のノード）で使用する必要があります

* ***type – 文字列 – mobilecontentpackageslisting***
* ***path &#x200B;**-**String*** - アプリシェルへのパス（pge-type=app-instance を持つノード）。
* ***targetRootDirectory – 文字列*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***order - Long* -**&#x200B;ContentSync がこのハンドラーを実行する順序。 この数は、100 などのその他すべてのハンドラーよりも高く設定する必要があります。 従来のコンテンツハンドラーの後に実行する必要があります。

>[!NOTE]
>
>次のコードブロックは正確な実装ではないので、参考にして使用してください。

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

**widgetconfig** コマンドセンターで行われた編集を指定された config.xml に結合する、更新された config.xml が含まれています。 このハンドラーが含まれていない場合、管理インターフェイスを介して変更されるアプリの詳細はキャッシュに含まれません。

このハンドラーは、AEM アプリシェルの ContentSync 設定（pge-type=[app-instance] のノード）で使用する必要があります。

* ***type – 文字列* - &#x200B;** widgetconfig
* ***path &#x200B;**-**String*** - アプリシェルの子ノードのパス（pge-type=[app-instance] を持つノード）。
* ***targetRootDirectory – 文字列*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String*** - アプリのアイコンを配置するディレクトリ

**mobileADBMobileConfigJSON** AMS クラウドサービスが設定されている場合は、ADBMobileConfig.JSON ファイルを含めます。

これは、分析サポート用の AMS プラグインを設定する際にコンパイル時に使用されます。

ハンドラーは、AEM アプリシェルのコンテンツ同期設定（page-type=app-instance のノード）で使用する必要があります

* ***type – 文字列*** - mobileADBMobileConfigJSON
* ***path – 文字列*** - アプリシェル（pge-type=app-instance または/libs/mobileapps/core/components/instance を拡張する RT を持つノード）へのパス
* ***targetRootDirectory – 文字列*** – このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス

**notificationsconfig** デバイスで必要な通知設定を抽出します。 プロパティは、アプリに関連付けられたそれぞれのプッシュサービスクラウドサービス設定から抽出されます。

Cloud Service の jcr:content ノード内のAEM以外のプロパティが抽出され、**pge-notifications-config.json** JSON ファイルに追加されて、アプリコンテンツの www ルートに含められます。

AEMのプロパティは、「cq」、「sling」または「jcr」で名前がスペースで区切られたプロパティです。 その他のプロパティは、content-sync config ノードの「excludeProperties」プロパティを使用して除外できます。

* ***type – 文字列*** - notificationsconfig
* ***excludeProperties – 文字列[]*** – 除外するプロパティ

**contentsyncconfigcontent** 既存の ContentSync 設定からコンテンツを収集します。

* ***type - String*** - contentsyncconfigcontent
* ***path – 文字列*** – 次のいずれかのパスです。

   * 別の ContentSync 設定
   * コンテンツパッケージに追加します（ContentSync 設定を検索するには、phonegap-exportTemplate プロパティを使用します）。
   * モバイル リソースに対する応答（app-content はそのリソースの下にあり、これらのコンテンツパッケージに pge-includeInBuild プロパティが true の場合は、phonegap-exportTemplate を使用して ContentSync 設定が検索されます）

* ***autoCreateFirstUpdateBeforeImport - ブール値*** - true の場合、一度インポートする前に、ターゲット設定で最初の **update** を作成します（一度インポートできない場合）

* ***autoFillBeforeImport - ブール値*** - true の場合、読み込む前にターゲット設定を更新/入力します
* ***configSuffix – 文字列*** - app-content の「phonegap-exportTemplate」プロパティに示されているパスに追加する文字列。 これは、様々なエクスポートテンプレートを区別するために使用できます。 例えば、このプロパティを **&quot;-dev&quot;** に設定すると、（*&quot;/../.../../appconfig&quot;* を使用する必要があることを示すことができます（*&quot;/../.../appconfig&quot;* とは異なります）。

**アプリアセット** アプリインスタンスに関連付けられているすべてのアセットが含まれます。 このハンドラーには、指定されたパスで見つかったアセットと、アプリインスタンスの appAssetPath プロパティが参照するアセットが含まれます。

* ***type – 文字列*** - app-assets

* ***path &#x200B;**-**String*** - アプリアセットが保存されているアプリインスタンスの下の場所へのパス

**mobileappoffers** ターゲットコンテンツをレンダリングするための新しいコンテンツ同期ハンドラーがPersonalizationのユースケースに導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者によって作成された、関連するターゲットオファーのレンダリング方法を認識しています。 mobileappoffers ハンドラーは抽象ページ更新ハンドラーを拡張するので、プロパティの多くは似ています。 mobileappoffers ハンドラーの詳細には、以下のプロパティがあります。

mobileappsoffers ハンドラーは mobileappspages ハンドラーを実行し、次のプロパティを追加します。

* ***locationRoot – 文字列*** - モバイルアプリケーションの場所を指定します
* ***includePageTypes – 文字列*** - デフォルトでは、cq/personalization/components/teaserpage と cq/personalization/components/offerproxy がサポートされます。
* ***selector - String*** - tandt に設定する必要があります
* ***path - String***- キャンペーンのブランドへのパス

**mobileappconfig** mobileappconfig コンテンツ同期ハンドラーは、MobileAppsConfig.json に JSON データを挿入する方法を提供します。 プロバイダークラスを登録するには、開発者はプロバイダーのリストで MobileAppsInfoProvider クラスを追加します。 このハンドラーは、MobileAppsInfoProviders のリストを繰り返し処理し、結果の json ファイルにプロバイダーがデータを挿入できるようにします。 このハンドラーがサポートするプロパティのリストを以下に示します。

* ***path &#x200B;**-**String*** - pge-type=app-instance または/libs/mobileapps/core/components/instance を拡張する RT を持つアプリインスタンスノードへのパス
* ***providers – 文字列*** `[]` – 完全修飾 MobileAppsInfoProviders のリスト
* ***targetRootDirectory – 文字列*** - MobileAppsConfig.json ファイルを書き込むディレクトリ。
* **fileName – 文字列** - JSON を書き込むファイルのオプション名。デフォルトは MobileAppsConfig.json です。

複数の mobileappconfig ハンドラーを、異なる JSON ファイルに書き込む一意のプロバイダーセットで設定することができます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**整合性チェックの手順** キャッシュのクリア

* キャッシュのクリア
* ハンドラーを実行します（キャッシュが更新されます）
* ハンドラーを再度実行します（キャッシュは更新しないでください）

**デバッグ手順**

* 設定を実行します
* 設定をエクスポートするか、デバイスでレビュー
* レンダリングが失敗した場合は、見つからない *styles/assets/libs* を確認するか、*styles/assets/libs* への不正なパスを確認します。

**ログ** パッケージ `com.day.cq.contentsync` で OSGI ロガー設定を使用した ContentSync のデバッグログを有効にします。これにより、実行されたハンドラーと、それらがキャッシュを更新したかどうか、およびキャッシュを更新して報告したかどうかを追跡できます。

## その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile アプリの開発を開始するには、[ ここ ](/help/mobile/getting-started-aem-mobile.md) をクリックします。
