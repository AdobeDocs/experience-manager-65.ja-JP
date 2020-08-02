---
title: Adobe Experience Manager6.5リリースの廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 44%

---


# 非推奨（廃止予定）の機能と削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

AEM機能の差し迫った削除または交換を伝えるには、次の規則が適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨ですが、機能は引き続きご利用いただけますが、それ以上強化されません。
1. 非推奨の機能が削除されたのは、最も早い時期に次のメジャーリリースで発生しています。 削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 非推奨（廃止予定）の機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| Creative Cloud統合 | AEMからCreative Cloudへのフォルダ共有は、クリエイティブユーザがAEMのアセットにアクセスできるように、AEM 6.2で導入されました。これにより、CCアプリケーションでアセットを開いて、新しいファイルをアップロードしたり、AEMに変更を保存したりできます。 Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することを強くお勧めします。 | AdobeアセットリンクやAEMデスクトップアプリケーションを含む、新しいCreative Cloud統合機能に切り替えることをお勧めします。 詳しくは、「AEMとCreative Cloud統合のベストプラクティス」を参照してください。 |
| Assets | `AssetDownloadServlet` は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、](/help/sites-administering/security-checklist.md)AEM セキュリティチェックリスト[を参照してください。 | 設定について詳しくは、[AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。 |
| Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | ユーザーのアクセス制御設定を保持し、適切な権限を確保します。 |
| Adobe Search&amp;Promote | Adobe Search&amp;Promoteとの統合は廃止されます。 Search&amp;Promote 統合機能がさらに強化される予定はありません。Search&amp;Promote 統合は廃止中も引き続き完全にサポートされます。 |  |
| DTM タグマネージャー | DTM（Dynamic Tag Manager）との統合は廃止されました。 | Adobe Experience Platform Launch をタグマネージャーとして使用してください。。 |
| Adobe Target | AEM 6.5 では、Adobe I/O ベースの Adobe Target Standard API（Rest API）を使用して AEM が Adobe Target サービスに接続できるようになったので、Target Classic API（XML）方式は廃止されました。 | Reconfigure the integration to [use the new API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
| Adobe Target | Using the `mbox.js` based integration with Adobe Target in AEM is deprecated. | Switch to use `at.js` 1.x. |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEMエンジンとコマースエンジンの統合を可能にする一連のマイクロサービスとして2018年に提供されました。 Adobeが2018年半ばにMagentoを獲得した後、Adobeは2つの理由からアプローチを変更することを決定しました。 Magentoには独自のコマースAPI （RESTおよびGraphQL）のセットがあり、2セットのAPIを維持するのはお勧めできません。 市場の動向から、お客様はGraphQLに向かって進んでいることがわかりました。これは、データをより効率的にクエリする方法であるためです。 2019年に、Adobeは、MagentoのGraphQL APIを真実の源泉として使用する新しいCommerce Integration Frameworkをリリースしました。 Adobeは、CIF RESTにこれ以上投資する予定はありません。 お客様には、交換ソリューションの使用を強くお勧めします。 | AEMとMagentoの統合の場合は、 [AEM CIFアーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIFコアコンポーネントに切り替えます](https://github.com/adobe/aem-core-cif-components)。 See AEM and Magento integration [using Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). 新しいアプローチを使用したサードパーティ(Magento以外)の統合のサポートは、アドビのロードマップに記載されています。 |
| コンポーネント（AEM Sites） | Adobe does not plan to make further enhancements to most of the Foundation Components stored in `/libs/foundation/components`. Look for the `cq:deprecated` and `cq:deprecatedReason` property in the component folder. AEM 6.5にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、これらをそのまま使用できます。 また、Foundation Componentsは、非推奨になっても完全にサポートされます。 | Adobeでは、今後のプロジェクトでコアコンポーネントの使用をお勧めします。 Existing sites can remain as is or use the [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) to refactor the site to use Core Components. |
| コンポーネント（AEM Sites） | Design Importer Components `/libs/wcm/designimporter/components` have been marked as deprecated starting 6.5. Adobe does not plan to make further enhancements to that implementation of the design importer. | Adobeでは、今後のリリースで使用事例の代替実装を提供する予定です。 |
| Foundation | Granite オフロードフレームワーク. Adobeでは、アセット処理を外部化するためにCQ 5.6.1で導入されたオフロードフレームワークをさらに拡張する予定はありません。 | アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。 |
| 開発者向け | `Hobbes.js`」を選択します。Adobe does not plan to make further enhancements to the `hobbes.js` user interface testing framework. | Adobeでは、Seleniumの自動化を使用することをお勧めします。 |
| 開発者向け | jQuery UI クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加する際に、引き続きjQuery UIが必要な場合をお勧めします。 |
| 開発者向け | jQuery Animationクライアントライブラリ(`granite.jquery.animation`)。 配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加する際に、jQuery Animationsを必要とするお客様に推奨します。 |
| 開発者向け | Handlebars クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Handlebars クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加する際に、コードのハンドルバーが必要な場合にお勧めします。 |
| 開発者向け | Lawnchair クライアントライブラリ. 配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリがさらに保守および更新される予定はありません。 | Adobeでは、コードをプロジェクトコードベースに追加するためにLawnchairを必要とするお客様に推奨します。 |
| 開発者向け | `Granite.Sling.js`クライアントライブラリに埋め込みます。配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能がさらに強化される予定はありません。 | Adobeでは、ライブラリの機能に依存しているお客様に、コードを使用しなくなるようにリファクタリングすることをお勧めします。 |
| 開発者向け | YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4までは、YUIはJavaScriptを縮小するためのデフォルトで、Google Closure Compiler(GCC)に切り替えるオプションを持っていました。 AEM 6.5 以降は、GCC がデフォルトになっています。 | Adobeでは、AEM 6.5にアップグレードしてGCCに切り替えて導入することを推奨しています。 |
| 開発者向け | CRXDE Lite のクラシック UI ダイアログエディター. 配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。 | 置き換えが利用できません。 |
| フォーム | AEM MobileとのAEM Forms統合は廃止されました。 | 置き換えはありません。 |

## 削除された機能 {#removed-features}

この節では、AEM 6.5から削除された機能と機能に関するリストを示します。以前のリリースでは、これらの機能は非推奨としてマークされていました。

| 領域 | 機能 | 代替手段 |
|--- |--- |--- |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。Adobe Analyticsが提供するActivityMap [プラグインを使用します](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html)。 |
| 統合 | ExactTarget統合は、デフォルトの配布(Quickstart)から削除され、使用できなくなりました。 | 代替機能はありません. |
| 統合 | Salesforce Force API integration has been removed from the default distribution (Quickstart) and is now an extra package to install from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | この機能は引き続き使用できます。 |
| フォーム | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません. |
| フォーム | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません. |
| フォーム | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |
| フォーム | LiveCycleES4 SP1からAEM 6.5Forms（JEE上）へのシングルホップアップグレードは利用できません | AEM Formsアップグレードドキュメントの [利用可能なアップグレードパス](../forms/using/upgrade.md) を参照してください。 |
| フォーム | JEE上のAEM Formsから、UPDベースのクラスタリングのサポートを削除しました。 | JEE上のAEM Formsでは、TCPベースのクラスタリングのみを使用できます。 UDPマルチキャストサーバーを以前のバージョンからAEM 5.5Forms（JEE上）にアップグレードする場合は、手動設定を実行してTCPベースのGemfireクラスタリングに切り替えます。 詳細な手順については、「JEE上のAEM 6.5 formsへの [アップグレード」を参照してください。](../forms/using/upgrade-forms-jee.md) |
| 開発者向け | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| 開発者向け | Remove `customJavaScriptPath` support in HTML Client Library Manager. | 代替機能はありません |
| [!DNL Assets] | アセットのオフロード機能は、 [!DNL Adobe Experience Manager] 6.5で削除されました。 | 置き換えが利用できません。 |
| キャッシュ | `system/console/slingjsp` は、AEM 6.5では使用できなくなりました。 | クラスとスライトリーキャッシュは、Apache Sling Commons FileSystem ClassLoaderバンドルの下に格納されます。 AEM Webコンソールでバンドル番号を確認し、キャッシュフォルダーをファイルシステムから直接削除できます(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |

## Pre-announcement for next release {#pre-announcement-for-next-release}

このセクションは、今後のリリースで予定されている変更を事前に発表するために使用します。 発表された変更はまだ有効ではありませんが、お客様に影響を与えます。 例えば、この機能は非推奨とはなっていませんが、非推奨になった後のユーザーに影響を与えます。 これらの更新は、計画を立てるために提供されます。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| Foundation | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/dialog-conversion.md)詳細情報[）。 |
