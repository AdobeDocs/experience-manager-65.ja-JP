---
title: アップグレード前のメンテナンスタスク
seo-title: Pre-Upgrade Maintenance Tasks
description: AEMで推奨されるアップグレード前のタスクについて説明します。
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
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '2031'
ht-degree: 99%

---

# アップグレード前のメンテナンスタスク{#pre-upgrade-maintenance-tasks}

アップグレードの開始前に、次のメンテナンスタスクに従って、システムの準備が完了し、問題が発生した場合にロールバックができる状態にしておくことが重要です。

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

アップグレードを実行する際には、コンテンツとコードのアップグレードアクティビティに加えて、リポジトリの移行を実行する必要があります。この移行により、新しいセグメント Tar 形式でリポジトリのコピーが作成されます。その結果、大容量になり得るリポジトリの 2 番目のバージョンを保持するために十分なディスク領域が必要になります。

## AEM の完全なバックアップ {#fully-back-up-aem}

アップグレードの開始前に、AEM を完全にバックアップする必要があります。該当する場合は、リポジトリ、アプリケーションのインストール、データストア、Mongo インスタンスを必ずバックアップします。AEM インスタンスのバックアップと復元についての詳細情報は、[バックアップと復元](/help/sites-administering/backup-and-restore.md)を参照してください。

## /etc に対する変更のバックアップ {#backup-changes-etc}

アップグレードプロセスは、リポジトリの `/apps` パスおよび `/libs` パスの下にある既存のコンテンツおよび設定のメンテナンスやマージに役立ちます。Context Hub 設定などの `/etc` パスに加えられた変更は、多くの場合、アップグレード後に再適用する必要があります。アップグレードにより、マージできない変更のバックアップコピーが `/var` の下に作成されますが、アップグレードの開始前にこれらの変更を手動でバックアップすることをお勧めします。

## quickstart.properties ファイルの生成 {#generate-quickstart-properties}

jar ファイルから AEM を起動すると、`crx-quickstart/conf` の下に `quickstart.properties` ファイルが生成されます。これまで AEM を起動スクリプトでのみ起動していた場合、このファイルは存在せず、アップグレードは失敗します。このファイルが存在するかどうかを確認し、存在しない場合は jar ファイルから AEM を再起動します。

## ワークフローおよび監査ログのパージの設定 {#configure-wf-audit-purging}

`WorkflowPurgeTask` タスクと `com.day.cq.audit.impl.AuditLogMaintenanceTask` タスクには個別の OSGi 設定が必要であり、この設定がない場合は機能しません。アップグレード前のタスクの実行中にこれらのタスクが失敗した場合、最も考えられる原因は、タスクに設定がないことです。したがって、これらのタスクに OSGi 設定を追加するか、タスクを実行しない場合はアップグレード前の最適化タスクリストから完全に削除してください。ワークフローのパージタスクの設定に関するドキュメントは[ワークフローインスタンスの管理](/help/sites-administering/workflows-administering.md)で、監査ログのメンテナンスタスクの設定に関するドキュメントは [AEM 6 の監査ログのメンテナンス](/help/sites-administering/operations-audit-log.md)で参照できます。

