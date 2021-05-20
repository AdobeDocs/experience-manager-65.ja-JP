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
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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

AEM Communitiesは、サイト訪問者との関係を構築します。

* **** ブログ、Q&amp;A、イベントカレンダー、
* **フォーラム、コメント、その他のコミュニティコンテンツを通じてインサイト**&#x200B;を得る間、多くの場合、ユーザー生成コンテンツ(UGC)と呼ばれます。
* パブリッシュ環境で、信頼されたメンバーによる&#x200B;**モデレート**&#x200B;を許可します。
* **twitterと** Facebookとのソーシャルログイン
* **コミュニティ** コンテンツのインライン翻訳
* **公開済みのコミュ** ニティサイトから作成されたコミュニティグループ
* **** バッジを授与する
* **ファイル共有**、
* **** 通知とアクティビティ **ストリーム**
* ユーザー生成コンテンツ内の他の登録済みメンバーに&#x200B;**タグ付け**(@mention)を許可し、メンバーの注意を引き出します。
* イネーブルメントコンポーネント（カタログとコースの再生、割り当て、ファイルライブラリなど）で&#x200B;**キーボードナビゲーション**&#x200B;をサポートします。

Communities の機能は、GitHub.com で公開されている [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)で試すことができます。また、新しい We.Retail のリファレンス実装内でも試すことができます。

## コミュニティサイト  {#community-sites}

コミュニティサイトは、シンプルなウィザードで作成できる AEM サイトです。作成される Web サイトには、数多くの一般的な機能があらかじめ組み込まれています。

[サイト作成ウィザード](/help/communities/sites-console.md):

