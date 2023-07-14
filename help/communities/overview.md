---
title: AEM Communities の概要
description: AEM Communitiesの機能とセットアップの概要
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 2%

---

# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager(AEM)Communities を使用すると、パフォーマンスの向上、サイト管理の向上、貴重なコミュニティメンバーへのサイト訪問者の転換を促すオンプレミスのコミュニティサイトを迅速に作成できます。

## Communities の機能 {#communities-features}

AEM Communitiesを使用すると、サイト訪問者との関係を構築できます。次の機能があります。

* **通知** ブログ、Q&amp;A、イベントカレンダーを通じて
* While **洞察を得る** フォーラム、コメント、その他のコミュニティコンテンツを通じて、多くの場合、ユーザー生成コンテンツ (UGC) と呼ばれます。
* 可能です **モデレート** パブリッシュ環境の信頼できるメンバーによる
* **ソーシャルログイン** twitterとFacebookと
* **インライン翻訳** コミュニティコンテンツの
* **コミュニティグループの作成** 公開されたコミュニティサイトから
* **スコア** バッジを授与する
* **ファイル共有**,
* **通知** および **アクティビティストリーム**,
* 許可 **タグ付け** (@mention) ユーザー生成コンテンツに登録された他のメンバーの注意を引くため。

コミュニティの機能は、 [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) GitHub.com で公開されている、または新しい We.Retail 参照実装で使用できます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、簡単なウィザードを使用して作成されたAEMサイトで、多くの共通機能があらかじめサイトに組み込まれた Web サイトになります。

この [サイト作成ウィザード](/help/communities/sites-console.md):

