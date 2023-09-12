---
title: Adobe Experience Manager 6.5 リリースで廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: aec2eb3303ad9747f6f56ae2eb31c3c7ed7b0c24
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 75%

---

# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

アドビでは、製品の機能を絶えず評価して、常に下位互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

Adobe Experience Manager(AEM) 機能の差し迫った削除または置き換えを伝達するために、次の規則が適用されます。

1. 廃止の発表がまず行われます。廃止中は、機能はまだ使用可能ですが、それ以上の機能強化は行われません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースで行われます。削除の実際の目標日は、後日発表されます。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 廃止される機能 {#deprecated-features}

この節では、AEM 6.5 で非推奨とマークされている機能を示します。一般に、将来のリリースで削除が予定されている機能は、まず非推奨（廃止予定）に設定され、代わりの機能も提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するように実装を変更するための計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 | バージョン (SP) |
|---|---|---|---|
| Screens | AEMの ActiveMQ。 2 つのAEMパブリッシュインスタンス間の通信に ActiveMQ が使用されていました。 | Adobeでは、ロードバランサーを使用することをお勧めします。 |  |
| [!DNL Sites] | **ソーシャルメディアのステータス**&#x200B;のエクスペリエンスフラグメントのプロパティ。 |   | 6.5.11.0 |
| [!DNL Sites] | シンプルなコンテンツフラグメントを作成するためのコンテンツフラグメントテンプレート。 | 現在の[モデルベースの構造化コンテンツフラグメント](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud 統合 | AEMからCreative Cloudへのフォルダー共有は、AEM 6.2 で導入されました。クリエイティブユーザーにAEMのアセットへのアクセス権を付与し、クリエイティブユーザーがアセットをで開くことができるようにします。 [!DNL Creative Cloud] アプリケーションを起動し、新しいファイルをアップロードしたり、変更をAEMに保存したりします。 Creative Cloudアプリケーションの新機能であるAdobeAsset Link がリリースされ、Photoshop、InDesign、Illustrator内からAEM内から直接、より優れたユーザーエクスペリエンスと、より強力なアセットへのアクセスを提供します。 AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することをお勧めします。 | Adobe Asset Link や AEM Desktop App などの新しい Creative Cloud 統合機能に切り替えることをお勧めします。 |  |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |  |
| 統合 | [!DNL Experience Manager] 6.5 で [!DNL Experience Manager] と [!DNL Adobe Target] の統合が更新されたことにより、**[!UICONTROL AEM クラウドサービスのオプトイン]**&#x200B;画面は非推奨になりました。この統合では、Adobe Target Standard API をサポートしています。API は、Adobe IMS と [!DNL Adobe I/O Runtime] の認証方法を使用します。これは、Adobe Experience Platform Launch が分析およびパーソナライゼーション用に [!DNL Experience Manager] ページを構築する役割が増大していることをサポートするもので、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O Runtime] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 | 6.5.7.0 |
| コネクタ | Microsoft® SharePoint 2010 および Microsoft® SharePoint 2013 用の Adobe JCR Connector は、[!DNL Experience Manager] 6.5 で非推奨になりました。 | 該当なし |  |
| Dynamic Tag Manager (DTM) | DTM との統合は廃止されました。 | Adobe Experience Platform Launchをタグマネージャーとして使用するように切り替えます。 |   |
| Adobe Target | AEM 6.5 では、[!DNL Adobe I/O] ベースの Adobe Target Standard API（Rest API）を使用して AEM が Adobe Target サービスに接続できるようになり、Target Classic API（XML）方式は廃止されました。 | [新しい API を使用](/help/sites-administering/target.md)するように統合機能を再設定してください。 |  |
| Adobe Target | `mbox.js` を使用した AEM と Adobe Target の統合は廃止されました。 | `at.js` 1.x の使用に切り替えてください。 |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEM とコマースエンジン間の統合を可能にするマイクロサービスのセットとして 2018年に提供されています。Adobeが 2018 年半ばにAdobe Commerce( 旧Magento) を買収した後、Adobeは 2 つの理由からアプローチを変更することを決定しました。 Commerce には独自のコマース API(REST とGraphQL) のセットがあり、2 組の API を維持するのはお勧めしません。 市場の動向から、お客様はデータをクエリするよりも効率的な GraphQL へと移行しつつあることがわかっています。2019 年に、Adobeは、コマースのGraphQL API を情報源として使用する新しいコマース統合フレームワークをリリースしました。 アドビでは今後、CIF REST に投資する予定はありません。代替ソリューションを使用することをお勧めします。 | AEM-Commerce 統合の場合は、 [AEM CIF アーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components). [コマース統合フレームワークを使用](/help/commerce/cif/integrating/magento.md)した、AEM と Adobe Commerce の統合を参照してください。新しいアプローチとのサードパーティ（コマース以外）統合のサポートは、Adobeのロードマップに記載されています。 |  |
| コンポーネント（AEM Sites） | アドビでは、`/libs/foundation/components` に格納されている基盤コンポーネントのほとんどについて、今後機能強化する予定はありません。コンポーネントフォルダーの `cq:deprecated` および `cq:deprecatedReason` プロパティを参照してください。AEM 6.5 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。さらに、基盤コンポーネントは、非推奨（廃止予定）になってもサポートされます。 | アドビは、将来のプロジェクトではコアコンポーネントを使用することをお勧めします。既存のサイトは現状のままでもかまいませんし、コアコンポーネントを使用するように [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) でサイトをリファクタリングすることもできます。 |  |
| コンポーネント（AEM Sites） | デザインインポーターコンポーネント `/libs/wcm/designimporter/components` は、6.5 以降、廃止となりました。アドビでは、このデザインインポーター実装を今後機能強化する予定はありません。 | 今後のリリースで使用事例の代替実装を提供する予定です。 |  |
| 基盤 | Granite オフロードフレームワーク。アドビでは、アセット処理を外部化するために CQ 5.6.1 に導入されたオフロードフレームワークの機能を今後強化する予定はありません。 | Adobeは、次世代のクラウドネイティブなオフロードフレームワークに取り組んでいます。 |  |
| デベロッパー向け | `Hobbes.js`。アドビでは、今後 `hobbes.js` ユーザーインタフェイステストフレームワークの機能を強化する予定はありません。 | アドビでは、Selenium の自動化を使用することをお勧めします。 |  |
| デベロッパー向け | jQuery UI クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリの保守や更新を行う予定はありません。。 | コードに jQuery UI が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | jQuery アニメーションクライアントライブラリ（`granite.jquery.animation`）。アドビでは今後、配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリの保守や更新を行う予定はありません。。 | コードに jQuery アニメーションが引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | Handlebars クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Handlebar クライアントライブラリの保守や更新を行う予定はありません。。 | Adobeは、引き続き `Handlebars` を使用して、プロジェクトのコードベースに追加できます。 |  |
| デベロッパー向け | Lawnchair クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリの保守や更新を行う予定はありません。。 | コードに Lawnchair が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| デベロッパー向け | `Granite.Sling.js` クライアントライブラリ。アドビでは、配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能を今後強化する予定はありません。。 | このライブラリの機能に頼っている場合は、それを使用しないようにコードをリファクタリングすることをお勧めします。 |  |
| デベロッパー向け | YUI を使用した JavaScript クライアントライブラリの圧縮/縮小。 アドビでは、YUI ライブラリを今後更新する予定はありません。AEM 6.4 までは、JavaScript を軽量化するデフォルトの手段は YUI で、Google Closure Compiler（GCC）に切り替えるオプションもありました。AEM 6.5 以降は、GCC がデフォルトになっています。 | AEM 6.5 にアップグレードする場合は、GCC に切り替えることをお勧めします。 |  |
| デベロッパー向け | クラシック UI ダイアログエディタのCRXDE Lite。 アドビでは、配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能を今後強化する予定はありません。 | 代替手段はありません。 |  |
| Forms | AEM Forms と AEM Mobile の統合は非推奨（廃止予定）となりました。 | 代替手段はありません。 |  | デベロッパー向け | クラシック UI ダイアログエディタのCRXDE Lite。 アドビでは、配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能を今後強化する予定はありません。 | 代替機能はありません。 |  |
| デベロッパー向け | Lodash／underscore クライアントライブラリ。アドビでは今後、配布版（クイックスタート）の一部として含まれている Lodash/underscore クライアントライブラリの保守や更新を行う予定はありません。。 | コードに Lodash／underscore が引き続き必要な場合は、このクライアントライブラリをプロジェクトコードベースに追加することをお勧めします。 |  |
| Screens | Adobeでは、2Publishers のセットアップに使用するcom.adobe.cq.screens.mq.activemq バンドルと関連する設定をさらに保守および更新する予定はありません。 | Adobeでは、2Publishers のセットアップを引き続き必要とするお客様に、ロードバランサーのアプローチを使用することをお勧めします。 |  |

## 削除された機能 {#removed-features}

この節では、AEM 6.5 で削除された機能について説明します。以前のリリースでは、これらの機能は「廃止」とマークされていました。

| 領域 | 機能 | 代替手段 | バージョン (SP) |
|--- |--- |--- |--- |
| [!DNL Experience Cloud] との統合 | [!DNL Adobe I/O] 経由での設定を使用して、アセットを [!DNL Experience Cloud] と同期できます。[!DNL Adobe Experience Cloud] は、以前は [!DNL Adobe Experience Cloud] と呼ばれていました。 | 質問がある場合は、[アドビカスタマーサポートまでお問い合わせください](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja#support)。 |  |
| AnalyticsActivity Map | AEMに含まれるActivity Mapのバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。[Adobe Analytics が提供する ActivityMap プラグイン](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ja)を使用してください。 |  |
| 統合 | ExactTarget の統合は、デフォルトの配布（クイックスタート）から削除され、使用できなくなりました。 | 代替手段はありません。 |  |
| 統合 | Salesforce Force API との統合はデフォルトの配布版（クイックスタート）から削除され、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からインストールする追加パッケージになりました。 | 機能は引き続き利用できます。 |
| Forms | Central 製品のサポートが終了したので、AdobeCentral Migration Bridge サービスのAdobeは削除されました。 | 代替機能はありません. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |  |
| Forms | LiveCycle ES4 SP1 から JEE での AEM 6.5 Forms へ直接アップグレードすることはできません | 詳しくは、AEM Forms のアップグレードに関するドキュメントの[使用可能なアップグレードパス](../forms/using/upgrade.md)を参照してください。 |  |
| Forms | JEE 上の AEM Forms で、UPD ベースのクラスタリングがサポートされなくなりました。 | JEE 上の AEM Forms で使用できるのは、TCP ベースのクラスタリングのみです。UDP マルチキャストサーバーを以前のバージョンから JEE 上のAEM 5.5 Formsにアップグレードする場合は、手動設定を実行して、TCP ベースの GemFire クラスタリングに切り替えます。 詳しい手順については、[JEE での AEM 6.5 Forms へのアップグレード](../forms/using/upgrade-forms-jee.md)を参照してください。 |  |
| デベロッパー向け | Firebug Lite がデフォルトの配布版（クイックスタート）から削除されました | ブラウザーの組み込みの開発者コンソールを使用する |
| デベロッパー向け | HTML クライアントライブラリマネージャーで `customJavaScriptPath` がサポートされなくなりました。 | 代替機能はありません |  |
| [!DNL Assets] | アセットのオフロード機能は、[!DNL Adobe Experience Manager] 6.5 でサポートされなくなりました。 | 代替機能はありません。 |  |
| キャッシュ | `system/console/slingjsp` が削除され、AEM 6.5 では使用できなくなりました。 | クラスとわずかなキャッシュが、Apache Sling Commons FileSystem ClassLoader バンドルに格納されています。AEM web コンソールでバンドル番号を確認し、ファイルシステムから直接キャッシュフォルダーを削除できます（`crx-quickstart/launchpad/felix/bundle<ID>`）。 |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
