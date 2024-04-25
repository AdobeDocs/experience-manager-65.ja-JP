---
title: AEM Communities の概要
description: Adobe Experience Manager Communities の機能と設定の基礎について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager（AEM） Communities を使用すると、パフォーマンスとサイト管理を向上させ、サイト訪問者を価値のあるコミュニティメンバーに変換することを促すオンプレミスコミュニティサイトをすばやく作成できます。

## Communities の機能 {#communities-features}

AEM Communitiesを使用すると、次のようなサイト訪問者との関係を構築できます。

* **通知** ブログ、Q&amp;A、イベントカレンダーにより、
* While **インサイトの獲得** フォーラム、コメント、その他のコミュニティコンテンツ（多くの場合、ユーザー生成コンテンツ（UGC）と呼ばれます）を通じて。
* 次の操作が可能です **中和** パブリッシュ環境の信頼されたメンバーによって、
* **ソーシャルログイン** twitterとFacebookにより、
* **インライン翻訳** コミュニティコンテンツの、
* **コミュニティグループの作成** 公開されたコミュニティサイトから、
* **スコアリング** バッジを付与するには、
* **ファイル共有**,
* **通知** および **アクティビティストリーム**,
* を許可 **タギング** （@mention）ユーザー生成コンテンツの他の登録メンバーが注目を集める。

Communities の機能は、 [AEM デモマシン](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) GitHub.comまたは新しいで公開されています `We.Retail` のリファレンス実装。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードを使用して作成されたAEM サイトであり、サイトに事前接続された多くの一般的な機能を備えた web サイトになります。

この [サイト作成ウィザード](/help/communities/sites-console.md):

