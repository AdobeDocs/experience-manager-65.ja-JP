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
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# AEM Communities の概要{#aem-communities-overview}

Adobe Experience Manager（AEM）Communities では、高いパフォーマンスと優れたサイト管理機能を持つオンプレミスのコミュニティサイトを素早く作成し、サイト訪問者を価値あるコミュニティメンバーに転換できます。

AEM Communities のライセンス、イネーブルメント機能の追加ライセンスおよび Adobe Analytics に関する情報については、アカウント担当者にお問い合わせください。

## Communities の機能 {#communities-features}

AEM Communitiesでは、サイト訪問者との関係を開発できます。このような関係は次のとおりです。

* **ブログ** 、Q&amp;A、イベントカレンダーを通じて、
* **フォーラム、コメント、その他のコミュニティコンテンツを通じてインサイトを得る一方で、ユーザー生成コンテンツ(UGC)と呼ばれる場合もあります。
* **モデレート**信頼できるメンバーが発行環境で使用できます。
* **ソーシャルログイン**TwitterおよびFacebookを使用した場合、
* **コミュニティ** ・コンテンツのインライン翻訳、
* **コミュニティグループの作成**公開済みコミュニティサイトから、
* **スコア**バッジを裁定
* **ファイル共有**、
* **通知**およびアクティビティ **ストリーム**、

* ユーザ **ー生成コンテンツに登録された他のメンバーにタグ付け** (@mention)して、そのメンバーの注意を引くことができます。
* 有効化コン **ポーネント** （カタログとコースの再生、割り当て、ファイルライブラリなど）のキーボードナビゲーションをサポートします。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

The [site creation wizard](/help/communities/sites-console.md):

