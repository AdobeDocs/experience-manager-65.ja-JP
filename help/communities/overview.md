---
title: AEM Communities の概要
seo-title: AEM Communities の概要
description: AEM Communities の機能とセットアップの概要
seo-description: AEM Communities の機能とセットアップの概要
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 4533fa42fa3fa9f157d5ca8fee1251005b1d587e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 32%

---


# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager（AEM）Communities では、高いパフォーマンスと優れたサイト管理機能を持つオンプレミスのコミュニティサイトを素早く作成し、サイト訪問者を価値あるコミュニティメンバーに転換できます。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Communities の機能 {#communities-features}

AEM Communitiesは、サイト訪問者との関係を発展させる。

* **ブログ、Q&amp;A、** イベントカレンダー、
* **フォーラム、コメント、その他のコミュニティコンテンツを通じてインサイト**&#x200B;を得る一方で、多くの場合はユーザー生成コンテンツ(UGC)と呼ばれます。
* これは、公開環境の信頼できるメンバーによる&#x200B;**モデレート**&#x200B;を許可します。
* **TwitterやFacebookとのソーシャル** ログイン、
* **コミュニティコンテンツのインライン** 翻訳、
* **公開済みコミュニティサイトでのコミュニティグループ** 作成、
* **バッジ** を賞めるスコーリング
* **ファイル共有**、
* **** 通知と **アクティビティストリーム**、
* ユーザー生成コンテンツ内の他の登録メンバー(@mention)に&#x200B;**タグ付け**&#x200B;を行って、メンバーの注意を引くことを許可します。
* 有効化コンポーネント（カタログとコースの再生、割り当て、ファイルライブラリなど）に対して&#x200B;**キーボードナビゲーション**&#x200B;をサポート。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト  {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

[サイト作成ウィザード](/help/communities/sites-console.md):

