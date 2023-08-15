---
title: 既製のアプリハンドラー
seo-title: Out of the Box App Handlers
description: このページでは、AEMを使用したAdobe PhoneGap Enterprise 向けの標準ハンドラーについて説明します。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 1%

---

# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

コンテンツ同期ハンドラーの開発については、次のガイドラインを参照してください。

* ハンドラーはを実装する必要があります *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接またはを実行するクラスの拡張）
* ハンドラーは拡張できます *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* ハンドラーは、ContentSync キャッシュを更新した場合にのみ true を報告する必要があります。 true と誤ってレポートされると、AEMで更新を作成できます。
* ハンドラーは、コンテンツが実際に変更された場合にのみキャッシュを更新する必要があります。 ホワイトが不要な場合はキャッシュに書き込まず、不要な更新の作成を避けます。

## 標準提供のハンドラー {#out-of-the-box-handlers}

次のリストの既製のアプリハンドラーを示します。

**mobileapppages** アプリのページをレンダリングします。

* ***type - String*** - mobileapppages
* ***path - String***  — ページへのパス
* ***extension - String***  — リクエストで使用する拡張子。 ページの場合、これはほとんど常にです。 *html*&#x200B;ですが、その他の方法はまだ可能です。

* ***selector - String***  — オプションのセレクター（ドット区切り）。 一般的な例は次のとおりです。 *タッチ* モバイルバージョンのページをレンダリングする場合。

* ***deep - Boolean***  — 子ページも含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true.*

* ***includeImages — ブール値***  — 画像を含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true*.

   * デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントのみが含めると見なされます。

* ***includeVideos - Boolean***  — ビデオを含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true*.

* ***includeModifiedPagesOnly — ブール値*** - false または省略した場合は、すべてのページをレンダリングし、レンダリングで更新を確認します。 true の場合、lastModified ページの変更に基づいて異なります。
* ***+ rewrite （ノード）***
  ***- relativeParentPath - String***  — 他のすべての相対パスを書き込むパス。

>[!NOTE]
>
>このハンドラーの影響を受ける画像およびビデオコンポーネントのリソースタイプは、 *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler OSGi サービス*.

**mobilepageassets** アプリページのアセットを収集します。

**mobilecontentlisting** ContentSync zip のコンテンツをリストします。 これは、デバイス上のクライアント側 js がAEMアプリに必要な最初のファイルコピーを実行するために使用します。

このハンドラーは、AEM Apps の ContentSync 設定に追加する必要があります。

* ***type - String - mobilecontentlisting***
* ***パス*** - String — 空のままにします。有効なハンドラーとして表示するには存在する必要がありますが、パスは現在の ContentSync キャッシュと推測されます。 この値は無視されます。
* ***targetRootDirectory* -**String — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***注文 — 長い* -**コンテンツ同期でこのハンドラーを実行する順序です。 この数は、100 など他のすべてのハンドラーよりも大きく設定する必要があります。 従来のコンテンツハンドラーの後に実行する必要があります。

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

**mobilecontentpackageslisting** 特定のアプリ内のAEMコンテンツパッケージと、更新リクエストをおこなう serverURL をリストします。 これは、デバイス上のクライアント側 js を使用して、コンテンツの更新をリクエストします

ハンドラーは、AEM App Shell ContentSync 設定（pge-type=app-instance のノード）で使用する必要があります

* ***type - String - mobilecontentpackageslisting***
* ***パス&#x200B;**-**文字列***  — アプリシェルのパス（pge-type=app-instance のノード）。
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***注文 — 長い* -**コンテンツ同期でこのハンドラーを実行する順序です。 この数は、100 など他のすべてのハンドラーよりも大きく設定する必要があります。 従来のコンテンツハンドラーの後に実行する必要があります。

>[!NOTE]
>
>次のコードブロックは正確な実装ではないので、参照例として使用してください。

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

**widgetconfig** コマンドセンターで行われた編集を提供された config.xml と結合する、更新された config.xml を含めます。 このハンドラーが含まれていない場合、管理インターフェイスを介して変更されたアプリの詳細はキャッシュに含まれません。

このハンドラーは、AEM App Shell ContentSync 設定（pge-type=のノード）で使用する必要があります[app-instance]) をクリックします。

* ***type - String* - **widgetconfig
* ***パス&#x200B;**-**文字列***  — 任意のアプリシェルの子ノード（pge-type=のノード）へのパス[app-instance]) をクリックします。
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String***  — アプリのアイコンを配置するディレクトリ。

**mobileADBMobileConfigJSON** AMS クラウドサービスが設定されている場合は、 ADBMobileConfig.JSON ファイルを含めます。

これは、解析サポート用に AMS プラグインを設定するためにコンパイル時に使用されます。

ハンドラーは、AEM App Shell ContentSync 設定（pge-type=app-instance のノード）で使用する必要があります

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String***  — アプリシェルへのパス（pge-type=app-instance のノードまたは/libs/mobileapps/core/components/instance を拡張する RT）
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。

