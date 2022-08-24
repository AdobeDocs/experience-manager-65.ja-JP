---
title: 既製のアプリハンドラー
seo-title: Out of the Box App Handlers
description: このページでは、AEM の Adobe PhoneGap Enterprise で使用できる既製のハンドラーについて説明します。
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 31%

---

# 既製のアプリハンドラー{#out-of-the-box-app-handlers}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

コンテンツ同期ハンドラーの開発については、以下のガイドラインを参照してください。

* ハンドラーはを実装する必要があります *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接またはを実行するクラスの拡張）
* ハンドラーは、*com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler* を拡張できます。
* ハンドラーは、ContentSync キャッシュを更新した場合にのみ true を報告する必要があります。 誤って true を返すと、AEM で更新が作成されます。
* ハンドラーは、コンテンツが実際に変更された場合にのみ、キャッシュを更新する必要があります。ホワイトが不要な場合はキャッシュに書き込まず、不要な更新の作成を避けます。

## 既製のハンドラー {#out-of-the-box-handlers}

以下に、既製のアプリハンドラーのリストを示します。

**mobileapppages** アプリのページをレンダリングします。

* ***type - String*** - mobileapppages
* ***path - String***  — ページへのパス
* ***extension - String***  — リクエストで使用する拡張子。 ページの場合、これはほとんど常にです *html*&#x200B;ですが、他の方法もまだ可能です。

* ***selector - String***  — オプションのセレクター（ドット区切り）。 一般的な例は次のとおりです。 *タッチ* モバイルバージョンのページをレンダリングする場合。

* ***deep - Boolean***  — 子ページも含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true* です。

* ***includeImages — ブール値***  — 画像を含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true* です。

   * デフォルトでは、リソースタイプが foundation/components/image の画像コンポーネントだけが追加の対象になります。

* ***includeVideos - Boolean***  — ビデオを含める必要があるかどうかを指定する、オプションのブール型プロパティ。 デフォルト値は *true* です。

* ***includeModifiedPagesOnly — ブール値*** - false または省略した場合は、すべてのページをレンダリングし、レンダリングで更新を確認します。 true の場合、最後に変更されたページに対する変更に基づいて差異を処理します。
* ***+ rewrite （ノード）***
   ***- relativeParentPath - String***  — 他のすべての相対パスを書き込むパス。

>[!NOTE]
>
>このハンドラーの影響を受ける画像およびビデオコンポーネントのリソースタイプは、 *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*MobilePagesUpdateHandler* OSGi サービスのプロパティによって設定します。

**mobilepageassets** アプリページのアセットを収集します。

**mobilecontentlisting** ContentSync zip のコンテンツをリストします。 これは、デバイスのクライアント側 js によって使用され、AEM アプリで必要な最初のファイルコピーを実行します。

このハンドラーは、すべての AEM アプリコンテンツ同期設定に追加する必要があります。

* ***type - String - mobilecontentlisting***
* ***パス*** - String — 空のままにします。有効なハンドラーとして表示するには存在する必要がありますが、パスは現在の ContentSync キャッシュと推測されます。 この値は無視されます。
* ***targetRootDirectory* -**String — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***注文 — 長* -**コンテンツ同期でこのハンドラーを実行する順序です。 この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

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
* ***注文 — 長* -**コンテンツ同期でこのハンドラーを実行する順序です。 この番号は、他のすべてのハンドラーよりも大きい値に設定する必要があります（100 など）。従来のコンテンツハンドラーの後に実行する必要があります。

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

**widgetconfig** コマンドセンターで行われた編集を提供された config.xml と結合する、更新された config.xml を含めます。 このハンドラーがアプリに含まれていない場合、管理インターフェイスで変更された詳細はキャッシュに含まれません。

このハンドラーは、AEM App Shell ContentSync 設定（pge-type=のノード）で使用する必要があります[app-instance]) をクリックします。

* ***type - String* - **widgetconfig
* ***パス&#x200B;**-**文字列***  — アプリシェルの子ノード（pge-type=のノード）へのパス[app-instance]) をクリックします。
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。
* ***targetIconDirectory - String***  — アプリのアイコンを配置するディレクトリ。

**mobileADBMobileConfigJSON** AMS クラウドサービスが設定されている場合は、 ADBMobileConfig.JSON ファイルを含めます。

これは、解析をサポートするための AMS プラグインを設定するためにコンパイル時に使用されます。

ハンドラーは、AEM App Shell ContentSync 設定（pge-type=app-instance のノード）で使用する必要があります

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String***  — アプリシェルへのパス（pge-type=app-instance のノードまたは/libs/mobileapps/core/components/instance を拡張する RT）
* ***targetRootDirectory - String***  — このハンドラーのコンテンツ更新のターゲットルートとしてパスに追加するプレフィックス。

