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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 33%

---


# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager（AEM）Communities では、高いパフォーマンスと優れたサイト管理機能を持つオンプレミスのコミュニティサイトを素早く作成し、サイト訪問者を価値あるコミュニティメンバーに転換できます。

AEM Communities のライセンス、イネーブルメント機能の追加ライセンスおよび Adobe Analytics に関する情報については、アカウント担当者にお問い合わせください。

## Communities の機能 {#communities-features}

AEM Communitiesは、サイト訪問者との関係を発展させる。

* **ブログ** 、Q&amp;A、イベントカレンダー、
* フォーラム **、コメント、その他のコミュニティコンテンツを通じてインサイトを** 得ながら、ユーザー生成コンテンツ(UGC)と呼ばれることもあります。
* これは、 **公開環境の信頼できるメンバーによるモデレート** 、
* **TwitterおよびFacebookでのソーシャルログイン** 、
* **コミュニティコンテンツのインライン翻訳** 、
* **公開されたコミュニティサイトからコミュニティグループを作成** 、
* **バッジを審査するスコア** 、
* **ファイル共有**、
* **通知** / **アクティビティストリーム**、
* ユーザー生成コンテンツ内の他の登録済みメンバーに **タグ付け** (@mention)して、そのメンバーの注意を引くことを許可します。
* 有効化コンポーネント(カタログとコースの再生 **、割り当て、ファイルライブラリなど)の** キーボードナビゲーションをサポートします。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

The [site creation wizard](/help/communities/sites-console.md):

* Assembles features of the site, based on the selected [community site template](/help/communities/sites.md) which is:

   * [コミュニティ機能](#community-functions)から作成したテンプレート
   * optional [community groups](#communitygroups) feature

* 次の設定を行います。

   * モデレート
   * ログイン
   * 翻訳

* 重要な機能を提供します。

   * Responsive design: uses [Twitter Bootstrap themes](https://getbootstrap.com)

   * Login : self-registration, [social login](/help/communities/social-login.md), user profiles

      * 通知：メンバーは、メンバーに関連性のあるイベントと、 [@mensionedの場所にユーザー生成コンテンツを参照できます](/help/communities/overview.md#mentionssupport)。

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送信または受信できます。
      * 検索：コミュニティサイト内を検索する機能。
      * Language switching: ability to select a language for a [multilingual site](/help/sites-administering/translation.md).

      * 管理：権限を持つメンバーがコミュニティサイト内のユーザーをモデレートおよび管理できるようにするアクセス。

* ページレベルのオーサリング手順を多数排除します。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションのアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能に対しては、ナビゲーションリンクが提供されます。

To experience the ease of quickly creating a new community site, visit [Getting Started with AEM Communities](/help/communities/getting-started.md).

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの持続性と推奨されるデプロイメントの詳細については、次を参照してください。

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md):UGCで使用可能なSRPストレージオプションについて説明します。
* [推奨トポロジ](/help/communities/topologies.md)。使用事例とSRPの選択に基づくトポロジを説明します。
* [AEM 6.5 Communities](/help/communities/upgrade.md)(AEM 6.5に移行する際のUGCに関する有用な情報を提供)へのアップグレード

## コミュニティコンソール {#communities-consoles}

In the author environment, the global navigation console provides access to the [Communities console](/help/communities/consoles.md), which contains:

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

   * Select and configure the [common store](/help/communities/working-with-srp.md) for the site.

* [コンポーネントガイド](/help/communities/components-guide.md)

   * A sample site, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), that provides a sample of all Communities components with their default configuration and the ability to experiment with them.

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、どのサンプルサイトにも依存しないコミュニティサイトを迅速に設定するために、コミュニティサイトテンプレートの選択に基づいて行われます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザプロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](/help/communities/sites.md)を参照してください。

## コミュニティ機能 {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能とは、通常のAEMページで、コミュニティサイトテンプレートに容易に組み込むことができる機能に結合されたコンポーネントを含む。

[コミュニティ機能コンソール](/help/communities/functions.md)を参照してください。

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、サブコミュニティを作成者と発行環境の両方から許可されたユーザーおよびコミュニティメンバーがコミュニティサイト内で動的に作成する機能です。

From the author environment, community groups (sub-communities) may be created within an existing community site or nested within an existing group, when the structure of the template contains the [Groups function](/help/communities/functions.md#groups-function).

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にGroups機能を追加すると、1つのグループテンプレートを指定するか、新しいコミュニティグループを作成する際に選択したテンプレートを指定するように設定されます。

関連トピック：

* [サイトグループコンソール](/help/communities/groups.md) 。作成者環境でサブコミュニティを作成できます。
* [グループテンプレートコンソール](/help/communities/tools-groups.md) 。グループのサイト構造を作成できます。
* [「AEM Communitiesを使用する前に](/help/communities/getting-started.md) 」のチュートリアルを参照してください。

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](/help/communities/author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](/help/communities/components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ {#types-of-communities}

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

To experience the ease of quickly creating a new engagement community, visit [Getting Started with AEM Communities](/help/communities/getting-started.md).

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

有効化コミュニティの機能には、次のものがあります。

* All the features of an [engagement community](#engagement-community).
* コンテンツと学習を割り当てる機能メンバーおよびメンバー・グループへのリソース。
* クイズやテストなど、SCORMコンテンツをサポートします。
* 割り当て完了の追跡。
* レポートと解析へのアクセス。
* フォーラム、メッセージング、コメントおよびレーティングを通じて、学習リソースに関する会話を行う機能。

An enablement community may be created when the [Enablement add-on is configured](/help/communities/enablement.md), which requires additional licensing for use in a production environment. An enablement community site will include the [assignments function](#community-functions).

To experience the ease of creating a new enablement community, visit [Getting Started with AEM Communities for Enablement](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machineは、AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) Sites [, Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), Communities [, Communities, Communities Apps, Communities Apps, Apps Apps, Apps Appsは、QuickStartインスタンスを起動するよりもセットアップが必要な場合が多い、Forms Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)Assets, Cosets, Com, Com, Comm, Cos, Com, Dens, Demos, Demos, Demos, Des, Des, Des, Des, Dens, Des, Den, Des, Des, Dens, Demos, Demos, Dens, Dens, [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), Demos, Demos, Des, Des, Des The AEM Demo Machine will setup additional [infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) such as MongoDB, Solr, MySQL, FFmpeg and email servers.

AEMデモマシンには次のものが含まれます。

* A [graphical user interface](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Apache ANT scripts with configurable [properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) and [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* インストールするパッケージです。

AEM Demo Machineは、Windows、MacOS、およびLinuxでCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4で正常にテストされました。

AEM Demo Machineには有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント {#aem-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments.
* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](administer-landing.md)を参照してください。
* Visit [Developing Communities](communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.
* Visit [Authoring Communities Components](author-communities.md) to learn how to author with and configure Communities components.