* 選択した[コミュニティサイトテンプレート](/help/communities/sites.md)に基づいて、サイトの機能を構築します。

   * [コミュニティ機能](#community-functions)から作成したテンプレート
   * オプションの[コミュニティグループ](#communitygroups)機能

* 設定を使用して、次の設定をおこないます。

   * モデレート
   * ログイン
   * 翻訳

* 基本的な機能を提供します。

   * レスポンシブデザイン：[TwitterBootstrapテーマ](https://getbootstrap.com)を使用

   * ログイン：自己登録、[ソーシャルログイン](/help/communities/social-login.md)、ユーザープロファイル

      * 通知：
メンバーは、自分に関連するイベントと、ユーザーが生成したコンテンツを[@mentioned](/help/communities/overview.md#mentionssupport)として参照できます。

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送受信できます。
      * 検索：コミュニティサイト内で検索する機能。
      * 言語の切り替え：[多言語サイト](/help/sites-administering/translation.md)の言語を選択する機能。

      * 管理：コミュニティサイト内のユーザーをモデレートおよび管理する権限を持つメンバーのアクセス権

* ページレベルのオーサリング手順が多くなりません。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能のナビゲーションリンクが提供されます。

新しいコミュニティサイトを簡単に作成するには、[AEM Communitiesの概要](/help/communities/getting-started.md)を参照してください。

## コミュニティコンテンツの永続性 {#community-content-persistence}

AEM Communities でコミュニティコンテンツのパフォーマンスと同期を改善するには、ユーザー生成コンテンツ（UGC）専用の共通ストアを用意し、それをすべての AEM インスタンス（オーサーおよびパブリッシュ）で共有することが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を介して簡単にアクセスできます。SRP はアクセスを基本トポロジから切り離すレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、以下を参照してください。

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md):UGCで使用可能なSRPストレージオプションについて説明します。
* [推奨されるトポロジ](/help/communities/topologies.md)：使用例とSRPの選択に基づくトポロジについて説明します。
* [AEM 6.5 Communitiesへのアップグレード](/help/communities/upgrade.md):AEM 6.5に移行する際のUGCに関する有用な情報を提供します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールから[コミュニティコンソール](/help/communities/consoles.md)にアクセスできます。このコンソールには、次のものが含まれます。

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの作成
   * サイト編集
   * サイト管理
   * [コミュニティグループ](/help/communities/groups.md)コンソール

* [モデレート](/help/communities/moderation.md)コンソール

   * オーサー環境とパブリッシュ環境向けの一般的な一括モデレートUI。
   * 新しいフィルター条件。

* [メンバーおよびグループ](/help/communities/members.md)管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理する機能を提供します。
   * メンバーを禁止する機能を提供します。
   * オーサー環境からパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理する機能を提供します。

* [レポート](/help/communities/reports.md)コンソール

   * 割り当て、投稿および表示に関するレポートを生成できます。

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

   * サイトの[共通ストア](/help/communities/working-with-srp.md)を選択して設定します。

* [コンポーネントガイド](/help/communities/components-guide.md)

   * すべてのコミュニティコンポーネントのサンプルと、それらを使用したデフォルトの設定および実験機能を提供する、サンプルサイト、[コミュニティコンポーネント](https://localhost:4502/editor.html/content/community-components/en.html)。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、任意のサンプルサイトとは独立したコミュニティサイトをすばやく設定するために、コミュニティサイトテンプレートの選択に基づいておこなわれます。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、ログイン、ユーザープロファイル、メッセージング、サイトメニュー、検索、テーマ、ブランディング機能など、コミュニティサイトの構造を提供します。

[サイトテンプレートコンソール](/help/communities/sites.md)を参照してください。

## コミュニティ機能  {#community-functions}

コミュニティに必要とされる機能はだいたい決まっています。AEM Communities では、こうした機能が基本要素として用意されており、「コミュニティ機能」と呼ばれています。

コミュニティ機能とは、通常のAEMページには、コミュニティサイトテンプレートに簡単に組み込める機能にまとめられたコンポーネントが含まれます。

[コミュニティ機能コンソール](/help/communities/functions.md)を参照してください。

## コミュニティグループとグループテンプレート  {#community-groups-and-group-templates}

コミュニティグループ機能を使用すると、許可されたユーザーとコミュニティメンバーが、オーサー環境とパブリッシュ環境の両方からコミュニティサイト内にサブコミュニティを動的に作成できます。

テンプレートの構造に[グループ機能](/help/communities/functions.md#groups-function)が含まれる場合は、オーサー環境から、コミュニティグループ（サブコミュニティ）を既存のコミュニティサイト内に作成したり、既存のグループ内にネストしたりできます。

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 グループ機能をテンプレート構造に追加すると、1つのグループテンプレートを指定するか、新しいコミュニティグループの作成時にテンプレートの選択肢を提供するように設定されます。

関連トピック：

* [サイトグル](/help/communities/groups.md) ープコンソールを使用して、オーサー環境でサブコミュニティを作成できます。
* [グループテンプ](/help/communities/tools-groups.md) レートコンソールを使用して、グループのサイト構造を作成します。
* [ネストされたグループを含む](/help/communities/getting-started.md) コミュニティサイトをすばやく作成するためのチュートリアルについては、 AEM Communitiesの概要を参照してください。

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構成要素である[コミュニティコンポーネント](/help/communities/author-communities.md)は、AEM サイトに Communities 機能を追加するために使用します。

[コミュニティコンポーネントガイド](/help/communities/components-guide.md)では、これらのコンポーネントをインタラクティブに検討できます。

## コミュニティのタイプ  {#types-of-communities}

### Engagement Community {#engagement-community}

エンゲージメントコミュニティは、顧客の情報提供、フィードバックの要請、コミュニティメンバーとしての顧客のインタラクションを可能にする、ユーザーの関心を集めたコミュニティサイトです。

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
* Analyticsレポート

新しいエンゲージメントコミュニティをすばやく簡単に作成するには、[AEM Communitiesの概要](/help/communities/getting-started.md)を参照してください。

### イネーブルメントコミュニティ {#enablement-community}

イネーブルメントコミュニティは、オンライン学習機能を用意したコミュニティサイトです。

イネーブルメントコミュニティの機能には、次のものが含まれます。

* [エンゲージメントコミュニティ](#engagement-community)のすべての機能。
* コンテンツと学習を割り当てる機能メンバーおよびメンバー・グループに対するリソース。
* クイズやテストなど、SCORMコンテンツをサポートします。
* 割り当て完了の追跡。
* Reports &amp; Analyticsにアクセスする。
* フォーラム、メッセージング、コメントおよび評価を通じて学習リソースに関する会話を行う機能。

イネーブルメントコミュニティは、[イネーブルメントアドオンが設定されると作成される場合があります。](/help/communities/enablement.md)には、実稼動環境で使用する追加のライセンスが必要です。 イネーブルメントコミュニティサイトには、[割り当て機能](#community-functions)が含まれます。

新しいイネーブルメントコミュニティを簡単に作成するには、[AEM Communitiesを使い始める](/help/communities/getting-started-enablement.md)を参照してください。

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)は、AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)および[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)のデモを管理および実行します。クイックスタートインスタンスを起動するだけで済みます。 AEM Demo Machineは、MongoDB、Solr、MySQL、FFmpeg、電子メールサーバーなど、追加の[インフラストラクチャ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)を設定します。

AEM Demo Machineには、次の機能が含まれます。

* [グラフィカルユーザーインターフェイス](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 設定可能な[プロパティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)と[ターゲット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)を持つApache ANTスクリプト。

* インストールするパッケージ。

AEM Demo Machineは、Windows、MacOSおよびLinux上のCQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4で正常にテストされました。

AEM Demo Machineには、有効なAEMライセンスが必要です。

>[!NOTE]
>
>AEM Demo Machine の[紹介ビデオ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)を参照してください（13:26）。

## AEM Communities ドキュメント  {#aem-communities-documentation}

* 推奨されるデプロイメントについては、[Communitiesのデプロイ](deploy-communities.md)を参照してください。
* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについては、[コミュニティサイトの管理](administer-landing.md)を参照してください。
* ソーシャルコンポーネントフレームワーク(SCF)とコミュニティのコンポーネントと機能のカスタマイズについては、 [コミュニティの開発](communities.md)を参照してください。
* コミュニティコンポーネントを使用してオーサリングおよび設定する方法については、 [コミュニティコンポーネントのオーサリング](author-communities.md)を参照してください。
