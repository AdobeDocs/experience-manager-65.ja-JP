---
title: Adobe Experience Manager 6.5 リリースで廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 42%

---

# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

AEM機能の差し迫った削除または置き換えを伝達するために、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表が行われます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上の機能強化はおこなわれません。
1. 非推奨（廃止予定）の機能は、以下のメジャーリリースで最も早く削除されます。 削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 | バージョン (SP) |
|---|---|---|---|
| [!DNL Sites] | のエクスペリエンスフラグメントプロパティ **ソーシャルメディアのステータス**. |  | 6.5.11.0 |
| [!DNL Sites] | シンプルなコンテンツフラグメントを作成するためのコンテンツフラグメントテンプレート。 | 現在は[モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud統合 | AEMからCreative Cloudフォルダーへの共有は、クリエイティブユーザーがAEMのアセットにアクセスできるようにする方法としてAEM 6.2 で導入され、 [!DNL Creative Cloud] アプリケーションを起動し、新しいファイルをアップロードしたり、変更をAEMに保存したりします。 Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することを強くお勧めします。 | AdobeAsset Link やAEMデスクトップCreative Cloudなど、新しいアプリケーション統合機能に切り替えることをお勧めします。 |  |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、](/help/sites-administering/security-checklist.md)AEM セキュリティチェックリスト[を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |  |
| Assets | ユーザーが、に対する十分な（読み取りおよび書き込み）権限を持っていない場合 `/content/dam/collections`に値を指定しない場合、ユーザーはコレクションを作成できません。 | ユーザーのアクセス制御設定を保持し、適切な権限を確保します。 |  |
| Adobe Search&amp;Promote | Adobe Search&amp;Promoteとの統合は廃止されました。 Search&amp;Promote 統合機能がさらに強化される予定はありません。Search&amp;Promote 統合は廃止中も引き続き完全にサポートされます。 |  |  |
| DTM タグマネージャー | DTM（Dynamic Tag Manager）との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用してください。。 |  |
| Adobe Target | を使用してAEMがAdobe Targetサービスに接続する機能を追加すると、 [!DNL Adobe I/O] AEM 6.5 のAdobe Target Standard API(Rest API) をベースとしている場合、Target Classic API(XML) の方法は非推奨（廃止予定）となりました。 | 統合の再設定先： [新しい API の使用](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |  |
| Adobe Target | の使用 `mbox.js` AEMでのAdobe Targetとの統合は非推奨（廃止予定）となりました。 | 使用に切り替え `at.js` 1.x. |  |
| コマース | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEMとコマースエンジン間の統合を可能にするマイクロサービスのセットとして 2018 年に提供されています。 Adobeが 2018 年半ばにMagentoを獲得した後、Adobeは 2 つの理由でアプローチを変更することを決定しました。 Magentoには独自のコマース API（REST および GraphQL）のセットがあり、2 組の API を維持することはお勧めしません。 市場の動向から、お客様は GraphQL に移行していることが示されました。これは、データをクエリするより効率的な方法であるからです。 2019 年に、Adobeは、Magentoの GraphQL API を情報源として使用した新しい Commerce Integration Framework をリリースしました。 Adobeは、CIF REST にこれ以上投資する予定はありません。 お客様は、代替ソリューションを使用することを強くお勧めします。 | AEM-Magento統合の場合は、 [AEM CIF アーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components). AEMとAdobe Commerceの統合を参照 [コマース統合フレームワークの使用](/help/commerce/cif/integrating/magento.md). 新しいアプローチとのサードパーティ (Magento以外 ) 統合のサポートは、アドビのロードマップに記載されています。 |  |
| コンポーネント（AEM Sites） | Adobeでは、 `/libs/foundation/components`. を探します。 `cq:deprecated` および `cq:deprecatedReason` プロパティをコンポーネントフォルダーに追加します。 AEM 6.5 には基盤コンポーネントが含まれています。以前のリリースからアップグレードするお客様は、それらをそのまま使用できます。 また、基盤コンポーネントは、非推奨（廃止予定）の場合でも完全にサポートされます。 | Adobeは、将来のプロジェクトではコアコンポーネントを使用することをお勧めします。 既存のサイトは、そのまま残すか、 [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) を使用して、コアコンポーネントを使用するようにサイトをリファクタリングします。 |  |
| コンポーネント（AEM Sites） | デザインインポーターのコンポーネント `/libs/wcm/designimporter/components` は 6.5 以降、非推奨としてマークされています。Adobeは、デザインインポーターのその実装をさらに強化する予定はありません。 | Adobeは、今後のリリースでこのユースケースの代替実装を提供する予定です。 |  |
| 基盤 | Granite オフロードフレームワーク. Adobeは、CQ 5.6.1 で導入されたオフロードフレームワークをさらに強化して、アセット処理を外部化する予定はありません。 | アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。 |  |
| 開発者 | `Hobbes.js`」を選択します。Adobeは、 `hobbes.js` ユーザーインターフェイステストフレームワーク。 | Adobeでは、Selenium の自動化を使用することをお勧めします。 |  |
| 開発者 | jQuery UI クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードに jQuery UI を引き続き必要とするお客様が、コードをプロジェクトコードベースに追加することをお勧めします。 |  |
| 開発者 | jQuery Animation クライアントライブラリ (`granite.jquery.animation`) をクリックします。 配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードに jQuery アニメーションを引き続き必要とする場合に、そのコードをプロジェクトコードベースに追加することをお勧めします。 |  |
| 開発者 | Handlebars クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Handlebars クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加するために Handlebars を引き続き必要とするお客様にお勧めします。 |  |
| 開発者 | Lawnchair クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加するために Lawnchair がまだ必要なお客様にお勧めします。 |  |
| 開発者 | `Granite.Sling.js`クライアントライブラリに埋め込みます。配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能がさらに強化される予定はありません。 | Adobeでは、ライブラリの機能に依存してコードをリファクタリングし、使用しなくすることをお勧めします。 |  |
| 開発者 | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4 までは、YUI はGoogle Closure Compiler(GCC) に切り替えるオプションを使用して JavaScript を縮小するデフォルトでした。 AEM 6.5 以降は、GCC がデフォルトになっています。 | Adobeでは、実装のためにAEM 6.5 にアップグレードして GCC に切り替えることをお勧めします |  |
| 開発者 | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代替手段はありません。 |  |
| Forms | AEM FormsとAEM Mobileの統合は非推奨（廃止予定）となりました。 | 置換できるものはありません。 |  | 開発者 | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代替手段はありません。 |  |
| 開発者 | クライアントライブラリをダッシュ/アンダースコアで読み込みます。 Adobeは、配布版 (Quickstart) の一部として提供される Lodash/underscore クライアントライブラリをさらに保守および更新する予定はありません | Adobeでは、コードに Lodash/underscore を必要とする場合に、プロジェクトコードベースに追加することをお勧めします。 |  |

## 削除された機能 {#removed-features}

この節では、AEM 6.5 から削除された機能を示します。以前のリリースでは、これらの機能は非推奨とマークされていました。

| 領域 | 機能 | 代替手段 | バージョン (SP) |
|--- |--- |--- |--- |
| 他のソリューションとの統合： [!DNL Experience Cloud] | アセットを [!DNL Experience Cloud] 経由での設定の使用 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 以前は [!DNL Adobe Marketing Cloud]. | クエリがある場合は、 [連絡先Adobeカスタマーサポート](https://www.adobe.com/account/sign-in.supportportal.html). |  |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。以下を使用： [Adobe Analyticsが提供する ActivityMap プラグイン](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html). |  |
| 統合 | ExactTarget の統合は、デフォルトの配布（クイックスタート）から削除され、使用できなくなりました。 | 代替機能はありません. |  |
| 統合 | Salesforce Force API 統合は、デフォルトの配布版（クイックスタート）から削除され、今後は、追加のパッケージとしてからインストールされます。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | この機能は引き続き使用できます。 |
| Forms | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |  |
| Forms | LiveCycleES4 SP1 からAEM 6.5 Forms on JEE へのシングルホップアップグレードは使用できません | 詳しくは、 [使用可能なアップグレードパス](../forms/using/upgrade.md) (AEM Formsアップグレードドキュメント ) |  |
| Forms | JEE 上のAEM Formsから、UPD ベースのクラスタリングのサポートを削除しました。 | JEE 上のAEM Formsで使用できるのは、TCP ベースのクラスタリングのみです。 UDP マルチキャストサーバーを以前のバージョンから JEE 上のAEM 5.5 Formsにアップグレードする場合は、手動設定を実行して、TCP ベースの GemFire クラスタリングに切り替えます。 詳しい手順については、 [JEE 上のAEM 6.5 Forms へのアップグレード](../forms/using/upgrade-forms-jee.md) |  |
| 開発者 | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| 開発者 | 削除 `customJavaScriptPath` HTMLクライアントライブラリマネージャーでのサポート。 | 代替機能はありません |  |
| [!DNL Assets] | アセットのオフロード機能は、 [!DNL Adobe Experience Manager] 6.5. | 代替手段はありません。 |  |
| キャッシュ | `system/console/slingjsp` は、AEM 6.5 では使用できなくなりました。 | クラスと Slightly キャッシュは、Apache Sling Commons FileSystem ClassLoader バンドルに格納されます。 AEM Web コンソールでバンドル番号を確認し、ファイルシステムから直接キャッシュフォルダーを削除できます (`crx-quickstart/launchpad/felix/bundle<ID>`) をクリックします。 |  |

## 次回リリースの事前発表 {#pre-announcement-for-next-release}

この節では、今後のリリースで変更を事前にお知らせします。 発表された変更はまだ有効ではありませんが、お客様に影響を与えます。 例えば、これらの機能はまだ非推奨になっていませんが、廃止後のユーザーに影響を与えます。 これらの更新は、計画を立てるために提供されます。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| 基盤 | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/modernization-tools.md)詳細情報[）。 |