CQ 5.6 でのワークフローと監査ログのパージ、AEM 6.0 での監査ログのパージについては、[ワークフローと監査ノードのパージ](https://helpx.adobe.com/jp/experience-manager/kb/howtopurgewf.html)を参照してください。

## アップグレード前のタスクのインストール、設定および実行 {#install-configure-run-pre-upgrade-tasks}

AEM で可能なカスタマイズのレベルにより、通常、アップグレードの実行方法は環境によって異なります。そのため、標準化されたアップグレード手順の作成は簡単ではありません。

以前のバージョンでは、停止または失敗した AEM アップグレードを安全に再開することも困難でした。この問題により、完全なアップグレード手順の再開が必要になったり、警告が表示されずに不完全なアップグレードが実行されたりすることがありました。

これらの問題に対処するために、アドビはアップグレードプロセスにいくつかの拡張機能を追加し、より柔軟で使いやすくしました。以前は手動で実行する必要があった、アップグレード前のメンテナンスタスクの最適化と自動化が進められています。また、アップグレード後のレポートを追加して、プロセスを完全に調べて問題を見つけやすくしました。

現在、アップグレード前のメンテナンスタスクは、部分的または完全に手動で実行される様々なインターフェイスに分散されています。AEM 6.3 で導入されたアップグレード前のメンテナンスの最適化により、共通の方法でこれらのタスクをトリガーし、その結果をオンデマンドで調べることができます。

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

1. 「**preupgradetasks**」を検索し、最初に一致したコンポーネントをクリックします。コンポーネントのフルネームは `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl` です。

1. 次に示すように、実行が必要なメンテナンスタスクのリストを変更します。

   ![1487758925984](assets/1487758925984.png)

タスクリストは、インスタンスの開始に使用する実行モードによって異なります。各メンテナンスタスクの設計対象となる実行モードの説明を次に示します。

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
   <td>マークアンドスイープを実行します。共有データストアの場合、この手順を削除して<br />手動で実行するか、実行前にインスタンスを適切に準備します。</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2／crx3</td>
   <td>実行前に、Adobe Granite のワークフローのパージ設定 OSGi を設定する必要があります。</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>AEM 6.0～6.2 の TarMK インスタンスについては、代わりに手動でオフラインでのリビジョンクリーンアップを実行します。</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>実行前に、監査ログのパージスケジューラー OSGi 設定を設定する必要があります。</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` を使用する場合、マークアンドスイープフェーズでデータストアガベージコレクション操作を呼び出します。共有データストアを使用するデプロイメントでは、別のインスタンスで参照される項目が削除されないように、適切に再設定するかインスタンスを準備します。場合によっては、そのために、このアップグレード前のタスクをトリガーする前に、すべてのインスタンスに対してマークフェーズを手動で実行する必要があります。

### アップグレード前のヘルスチェックのデフォルトの設定 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI コンポーネントは、`runAllPreUpgradeHealthChecks` メソッドが呼び出されたときに実行されるアップグレード前のヘルスチェックタグのリストで事前設定されています。

* **system** - Granite のメンテナンスヘルスチェックで使用するタグです。

* **pre-upgrade** - アップグレード前に実行するように設定できるすべてのヘルスチェックに追加できるカスタムタグです。

このリストは編集できます。タグの横のプラス&#x200B;**（+）**&#x200B;ボタンとマイナス&#x200B;**（-）**&#x200B;ボタンを使用して、カスタムタグを追加したり、デフォルトのタグを削除したりすることができます。

**MBean メソッド**

マネージド Bean 機能には、[JMX コンソール](/help/sites-administering/jmx-console.md)を使用してアクセスできます。

以下の手順で MBean にアクセスできます。

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
   <td>アップグレード前のヘルスチェックのタグ名のリストを表示します。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>アクション</td>
   <td>リストに含まれるアップグレード前のメンテナンスタスクをすべて実行します。</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>パラメーターで名前が指定されたアップグレード前のメンテナンスタスクを実行します。</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td><code>runAllPreUpgradeTasksmaintenance</code> タスクが実行中かどうかを確認します。</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>アップグレード前のメンテナンスタスクが実行中かどうかをチェックし、<br />現在実行されているタスクの名前を含んだ配列を返します。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>パラメーターで名前が指定されたアップグレード前のメンテナンスタスクの正確な実行時間を表示します。</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>アクション</td>
   <td>パラメーターで名前が指定されたアップグレード前のメンテナンスタスクの最終実行状態を表示します。</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>アクション</td>
   <td><p>アップグレード前のすべてのヘルスチェックを実行して、sling ホームパスにある <code>preUpgradeHCStatus.properties</code> というファイルにそれらのステータスを保存します。<code>shutDownOnSuccess</code> パラメーターが <code>true</code> に設定されていると、AEM インスタンスがシャットダウンされますが、これはアップグレード前のすべてのヘルスチェックのステータスが OK の場合のみです。</p> <p>properties ファイルは今後のアップグレードの前提条件として使用され、<br />アップグレード前のヘルスチェックの実行に失敗した場合は、<br />アップグレードプロセスが停止されます。アップグレード前のヘルスチェックの結果を無視して<br />アップグレードを開始する場合は、このファイルを削除できます。</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>アクション</td>
   <td>指定された AEM バージョンにアップグレードしたときに適合しなくなる<br />すべての読み込み済みパッケージをリストします。ターゲットの AEM バージョンは、<br />パラメーターとして指定する必要があります。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>MBean メソッドは、以下から呼び出すことができます。
>
>* JMX コンソール
>* JMX に接続する外部アプリケーション
>* cURL
>

## カスタムログインモジュールの無効化 {#disable-custom-login-modules}

>[!NOTE]
>
>この手順は、AEM 5 バージョンからアップグレードする場合にのみ必要です。以前の AEM 6 バージョンからのアップグレードの場合は、完全にスキップできます。

カスタム `LoginModules` がリポジトリレベルで認証設定される方法は、Apache Oak で根本的に変更されました。

CRX2 を使用していた旧バージョンの AEM では、`repository.xml` ファイルで設定をおこないましたが、AEM 6 以降では、web コンソールを使用して、Apache Felix JAAS Configuration Factory サービスで設定をおこないます。

そのため、既存の設定を無効にして、アップグレード後、Apache Oak 用に再作成する必要があります。

`repository.xml` の JAAS 設定で定義したカスタムモジュールを無効にするには、デフォルトの `LoginModule` を使用するように設定を編集する必要があります（以下の例を参照）。

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
>パッケージは、AEM インスタンスをシャットダウンした後でのみ crx-quickstart/install ディレクトリから削除します。これは、インプレースアップグレード手順を開始する前の最後の手順の 1 つです。

ローカルファイルシステムの `crx-quickstart/install` ディレクトリを介してデプロイされたサービスパック、機能パックまたはホットフィックスを削除します。これにより、更新が完了した後に、新しい AEM バージョンに古いホットフィックスおよびサービスパックが誤ってインストールされることを防止できます。

## すべてのコールドスタンバイインスタンスの停止 {#stop-tarmk-coldstandby-instance}

TarMK コールドスタンバイを使用している場合は、すべてのコールドスタンバイインスタンスを停止します。これにより、アップグレードで問題が発生した場合でも、効率的にオンラインに戻すことができます。アップグレードが正常に完了したら、アップグレードされたプライマリインスタンスからコールドスタンバイインスタンスを再構築する必要があります。

## カスタムのスケジュール済みジョブの無効化 {#disable-custom-scheduled-jobs}

アプリケーションコードに含まれている OSGi スケジュール済みジョブを無効にします。

## オフラインでのリビジョンクリーンアップの実行 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>この手順は、TarMK インストール環境でのみ必要です。

TarMK を使用している場合は、アップグレードの前にオフラインでのリビジョンクリーンアップを実行してください。これにより、リポジトリの移行ステップが作成され、後続のアップグレードタスクがより迅速に実行されます。また、アップグレード完了後に、オンラインでのリビジョンクリーンアップが正常に実行されるようになります。オフラインでのリビジョンクリーンアップの実行について詳しくは、[オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)を参照してください。

## データストアのガベージコレクションの実行 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>この手順は、crx3 を実行するインスタンスにのみ必要です。

CRX3 インスタンスでリビジョンクリーンアップを実行した後は、データストアのガベージコレクションを実行して、データストア内の参照されていない BLOB を削除する必要があります。手順については、[データストアのガベージコレクション](/help/sites-administering/data-store-garbage-collection.md)に関するドキュメントを参照してください。

## 必要に応じてデータベーススキーマをアップグレード {#upgrade-the-database-schema-if-needed}

通常、AEM が永続性の処理に使用する基礎的な Apache Oak スタックは、必要に応じてデータベーススキーマのアップグレードに対処します。

ただし、スキーマを自動的にアップグレードできない場合も考えられます。それは、ほとんどの場合、権限が限られているユーザーの下でデータベースが実行されている、セキュリティレベルの高い環境です。このような状況が発生した場合、AEM は引き続き古いスキーマを使用します。

このようなシナリオが発生しないようにするには、次の手順を実行してスキーマをアップグレードします。

1. アップグレードが必要な AEM インスタンスをシャットダウンします。
1. データベーススキーマをアップグレードします。この結果を達成するために必要なツール確認するには、データベースのタイプに関するドキュメントを参照してください。

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

サービスユーザーが以前の AEM バージョンで、通常のユーザーとして適切にタグ付けされていない場合があります。

このような状況が発生した場合、アップグレードは失敗し、次のようなメッセージが表示されます。

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

この問題を回避するには、必ず次の手順を実行してください。

1. インスタンスを実稼動トラフィックから切り離します。
1. 問題の原因となっている 1 人以上のユーザーのバックアップを作成します。バックアップの作成は、パッケージマネージャーから実行できます。詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md)を参照してください。
1. 問題の原因となっている 1 人以上のユーザーを削除します。以下は、このカテゴリに該当する可能性のあるユーザーのリストです。

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## ログファイルのローテーション {#rotate-log-files}

アップグレードを開始する前に、現在のログファイルをアーカイブすることをお勧めします。これにより、アップグレード中やアップグレード後にログファイルを監視およびスキャンして、発生する可能性のある問題を特定および解決することが容易になります。
