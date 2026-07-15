---
title: AEM Communities の概要
description: Adobe Experience Manager Communitiesの機能と設定の基本について説明します。
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
source-wordcount: '1331'
ht-degree: 2%

---

# AEM Communities の概要 {#aem-communities-overview}

Adobe Experience Manager （AEM） Communitiesを使用すると、パフォーマンスの向上、サイト管理の改善、サイト訪問者の価値あるコミュニティ会員へのコンバージョンを促進するオンプレミスのコミュニティサイトをすばやく作成できます。

## Communities の機能 {#communities-features}

AEM Communitiesは、次のようなサイト訪問者との関係構築を可能にします。

* ブログ、Q&amp;A、イベントカレンダーを通じて&#x200B;**情報**,
* フォーラム、コメント、その他のコミュニティコンテンツを通じて&#x200B;**インサイト**&#x200B;を獲得する方法は、「ユーザー生成コンテンツ」（UGC）と呼ばれることが多いです。
* パブリッシュ環境の信頼できるメンバーによる&#x200B;**モデレーション**&#x200B;が許可されます。
* **TwitterとFacebookのソーシャルログイン**
* コミュニティコンテンツの&#x200B;**インライン翻訳**,
* 公開されたコミュニティサイトから&#x200B;**コミュニティグループの作成**,
* バッジの授与に&#x200B;**スコアリング**,
* **ファイル共有**,
* **通知**&#x200B;および&#x200B;**アクティビティストリーム**,
* ユーザー生成コンテンツ内の&#x200B;**タグ付け** （@mention）の他の登録メンバーに対して、注意を引き出せるようにします。

コミュニティ機能は、GitHub.comで公開されている[AEM デモマシン ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)を使用するか、新しい`We.Retail`参照実装を使用してデモできます。

## コミュニティサイト {#community-sites}

コミュニティサイトは、シンプルなウィザードを使用して作成されたAEM サイトです。その結果、サイトに事前に接続された多くの一般的な機能を備えたweb サイトが作成されます。

[ サイト作成ウィザード ](/help/communities/sites-console.md):

