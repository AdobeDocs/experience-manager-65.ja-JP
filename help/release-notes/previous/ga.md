---
title: 一般リリースノート： [!DNL Adobe Experience Manager] 6.5
description: '[!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能情報、インストール方法および詳細な変更リストが記載されています。'
source-git-commit: 9b15215a68495a800e94a58b523e1b7baa0c0203
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 57%

---

# 一般リリースノート： [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 |
| 種類 | メジャーリリース |
| 正式版の日付 | 2019年4月8日（PT） |
| 推奨されるアップデート | 詳しくは、 [AEM最新の更新](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html). |

### 参考情報 {#trivia}

このバージョンののリリースサイクル [!DNL Adobe Experience Manager] 2018 年 4 月 4 日に開始し、23 回の品質保証とバグ修正を繰り返し、2019 年 3 月 28 日に終了しました。 このリリースで修正された、機能強化と新機能を含むお客様関連の問題の総数は 1345 件です。   

[!DNL Adobe Experience Manager] 6.5 は 2019 年 4 月 8 日より一般に提供されています。

![AEM 6.5 ログイン画面](/help/assets/assets/aem65-login-v4.png)

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 は、 [!DNL Adobe Experience Manager] 6.4 コードベース。 新機能および強化機能、お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、 [!DNL Adobe Experience Manager] 6.4 Service Pack は、SP4 までのリリースです。

以下のリストでは概要を説明します。その後のページでは詳細を示します。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

のプラットフォーム [!DNL Adobe Experience Manager] 6.5 OSGi ベースのフレームワーク（Apache Sling および Apache Felix）の更新バージョンと Java コンテンツリポジトリの上に構築：Apache Jackrabbit Oak 1.10.2.

Quickstart は、サーブレットエンジンとして Eclipse Jetty 9.4.15 を使用します。

#### Java サポート  {#java-support}

* 既にサポートされている Java 8 に加えて、Java 11 を新しくサポートします。。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、 [インストールと更新](/help/sites-deploying/custom-standalone-install.md) 」セクションに入力します。
* Java 11 および Java 8 のメンテナンスアップデートは、Adobeから一般公開されていない場合、AEM関連プロジェクトでのお客様向けの使用を目的として、Oracle別に配布されます。

#### Java の開発 {#java-development}

* 現在 [Uberjar の 2 つのバージョン](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)：非推奨とマークされていないパブリックインターフェイスを含む推奨バージョン、および非推奨とマークされたインターフェイスを含むバージョン。

#### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* ユーザーおよびグループ用の新しい権限管理 UI。
* 列表示では、画面上に表示されるエントリのみを読み込み、それ以外のエントリはユーザーがスクロールを開始した場合にのみ読み込まれるようになりました。リストおよびカード表示では、AEM 6.0 以降、この機能が既に実装されています（AEM 6.4 で改善されました）。。
* 列表示に、該当する場合、ページ/アセットのワークフローステータスが含まれるようになりました。
* この [すべてを選択](/help/sites-authoring/basic-handling.md#select-all) 「 」アクションを使用すると、同じフォルダー内のすべてのページ/アセットに対してアクションをすばやく実行できます。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションは、読み込まれたページ／アセットだけでなく、すべてのページ／アセットに対してアクションを実行しようとします。アクションがバルクアクションを処理するようにアップグレードされていない場合、警告ダイアログが表示されます。

>[!CAUTION]
>
>クラシック UI の機能がさらに強化される予定はありません。AEM 6.5 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は廃止中は引き続き完全にサポートされます。[詳細情報](/help/sites-deploying/ui-recommendations.md)。

#### 検索およびインデックス作成 {#indexing-and-search}

* Oak 内の検索では動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールには、結果の推定量が表示されます。
* 結果に動的ファセットを提供するように QueryBuilder が拡張されました。

#### アップグレード {#upgrade}

* AEM 6.5 への直接インプレースアップグレードは、AEM 6.2、6.3、6.4 を使用しているお客様に対してサポートされています。5.x または 6.0／6.1 を使用しているお客様がインプレースアップグレードを使用するには、まず 6.4 にアップグレードした後、6.5 にアップグレードするか、インスタンス間のコンテンツの転送を通じて AEM 6.5 に直接アップグレードする必要があります。
* アップグレード手順は 6.5 でもほぼ変わりません。
* 6.4 で導入された下位互換性、アップグレードの複雑さの評価、持続可能なアップグレードの機能を引き続きサポートしています。必要に応じて、これらの分野でバージョン固有の更新がおこなわれてきました。
* パターン検出パッケージが簡素化され、利用可能なソースバージョンごとに、6.5 へのアップグレードを評価するパッケージが 1 つ用意されるようになりました。
* アップグレード手順の詳細については、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md).