* 選択したに基づいてサイトの機能を構築します [コミュニティサイトテンプレート](/help/communities/sites.md) 例：

   * 次の場所から作成 [コミュニティ機能](#community-functions)
   * オプション [コミュニティグループ](#communitygroups) 機能

* 設定を使用して次の設定を行います。

   * モデレート
   * ログイン
   * 翻訳

* 基本的な機能を提供します。

   * レスポンシブデザイン：uses [TwitterBootstrapテーマ](https://getbootstrap.com)

   * ログイン：自己登録 [ソーシャルログイン](/help/communities/social-login.md)、ユーザープロファイル

      * 通知：メンバーは、自分に関連するイベントや、自分が属する場所でユーザーが生成したコンテンツを見ることができます。 [@mentioned](/help/communities/overview.md#mentionssupport).

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送受信できます。
      * 検索：コミュニティサイト内での検索機能
      * 言語の切り替え：言語を選択する機能 [多言語サイト](/help/sites-administering/translation.md).

      * 管理：コミュニティサイト内のユーザーをモデレートおよび管理する権限を持つメンバーのアクセス権。

* 次の多くのページレベルのオーサリング手順を排除：

   * ブランディング：コミュニティサイトのすべてのページに表示するバナー画像のオプションアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能に対してナビゲーションリンクが提供されます。

簡単にコミュニティサイトを簡単に作成するには、 [AEM Communitiesの概要](/help/communities/getting-started.md).

## コミュニティコンテンツの持続性 {#community-content-persistence}

コミュニティコンテンツのパフォーマンスと同期を向上させるために、AEM Communitiesには、すべてのAEM（オーサーおよびパブリッシュ）インスタンス間で共有される、ユーザー生成コンテンツ (UGC) 用の共通ストアが必要です。

コミュニティコンテンツには、ストレージリソースプロバイダー (SRP) を通じて簡単にアクセスできます。SRP は、基になるトポロジとは別にアクセスするためのレイヤーを提供し、UGC 用の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、以下を参照してください。

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md)- UGC で使用可能な SRP ストレージオプションについて説明します。
* [推奨されるトポロジ](/help/communities/topologies.md)：使用例と SRP の選択に基づくトポロジについて説明します。
* [AEM 6.5 Communities へのアップグレード](/help/communities/upgrade.md)- AEM 6.5 に移行する際の UGC に関する有用な情報を提供します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールから [コミュニティコンソール](/help/communities/consoles.md)（次を含む）:

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの作成
   * サイト編集
   * サイト管理
   * [コミュニティグループ](/help/communities/groups.md) コンソール

* [モデレート](/help/communities/moderation.md) コンソール

   * オーサー環境およびパブリッシュ環境向けの一般的な一括モデレート UI です。
   * 新しいフィルター条件。

* [メンバーとグループ](/help/communities/members.md) 管理コンソール

   * オーサー環境からパブリッシュ側のユーザー（メンバー）を作成および管理する機能を提供します。
   * メンバーを禁止する機能を提供します。
   * オーサー環境からパブリッシュ側のユーザーグループ（メンバーグループ）を作成および管理する機能を提供します。

* [レポート](/help/communities/reports.md) コンソール

   * 割り当て、投稿、表示に関するレポートを生成できます。

グローバルツールコンソールから、次のコミュニティツールにアクセスできます。

* [サイトテンプレート](/help/communities/tools.md#sitetemplatesconsole) コンソール

   * コミュニティサイトテンプレートを作成および管理します。

* [グループテンプレート](/help/communities/tools.md#grouptemplatesconsole) コンソール

   * コミュニティグループテンプレートを作成および管理します。

* [コミュニティ機能](/help/communities/tools.md#communityfunctionsconsole) コンソール

   * コミュニティ機能を作成および管理します。

* [ストレージ設定](/help/communities/tools.md#storageconfiguratonconsole) コンソール

   * を選択して設定します。 [共通店](/help/communities/working-with-srp.md) サイトの

* [コンポーネントガイド](/help/communities/components-guide.md)

   * サンプルサイト [コミュニティコンポーネント](https://localhost:4502/editor.html/content/community-components/en.html) では、すべてのコミュニティコンポーネントのサンプルをデフォルトの設定と、それらを使用した実験が可能です。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイトの作成は、サンプルサイトとは独立したコミュニティサイトをすばやく設定するために、コミュニティサイトテンプレートの選択に基づいておこなわれます。

コミュニティサイトテンプレートは、コミュニティ機能とコミュニティグループテンプレートで構成され、ログイン、ユーザープロファイル、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトの構造を提供します。

詳しくは、 [サイトテンプレートコンソール](/help/communities/sites.md).

## コミュニティ機能 {#community-functions}

コミュニティ体験で期待される機能は、よく知られています。 AEM Communitiesでは、これらの機能はコミュニティ機能と呼ばれる構築ブロックとして使用できます。

コミュニティ機能は、通常のAEMページで、コミュニティサイトテンプレートに簡単に組み込むことのできる機能内に組み込まれたコンポーネントを含みます。

詳しくは、 [コミュニティ機能コンソール](/help/communities/functions.md).

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能を使用すると、許可されたユーザーとコミュニティメンバーがオーサー環境とパブリッシュ環境の両方からコミュニティサイト内にサブコミュニティを動的に作成できます。

テンプレートの構造に [グループ機能](/help/communities/functions.md#groups-function).

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 グループ機能をテンプレート構造に追加すると、1 つのグループテンプレートを指定するか、新しいコミュニティグループの作成時にテンプレートの選択肢を提供するように設定されます。

関連トピック：

* [サイトグループコンソール](/help/communities/groups.md) オーサー環境でサブコミュニティを作成する場合。
* [グループテンプレートコンソール](/help/communities/tools-groups.md) グループのサイト構造を作成する場合。
* [AEM Communitiesの概要](/help/communities/getting-started.md) ネストされたグループを含むコミュニティサイトをすばやく作成するためのチュートリアルです。

## コミュニティコンポーネント {#community-components}

この [コミュニティコンポーネント](/help/communities/author-communities.md) コミュニティサイトを構築する際に、AEMサイトにコミュニティ機能を追加する際に使用できます。

この [コミュニティコンポーネントガイド](/help/communities/components-guide.md) は、コンポーネントをインタラクティブに調査するために使用できます。

## Engagement Community {#engagement-community}

エンゲージメントコミュニティとは、顧客のエンゲージメントに焦点を当てたコミュニティサイトで、顧客に対して、情報を提供し、フィードバックを提供し、顧客がコミュニティメンバーとしてやり取りできるようにします。

エンゲージメントコミュニティの機能には次のものが含まれます。

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
* Analytics レポート

エンゲージメントコミュニティを素早く簡単に作成するには、次を参照してください。 [AEM Communitiesの概要](/help/communities/getting-started.md).

## AEM Demo Machine {#aem-demo-machine}

この [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEMのデモを管理および実行します [サイト](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [コミュニティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [アプリ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) および [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)（多くの場合、クイックスタートインスタンスを起動するよりも多くの設定が必要です）。 AEM Demo Machine が追加の [インフラ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) （MongoDB、Solr、MySQL、FFmpeg、電子メールサーバーなど）。

AEM Demo Machine には、以下が含まれます。

* A [グラフィカルユーザーインターフェイス](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 設定可能な Apache ANT スクリプト [プロパティ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) および [ターゲット](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* インストールするパッケージ。

AEM Demo Machine は、Windows、MacOS、および Linux®上で CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4 で正常にテストされました。

AEM Demo Machine には、有効なAEMライセンスが必要です。

>[!NOTE]
>
>表示 [ビデオの紹介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) をAEM Demo Machine (13:26)に追加します。

## AEM Communities Documentation {#aem-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照して、推奨されるデプロイメントについて確認してください。
* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、タグ付け、通知、スコア付け、バッジについて説明します。
* 訪問 [コミュニティの開発](communities.md) ソーシャルコンポーネントフレームワーク (SCF) と、コミュニティのコンポーネントと機能のカスタマイズについて説明します。
* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