* 選択した[ コミュニティサイトテンプレート ](/help/communities/sites.md)に基づいて、サイトの機能をアセンブリします。

   * [ コミュニティ関数](#community-functions)から作成
   * オプションの[ コミュニティグループ ](#communitygroups)機能

* 設定を使用して設定を行います。

   * モデレーション
   * ログイン
   * 翻訳

* 必須の機能を提供します。

   * レスポンシブデザイン：[Twitter Bootstrap テーマ ](https://getbootstrap.com)を使用

   * ログイン：自己登録、[ ソーシャルログイン ](/help/communities/social-login.md)、ユーザープロファイル

      * 通知：
メンバーは、自分に関連するイベントと、自分が[@mentioned](/help/communities/overview.md#mentionssupport)であるユーザー生成コンテンツを表示します。

      * メッセージ：メンバーは、コミュニティサイト内でメッセージを送受信できます。
      * 検索：コミュニティサイト内で検索する機能。
      * 言語の切り替え：[多言語サイト ](/help/sites-administering/translation.md)の言語を選択できます。

      * 管理：許可されたメンバーがコミュニティサイト内のユーザーを管理および管理するためのアクセス。

* ページレベルのオーサリング作業が大幅に不要になります。

   * ブランディング：コミュニティサイトのすべてのページに表示するためのバナー画像のオプションのアップロード
   * ナビゲーションメニュー：コミュニティサイトテンプレートに含まれる機能には、ナビゲーションリンクが用意されています。

コミュニティサイトをすばやく簡単に作成する方法については、[AEM Communitiesの概要](/help/communities/getting-started.md)を参照してください。

## コミュニティコンテンツの永続性 {#community-content-persistence}

コミュニティコンテンツのパフォーマンスと同期性を向上させるために、AEM Communitiesでは、すべてのAEM（オーサーインスタンスとパブリッシュ インスタンス）間で共有されるユーザー生成コンテンツ（UGC）専用の共通ストアが必要です。

コミュニティコンテンツは、ストレージリソースプロバイダー（SRP）を通じて簡単にアクセスできます。SRPは、基盤となるトポロジからのアクセスを分離するレイヤーを提供し、UGC用の共通ストアをサポートします。

コミュニティコンテンツの永続性と推奨されるデプロイメントについて詳しくは、次を参照してください。

* [ コミュニティコンテンツストレージ ](/help/communities/working-with-srp.md):UGCで使用可能なSRP ストレージオプションについて説明します。
* [推奨トポロジ ](/help/communities/topologies.md)：ユースケースとSRPの選択に基づいてトポロジについて説明します。
* [AEM 6.5 Communities](/help/communities/upgrade.md)へのアップグレード - AEM 6.5への移行時にUGCに関する有益な情報を提供します。

## コミュニティコンソール {#communities-consoles}

オーサー環境では、グローバルナビゲーションコンソールによって[Communities コンソール ](/help/communities/consoles.md)にアクセスできます。これには次のものが含まれます。

* [サイト](/help/communities/sites-console.md)コンソール

   * サイトの構築
   * サイト編集
   * サイト管理
   * [ コミュニティグループ ](/help/communities/groups.md) コンソール

* [ モデレーション ](/help/communities/moderation.md) コンソール

   * オーサー環境とパブリッシュ環境の一般的な一括モデレーション UI。
   * 新しいフィルタリング条件。

* [ メンバーとグループ ](/help/communities/members.md)管理コンソール

   * オーサー環境からパブリッシュサイドユーザー（メンバー）を作成および管理できます。
   * メンバーを禁止できます。
   * オーサー環境からパブリッシュサイドのユーザーグループ（メンバーグループ）を作成および管理できます。

* [Reports](/help/communities/reports.md) コンソール

   * 割り当て、投稿、ビューに関するレポートを生成できます。

グローバルツールコンソールでは、次のコミュニティツールにアクセスできます。

* [ サイトテンプレート ](/help/communities/tools.md#sitetemplatesconsole) コンソール

   * コミュニティサイトテンプレートの作成と管理。

* [ テンプレートをグループ ](/help/communities/tools.md#grouptemplatesconsole) コンソール

   * コミュニティグループテンプレートの作成と管理。

* [ コミュニティ関数](/help/communities/tools.md#communityfunctionsconsole) コンソール

   * コミュニティ機能の作成と管理：

* [ ストレージ設定](/help/communities/tools.md#storageconfiguratonconsole) コンソール

   * サイトの[共通ストア ](/help/communities/working-with-srp.md)を選択して設定します。

* [コンポーネントガイド](/help/communities/components-guide.md)

   * サンプルサイト「[ コミュニティコンポーネント ](https://localhost:4502/editor.html/content/community-components/en.html)」では、すべてのコミュニティコンポーネントのサンプルを、デフォルト設定とそれらをテストする機能とともに提供します。

## コミュニティサイトテンプレート {#community-site-templates}

コミュニティサイト作成は、コミュニティサイトテンプレートの選択に基づいて作成され、サンプルサイトから独立したコミュニティサイトを迅速に設定します。

コミュニティ機能とコミュニティグループテンプレートで構成されるコミュニティサイトテンプレートは、コミュニティサイトの構造を提供します。 ログイン機能、ユーザープロファイル、メッセージ機能、サイトメニュー、検索機能、テーマ機能、ブランディング機能などが含まれます。

[ サイトテンプレートコンソール ](/help/communities/sites.md)を参照してください。

## コミュニティ機能 {#community-functions}

コミュニティ体験に期待される機能は周知の事実。 AEM Communitiesでは、これらの機能はコミュニティ関数と呼ばれる構成要素として利用できます。

コミュニティ機能は通常のAEM ページで、コミュニティサイトテンプレートに簡単に組み込まれる機能にコンポーネントが一緒に接続されています。

[ コミュニティ機能コンソール ](/help/communities/functions.md)を参照してください。

## コミュニティグループとグループテンプレート {#community-groups-and-group-templates}

コミュニティグループ機能は、オーサー環境とパブリッシュ環境の両方から許可されたユーザーとコミュニティメンバーが、コミュニティサイト内でサブコミュニティを動的に作成する機能です。

オーサー環境から、テンプレートの構造に[Groups関数](/help/communities/functions.md#groups-function)が含まれている場合、コミュニティグループ（サブコミュニティ）を既存のコミュニティサイト内に作成したり、既存のグループ内にネストしたりできます。

コミュニティグループを作成するには、コミュニティグループページのデザインを提供するコミュニティグループテンプレートを選択する必要があります。 グループ関数がテンプレート構造に追加される場合、1つのグループテンプレートを指定するか、新しいコミュニティグループの作成時にテンプレートの選択肢を提供するように設定されます。

関連トピック：

* オーサー環境でサブコミュニティを作成するための[ サイトグループコンソール ](/help/communities/groups.md)。
* グループ用のサイト構造を作成するための[ グループテンプレートコンソール ](/help/communities/tools-groups.md)。
* ネストされたグループを含むコミュニティサイトをすばやく作成するためのチュートリアルについては、[AEM Communitiesの基本を学ぶ](/help/communities/getting-started.md)を参照してください。

## コミュニティコンポーネント {#community-components}

コミュニティサイトが構築されている[ コミュニティコンポーネント ](/help/communities/author-communities.md)は、AEM サイトにコミュニティ機能を追加するために使用できます。

[ コミュニティコンポーネントガイド ](/help/communities/components-guide.md)は、コンポーネントのインタラクティブな探索に使用できます。

## エンゲージメントコミュニティ {#engagement-community}

エンゲージメントコミュニティとは、顧客に情報を提供し、フィードバックを求め、顧客がコミュニティメンバーとして交流できるようにすることに重点を置いたコミュニティサイトです。

エンゲージメントコミュニティの機能には、次のようなものがあります。

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
* 分析レポート

エンゲージメントコミュニティをすばやく簡単に構築する方法については、[AEM Communitiesの概要](/help/communities/getting-started.md)をご覧ください。

## AEMのデモマシン {#aem-demo-machine}

[AEM デモマシン ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)は、AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)および[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)のデモを管理および実行します。多くの場合、QuickStart インスタンスを起動するよりも多くの設定が必要です。 AEMのデモマシンは、MongoDB、Solr、MySQL、FFmpeg、メールサーバーなど、追加の[ インフラストラクチャ ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)を設定します。

AEMのデモマシンには、以下が含まれます。

* [ グラフィカルユーザーインターフェイス ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 設定可能な[ プロパティ ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)と[ ターゲット ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)を含むApache ANT スクリプト。

* インストールするパッケージ。

AEMのデモマシンは、CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3、AEM 6.4でWindows、macOS、Linux®で正常にテストされました。

AEM デモマシンには、有効なAEM ライセンスが必要です。

>[!NOTE]
>
>AEM デモマシン （13:26）に関する[ ビデオの概要](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be)を表示します。

## AEM Communities Documentation {#aem-communities-documentation}

* [ コミュニティのデプロイ ](deploy-communities.md)にアクセスすると、推奨されるデプロイメントについて確認できます。
* [ コミュニティサイトの管理](administer-landing.md)にアクセスして、コミュニティサイトの作成、コミュニティグループの追加、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレーション、メンバーの管理、タグ付け、通知、スコアリング、バッジについて学ぶことができます。
* [ コミュニティの開発](communities.md)にアクセスして、ソーシャルコンポーネントフレームワーク（SCF）とコミュニティのコンポーネントと機能のカスタマイズについて学ぶことができます。
* [Communities コンポーネントのオーサリング ](author-communities.md)にアクセスして、Communities コンポーネントのオーサリングと設定方法を学ぶことができます。