#### プロジェクトとワークフロー {#projects-and-workflows}

* 6.4 で導入された新しいワークフローモデルエディターが改善され、コピーや公開などの操作、ワークフローステップでの変数のサポート、機能強化が追加されました。 `OR` および `AND` 分割。

#### リポジトリ {#repository}

* Adobe Experience Manager 6.5 の基盤は、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java コンテンツリポジトリの Apache Jackrabbit Oak 1.10.2 上に構築されています。
* 修正された問題の概要については、 [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) および [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>AEM 6.3 以降の新しいバージョンの Oak セグメント Tar では、リポジトリを移行する必要があります。この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。

#### OSGi {#osgi}

* OSGi Promises および Converter ユーティリティライブラリが追加されました。

#### セキュリティ {#security}

* 管理者ユーザーのパスワードの有効期限が追加されました。

#### Web サーバー {#web-server}

* クイックスタートの配布では、Eclipse Jetty 9.4.15 をサーブレットエンジンとして使用します (AEM 6.4 は 9.3.22 に付属しています )。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 管理された単一ページアプリ {#managed-single-page-apps}

ページエディターでは、コンテンツのコンテキスト内編集と、レンダリングされたクライアント側エクスペリエンス内での作成／レイアウトの機能が追加されました（[SPA エディター](/help/sites-developing/spa-architecture.md)とも呼ばれます）。JavaScript フレームワークの React または Angular を使用して作成された既存の単一ページアプリを、AEM SJ SDK を使用して拡張することで、お客様による編集が可能になります。

SPA のサポートは AEM 6.4 SP2 の一部として導入されたものですが、AEM 6.5 ではさらに以下が可能になりました。

* テンプレートエディターを使用して、AEM で編集可能な SPA の部分を編集および設定できます。
* マルチサイト管理を使用して、国、フランチャイズまたはホワイトラベルの付いたSPAエクスペリエンスを作成する

#### ヘッドレスコンテンツ管理 {#headless-content-management}

AEM では、様々な形式で様々なスタックレベルからコンテンツを提供できます。一部は、2008 年以降、](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)Sling GET[ および ](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)POST Servlet[ で機能しています。コンテンツサービス（[Sling Model エクスポーター](https://docs.adobe.com/content/help/ja-JP/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)）は AEM 6.3 で導入されたもので、AEM SJ SDK で単一ページアプリの改善に使用されている方法です。[HTTP API for Assets](/help/assets/mac-api-assets.md) は、AEM 6.5 向けに拡張された CRUD API です。

新しい HTTP API 機能：

* [HTTP API for Assets でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになり、フラグメントの作成、更新、読み取り、削除が可能になりました。
* [コンテンツフラグメントリストのコアコンポーネント](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)でコンテンツサービスを通じてコンテンツフラグメントのリストを公開します。
* コンポーネントごとにコンテンツサービスのデフォルト JSON 出力を表示する[コアコンポーネントライブラリ](https://opensource.adobe.com/aem-core-wcm-components/library.html)

#### Screens アドオン {#screens-add-on}

インタラクティブなキオスク端末からデジタルサイネージに至るまで、あらゆるデジタル表示でのエクスペリエンスを効率良くデザイン、配信、最適化します。

* コンテンツ再利用の向上により、デジタルと実店舗の区別なくエクスペリエンスとコンテンツを統一できます。
* ローンチのサポートにより、オーサリングおよび承認／公開ワークフローを効率化します。
* SPA エディターを使用して、機能豊富でインタラクティブなエクスペリエンスを編集および配信できます。
* ローンチを使用したサイネージコンテンツの将来のコンテンツ変更の計画
* シーケンスチャンネルでのメーター制再生が可能になりました。
* Excel シートなどのソースファイルを使用してプロジェクト構造を自動作成する
* 堅牢なオンラインおよびオフライン操作（スマート同期）が追加されてメディアプレイヤーのサポートが強化され、大規模なサイネージネットワークにも対応できるようになりました。
* 動的プレースホルダーを使用して、データでトリガーされるコンテンツの場所または設定別にパーソナライズできます。
* Adobe Analytics と AEM Screens Player の連携でインサイトの統合が促進されます。

AEM Screensの変更点について詳しくは、 [AEM Screens User Guide](https://docs.adobe.com/content/help/ja/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### コンポーネントとテンプレートの開発 {#component-amp-template-development}

* 新規プロジェクト用の Maven プロジェクトアーキタイプ 18 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases) を参照）。
* 新規プロジェクト用の単一ページアプリ Maven プロジェクトアーキタイプ 1.0.6 以上（[リリースノートの GitHub](https://github.com/adobe/aem-spa-project-archetype/releases) を参照）。
* HTL バージョン 1.4（[リリースノートの GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4) を参照）。

   * 文字列、配列およびオブジェクトに対する&quot;in&quot;演算子

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * data-sly-set を使用した変数宣言：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 次の制御パラメータをリストし、繰り返します。開始、ステップ、終了：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap の識別子：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 負の数のサポート

* コアコンポーネント 2.3.2 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照）。
* レイアウトコンテナのグリッドシステム（[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照）。
* Clientlib マネージャ：Google Closure Compiler をデフォルトで JavaScript clientlibs の縮小（古いデフォルトは Yahoo YUI）に設定し、Google Closure Compiler をバージョンv20190121に更新しました。
* テンプレートエディターとポリシー

   * JS SDK(SPA Editor とも呼ばれます ) を使用するシングルページアプリ用のテンプレートを作成および編集します

* 参照サイト We.Retail 4.0（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照）。
* 既存のサイトをアップグレードして最新のエディター機能を利用するためのツールキットについては、 [GitHub リポジトリ](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEMには、既存のカスタムコードとの互換性を最大限に高めるために、jQuery ライブラリのバージョン1.12.4が含まれています。 セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

#### サイト管理 {#site-administration}

* [参照](/help/sites-authoring/author-environment-tools.md#references)レールには、選択したページを参照する内部リンクを一覧表示する新しいセクションがあります。これは、ページをオフラインで取得したり削除することが想定される場合や、オフラインで取得する前に調整する必要があるページを確認する場合に便利です。
* [リスト表示](/help/sites-authoring/basic-handling.md#list-view)には、ページが現在ワークフローに含まれている場合にステータスを表示する新しいワークフロー列があります。
* [ページのプロパティ](/help/sites-authoring/editing-page-properties.md)で、ページにサムネールを割り当てるときに既存のアセットを参照できるようになりました（「サムネール」タブ）。

#### ページエディター {#page-editor}

* JS SDK を利用する React および Angular クライアント側コンポーネントで構築された単一ページアプリエクスペリエンスのコンテキスト内編集および作成が可能になりました（SPA エディターとも呼ばれます）。
* 基礎モードは、ページに基礎モードが設定されている場合にのみ表示されます。

#### コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* 全般的なコメントを書き込んだり、テキスト内のコメントを表示（タイムラインレールにも表示）するための新しい[注釈](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)レールがコンテンツフラグメントエディターに追加されました。
* 複数行テキスト要素のデフォルトコンテンツタイプを [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md) シンプルテキスト、リッチテキストまたは Markdown に
* RTE（フルスクリーン表示）でテキストを選択して、[コメント／注釈](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)を追加できます。
* 参照レールでコンテンツフラグメント並列に表示して、[バージョンを比較](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)できるようになりました。
* アセットのダウンロードレポートにコンテンツフラグメントが適宜表示されるようになりました。
* /api.json を通じて、[Assets HTTP API でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになりました。コンテンツフラグメントの作成、更新、読み取りおよび削除のための API が用意されています。

#### エクスペリエンスフラグメント {#experience-fragments}

* [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)のインデックス作成を改善して、フラグメントの使用ページの検索でコンテンツが見つかるようになりました。
* 「[Adobe Target に書き出し](/help/sites-administering/experience-fragments-target.md)」オプションで、エクスペリエンスフラグメントを JSON（デフォルトは HTML）またはその両方として送信できるようになりました。

#### 翻訳 {#translation}

* プロジェクトマスターを使用して、翻訳プロジェクトを手軽に作成できます。
* 翻訳ジョブをデフォルトで承認済みステータスに設定することで、翻訳プロジェクトの実行を簡略化できます
* サードパーティ翻訳メモリの変更点に合わせて翻訳済みページを更新できます。
* 翻訳ジョブを JSON 形式で書き出すことができます。
* V3 API を使用するためのMicrosoft Translation 統合の更新

#### マルチサイト管理（MSM） {#multi-site-management-msm}

* PushOnModify を使用するロールアウト設定の場合、ページ移動操作の処理を改善し、状態の不整合を防ぎます。
* ライブコピー構造内に新しいページを作成すると、デフォルトでスタンドアロンページが作成されるようになりました。
* JS SDK(SPA Editor とも呼ばれます ) を使用しているシングルページアプリで MSM 機能を使用する

#### ローンチ {#launches}

* ローンチの新しいレビューおよび承認ワークフローと、承認済みのローンチページのみ昇格させる機能が追加されました。
* [プロモーションステップの直後にローンチを削除するオプションが UI に追加](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)されました。

#### コンテンツのターゲット設定とシミュレーション {#content-targeting-simulation}

* ContextHub データレイヤーおよびクライアント側ルールエンジンの JavaScript が更新され、jQuery 3 をデフォルトで使用するようになりました。

#### AEMとAdobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>現在：
>
>* のみ `at.js 1.x` は、AEM Activities コンソール内でAdobe Targetをターゲティングエンジンとして使用している場合にサポートされます。
>
>* 両方 `at.js. 1.x` および `at.js 2.x` は、エクスペリエンスフラグメントの Target への書き出しを使用し、Target のコンソール内でアクティビティを実行する場合にサポートされます。


* Adobe Target との連携で Target Standard API を使用できるようになりました。以前のバージョンのAEMでは、現在は非推奨（廃止予定）となっていた Target Classic HTTP API を使用していました。
* Adobe Target `mbox.js` バージョン 63 が含まれています。 Adobeでは、実装をに切り替えることを強くお勧めします。 `at.js` v1.x.
* `at.js` バージョン 1.5.0 が含まれるようになりました。 Adobeでは、 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) 規定を設ける `at.js` v1.x をサイトに挿入します。

#### AEMとAdobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 が含まれています。 Adobeでは、実装をに切り替えることをお勧めします。 `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 が含まれています。 Adobeでは、 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) を使用して、AppMeasurement.js をサイトにプロビジョニングします。

#### AEM and Commerce {#aem-commerce}

Commerce Integration Framework の改善は、AEM 6.4 以降、より迅速なリリースサイクルに入っています。 [詳細情報](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Communities アドオン {#communities-add-on}

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md)の節を参照してください。

##### コミュニティエンゲージメントの強化 {#enhancements-to-community-engagement}

**@Mentions support**
AEM Communitiesでは、ユーザー生成コンテンツで、登録ユーザーが他の登録済みメンバーにタグ付け（メンション）して、注意を引くことができるようになりました。 タグ付け（メンション）されたメンバーには、対応するユーザー生成コンテンツへのディープリンクが付いた通知が届きます。ただし、Web および電子メール通知の無効化/有効化はオプトインできます。

![@メンションのサポート](/help/release-notes/assets/at-mentions.png)

コミュニティユーザーは、自分の名、姓またはユーザー名を検索しなくても、誰かが自分に接触してきたかどうか、または誰かが自分の注意を引く必要があるのかどうかを確認することができます。さらに、UGC 作成者は、問題に最もうまく対処し入力を追加できる特定の登録ユーザーからの応答を探すことができます。

コミュニティ管理者は、 **メンションを有効にする** コミュニティコンポーネントでは、登録ユーザーがこれらのコンポーネントの機能を使用できるようにします。

**グループメッセージ送信**

コミュニティの登録メンバーは、同じメッセージをグループメンバーに個々に送信するのではなく、1 回の電子メール作成でダイレクトメッセージをグループに一括送信できるようになりました。許可する手順は次のとおりです。 [グループメッセージ](/help/communities/configure-messaging.md)、 [メッセージング操作サービス](/help/communities/messaging.md#group-messaging).

![グループメッセージ](/help/release-notes/assets/group-messaging.png)

##### 一括モデレートの機能強化 {#enhancements-to-bulk-moderation}

一括モデレートのカスタムフィルター

[カスタムフィルター](/help/communities/moderation.md#custom-filters) が開発され、一括モデレート UI に追加できるようになりました。

タグによるフィルタリングの例を示す[サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)を ](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)GitHub [ で入手できます。このプロジェクトをベースに、類似のスタムフィルターを開発できます。

![カスタムフィルター](/help/release-notes/assets/custom-tag-filter.png)

**一括モデレートのリスト表示**

UI が改善された新しいリスト表示が一括モデレートに提供され、ユーザ生成コンテンツエントリを表示できるようになりました。

![リスト表示での一括モデレート](/help/release-notes/assets/list-view-moderation.png)

##### サイトおよびグループ管理の機能強化 {#enhancements-to-site-and-group-management}

**作成者側のサイトおよびグループ管理者**

AEM 6.5 以降の Communities では、様々なコミュニティサイトやグループ／ネストされたグループの分散管理が可能です。複数のコミュニティサイトやネストされたグループをホストしている組織では、サイト（およびグループ）の作成時に作成者側で管理者ロールのメンバーを選択できるようになりました。

![サイト管理者](/help/release-notes/assets/site-admin.png)

サイト管理者はデフォルトの管理者になり、任意の階層レベルにグループを作成できます。これらの管理者は、後で他のグループ管理者が削除できます。 グループ管理者はグループ G1 を管理し、G1 内にネストしたサブグループを作成することができます。

##### イネーブルメントの機能強化 {#enhancements-to-enablement}

**SCORM 2017.1 のサポート**

AEM 6.5 Communities のイネーブルメント機能は、共有可能なコンテンツオブジェクト参照モデルをサポートしています [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) エンジン。

* イネーブルメントコンポーネントでのキーボードナビゲーションのサポート
* AEM Communitiesのイネーブルメントコンポーネント（カタログとコースの再生、割り当て、ファイルライブラリなど）は、キーボードナビゲーションをサポートし、アクセシビリティを向上させます。

##### その他の機能強化 {#other-enhancements}

* Solr 7 のサポート
* AEM 6.5 Communities では、MSRP と DSRP の設定時に、Apache Solr 7.0 バージョンの検索プラットフォームをサポートしています。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 には、AEM ユーザー、DAM ロール、および関連するクリエイティブおよびマーケティングロールの生産性を高めるため、以下の機能およびき機能強化が導入されています。

#### との統合 [!DNL Adobe Creative Cloud] とクリエイティブワークフロー {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] では、様々な方法で と連携し、クリエイティブチームとマーケティングチームが密接に共同作業するワークフローでアセットを共有できます。[!DNL Adobe Creative Cloud][!DNL Experience Manager] 6.5 では連携を引き続き改善し効率化して、より多くのチャンスを明らかにし、既存の手段の無駄も省きます。

の特定の機能と統合について説明します。 [!DNL Experience Manager] 6.5 コンテンツベロシティの使用例を最もサポートするために使用できるもの。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] は、コンテンツ作成プロセスでのクリエイティブとマーケターのコラボレーションを強化します。 クリエイティブは、 [!DNL Experience Manager Assets]最も身近なアプリを残すことなく。 クリエイティブは、のアプリ内パネルを使用して、アセットの参照、検索、チェックアウト、チェックインをシームレスにおこなえます。 [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]、および [!DNL Adobe InDesign] アプリ

[!DNL Adobe Asset Link] は、 [Creative Cloud](https://www.adobe.com/jp/creativecloud/business/enterprise.html) 提供 詳しくは、 [!DNL Experience Manager] デプロイメントについては、 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html).

![Adobe Photoshopでのアセットの検索](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] の統合 {#stock}

組織で使用できる [!DNL Adobe Stock] 内部の企業計画 [!DNL Experience Manager Assets] を使用すれば、ライセンスが必要なアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く利用できます。 すばやく検索、プレビュー、ライセンスを取得できます [!DNL Adobe Stock] の強力な DAM 機能を使用してExperience Managerに保存されたアセット [!DNL Experience Manager].

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。

詳しくは、 [Experience Manager AssetsでのAdobe Stock Assets の使用](/help/assets/aem-assets-adobe-stock.md).

![Experience Manager Assets内からAdobe Stockの画像とライセンスをプレビュー](/help/release-notes/assets/stock_image_preview_license_options.png)

*図：プレビュー [!DNL Adobe Stock] 内からの画像とライセンス [!DNL Experience Manager Assets].*

![Experience Managerでライセンス済みのAdobe Stock画像を検索およびフィルタリング](/help/release-notes/assets/aem-search-filters2.jpg)

*図：ライセンスを検索してフィルター [!DNL Adobe Stock] 画像 [!DNL Experience Manager].*

##### の動的参照 [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] 使用される [!DNL Adobe InDesign] ファイルは動的です。 参照元のアセットがリポジトリー内に移動すると、参照は自動的に更新されます。 詳しくは、 [複合アセットの管理方法](/help/assets/managing-linked-subassets.md).

#### Brand Portal の機能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] では、承認済みアセットを容易に取得、効果的に制御し、それらのアセットを様々なデバイスをまたいで外部のベンダー／代理店、および内部のビジネスユーザーへと安全に配布できます。アセットの共有を効率化し、アセットの市場投入時間を短縮し、コンプライアンスに違反した使用や不正アクセスのリスクをなくすことができます。

詳しくは、 [Brand Portalの新機能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=ja).

#### Connected Assets {#connectedassets}

大規模企業では、Web サイトの作成に必要なインフラストラクチャを分散させることができます。しかし、Web サイトの作成機能と必要なデジタルアセットが、分断させた状態で別々の場所に存在する場合があります。

[!DNL Experience Manager Sites] は Web ページの作成機能を備え、 は Web サイトに必要なアセットを提供するデジタルアセット管理（DAM）システムです。[!DNL Experience Manager Assets][!DNL Experience Manager] では、[!DNL Sites] と [!DNL Assets] の統合により、上記の使用事例をサポートできるようになりました。詳しくは、 [Connected Assets の機能の設定方法と使用方法](/help/assets/use-assets-across-connected-assets-instances.md).

![アセットを [!DNL Experience Manager] にデプロイする [!DNL Sites] 別のページ [!DNL Experience Manager] デプロイメント](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*図：アセットを [!DNL Experience Manager] にデプロイする [!DNL Sites] 別のページの [!DNL Experience Manager] デプロイメント。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] で強化されたリッチメディアオーサリングと配信を提供 [!DNL Experience Manager Assets] 没入感のあるパーソナライズされた最先端のエクスペリエンスを推進する。 単一の高品質なプライマリアセットをアップロードし、Adobeの高度なクラウドレンダリングとビューアを使用することで、任意のレンディションの組み合わせをその場で配信して、組織のメディア戦略をサポートできます。

新しい [!DNL Dynamic Media] 機能： [Dynamic Mediaリリースノート](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### 360 ビデオのサポート {#video-support}

360 ビデオファイルを [!DNL Experience Manager] 最先端のビューアを使用して、デスクトップ、モバイル、VR ヘッドセットに VR エクスペリエンスを配信します。 詳しくは、 [360 ビデオの使用](/help/assets/360-video.md).

##### カスタムビデオサムネール {#custom-video-thumbnails}

DAM に保存されているビデオそのものまたは他のコンテンツのフレームを使用して、ビデオアセットのサムネールをカスタマイズできるようになりました。その他の手順については、 [ビデオサムネールについて](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### アクセシビリティの強化 {#accessibility-enhancements}

[!DNL Dynamic Media] ビューアで、Aria サポート、スクリーンリーダー、Alt-text などのアクセシビリティ機能が強化されました。 詳しくは、 [ビューアリファレンスガイド](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### 検索エクスペリエンスの強化 {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5 以降では、マーケターは検索結果ページから目的のアセットをより迅速に検出できます。 検索フィルターのアセット数は、検索フィルターを適用する前でも更新されます。フィルターに対するアセット数を確認すると、検索結果を効率的にナビゲートすることができます。詳しくは、 [Experience Manager内のアセットの検索](/help/assets/search-assets.md).

![検索ファセットで検索結果をフィルタリングしない場合のアセット数の表示](/help/assets/assets/asset_search_results_in_facets_filters.png)

*図：検索ファセットで検索結果をフィルタリングしない場合のアセット数の表示*

#### 使いやすさの向上 {#usability-enhancement}

フォルダー内または検索結果から一度に読み込まれたすべてのアセットを選択できるようになりました。 複数のアセットをすばやく管理するのに役立ちます。チェックボックスをオンにすると、シナリオに合うすべてのアセット（検索結果など）が選択され、 [!DNL Experience Manager] インターフェイス。

![「すべて選択」オプションを使用すると、読み込まれたすべてのアセットを 1 回のクリックで選択できます。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*図：「すべて選択」オプションを使用すると、読み込まれたすべてのアセットを 1 回のクリックで選択できます。*

#### メタデータの機能強化 {#metadata-enhancements}

[!DNL Assets] を使用すると、フォルダープロパティページに表示されるレイアウトとメタデータを定義する、アセットフォルダーのメタデータスキーマを作成できます。 既存のフォルダーにフォルダーメタデータスキーマを割り当てたり、フォルダーの作成時にフォルダーを割り当てたりできるようになりました。 詳しくは、](/help/assets/metadata-config.md#folder-metadata-schema)フォルダーメタデータスキーマ[を参照してください。

カスケードメタデータを指定すると、選択肢をフォームに手動で入力するのではなく、実行時に JSON ファイルから読み込むことができます。詳しくは、 [カスケードメタデータ](/help/assets/metadata-schemas.md#cascading-metadata).

#### レポート機能の強化 {#reporting-enhancements}

ダウンロードしたレポートに、コンテンツフラグメントとリンク共有が含まれます。 詳しくは、[AEM Assets レポート](/help/assets/asset-reports.md)を参照してください。

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

詳しくは、 [AEM 6.5 Formsの新機能および機能強化の概要](/help/forms/using/whats-new.md) を参照してください。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

使用している AEM 6.5 インスタンスを Livefyre と連携させることができます。詳しくは、 [Livefyre とAEMを統合する方法](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### 顧客中心の開発を活用 {#leverage-customer-focused-development}

アドビは、お客様が開発のすべての段階、つまり仕様、開発、テストに関与できる顧客中心開発モデルを使用しています。このプロセスにご協力いただいているお客様とパートナーの皆様に感謝いたします。

アドビでは、お客様中心のバグ修正と機能強化リクエストの開発に関する情報収集、優先順位付け、追跡の手順およびプロセスを整備しています。この [Experience Managerサポートポータル](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support) は、Adobe機能強化および欠陥追跡システムと統合されています。 お客様の質問は、可能な場合はカスタマーサポートチームが特定し、解決します。 研究開発部門にエスカレートされた場合は、すべての顧客情報が収集され、優先順位付けとレポートに使用されます。有料サポート、保証に関する問題、お客様が有料で提供する機能強化に対して、優先度が高くなっています。

この優先順位付けのプロセスにより、AEM 6.5 では 750 件を超えるお客様中心の変更がおこなわれました。

## このリリースに含まれるファイルのリスト {#list-of-files-that-are-part-of-the-release}

**基盤**

* スタンドアロンのクイックスタート： `cq-quickstart-6.5.0.jar`.
* アプリケーションサーバーのクイックスタート： `cq-quickstart-6.5.0.war`.
* 様々な Web サーバーおよびプラットフォーム向けの Dispatcher 4.3.2 以降。 詳しくは、 [ダウンロードリンク](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
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

* スマートコンテンツの言語モデル。英語は事前インストール済み。ほかに以下の言語がダウンロード可能

   * [ドイツ語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [スペイン語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [イタリア語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [フランス語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* ダイアログ変換ツールなどを含む AEM Modernize Tool Suite（[GitHub プロジェクト](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 強化された PDF Rasterizer を追加するためのパッケージ（[詳細](/help/assets/aem-pdf-rasterizer.md)）
* 強化された RAW 画像のサポートを追加するためのパッケージ（[詳細](/help/assets/camera-raw.md)）

**Forms**

* [AEM Forms の機能パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

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

## インストールと更新 {#install-update}

設定要件については、 [インストール手順](/help/sites-deploying/custom-standalone-install.md).

詳しい手順については、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md).

## サポートされているプラットフォーム {#supported-platforms}

サポートレベルを含む、サポート対象プラットフォームの完全なマトリックスを見つけます。 [AEM 6.5 の技術要件](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oracleは、OracleJava SE 製品の長期サポート (LTS) モデルに移行しました。 Java 9 と 10 は、Oracle別の非 LTS リリースです。詳しくは、 [OracleJava SE サポート・ロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html). Adobeは、AEMを実稼動環境でのみ実行するための Java の LTS リリースをサポートしています。 AEM 6.5 で使用する場合は、Java 11 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を常時評価して、さらに強力なバージョンへの置き換えの計画や、将来の展望や拡張に備えた部分的な再実装の決定を継続的におこなっています。

の場合 [!DNL Adobe Experience Manager] 6.5, [非推奨（廃止予定）および削除された機能のリストを読む](/help/release-notes/deprecated-removed-features.md). このページには、近い将来におこなわれる変更の予告と、前のリリースからアップデートするお客様向けの重要な注意事項も含まれています。

## 既知の問題 {#known-issues}

### Platform {#platform}

* CRX-Quickstart とその内容が削除された場所に問題が報告されます。

   これらの各アクションで、 `htmllibmanager.fileSystemOutputCacheLocation` が空の文字列ではありません：

   1. 呼び出し `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. AEM 6.5 へのアップグレード.
   3. AEM 6.5 での「遅延コンテンツ移行」の実行

   A [ナレッジベース](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) この記事では、詳細とこの問題の回避策について説明します。

* AEM 6.5 インスタンスで JDK 11 を使用している場合、一部のパッケージをデプロイすると、一部のページが空白で表示されることがあります。 ログファイルには、次のエラーメッセージが表示されます。

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

このエラーを解決するには：

1. AEM インスタンスを停止してに移動します。 `<aem_server_path_on_server>crx-quickstart\conf` をクリックし、 `sling.properties` ファイル。 Adobeは、このファイルのバックアップを作成することをお勧めします。

1. `org.osgi.framework.bootdelegation=` を検索。追加 `jdk.internal.reflect,jdk.internal.reflect.*` 結果を表示するプロパティ。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. ファイルを保存し、AEMインスタンスを再起動します。

## Sites {#sites}

* **ページバージョンの操作**:ページが移動されている場合は、移動前に行われたバージョンのプレビューを実行できなくなりました。

### Assets {#assets}

* **検索：** 検索文字列の先頭にスペース ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

### Forms {#forms}

* AEM Formsを Linux オペレーティングシステムにインストールすると、ハードウェアセキュリティモジュールを使用したデジタル署名が機能しない。 （CQ-4266721）
* （WebSphere 上のAEM Forms のみ）**ユーザー名**&#x200B;を検索条件として&#x200B;**管理者**&#x200B;を検索する場合、**Forms のワークフロー**／**タスクの検索**&#x200B;を実行しても結果が返されない（CQ-4266457）

* AEM Formsは、JPEG圧縮を含む TIF およびTIFFファイルをPDFドキュメントに変換できません。 （CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* （JBoss 7 のみ）以前のバージョンからAEM 6.5 Formsにアップグレードし、以前のバージョンで、デフォルトの送信またはデフォルトのレンダリングプロセスのコピーを作成して使用したプロセス (.lca) がある場合、そのようなプロセス (.lca) を使用するFormsは必要なアクションを実行できません。 （CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer インストーラーを使用するには、32 ビット版の [Visual C++再配布可能ランタイムパッケージ 2012](https://support.microsoft.com/ja-jp/help/2977003/the-latest-supported-visual-c-downloads) および [Visual C++再配布可能ランタイムパッケージ 2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* PDFジェネレーターは、スマートカードベースの認証をサポートしていません。  管理者がグループポリシーを有効にしたとき `Interactive Logon: Require Smart card` Windows サーバーでは、既存のすべてのPDFジェネレーターユーザーが無効化されます。

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなる問題を解決するには、パブリッシュインスタンスで CRXDE を開き、に移動します。 `/libs/fd/af/runtime/clientlibs/guideChartReducer`をクリックし、次に示すプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

* AEM Formsを起動すると、 `SAX Security Manager could not be setup` 警告が表示されます。
* Apple iOSまたはAdobe Acrobat Readerバージョン20.10.00を実行する iPadOS で、AEM Forms Document Security で保護されたPDFを開いたとき。
* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 では、この問題を修正しています。

## 製品のダウンロードとサポート（制限付きサイト） {#product-download-and-support-restricted-sites}

以下のサイトは、のお客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/).

* の追加機能に関する製品アップデート、パッチ、パッケージ [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Admin Console](https://adminconsole.adobe.com/). 詳しくは、 [新しいAdobeカスタマーサポートエクスペリエンス](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
