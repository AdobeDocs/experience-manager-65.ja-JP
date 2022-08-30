---
title: Adobe Experience Manager 6.5 リリースで廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 96%

---

# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に下位互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

近い将来行われる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. 廃止の発表がまず行われます。廃止中は、機能はまだ使用可能ですが、それ以上の機能強化は行われません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースで行われます。削除の実際の目標期日を通知します。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 廃止される機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|---|---|---|---|
| [!DNL Sites] | **ソーシャルメディアのステータス**&#x200B;のエクスペリエンスフラグメントのプロパティ。 |  | 6.5.11.0 |
| [!DNL Sites] | シンプルなコンテンツフラグメントを作成するためのコンテンツフラグメントテンプレート。 | 現在の[モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud 統合 | AEM／Creative Cloud フォルダー共有は、クリエイティブユーザーが AEM のアセットにアクセスできるようにする手段として AEM 6.2 に導入されました。その結果、ユーザーはアセットを [!DNL Creative Cloud] アプリケーションで開いたり、AEM に新しいファイルをアップロードまたは変更を保存したりできるようになりました。Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能はAEMに含まれていますが、代替ソリューションを使用することをお勧めします。 | Adobe Asset Link や AEM Desktop App などの新しい Creative Cloud 統合機能に切り替えることをお勧めします。 |  |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |  |
| Assets | ユーザーが `/content/dam/collections` に十分な（読み取りと書き込みの）権限を持っていない場合、ユーザーはコレクションを作成できません。 | ユーザーのアクセス制御設定を保持し、適切な権限を確保します。 |  |
| Adobe Search &amp; Promote | Adobe Search &amp; Promote との統合は廃止されました。Search&amp;Promote 統合機能がさらに強化される予定はありません。Adobe Search&amp;Promoteの統合は、廃止中も引き続き完全にサポートされます。 |  |  |
| DTM タグマネージャー | DTM（Dynamic Tag Manager）との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用してください。。 |  |
| Adobe Target | AEM 6.5 では、[!DNL Adobe I/O] ベースの Adobe Target Standard API（Rest API）を使用して AEM が Adobe Target サービスに接続できるようになり、Target Classic API（XML）方式は廃止されました。 | [新しい API を使用](/help/sites-administering/target.md)するように統合機能を再設定してください。 |  |
| Adobe Target | `mbox.js` を使用した AEM と Adobe Target の統合は廃止されました。 | `at.js` 1.x の使用に切り替えてください。 |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEM とコマースエンジン間の統合を可能にするマイクロサービスのセットとして 2018年に提供されています。アドビでは、2018年半ばに Magento を買収した後、2 つの理由でアプローチを変更することを決定しました。Magento には独自の Commerce API（REST および GraphQL）のセットがあり、2 組の API を維持することはお勧めしません。市場の動向から、お客様はデータをクエリするよりも効率的な GraphQL へと移行しつつあることがわかっています。2019年、アドビは、Magento の GraphQL API を情報源として使用した新しい Commerce 統合フレームワークをリリースしました。アドビでは今後、CIF REST に投資する予定はありません。お客様は、代替ソリューションを使用することをお勧めします。 | AEM と Magento 統合の場合は、 [AEM CIF アーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)に切り替えます。[コマース統合フレームワークを使用](/help/commerce/cif/integrating/magento.md)した、AEM と Adobe Commerce の統合を参照してください。新しいアプローチとのサードパーティ（Magento 以外）統合のサポートは、アドビのロードマップに記載されています。 |  |
| コンポーネント（AEM Sites） | アドビでは、`/libs/foundation/components` に格納されている基盤コンポーネントのほとんどについて、今後機能強化する予定はありません。コンポーネントフォルダーの `cq:deprecated` および `cq:deprecatedReason` プロパティを参照してください。AEM 6.5 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。また、基盤コンポーネントは非推奨（廃止予定）の場合でもサポートされます。 | アドビは、将来のプロジェクトではコアコンポーネントを使用することをお勧めします。既存のサイトは現状のままでもかまいませんし、コアコンポーネントを使用するように [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) でサイトをリファクタリングすることもできます。 |  |
| コンポーネント（AEM Sites） | デザインインポーターコンポーネント `/libs/wcm/designimporter/components` は、6.5 以降、廃止となりました。アドビでは、このデザインインポーター実装を今後機能強化する予定はありません。 | 今後のリリースで使用事例の代替実装を提供する予定です。 |  |
| 基盤 | Granite オフロードフレームワーク。アドビでは、アセット処理を外部化するために CQ 5.6.1 に導入されたオフロードフレームワークの機能を今後強化する予定はありません。 | アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。 |  |
| デベロッパー向け | `Hobbes.js`。アドビでは、今後 `hobbes.js` ユーザーインタフェイステストフレームワークの機能を強化する予定はありません。 | アドビでは、Selenium の自動化を使用することをお勧めします。 |  |
| デベロッパー向け | jQuery UI クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリの保守や更新を行う予定はありません。 | コードに jQuery UI が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | jQuery アニメーションクライアントライブラリ（`granite.jquery.animation`）。アドビでは今後、配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリの保守や更新を行う予定はありません。 | コードに jQuery アニメーションが引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | Handlebars クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Handlebar クライアントライブラリの保守や更新を行う予定はありません。 | コードに Handlebars が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | Lawnchair クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリの保守や更新を行う予定はありません。 | コードに Lawnchair が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | `Granite.Sling.js` クライアントライブラリ。アドビでは、配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能を今後強化する予定はありません。 | このライブラリの機能に頼っている場合は、それを使用しないようにコードをリファクタリングすることをお勧めします。 |  |
| デベロッパー向け | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4 までは、JavaScript を軽量化するデフォルトの手段は YUI で、Google Closure Compiler（GCC）に切り替えるオプションもありました。AEM 6.5 以降は、GCC がデフォルトになっています。 | AEM 6.5 にアップグレードする場合は、GCC に切り替えることをお勧めします。 |  |
| デベロッパー向け | クラシック UI ダイアログエディタのCRXDE Lite。 アドビでは、配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能を今後強化する予定はありません。 | 代替手段はありません。 |  |
| Forms | AEM Forms と AEM Mobile の統合は非推奨（廃止予定）となりました。 | 代替手段はありません。 |  | デベロッパー向け | クラシック UI ダイアログエディタのCRXDE Lite。 アドビでは、配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能を今後強化する予定はありません。 | 代替機能はありません。 |  |
| デベロッパー向け | Lodash／underscore クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Lodash/underscore クライアントライブラリの保守や更新を行う予定はありません。 | コードに Lodash／underscore が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |

## 削除された機能 {#removed-features}

この節では、AEM 6.5 で削除された機能について説明します。以前のリリースでは、これらの機能は「廃止」とマークされていました。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|--- |--- |--- |--- |
| [!DNL Experience Cloud] との統合 | [!DNL Adobe I/O] 経由での設定を使用して、アセットを [!DNL Experience Cloud] と同期できます。[!DNL Adobe Experience Cloud] は、以前は [!DNL Adobe Experience Cloud] と呼ばれていました。 | 質問がある場合は、[アドビカスタマーサポートまでお問い合わせください](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)。 |  |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。[Adobe Analytics が提供する ActivityMap プラグイン](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ja)を使用してください。 |  |
| 統合 | ExactTarget の統合は、デフォルトの配布（クイックスタート）から削除され、使用できなくなりました。 | 代替手段はありません。 |  |
| 統合 | Salesforce Force API との統合はデフォルトの配布版（クイックスタート）から削除され、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からインストールする追加パッケージになりました。 | 機能は引き続き利用できます。 |
| Forms | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |  |
| Forms | LiveCycle ES4 SP1 から JEE での AEM 6.5 Forms へ直接アップグレードすることはできません | 詳しくは、AEM Forms のアップグレードに関するドキュメントの[使用可能なアップグレードパス](../forms/using/upgrade.md)を参照してください。 |  |
| Forms | JEE 上の AEM Forms で、UPD ベースのクラスタリングがサポートされなくなりました。 | JEE 上の AEM Forms で使用できるのは、TCP ベースのクラスタリングのみです。UDP マルチキャストサーバーを以前のバージョンから JEE での AEM 5.5 Forms にアップグレードする場合は、手動設定を実行して、TCP ベースの GemFire クラスタリングに切り替えます。詳しい手順については、[JEE での AEM 6.5 Forms へのアップグレード](../forms/using/upgrade-forms-jee.md)を参照してください。 |  |
| デベロッパー向け | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| デベロッパー向け | HTML クライアントライブラリマネージャーで `customJavaScriptPath` がサポートされなくなりました。 | 代替機能はありません |  |
| [!DNL Assets] | アセットのオフロード機能は、[!DNL Adobe Experience Manager] 6.5 でサポートされなくなりました。 | 代替機能はありません。 |  |
| キャッシュ | `system/console/slingjsp` は、AEM 6.5 ではサポートされなくなりました。 | クラスとわずかなキャッシュが、Apache Sling Commons FileSystem ClassLoader バンドルに格納されています。AEM web コンソールでバンドル番号を確認し、ファイルシステムから直接キャッシュフォルダーを削除できます（`crx-quickstart/launchpad/felix/bundle<ID>`）。 |  |

## 次期リリースに関する予告 {#pre-announcement-for-next-release}

このセクションでは、今後のリリースで予定されている変更内容を事前にお知らせします。予告した変更内容はまだ実施されていませんが、お客様に影響を与えます。例えば、この機能はまだ非推奨になっていませんが、廃止後のユーザーに影響を与えます。 計画を立てる際の参考情報としてご覧ください。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| 基盤 | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/modernization-tools.md)詳細情報[）。 |