* 選択した[コミュニティサイトテンプレート](/help/communities/sites.md)に基づいて、サイトの機能をアセンブルします。次に例を示します。

   * [コミュニティ機能](#community-functions)から作成したテンプレート
   * オプションの[コミュニティグループ](#communitygroups)機能

* 次の設定を行います。

   * モデレート
   * ログイン
   * 翻訳

* 重要な機能を提供します。

   * レスポンシブデザイン：[TwitterBootstrapテーマ](https://getbootstrap.com)を使用

   * ログイン：自己登録， [ソーシャルログイン](/help/communities/social-login.md)，ユーザープロファイル

      * 通知：
会員は、彼らに関連するイベントと、[@mensioned](/help/communities/overview.md#mentionssupport)の場所でユーザーが生成したコンテンツを見る。

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送信または受信できます。
      * 検索：コミュニティサイト内を検索する機能。
      * 言語の切り替え：[多言語サイト](/help/sites-administering/translation.md)の言語を選択する機能。

      * 管理：権限を持つメンバーがコミュニティサイト内のユーザーをモデレートおよび管理できるようにするアクセス。

* ページレベルのオーサリング手順を多数排除します。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションのアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能に対しては、ナビゲーションリンクが提供されます。

新しいコミュニティサイトをすばやく作成できることを体験するには、[AEM Communitiesの使い始めに](/help/communities/getting-started.md)を参照してください。

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの持続性と推奨されるデプロイメントの詳細については、次を参照してください。

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md):UGCで使用可能なSRPストレージオプションについて説明します。
* [推奨トポロジ](/help/communities/topologies.md)。使用事例とSRPの選択に基づくトポロジを説明します。
* [AEM 6.5 Communities](/help/communities/upgrade.md)(AEM 6.5に移行する際のUGCに関する有用な情報を提供)へのアップグレード

## コミュニティコンソール {#communities-consoles}

作成者環境では、グローバルナビゲーションコンソールから[Communitiesコンソール](/help/communities/consoles.md)にアクセスできます。このコンソールには次のものが含まれます。

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの作成
   * サイトの編集
   * サイト管理
   * [コミュニティグループ](/help/communities/groups.md)コンソール

* [モデレート](/help/communities/moderation.md)コンソール

   * 作成者および公開環境用の一般的な一括モデレートUI。
   * 新しいフィルター条件。

* [メンバーおよびグループ](/help/communities/members.md)管理コンソール

   * 作成者環境から発行側ユーザー（メンバー）を作成および管理する機能を提供します。
   * メンバーを禁止する機能を提供します。
   * 作成者環境から、発行側のユーザーグループ（メンバーグループ）を作成および管理できます。

* [レポート](/help/communities/reports.md)コンソール

   * 割り当て、投稿、表示に関するレポートを生成できます。

* [リソース](/help/communities/resources.md)コンソール

   * イネーブルメントリソースと学習パスを作成する機能を提供します。
   * イネーブルメントリソースと学習パスに関するレポートにアクセスできます。

グローバルツールコンソールから次のコミュニティツールにアクセスできます。

* [サイトテンプレート](/help/communities/tools.md#sitetemplatesconsole)コンソール

   * コミュニティサイトテンプレートを作成および管理します。

* [グループテンプレート](/help/communities/tools.md#grouptemplatesconsole)コンソール

   * コミュニティグループテンプレートを作成および管理します。

* [コミュニティ機能](/help/communities/tools.md#communityfunctionsconsole)コンソール

   * コミュニティ機能を作成および管理します。

* [ストレージ設定](/help/communities/tools.md#storageconfiguratonconsole)コンソール

   * サイトの[共通ストア](/help/communities/working-with-srp.md)を選択して構成します。

* [コンポーネントガイド](/help/communities/components-guide.md)

   * すべてのCommunitiesコンポーネントのサンプルと、それらを試す機能を提供するサンプルサイト[コミュニティコンポーネント](https://localhost:4502/editor.html/content/community-components/en.html)です。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、どのサンプルサイトにも依存しないコミュニティサイトを迅速に設定するために、コミュニティサイトテンプレートの選択に基づいて行われます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザプロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](/help/communities/sites.md)を参照してください。

## コミュニティ機能  {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能とは、通常のAEMページで、コミュニティサイトテンプレートに容易に組み込むことができる機能に結合されたコンポーネントを含む。

[コミュニティ機能コンソール](/help/communities/functions.md)を参照してください。

## コミュニティグループとグループテンプレート  {#community-groups-and-group-templates}

コミュニティグループ機能は、サブコミュニティを作成者と発行環境の両方から許可されたユーザーおよびコミュニティメンバーがコミュニティサイト内で動的に作成する機能です。

作成者環境から、コミュニティグループ（サブコミュニティ）を既存のコミュニティサイト内に作成したり、テンプレートの構造に[Groups関数](/help/communities/functions.md#groups-function)が含まれる場合に既存のグループ内にネストしたりできます。

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にGroups機能を追加すると、1つのグループテンプレートを指定するか、新しいコミュニティグループを作成する際に選択したテンプレートを指定するように設定されます。

関連トピック：

* [サイトグループ](/help/communities/groups.md) コンソールは、作成者環境でサブコミュニティを作成するために使用します。
* [グループテンプレート](/help/communities/tools-groups.md) コンソールを使用して、グループのサイト構造を作成できます。
* [入れ子グループを含むコミュニティサイトをすばやく作成するためのチュートリアルについては、AEM](/help/communities/getting-started.md) コミュニティの概要を参照してください。

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](/help/communities/author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](/help/communities/components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ  {#types-of-communities}

### Engagement Community {#engagement-community}

エンゲージメントコミュニティは、コミュニティのメンバーとしての顧客の情報提供、フィードバックの要請、顧客の対話を可能にする顧客の関与に重点を置いたコミュニティサイトです。

エンゲージメントコミュニティの機能には次のものがあります。

* ログイン
* メッセージ
* フォーラム
* コメント
* レビュー
* 評価
* 投票
* ブログ
* グループ
* カレンダー
* 翻訳
* モデレート
* 通知
* スコアリングとバッジ
* 解析レポート

新しいエンゲージメントコミュニティをすばやく作成できることを体験するには、[AEM Communitiesの使い始めに](/help/communities/getting-started.md)を参照してください。

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

有効化コミュニティの機能には、次のものがあります。

* [エンゲージメントコミュニティ](#engagement-community)のすべての機能。
* コンテンツと学習を割り当てる機能メンバーおよびメンバー・グループへのリソース。
* クイズやテストなど、SCORMコンテンツをサポートします。
* 割り当て完了の追跡。
* レポートと解析へのアクセス。
* フォーラム、メッセージング、コメントおよびレーティングを通じて、学習リソースに関する会話を行う機能。

[有効化アドオンが](/help/communities/enablement.md)設定されている場合は、有効化コミュニティが作成される可能性があります。この場合、実稼働環境で使用する追加のライセンスが必要になります。 有効化コミュニティサイトには、[割り当て関数](#community-functions)が含まれます。

新しい有効化コミュニティを簡単に作成するには、[AEM Communitiesでの利用の手引き](/help/communities/getting-started-enablement.md)を参照してください。

## AEM Demo Machine {#aem-demo-machine}

[AEMデモマシン](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)は、AEM [サイト](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[アセット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[コミュニティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[アプリ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)、[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)のデモを管理し、実行します。QuickStartインスタンスの起動のみを行います。 AEM Demo Machineは、MongoDB、Solr、MySQL、FFmpeg、電子メールサーバーなど、追加の[インフラストラクチャ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)をセットアップします。

AEMデモマシンには次のものが含まれます。

* [グラフィカルユーザーインターフェイス](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 設定可能な[プロパティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)と[ターゲット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)を持つApache ANTスクリプト

* インストールするパッケージです。

AEM Demo Machineは、Windows、MacOS、およびLinuxでCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4で正常にテストされました。

AEM Demo Machineには有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント  {#aem-communities-documentation}

* 推奨される展開については、[Communitiesの展開](deploy-communities.md)を参照してください。
* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](administer-landing.md)を参照してください。
* Social Component Framework(SCF)とCommunitiesのコンポーネントと機能のカスタマイズについては、[Developing Communities](communities.md)を参照してください。
* Communitiesコンポーネントの作成方法と設定方法については、[Authoring Communities Components](author-communities.md)を参照してください。

