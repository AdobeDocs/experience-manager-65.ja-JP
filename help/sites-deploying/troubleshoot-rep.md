---
title: レプリケーションのトラブルシューティング
seo-title: レプリケーションのトラブルシューティング
description: この記事では、レプリケーションに関する問題のトラブルシューティング方法について説明します。
seo-description: この記事では、レプリケーションに関する問題のトラブルシューティング方法について説明します。
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 67%

---


# レプリケーションのトラブルシューティング{#troubleshooting-replication}

このページでは、レプリケーションに関する問題のトラブルシューティング方法について説明します。

## 問題 {#problem}

レプリケーション（順方向のレプリケーション）が何らかの原因で失敗する

## 解像度 {#resolution}

レプリケーションが失敗するのには様々な原因があります。ここでは、これらの問題を分析する際に採用できるアプローチについて説明します。

**「アクティベート」ボタンをクリックすると、レプリケーションがトリガーされますか。トリガーされない場合は、次の操作をおこないます。**

1. /crx/explorerに移動し、adminとしてログインします。
1. 「Content Explorer」を開きます。
1. ノード /bin/replicate または /bin/replicate.json が存在するかを確認します。ノードが存在する場合は、削除して保存します。

**レプリケーションがレプリケーションエージェントのキュー内で待機している状態ですか。**

/etc/replication/agents.author.htmlに移動し、レプリケーションエージェントをクリックして確認します。

**1 つまたは複数のエージェントキューで動きがない場合：**

