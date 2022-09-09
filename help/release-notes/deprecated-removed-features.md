---
title: Adobe Experience Manager 6.5 リリースで廃止および削除された機能です。
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 62%

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
<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->
| DTM Tag Manager | DTM(Dynamic Tag Manager) との統合は廃止されました。 | Adobe Experience Platform Launchをタグマネージャーとして使用するように切り替えます。 || |Adobe Target|AEMが [!DNL Adobe I/O] AEM 6.5 のAdobe Target Standard API(Rest API) をベースとしている場合、Target Classic API(XML) の方法は非推奨（廃止予定）となりました。|統合の再設定先 [新しい API の使用](/help/sites-administering/target.md). || |Adobe Target| `mbox.js` AEMでのAdobe Targetとの統合は非推奨（廃止予定）となりました。|切り替えて使用 `at.js` 1.x.|| |コマース | [CIF REST](https://github.com/adobe/commerce-cif-api) は、AEMとコマースエンジン間の統合を可能にするマイクロサービスのセットとして 2018 年に提供されています。 アドビでは、2018年半ばに Magento を買収した後、2 つの理由でアプローチを変更することを決定しました。Magento には独自の Commerce API（REST および GraphQL）のセットがあり、2 組の API を維持することはお勧めしません。市場の動向から、お客様はデータをクエリするよりも効率的な GraphQL へと移行しつつあることがわかっています。2019年、アドビは、Magento の GraphQL API を情報源として使用した新しい Commerce 統合フレームワークをリリースしました。アドビでは今後、CIF REST に投資する予定はありません。お客様は、代替ソリューションを使用することをお勧めします。|AEM-Magento統合の場合は、 [AEM CIF アーキタイプ](https://github.com/adobe/aem-cif-project-archetype) および [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components). [コマース統合フレームワークを使用](/help/commerce/cif/integrating/magento.md)した、AEM と Adobe Commerce の統合を参照してください。新しいアプローチとのサードパーティ（Magento 以外）統合のサポートは、アドビのロードマップに記載されています。|| |コンポーネント (AEM Sites) |Adobeは、 `/libs/foundation/components`. コンポーネントフォルダーの `cq:deprecated` および `cq:deprecatedReason` プロパティを参照してください。AEM 6.5 には基盤コンポーネントが含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。また、基盤コンポーネントは非推奨（廃止予定）の場合でもサポートされます。 |Adobeは、将来のプロジェクトではコアコンポーネントを使用することをお勧めします。 既存のサイトは現状のままでもかまいませんし、コアコンポーネントを使用するように [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) でサイトをリファクタリングすることもできます。|| |コンポーネント (AEM Sites)|デザインインポーターのコンポーネント `/libs/wcm/designimporter/components` は 6.5 以降、非推奨としてマークされています。Adobeは、デザインインポーターのその実装をさらに強化する予定はありません。 |Adobeは、今後のリリースでこのユースケースの代替実装を提供する予定です。 || |Foundation|Granite オフロードフレームワーク。 アドビでは、アセット処理を外部化するために CQ 5.6.1 に導入されたオフロードフレームワークの機能を今後強化する予定はありません。|Adobeは、次世代のクラウドネイティブなオフロードフレームワークに取り組んでいます。||
|開発者向け|`Hobbes.js`. アドビでは、今後 `hobbes.js` ユーザーインタフェイステストフレームワークの機能を強化する予定はありません。|Adobeでは、Selenium の自動化を使用することをお勧めします。|| |開発者|jQuery UI クライアントライブラリ。 Adobeは、配布版（クイックスタート）の一部として提供される jQuery UI クライアントライブラリをさらに保守および更新する予定はありません。|Adobeは、コードに jQuery UI をプロジェクトコードベースに追加する必要があるお客様に推奨します。|| |開発者|jQuery アニメーションクライアントライブラリ (`granite.jquery.animation`) をクリックします。 Adobeは、配布版 (Quickstart) の一部として提供される jQuery Animation クライアントライブラリをさらに保守および更新する予定はありません。|Adobeは、コードに jQuery Animations を必要とするお客様に、プロジェクトコードベースに追加することを推奨します。|| |Developers|Handlebars クライアントライブラリ。 Adobeは、配布版 (Quickstart) の一部として提供される Handlebar クライアントライブラリをさらに保守および更新する予定はありません|Adobeは、コードをプロジェクトコードベースに追加するために Handlebars が必要なお客様に推奨します。|| |開発者|Lawnchair クライアントライブラリ。 Adobeは、配布版 (Quickstart) の一部として提供される Lawnchair クライアントライブラリをさらに保守および更新する予定はありません。|Adobeは、コードをプロジェクトコードベースに追加するために Lawnchair が必要なお客様に推奨します。|| |開発者|`Granite.Sling.js` クライアントライブラリ。 Adobeは、配布（クイックスタート）の一部として提供される Granite.Sling.js クライアントライブラリをさらに強化する予定はありません|Adobeでは、コードをリファクタリングして使用しなくすることをお勧めします。|| |開発者|YUI を使用した JavaScript クライアントライブラリの圧縮/縮小 YUI ライブラリがさらに更新される予定はありません。AEM 6.4 までは、JavaScript を軽量化するデフォルトの手段は YUI で、Google Closure Compiler（GCC）に切り替えるオプションもありました。AEM 6.5 以降は、GCC がデフォルトになっています。|Adobeでは、AEM 6.5 にアップグレードして実装用に GCC に切り替えることをお勧めします|| |開発者|クラシック UI のダイアログエディターをCRXDE Lite。 Adobeは、配布版（クイックスタート）の一部として提供されるクラシック UI ダイアログエディタをさらに強化する予定はありません|代替機能はありません。 || |Forms|AEM FormsとAEM Mobileの統合は廃止されました。 |置換できません。 ||Developers|クラシック UI ダイアログエディター (CRXDE Lite)。 Adobeは、配布版（クイックスタート）の一部として提供されるクラシック UI ダイアログエディタをさらに強化する予定はありません|代替機能はありません。 || |開発者|Lodash/underscore クライアントライブラリ。 Adobeは、配布版 (Quickstart) の一部として提供される Lodash/underscore クライアントライブラリをさらに保守および更新する予定はありません |Adobeでは、コードに Lodash/underscore を必要とするお客様が、プロジェクトコードベースに追加することをお勧めします。 ||

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
