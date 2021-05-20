---
title: Adobe Experience Manager 6.5リリースの非推奨（廃止予定）および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 42%

---

# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

AEM機能の差し迫った削除または置き換えを伝達するために、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上の機能強化はおこなわれません。
1. 非推奨（廃止予定）の機能は、次のメジャーリリースで早く削除されます。 削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| Creative Cloud統合 | AEMからCreative Cloudへのフォルダー共有は、クリエイティブユーザーがCCアプリケーションでアセットを開き、新しいファイルをアップロードしたり、AEMに変更を保存したりできるように、AEMからアセットにアクセスする方法としてAEM 6.2で導入されました。 Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することを強くお勧めします。 | Asset LinkやAEMデスクトップCreative Cloudなど、新しいアプリケーション統合機能に切り替えることをお勧めします。 詳しくは、 AEMとCreative Cloud統合のベストプラクティスを参照してください。 |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、](/help/sites-administering/security-checklist.md)AEM セキュリティチェックリスト[を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |
| Assets | ユーザーが`/content/dam/collections`に対する十分な（読み取りと書き込みの）権限を持っていない場合、ユーザーはコレクションを作成できません。 | ユーザーのアクセス制御設定を保持し、適切な権限を確保します。 |
| Adobe Search&amp;Promote | Adobe Search&amp;Promoteとの統合は非推奨（廃止予定）となりました。 Search&amp;Promote 統合機能がさらに強化される予定はありません。Search&amp;Promote 統合は廃止中も引き続き完全にサポートされます。 |  |
| DTM タグマネージャー | DTM（Dynamic Tag Manager）との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用してください。。 |
| Adobe Target | AEM 6.5で、AEMが[!DNL Adobe I/O]ベースのAdobe Target Standard API(Rest API)を使用してAdobe Targetサービスに接続する機能が追加されたことで、Target Classic API(XML)の方法は廃止されました。 | [に統合を再設定し、新しいAPI](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)を使用します。 |
| Adobe Target | AEMでのAdobe Targetとの`mbox.js`ベースの統合の使用は非推奨（廃止予定）となりました。 | `at.js` 1.xを使用するように切り替えます。 |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEMとコマースエンジン間の統合を可能にするマイクロサービスのセットとして2018年に提供されました。Adobeが2018年半ばにMagentoを獲得した後、Adobeは2つの理由でアプローチを変えることを決めた。 Magentoには独自のコマースAPI（RESTおよびGraphQL）のセットがあり、2つのAPIセットを維持することはお勧めしません。 市場の動向からは、データをクエリするより効率的な方法であるため、お客様がGraphQLに移行していることが示されました。 2019年に、Adobeは、MagentoのGraphQL APIを情報源として使用する新しいコマース統合フレームワークをリリースしました。 Adobeは、CIF RESTにこれ以上投資する予定はありません。 お客様は、代替ソリューションを使用することを強くお勧めします。 | AEMとMagentoの統合の場合、[AEM CIFアーキタイプ](https://github.com/adobe/aem-cif-project-archetype)および[AEM CIFコアコンポーネント](https://github.com/adobe/aem-core-cif-components)に切り替えます。 「AEMとMagentoの統合[コマース統合フレームワークの使用](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)」を参照してください。 新しいアプローチとのサードパーティ(Magento以外)統合のサポートは、アドビのロードマップです。 |
| コンポーネント（AEM Sites） | Adobeは、`/libs/foundation/components`に格納されている基盤コンポーネントの大部分をさらに強化する予定はありません。 コンポーネントフォルダー内で`cq:deprecated`および`cq:deprecatedReason`プロパティを探します。 AEM 6.5には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様は、そのまま使用できます。 さらに、非推奨（廃止予定）の基盤コンポーネントも完全にサポートされています。 | Adobeは、今後のプロジェクトでコアコンポーネントを使用することをお勧めします。 既存のサイトはそのまま残すか、[AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools)を使用して、コアコンポーネントを使用するようにサイトをリファクタリングできます。 |
| コンポーネント（AEM Sites） | デザインインポーターコンポーネント`/libs/wcm/designimporter/components`は6.5以降、非推奨とマークされています。Adobeは、デザインインポーターの実装をさらに強化する予定はありません。 | Adobeは、今後のリリースでこのユースケースの代替実装を提供する予定です。 |
| 基盤 | Granite オフロードフレームワーク. Adobeは、CQ 5.6.1で導入されたオフロードフレームワークをさらに強化して、アセット処理を外部化する予定はありません。 | アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。 |
| 開発者向け | `Hobbes.js`」を選択します。Adobeは、`hobbes.js`ユーザーインターフェイステストフレームワークをさらに強化する予定はありません。 | Adobeでは、Seleniumの自動化を使用することをお勧めします。 |
| 開発者向け | jQuery UI クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、引き続きコードにjQuery UIを必要とするお客様に対して、コードをプロジェクトコードベースに追加することをお勧めします。 |
| 開発者向け | jQuery Animationクライアントライブラリ(`granite.jquery.animation`)。 配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリがさらに保守および更新される予定はありません。 | Adobeは、コードにjQueryアニメーションがまだ必要な場合に、プロジェクトコードベースにコードを追加することをお勧めします。 |
| 開発者向け | Handlebars クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Handlebars クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードを引き続きHandlebarsに追加する必要があるお客様に対して、そのコードをプロジェクトコードベースに追加することをお勧めします。 |
| 開発者向け | Lawnchair クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加するために引き続きLawnchairが必要なお客様にお勧めします。 |
| 開発者向け | `Granite.Sling.js`クライアントライブラリに埋め込みます。配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能がさらに強化される予定はありません。 | Adobeでは、ライブラリの機能に依存してコードをリファクタリングし、使用しなくすることをお勧めします。 |
| 開発者向け | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4までは、YUIは、Google Closure Compiler(GCC)に切り替えるオプションを使用してJavaScriptを縮小するデフォルトでした。 AEM 6.5 以降は、GCC がデフォルトになっています。 | Adobeでは、AEM 6.5にアップグレードしてGCCに切り替えることをお勧めします |
| 開発者向け | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代替手段はありません。 |
| フォーム | AEM FormsとAEM Mobileの統合は非推奨（廃止予定）となりました。 | 代替機能はありません。 |  | 開発者向け | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代替手段はありません。 |
| 開発者向け | Lodash/underscoreクライアントライブラリ。 Adobeは、配布版（クイックスタート）の一部として含まれるLodash/underscoreクライアントライブラリをさらに保守および更新する予定はありません | Adobeでは、コードに引き続きLodash/underscoreが必要な場合に、それをプロジェクトコードベースに追加することをお勧めします。 |

## 削除された機能 {#removed-features}

この節では、AEM 6.5から削除された機能について説明します。以前のリリースでは、これらの機能は非推奨とマークされていました。

| 領域 | 機能 | 代替手段 |
|--- |--- |--- |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。Adobe Analytics](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html)が提供する[ActivityMapプラグインを使用します。 |
| 統合 | ExactTargetの統合は、デフォルトの配布（クイックスタート）から削除され、使用できなくなりました。 | 代替機能はありません. |
| 統合 | Salesforce Force API統合は、デフォルトの配布版（クイックスタート）から削除され、[ソフトウェア配布版](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からインストールする追加パッケージになりました。 | この機能は引き続き使用できます。 |
| フォーム | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません. |
| フォーム | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |
| フォーム | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |
| フォーム | JEE上のLiveCycleES4 SP1からAEM 6.5 Formsへのシングルホップアップグレードは使用できません | AEM Formsのアップグレードに関するドキュメントの[利用可能なアップグレードパス](../forms/using/upgrade.md)を参照してください。 |
| フォーム | JEE上のAEM FormsからUPDベースのクラスタリングのサポートを削除 | JEE上のAEM Formsでは、TCPベースのクラスタリングのみを使用できます。 UDPマルチキャストサーバーを以前のバージョンからJEE上のAEM 5.5 Formsにアップグレードする場合は、手動設定を実行して、TCPベースのGemfireクラスタリングに切り替えます。 詳しい手順については、「[JEE上のAEM 6.5 formsへのアップグレード](../forms/using/upgrade-forms-jee.md)」を参照してください。 |
| 開発者向け | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| 開発者向け | HTMLクライアントライブラリマネージャーで`customJavaScriptPath`サポートを削除します。 | 代替機能はありません |
| [!DNL Assets] | [!DNL Adobe Experience Manager] 6.5では、アセットのオフロード機能が削除されました。 | 代替手段はありません。 |
| キャッシュ | `system/console/slingjsp` は、AEM 6.5では使用できなくなりました。 | クラスとSlightlyキャッシュは、Apache Sling Commons FileSystem ClassLoaderバンドルに格納されます。 バンドル番号をAEM Webコンソールで確認し、ファイルシステムから直接キャッシュフォルダーを削除できます(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |

## 次期リリースの発表前{#pre-announcement-for-next-release}

この節は、今後のリリースで変更予定を事前にお知らせする場合に使用します。 発表された変更は、まだ有効ではありませんが、お客様に影響を与えます。 例えば、これらの機能はまだ非推奨ではなく、非推奨となった後にユーザーに影響を与えます。 これらの更新は、計画のために提供されます。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| 基盤 | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/modernization-tools.md)詳細情報[）。 |
