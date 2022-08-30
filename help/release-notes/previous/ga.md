---
title: 一般リリースノート（ [!DNL Adobe Experience Manager]  6.5）
description: 「[!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法および詳細な変更リストが記載されています」
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '4697'
ht-degree: 74%

---

# 一般リリースノート（[!DNL Adobe Experience Manager] 6.5）{#general-release-notes-for-adobe-experience-manager}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 |
| 種類 | メジャーリリース |
| 一般公開日 | 2019年4月8日（PT） |
| 推奨されるアップデート | 詳しくは、 [AEM の最新のアップデート](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=en)を参照してください。 |

### 参考情報 {#trivia}

このバージョンののリリースサイクル [!DNL Adobe Experience Manager] 2018 年 4 月 4 日に開始し、23 回の品質保証とバグ修正を繰り返し、2019 年 3 月 28 日に終了しました。 このリリースで修正された機能強化や新機能を含む、お客様関連の問題の総数は 1345 です。

[!DNL Adobe Experience Manager] 6.5 は、2019年4月8日（PT）に一般公開されました。

![AEM 6.5 ログイン画面](/help/assets/assets/aem65-login-v4.png)

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 は、[!DNL Adobe Experience Manager] 6.4 コードベースに対するアップグレードリリースです。新機能と拡張機能、主なお客様向けの修正、優先度の高いお客様向けの機能強化、製品の安定化に向けた一般的なバグ修正を提供します。 また、[!DNL Adobe Experience Manager] 6.4 の SP4 までのサービスパックリリースも含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

のプラットフォーム [!DNL Adobe Experience Manager] 6.5 OSGi ベースのフレームワーク（Apache Sling および Apache Felix）の更新バージョンと Java™ Content Repository の上に構築：Apache Jackrabbit Oak 1.10.2.

Quickstart は、サーブレットエンジンとして Eclipse Jetty 9.4.15 を使用します。

#### Java™サポート  {#java-support}

* Java™ 11 の新しいサポートと、既にサポートされている Java™ 8。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* Java™ 11 および Java™ 8 のメンテナンスアップデートは、AdobeがAEM関連のプロジェクトでのお客様向けの使用を目的として、Oracleから公開されない場合に配布されます。

#### Java™開発 {#java-development}

* 現在 [Uberjar の 2 つのバージョン](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)：非推奨とマークされていないパブリックインターフェイスを含む推奨バージョン、および非推奨とマークされたインターフェイスを含むバージョン。

#### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* ユーザーとグループの新しい権限管理 UI
* 列表示では、画面に表示されるエントリのみが読み込まれ、ユーザーがスクロールを開始したときにのみ読み込まれるようになりました。 リスト表示とカード表示は、6.0 以降に既に行われています（6.4 で改善されました）。
* 列表示には、該当する場合、ページやアセットのワークフローステータスが含まれるようになりました。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションを使用すると、同じフォルダー内のすべてのページやアセットに対してアクションを手軽に実行することができます。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションは、読み込まれたページやアセットだけでなく、すべてのページやアセットに対してアクションの実行を試みます。アクションがバルクアクションを処理するようにアップグレードされていない場合、警告ダイアログが表示されます。

>[!CAUTION]
>
>クラシック UI の機能がさらに強化される予定はありません。AEM 6.5 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は非推奨の間も引き続き完全にサポートされます。 [詳細情報](/help/sites-deploying/ui-recommendations.md)。

#### 検索およびインデックス作成 {#indexing-and-search}

* Oak の検索で動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールには、結果の推定数が表示されます。
* QueryBuilder は、動的ファセットを使用して結果を返すように拡張されました。

#### アップグレード {#upgrade}

* AEM 6.2、6.3、6.4 を実行しているお客様は、AEM 6.5 への直接インプレースアップグレードがサポートされています。インプレースアップグレードを使用するお客様は、まず 6.4 にアップグレードする必要があります。 その後、6.5 にアップグレードするか、インスタンス間で直接AEM 6.5 にコンテンツを転送する方法でアップグレードします。
* アップグレード手順は 6.5 でもほぼ変わりません。
* アドビでは、6.4 で導入された後方互換性、アップグレードの複雑性の評価、持続可能なアップグレードの機能を引き続きサポートします。必要に応じて、これらの領域にバージョン固有の更新がおこなわれました。
* パターン検出のパッケージ化がシンプルになりました。 6.5 へのアップグレードを評価するパッケージが 1 つあり、利用可能なソースバージョンに対して 1 つあります。
* アップグレードの手順について詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

#### プロジェクトとワークフロー {#projects-and-workflows}

* 6.4 で導入された新しいワークフローモデルのエディターが改善され、コピーや公開などの新しい操作、ワークフローステップでの変数のサポート、強化された `OR` 分割および `AND` 分割が追加されました。

#### リポジトリ {#repository}

* Adobe Experience Manager 6.5 の基盤は、OSGi ベースのフレームワーク（Apache Sling および Apache Felix）の更新バージョンと Java™ Content Repository の上に構築されています。Apache Jackrabbit Oak 1.10.2.
* 修正された問題の概要については、[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) および [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) を参照してください。

>[!CAUTION]
>
>AEM 6.3 以降に存在する Oak Segment Tar の新しいバージョンには、リポジトリの移行が必要です。 この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。

#### OSGi {#osgi}

* OSGi Promises および Converter ユーティリティライブラリが追加されました。

#### セキュリティ {#security}

* 管理者ユーザーのパスワードの有効期限を追加しました。

#### Web サーバー {#web-server}

* クイックスタート配布版では、Eclipse Jetty 9.4.15 をサーブレットエンジンとして使用します（AEM 6.4 には 9.3.22 が付属）。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 管理された単一ページアプリ {#managed-single-page-apps}

ページエディターでは、コンテンツのコンテキスト内編集と、レンダリングされたクライアント側エクスペリエンス内での作成／レイアウトの機能が追加されました（[SPA エディター](/help/sites-developing/spa-architecture.md)とも呼ばれます）。JavaScript フレームワークの React または Angular を使用して作成された既存の単一ページアプリを、AEM SJ SDK を使用して拡張することで、お客様による編集が可能になります。

SPA のサポートは AEM 6.4 SP2 の一部として導入されたものですが、AEM 6.5 ではさらに以下が可能になりました。

* テンプレートエディターを使用して、AEM で編集可能な SPA の部分を編集および設定できます。
* マルチサイト管理を使用して、国、フランチャイズまたはホワイトラベルの付いたSPAエクスペリエンスを作成する

#### ヘッドレスコンテンツ管理 {#headless-content-management}

AEMは、様々な形式やスタックの様々なレベルからコンテンツを提供できます。 一部は、2008 年以降、](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)Sling GET[ および ](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)POST Servlet[ で機能しています。コンテンツサービス（[Sling Model エクスポーター](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=en)）は AEM 6.3 で導入されたもので、AEM SJ SDK で単一ページアプリの改善に使用されている方法です。[HTTP API for Assets](/help/assets/mac-api-assets.md) は、AEM 6.5 向けに拡張された CRUD API です。

新しい HTTP API の機能は次のとおりです。

* 追加済み [アセットの HTTP API に対するコンテンツフラグメントのサポート](/help/assets/assets-api-content-fragments.md) フラグメントを作成、更新、読み取り、削除するには、次の手順に従います。
* [コンテンツフラグメントリストのコアコンポーネント](https://www.aemcomponents.dev)でコンテンツサービスを通じてコンテンツフラグメントのリストを公開します。
* コンポーネントごとにコンテンツサービスのデフォルト JSON 出力を表示する[コアコンポーネントライブラリ](https://www.aemcomponents.dev)

#### Screens アドオン {#screens-add-on}

インタラクティブなキオスクからデジタルサイネージに至るまで、すべてのデジタルディスプレイでエクスペリエンスを効率的に設計、配信および最適化します。

* コンテンツ再利用の向上により、デジタルと実店舗の区別なくエクスペリエンスとコンテンツを統一できます。
* ローンチのサポートにより、オーサリングおよび承認／公開ワークフローを効率化します。
* SPA エディターを使用して、機能豊富でインタラクティブなエクスペリエンスを編集および配信できます。
* ローンチを使用して、サイネージコンテンツの今後の変更を計画できるようになりました。
* シーケンスチャンネルでの従量制再生が可能になりました。
* ソースファイル（Excel シートなど）を使用してプロジェクト構造を自動作成できるようになりました。
* 堅牢なオンラインおよびオフラインの操作（スマート同期）が追加されてメディアプレイヤーのサポートが強化され、大規模なサイネージネットワークにも対応できるようになりました。
* 動的プレースホルダーを使用して、データでトリガーされるコンテンツの場所または設定別にパーソナライズできます。
* Adobe Analytics と AEM Screens Player の連携でインサイトの統合が促進されます。

AEM Screens の変更点について詳しくは、[AEM Screens ユーザーガイド](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=ja)のリリースノートを参照してください。

#### コンポーネントとテンプレートの開発 {#component-amp-template-development}

* 新規プロジェクト用の Maven プロジェクトアーキタイプ 18 以降 ( [リリースノート用の GitHub](https://github.com/adobe/aem-project-archetype/releases).
* 新しいプロジェクト用の単一ページアプリ Maven プロジェクトアーキタイプ 1.0.6 以降 ( [リリースノート用の GitHub](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL バージョン 1.4( [リリースノート用の GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * 文字列、配列およびオブジェクトに対する「in」演算子：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * data-sly-set を使用した変数の宣言
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 制御パラメーターのリストと繰り返し（begin、step、end）
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap の識別子

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 負の数のサポート

* コアコンポーネント 2.3.2 以降 ( [リリースノート用の GitHub](https://github.com/adobe/aem-core-wcm-components/releases).
* レイアウトコンテナのグリッドシステム ( [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* クライアントライブラリマネージャー：JavaScript クライアントライブラリの軽量化に合わせて Google Closure Compiler がデフォルトになり（以前のデフォルトは Yahoo YUI でした）、Google Closure Compiler がバージョン v20190121 に更新されました。
* テンプレートエディターとポリシー

   * JS SDK を使用している単一ページアプリのテンプレートを作成および編集できます（SPA エディターとも呼ばれます）。

* リファレンスサイト We.Retail 4.0( [リリースノート用の GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* 最新のエディタ機能を使用するために既存のサイトをアップグレードするツールキットについては、 [GitHub リポジトリ](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM には、既存のカスタムコードとの互換性を最大限に高めるために、jQuery ライブラリのバージョン 1.12.4 が含まれています。セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

#### サイト管理 {#site-administration}

* [参照](/help/sites-authoring/author-environment-tools.md#references)レールには、選択したページを参照する内部リンクを一覧表示する新しいセクションがあります。これは、ページをオフラインで取得したり削除することが想定される場合や、オフラインで取得する前に調整する必要があるページを確認する場合に便利です。
* この [リスト表示](/help/sites-authoring/basic-handling.md#list-view) には、ページがワークフロー内にあるときのステータスを示す新しいワークフロー列があります。
* [ページのプロパティ](/help/sites-authoring/editing-page-properties.md)で、ページにサムネールを割り当てるときに既存のアセットを参照できるようになりました（「サムネール」タブ）。

#### ページエディター {#page-editor}

* JS SDK(SPA Editor とも呼ばれます ) を使用する React およびAngularのクライアントサイドコンポーネントを使用して構築された、シングルページアプリエクスペリエンスのコンテキスト内編集と構成を可能にします
* 基礎モードは、ページに基礎モードが設定されている場合にのみ表示されます。

#### コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* 新規 [注釈](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) コンテンツフラグメントエディターのパネルを使用して、一般的なコメントを作成したり、テキスト内でおこなわれたコメントを表示したりできます（タイムラインパネルにも表示されます）。
* 複数行テキスト要素のデフォルトコンテンツタイプを [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md) シンプルテキスト、リッチテキストまたは Markdown へ
* RTE（フルスクリーン表示）でテキストを選択して、[コメント／注釈](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)を追加できます。
* 参照レールでコンテンツフラグメント並列に表示して、[バージョンを比較](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)できるようになりました。
* アセットのダウンロードレポートにコンテンツフラグメントが適宜表示されるようになりました。
* /api.json を通じて、[Assets HTTP API でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになりました。コンテンツフラグメントの作成、更新、読み取り、削除をおこなうための API があります。

#### エクスペリエンスフラグメント {#experience-fragments}

* [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)のインデックス作成を改善して、フラグメントの使用ページの検索でコンテンツが見つかるようになりました。。
* この [Target に書き出し](/help/sites-administering/experience-fragments-target.md) 「 」オプションを使用すると、エクスペリエンスフラグメントを JSON( デフォルトは「HTML」) またはその両方として送信できるようになりました。

#### 翻訳 {#translation}

* プロジェクトマスターを使用して、翻訳プロジェクトを手軽に作成できます。。
* 翻訳ジョブをデフォルトで承認済みステータスに設定することで、翻訳プロジェクトの実行を簡単にします。
* サードパーティの翻訳メモリの変更を使用して翻訳済みページを更新することを許可します。
* JSON 形式での翻訳ジョブの書き出しを許可します。
* V3 API を使用するようにMicrosoft®翻訳統合を更新しました。

#### マルチサイト管理（MSM） {#multi-site-management-msm}

* PushOnModify を使用するロールアウト設定について、矛盾した状態を避けるためにページ移動操作の処理を改善しました。。
* ライブコピー構造内にページを作成すると、デフォルトでスタンドアロンページが作成されます。
* JS SDK を使用している単一ページアプリで MSM 機能を使用できます（SPA エディターとも呼ばれます）。

#### ローンチ {#launches}

* ローンチの新しいレビューおよび承認ワークフローと、承認済みのローンチページのみ昇格させる機能が追加されました。
* [プロモーションステップの直後にローンチを削除するオプションが UI に追加](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)されました。

#### コンテンツのターゲット設定とシミュレーション {#content-targeting-simulation}

* ContextHub データレイヤーおよびクライアント側ルールエンジンの JavaScript が更新され、jQuery 3 をデフォルトで使用するようになりました。

#### AEM と Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>現在：
>
>* AEM アクティビティ コンソールで Adobe Target をターゲティングエンジンとして使用している場合、`at.js 1.x` のみをサポートしています。
>
>* Target へのエクスペリエンスフラグメントのエクスポートを使用し、Target のコンソールでアクティビティを実行している場合、`at.js. 1.x` と `at.js 2.x` の両方をサポートしています。


* Adobe Targetの統合で Target Standard API が使用されるようになりました。 以前のバージョンの AEM では Target Classic HTTP API を使用していましたが、現在は非推奨になっています。
* Adobe Target の `mbox.js` バージョン 63 が含まれています。Adobeでは、実装を `at.js` v1.x.
* `at.js` バージョン 1.5.0 が含まれるようになりました。[Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) を使用して `at.js` 1.x をサイトにプロビジョ二ングすることをお勧めします。

#### AEM と Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 が含まれています。実装を `AppMeasurement.js` に切り替えることをお勧めします。
* `AppMeasurement.js` v1.8.0 が含まれています。Adobeでは、 [Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html) を使用して、AppMeasurement.js をサイトにプロビジョニングします。

#### AEM と Commerce {#aem-commerce}

AEM 6.4 以降、コマース統合フレームワークの改善のリリースサイクルが早くなりました。詳しくは[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html)を参照してください。

#### Communities アドオン {#communities-add-on}

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md)の節を参照してください。

##### コミュニティエンゲージメントの強化 {#enhancements-to-community-engagement}

**@メンションのサポート**
AEM Communities では、登録ユーザーがユーザー生成コンテンツで他の登録メンバーをタグ付け（メンション）して注意を引くことができるようになりました。タグ付け（メンション）されたメンバーには、対応するユーザー生成コンテンツへのディープリンクが付いた通知が届きます。ただし、ユーザーは web とメールでの通知を無効にしたり有効にしたりすることができます。

![@メンションのサポート](/help/release-notes/assets/at-mentions.png)

コミュニティユーザーは、姓、名またはユーザー名を検索して、誰かが自分に連絡を取ったか、注意を払う必要があるかを確認する必要はありません。 さらに、UGC 作成者は、問題に最もうまく対処し入力を追加できる特定の登録ユーザーからの応答を探すことができます。

コミュニティ管理者は、コミュニティコンポーネントで&#x200B;**メンションを有効化**&#x200B;して、これらのコンポーネントの機能を登録ユーザーが使用できるようにする必要があります。

**グループメッセージ送信**

コミュニティの登録メンバーは、同じメッセージをグループメンバーに個々に送信するのではなく、1 回の電子メール作成でダイレクトメッセージをグループに一括送信できるようになりました。[グループメッセージング](/help/communities/configure-messaging.md)を許可する には、[Messaging Operations Service](/help/communities/messaging.md#group-messaging) の両方のインスタンスを有効にします。

![グループメッセージ](/help/release-notes/assets/group-messaging.png)

##### 一括モデレートの機能強化 {#enhancements-to-bulk-moderation}

一括モデレートのカスタムフィルター

[カスタムフィルター](/help/communities/moderation.md#custom-filters) が開発され、一括モデレート UI に追加できるようになりました。

A [サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) これは、タグを介したフィルタリングを示しています。 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). このプロジェクトをベースに、類似のスタムフィルターを開発できます。

![カスタムフィルター](/help/release-notes/assets/custom-tag-filter.png)

**一括モデレートのリスト表示**

UI が改善された新しいリスト表示が一括モデレートに提供され、ユーザ生成コンテンツエントリを表示できるようになりました。

![リスト表示での一括モデレート](/help/release-notes/assets/list-view-moderation.png)

##### サイトおよびグループ管理の機能強化 {#enhancements-to-site-and-group-management}

**作成者側のサイトおよびグループ管理者**

AEM 6.5 以降の Communities では、様々なコミュニティサイトやグループ／ネストされたグループの分散管理が可能です。複数のコミュニティサイトやネストされたグループをホストしている組織では、サイト（およびグループ）の作成時に作成者側で管理者ロールのメンバーを選択できるようになりました。

![サイト管理者](/help/release-notes/assets/site-admin.png)

サイト管理者は、任意の階層レベルにグループを作成でき、それらのデフォルトの管理者になります。これらの管理者は、後で他のグループの管理者によって削除することができます。グループ管理者はグループ G1 を管理し、G1 内にネストしたサブグループを作成することができます。

##### イネーブルメントの機能強化 {#enhancements-to-enablement}

**SCORM 2017.1 のサポート**

AEM 6.5 Communities のイネーブルメント機能は、Shareable Content Object Reference Model[（SCORM）2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) エンジンに対応しています。

* イネーブルメントコンポーネントでのキーボードナビゲーションのサポート
* AEM Communities のイネーブルメントコンポーネント（カタログやコース再生、割り当て、ファイルライブラリなど）では、アクセシビリティを向上させるためにキーボードナビゲーションをサポートしています。

##### その他の機能強化 {#other-enhancements}

* Solr 7 のサポート
* AEM 6.5 Communities では、MSRP と DSRP の設定時に、Apache Solr 7.0 バージョンの検索プラットフォームをサポートしています。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 には、AEM ユーザー、DAM ロール、および関連するクリエイティブおよびマーケティングロールの生産性を高めるため、以下の機能および機能強化が導入されています。

#### [!DNL Adobe Creative Cloud] との統合およびクリエイティブワークフロー {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] は、クリエイティブチームとマーケティングチームやビジネスチームが密接に連携できるように、[!DNL Adobe Creative Cloud] と統合して、ワークフローで使用するアセットを共有する様々な方法を提供します。[!DNL Experience Manager] 6.5 では統合を継続的に改善し効率化して、より多くのチャンスを明らかにし、既存の手段の無駄も省きます。

コンテンツ速度のユースケースを最適にサポートできる、[!DNL Experience Manager] 6.5の具体的な機能と統合について説明します。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] を使用すると、コンテンツ作成プロセスでのクリエイティブ担当者とマーケティング担当者のコラボレーションを強化できます。クリエイティブ担当者は、使い慣れたアプリを離れることなく、[!DNL Experience Manager Assets] に保存されているコンテンツにアクセスできます。[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]、[!DNL Adobe InDesign] などのアプリ内のパネルを使用して、アセットをシームレスに参照、検索、チェックアウトおよびチェックインすることもできます。

[!DNL Adobe Asset Link] は、[Creative Cloud エンタープライズ版](https://www.adobe.com/creativecloud/business/enterprise.html)に含まれています。[!DNL Experience Manager] デプロイメントの必要な設定など、詳しくは、[Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html?lang=ja) を参照してください。

![Adobe Photoshop でのアセットの検索](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] の統合 {#stock}

組織では、[!DNL Experience Manager Assets] 内で [!DNL Adobe Stock] エンタープライズ版プランを使用して、ライセンスを受けたアセットをクリエイティブおよびマーケティングプロジェクトで幅広く利用できます。[!DNL Experience Manager] の強力な DAM 機能を使用して、Experience Manager に保存されている [!DNL Adobe Stock] アセットをすばやく検索、プレビュー、ライセンス取得することができます。

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、何百万点もの質の高い選ばれた著作権使用料不要の写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。

詳しくは、[Experience Manager Assets での Adobe Stock アセットの使用](/help/assets/aem-assets-adobe-stock.md)を参照してください。

![Experience Manager Assets 内での Adobe Stock 画像およびライセンスのプレビュー](/help/release-notes/assets/stock_image_preview_license_options.png)

*図：[!DNL Experience Manager Assets] 内での [!DNL Adobe Stock] 画像およびライセンスのプレビュー。*

![Experience Manager でのライセンス取得済み Adobe Stock 画像の検索とフィルタリング](/help/release-notes/assets/aem-search-filters2.jpg)

*図：[!DNL Experience Manager] でのライセンス取得済み [!DNL Adobe Stock] 画像の検索とフィルタリング。*

##### [!DNL Adobe InDesign] での動的な参照 {#dynamic-references-in-indesign}

[!DNL Adobe InDesign] ファイルで使用される [!DNL Experience Manager Assets] は動的です。参照先アセットがリポジトリ内で移動すると、参照が自動的に更新されます。詳しくは、[複合アセットの管理方法](/help/assets/managing-linked-subassets.md)を参照してください。

#### Brand Portal の機能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] を利用すると、外部のベンダーや代理店、内部のビジネスユーザーに対して、承認されたアセットをデバイス間で簡単に取得し、効果的に制御し、安全に配布することができます。アセットの共有を効率化し、アセットを市場に投入するまでの時間を短縮し、コンプライアンスに違反した使用や不正アクセスのリスクをなくすことができます。

詳しくは、[Brand Portal の新機能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja)を参照してください。

#### Connected Assets {#connectedassets}

大規模企業では、Web サイトの作成に必要なインフラストラクチャを分散させることができます。しかし、Web サイトの作成機能と必要なデジタルアセットが、分断させた状態で別々の場所に存在する場合があります。

[!DNL Experience Manager Sites] は、web ページの作成機能を備えています。[!DNL Experience Manager Assets] は Web サイトに必要なアセットを提供するデジタルアセット管理（DAM）システムです。[!DNL Experience Manager] では、[!DNL Sites] と [!DNL Assets] の統合により、上記のユースケースをサポートできるようになりました。詳しくは、[Connected Assets の機能の設定方法と使用方法](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。

![[!DNL Experience Manager] デプロイメントから別の [!DNL Experience Manager] デプロイメントの [!DNL Sites] ページにアセットをドラッグ](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*図：[!DNL Experience Manager] デプロイメントから別の [!DNL Experience Manager] デプロイメントの [!DNL Sites] ページにアセットをドラッグ。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] を利用すると、リッチメディアのオーサリングと配信が [!DNL Experience Manager Assets] で強化され、臨場感あふれるパーソナライズされた最先端のエクスペリエンスを促進できます。高品質な主力のアセットを 1 つアップロードし、アドビの高度なクラウドレンダリングとビューアを使用することで、あらゆる組み合わせの演出をその場で提供することができ、お客様のメディア戦略をサポートします。

新しい [!DNL Dynamic Media] 機能について詳しくは、[Dynamic Media のリリースノート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html?lang=ja-JP)を参照してください。

##### 360 ビデオのサポート {#video-support}

最先端ビューアを使用してデスクトップ、モバイルおよび VR ヘットセットに VR エクスペリエンスを提供することで、360 度ビデオのファイルを [!DNL Experience Manager] で直接管理できます。詳しくは、[360 度ビデオ の使用](/help/assets/360-video.md)を参照してください。

##### カスタムビデオのサムネール {#custom-video-thumbnails}

ビデオアセットのサムネールをカスタマイズするために、ビデオそのものまたは DAM に保存されている他のコンテンツのフレームを使用できるようになりました。詳しくは、[ビデオのサムネールについて](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)を参照してください。

##### アクセシビリティの強化 {#accessibility-enhancements}

[!DNL Dynamic Media] ビューアでは、Aria フォントのサポート、スクリーンリーダー、代替テキストなどの拡張アクセシビリティ機能をサポートするようになりました。詳しくは、[ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=ja-JP)を参照してください。

#### 検索エクスペリエンスの強化 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5 以降では、マーケティング担当者が検索結果ページから目的のアセットをすばやく見つけることができます。検索ファセットのアセット数は、検索フィルターを適用する前でも更新されます。フィルターに対するアセット数を確認すると、検索結果を効率的にナビゲートすることができます。詳しくは、[Experience Manager でのアセットの検索](/help/assets/search-assets.md)を参照してください。

![検索ファセットで検索結果をフィルタリングしない場合のアセット数の表示](/help/assets/assets/asset_search_results_in_facets_filters.png)

*図：検索ファセットで検索結果をフィルタリングしない場合のアセット数の表示。*

#### 使いやすさの向上 {#usability-enhancement}

フォルダー内または検索結果から読み込まれたすべてのアセットをすべて選択できるようになりました。複数のアセットをすばやく管理するのに役立ちます。チェックボックスをオンにすると、[!DNL Experience Manager] インターフェイスに表示されるアセットだけでなく、シナリオに合致するすべてのアセット（検索結果）が選択されます。

![「すべてを選択」オプションを使用して、読み込まれたすべてのアセットをワンクリックで選択](/help/release-notes/assets/select-all-in-aem-assets.gif)

*図：「すべてを選択」オプションを使用して、読み込まれたすべてのアセットをワンクリックで選択。*

#### メタデータの機能強化 {#metadata-enhancements}

[!DNL Assets] では、アセットフォルダーのメタデータスキーマを作成できます。これにより、フォルダープロパティのページに表示されるレイアウトとメタデータを定義します、フォルダーのメタデータスキーマを既存のフォルダーまたは作成するフォルダーに割り当てることができるようになりました。詳しくは、](/help/assets/metadata-config.md#folder-metadata-schema)フォルダーメタデータスキーマ[を参照してください。

カスケードメタデータを指定すると、選択肢をフォームに手動で入力するのではなく、実行時に JSON ファイルから読み込むことができます。詳しくは、[カスケードメタデータ](/help/assets/metadata-schemas.md#cascading-metadata)を参照してください。

#### レポート機能の強化 {#reporting-enhancements}

ダウンロードされたレポートに、コンテンツフラグメントとリンク共有が含まれるようになりました。詳しくは、[AEM Assets レポート](/help/assets/asset-reports.md)を参照してください。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Formsには、いくつかの新機能および機能強化が含まれています。 主なものは次のとおりです。

* 送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を追跡できるトランザクションレポート
* インタラクティブコミュニケーションのユーザビリティの向上
* アダプティブフォームでのクラウドベースの電子署名
* AEM Sitesシングルページアプリケーション (SPA) にアダプティブフォームとインタラクティブ通信を埋め込む。
* AEM ワークフローでの変数のサポート
* インタラクティブコミュニケーションでのデータ表示パターンのサポート
* アダプティブフォームおよびインタラクティブコミュニケーションテーブルの並べ替え
* フォームデータモデルでの入力データの自動検証

新機能や機能強化、ドキュメントのリソースについては、[AEM 6.5 Forms の新機能および機能強化の概要](/help/forms/using/whats-new.md)を参照してください。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

使用している AEM 6.5 インスタンスを Livefyre と統合できます。詳しくは、[Livefyre と AEM を統合する方法](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html?lang=ja-JP)を参照してください。

### 顧客中心の開発を使用 {#leverage-customer-focused-development}

Adobeは、お客様が仕様、開発、およびテスト中に開発プロセスのすべての段階に貢献できる、お客様中心の開発モデルを使用しています。 このプロセスで貢献しているすべてのお客様およびパートナーに感謝します。

Adobeには、お客様中心のバグ解決と拡張リクエストの開発の収集、優先順位付け、追跡を可能にする手順とプロセスが用意されています。 [Experience Manager サポート ポータル](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support)は、アドビの機能強化および欠陥追跡システムと統合されています。お客様からの問い合わせは、可能であれば、カスタマーサポートチームで特定して解決します。研究開発部門にエスカレートされた場合は、お客様の情報をすべて収集して、優先順位付けとレポートに使用します。開発では有償のサポート、保証の問題、有償の顧客向け強化機能が優先されます。

この優先順位付けのプロセスにより、AEM 6.5 では 750 件を超えるお客様中心の変更がおこなわれました。

## このリリースに含まれるファイルのリスト {#list-of-files-that-are-part-of-the-release}

**基盤**

* スタンドアロンのクイックスタート： `cq-quickstart-6.5.0.jar`。
* アプリケーションサーバーのクイックスタート：`cq-quickstart-6.5.0.war`。
* 様々な web サーバーとプラットフォーム向けの Dispatcher 4.3.2 以降。[ダウンロードリンク](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=ja-JP)を参照してください。
* Eclipse IDE 用プラグイン（[詳細およびダウンロード](/help/sites-developing/aem-eclipse.md)）

* Brackets コードエディターの拡張機能（[詳細およびダウンロード](/help/sites-developing/aem-brackets.md)）
* Maven／Gradle の依存関係（[ダウンロードリンク](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**Sites**

* コアコンポーネント（[GitHub プロジェクト](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail 参照実装（[詳細](/help/sites-developing/we-retail.md)）
* Maven プロジェクトアーキタイプ：

   * フルスタックサイトの場合：[GitHub プロジェクト](https://github.com/adobe/aem-project-archetype)
   * React または Angular を使用した単一ページアプリの場合：[GitHub プロジェクト](https://github.com/adobe/aem-spa-project-archetype)

* 様々なプラットフォーム向けの AEM Screens Players（[ダウンロード](https://download.macromedia.com/screens/)）

* スマートコンテンツの言語モデル。英語がプレインストールされています。他の言語もダウンロードできます。

   * [ドイツ語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [スペイン語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [イタリア語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [フランス語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite（ダイアログ変換ツールなど） （[GitHub プロジェクト](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 強化された PDF Rasterizer を追加するためのパッケージ（[詳細](/help/assets/aem-pdf-rasterizer.md)）
* 強化された RAW 画像のサポートを追加するためのパッケージ（[詳細](/help/assets/camera-raw.md)）

**Forms**

* [AEM Forms の機能パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)
* [AEM Forms OSGi Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 言語 {#languages}

次の言語のユーザーインターフェイスが使用できます。

* 英語
* ドイツ語
* フランス語
* スペイン語
* イタリア語
* ポルトガル語（ブラジル）
* 日本語
* 簡体字中国語
* 繁体字中国語（限定的にサポート）
* 韓国語

[!DNL Experience Manager] 6.5 は、中国語エンコーディング規格の使用に関する GB18030-2005 CITS の認定を受けています。

## インストールとアップデート {#install-update}

設定要件について詳しくは、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

手順について詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

サポートしているプラットフォーム（サポートレベルを含む）の完全な一覧表は、[AEM 6.5 の技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

>[!NOTE]
>
>Oracleは、OracleJava™ SE 製品の長期サポート (LTS) モデルに移行しました。 Java™ 9 と 10 は非 LTS リリースで、Oracle別。詳しくは、 [OracleJava™ SE サポート・ロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html). AdobeはAEMを実稼動環境でのみ実行するために、Java™の LTS リリースをサポートしています。 AEM 6.5 で使用する場合は、Java™ 11 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

Adobeは、製品の機能を絶えず評価し、機能をより強力なバージョンに置き換える予定や、将来の期待や拡張に備えるために、選択したパーツの再実装を決定しています。

[!DNL Adobe Experience Manager] 6.5 については、[廃止される機能および削除された機能のリスト](/help/release-notes/deprecated-removed-features.md)を参照してください。このページには、将来の変更に関する事前発表と、以前のリリースから更新するお客様向けの重要なお知らせも含まれています。

## 既知の問題 {#known-issues}

### Platform {#platform}

* CRX-Quickstart とその内容が削除された場所に問題が報告されます。

   次の各アクションで、プロパティ `htmllibmanager.fileSystemOutputCacheLocation` が空の文字列ではありません。

   1. `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true` の呼び出し。
   2. AEM 6.5 へのアップグレード。
   3. AEM 6.5 での「遅延コンテンツ移行」の実行。

   [ナレッジベース](https://helpx.adobe.com/jp/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)の記事には、この問題の詳細と回避策が記載されています。

* AEM 6.5 インスタンスで JDK 11 を使用している場合、一部のパッケージをデプロイすると、一部のページが空白で表示されることがあります。次のエラーメッセージがログファイルに表示されます。

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

このエラーを解決するには：

1. AEM インスタンスを停止します。`<aem_server_path_on_server>crx-quickstart\conf` に移動し、`sling.properties` ファイルを開きます。アドビでは、このファイルのバックアップを取っておくことをお勧めします。

1. `org.osgi.framework.bootdelegation=` を検索します。`jdk.internal.reflect,jdk.internal.reflect.*` プロパティを追加して、結果を次のように表示します。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. ファイルを保存し、AEM インスタンスを再起動します。

### Sites {#sites}

* **ページバージョンの処理**：[ページを移動すると、移動前に作成したバージョンのプレビューを実行できなくなります。](/help/sites-authoring/working-with-page-versions.md#previewing-a-version)

### Assets {#assets}

* **検索：** 検索文字列の先頭にスペース ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

### Forms {#forms}

* AEM Formsを Linux®オペレーティングシステムにインストールすると、ハードウェアセキュリティモジュールを使用したデジタル署名が機能しない。 （CQ-4266721）
* (AEM Forms on WebSphere®のみ ) **Forms Workflow** > **タスク検索** オプションを指定すると、 **管理者** と **ユーザー名** を検索条件として使用します。 （CQ-4266457）

* AEM Formsが、JPEG圧縮を含む TIF およびTIFFファイルをPDFドキュメントに変換できない。 （CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* (JBoss® 7 のみ ) 以前のバージョンからAEM 6.5 Formsにアップグレードし、デフォルトの送信プロセスまたはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス (.lca) がある場合、そのようなプロセス (.lca) を使用するHTML5 Formsは必要なアクションを実行できません。 （CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer インストーラーを実行するには、32 ビット版の [Visual C++ 再頒布可能ランタイムパッケージ 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) と [Visual C++ 再頒布可能ランタイムパッケージ 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1) が必要です。インストールを開始する前に、前述の再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* PDF ジェネレーターは、スマートカードベースの認証をサポートしていません。管理者が Windows サーバーでグループポリシー `Interactive Logon: Require Smart card` を有効にすると、既存のすべての PDF Generator のユーザーが無効になります。

* Dispatcher を通じて、フォームをホストするコンポーネントおよびパブリッシュインスタンスの値を動的に更新するようにアダプティブフォームを設定すると、フィールドの値を動的に更新する機能が動作しなくなります。 この問題を解決するには、パブリッシュインスタンスで CRXDE を開き、`/libs/fd/af/runtime/clientlibs/guideChartReducer` を検索して、次のプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

* AEM Forms を起動すると、`SAX Security Manager could not be setup` 警告が表示されます。
* Apple iOSまたはAdobe Acrobat Reader 20.10.00を実行している iPadOS で、AEM Forms Document Security で保護されたPDFを開くとき
* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 では、この問題を修正しています。

## 製品のダウンロードとサポート（制限付きサイト） {#product-download-and-support-restricted-sites}

以下のサイトは、お客様のみが利用できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/)。

* 製品の追加機能に関する[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上のアップデート、パッチ、パッケージ。

* [Admin Console 経由でのカスタマーサポート](https://adminconsole.adobe.com/)。詳しくは、[新しいアドビカスタマーサポートエクスペリエンス](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)を参照してください。
