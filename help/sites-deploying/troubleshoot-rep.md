---
title: レプリケーションのトラブルシューティング
seo-title: Troubleshooting Replication
description: この記事では、レプリケーションに関する問題のトラブルシューティング方法について説明します。
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 100%

---

# レプリケーションのトラブルシューティング{#troubleshooting-replication}

このページでは、レプリケーションに関する問題のトラブルシューティング方法について説明します。

## 問題 {#problem}

レプリケーション（順方向のレプリケーション）が何らかの原因で失敗する

## 解決方法 {#resolution}

レプリケーションが失敗するのには様々な原因があります。ここでは、これらの問題を分析する際に採用できるアプローチについて説明します。

**「アクティベート」ボタンをクリックすると、レプリケーションがトリガーされますか。トリガーされない場合は、次の操作をおこないます。**

1. /crx/explorer に移動し、管理者としてログインします。
1. 「Content Explorer」を開きます。
1. ノード /bin/replicate または /bin/replicate.json が存在するかを確認します。ノードが存在する場合は、削除して保存します。

**レプリケーションがレプリケーションエージェントのキュー内で待機している状態ですか。**

確認するには、/etc/replication/agents.author.html に移動し、レプリケーションエージェントをクリックします。

**1 つまたは複数のエージェントキューが停止している場合：**

1. キューのステータスには「**ブロック**」と示されていますか。その場合、パブリッシュインスタンスが実行していないか、完全に応答しない状態になっていますか。パブリッシュインスタンスを確認し、何が問題かを調査します。例えば、ログをチェックして、OutOfMemory エラーなどの問題が発生していないかを確認します。単に一般的な遅延が発生している場合は、スレッドダンプを取得して分析します。
1. キューのステータスは「**Queue is active - # pending**」と示されていますか。基本的に、レプリケーションジョブはソケット読み取りにおいて、パブリッシュインスタンスまたは Dispatcher の応答待ちで停止する可能性があります。この場合、パブリッシュインスタンスまたは Dispatcher が高負荷の状態か、ロックによって停止状態になる可能性があります。そのような場合は、オーサーまたはパブリッシュでスレッドダンプを取得してください。

   * スレッドダンプアナライザーでオーサーのスレッドダンプを開き、レプリケーションエージェントの sling イベントジョブが socketRead で停止していないかを確認します。
   * スレッドダンプアナライザーでパブリッシュのスレッドダンプを開き、パブリッシュインスタンスが応答しない原因を分析します。オーサーからレプリケーションを受信するスレッドである POST /bin/receive という名前のスレッドを確認します。

**すべてのエージェントキューが停止している場合**

1. リポジトリの破損などの問題があり、コンテンツの特定の部分を /var/replication/data にシリアライズできない可能性があります。logs/error.log で、関連するエラーがないか確認してください。不正なレプリケーション項目を除去するには、次の操作を行います。

   1. https://&lt;host>:&lt;port>/crx/de にアクセスし、管理者ユーザーでログインします。
   1. トップメニューから「ツール」をクリックしてください。
   1. 拡大鏡ボタンをクリックしてください。
   1. 種類として「XPath」を選択します。
   1. 「Query」ボックスに、次のクエリーを入力します。/jcr:root/var/eventing/jobs//element(&#42;、slingevent:Job) order by @slingevent:created
   1. 「検索」をクリックします。
   1. 検索結果の上位の項目が、最新の Sling イベントジョブです。各ジョブをクリックして、キューの一番上に表示されるものと同じ、動きのないレプリケーションを見つけます。

1. Sling イベントフレームワークジョブのキューに問題が発生している可能性があります。/system/console の org.apache.sling.event バンドルを再起動してみます。
1. ジョブの処理が完全に無効になっている可能性があります。Felix コンソールの「Sling Eventing」タブで確認できます。Apache Sling Eventing (JOB PROCESSING IS DISABLED!) と表示されるか確認します。

   * 表示される場合は、Felix コンソールの「Configuration」タブで Apache Sling Job Event Handler を確認します。「Job processing Enabled」チェックボックスがチェックされていない場合があります。このチェックボックスがチェックされているのに「job processing is disabled」と表示される場合は、ジョブの処理を無効にしているオーバーレイが /apps/system/config にないか確認します。osgi:config ノードを作成し、jobmanager.enabled のブール値を true にして、アクティベートを開始したらキューにジョブが残っていないかを再確認します。

