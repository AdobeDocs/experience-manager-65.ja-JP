---
title: ワークフローのベストプラクティス
seo-title: Workflow Best Practices
description: Adobe Experience Managerでのワークフローの操作に関するベストプラクティスについて説明します。
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 26%

---

# ワークフローのベストプラクティス{#workflow-best-practices}

ワークフローを使用すると、Adobe Experience Manager(AEM) アクティビティを自動化できます。

多くの場合、AEM環境で発生する処理の量が多いので、ベストプラクティスに従ってカスタムワークフロー手順が記述されない場合や、標準のワークフローが可能な限り効率的に実行するように設定されていない場合、結果としてシステムに影響が出ます。

したがって、ワークフローの実装を慎重に計画することを強くお勧めします。

## 設定 {#configuration}

ワークフロープロセス（カスタマイズされた、またはそのまま使用できる）を設定する際には、いくつかの点に注意する必要があります。

### 一時的ワークフロー {#transient-workflows}

取り込みの負荷を高く抑えるために、 [一時的なワークフロー](/help/sites-developing/workflows.md#transient-workflows).

ワークフローが一時的な場合、中間の作業手順に関連するランタイムデータは、実行時に JCR に保持されません（出力レンディションはもちろん保持されます）。

次のような利点があります。

* ワークフロー処理時間が最大 10%短縮されました。
* リポジトリの増加を大幅に削減します。
* パージに必要な CRUD ワークフローはなくなりました。
* さらに、コンパクト化する TAR ファイルの数を減らします。

>[!CAUTION]
>
>業務上、監査目的でワークフローの実行時データを保持／アーカイブすることが求められる場合は、この機能を有効にしないでください。

### DAM ワークフローの調整 {#tuning-dam-workflows}

DAM ワークフローのパフォーマンスチューニングガイドラインについては、 [AEM Assets Performance Tuning Guide](/help/assets/performance-tuning-guidelines.md).

### 同時ワークフローの最大数の設定 {#configure-the-maximum-number-of-concurrent-workflows}

AEMでは、複数のワークフロースレッドを同時に実行できます。 デフォルトでは、スレッド数はシステム上のプロセッサコア数の半分に設定されています。

実行されるワークフローがシステムリソースを要求する場合、AEMがオーサリング UI のレンダリングなど、他のタスクに使用する負荷がほとんど残っていないことを意味する場合があります。 その結果、バルク画像のアップロードなどのアクティビティ中にシステムの動作が遅くなる場合があります。

この問題に対処するため、Adobeでは、 **並列ジョブの最大数** は、システム上のプロセッサコア数の半分から 4 分の 3 の間に設定します。 これにより、このようなワークフローを処理する際にシステムの応答が遅くならないように、十分な容量が確保されます。

**Maximum Parallel Jobs**&#x200B;を設定するには、次のいずれかを実行します。

* **キュー：Granite のワークフローキュー**（**Apache Sling Job Queue Configuration**）用に、AEM web コンソールから **[OSGi 設定](/help/sites-deploying/configuring-osgi.md)**&#x200B;を行います。

* `http://localhost:4502/system/console/slingevent` の **Job Queue Configuration：Granite のワークフローキュー**&#x200B;用に、AEM web コンソールの **Sling ジョブ**&#x200B;オプションからキューを設定します。

さらに、**Granite Workflow External Process Job Queue** 用に別の設定があります。これは、外部バイナリを起動するワークフロープロセス（例： ）に使用されます。 **InDesign Server** または **Image Magick**.

### 個々のジョブキューの設定 {#configure-individual-job-queues}

場合によっては、個々のジョブキューを設定して、同時スレッドや他のキューオプションを個々のジョブ単位で制御すると便利です。 個々のキューは、Web コンソールから、 **Apache Sling Job Queue Configuration** 工場です。 一覧表示する適切なトピックを見つけるには、ワークフローのモデルを実行し、トピックを **Sling ジョブ**&#x200B;コンソール（例えば `http://localhost:4502/system/console/slingevent`）で探してください。

また、個々のジョブキューを一時的ワークフローに追加することもできます。

### ワークフローのパージの設定 {#configure-workflow-purging}

標準インストールのAEMには、メンテナンスコンソールが用意されています。このコンソールでは、日次および週次のメンテナンスアクティビティをスケジュールし、設定できます。次に例を示します。

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

デフォルトでは、 **週別メンテナンスウィンドウ** には、 **ワークフローのパージ** タスクを設定する必要がありますが、実行する前に設定する必要があります。 ワークフローのパージを設定するには、新しい **AdobeGranite のワークフローのパージ設定** を Web コンソールに追加する必要があります。

AEMのメンテナンスタスクについて詳しくは、 [運用ダッシュボード](/help/sites-administering/operations-dashboard.md).

## カスタマイズ {#customization}

カスタムワークフロープロセスを記述する際は、いくつかの点に留意する必要があります。

### ロケーション {#locations}

ワークフローモデル、ランチャー、スクリプトおよび通知の定義は、タイプ（標準、カスタムなど）に応じてリポジトリに保持されます。

>[!NOTE]
>
>[AEM 6.5 のリポジトリの再構成](/help/sites-deploying/repository-restructuring.md)も参照してください。

#### 場所 — ワークフローモデル {#locations-workflow-models}

ワークフローモデルは、タイプに応じてリポジトリに保存されます。

* 既製のワークフローデザインは、次のパスに保持されます。

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >次の操作は実行しないでください。
  >
  >* カスタムワークフローモデルの任意の場所をこのフォルダーに配置します。
  >* `/libs` 内の設定を編集すること
  >
  >変更は、アップグレード時またはホットフィックス、累積修正パック、またはサービスパックのインストール時に上書きされる場合があります。

* カスタムワークフローデザインは、次の場所に保持されます。

  ```
  /conf/global/settings/workflow/models/...
  ```

* 実行時のワークフロー設計（デフォルトとカスタムの両方）は、次のパスに保管されます。

  `/var/workflow/models/`

* レガシーのワークフロー設計（設計時と実行時の両方）は、次のパスに保管されます。

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >これらのデザインが編集された場合 *AEM UI の使用*&#x200B;を指定した場合、詳細が新しい場所にコピーされます。

#### 場所 — ワークフローランチャー {#locations-workflow-launchers}

ワークフローランチャーの定義も、次のタイプに従ってリポジトリに保存されます。

* 標準のワークフローランチャーは、次のパスに保持されます。

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >次の操作は実行しないでください。
  >
  >* カスタムワークフローランチャーの任意の場所をこのフォルダーに配置します。
  >* `/libs` 内の設定を編集すること
  >
  >変更は、アップグレード時またはホットフィックス、累積修正パック、またはサービスパックのインストール時に上書きされる場合があります。

* カスタムワークフローランチャーは、次の場所に保持されます。

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* レガシーのワークフローランチャーは、次のパスに保管されます。

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >これらの定義が編集された場合 *AEM UI の使用*&#x200B;を指定した場合、詳細が新しい場所にコピーされます。

#### 場所 — ワークフロースクリプト {#locations-workflow-scripts}

ワークフロースクリプトも、タイプに応じてリポジトリに保存されます。

* 標準のワークフロースクリプトは、次のパスに保持されます。

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >次の操作は実行しないでください。
  >
  >* カスタムワークフロースクリプトをこのフォルダーに配置する
  >* `/libs` 内の設定を編集すること
  >
  >変更は、アップグレード時またはホットフィックス、累積修正パック、またはサービスパックのインストール時に上書きされる場合があります。

* カスタムワークフロースクリプトは、次の場所に保持されます。

  ```
  /apps/workflow/scripts/...
  ```

* レガシーのワークフロースクリプトは、次のパスに保管されます。

  `/etc/workflow/scripts/`

#### ロケーション — ワークフロー通知 {#locations-workflow-notifications}

ワークフロー通知も、タイプに応じてリポジトリに保存されます。

* 既製のワークフロー通知の定義は、次のパスに保持されます。

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >次の操作は実行しないでください。
  >
  >* このフォルダーにカスタムワークフロー通知定義を配置する
  >* `/libs` 内の設定を編集すること
  >
  >変更は、アップグレード時またはホットフィックス、累積修正パック、またはサービスパックのインストール時に上書きされる場合があります。

* カスタムワークフロー通知の定義は、次の場所に保持されます。

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

カスタム開発の場合と同様に、可能な限りユーザーのセッションを使用することをお勧めします。

* セキュリティガイドラインを最も遵守するために
* システムがセッションの開閉を管理できるようにするには

ワークフロープロセスを実装する場合：

* ワークフローセッションが提供されます。このワークフローセッションは、特別な理由がない限り使用する必要があります。 
* ワークフローステップから新しいセッションを作成しないでください。これにより、状態に不整合が生じ、ワークフローエンジンで同時実行の問題が発生する可能性があります。
* ワークフローのプロセスステップ内から新しい JCR セッションを取得しないでください。プロセスステップ API で提供されるワークフローセッションを jcr セッションに適応させる必要があります。 次に例を示します。

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

セッションの保存：

* ワークフロープロセス内で `WorkflowSession` がリポジトリを変更するために使用されている場合は、セッションを明示的に保存しないでください。ワークフローにより、セッションは完了時に保存されます。
* `Session.Save` は、ワークフローステップから呼び出すことはできません。

   * ワークフロー JCR セッションを適応させることをお勧めします。その後ワークフローの実行が完了すると、ワークフローエンジンによってセッションが自動保存されるので、`save` は必要ありません。
   * プロセスステップで独自の jcr セッションを作成することはお勧めしません。

* 不要な保存操作をなくすことでオーバーヘッドを減らし、ワークフローの効率を高めることができます。

>[!CAUTION]
>
>ここでのレコメンデーションにもかかわらず、独自の JCR セッションを作成する場合は、それを保存する必要があります。

### ランチャーの数/範囲の最小化 {#minimize-the-number-scope-of-launchers}

全ての [ワークフローランチャー](/help/sites-administering/workflows-starting.md#workflows-launchers) 登録済み：

* 他のランチャーのグロビングプロパティで指定されたすべてのパスで変更をリッスンします。
* イベントがディスパッチされると、ワークフローエンジンは各ランチャーを評価して、実行する必要があるかどうかを判断します。

ランチャーが多すぎると、評価プロセスの実行に時間がかかります。

単一のランチャーでリポジトリのルートにグロビングパスを作成すると、ワークフローエンジンはリスンを実行し、リポジトリ内のすべてのノードに対する作成/変更イベントを評価します。 このため、必要なランチャーのみを作成し、グロビングパスをできる限り具体的にすることをお勧めします。

これらのランチャーがワークフローの動作に与える影響により、使用中でない標準のランチャーを無効にすると便利です。

### ランチャーの設定の強化 {#configuration-enhancements-for-launchers}

カスタムの[ランチャー設定](/help/sites-administering/workflows-starting.md#workflows-launchers)が強化され、以下の点がサポートされるようになりました。

* 複数の条件を「AND」で結合する。
* 1 つの条件内に OR 条件を含める。
* 機能フラグが有効か無効かに基づいてランチャーを無効にする/有効にします。
* ランチャー条件で正規表現をサポートする。

### 他のワークフローからワークフローを開始しない {#do-not-start-workflows-from-other-workflows}

ワークフローは、メモリ内に作成されたオブジェクトとリポジトリ内で追跡されるノードの両方の点で、大量のオーバーヘッドを伴う可能性があります。 このため、追加のワークフローを開始するよりも、ワークフロー内で処理を実行する方がよいと考えられます。

例えば、一連のコンテンツに対するビジネスプロセスを実装し、そのコンテンツをアクティベートするワークフローがこれに該当します。 これらの各ノードをアクティブにするカスタムワークフロープロセスを作成する方が、 **コンテンツを有効化** 公開する必要がある各コンテンツノードのモデル。 この方法では追加の開発作業が必要になりますが、実行時は、アクティベーションごとに別のワークフローインスタンスを開始するよりも効率的です。

別の例として、1 つの多数のノードを処理し、ワークフローパッケージを作成して、そのパッケージをアクティベートするワークフローがあります。 パッケージを作成し、パッケージをペイロードとして別のワークフローを開始する代わりに、パッケージを作成するステップでワークフローのペイロードを変更し、同じワークフローモデル内でパッケージをアクティブ化するステップを呼び出すことができます。

### ハンドラー処理の設定 {#handler-advance}

ワークフローモデルを設計する際に、ワークフローステップでハンドラー処理の設定を有効にすることができます。 または、ワークフローステップにコードを追加して、次に実行するステップを決定し、次に実行するステップを決定することもできます。

ハンドラー処理のパフォーマンスが向上するので、ハンドラー処理の使用をお勧めします。

### ワークフローステージ {#workflow-stages}

次の項目を定義できます。 [ワークフローステージ](/help/sites-developing/workflows.md#workflow-stages)次に、特定のワークフローステージにタスク/ステップを割り当てます。

この情報は&#x200B;[**、**&#x200B;インボックス&#x200B;**から作業項目の「ワークフロー情報**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)」タブをクリックしたときにワークフローの進行状況を表示するために使用されます。既存のワークフローモデルを編集してステージを追加することができます。

### ページプロセスステップを有効化 {#activate-page-process-step}

The **ページのアクティベートプロセス** ステップによってページがアクティベートされますが、参照されている DAM アセットが自動的に見つからず、それらもアクティベートされません。

この手順をワークフローモデルの一部として使用する場合は、この点に注意してください。

### アップグレードに関する考慮事項 {#upgrade-considerations}

インスタンスをアップグレードする場合：

* インスタンスをアップグレードする前に、カスタムワークフローモデルが必ずバックアップされていることを確認してください。
* カスタムワークフローが以下に保存されていないことを確認します。 [場所](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>[AEM 6.5 のリポジトリの再構成](/help/sites-deploying/repository-restructuring.md)も参照してください。

## システムツール {#system-tools}

ワークフローの監視、保守、トラブルシューティングに役立つ多くのシステムツールを使用できます。 以下に示す URL の例ではすべて `localhost:4502` を使用していますが、どのオーサーインスタンス（`<hostname>:<port>`）を使用しても構いません。

### Sling ジョブ処理コンソール {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling ジョブ処理コンソールには、次の情報が表示されます。

* 前回の再起動以降の、システム内のジョブの状態に関する統計。
* すべてのジョブキューの設定も表示され、設定マネージャーでその設定を編集するためのショートカットが提供されます。

### ワークフローレポートツール {#workflow-report-tool}

パフォーマンスの低下を防ぐため、ワークフローレポートツールは 6.3 で削除されています。

### ワークフローメンテナンス操作 MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

ワークフローメンテナンス MBean は、完了したワークフローのパージやワークフロー統計情報の取得など、いくつかの便利なメンテナンスルーチンを公開します。

## その他の情報 {#further-information}

詳しくは、次のセクションを参照してください。

* [ワークフローの操作](/help/sites-authoring/workflows.md)
* [ワークフローの管理](/help/sites-administering/workflows.md)
* [ワークフローの作成と拡張 ](/help/sites-developing/workflows.md)
* [パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)
