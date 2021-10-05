---
title: Adobe Experience Manager 6.5 リリースの非推奨（廃止予定）および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 42%

---

# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

AEM機能の差し迫った削除または置き換えを伝達するには、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表が行われます。非推奨（廃止予定）の機能は引き続き使用できますが、それ以上強化されません。
1. 非推奨（廃止予定）の機能は、次のメジャーリリースで早く削除されます。 削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| [!DNL Sites] | テンプレートベースのシンプルなコンテンツフラグメント。 | [モデルベースの構造化コンテンツフラグメ](/help/assets/content-fragments/content-fragments-models.md) ントスノー。 |
| Creative Cloud統合 | AEMからCreative Cloudへのフォルダー共有は、クリエイティブユーザーがAEMのアセットにアクセスできるように、 AEM 6.2 で導入されました。これにより、 [!DNL Creative Cloud] アプリケーションでアセットを開いたり、新しいファイルをアップロードしたり、変更をAEMに保存したりできます。 Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することを強くお勧めします。 | AdobeAsset Link やAEMデスクトップアプリケーションなど、新しいCreative Cloud統合機能に切り替えることをお勧めします。 |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、](/help/sites-administering/security-checklist.md)AEM セキュリティチェックリスト[を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |
| Assets | ユーザーが `/content/dam/collections` に対する十分な（読み取りと書き込みの）権限を持っていない場合、ユーザーはコレクションを作成できません。 | ユーザーのアクセス制御設定を保持し、適切な権限を確保します。 |
| Adobe Search&amp;Promote | Adobe Search&amp;Promoteとの統合は非推奨（廃止予定）となりました。 Search&amp;Promote 統合機能がさらに強化される予定はありません。Search&amp;Promote 統合は廃止中も引き続き完全にサポートされます。 |  |
| DTM タグマネージャー | DTM（Dynamic Tag Manager）との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用してください。。 |
| Adobe Target | AEM 6.5 では、AEMが [!DNL Adobe I/O] ベースのAdobe Target Standard API(Rest API) を使用してAdobe Targetサービスに接続する機能が追加され、Target Classic API(XML) の方法は非推奨（廃止予定）となりました。 | 統合を [ 新しい API](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) を使用するように再設定します。 |
| Adobe Target | AEMでのAdobe Targetとの `mbox.js` ベースの統合の使用は非推奨（廃止予定）となりました。 | `at.js` 1.x を使用するように切り替えます。 |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEMとコマースエンジン間の統合を可能にする一連のマイクロサービスとして 2018 年に提供されました。Adobeが 2018 年半ばにMagentoを獲得した後、Adobeは 2 つの理由でアプローチを変えることにした。 Magentoには独自のコマース API（REST および GraphQL）のセットがあり、2 組の API を維持することはお勧めしません。 市場の動向から、データをより効率的にクエリする方法であるため、お客様は GraphQL に移行していることがわかります。 2019 年に、Adobeは、Magentoの GraphQL API を真実のソースとして使用した新しいコマース統合フレームワークをリリースしました。 Adobeは、CIF REST にこれ以上投資する予定はありません。 お客様は、代替ソリューションを使用することを強くお勧めします。 | AEM-Magento統合の場合、[AEM CIF アーキタイプ ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント ](https://github.com/adobe/aem-core-cif-components) に切り替えます。 「AEMとMagentoの統合 [ コマース統合フレームワークの使用 ](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)」を参照してください。 新しいアプローチとのサードパーティ (Magento以外 ) 統合のサポートは、アドビのロードマップに記載されています。 |
| コンポーネント（AEM Sites） | Adobeは、`/libs/foundation/components` に格納されている基盤コンポーネントのほとんどをさらに強化する予定はありません。 コンポーネントフォルダー内の `cq:deprecated` および `cq:deprecatedReason` プロパティを探します。 AEM 6.5 には基盤コンポーネントが含まれており、以前のリリースからアップグレードしたお客様は、引き続き基盤コンポーネントをそのまま使用できます。 また、基盤コンポーネントは非推奨ですが、完全にサポートされています。 | Adobeは、今後のプロジェクトではコアコンポーネントを使用することをお勧めします。 既存のサイトはそのまま残すか、[AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) を使用して、コアコンポーネントを使用するようにサイトをリファクタリングできます。 |
| コンポーネント（AEM Sites） | デザインインポーターコンポーネント `/libs/wcm/designimporter/components` は 6.5 以降、非推奨とマークされています。Adobeは、デザインインポーターのその実装をさらに強化する予定はありません。 | Adobeは、今後のリリースでこのユースケースの代替実装を提供する予定です。 |
| 基盤 | Granite オフロードフレームワーク. Adobeは、CQ 5.6.1 で導入されたオフロードフレームワークをさらに強化して、アセット処理を外部化する予定はありません。 | アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。 |
| デベロッパー向け | `Hobbes.js`」を選択します。Adobeは、`hobbes.js` ユーザーインターフェイステストフレームワークをさらに強化する予定はありません。 | Adobeでは、Selenium の自動化を使用することをお勧めします。 |
| デベロッパー向け | jQuery UI クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードに jQuery UI を引き続き必要とするお客様に対して、コードをプロジェクトコードベースに追加することをお勧めします。 |
| デベロッパー向け | jQuery Animation クライアントライブラリ (`granite.jquery.animation`)。 配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリがさらに保守および更新される予定はありません。 | Adobeは、コードに jQuery アニメーションを引き続き必要とするお客様に対し、それをプロジェクトコードベースに追加することをお勧めします。 |
| デベロッパー向け | Handlebars クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Handlebars クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードを引き続き Handlebars でプロジェクトコードベースに追加する必要があるお客様にお勧めします。 |
| デベロッパー向け | Lawnchair クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加するために Lawnchair がまだ必要なお客様にお勧めします。 |
| デベロッパー向け | `Granite.Sling.js`クライアントライブラリに埋め込みます。配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能がさらに強化される予定はありません。 | Adobeでは、ライブラリの機能に依存してコードをリファクタリングし、使用しなくすることをお勧めします。 |
| デベロッパー向け | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4 までは、YUI はGoogle Closure Compiler(GCC) に切り替えるオプションを使用して JavaScript を縮小するデフォルトでした。 AEM 6.5 以降は、GCC がデフォルトになっています。 | Adobeでは、AEM 6.5 にアップグレードして実装用に GCC に切り替えることをお勧めします |
| デベロッパー向け | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代わりの製品はありません。 |
| Forms | AEM FormsとAEM Mobileの統合は廃止されました。 | 交換できません。 |  | デベロッパー向け | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 代わりの製品はありません。 |
| デベロッパー向け | Lodash/Underscore クライアントライブラリ。 Adobeは、配布版（クイックスタート）の一部として含まれる Lodash/underscore クライアントライブラリをさらに保守および更新する予定はありません | Adobeでは、コードに引き続き Lodash/underscore が必要な場合に、そのコードをプロジェクトコードベースに追加することをお勧めします。 |

## 削除された機能 {#removed-features}

この節では、AEM 6.5 から削除された機能について説明します。以前のリリースでは、これらの機能は非推奨とマークされていました。

| 領域 | 機能 | 代替手段 |
|--- |--- |--- |
| [!DNL Experience Cloud] との統合 | [!DNL Adobe I/O] を介した設定を使用して、アセットを [!DNL Experience Cloud] と同期できます。 [!DNL Adobe Experience Cloud] は、以前はと呼ばれていま [!DNL Adobe Marketing Cloud]した。 | 質問がある場合は、[Adobeカスタマーケア ](https://www.adobe.com/account/sign-in.supportportal.html) にお問い合わせください。 |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。Adobe Analytics](https://docs.adobe.com/content/help/ja/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html) が提供する [ActivityMap プラグインを使用します。 |
| 統合 | ExactTarget の統合は、デフォルトの配布（クイックスタート）から削除され、使用できなくなりました。 | 代替機能はありません. |
| 統合 | Salesforce Force API 統合は、デフォルトの配布版（クイックスタート）から削除され、[ ソフトウェア配布版 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) からインストールする追加のパッケージになりました。 | この機能は引き続き使用できます。 |
| Forms | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |
| Forms | JEE 上のLiveCycleES4 SP1 からAEM 6.5 Formsへのシングルホップアップグレードは使用できません | AEM Formsのアップグレードドキュメントの [ 利用可能なアップグレードパス ](../forms/using/upgrade.md) を参照してください。 |
| Forms | JEE 上のAEM Formsから UPD ベースのクラスタリングのサポートを削除 | JEE 上のAEM Formsでは、TCP ベースのクラスタリングのみを使用できます。 UDP マルチキャストサーバーを以前のバージョンから JEE 上のAEM 5.5 Formsにアップグレードする場合は、TCP ベースの GemFire クラスタリングに切り替えるための手動設定を実行します。 詳しい手順については、「[JEE 上のAEM 6.5 forms へのアップグレード ](../forms/using/upgrade-forms-jee.md)」を参照してください。 |
| デベロッパー向け | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| デベロッパー向け | Client Library Manager で `customJavaScriptPath` サポートをHTMLします。 | 代替機能はありません |
| [!DNL Assets] | [!DNL Adobe Experience Manager] 6.5 では、アセットのオフロード機能が削除されました。 | 代わりの製品はありません。 |
| キャッシュ | `system/console/slingjsp` は、AEM 6.5 では使用できなくなりました。 | クラスと Slightly キャッシュは、Apache Sling Commons FileSystem ClassLoader バンドルに格納されます。 バンドル番号をAEM Web コンソールで確認し、ファイルシステムから直接キャッシュフォルダーを削除できます (`crx-quickstart/launchpad/felix/bundle<ID>`)。 |

## 次回リリースの事前発表 {#pre-announcement-for-next-release}

この節は、今後のリリースで予定されている変更を事前に発表する場合に使用します。 発表された変更はまだ有効ではありませんが、お客様に影響を与えます。 例えば、この機能はまだ廃止されていませんが、廃止後はユーザーに影響を与えます。 これらの更新は、計画のために提供されます。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| 基盤 | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/modernization-tools.md)詳細情報[）。 |