1. Does the queue show **blocked** status? If so then is the publish instance not running or totally unresponsive? Check the publish instance to see what is wrong with it (i.e. check the logs, and see if there is an OutOfMemory error or some other issue. Then if it is just generally slow then take thread dumps and analyze them.
1. Does the queue status show **Queue is active - # pending**? Basically the replication job could be stuck in a socket read waiting for the pubilsh instance or dispatcher to respond. This could mean that the publish instance or dispatcher is under high load or stuck in a lock. Take thread dumps from author and publish in this case.

   * スレッドダンプアナライザーでオーサーのスレッドダンプを開き、レプリケーションエージェントの sling イベントジョブが socketRead で動かなくなっていないかを確認します。
   * 発行からのスレッドダンプをスレッドダンプアナライザーで開き、発行インスタンスが応答しない原因となっている可能性があるものを分析します。/bin/receiveというPOSTを持つスレッド（作成者からレプリケーションを受け取るスレッド）が名前に含まれているはずです。

**すべてのエージェントキューに動きがない場合**

1. リポジトリの破損やその他の問題が原因で、/var/replication/dataの下で特定のコンテンツ部分をシリアライズできない可能性があります。logs/error.logを参照して、関連するエラーがないか確認します。不正なレプリケーションアイテムを消去するには、次の手順を実行します。

   1. https://&lt;host>:&lt;port>/crx/deに移動し、管理者ユーザーとしてログインします。
   1. トップメニューから「ツール」をクリックしてください。
   1. 拡大鏡ボタンをクリックしてください。
   1. 種類として「XPath」を選択します。
   1. 「クエリ」ボックスに、@slingevent:createdによる/jcr:root/var/eventing/jobs//element(*,slingevent:Job)順序を/jcr:root/var/eventing/jobクエリーに入力します。
   1. 「検索」をクリックします。
   1. 検索結果の上位の項目が、最新の Sling イベントジョブです。各ジョブをクリックして、キューの一番上に表示されるものと同じ、動きのないレプリケーションを見つけます。

1. Sling イベントフレームワークジョブのキューに問題が発生している可能性があります。/system/console の org.apache.sling.event バンドルを再起動してみます。
1. ジョブの処理が完全に無効になっている可能性があります。Felix コンソールの「Sling Eventing」タブで確認できます。Apache Sling Eventing (JOB PROCESSING IS DISABLED!) と表示されるか確認します。

   * 表示される場合は、Felix コンソールの「Configuration」タブで Apache Sling Job Event Handler を確認します。「Job processing Enabled」チェックボックスがチェックされていない場合があります。このチェックボックスがチェックされているのに「job processing is disabled」と表示される場合は、ジョブの処理を無効にしているオーバーレイが /apps/system/config にないか確認します。osgi:config ノードを作成し、jobmanager.enabled のブール値を true にして、アクティベートを開始したらキューにジョブが残っていないかを再確認します。

1. また、DefaultJobManager 設定に不整合がある状態になる場合もあります。OSGi コンソール経由で「Apache Sling Job Event Handler」を手動で変更したユーザーがいる場合にこのような事態になります（例えば、「Job Processing Enabled」プロパティを無効にした後に再度有効にして、設定を保存した場合）。

   * この時点で、crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config に保存されている DefaultJobManager 設定に不整合がある状態になります。さらに、「Apache Sling Job Event Handler」プロパティで「Job Processing Enabled」がチェックされた状態でも、いずれかのユーザーが「Sling Eventing」タブに移動すると、「JOB PROCESSING IS DISABLED」というメッセージが表示され、レプリケーションが動作しません。
   * この問題を解決するには、OSGiコンソールの設定ページに移動して、「Apache Slingジョブイベントハンドラ」の設定を削除する必要があります。次に、クラスターのマスターノードを再起動して、設定を一貫した状態に戻します。この問題は修正され、レプリケーションは再び機能します。

**replication.log の作成**

すべてのレプリケーションログを、個別のログファイルに DEBUG レベルで追加するように設定すると、場合によっては非常に便利です。次の手順を実行します。

1. https://host:port/system/console/configMgrに移動し、adminとしてログインします。
1. Find the Apache Sling Logging Logger factory and create an instance by clicking the **+** button on the right of the factory configuration. This will create a new logging logger.
1. 次のように設定します。

   * ログレベル：DEBUG
   * Log File Path:logs/replication.log
   * カテゴリ:com.day.cq.replication

1. 問題が何らかの形で Sling イベントまたはジョブに関連する疑いがある場合は、この Java パッケージをカテゴリ org.apache.sling.event に追加することもできます。

## レプリケーションエージェントキューの一時停止  {#pausing-replication-agent-queue}

オーサーシステムの負荷を軽減するために、レプリケーションキューを無効にせずに一時停止することが適している場合があります。現在、これをおこなう唯一の方法は、無効なポートを一時的に設定することです。5.4 以降は、レプリケーションエージェントキューに一時停止ボタンが表示されますが、一部の制限があります。

1. 状態が永続化されません。そのため、サーバーまたはレプリケーションバンドルを再起動すると、実行中の状態に戻ります。
1. 一時停止は短い期間（他のスレッドによるレプリケーションを含むアクティビティがなくなってから 1 時間）アイドル状態になりますが、長い期間は不可能です。スレッドのアイドル状態を防ぐ機能が Sling にあるからです。基本的には、ジョブキュースレッドが長い期間未使用の状態であるかを確認し、そうである場合はクリーンアップサイクルを開始します。クリーンアップサイクルによってスレッドが停止するので、一時停止されている設定が消失します。ジョブは永続化されるので、新しいスレッドを開始してキューを処理します。このキューには、一時停止設定の詳細情報がありません。そのため、キューが実行状態になります。

## ユーザーのアクティベート時にページ権限がレプリケートされない {#page-permissions-are-not-replicated-on-user-activation}

ページ権限は、ユーザーに付与されるのではなく、アクセス権が付与されるノードに保存されるので、レプリケートされません。

ページ権限は一般的にオーサーからパブリッシュにレプリケートするべきではなく、デフォルトではレプリケートされません。これは、これらの 2 つの環境でアクセス権が異なる必要があるためです。そのため、パブリッシュではオーサーとは別に ACL を設定することが推奨されます。

## オーサーからパブリッシュに名前空間情報をレプリケーションするときにレプリケーションキューがブロックされました {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

場合によっては、オーサーインスタンスからパブリッシュインスタンスに名前空間情報をレプリケーションしようとすると、レプリケーションキューがブロックされます。This happens because the replication user does not have `jcr:namespaceManagement` privilege. この問題を回避するには、次のことを確認してください。

* The replication user (as configured under the [Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) also exists on the Publish instance.
* ユーザーは、コンテンツがインストールされているパスで読み取りおよび書き込み権限を持っています。
* The user has `jcr:namespaceManagement` privilege at the repository level. 次のようにして権限を付与できます。

1. Login to CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) as administrator.
1. 「**アクセス制御**」タブをクリックします。
1. 「**リポジトリ**」を選択します。
1. 「**エントリを追加**」（プラスアイコン）をクリックします。
1. ユーザーの名前を入力します。
1. Select `jcr:namespaceManagement` from the privileges list.
1. 「OK」をクリックします。