**notificationsconfig** デバイスで必要な通知設定を抽出します。 プロパティは、アプリに関連付けられた各プッシュサービスクラウドサービス設定から抽出されます。

クラウドサービスの jcr:content ノード内の非AEMプロパティが抽出され、 **pge-notifications-config.json** アプリコンテンツの www ルートに含める JSON ファイル。

AEM プロパティは、「cq」、「sling」または「jcr」のネームスペースが付いたプロパティです。他のプロパティは、コンテンツ同期設定ノードの「excludeProperties」プロパティを使用して除外できます。

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
* ***configSuffix - String*** - app-content の「phonegap-exportTemplate」プロパティで示されるパスに追加する文字列。 これは、異なる書き出しテンプレートを区別するために使用できます。 例えば、このプロパティを **&quot;-dev&quot;** 示す *&quot;/../../../appconfig-dev&quot;* を ( *&quot;/../../../appconfig&quot;*) をクリックします。

**app-assets** アプリインスタンスに関連付けられているすべてのアセットが含まれます。 このハンドラーには、指定されたパスの下に見つかったアセットと、アプリインスタンスの appAssetPath プロパティで参照されているアセットが含まれます。

* ***type - String*** - app-assets

* ***パス&#x200B;**-**文字列***  — アプリアセットが保存されるアプリインスタンス下の場所へのパス

**mobileappoffers** ターゲットコンテンツをレンダリングするための、パーソナライゼーションの使用例に新しいコンテンツ同期ハンドラーが導入されました。 「mobileappoffers」ハンドラーは、コンテンツ作成者が作成した関連するターゲットオファーをレンダリングする方法を認識しています。 mobileappoffers ハンドラーは抽象ページ更新ハンドラーを拡張したので、多くのプロパティは類似しています。 mobileappoffers ハンドラーの詳細には、次のプロパティがあります。

mobileappsoffers ハンドラーは mobileappspages ハンドラーを拡張し、以下のプロパティが追加されます。

* ***locationRoot - String***  — モバイルアプリケーションの場所を指定します
* ***includePageTypes - String***  — デフォルトで cq/personalization/components/teaserpage および cq/personalization/components/offerproxy をサポートします。
* ***selector - String*** - tandt に設定する必要があります。
* ***path - String*** — キャンペーンのブランドへのパス

**mobileappconfig** mobileappconfig コンテンツ同期ハンドラーを使用すると、MobileAppsConfig.json に JSON データを挿入できます。 プロバイダークラスを登録するには、開発者の MobileAppsInfoProvider クラスをプロバイダーのリストに追加します。 ハンドラーは、MobileAppsInfoProviders のリストを反復し、プロバイダーが結果の JSON ファイルにデータを挿入できるようにします。 このハンドラーがサポートするプロパティのリストは以下のとおりです。

* ***パス&#x200B;**-**文字列*** - pge-type=app-instance を持つアプリインスタンスノードへのパス、または/libs/mobileapps/core/components/instance を拡張する RT へのパス
* ***providers - String*** `[]`  — 完全修飾された MobileAppsInfoProviders のリスト
* ***targetRootDirectory - String*** - MobileAppsConfig.json ファイルの書き込み先ディレクトリ。
* **fileName - String** - JSON の書き込み先のファイル名（オプション）。デフォルトは MobileAppsConfig.json です。

それぞれが異なる JSON ファイルに書き出す固有のプロバイダーセットを持つ、複数の mobileappconfig ハンドラーを設定することもできます。

### コンテンツ同期ハンドラーのテスト {#testing-content-sync-handlers}

**整合性チェックの手順** キャッシュをクリア

* キャッシュのクリア
* ハンドラーを実行（キャッシュが更新されます）
* ハンドラーを再実行（キャッシュは更新されません）

**デバッグの手順**

* 設定を実行
* 設定を書き出すか、デバイス上で確認
* レンダリングに失敗した場合は、*styles/assets/libs* があるかどうか、または *styles/assets/libs* へのパスが正しいかを確認

**ログ** パッケージの OSGI ロガー設定を使用した ContentSync デバッグログの有効化 `com.day.cq.contentsync` これにより、実行されたハンドラーを追跡し、ハンドラーがキャッシュを更新し、キャッシュの更新をレポートしたかどうかを追跡できます。

## その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM での Adobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>AEM Mobile アプリの開発の概要については、[こちら](/help/mobile/getting-started-aem-mobile.md)を参照してください。
