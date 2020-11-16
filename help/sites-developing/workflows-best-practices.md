---
title: ワークフローのベストプラクティス
seo-title: ワークフローのベストプラクティス
description: 'null'
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 88%

---


# ワークフローのベストプラクティス{#workflow-best-practices}

ワークフローにより、Adobe Experience Manager（AEM）のアクティビティを自動化できます。

ワークフローは、通常、AEM 環境で発生する大量の処理を表します。そのため、カスタムワークフローステップがベストプラクティスに従って記述されていない場合や標準提供のワークフローが可能な限り効率的に実行されるよう設定されていない場合は、システムのパフォーマンスが低下する可能性があります。

したがって、ワークフローの実装は慎重に計画することを強くお勧めします。

## 設定 {#configuration}

（カスタマイズされたものか標準提供されたものかに関わらず）ワークフロープロセスを設定する際は、いくつかの点に注意してください。

### 一時的ワークフロー {#transient-workflows}

高い取り込み負荷を最適化するには、[ワークフローを一時的](/help/sites-developing/workflows.md#transient-workflows)として定義することができます。

ワークフローが一時的である場合、中間の作業ステップに関連する実行時データは、実行時に JCR に保持されません（出力レンディションはもちろん保持されます）。

次のような利点があります。

* ワークフロー処理時間が短縮されます（最大 10 ％）。
* リポジトリの肥大化が大幅に抑制されます。
* CRUD ワークフローをパージする必要はありません。
* さらに、圧縮する TAR ファイルの数が削減されます。

>[!CAUTION]
>
>業務上、監査目的でワークフローの実行時データを保持／アーカイブすることが求められる場合は、この機能を有効にしないでください。

### DAM ワークフローの調整 {#tuning-dam-workflows}

DAM ワークフローのパフォーマンスチューニングガイドラインについては、[AEM Assets パフォーマンスチューニングガイド](/help/assets/performance-tuning-guidelines.md)を参照してください。

### 同時実行ワークフローの最大数の設定 {#configure-the-maximum-number-of-concurrent-workflows}

AEM では、複数のワークフロースレッドを同時に実行できます。デフォルトでは、スレッド数はシステム上のプロセッサーコア数の半分になるように設定されています。

実行中のワークフローがシステムリソースを要求している場合、AEM が他のタスク（オーサリング UI のレンダリングなど）に使用できるリソースがほとんどないことを意味している可能性があります。その結果、画像の一括アップロードなどのアクティビティでシステムの応答が遅くなる場合があります。

この問題に対処するには、**Maximum Parallel Jobs** の数値をシステム上のプロセッサーコア数の半分から 4 分の 3 に相当する数に設定することをお勧めします。これにより、システムがこれらのワークフローを処理する際に、応答性を維持できる十分な容量が得られます。

To configure **Maximum Parallel Jobs**, you can either:

* Configure the **[OSGi Configuration](/help/sites-deploying/configuring-osgi.md)** from the AEM Web console; for **Queue: Granite Workflow Queue** (an **Apache Sling Job Queue Configuration**).

* Configure the queue can from the **Sling Jobs** option of the AEM Web console; for **Job Queue Configuration: Granite Workflow Queue**, at `http://localhost:4502/system/console/slingevent`.

Additionally, there is a separate configuration for the **Granite Workflow External Process Job Queue**. これは、**InDesign Server** や **Image Magick** などの外部バイナリを起動するワークフロープロセスに使用されます。

### 個々のジョブキューの設定 {#configure-individual-job-queues}

場合によっては、同時スレッドまたは他のキューオプションを個々のジョブに応じて制御するように個々のジョブキューを設定すると便利なことがあります。Web コンソールから個々のキューを追加および設定するには、**Apache Sling Job Queue Configuration** ファクトリを使用します。To find the appropriate topic to list, execute your workflow’s model and look for it in the **Sling Jobs** console; for example, at `http://localhost:4502/system/console/slingevent`.

また、個々のジョブキューを一時的ワークフローに追加することもできます。

### ワークフローのパージの設定 {#configure-workflow-purging}

標準インストールの場合、AEM にはメンテナンスコンソールが用意されており、このコンソールでは、日次および週次のメンテナンスアクティビティをスケジュールおよび設定できます。次に例を示します。

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

デフォルトでは、**週別メンテナンスウィンドウ**&#x200B;に&#x200B;**ワークフローのパージ**&#x200B;タスクがありますが、このタスクを実行するには事前に設定する必要があります。ワークフローのパージを設定するには、Web コンソールで新しい **Adobe Granite のワークフローのパージ設定**&#x200B;を追加する必要があります。

AEM のメンテナンスタスクについて詳しくは、[操作ダッシュボード](/help/sites-administering/operations-dashboard.md)を参照してください。

## カスタマイズ {#customization}

カスタムワークフロープロセスを記述する際は、留意する必要がある点がいくつかあります。

### ロケーション {#locations}

ワークフローのモデル、ランチャー、スクリプトおよび通知の定義は、タイプ（デフォルト、カスタムなど）に応じてリポジトリに保管されます。

>[!NOTE]
>
>[AEM 6.5 のリポジトリの再構成](/help/sites-deploying/repository-restructuring.md)も参照してください。

#### 場所 - ワークフローモデル {#locations-workflow-models}

ワークフローモデルは、タイプに応じて次のリポジトリに保管されます。

* デフォルトのワークフロー設計は、次のパスに保管されます。

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >禁止事項：
   >
   >* カスタムのワークフローモデルをこのフォルダーに配置すること
   >* edit anything in `/libs`

   >
   >変更内容が、アップグレード時や、ホットフィックス、Cumulative Fix Pack またはサービスパックの適用時に上書きされる場合があるからです。

* カスタムのワークフロー設計は、次の場所に保管されます。

   ```
   /conf/global/settings/workflow/models/...
   ```

* 実行時のワークフロー設計（デフォルトとカスタムの両方）は、次のパスに保管されます。

   `/var/workflow/models/`

* レガシーのワークフロー設計（設計時と実行時の両方）は、次のパスに保管されます。

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >これらの設計が *AEM UI を使用*&#x200B;して編集された場合は、詳細情報が新しい場所にコピーされます。

#### 場所 - ワークフローランチャー {#locations-workflow-launchers}

ワークフローランチャーの定義も、タイプに応じて次のリポジトリに保管されます。

* デフォルトのワークフローランチャーは、次のパスに保管されます。

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >禁止事項：
   >
   >* カスタムのワークフローランチャーをこのフォルダーに配置すること
   >* edit anything in `/libs`

   >
   >変更内容が、アップグレード時や、ホットフィックス、Cumulative Fix Pack またはサービスパックの適用時に上書きされる場合があるからです。

* カスタムのワークフローランチャーは、次の場所に保管されます。

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* レガシーのワークフローランチャーは、次のパスに保管されます。

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >これらの定義が *AEM UI を使用*&#x200B;して編集された場合は、詳細情報が新しい場所にコピーされます。

#### 場所 - ワークフロースクリプト {#locations-workflow-scripts}

ワークフロースクリプトも、タイプに応じて次のリポジトリに保管されます。

* デフォルトのワークフロースクリプトは、次のパスに保管されます。

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >禁止事項：
   >
   >* カスタムのワークフロースクリプトをこのフォルダーに配置すること
   >* edit anything in `/libs`

   >
   >変更内容が、アップグレード時や、ホットフィックス、Cumulative Fix Pack またはサービスパックの適用時に上書きされる場合があるからです。

* カスタムのワークフロースクリプトは、次の場所に保管されます。

   ```
   /apps/workflow/scripts/...
   ```

* レガシーのワークフロースクリプトは、次のパスに保管されます。

   `/etc/workflow/scripts/`

#### 場所 - ワークフロー通知 {#locations-workflow-notifications}

ワークフロー通知も、タイプに応じて次のリポジトリに保管されます。

* デフォルトのワークフロー通知の定義は、次のパスに保管されます。

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >禁止事項：
   >
   >* カスタムのワークフロー通知の定義をこのフォルダーに配置すること
   >* edit anything in `/libs`

   >
   >変更内容が、アップグレード時や、ホットフィックス、Cumulative Fix Pack またはサービスパックの適用時に上書きされる場合があるからです。

* カスタムのワークフロー通知の定義は、次の場所に保管されます。

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >ワークフロー通知のテキストを上書きする場合は、次の場所にオーバーレイされるパスを作成します。
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* レガシーのワークフロー通知の定義は、次のパスに保管されます。

   `/etc/workflow/notification/`

### プロセスセッション {#process-sessions}

カスタム開発の場合と同様に、以下の理由により、可能な場合はユーザーのセッションを使用することを常にお勧めします。

* セキュリティガイドラインに準拠するため
* システムでセッションの開始と終了を管理できるようにするため

ワークフロープロセスを実装すると、次のようになります。

* ワークフローセッションが提供されます。このワークフローセッションは、特別な理由がない限り使用する必要があります。  
* ワークフローステップから新しいセッションを作成することはできません。これは、状態の不整合が生じると同時に、ワークフローエンジン内で同時実行の問題が発生する可能性があるからです。
* ワークフローのプロセスステップ内から新しい JCR セッションを取得することはできません。Process Step API から提供されるワークフローセッションを JCR セッションに適応させる必要があります。次に例を示します。

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

セッションの保存：

* Inside a workflow process, if the `WorkflowSession` is being used to modify the repository then do not explicitly save the session - the workflow will save the session when it completes.
* `Session.Save` は、ワークフローステップ内から呼び出されないでください。

   * it is recommended to adapt the workflow jcr session; then `save` is not necessary as the workflow engine saves the session automatically once the workflow has finished executing.
   * プロセスの各ステップでは、独自の JCR セッションを作成しないことをお勧めします。

* 不要な保存操作をなくすことでオーバーヘッドを減らし、ワークフローの効率を高めることができます。

>[!CAUTION]
>
>推奨はされませんが、独自の JCR セッションを作成した場合は保存する必要があります。

### ランチャーの数／範囲の最小化 {#minimize-the-number-scope-of-launchers}

登録されているすべての[ワークフローランチャー](/help/sites-administering/workflows-starting.md#workflows-launchers)に対応するリスナーは 1 つです。

* このリスナーは、他のランチャーのグロビングプロパティで指定されているすべてのパスで変更をリッスンします。
* イベントがディスパッチされると、ワークフローエンジンは、各ランチャーを評価して、それを実行する必要があるかどうかを判断します。

作成するランチャーが多すぎると、評価プロセスの実行速度が低下します。

1 つのランチャーのリポジトリのルートにグロビングパスを作成すると、ワークフローエンジンは、作成／変更イベントをリッスンして、リポジトリ内の各ノードに対して評価します。このため、必要なランチャーのみを作成し、グロビングパスをできるだけ明確にすることをお勧めします。

これらのランチャーがワークフローの動作に与える影響により、使用されていない標準提供のランチャーを無効にすると有用な場合があります。

### ランチャーの設定の強化 {#configuration-enhancements-for-launchers}

The custom [launcher configuration](/help/sites-administering/workflows-starting.md#workflows-launchers) has been enhanced to support the following:

* 複数の条件を「AND」で組み合わせる。
* 1 つの条件内に複数の OR 条件を含める。
* 機能フラグが有効か無効かに基づいてランチャーを無効または有効にする。
* ランチャー条件で正規表現をサポートする。

### ワークフローを他のワークフローから開始しない {#do-not-start-workflows-from-other-workflows}

ワークフローは、オブジェクトがメモリ内に作成され、リポジトリ内でノードが追跡されるという両方の点において、大量のオーバーヘッドを生成する可能性があります。このため、ワークフローでは、他のワークフローを開始するのではなく、そのワークフロー内で処理をおこなうことをお勧めします。

この例として、一連のコンテンツに対するビジネスプロセスを実装し、そのコンテンツをアクティベートするワークフローが挙げられます。公開する必要があるコンテンツノードごとに&#x200B;**コンテンツをアクティベート**&#x200B;モデルを開始するのではなく、これらの各ノードをアクティベートするカスタムワークフロープロセスを作成することをお勧めします。この手法では追加の開発作業が必要になりますが、実行時には、アクティベートするたびに別のワークフローインスタンスを開始するよりも効率的です。

もう 1 つの例として、多数のノードを処理し、ワークフローパッケージを作成してアクティベートするワークフローが挙げられます。パッケージを作成し、そのパッケージをペイロードとして別のワークフローを開始するのではなく、パッケージを作成するステップ内でワークフローのペイロードを変更した後、同じワークフローモデル内でそのステップを呼び出してパッケージをアクティベートすることができます。

### ハンドラー処理の設定 {#handler-advance}

ワークフローモデルを設計する際に、ワークフローステップのハンドラー処理の設定を有効にすることができます。また、次に実行するステップを決定するコードをワークフローステップに追加し、実行することもできます。

パフォーマンスが向上するので、ハンドラー処理の設定を使用することをお勧めします。

### ワークフローステージ {#workflow-stages}

[ワークフローステージ](/help/sites-developing/workflows.md#workflow-stages)を定義し、タスク／ステップを特定のワークフローステージに割り当てることができます。

この情報は、[****&#x200B;インボックス&#x200B;**から作業項目の「ワークフロー情報**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)」タブをクリックしたときにワークフローの進行状況を表示するために使用されます。既存のワークフローモデルを編集して、ステージを追加できます。

### ページをアクティベートプロセスステップ {#activate-page-process-step}

**ページをアクティベートプロセス**&#x200B;ステップを実行するとページがアクティベートされますが、参照される DAM アセットは自動的に検出され、アクティベートされるわけではありません。

このステップをワークフローモデルの一部として使用することを計画している場合は、この点に注意する必要があります。

### アップグレードに関する考慮事項 {#upgrade-considerations}

インスタンスをアップグレードする場合：

* インスタンスをアップグレードする前に、すべてのカスタムワークフローモデルがバックアップされていることを確認してください。
* 次の[場所](#locations)にカスタムワークフローが格納されていないことを確認してください。

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>[AEM 6.5 のリポジトリの再構成](/help/sites-deploying/repository-restructuring.md)も参照してください。

## システムツール {#system-tools}

ワークフローの監視、メンテナンスおよびトラブルシューティングに役立つ多くのシステムツールがあります。All example URLs below use `localhost:4502`, but should be available on any author instance ( `<hostname>:<port>`).

### Sling ジョブ処理コンソール {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling ジョブ処理コンソールには次の情報が表示されます。

* 前回の再起動以降のシステム内のジョブの状態に関する統計情報が表示されます。
* すべてのジョブキューの設定も表示され、設定マネージャーでその設定を編集するためのショートカットが提供されます。

### ワークフローレポートツール {#workflow-report-tool}

ワークフローレポートツールは、パフォーマンスの低下を防ぐために 6.3 では削除されています。

### ワークフローメンテナンス操作 MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

ワークフローメンテナンス MBean は、完了したワークフローのパージやワークフロー統計情報の取得など、いくつかの便利なメンテナンスルーチンを公開します。

## その他の情報 {#further-information}

詳しくは、次のセクションを参照してください。

* [ワークフローの操作](/help/sites-authoring/workflows.md)
* [ワークフローの管理](/help/sites-administering/workflows.md)
* [ワークフローの作成と拡張](/help/sites-developing/workflows.md)
* [パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)