1. また、DefaultJobManager 設定に不整合がある状態になる場合もあります。OSGi コンソール経由で「Apache Sling Job Event Handler」を手動で変更したユーザーがいる場合にこのような事態になります（例えば、「Job Processing Enabled」プロパティを無効にした後に再度有効にして、設定を保存した場合）。

   * この時点で、crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config に保存されている DefaultJobManager 設定に不整合がある状態になります。さらに、「Apache Sling Job Event Handler」プロパティで「Job Processing Enabled」がチェックされた状態でも、いずれかのユーザーが「Sling Eventing」タブに移動すると、「JOB PROCESSING IS DISABLED」というメッセージが表示され、レプリケーションが動作しません。
   * この問題を解決するには、OSGi コンソールの「Configuration」ページに移動して、「Apache Sling Job Event Handler」設定を削除する必要があります。次に、クラスターのマスターノードを再起動して、設定を整合性のある状態に戻します。この操作によって問題が修正され、レプリケーションが再び動作を開始します。

**replication.log の作成**

すべてのレプリケーションログを、個別のログファイルに DEBUG レベルで追加するように設定すると、場合によっては非常に便利です。次の手順を実行します。

1. https://host:port/system/console/configMgr にアクセスし、Admin でログインします。
1. Apache Sling Logging Logger ファクトリを探して、ファクトリ設定の右側の「**+**」ボタンをクリックしてインスタンスを作成します。新しいログロガーが作成されます。
1. 次のように設定します。

   * ログレベル：DEBUG
   * ログファイルのパス：logs/replication.log
   * カテゴリ：com.day.cq.replication

1. 問題が何らかの形で Sling イベントまたはジョブに関連する疑いがある場合は、この Java パッケージをカテゴリ org.apache.sling.event に追加することもできます。

## レプリケーションエージェントキューの一時停止  {#pausing-replication-agent-queue}

オーサーシステムの負荷を軽減するために、レプリケーションキューを無効にせずに一時停止することが適している場合があります。現在、これをおこなう唯一の方法は、無効なポートを一時的に設定することです。5.4 以降は、レプリケーションエージェントキューに一時停止ボタンが表示されますが、一部の制限があります。

1. 状態が永続化されません。そのため、サーバーまたはレプリケーションバンドルを再起動すると、実行中の状態に戻ります。
1. 一時停止は短い期間（他のスレッドによるレプリケーションを含むアクティビティがなくなってから 1 時間）アイドル状態になりますが、長い期間は不可能です。スレッドのアイドル状態を防ぐ機能が Sling にあるからです。基本的には、ジョブキュースレッドが長い期間未使用の状態であるかを確認し、そうである場合はクリーンアップサイクルを開始します。クリーンアップサイクルによってスレッドが停止するので、一時停止されている設定が消失します。ジョブは永続化されるので、新しいスレッドを開始してキューを処理します。このキューには、一時停止設定の詳細情報がありません。そのため、キューが実行状態になります。

## ユーザーのアクティベート時にページ権限がレプリケートされない {#page-permissions-are-not-replicated-on-user-activation}

ページ権限は、ユーザーに付与されるのではなく、アクセス権が付与されるノードに保存されるので、レプリケートされません。

ページ権限は一般的にオーサーからパブリッシュにレプリケートするべきではなく、デフォルトではレプリケートされません。これは、これらの 2 つの環境でアクセス権が異なる必要があるためです。そのため、パブリッシュではオーサーとは別に ACL を設定することが推奨されます。

## オーサーからパブリッシュに名前空間情報をレプリケーションするときにレプリケーションキューがブロックされました {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

場合によっては、オーサーインスタンスからパブリッシュインスタンスに名前空間情報をレプリケーションしようとすると、レプリケーションキューがブロックされます。これは、レプリケーションユーザーが `jcr:namespaceManagement` 権限を持っていないために起こります。この問題を回避するには、次のことを確認してください。

* レプリケーションユーザー（「[トランスポート](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)」タブ／ユーザーで設定）はパブリッシュインスタンス上にも存在します。
* ユーザーは、コンテンツがインストールされているパスで読み取りと書き込みの権限を持っています。
* ユーザーはリポジトリレベルで `jcr:namespaceManagement` 権限を持っています。次のようにして権限を付与できます。

1. CRX/DE（`https://localhost:4502/crx/de/index.jsp`）に管理者としてログインします。
1. 「**アクセス制御**」タブをクリックします。
1. 「**リポジトリ**」を選択します。
1. 「**エントリを追加**」（プラスアイコン）をクリックします。
1. ユーザーの名前を入力します。
1. 権限リストから `jcr:namespaceManagement` を選択します。
1. 「OK」をクリックします。
