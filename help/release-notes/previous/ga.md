---
title: 一般リリースノート（ [!DNL Adobe Experience Manager]  6.5）
description: '[!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法および詳細な変更リストが記載されています。'
source-git-commit: 37f1df9f9421ff18fff45723b6eb081f0192520a
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 99%

---

# 一般リリースノート（[!DNL Adobe Experience Manager] 6.5）{#general-release-notes-for-adobe-experience-manager}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 |
| 種類 | メジャーリリース |
| 一般公開日 | 2019年4月8日（PT） |
| 推奨されるアップデート | 詳しくは、 [AEM の最新のアップデート](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html?lang=ja)を参照してください。 |

### 参考情報 {#trivia}

このバージョンの [!DNL Adobe Experience Manager] のリリースサイクルは、2018年4月4日（PT）に開始し、23 回の品質保証とバグ修正を繰り返し、2019年3月28日（PT）に終了しました。このリリースで修正された、機能強化と新機能を含むお客様関連の問題の総数は 1345 件です。   

[!DNL Adobe Experience Manager] 6.5 は、2019年4月8日（PT）に一般公開されました。

![AEM 6.5 ログイン画面](/help/assets/assets/aem65-login-v4.png)

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 は、[!DNL Adobe Experience Manager] 6.4 コードベースに対するアップグレードリリースです。新機能と強化された機能、お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、[!DNL Adobe Experience Manager] 6.4 の SP4 までのサービスパックリリースも含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 のプラットフォームは、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java コンテンツリポジトリの Apache Jackrabbit Oak 1.10.2 上に構築されています。

Quickstart は、サーブレットエンジンとして Eclipse Jetty 9.4.15 を使用します。

#### Java サポート  {#java-support}

* 既にサポートされている Java 8 に加えて、Java 11 を新しくサポートします。。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* Java 11 および Java 8 のメンテナンスアップデートが Oracle から公開されない場合は、AEM 関連プロジェクトで使用するお客様向けにアドビが配布します。

#### Java の開発 {#java-development}

* [Uberjar から 2 つのバージョン](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)（廃止予定としてマークされていないパブリックインターフェイスを使用した推奨バージョンと、廃止予定としてマークされているインターフェイスを含むバージョン）がリリースされました。

#### ユーザーインターフェイス {#user-interface}

UI に対して様々な機能強化がおこなわれ、生産性と使いやすさが向上しました。

