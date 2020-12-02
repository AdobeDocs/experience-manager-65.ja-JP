---
title: ' [!DNL Adobe Experience Manager] 6.5の一般的なリリースノート'
description: '[!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能情報、インストール方法および詳細な変更リストが記載されています。'
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 65%

---


# [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}の一般的なリリースノート

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 |
| 種類 | メジャーリリース |
| 正式版の日付 | 2019 年 4 月 8 日 |
| 推奨されるアップデート | [AEM最近のアップデート](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html)を参照してください。 |

### 参考情報 {#trivia}

このバージョンの[!DNL Adobe Experience Manager]のリリースサイクルは、2018年4月4日を起点とし、23回にわたる品質保証とバグ修正を経て2019年3月28日に終了しました。 このリリースで修正された、機能強化と新機能を含むお客様関連の問題の総数は 1345 件です。   

[!DNL Adobe Experience Manager] 6.5は、2019年4月8日から一般に提供されています。

![AEM 6.5 ログイン画面](/help/assets/assets/aem65-login-v4.png)

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5は、 [!DNL Adobe Experience Manager] 6.4コードベースへのアップグレードリリースです。新機能および強化機能、お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、SP4までの[!DNL Adobe Experience Manager] 6.4 Service Packのリリースも含まれます。

以下のリストで概要を説明します。その後のページでは詳細をリストします。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

変更点の完全なリストについては、[AEM の基盤](/help/release-notes/wcm-platform.md)を参照してください。

[!DNL Adobe Experience Manager] 6.5のプラットフォームは、OSGiベースのフレームワーク（Apache SlingおよびApache Felix）の更新版とJava Content Repositoryの上に構築されます。Apache Jackrabbit Oak 1.10.2。

Quickstart は、サーブレットエンジンとして Eclipse Jetty 9.4.15 を使用します。

#### Java サポート  {#java-support}

