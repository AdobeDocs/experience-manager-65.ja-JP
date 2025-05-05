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

* ブログ、Q&amp;A、イベントカレンダーを通じた **通知**
* フォーラム、コメント、その他のコミュニティコンテンツを通じて **インサイトを得る** 一方で、多くの場合、ユーザー生成コンテンツ（UGC）と呼ばれます。
* これにより、Publish環境の信頼できるメンバーによる **モデレート** が可能になります。
* **ソーシャルログイン**:TwitterとFacebook、
* コミュニティコンテンツの **インライン翻訳**、
* 公開されたコミュニティサイトからの **コミュニティグループの作成**、
* バッジを付与する **スコア付け**、
* **ファイル共有**、
* **通知** および **アクティビティストリーム**、
* ユーザー作成コンテンツ内の他の登録メンバーが **タグ付け** （@mention）して注意を引くことを許可します。

Communities の機能は、GitHub.comで公開されている [AEM デモマシン ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) を使用して、または新しい `We.Retail` リファレンス実装を使用してデモできます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードを使用して作成されたAEM サイトであり、サイトに事前接続された多くの一般的な機能を備えた web サイトになります。

[ サイト作成ウィザード ](/help/communities/sites-console.md):

* 選択した [ コミュニティサイトテンプレート ](/help/communities/sites.md) に基づいて、サイトの機能を組み立てます。

   * [ コミュニティ関数 ](#community-functions) から構築
   * オプション [ コミュニティグループ ](#communitygroups) 機能

* 設定を使用して以下を設定します。

   * 中和
   * ログイン
   * 翻訳

* 次の基本的な機能を提供します。

   * レスポンシブデザイン：[TwitterのBootstrapテーマを使用 ](https://getbootstrap.com)

   * ログイン：セルフ登録、[ ソーシャルログイン ](/help/communities/social-login.md)、ユーザープロファイル

      * 通知：
メンバーには、自分に関連するイベントや、自分が [@mentioned](/help/communities/overview.md#mentionssupport) であるユーザー生成コンテンツが表示されます。

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送受信できます。
      * 検索：コミュニティサイト内を検索する機能。
      * 言語切り替え：[ 多言語サイト ](/help/sites-administering/translation.md) の言語を選択する機能。

      * 管理：権限のあるメンバーがコミュニティサイト内のユーザーを管理および管理するためのアクセス権。

* 多くのページレベルのオーサリング手順が不要になります。

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションのアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能へのナビゲーションリンクが提供されます。

コミュニティサイトをすばやく簡単に作成する方法については、[AEM Communitiesの基本を学ぶ ](/help/communities/getting-started.md) を参照してください。

## コミュニティコンテンツの永続性 {#community-content-persistence}

コミュニティコンテンツのパフォーマンスと同期を向上させるために、AEM Communitiesには、すべてのAEM（オーサーおよびパブリッシュ）インスタンス間で共有されるユーザー生成コンテンツ（UGC）専用の共通ストアが必要です。

コミュニティコンテンツには、ストレージリソースプロバイダー（SRP）を通じて簡単にアクセスできます。SRP は、基盤となるトポロジからのアクセスを分離するレイヤーを提供し、UGC の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、以下を参照してください。

* [ コミュニティ・コンテンツ・ストレージ ](/help/communities/working-with-srp.md):UGC で利用可能な SRP ストレージ・オプションについて説明します。
* [ 推奨トポロジ ](/help/communities/topologies.md) - ユースケースと SRP の選択に基づいてトポロジについて説明します。
* [AEM 6.5 Communities へのアップグレード ](/help/communities/upgrade.md) - AEM 6.5 への移行時の UGC に関する役に立つ情報を提供します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールを使用して、以下を含む [Communities コンソール ](/help/communities/consoles.md) にアクセスできます。

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの作成
   * サイト編集
   * サイト管理
   * [ コミュニティグループ ](/help/communities/groups.md) コンソール

* [ モデレート ](/help/communities/moderation.md) コンソール

   * オーサー環境およびPublish環境向けの共通の一括モデレート UI。
   * 新しいフィルター条件。

* [ メンバーおよびグループ ](/help/communities/members.md) 管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理できます。
   * メンバーを禁止できます。
   * オーサー環境でパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理できます。

* [ レポート ](/help/communities/reports.md) コンソール

   * 割り当て、投稿、ビューに関するレポートを生成できます。

グローバルツールコンソールを使用すると、次の Communities ツールにアクセスできます。

* [ サイトテンプレート ](/help/communities/tools.md#sitetemplatesconsole) コンソール

   * コミュニティサイトテンプレートを作成および管理します。

* [ グループテンプレート ](/help/communities/tools.md#grouptemplatesconsole) コンソール

   * コミュニティグループテンプレートを作成および管理します。

* [ コミュニティ機能 ](/help/communities/tools.md#communityfunctionsconsole) コンソール

   * コミュニティ機能を作成および管理します。

* [ ストレージ設定 ](/help/communities/tools.md#storageconfiguratonconsole) コンソール

   * サイトの [ 共通ストア ](/help/communities/working-with-srp.md) を選択して設定します。

* [コンポーネントガイド](/help/communities/components-guide.md)

   * サンプルサイト [ コミュニティコンポーネント ](https://localhost:4502/editor.html/content/community-components/en.html) では、すべての Communities コンポーネントのサンプルを提供しています。デフォルトの設定と、それらを使用した実験機能が含まれています。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、任意のサンプルサイトに依存しないコミュニティサイトをすばやく設定するために、コミュニティサイトテンプレートを選択することに基づいています。

コミュニティサイトテンプレートは、コミュニティ機能とコミュニティグループテンプレートで構成され、コミュニティサイトの構造を提供します。 ログイン、ユーザープロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディングなどの機能が含まれます。

[ サイトテンプレートコンソール ](/help/communities/sites.md) を参照してください。

## コミュニティ機能 {#community-functions}

コミュニティエクスペリエンスに期待される機能はよく知られています。 AEM Communitiesでは、これらの機能はコミュニティ機能と呼ばれる構築ブロックとして使用できます。

コミュニティ機能は、通常のAEM ページに含まれるコンポーネントがワイヤリングされて、コミュニティサイトテンプレートに簡単に組み込まれる機能になります。

[ コミュニティ関数コンソール ](/help/communities/functions.md) を参照してください。

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、オーサー環境とパブリッシュ環境の両方から許可されたユーザーとコミュニティメンバーによって、コミュニティサイト内にサブコミュニティを動的に作成する機能です。

テンプレートの構造に [Groups 関数 ](/help/communities/functions.md#groups-function) が含まれている場合、オーサー環境では、コミュニティグループ（サブコミュニティ）は既存のコミュニティサイト内に作成されるか、既存のグループ内にネストされます。

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 テンプレート構造にグループ機能を追加すると、グループテンプレートを 1 つ指定するように設定されるか、新しいコミュニティグループを作成するときにテンプレートの選択を提供します。

関連トピック：

* [ サイトグループコンソール ](/help/communities/groups.md)：オーサー環境でサブコミュニティを作成します。
* [ グループテンプレートコンソール ](/help/communities/tools-groups.md)：グループのサイト構造を作成します。
* ネストされたグループを含むコミュニティサイトをすばやく作成するためのチュートリアル用 [AEM Communitiesの基本を学ぶ ](/help/communities/getting-started.md)。

## コミュニティコンポーネント {#community-components}

コミュニティサイトの構築元となる [ コミュニティコンポーネント ](/help/communities/author-communities.md) を使用して、任意のAEM サイトにコミュニティ機能を追加できます。

[ コミュニティコンポーネントガイド ](/help/communities/components-guide.md) は、コンポーネントをインタラクティブに探索するために使用できます。

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

エンゲージメントコミュニティをすばやく簡単に作成する方法については、[AEM Communitiesの基本を学ぶ ](/help/communities/getting-started.md) を参照してください。

## AEM デモマシン {#aem-demo-machine}

[AEM デモマシン ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) は、AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets) [、&lbrace;Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities) [、&lbrace; アプリ ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)、[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms) のデモを管理および実行します。多くの場合、QuickStart インスタンスを起動するだけよりも多くの設定が必要です。 AEM デモマシンで、MongoDB、Solr、MySQL、FFmpeg、メールサーバーなど [&#128279;](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 追加の  インフラストラクチャを設定します。

AEM デモマシンには以下が含まれます。

* [ グラフィカルユーザーインターフェイス ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 設定可能な [ プロパティ ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) および [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) を持つ Apache ANT スクリプト

* インストールするパッケージ。

AEM デモマシンは、Windows、macOS、Linux® で、CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4 を使用してテストされました。

AEM デモマシンには有効なAEM ライセンスが必要です。

>[!NOTE]
>
>AEM デモマシンの [ ビデオの紹介 ](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) を表示します（13:26）。

## AEM Communities ドキュメント {#aem-communities-documentation}

* 推奨されるデプロイメントについて詳しくは、[Communities のデプロイ ](deploy-communities.md) を参照してください。
* コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツの管理、メンバーの管理、タグ付け、通知、スコアリング、バッジについて詳しくは、[ コミュニティサイトの管理 ](administer-landing.md) を参照してください。
* [ コミュニティの開発 ](communities.md) を参照して、ソーシャルコンポーネントフレームワーク（SCF）と、コミュニティのコンポーネントや機能のカスタマイズについて学ぶことができます。
* Communities コンポーネントを使用してオーサリングする方法と設定する方法については、[Communities コンポーネントのオーサリング ](author-communities.md) を参照してください。
