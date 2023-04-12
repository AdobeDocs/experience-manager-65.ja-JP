---
title: アップグレード前のメンテナンスタスク
seo-title: Pre-Upgrade Maintenance Tasks
description: AEMでのアップグレード前のタスクについて説明します。
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 25%

---

# アップグレード前のメンテナンスタスク{#pre-upgrade-maintenance-tasks}

アップグレードを開始する前に、次のメンテナンスタスクに従って、問題が発生した場合にシステムの準備が整い、ロールバックが可能であることを確認することが重要です。

* [十分なディスク領域の確保](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM の完全なバックアップ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [/etc に対する変更のバックアップ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [quickstart.properties ファイルの生成](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [ワークフローおよび監査ログのパージの設定](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [アップグレード前のタスクのインストール、設定および実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [カスタムログインモジュールの無効化](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [/install ディレクトリからの更新の削除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [すべてのコールドスタンバイインスタンスの停止](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [カスタムのスケジュール済みジョブの無効化](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [データストアのガベージコレクションの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [必要に応じてデータベーススキーマをアップグレード](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [アップグレードの妨げになる可能性のあるユーザーの削除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [ログファイルのローテーション](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 十分なディスク領域の確保 {#ensure-sufficient-disk-space}

アップグレードを実行する際には、コンテンツおよびコードのアップグレードアクティビティに加えて、リポジトリの移行を実行する必要があります。 移行により、新しい Segment Tar 形式でリポジトリのコピーが作成されます。 その結果、リポジトリの 1 つ目の大きなサイズのバージョンを保持するのに十分なディスク容量が必要になります。

## AEM の完全なバックアップ {#fully-back-up-aem}

アップグレードを開始する前に、AEMを完全にバックアップする必要があります。 必要に応じて、リポジトリ、アプリケーションのインストール、データストア、Mongo の各インスタンスを必ずバックアップしてください。 AEMインスタンスのバックアップと復元について詳しくは、 [バックアップと復元](/help/sites-administering/backup-and-restore.md).

## /etc に対する変更のバックアップ {#backup-changes-etc}

アップグレードプロセスは、リポジトリの `/apps` パスおよび `/libs` パスの下にある既存のコンテンツおよび設定のメンテナンスやマージに役立ちます。( `/etc` パス（Context Hub 設定を含む）は、多くの場合、アップグレード後にこれらの変更を再適用する必要があります。 アップグレードでは、マージできない変更のバックアップコピーが作成されます `/var`の場合、Adobeでは、アップグレードを開始する前に、これらの変更を手動でバックアップすることをお勧めします。

## quickstart.properties ファイルの生成 {#generate-quickstart-properties}

jar ファイルからAEMを起動する場合、 `quickstart.properties` ファイルは、 `crx-quickstart/conf`. AEMが以前に開始スクリプトで起動しただけの場合、このファイルは存在せず、アップグレードは失敗します。 このファイルが存在するかどうかを確認し、存在しない場合は jar ファイルからAEMを再起動します。

## ワークフローおよび監査ログのパージの設定 {#configure-wf-audit-purging}

この `WorkflowPurgeTask` および `com.day.cq.audit.impl.AuditLogMaintenanceTask` タスクには別々の OSGi 設定が必要で、設定なしでは機能しません。 アップグレード前のタスクの実行中に失敗した場合は、設定が見つからない可能性が最も高い理由です。 したがって、これらのタスクの OSGi 設定を追加するか、実行しない場合はアップグレード前の最適化タスクリストから完全に削除してください。 ワークフローのパージタスクの設定に関するドキュメントについては、を参照してください。 [ワークフローインスタンスの管理](/help/sites-administering/workflows-administering.md) 監査ログのメンテナンスタスク設定は、次の場所にあります。 [AEM 6 での監査ログのメンテナンス](/help/sites-administering/operations-audit-log.md).

CQ 5.6 でのワークフローおよび監査ログのパージとAEM 6.0 での監査ログのパージについては、 [ワークフローと監査ノードのパージ](https://helpx.adobe.com/jp/experience-manager/kb/howtopurgewf.html).

## アップグレード前のタスクのインストール、設定および実行 {#install-configure-run-pre-upgrade-tasks}

カスタマイズ可能なAEMのレベルにより、通常、環境は一様なアップグレード実行方法に準拠しません。 そのため、アップグレードのための標準化された手順を作成するのは困難です。

以前のバージョンでは、停止したAEMのアップグレードや、安全に再開できなかったのアップグレードも困難でした。 この問題が原因で、完全なアップグレード手順の再開が必要だった場合や、不良なアップグレードが警告を発生させずに実行された場合がありました。

これらの問題に対処するため、Adobeはアップグレードプロセスにいくつかの機能強化を加え、より柔軟で使いやすいものにしました。 アップグレード前のメンテナンスタスクを手動で実行する必要があった場合は、最適化と自動化が行われています。 また、アップグレード後のレポートが追加され、問題がより簡単に見つかることを期待してプロセスを完全に詳細に調べることができます。

アップグレード前のメンテナンスタスクは、現在、手動で部分的または完全に実行される様々なインターフェイスに分散されています。 AEM 6.3 で導入されたアップグレード前のメンテナンス最適化により、これらのタスクを統合的にトリガーし、その結果をオンデマンドで調べることができます。

アップグレード前の最適化手順に含まれるすべてのタスクは、AEM 6.0 以降のすべてのバージョンと互換性があります。

### 設定方法 {#how-to-set-it-up}

AEM 6.3 以降では、アップグレード前のメンテナンス最適化タスクが quickstart jar に含まれています。

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### 使用方法 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI コンポーネントは、アップグレード前のメンテナンスタスクのリストで事前設定されており、それらのすべてのタスクを一度に実行できます。以下の手順に従ってタスクを設定できます。

1. *https://serveraddress:serverport/system/console/configMgr* にブラウジングして web コンソールに移動

1. 「**preupgradetasks**」と入力し、最初に一致したコンポーネントをクリックします。 コンポーネントのフルネームは、`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl` です。

1. 次に示すように、実行する必要があるメンテナンスタスクのリストを変更します。

   ![1487758925984](assets/1487758925984.png)

タスクリストは、インスタンスの開始に使用される実行モードに応じて異なります。 以下に、各メンテナンスタスクが設計された実行モードの説明を示します。

<table>
 <tbody>
  <tr>
   <td><strong>タスク</strong></td>
   <td><strong>実行モード</strong></td>
   <td><strong>メモ</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>マークとスイープを実行します。 共有データストアの場合は、このステップを削除し、次を実行します。<br /> を手動で、または適切にインスタンスを準備してから実行してください。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>実行する前に、Adobe「Granite Workflow Purge Configuration」OSGi を設定する必要があります。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>AEM 6.0 から 6.2 の TarMK インスタンスの場合は、代わりにオフラインでのリビジョンクリーンアップを手動で実行します。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>実行する前に、 Audit Log Purge Scheduler OSGi 設定を設定する必要があります。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>この `DataStoreGarbageCollectionTask` を使用すると、mark and sweep フェーズでデータストアのガベージコレクション操作が呼び出されます。 共有データストアを使用するデプロイメントでは、適切に再設定するか、別のインスタンスが参照する項目が削除されないようにインスタンスを準備します。 このプロセスでは、このアップグレード前のタスクをトリガーする前に、すべてのインスタンスに対して手動でマークフェーズを実行する必要が生じる場合があります。

### アップグレード前のヘルスチェックのデフォルト設定 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI コンポーネントは、`runAllPreUpgradeHealthChecks` メソッドが呼び出されたときに実行されるアップグレード前のヘルスチェックタグのリストで事前設定されています。

* **システム** - granite のメンテナンスヘルスチェックで使用されるタグ

* **アップグレード前**  — アップグレード前に実行するように設定できるすべてのヘルスチェックに追加できるカスタムタグ

リストは編集可能です。 プラス記号は **(+)** およびマイナス **(-)** タグの横にあるボタンを使用して、カスタムタグを追加したり、デフォルトのタグを削除したりできます。

**MBean メソッド**

管理 Bean 機能には、 [JMX コンソール](/help/sites-administering/jmx-console.md).

MBean にアクセスするには、次の方法があります。

1. JMX コンソール（*https://serveraddress:serverport/system/console/jmx*）に移動
1. 「**PreUpgradeTasks**」を検索し、結果をクリックします。

1. 「**操作**」セクションからメソッドを選択し、次のウィンドウで「**呼び出し**」を選択します。

`PreUpgradeTasksMBeanImpl` によって公開されている使用可能なすべてのメソッドのリストを以下に示します。

<table>
 <tbody>
  <tr>
   <td><strong>メソッド名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFO</td>
   <td>使用可能なアップグレード前のメンテナンスタスク名のリストを表示します。</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>情報</td>
   <td>アップグレード前のヘルスチェックタグ名のリストを表示します。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>アクション</td>
   <td>リスト内のアップグレード前のメンテナンスタスクをすべて実行します。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>指定された名前をパラメーターとして使用して、アップグレード前のメンテナンスタスクを実行します。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>次の項目をチェックします。 <code>runAllPreUpgradeTasksmaintenance</code> タスクが実行中です。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>アップグレード前のメンテナンスタスクが実行中かどうかを確認し、<br /> 現在実行中のタスクの名前を含む配列を返します。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>パラメーターとして指定された名前で、アップグレード前のメンテナンスタスクの正確な実行時間を表示します。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>アップグレード前のメンテナンスタスクの最後の実行状態を、パラメーターとして指定された名前で表示します。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>アクション</td>
   <td><p>すべてのアップグレード前のヘルスチェックを実行し、そのステータスを次の名前のファイルに保存 <code>preUpgradeHCStatus.properties</code> sling ホームパス内にある この <code>shutDownOnSuccess</code> パラメーターが <code>true</code>AEMインスタンスはシャットダウンされますが、アップグレード前のヘルスチェックのステータスがすべて OK の場合に限られます。</p> <p>properties ファイルは、今後のアップグレードの前提条件として使用されます<br /> アップグレード前のヘルスチェックの場合、アップグレードプロセスは停止します。<br /> 実行に失敗しました。 アップグレード前の結果を無視する場合<br /> ヘルスチェックを実行して、アップグレードを開始します。このファイルは削除できます。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>アクション</td>
   <td>次の場合に満たされなくなった、インポートされたすべてのパッケージをリストします：<br /> 指定したAEMバージョンにアップグレードしています。 対象のAEMのバージョンが<br /> をパラメーターとして指定する。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean メソッドは、次の場所から呼び出すことができます。
>
>* JMX コンソール
>* JMX に接続する外部アプリケーション
>* cURL
>


## カスタムログインモジュールの無効化 {#disable-custom-login-modules}

>[!NOTE]
>
>この手順は、AEM 5 バージョンからアップグレードする場合にのみ必要です。 古いAEM 6 バージョンからのアップグレードの場合は、完全にスキップできます。

カスタム `LoginModules` がリポジトリレベルで認証設定される方法は、Apache Oak で根本的に変更されました。

CRX2 を使用していた旧バージョンの AEM では、`repository.xml` ファイルで設定をおこないましたが、AEM 6 以降では、web コンソールを使用して、Apache Felix JAAS Configuration Factory サービスで設定をおこないます。

そのため、既存の設定を無効にして、アップグレード後、Apache Oak 用に再作成する必要があります。

の JAAS 設定で定義されたカスタムモジュールを無効にするには、以下を実行します。 `repository.xml`の場合、デフォルトの `LoginModule`、次の例のように。

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>詳しくは、[外部ログインモジュールによる認証](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)を参照してください。
>
>AEM 6 での `LoginModule` 設定例については、[AEM 6 での LDAP の設定](/help/sites-administering/ldap-config.md)を参照してください。

## /install ディレクトリからの更新の削除 {#remove-updates-install-directory}

>[!NOTE]
>
>AEMインスタンスをシャットダウンした後に、crx-quickstart/install ディレクトリからパッケージを削除するだけです。 この手順は、インプレースアップグレード手順を開始する前の最後の手順の 1 つです。

を通じてデプロイされたサービスパック、機能パック、またはホットフィックスを削除します。 `crx-quickstart/install` ローカルファイルシステム上のディレクトリ。 これにより、更新が完了した後に、新しいAEMバージョン上に古いホットフィックスとサービスパックが誤ってインストールされるのを防ぎます。

## すべてのコールドスタンバイインスタンスの停止 {#stop-tarmk-coldstandby-instance}

TarMK コールドスタンバイを使用する場合は、すべてのコールドスタンバイインスタンスを停止します。 これにより、アップグレードで問題が発生した場合に、効率的にオンラインに戻す方法が保証されます。 アップグレードが正常に完了したら、アップグレードされたプライマリインスタンスからコールドスタンバイインスタンスを再構築する必要があります。

## カスタムのスケジュール済みジョブの無効化 {#disable-custom-scheduled-jobs}

アプリケーションコードに含まれる OSGi スケジュール済みジョブを無効にします。

## オフラインでのリビジョンクリーンアップの実行 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>この手順は、TarMK インストールでのみ必要です

TarMK を使用する場合は、アップグレードの前にオフラインでのリビジョンクリーンアップを実行する必要があります。 これにより、リポジトリの移行手順とそれ以降のアップグレードタスクの実行が大幅に高速になり、アップグレードが完了した後にオンラインでのリビジョンクリーンアップを正常に実行できるようになります。 オフラインでのリビジョンクリーンアップの実行については、 [オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## データストアのガベージコレクションの実行 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>この手順は、crx3 を実行するインスタンスでのみ必要です

CRX3 インスタンスでリビジョンクリーンアップを実行した後、データストアのガベージコレクションを実行して、データストア内の参照されていない BLOB をすべて削除する必要があります。 手順については、 [データストアのガベージコレクション](/help/sites-administering/data-store-garbage-collection.md).

## 必要に応じてデータベーススキーマをアップグレード {#upgrade-the-database-schema-if-needed}

通常、AEMが永続化に使用する基になる Apache Oak スタックは、必要に応じてデータベーススキーマのアップグレードを処理します。

ただし、スキーマを自動的にアップグレードできない場合が考えられます。このような場合、ほとんどの場合、権限が制限されたユーザーでデータベースが実行されている高いセキュリティ環境です。 このような状況が発生した場合、AEMは古いスキーマを引き続き使用します。

このようなシナリオが発生しないようにするには、次の手順を実行してスキーマをアップグレードします。

1. アップグレードする必要があるAEMインスタンスをシャットダウンします。
1. データベーススキーマをアップグレードします。結果を得るために必要なツールについては、データベースタイプのドキュメントを参照してください。

   Oak でのスキーマのアップグレードの処理方法について詳しくは、Apache Web サイトで[このページ](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)を参照してください。

1. AEM のアップグレードを続行します。

## アップグレードの妨げになる可能性のあるユーザーの削除 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>このアップグレード前のメンテナンスタスクは、次の場合にのみ必要です。
>
>* AEM 6.3 より前の AEM バージョンからアップグレードしている
>* アップグレード中に以下に示すエラーが発生した
>


サービスユーザーが古いAEMバージョンになり、通常のユーザーとして不適切にタグ付けされる場合は、例外的なケースがあります。

このような状況が発生した場合、アップグレードは次のようなメッセージで失敗します。

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

この問題を回避するには、必ず次の手順を実行してください。

1. 実稼動トラフィックからインスタンスを分離する
1. 問題の原因となる 1 人以上のユーザーのバックアップを作成します。 このタスクは、パッケージマネージャーを使用して実行できます。 詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。
1. 問題の原因となっている 1 人以上のユーザーを削除します。 以下は、このカテゴリに該当する可能性のあるユーザーのリストです。

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## ログファイルのローテーション {#rotate-log-files}

Adobeでは、アップグレードを開始する前に現在のログファイルをアーカイブすることをお勧めします。 これにより、アップグレード中およびアップグレード後にログファイルを監視およびスキャンし、発生する可能性のある問題を特定して解決しやすくなります。