* assembles features of the site, based on the selected [community site template](/help/communities/sites.md) which is:

   * [コミュニティ機能](#community-functions)から作成したテンプレート
   * optional [community groups](#communitygroups) feature

* 設定を使用して次の機能を構成します。

   * モデレート
   * ログイン
   * 翻訳

* 次の基本的機能を提供します。

   * レスポンシブデザイン：[Twitter Bootstrap のテーマ](https://getbootstrap.com)を使用

   * ログイン：自己登録、[ソーシャルログイン、](/help/communities/social-login.md)ユーザープロファイル

   * 通知：メンバーは、自分に関連するイベントを表示し、ユーザーが生成したコンテンツを [@mensionedの場所に表示します](/help/communities/overview.md#mentionssupport)。

   * メッセージング：メンバーによるコミュニティサイト内でのメッセージを送信または受信
   * 検索：コミュニティサイト内での検索機能
   * language switching:
ability to select a language for a [multilingual site](/help/sites-administering/translation.md)

   * 管理：コミュニティサイト内のユーザーをモデレートおよび管理するためのアクセス権を許可されたメンバーに付与

* 次に示すページレベルのオーサリング手順が不要になります。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像をオプションでアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能のナビゲーションリンクを提供

To experience the ease of quickly creating a new community site, visit [Getting Started with AEM Communities](/help/communities/getting-started.md).

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続化と推奨されるデプロイの詳細については、以下を参照してください。

* [Community Content Storage](/help/communities/working-with-srp.md)（コミュニティコンテンツストレージ）。UGCで使用可能なSRPストレージオプションについて説明します。
* [推奨トポロジ](/help/communities/topologies.md)。使用事例とSRPの選択に基づくトポロジを説明します。
* [AEM 6.5 Communitiesへのアップグレード](/help/communities/upgrade.md)。AEM 6.5に移行する際のUGCに関する有用な情報を提供します。

## コミュニティコンソール {#communities-consoles}

In the author environment, the global navigation console provides access to the [Communities console](/help/communities/consoles.md), which contains:

* [サイト](/help/communities/sites-console.md)コンソール

   * サイト作成
   * サイト編集
   * サイト管理
   * [コミュニティグループ](/help/communities/groups.md)コンソール

* [モデレート](/help/communities/moderation.md)コンソール

   * オーサー環境とパブリッシュ環境に共通する一括モデレート UI
   * 新しいフィルタリング条件

* [メンバーおよびグループ](/help/communities/members.md)管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理できます。
   * メンバーを禁止できます。
   * オーサー環境からパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理できます。

* [レポート](/help/communities/reports.md)コンソール

   * 割り当て、投稿、閲覧に関するレポートを生成できます。

* [リソース](/help/communities/resources.md)コンソール

   * イネーブルメントリソースと学習パスを作成できます。
   * イネーブルメントリソースと学習パスに関するレポートにアクセスできます。

グローバルツールコンソールから次のコミュニティツールにアクセスできます。

* [サイトテンプレート](/help/communities/tools.md#sitetemplatesconsole)コンソール

   * コミュニティサイトテンプレートを作成および管理できます。

* [グループテンプレート](/help/communities/tools.md#grouptemplatesconsole)コンソール

   * コミュニティグループテンプレートを作成および管理できます。

* [コミュニティ機能](/help/communities/tools.md#communityfunctionsconsole)コンソール

   * コミュニティ機能を作成および管理できます。

* [ストレージ設定](/help/communities/tools.md#storageconfiguratonconsole)コンソール

   * select and configure the [common store](/help/communities/working-with-srp.md) for the site

* [コンポーネントガイド](/help/communities/components-guide.md)

   * サンプルサイトの [Community Components](https://localhost:4502/editor.html/content/community-components/en.html) には、デフォルト設定のすべてのコミュニティコンポーネントのサンプルが用意されており、コンポーネントを試すことができます。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、コミュニティサイトテンプレートの選択に基づいて行われ、どのサンプルサイトにも依存しないコミュニティサイトをすばやく設定できます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザプロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランド化機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](/help/communities/sites.md)を参照してください。

## コミュニティ機能 {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能は、通常のAEMページで、コミュニティサイトテンプレートに簡単に組み込める機能に結び付けられたコンポーネントを含みます。

[コミュニティ機能コンソール](/help/communities/functions.md)を参照してください。

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、サブコミュニティを、作成者環境と発行環境の両方から、許可されたユーザーとコミュニティメンバーによってコミュニティサイト内に動的に作成させる機能です。

From the author environment, community groups (sub-communities) may be created within an existing community site or nested within an existing group, when the structure of the template contains the [Groups function](/help/communities/functions.md#groups-function).

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にグループ機能を追加すると、新しいコミュニティグループの作成時に、1つのグループテンプレートを指定するか、テンプレートの選択を行うように設定されます。

関連トピック:

* [作成者環境でサブコミュニティ](/help/communities/groups.md) を作成するためのサイトグループコンソール
* [グループ用のサイト構造を作成するための](/help/communities/tools-groups.md) 、グループテンプレートコンソール
* [AEM Communities使用の手引き](/help/communities/getting-started.md) 」のチュートリアルを参照してください。

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](/help/communities/author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](/help/communities/components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ {#types-of-communities}

### Engagement Community {#engagement-community}

エンゲージメントコミュニティは、顧客に情報を提供し、フィードバックを要請し、顧客がコミュニティメンバーとしてやり取りできるようにすることを目的としたコミュニティサイトです。

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
* スコアとバッジ
* 分析レポート

To experience the ease of quickly creating a new engagement community, visit [Getting Started with AEM Communities](/help/communities/getting-started.md).

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

有効化コミュニティの機能には、次のものがあります。

* [エンゲージメントコミュニティ](#engagement-community)の全機能
* コンテンツと学習リソースをメンバーとメンバーグループに割り当てる機能
* クイズやテストなど SCORM コンテンツに対応
* 割り当て完了のトラッキング
* レポートと分析へのアクセス
* フォーラム、メッセージ、コメントおよび評価を通じ、学習リソースについて話し合う機能

An enablement community may be created when the [Enablement add-on is configured](/help/communities/enablement.md), which requires additional licensing for use in a production environment. An enablement community site will include the [assignments function](#community-functions).

To experience the ease of creating a new enablement community, visit [Getting Started with AEM Communities for Enablement](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machineは](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM Sites [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), Communities Apps, Communities Communities Communities FormsはQuickStartを起動するよりも設定が必要な場合が多い [AEM Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), Demoを管理し、AEM Semo Sites Sites Dem Sitesのデモを実行します。 The AEM Demo Machine will setup additional [infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) such as MongoDB, Solr, MySQL, FFmpeg and email servers.

AEMデモマシンには、次の機能が含まれます。

* a [graphical user interface](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Apache ANT scripts with configurable [properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) and [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* インストール用パッケージ

AEM Demo Machineは、Windows、MacOSおよびLinux上でCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3およびAEM 6.4で正常にテストされました。

AEM Demo Machineには有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント {#aem-communities-documentation}

* Visit [Deploying Communities](/help/communities/deploy-communities.md) to learn about recommended deployments.
* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](/help/communities/administer-landing.md)を参照してください。
* Visit [Developing Communities](/help/communities/communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.
* Visit [Authoring Communities Components](/help/communities/author-communities.md) to learn how to author with and configure Communities components.