**notificationsconfig** デバイスで必要な通知設定を抽出します。 プロパティは、アプリに関連付けられた各プッシュサービスクラウドサービス設定から抽出されます。

クラウドサービスの jcr:content ノード内のAEM以外のプロパティが抽出され、 **pge-notifications-config.json** アプリコンテンツの www ルートに含める JSON ファイル。

AEMプロパティは、「cq」、「sling」または「jcr」という名前空間が付けられたプロパティです。 content-sync config ノードの「excludeProperties」プロパティを使用して、他のプロパティを除外できます。

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]***  — 除外するプロパティ

**contentsyncconfigcontent** 既存のコンテンツ同期設定からコンテンツを収集します。

* ***type - String*** - contentsyncconfigcontent
* ***path - String***  — 次のいずれかへのパス：

   * 別のコンテンツ同期設定
   * をコンテンツパッケージに追加します（phonegap-exportTemplate プロパティを使用して ContentSync 設定を検索します）。
   * をモバイルリソースに追加します（app-content のはそのリソースの下に見つかります。これらのコンテンツパッケージに pge-includeInBuild プロパティが true の場合、phonegap-exportTemplate を使用して ContentSync 設定が見つかります）。

* ***autoCreateFirstUpdateBeforeImport — ブール値*** - true の場合、初期値を作成 **更新** が存在しない場合は、インポート前の target 設定で

* ***autoFillBeforeImport — ブール値*** - true の場合は、読み込む前にターゲット設定を更新または入力します
* ***configSuffix - String*** - app-content の「phonegap-exportTemplate」プロパティで示されるパスに追加する文字列。 これは、異なる書き出しテンプレートを区別するために使用できます。 例えば、このプロパティを **&quot;-dev&quot;** 示す *&quot;/../../../appconfig-dev&quot;* 使用する必要がある ( *&quot;/../../../appconfig&quot;*) をクリックします。

**app-assets** アプリインスタンスに関連付けられているすべてのアセットが含まれます。 このハンドラーには、指定されたパスの下に見つかったアセットと、アプリインスタンスの appAssetPath プロパティで参照されているアセットが含まれます。

* ***type - String*** - app-assets

* ***パス&#x200B;**-**文字列***  — アプリアセットが保存されるアプリインスタンス下の場所へのパス

**mobileappoffers** ターゲットコンテンツをレンダリングするための、パーソナライゼーションの使用例に新しいコンテンツ同期ハンドラーが導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者が作成した関連するターゲットオファーをレンダリングする方法を認識しています。 mobileappoffers ハンドラーは抽象ページ更新ハンドラーを拡張したので、多くのプロパティは類似しています。 mobileappoffers ハンドラーの詳細には、次のプロパティがあります。

mobileappsoffers ハンドラーは mobileappspages ハンドラーを拡張し、次のプロパティを追加します。

* ***locationRoot - String***  — モバイルアプリケーションの場所を指定します
* ***includePageTypes - String***  — デフォルトで cq/personalization/components/teaserpage および cq/personalization/components/offerproxy をサポートします。
* ***selector - String*** - tandt に設定する必要があります。
* ***path - String*** — キャンペーンのブランドへのパス

**mobileappconfig** mobileappconfig コンテンツ同期ハンドラーを使用すると、MobileAppsConfig.json に JSON データを挿入できます。 プロバイダークラスを登録するには、開発者の MobileAppsInfoProvider クラスをプロバイダーのリストに追加します。 ハンドラーは、MobileAppsInfoProviders のリストを反復し、プロバイダーが結果の JSON ファイルにデータを挿入できるようにします。 このハンドラーがサポートするプロパティのリストは次のとおりです。

* ***パス&#x200B;**-**文字列*** - pge-type=app-instance を持つアプリインスタンスノードへのパス、または/libs/mobileapps/core/components/instance を拡張する RT へのパス
* ***providers - String*** `[]`  — 完全修飾された MobileAppsInfoProviders のリスト
* ***targetRootDirectory - String*** - MobileAppsConfig.json ファイルの書き込み先ディレクトリ。
* **fileName - String** - JSON の書き込み先のファイル名（オプション）。デフォルトは MobileAppsConfig.json です。

複数の mobileappconfig ハンドラーを設定し、それぞれに一意のプロバイダーセットを設定して、異なる JSON ファイルに書き込むことができます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**整合性チェックの手順** キャッシュをクリア

* キャッシュのクリア
* ハンドラーを実行（キャッシュを更新）
* ハンドラーを再度実行します（キャッシュは更新しないでください）

**デバッグの手順**

* 設定を実行
* 設定を書き出すか、デバイスでレビューします
* レンダリングが失敗した場合は、見つからないかを確認します。 *styles/assets/libs* または、 *styles/assets/libs*

**ログ** パッケージの OSGI ロガー設定を使用した ContentSync デバッグログの有効化 `com.day.cq.contentsync` これにより、実行されたハンドラーを追跡し、ハンドラーがキャッシュを更新し、キャッシュの更新をレポートしたかどうかを追跡できます。

## その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobileアプリの開発を開始するには、 [ここ](/help/mobile/getting-started-aem-mobile.md).