* ユーザーとグループの新しい権限管理 UI
* 列表示では、画面上に表示されるエントリのみを読み込み、それ以外のエントリはユーザーがスクロールを開始した場合にのみ読み込まれるようになりました。リストおよびカード表示では、AEM 6.0 以降、この機能が既に実装されています（AEM 6.4 で改善されました）。。
* 列表示には、該当する場合、ページやアセットのワークフローステータスが含まれるようになりました。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションを使用すると、同じフォルダー内のすべてのページやアセットに対してアクションを手軽に実行することができます。
* 「[すべてを選択](/help/sites-authoring/basic-handling.md#select-all)」アクションは、読み込まれたページやアセットだけでなく、すべてのページやアセットに対してアクションの実行を試みます。アクションがバルクアクションを処理するようにアップグレードされていない場合、警告ダイアログが表示されます。

>[!CAUTION]
>
>クラシック UI の機能がさらに強化される予定はありません。AEM 6.5 にはクラシック UI が含まれており、以前のリリースからアップグレードするお客様はクラシック UI をそのまま使用し続けることができます。クラシック UI は非推奨になっても引き続き完全にサポートされます。[詳細情報](/help/sites-deploying/ui-recommendations.md)。

#### 検索およびインデックス作成 {#indexing-and-search}

* Oak の検索で動的ファセットをサポートするようになりました。例えば、アセット検索のフィルターレールに結果の予測件数が表示されます。
* QueryBuilder は、動的ファセットを使用して結果を返すように拡張されました。

#### アップグレード {#upgrade}

* AEM 6.5 への直接インプレースアップグレードは、AEM 6.2、6.3、6.4 を使用しているお客様に対してサポートされています。5.x または 6.0／6.1 を使用しているお客様がインプレースアップグレードを使用するには、まず 6.4 にアップグレードした後、6.5 にアップグレードするか、インスタンス間のコンテンツの転送を通じて AEM 6.5 に直接アップグレードする必要があります。
* アップグレード手順は 6.5 でもほぼ変わりません。
* 6.4 で導入された下位互換性、アップグレードの複雑さの評価、持続可能なアップグレードの機能を引き続きサポートしています。必要に応じて、これらの分野でバージョン固有の更新がおこなわれてきました。
* パターン検出パッケージが簡素化され、利用可能なソースバージョンごとに、6.5 へのアップグレードを評価するパッケージが 1 つ用意されるようになりました。
* アップグレードの手順について詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

#### プロジェクトとワークフロー {#projects-and-workflows}

* 6.4 で導入された新しいワークフローモデルのエディターが改善され、コピーや公開などの新しい操作、ワークフローステップでの変数のサポート、強化された `OR` 分割および `AND` 分割が追加されました。

#### リポジトリ {#repository}

* Adobe Experience Manager 6.5 の基盤は、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java コンテンツリポジトリの Apache Jackrabbit Oak 1.10.2 上に構築されています。
* 修正された問題の概要については、[Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) および [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) を参照してください。

>[!CAUTION]
>
>AEM 6.3 以降の新しいバージョンの Oak Segment Tar では、リポジトリを移行する必要があります。この手順は、古いバージョンの TarMK からアップグレードする場合、または別のタイプの格納機能から新しい Segment Tar に切り替える場合に必須です。新しい Segment Tar のメリットについて詳しくは、[Oak Segment Tar への移行に関する FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar) を参照してください。

#### OSGi {#osgi}

* OSGi Promises および Converter ユーティリティライブラリが追加されました。

#### セキュリティ {#security}

* 管理者ユーザーのパスワードの有効期限が追加されました。

#### Web サーバー {#web-server}

* クイックスタート配布版では、Eclipse Jetty 9.4.15 をサーブレットエンジンとして使用します（AEM 6.4 には 9.3.22 が付属）。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 管理された単一ページアプリ {#managed-single-page-apps}

ページエディターでは、コンテンツのコンテキスト内編集と、レンダリングされたクライアント側エクスペリエンス内での作成／レイアウトの機能が追加されました（[SPA エディター](/help/sites-developing/spa-architecture.md)とも呼ばれます）。JavaScript フレームワークの React または Angular を使用して作成された既存の単一ページアプリを、AEM SJ SDK を使用して拡張することで、お客様による編集が可能になります。

SPA のサポートは AEM 6.4 SP2 の一部として導入されたものですが、AEM 6.5 ではさらに以下が可能になりました。

* テンプレートエディターを使用して、AEM で編集可能な SPA の部分を編集および設定できます。
* マルチサイト管理を使用して国ごと、フランチャイズごと、またはホワイトレーベルの SPA エクスペリエンスを作成できます。

#### ヘッドレスコンテンツ管理 {#headless-content-management}

AEM では、様々な形式で様々なスタックレベルからコンテンツを提供できます。一部は、2008 年以降、](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)Sling GET[ および ](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)POST Servlet[ で機能しています。コンテンツサービス（[Sling Model エクスポーター](https://docs.adobe.com/content/help/ja/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)）は AEM 6.3 で導入されたもので、AEM SJ SDK で単一ページアプリの改善に使用されている方法です。[HTTP API for Assets](/help/assets/mac-api-assets.md) は、AEM 6.5 向けに拡張された CRUD API です。

新しい HTTP API の機能は次のとおりです。

* [HTTP API for Assets でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになり、フラグメントの作成、更新、読み取り、削除が可能になりました。
* [コンテンツフラグメントリストのコアコンポーネント](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)でコンテンツサービスを通じてコンテンツフラグメントのリストを公開します。
* コンポーネントごとにコンテンツサービスのデフォルト JSON 出力を表示する[コアコンポーネントライブラリ](https://opensource.adobe.com/aem-core-wcm-components/library.html)

#### Screens アドオン {#screens-add-on}

インタラクティブなキオスク端末からデジタルサイネージに至るまで、あらゆるデジタル表示でのエクスペリエンスを効率良くデザイン、配信、最適化します。

* コンテンツ再利用の向上により、デジタルと実店舗の区別なくエクスペリエンスとコンテンツを統一できます。
* ローンチのサポートにより、オーサリングおよび承認／公開ワークフローを効率化します。
* SPA エディターを使用して、機能豊富でインタラクティブなエクスペリエンスを編集および配信できます。
* ローンチを使用して、サイネージコンテンツの今後の変更を計画できるようになりました。
* シーケンスチャンネルでの従量制再生が可能になりました。
* ソースファイル（Excel シートなど）を使用してプロジェクト構造を自動作成できるようになりました。
* 堅牢なオンラインおよびオフラインの操作（スマート同期）が追加されてメディアプレイヤーのサポートが強化され、大規模なサイネージネットワークにも対応できるようになりました。
* 動的プレースホルダーを使用して、データでトリガーされるコンテンツの場所または設定別にパーソナライズできます。
* Adobe Analytics と AEM Screens Player の連携でインサイトの統合が促進されます。

AEM Screens の変更点について詳しくは、[AEM Screens ユーザーガイド](https://docs.adobe.com/content/help/ja/experience-manager-screens/user-guide/aem-screens-introduction.html)のリリースノートを参照してください。

#### コンポーネントとテンプレートの開発 {#component-amp-template-development}

* 新規プロジェクト用の Maven プロジェクトアーキタイプ 18 以上については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases) を参照してください。
* 新規プロジェクト用の単一ページアプリ Maven プロジェクトアーキタイプ 1.0.6 以上については、[リリースノートの GitHub](https://github.com/adobe/aem-spa-project-archetype/releases) を参照してください。
* HTL バージョン 1.4 については、[リリースノートの GitHub](https://github.com/adobe/htl-spec/releases/tag/1.4) を参照してください。

   * 文字列、配列、オブジェクトの「in」演算子

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

* コアコンポーネント 2.3.2 以上については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照してください。
* レイアウトコンテナのグリッドシステムについては、[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照してください。
* クライアントライブラリマネージャー：JavaScript クライアントライブラリの軽量化に合わせて Google Closure Compiler がデフォルトになり（以前のデフォルトは Yahoo YUI でした）、Google Closure Compiler がバージョン v20190121 に更新されました。
* テンプレートエディターとポリシー

   * JS SDK を使用している単一ページアプリのテンプレートを作成および編集できます（SPA エディターとも呼ばれます）。

* 参照サイト We.Retail 4.0 については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照してください。
* 既存のサイトをアップグレードして最新のエディター機能を利用するためのツールキットについては、[Github リポジトリ](https://github.com/adobe/aem-modernize-tools)を参照してください。

>[!CAUTION]
>
>AEM には、既存のカスタムコードとの互換性を最大限に高めるために、jQuery ライブラリのバージョン 1.12.4 が含まれています。セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

#### サイト管理 {#site-administration}

* [参照](/help/sites-authoring/author-environment-tools.md#references)レールには、選択したページを参照する内部リンクを一覧表示する新しいセクションがあります。これは、ページをオフラインで取得したり削除することが想定される場合や、オフラインで取得する前に調整する必要があるページを確認する場合に便利です。
* [リスト表示](/help/sites-authoring/basic-handling.md#list-view)には、ページが現在ワークフローに含まれている場合にステータスを表示する新しいワークフロー列があります。
* [ページのプロパティ](/help/sites-authoring/editing-page-properties.md)で、ページにサムネールを割り当てるときに既存のアセットを参照できるようになりました（「サムネール」タブ）。

#### ページエディター {#page-editor}

* JS SDK を利用する React および Angular クライアント側コンポーネントで構築された単一ページアプリエクスペリエンスのコンテキスト内編集および作成が可能になりました（SPA エディターとも呼ばれます）。
* 基礎モードは、ページに基礎モードが設定されている場合にのみ表示されます。

#### コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* 全般的なコメントを書き込んだり、テキスト内のコメントを表示（タイムラインレールにも表示）するための新しい[注釈](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)レールがコンテンツフラグメントエディターに追加されました。
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)で、複数行テキスト要素のデフォルトのコンテンツタイプを簡単なテキスト、リッチテキスト、マークダウンのいずれかに設定できます。
* RTE（フルスクリーン表示）でテキストを選択して、[コメント／注釈](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)を追加できます。
* 参照レールでコンテンツフラグメント並列に表示して、[バージョンを比較](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)できるようになりました。
* アセットのダウンロードレポートにコンテンツフラグメントが適宜表示されるようになりました。
* /api.json を通じて、[Assets HTTP API でコンテンツフラグメントがサポート](/help/assets/assets-api-content-fragments.md)されるようになりました。コンテンツフラグメントの作成、更新、読み取りおよび削除のための API が用意されています。

#### エクスペリエンスフラグメント {#experience-fragments}

* [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)のインデックス作成を改善して、フラグメントの使用ページの検索でコンテンツが見つかるようになりました。
* 「[Adobe Target に書き出し](/help/sites-administering/experience-fragments-target.md)」オプションで、エクスペリエンスフラグメントを JSON（デフォルトは HTML）またはその両方として送信できるようになりました。

#### 翻訳 {#translation}

* プロジェクトマスターを使用して、翻訳プロジェクトを手軽に作成できます。
* 翻訳ジョブをデフォルトで承認済みステータスに設定することで、翻訳プロジェクトの実行を簡略化できます。
* サードパーティ翻訳メモリの変更点に合わせて翻訳済みページを更新できます。
* 翻訳ジョブを JSON 形式で書き出すことができます。
* Microsoft Translation との連携機能を更新して、V3 API を使用します。

#### マルチサイト管理（MSM） {#multi-site-management-msm}

* PushOnModify を使用するロールアウト設定について、矛盾した状態を避けるためにページ移動操作の処理を改善しました。
* ライブコピー構造の中で新しいページを作成すると、デフォルトでスタンドアロンページが作成されるようになりました。
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


* Adobe Target との連携で Target Standard API を使用できるようになりました。以前のバージョンの AEM では Target Classic HTTP API を使用していましたが、現在は非推奨になっています。
* Adobe Target の `mbox.js` バージョン 63 が含まれています。実装を `at.js` 1.x に切り替えることを強くお勧めします。
* `at.js` バージョン 1.5.0 が含まれるようになりました。 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html?lang=ja) を使用して `at.js` 1.x をサイトにプロビジョ二ングすることをお勧めします。

#### AEM と Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 が含まれています。実装を `AppMeasurement.js` に切り替えることをお勧めします。
* `AppMeasurement.js` v1.8.0 が含まれています。 [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) を使用して AppMeasurement.js をサイトにプロビジョ二ングすることをお勧めします。

#### AEM と Commerce {#aem-commerce}

AEM 6.4 以降、コマース統合フレームワークの改善のリリースサイクルが早くなりました。詳しくは[こちら](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=ja)を参照してください。

#### Communities アドオン {#communities-add-on}

最新リリースを入手するには、このドキュメントの [Communities のデプロイ](/help/communities/deploy-communities.md)の節を参照してください。

##### コミュニティエンゲージメントの強化 {#enhancements-to-community-engagement}

**@メンションのサポート**
AEM Communities では、登録ユーザーがユーザー生成コンテンツで他の登録メンバーをタグ付け（メンション）して注意を引くことができるようになりました。タグ付け（メンション）されたメンバーには、対応するユーザー生成コンテンツへのディープリンクが付いた通知が届きます。ただし、ユーザーは web とメールでの通知を無効にしたり有効にしたりすることができます。

![@メンションのサポート](/help/release-notes/assets/at-mentions.png)

コミュニティユーザーは、自分の名、姓またはユーザー名を検索しなくても、誰かが自分に接触してきたかどうか、または誰かが自分の注意を引く必要があるのかどうかを確認することができます。さらに、UGC 作成者は、問題に最もうまく対処し入力を追加できる特定の登録ユーザーからの応答を探すことができます。

コミュニティ管理者は、コミュニティコンポーネントで&#x200B;**メンションを有効化**&#x200B;して、これらのコンポーネントの機能を登録ユーザーが使用できるようにする必要があります。

**グループメッセージ送信**

コミュニティの登録メンバーは、同じメッセージをグループメンバーに個々に送信するのではなく、1 回の電子メール作成でダイレクトメッセージをグループに一括送信できるようになりました。[グループメッセージング](/help/communities/configure-messaging.md)を許可する には、[Messaging Operations Service](/help/communities/messaging.md#group-messaging) の両方のインスタンスを有効にします。

![グループメッセージ](/help/release-notes/assets/group-messaging.png)

##### 一括モデレートの機能強化 {#enhancements-to-bulk-moderation}

一括モデレートのカスタムフィルター

[カスタムフィルター](/help/communities/moderation.md#custom-filters) が開発され、一括モデレート UI に追加できるようになりました。

タグによるフィルタリングの例を示す[サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)を [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) で入手できます。このプロジェクトをベースに、類似のスタムフィルターを開発できます。

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
* AEM 6.5 Communities は、MSRP および DSRP の設定時に、Apache Solr 7.0 バージョンの検索プラットフォームに対応しています。

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

AEM 6.5 Forms では、いくつかの新機能と機能強化が加えられています。主なものは次のとおりです。

* 送信されたフォーム、処理されたドキュメント、レンダリングされたドキュメントの数を追跡できるトランザクションレポート
* インタラクティブコミュニケーションのユーザビリティの向上
* アダプティブフォームでのクラウドベースの電子署名
* AEM Sites の単一ページアプリケーション（SPA）へのアダプティブフォームやインタラクティブコミュニケーションの組み込み
* AEM ワークフローでの変数のサポート
* インタラクティブコミュニケーションでのデータ表示パターンのサポート
* アダプティブフォームおよびインタラクティブコミュニケーションテーブルの並べ替え
* フォームデータモデルでの入力データの自動検証

新機能や機能強化、ドキュメントのリソースについては、[AEM 6.5 Forms の新機能および機能強化の概要](/help/forms/using/whats-new.md)を参照してください。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

使用している AEM 6.5 インスタンスを Livefyre と統合できます。詳しくは、[Livefyre と AEM を統合する方法](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html?lang=ja-JP)を参照してください。

### 顧客志向の開発の強化 {#leverage-customer-focused-development}

アドビは、お客様が開発のすべての段階、つまり仕様、開発、テストに関与できる顧客中心開発モデルを使用しています。このプロセスにご協力いただいているお客様とパートナーの皆様に感謝いたします。

アドビでは、お客様志向のバグ修正と機能強化リクエストの開発に関する、情報収集、優先順位付け、追跡のための手順とプロセスを整備しています。[Experience Manager サポート ポータル](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=ja#support)は、アドビの機能強化および欠陥追跡システムと統合されています。お客様からの問い合わせは、可能であれば、カスタマーサポートチームで特定して解決します。研究開発部門にエスカレートされた場合は、お客様の情報をすべて収集して、優先順位付けとレポートに使用します。開発では有償のサポート、保証の問題、有償の顧客向け強化機能が優先されます。

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

* スマートコンテンツの言語モデル。英語は事前インストール済み。ほかに以下の言語がダウンロード可能

   * [ドイツ語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [スペイン語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [イタリア語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [フランス語](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* ダイアログ変換ツールなどを含む AEM Modernize Tool Suite（[GitHub プロジェクト](https://github.com/adobe/aem-modernize-tools)）

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
>Oracle は Oracle Java SE 製品の長期サポート（LTS）モデルに移行しました。Java 9 および 10 は Oracle による非 LTS でのリリースです（[Oracle Java SE サポートロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html)を参照してください）。アドビでは、AEM を実稼働環境で実行するためにのみ、Java の LTS リリース版をサポートしています。AEM 6.5 で使用するバージョンとしては、Java 11 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を常時評価して、さらに強力なバージョンへの置き換えの計画や、将来の展望や拡張に備えた部分的な再実装の決定を継続的におこなっています。

[!DNL Adobe Experience Manager] 6.5 については、[廃止される機能および削除された機能のリスト](/help/release-notes/deprecated-removed-features.md)を参照してください。このページには、近い将来におこなわれる変更の予告と、前のリリースからアップデートするお客様向けの重要な注意事項も含まれています。

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

* **ページバージョンの操作**: [ページが移動されている場合、移動前に行われたバージョンではプレビューを実行できなくなりました](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **検索**：検索文字列の先頭にスペースが含まれている場合、検索結果が返されません（[OAK-4786](https://issues.apache.org/jira/browse/OAK-4786)）
* **フォルダーメタデータスキーマ**：選択ボタンを追加すると、「ID」フィールドと「値」フィールドが期待どおりにレンダリングされず、削除機能が機能しない（CQ-4261144）
* アセット名の変更時に、アセット名に空白を使用できない（CQ-4266403）

### Forms {#forms}

* AEM Forms が Linux オペレーティングシステムにインストールされている場合、ハードウェアセキュリティモジュールを使用したデジタル署名が機能しません（CQ-4266721）
* （WebSphere 上の AEM Forms のみ）**ユーザー名**&#x200B;を検索条件として&#x200B;**管理者**&#x200B;を検索する場合、**Forms ワークフロー**／**タスクの検索**&#x200B;を実行しても結果が返されません（CQ-4266457）

* AEM Forms で、JPEG 圧縮の TIF および TIFF ファイルを PDF ドキュメントに変換できません（CQ-4265972）
* **AEM Forms の移行**&#x200B;ページの「**AEM Forms アセットスキャナー**」オプションと「**レターからインタラクティブコミュニケーションへの移行**」オプションが機能しない（CQ-4266572）

* （JBoss 7のみ）AEM Forms を以前のバージョンから 6.5 にアップグレードにするとき、デフォルトの送信プロセスまたはレンダリングプロセスをコピーして使用しているプロセス（.lca）があると、そのプロセス（.lca）を使用する HTML5 フォームが必要なアクションを実行できません（CQ-4243928）
* アダプティブフォームで、ルールエディターからフォームデータモデルサービスを呼び出して画像選択コンポーネントの値を動的に更新する場合、画像選択コンポーネントの値が更新されない（CQ-4254754）
* AEM Forms Designer インストーラーを実行するには、32 ビット版の [Visual C++ 再頒布可能ランタイムパッケージ 2012](https://support.microsoft.com/ja-jp/help/2977003/the-latest-supported-visual-c-downloads) と [Visual C++ 再頒布可能ランタイムパッケージ 2013](https://support.microsoft.com/ja-jp/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package) が必要です。インストールを開始する前に、これらの再頒布可能ランタイムパッケージがインストールされていることを確認してください。（CQ-4265668）

* PDF ジェネレーターは、スマートカードベースの認証をサポートしていません。管理者が Windows サーバーでグループポリシー `Interactive Logon: Require Smart card` を有効にすると、既存のすべての PDF Generator のユーザーが無効になります。

* コンポーネントの値を動的に更新するようにアダプティブフォームが設定されていて、そのフォームをホストするパブリッシュインスタンスにディスパッチャーを通じてアクセスする場合、フィールドの値を動的に更新する機能が動作しなくなります。この問題を解決するには、パブリッシュインスタンスで CRXDE を開き、`/libs/fd/af/runtime/clientlibs/guideChartReducer` を検索して、次のプロパティを作成します。

   * 名前：allowProxy
   * タイプ：Boolean
   * 値：true
   * 保護：false
   * 必須：false
   * 複数：false
   * 自動作成：False

   このプロパティを設定すると、ランタイムフォルダー内のクライアントライブラリからプロキシにアクセスできます。（CQ-4268679）

* AEM Forms を起動すると、`SAX Security Manager could not be setup` 警告が表示されます。
* Adobe Acrobat Reader バージョン 20.10.00 を実行している Apple iOS または iPadOS で、AEM Forms Document Security で保護された PDF を開いたとき。
* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 では、この問題を修正しています。

## 製品のダウンロードとサポート（制限付きサイト） {#product-download-and-support-restricted-sites}

以下のサイトは、お客様のみが利用できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/)。

* 製品の追加機能に関する[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上のアップデート、パッチ、パッケージ。

* [Admin Console 経由でのカスタマーサポート](https://adminconsole.adobe.com/)。詳しくは、[新しいアドビカスタマーサポートエクスペリエンス](https://docs.adobe.com/content/help/ja-JP/customer-one/using/home.html)を参照してください。