* 選択されたに基づいて、サイトの機能を組み立てます [コミュニティサイトテンプレート](/help/communities/sites.md) これは次のとおりです。

   * 作成元 [コミュニティ機能](#community-functions)
   * optional [コミュニティグループ](#communitygroups) 機能

* 設定を使用して以下を設定します。

   * 中和
   * ログイン
   * 翻訳

* 次の基本的な機能を提供します。

   * レスポンシブデザイン：使用 [TwitterBootstrapテーマ](https://getbootstrap.com)

   * ログイン：セルフ登録、 [ソーシャルログイン](/help/communities/social-login.md)、ユーザープロファイル

      * 通知：メンバーには、自分に関連するイベントや、自分がいる場所にあるユーザー生成コンテンツが表示されます [@mentioned](/help/communities/overview.md#mentionssupport).

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送受信できます。
      * 検索：コミュニティサイト内を検索する機能。
      * 言語切り替え：の言語を選択する機能 [多言語サイト](/help/sites-administering/translation.md).

      * 管理：権限のあるメンバーがコミュニティサイト内のユーザーを管理および管理するためのアクセス権。

* 多くのページレベルのオーサリング手順が不要になります。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションのアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能へのナビゲーションリンクが提供されます。

コミュニティサイトをすばやく簡単に作成する方法については、次を参照してください。 [AEM Communitiesの概要](/help/communities/getting-started.md).

## コミュニティコンテンツの永続性 {#community-content-persistence}

コミュニティコンテンツのパフォーマンスと同期を向上させるために、AEM Communitiesには、すべてのAEM（オーサーおよびパブリッシュ）インスタンス間で共有されるユーザー生成コンテンツ（UGC）専用の共通ストアが必要です。

コミュニティコンテンツには、ストレージリソースプロバイダー（SRP）を通じて簡単にアクセスできます。SRP は、基盤となるトポロジからのアクセスを分離するレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、以下を参照してください。

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md)—UGC で利用可能な SRP ストレージオプションについて説明します。
* [推奨されるトポロジ](/help/communities/topologies.md) – 使用事例と SRP の選択に基づいてトポロジについて説明します。
* [AEM 6.5 Communities へのアップグレード](/help/communities/upgrade.md)- AEM 6.5 への移行時の UGC に関する有用な情報を提供します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールを使用して、以下にアクセスできます。 [コミュニティコンソール](/help/communities/consoles.md)。次を含みます。

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの作成
   * サイト編集
   * サイト管理
   * [コミュニティグループ](/help/communities/groups.md) コンソール

* [モデレート](/help/communities/moderation.md) コンソール

   * オーサー環境とパブリッシュ環境向けの共通の一括モデレート UI。
   * 新しいフィルター条件。

* [メンバーとグループ](/help/communities/members.md) 管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理できます。
   * メンバーを禁止できます。
   * オーサー環境でパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理できます。

* [報告書](/help/communities/reports.md) コンソール

   * 割り当て、投稿、ビューに関するレポートを生成できます。

グローバルツールコンソールを使用すると、次の Communities ツールにアクセスできます。

* [サイトテンプレート](/help/communities/tools.md#sitetemplatesconsole) コンソール

   * コミュニティサイトテンプレートを作成および管理します。

* [グループテンプレート](/help/communities/tools.md#grouptemplatesconsole) コンソール

   * コミュニティグループテンプレートを作成および管理します。

* [コミュニティ機能](/help/communities/tools.md#communityfunctionsconsole) コンソール

   * コミュニティ機能を作成および管理します。

* [ストレージ設定](/help/communities/tools.md#storageconfiguratonconsole) コンソール

   * を選択して設定します。 [共通店舗](/help/communities/working-with-srp.md) サイト用。

* [コンポーネントガイド](/help/communities/components-guide.md)

   * サンプルサイト： [コミュニティコンポーネント](https://localhost:4502/editor.html/content/community-components/en.html) には、すべての Communities コンポーネントのサンプルが含まれています。デフォルトの設定に加えて、それらを使用して実験する機能も示されています。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、任意のサンプルサイトに依存しないコミュニティサイトをすばやく設定するために、コミュニティサイトテンプレートを選択することに基づいています。

コミュニティサイトテンプレートは、コミュニティ機能とコミュニティグループテンプレートで構成され、コミュニティサイトの構造を提供します。 ログイン、ユーザープロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディングなどの機能が含まれます。

を参照してください。 [サイトテンプレートコンソール](/help/communities/sites.md).

## コミュニティ機能 {#community-functions}

コミュニティエクスペリエンスに期待される機能はよく知られています。 AEM Communitiesでは、これらの機能はコミュニティ機能と呼ばれる構築ブロックとして使用できます。

コミュニティ機能は、通常のAEM ページに含まれるコンポーネントがワイヤリングされて、コミュニティサイトテンプレートに簡単に組み込まれる機能になります。

を参照してください。 [コミュニティ機能コンソール](/help/communities/functions.md).

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、オーサー環境とパブリッシュ環境の両方から許可されたユーザーとコミュニティメンバーによって、コミュニティサイト内にサブコミュニティを動的に作成する機能です。

テンプレートの構造にを含む場合、オーサー環境では既存のコミュニティサイト内にコミュニティグループ（サブコミュニティ）を作成したり、既存のグループ内にネストしたりできます [Groups 関数](/help/communities/functions.md#groups-function).

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にグループ機能を追加すると、グループテンプレートを 1 つ指定するように設定されるか、新しいコミュニティグループを作成するときにテンプレートの選択を提供します。

関連トピック：

* [サイトグループコンソール](/help/communities/groups.md) オーサー環境でサブコミュニティを作成する場合。
* [グループテンプレートコンソール](/help/communities/tools-groups.md) グループのサイト構造を作成する場合
* [AEM Communitiesの概要](/help/communities/getting-started.md) ネストされたグループを含むコミュニティサイトをすばやく作成するためのチュートリアル。

## コミュニティコンポーネント {#community-components}

この [コミュニティコンポーネント](/help/communities/author-communities.md) コミュニティサイトの構築元を使用して、任意のAEM サイトにコミュニティ機能を追加できます。

この [コミュニティコンポーネントガイド](/help/communities/components-guide.md) は、コンポーネントのインタラクティブな探索に使用できます。

## エンゲージメントコミュニティ {#engagement-community}

エンゲージメントコミュニティは、顧客に情報を提供したり、フィードバックを求めたり、顧客がコミュニティメンバーとしてやり取りできるようにしたりすることに重点を置いたコミュニティサイトです。

エンゲージメントコミュニティの機能には、次のものが含まれます。

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
* スコアおよびバッジ
* Analytics レポート

エンゲージメントコミュニティをすばやく簡単に作成する方法については、を参照してください。 [AEM Communitiesの概要](/help/communities/getting-started.md).

## AEM デモマシン {#aem-demo-machine}

この [AEM デモマシン](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEMのデモの管理と実行 [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [アセット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [コミュニティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [アプリ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) および [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)（多くの場合、QuickStart インスタンスを起動するよりも詳細なセットアップが必要です）。 AEM デモマシンで追加の設定が行われます [インフラ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 例えば、MongoDB、Solr、MySQL、FFmpeg、メールサーバーなどです。

AEM デモマシンには以下が含まれます。

* A [グラフィカルユーザーインターフェイス](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 設定可能なを使用した Apache ANT スクリプト [プロパティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) および [ターゲット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* インストールするパッケージ。

AEM デモマシンは、Windows、macOS、Linux® で、CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4 を使用してテストされました。

AEM デモマシンには有効なAEM ライセンスが必要です。

>[!NOTE]
>
>を表示 [ビデオの紹介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) AEM デモマシンに移動（13:26）。

## AEM Communities ドキュメント {#aem-communities-documentation}

* 訪問 [Communities のデプロイ](deploy-communities.md) 推奨されるデプロイメントについて説明します。
* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコアおよびバッジについて説明します。
* 訪問 [コミュニティの開発](communities.md) ここでは、ソーシャルコンポーネントフレームワーク（SCF）と、Communities のコンポーネントや機能のカスタマイズについて説明します。
* 訪問 [Communities コンポーネントのオーサリング](author-communities.md) コミュニティのコンポーネントを使用してオーサリングおよび設定する方法について説明します。
