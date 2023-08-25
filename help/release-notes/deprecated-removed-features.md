---
title: Adobe Experience Manager 6.5 リリースで廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: c2e9b2f3ea2603766e4062229d8e5278feed8788
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 61%

---

# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

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
<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->
| Dynamic Tag Manager (DTM) | DTM との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用するように切り替えます。||
|Adobe Target|AEM 6.5 では、[!DNL Adobe I/O] ベースの Adobe Target Standard API（Rest API）を使用して AEM から Adobe Target サービスに接続できるようになったので、Target Classic API（XML）方式は非推奨（廃止予定）になりました。|[新しい API を使用](/help/sites-administering/target.md)するように統合機能を再設定します。||
|Adobe Target|AEM と Adobe Target との `mbox.js` ベースの統合は非推奨（廃止予定）になりました。|`at.js` 1.x を使用するように切り替えます。||
| Commerce | AEM とコマースエンジンとの統合を可能にする一連のマイクロサービスとして 2018年に [CIF REST](https://github.com/adobe/commerce-cif-api) が提供されました。Adobeが 2018 年半ばにAdobe Commerce( 旧Magento) を買収した後、Adobeは 2 つの理由からアプローチを変更することを決定しました。 Commerce には独自のコマース API(REST とGraphQL) のセットがあり、2 組の API を維持するのはお勧めしません。 市場の動向から、お客様はデータをクエリするよりも効率的な GraphQL へと移行しつつあることがわかっています。2019 年に、Adobeは、コマースのGraphQL API を情報源として使用する新しいコマース統合フレームワークをリリースしました。 アドビでは今後、CIF REST に投資する予定はありません。代替ソリューションを使用することをお勧めします。| AEM-Commerce 統合の場合は、 [AEM CIF アーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components). [コマース統合フレームワークを使用](/help/commerce/cif/integrating/magento.md)した、AEM と Adobe Commerce の統合を参照してください。新しいアプローチとのサードパーティ（コマース以外）統合のサポートは、Adobeのロードマップに記載されています。||
| コンポーネント（AEM Sites）| アドビでは、`/libs/foundation/components` に格納されている基盤コンポーネントのほとんどについて、今後機能強化する予定はありません。コンポーネントフォルダーの `cq:deprecated` および `cq:deprecatedReason` プロパティを参照してください。AEM 6.5 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。さらに、基盤コンポーネントは、非推奨（廃止予定）になってもサポートされます。| 今後のプロジェクトではコアコンポーネントを使用することをお勧めします。既存のサイトは現状のままでもかまいませんし、コアコンポーネントを使用するように [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) でサイトをリファクタリングすることもできます。||
|コンポーネント（AEM Sites）|デザインインポーターコンポーネント `/libs/wcm/designimporter/components` は、6.5 以降、非推奨（廃止予定）になりました。アドビでは、このデザインインポーター実装を今後機能強化する予定はありません。| アドビでは、今後のリリースでこのユースケースの代替実装を提供する予定です。||
|基盤|Granite オフロードフレームワーク。 アドビでは、アセット処理を外部化するために CQ 5.6.1 に導入されたオフロードフレームワークの機能を今後強化する予定はありません。|アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。||
|開発者向け|`Hobbes.js`。アドビでは、今後 `hobbes.js` ユーザーインタフェイステストフレームワークの機能を強化する予定はありません。|Selenium での自動化を使用することをお勧めします。||
|開発者向け|jQuery UI クライアントライブラリ。Adobeは、配布版（クイックスタート）の一部として提供される jQuery UI クライアントライブラリをさらに保守および更新する予定はありません。 |Adobeは、コードに jQuery UI を引き続き必要とするお客様に、コードをプロジェクトコードベースに追加することをお勧めします。||
|開発者向け|jQuery アニメーションクライアントライブラリ（`granite.jquery.animation`）。Adobeは、配布版 (Quickstart) の一部として提供される jQuery Animation クライアントライブラリをさらに保守および更新する予定はありません。 |Adobeは、コードに jQuery アニメーションを引き続き必要とするお客様に、コードをプロジェクトコードベースに追加することをお勧めします。||
|開発者向け|Handlebars クライアントライブラリ。 Adobeは、配布版 (Quickstart) の一部として提供される Handlebar クライアントライブラリをさらに保守および更新する予定はありません。 |Adobeは、引き続き `Handlebars` を使用して、プロジェクトのコードベースに追加できます。||
|開発者向け|Lawnchair クライアントライブラリ。 Adobeは、配布版 (Quickstart) の一部として提供される Lawnchair クライアントライブラリをさらに保守および更新する予定はありません。 |Adobeは、コードをプロジェクトコードベースに追加するために Lawnchair を引き続き必要とするお客様にお勧めします。||
|開発者向け|`Granite.Sling.js` クライアントライブラリ。 Adobeは、配布版（クイックスタート）の一部として提供される Granite.Sling.js クライアントライブラリをさらに強化する予定はありません。 |Adobeは、ライブラリの機能に依存してコードをリファクタリングし、使用しなくすることをお勧めします。||
|開発者向け|YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。アドビでは、YUI ライブラリを今後更新する予定はありません。AEM 6.4 までは、JavaScript を軽量化するデフォルトの手段は YUI で、Google Closure Compiler（GCC）に切り替えるオプションもありました。AEM 6.5 以降は、GCC がデフォルトになっています。|AEM 6.5 にアップグレードする場合は、実装で GCC に切り替えることをお勧めします||
|開発者向け|CRXDE Lite のクラシック UI ダイアログエディター。 アドビでは、配布版（クイックスタート）の一部として出荷されているクラシック UI ダイアログエディターの機能を今後強化する予定はありません| 代替機能はありません。||
|Forms|AEM Forms と AEM Mobile の統合は非推奨（廃止予定）になりました。代替機能はありません。||開発者向け|CRXDE Lite のクラシック UI ダイアログエディター。アドビでは、配布版（クイックスタート）の一部として出荷されているクラシック UI ダイアログエディターの機能を今後強化する予定はありません| 代替機能はありません。||
|開発者向け|Lodash／Underscore クライアントライブラリ。Adobeは、配布版 (Quickstart) の一部として提供される Lodash/underscore クライアントライブラリをさらに保守および更新する予定はありません。 |Adobeでは、コードに Lodash/underscore を必要とするお客様が、プロジェクトコードベースに追加することをお勧めします。 || |Screens|Adobeは、2Publishers の設定に使用するcom.adobe.cq.screens.mq.activemq バンドルと関連する設定をさらに保守および更新する予定はありません。|Adobeでは、2Publishers のセットアップを引き続き必要とするお客様に、ロードバランサーのアプローチを使用することをお勧めします。 ||

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

## 次期リリースに関する予告 {#pre-announcement-for-next-release}

このセクションでは、今後のリリースで予定されている変更内容を事前にお知らせします。予告した変更内容はまだ実施されていませんが、お客様に影響を与えます。例えば、機能がまだ非推奨（廃止予定）になっていなくても、廃止後はユーザーに影響を与えるような場合です。計画を立てる際の参考情報としてご覧ください。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| 基盤 | UI フレームワーク | Adobeは、2019 年に Coral UI 2 コンポーネントの廃止を予定しています。 AEM 6.2 で Coral UI 3 が導入され、AEM 6.5 は完全に Coral 3 をベースにしています。 Adobeでは、Coral 2 でカスタム UI を構築したお客様およびパートナーに対し、Coral 3 にリファクタリングすることをお勧めします。 Adobeは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています — [詳細を表示](/help/sites-developing/modernization-tools.md). |