* Java 11および既にサポートされているJava 8の新しいサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールと更新](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* Java 11およびJava 8のメンテナンスアップデートは、Oracleで公開されていない場合、AEM関連のプロジェクトでのお客様の利用を目的として、Adobeから配布されます。

#### Java の開発 {#java-development}

* 現在は[Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)の2つのバージョンがあり、非推奨とマークされていないパブリックインターフェイスを持つ推奨バージョンと、非推奨とマークされたインターフェイスを含むバージョンがあります。

#### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* ユーザーとグループの新しい権限管理UI。
* 列表示では、画面上に表示されるエントリのみを読み込み、それ以外のエントリはユーザーがスクロールを開始した場合にのみ読み込まれるようになりました。リストおよびカード表示では、AEM 6.0 以降、この機能が既に実装されています（AEM 6.4 で改善されました）。。
* 列表示に、該当する場合にページ/アセットのワークフローステータスが含まれるようになりました。
* [すべて選択](/help/sites-authoring/basic-handling.md#select-all)アクションを使用すると、同じフォルダー内のすべてのページ/アセットに対して、簡単にアクションを実行できます。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションは、読み込まれたページ／アセットだけでなく、すべてのページ／アセットに対してアクションを実行しようとします。バルクアクションを処理するようにアップグレードされていない場合は、警告ダイアログが表示されます。

>[!CAUTION]
>
>クラシック UI の機能がさらに強化される予定はありません。AEM 6.5 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は廃止中は引き続き完全にサポートされます。[詳細情報](/help/sites-deploying/ui-recommendations.md)。

#### 検索およびインデックス作成 {#indexing-and-search}

* Oak 内の検索では動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールに、結果の予測量が表示されます。
* QueryBuilderが拡張され、動的ファセットを結果に提供するようになりました。

#### アップグレード {#upgrade}

* AEM 6.5 への直接インプレースアップグレードは、AEM 6.2、6.3、6.4 を使用しているお客様に対してサポートされています。5.x または 6.0／6.1 を使用しているお客様がインプレースアップグレードを使用するには、まず 6.4 にアップグレードした後、6.5 にアップグレードするか、インスタンス間のコンテンツの転送を通じて AEM 6.5 に直接アップグレードする必要があります。

#### プロジェクトとワークフロー  {#projects-and-workflows}

* 6.4 で導入された新しいワークフローモデルエディターが改善され、「コピー」や「公開」などの新しい操作、ワークフローステップでの変数のサポート、強化された OR および AND 分割が追加されました。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

変更点の完全なリストは[AEM Sites とアドオン](/help/release-notes/sites.md)を参照してください。

#### 管理された単一ページアプリ {#managed-single-page-apps}

ページエディターでは、コンテンツのコンテキスト内編集と、レンダリングされたクライアント側エクスペリエンス内での作成／レイアウトの機能が追加されました（[SPA エディター](/help/sites-developing/spa-architecture.md)とも呼ばれます）。JavaScript フレームワークの React または Angular を使用して作成された既存の単一ページアプリを、AEM SJ SDK を使用して拡張することで、お客様による編集が可能になります。

SPA のサポートは AEM 6.4 SP2 の一部として導入されたものですが、AEM 6.5 ではさらに以下が可能になりました。

* テンプレートエディターを使用して、AEM で編集可能な SPA の部分を編集および設定できます。
* マルチサイト管理を使用して、国、フランチャイズ、または白いラベルのSPAエクスペリエンスを作成します。

#### ヘッドレスコンテンツ管理 {#headless-content-management}

AEM では、様々な形式で様々なスタックレベルからコンテンツを提供できます。一部は、2008 年以降、](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)Sling GET[ および ](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)POST Servlet[ で機能しています。コンテンツサービス（[Sling Model エクスポーター](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)）は AEM 6.3 で導入されたもので、AEM SJ SDK で単一ページアプリの改善に使用されている方法です。[HTTP API for Assets](/help/assets/mac-api-assets.md) は、AEM 6.5 向けに拡張された CRUD API です。

新しいHTTP API機能：

* [HTTP API for Assets でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになり、フラグメントの作成、更新、読み取り、削除が可能になりました。
* [コンテンツフラグメントリストのコアコンポーネント](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)でコンテンツサービスを通じてコンテンツフラグメントのリストを公開します。
* コンポーネントごとにコンテンツサービスのデフォルト JSON 出力を表示する[コアコンポーネントライブラリ](https://opensource.adobe.com/aem-core-wcm-components/library.html)

#### Screens アドオン  {#screens-add-on}

インタラクティブなキオスク端末からデジタルサイネージに至るまで、あらゆるデジタル表示でのエクスペリエンスを効率良くデザイン、配信、最適化します。

**デザイン**

* コンテンツ再利用の向上により、デジタルと実店舗の区別なくエクスペリエンスとコンテンツを統一できます。
* ローンチのサポートにより、オーサリングおよび承認／公開ワークフローを効率化します。
* SPA エディターを使用して、機能豊富でインタラクティブなエクスペリエンスを編集および配信できます。

**配信**

* 堅牢なオンラインおよびオフライン操作（スマート同期）が追加されてメディアプレイヤーのサポートが強化され、大規模なサイネージネットワークにも対応できるようになりました。

**最適化**

* 動的プレースホルダーを使用して、データでトリガーされるコンテンツの場所または設定別にパーソナライズできます。
* Adobe Analytics と AEM Screens Player の連携でインサイトの統合が促進されます。

AEM Screensへの変更の詳細については、『[AEM Screensユーザーガイド](https://docs.adobe.com/content/help/ja-JP/experience-manager-screens/user-guide/aem-screens-introduction.html)』の「リリースノート」を参照してください。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

[AEM 6.5 Assetsリリースノート](/help/release-notes/assets.md)の変更の完全リスト。

AEM 6.5 には、AEM ユーザー、DAM ロール、および関連するクリエイティブおよびマーケティングロールの生産性を高めるため、以下の機能およびき機能強化が導入されています。

#### Adobe Creative Cloud との連携  {#integration-with-adobe-creative-cloud}

[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)（Photoshop、Illustrator、InDesign などの Adobe Creative Cloud アプリケーションを使用するクリエイティブユーザー向けのアプリ内エクスペリエンス）の導入により、コンテンツ作成プロセスにおけるクリエイティブ担当者とマーケティング担当者のコラボレーションが効率化されます。AEMデスクトップアプリケーションは、任意のファイル形式やデスクトップアプリケーションを使用して、デスクトップ上のAEMのアセットを操作するユーザーのニーズを引き続きサポートします。

さらに、AEM は Adobe Stock と連携しているので、ユーザーは AEM Web UI から直接 Adobe Stock アセットの検索、プレビュー、ライセンス取得、保存をおこなえます。

![Photoshop の Asset Link パネル](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Connected Assets {#connected-assets}

「Connected Assets」機能は、中央AEM AssetsDAM展開の資産を活用する必要のあるAEM Sites展開の多い大規模な展開を対象としています。 一元的に管理されるアセットの管理を改善しながら、さまざまなサイトの導入に対するアセットの供給を効率的に行うことができます。

### Dynamic Media {#dynamic-media}

Dynamic Media により、リッチメディアのオーサリングと AEM Assets での配信が強化され、臨場感あふれるパーソナライズされた最先端のエクスペリエンスが促進されます。高品質のマスターアセットを使用すると、アドビの高度なクラウドレンダリング、スマート切り抜き、クラス最高のビューアを活用して、業界随一のパフォーマンスを備えた非常に魅力的なエクスペリエンスを提供できます。

新しい特長は次のとおりです。

* 360ビデオおよびVRヘッドセットのサポート
* カスタムビデオのサムネール
* アクセシビリティのサポート強化
* ホットリンク保護

#### ユーザーエクスペリエンスと検索 {#user-experience-and-search}

主要な機能強化により、動的検索ファセットを提供することで適切なアセットをすばやく見つけることができます。また、どのフォルダーまたは検索結果からでもすべてのアセットを選択できるようにすることで、複数のアセットを効率的に管理できます。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms では、いくつかの新機能と機能強化が加えられています。主なものを以下に示します。

* 送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を追跡できるトランザクションレポート
* インタラクティブコミュニケーションのユーザビリティの向上
* アダプティブフォームでのクラウドベースの電子署名
* AEM Sites の単一ページアプリケーション（SPA）へのアダプティブフォームやインタラクティブコミュニケーションの組み込み
* AEM ワークフローでの変数のサポート
* インタラクティブコミュニケーションでのデータ表示パターンのサポート
* アダプティブフォームおよびインタラクティブコミュニケーションテーブルの並べ替え
* フォームデータモデルでの入力データの自動検証

新機能および強化された機能とドキュメントのリソースについては、[AEM 6.5Forms](/help/forms/using/whats-new.md)の新機能および拡張機能の概要を参照してください。

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5 では、Communities に新機能や機能強化が加えられています。主なものを以下に示します。

* ユーザー生成コンテンツのオーサリング中における登録メンバーのタグ付け（@メンション）がサポートされています。
* グループメンバーへのダイレクトメッセージの一括送信がサポートされるようになりました。
* カスタムフィルターが開発され一括モデレート UI に追加されました。タグによるフィルタリングをデモする[サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)は、類似したカスタムフィルターを開発するための基盤として使用できます。
* 新しいリスト表示には、改善された一括モデレート UI が用意されています。
* 1 人のコミュニティ管理者ではなく、様々なコミュニティサイトおよびネストされたグループの管理者を個別に割り当てることができます。
* AEM 6.5 Communitiesのイネーブルメント機能は、[(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)エンジンをサポートします。
* アクセシビリティを向上させるために、イネーブルメントコンポーネントでキーボードナビゲーションをサポートしています。
* MSRP および DSRP. の設定時に Apache Solr 7.0 を選択できます。

変更の詳細なリストについては、[AEM 6.5 Communitiesリリースノート](/help/release-notes/communities-release-notes.md)を参照してください。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

使用している AEM 6.5 インスタンスを Livefyre と連携させることができます。[LivefyreとAEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)の統合方法を参照してください。

### お客様中心の開発を活用{#leverage-customer-focused-development}

アドビは、お客様が開発のすべての段階、つまり仕様、開発、テストに関与できる顧客中心開発モデルを使用しています。このプロセスにご協力いただいているお客様とパートナーの皆様に感謝いたします。

アドビでは、お客様中心のバグ修正と機能強化リクエストの開発に関する情報収集、優先順位付け、追跡の手順およびプロセスを整備しています。[Adobe Marketing Cloudサポートポータル](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html)は、Adobe機能強化と欠陥追跡システムと統合されています。 お客様からの問い合わせは、可能な場合はカスタマーケアで特定および解決されます。研究開発部門にエスカレートされた場合は、すべての顧客情報が収集され、優先順位付けとレポートに使用されます。有料サポート、保証付きの問題、お客様が支払った機能強化に対する開発が優先されます。

この優先順位付けのプロセスにより、AEM 6.5 では 750 件を超えるお客様中心の変更がおこなわれました。

## このリリースに含まれるファイルのリスト {#list-of-files-that-are-part-of-the-release}

**Foundation**

* スタンドアロンクイックスタート：`cq-quickstart-6.5.0.jar`.
* Application Server Quickstart:`cq-quickstart-6.5.0.war`.
* 様々なWebサーバーおよびプラットフォーム向けのDispatcher 4.3.2以降。 [ダウンロードリンク](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)を参照
* Eclipse IDE 用プラグイン（[詳細およびダウンロード](/help/sites-developing/aem-eclipse.md)）

* Brackets コードエディターの拡張機能（[詳細およびダウンロード](/help/sites-developing/aem-brackets.md)）
* Maven／Gradle の依存関係（[ダウンロードリンク](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/)）

**Sites**

* コアコンポーネント（[GitHub プロジェクト](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail 参照実装（[詳細](/help/sites-developing/we-retail.md)）
* Maven プロジェクトアーキタイプ：

   * フルスタックサイトの場合：[GitHub プロジェクト](https://github.com/adobe/aem-project-archetype)
   * React または Angular を使用した単一ページアプリの場合：[GitHub プロジェクト](https://github.com/adobe/aem-spa-project-archetype)

* 様々なプラットフォーム向けの AEM Screens Players（[ダウンロード](https://download.macromedia.com/screens/)）

* スマートコンテンツの言語モデル。英語は事前インストール済み。ほかに以下の言語がダウンロード可能

   * [ドイツ語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [スペイン語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [イタリア語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [フランス語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* ダイアログ変換ツールなどを含む AEM Modernize Tool Suite（[GitHub プロジェクト](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 強化された PDF Rasterizer を追加するためのパッケージ（[詳細](/help/assets/aem-pdf-rasterizer.md)）
* 強化された RAW 画像のサポートを追加するためのパッケージ（[詳細](/help/assets/camera-raw.md)）

**フォーム**

* [AEM Forms の機能パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)
* [AEM FormsOSGiクライアントSDK](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

## 言語 {#languages}

次の言語のユーザーインターフェイスが使用できます。

* 英語
* ドイツ語
* フランス語
* スペイン語
* イタリア語
* ブラジル語ポルトガル語
* 日本語
* 簡体字中国語
* 繁体字中国語（限定的にサポート）
* 韓国語

[!DNL Experience Manager] 6.5 は、中国語エンコーディング規格の使用に関する GB18030-2005 CITS の認定を受けています。

## インストールと更新{#install-update}

設定要件については、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

詳細な手順については、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

[AEM 6.5技術要件](/help/sites-deploying/technical-requirements.md)のサポートレベルを含む、サポートされているプラットフォームの完全なマトリックスを見つけます。

>[!NOTE]
>
>Oracleは、OracleJava SE製品の長期サポート(LTS)モデルに移行しました。 Java 9および10は、OracleのLTS以外のリリースです。[OracleJava SEのサポートロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html)を参照。 Adobeは、実稼働環境でのみAEMを実行するJavaのLTSリリースをサポートしています。 AEM 6.5では、Java 11が推奨されるバージョンです。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を常時評価して、さらに強力なバージョンへの置き換えの計画や、将来の展望や拡張に備えた部分的な再実装の決定を継続的におこなっています。

[!DNL Adobe Experience Manager] 6.5の場合、[廃止され、削除された機能のリスト](/help/release-notes/deprecated-removed-features.md)を読みます。 このページには、近い将来におこなわれる変更の予告と、前のリリースからアップデートするお客様向けの重要な注意事項も含まれています。

## 既知の問題 {#known-issues}

[既知の問題のリスト](/help/release-notes/known-issues.md)

### 製品のダウンロードとサポート（制限付きサイト） {#product-download-and-support-restricted-sites}

次のサイトは、お客様のみ利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/).

* [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)の追加機能に対する製品アップデート、パッチ、パッケージ。

* [Admin Consoleを介したカスタマーサポート](https://adminconsole.adobe.com/)。詳しくは、[新しいAdobeカスタマーサポート体験](https://docs.adobe.com/content/help/en/customer-one/using/home.html)を参照してください。
