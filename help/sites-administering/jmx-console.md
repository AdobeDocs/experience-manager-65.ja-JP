---
title: JMX コンソールを使用したサーバーリソースの監視
seo-title: Monitoring Server Resources Using the JMX Console
description: JMX コンソールを使用してサーバーリソースを監視する方法について説明します。
seo-description: Learn how to monitor server resources using the JMX console.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '4957'
ht-degree: 100%

---

# JMX コンソールを使用したサーバーリソースの監視{#monitoring-server-resources-using-the-jmx-console}

JMX コンソールを使用すると、CRX サーバー上のサービスを監視および管理できます。以下の節では、JMX フレームワークによって明らかになる属性および操作についてまとめます。

コンソール制御の使用方法について詳しくは、[JMX コンソールの使用](#using-the-jmx-console)を参照してください。JMX の背景情報については、Oracle web サイトの [Java Management Extensions (JMX) Technology](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) ページを参照してください。

JMX コンソールを使用して、MBean を作成し、サービスを管理する方法について詳しくは、[サービスと JMX コンソールの統合](/help/sites-developing/jmx-integration.md)を参照してください。

## ワークフローのメンテナンス {#workflow-maintenance}

実行中、完了済み、期限切れ、または失敗したワークフローインスタンスを管理するための操作です。

* ドメイン：com.adobe.granite.workflow
* タイプ：メンテナンス

>[!NOTE]
>
>その他のワークフロー管理ツールおよびワークフローインスタンスに考えられるステータスの説明は、[ワークフローコンソール](/help/sites-administering/workflows-administering.md)を参照してください。

### 運用 {#operations}

**listRunningWorkflowsPerModel** ワークフローモデルごとに、実行されているワークフローインスタンスの数をリストします。

* 引数：なし
* 戻り値：数およびモデル ID の列を含む表形式のデータ

**listCompletedWorkflowsPerModel** ワークフローモデルごとに、完了したワークフローインスタンスの数をリストします。

* 引数：なし
* 戻り値：数およびモデル ID の列を含む表形式のデータ

**returnWorkflowQueueInfo** 処理済み、および処理に向けて待機中のワークフロー項目に関する情報をリストします。

* 引数：なし
* 戻り値：以下の列を含む表形式のデータ：

   * ジョブ
   * キュー名
   * アクティブなジョブ
   * 平均処理時間
   * 平均待機時間
   * キャンセルされたジョブ
   * 失敗したジョブ
   * 完了したジョブ
   * 処理済みのジョブ
   * 待機中のジョブ

**returnWorkflowJobTopicInfo** ワークフロージョブの処理情報を、トピックごとにまとめてリストします。

* 引数：なし
* 戻り値：以下の列を含む表形式のデータ：

   * トピック名
   * 平均処理時間
   * 平均待機時間
   * キャンセルされたジョブ
   * 失敗したジョブ
   * 完了したジョブ
   * 処理済みのジョブ

**returnFailedWorkflowCount** 失敗したワークフローインスタンスの数を表示します。クエリ対象のワークフローモデルを指定したり、すべてのワークフローモデルの情報を取得したりできます。

* 引数：

   * モデル：問い合わせるモデルの ID。すべてのワークフローモデルについて失敗したワークフローインスタンスの数を確認するには、値を指定しません。ID は model ノードのパスで、例は次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：失敗したワークフローインスタンスの数。

**returnFailedWorkflowCountPerModel** ワークフローモデルごとに、失敗したワークフローインスタンスの数を表示します。

* 引数：なし
* 戻り値：数およびモデル ID の列を含む表形式のデータ

**terminateFailedInstances** 失敗したワークフローインスタンスを終了します。失敗したインスタンスをすべて終了するか、特定のモデルの失敗したインスタンスのみを終了するかを指定できます。オプションで、終了後にインスタンスを再開できます。また、操作をテストして、実際に操作を行わずに結果を確認することもできます。

* 引数：

   * インスタンスを再開：（オプション） `true` 値を指定して、インスタンスを終了後に再開します。デフォルト値 `false` では、終了したワークフローインスタンスは再開されません。
   * ドライラン：（オプション） `true` の値を指定して、実際に操作を行わずに操作の結果を確認します。デフォルト値 `false` では、操作が実行されます。
   * モデル：（オプション）操作が適用されるモデルの ID。すべてのワークフローモデルの失敗したインスタンスに操作を適用するには、モデルを指定しないでください。ID は model ノードのパスで、例は次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：以下の列を含む、終了されたインスタンスに関する表形式のデータ：

   * イニシエーター
   * インスタンス ID
   * モデル ID
   * ペイロード
   * 開始コメント
   * ワークフロータイトル

**retryFailedWorkItems** 失敗した作業項目のステップの実行を試みます。失敗した作業項目をすべて再試行するか、特定のワークフローモデルの失敗した作業項目のみを再試行するかを指定できます。オプションで、操作をテストして、実際に操作を行わずに結果を確認することもできます。

* 引数：

   * ドライラン：（オプション） `true` の値を指定して、実際に操作を行わずに操作の結果を確認します。デフォルト値 `false` では、操作が実行されます。
   * モデル：（オプション）操作の適用先のモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルの失敗した作業項目に対して操作が適用されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：以下の列を含む、再試行された作業項目に関する表形式のデータ：

   * イニシエーター
   * インスタンス ID
   * モデル ID
   * ペイロード
   * 開始コメント
   * ワークフロータイトル

**PurgeActive** 特定の時間が経過したアクティブなワークフローインスタンスを削除します。すべてのモデルのアクティブなインスタンスをパージするか、特定のモデルのインスタンスのみをパージするかを指定できます。オプションで、操作をテストして、実際に操作を行わずに結果を確認することもできます。

* 引数：

   * モデル：（オプション）操作の適用先のモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルのワークフローインスタンスに対して操作が適用されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * ワークフローが開始してからの日数：パージするワークフローインスタンスの有効期間（日数）。
   * ドライラン：（オプション） `true` の値を指定して、 実際に操作を行わずに操作の結果を確認します。デフォルト値 `false` では、操作が実行されます。

* 戻り値：以下の列を含む、パージされたアクティブなワークフローインスタンスに関する表形式のデータ：

   * イニシエーター
   * インスタンス ID
   * モデル ID
   * ペイロード
   * 開始コメント
   * ワークフロータイトル

**countStaleWorkflows** 古くなったワークフローインスタンスの数を返します。古くなったインスタンスの数は、すべてのワークフローモデルに関して、または特定のモデルに関して取得できます。

* 引数：

   * モデル：（オプション）操作の適用先のモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルのワークフローインスタンスに対して操作が適用されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：古くなったワークフローインスタンスの数。

**restartStaleWorkflows** 古くなったワークフローインスタンスを再開します古くなったインスタンスをすべて再開するか、特定のモデルの古くなったインスタンスのみを再開するかを指定できます。また、操作をテストして、実際に操作を行わずに結果を確認することもできます。

* 引数：

   * モデル：（オプション）操作が適用されるモデルの ID。すべてのワークフローモデルの古くなったインスタンスに操作を適用するには、モデルを指定しないでください。ID は model ノードのパスで、例は次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * ドライラン：（オプション） `true` の値を指定して、実際に操作を行わずに操作の結果を確認します。デフォルト値 `false` では、操作が実行されます。

* 戻り値：再開されたワークフローインスタンスのリスト。

**fetchModelList** すべてのワークフローモデルのリストを表示します。

* 引数：なし
* 戻り値：モデル ID 列とモデル名列を含む、ワークフローモデルを識別する表形式のデータ。

**countRunningWorkflows** 実行中のワークフローインスタンスの数を返します。実行中のインスタンスの数は、すべてのワークフローモデルに関して、または特定のモデルに関して取得できます。

* 引数：

   * モデル：（オプション）実行中のインスタンスの数を返すモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルの実行中のインスタンスの数が返されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：実行中のワークフローインスタンスの数。

**countCompletedWorkflows** 完了したワークフローインスタンスの数を返します。完了したインスタンスの数は、すべてのワークフローモデルに関して、または特定のモデルに関して取得できます。

* 引数：

   * モデル：（オプション）完了したインスタンスの数を返すモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルの完了したインスタンスの数が返されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* 戻り値：完了したワークフローインスタンスの数。

**purgeCompleted** 特定の期間が経過した完了済みワークフローの記録をリポジトリから削除します。この操作を定期的に使用すると、ワークフローを多用するときにリポジトリのサイズを最小限に抑えることができます。すべてのモデルの完了したインスタンスをパージするか、特定のモデルのインスタンスのみをパージするかを指定できます。オプションで、操作をテストして、実際に操作を行わずに結果を確認することもできます。

* 引数：

   * モデル：（オプション）操作の適用先のモデルの ID。モデルを指定しない場合は、すべてのワークフローモデルのワークフローインスタンスに対して操作が適用されます。ID は model ノードのパスで、例えば、次のようになります。

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * ワークフローが完了してからの日数：ワークフローインスタンスが完了状態になっている日数。
   * ドライラン：（オプション） `true` の値を指定して、実際に操作を行わずに操作の結果を確認します。デフォルト値 `false` では、操作が実行されます。

* 戻り値：以下の列を含む、パージされた完了済みのワークフローインスタンスに関する表形式のデータ：

   * イニシエーター
   * インスタンス ID
   * モデル ID
   * ペイロード
   * 開始コメント
   * ワークフロータイトル

## リポジトリ {#repository}

CRX リポジトリに関する情報

* ドメイン：com.adobe.granite
* タイプ：リポジトリ

### 属性 {#attributes}

**名前** JCR リポジトリ実装の名前。読み取り専用。

**バージョン** リポジトリの実装バージョン。読み取り専用。

**HomeDir** リポジトリが配置されているディレクトリ。デフォルトの場所は、＜QuickStart_Jar_Location＞／crx-quickstart／repository です。読み取り専用。

**CustomerName** ソフトウェアライセンスの発行対象である顧客の名前。読み取り専用。

**LicenseKey** リポジトリのこのインストールの一意なライセンスキー。読み取り専用。

**AvailableDiskSpace** リポジトリのこのインスタンスで使用可能なディスク容量（メガバイト単位）。読み取り専用。

**MaximumNumberOfOpenFiles** 一度に開くことのできるファイルの数。読み取り専用。

**SessionTracker** crx.debug.sessions システム変数の値。true は、デバッグセッションを示します。false は通常のセッションを示します。読み取り／書き込み。

**Descriptors** リポジトリのプロパティを表すキーと値のペア。すべてのプロパティは読み取り専用です。

<table>
 <tbody>
  <tr>
   <th>キー</th>
   <th>値</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>ノードとノードのプロパティに同じ名前を指定できるかどうかを示します。true は同じ名前がサポートされていることを示し、false はサポートされていないことを示します。 </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>参照不可能なノード識別子の安定性を示します。以下の値が指定可能です。
    <ul>
     <li>identifier.stability.indefinite.duration：識別子は変わりません。</li>
     <li>identifier.stability.method.duration：メソッド呼び出しの合間に識別子が変わる可能性があります。</li>
     <li>identifier.stability.save.duration：保存／更新サイクル内では、識別子は変わりません。</li>
     <li>identifier.stability.session.duration：セッション中は、識別子は変わりません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>JCR 1.0 XPath クエリ言語がサポートされているかどうかを示します。true はサポートを示し、false はサポートなしを示します。</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>system.id ファイル内のシステム識別子。</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>JCR 1.0 XPath クエリ言語がサポートされているかどうかを示します。true はサポートを示し、false はサポートなしを示します。</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>リポジトリ実装のバージョン。</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>あるノードのプライマリノードタイプを変更できるかどうかを示します。true はプライマリノードタイプを変更できることを示し、false は変更がサポートされていないことを示します。</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>ノードタイプの管理がサポートされているかどうかを示します。true はサポートされていることを示し、false はサポートなしを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>継承されたプロパティまたは子ノードで定義されているノードタイプを上書きできるかどうかを示します。true は上書きがサポートされていることを示し、false は上書きなしを示します。</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true はリポジトリ変更の非同期の監視がサポートされていることを示します。非同期の監視をサポートすると、変更が発生するたびに、アプリケーションが通知を受け取ったり、通知に応答したりできます。</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true は、フルテキスト検索を実行するために jcrfn:contains 関数（XPath の場合）または CONTAINS 関数（SQL の場合）を含む XPath クエリおよび SQL クエリで jcr:score 疑似プロパティが使用できることを示します。</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true は、リポジトリが単純なバージョン管理をサポートしていることを示します。単純なバージョン管理を使用すると、一連の連続したノードのバージョンが維持されます。</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true は、API を使用したワークスペースの作成および削除をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true は、既存のノードの mixin ノードタイプの追加および削除をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true は、プライマリ項目を子として含めるノード定義がリポジトリによって可能になることを示します。プライマリ項目は、項目名がわからなくとも、API を使用してアクセスできます。</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true は、LEVEL_1_SUPPORTED と OPTION_XML_IMPORT_SUPPORTED がいずれも true であることを示します。</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true はリポジトリによって API を使用した書き込みアクセスが提供されることを示し、false は読み取り専用アクセスを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true は、既存のノードで使用中のノード定義を変更できることを示します。</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>リポジトリが実装する JCR 仕様のバージョン。</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true は、アプリケーションがリポジトリのジャーナル監視を実行できることを示します。ジャーナル監視を使用すると、一連の変更通知を特定の期間にわたって取得できます。 </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>リポジトリがサポートするクエリ言語。値なしは、クエリサポートがないことを示します。</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true は、ノードを XML コードとして書き出すことをリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true は複数のバイナリプロパティを持つノードタイプの登録をリポジトリがサポートしていることを示し、false は 1 つのノードタイプに対して単一のバイナリプロパティがサポートされていることを示します。</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true は、ノードアクセス用のユーザーの権限を設定および決定するために、リポジトリがアクセス制御をサポートすることを示します。</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true は、リポジトリが設定とベースラインの両方をサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true は、リポジトリが共有可能なノードの作成をサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>リポジトリクラスターの識別子。</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true は、保存されたクエリをリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true は、リポジトリがフルテキスト検索をサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>ノードタイプの継承に関するリポジトリサポートのレベルを示します。以下の値が指定可能です。</p> <p>node.type.management.inheritance.minimal：プライマリノードタイプの登録は、nt:base のみをスーパータイプとして持つものに限られます。mixin ノードタイプの登録は、スーパータイプがないものに限られます。</p> <p>node.type.management.inheritance.single：プライマリノードタイプの登録は、スーパータイプが 1 つのものに限られます。mixin ノードタイプの登録は、スーパータイプが 1 つ以下のものに限られます。</p> <p><br /> node.type.management.inheritance.multiple：プライマリノードタイプは、1 つ以上のスーパータイプに登録できます。mixin ノードタイプは、0 個以上のスーパータイプに登録できます。</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true は、このクラスターノードがクラスターのマスターとして望ましいことを示します。</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true は、リポジトリがトランザクションをサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>リポジトリベンダーの URL。</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true は、ノードプロパティの値の制約をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>登録済みのノードタイプが指定可能なプロパティタイプを表す javax.jcr.PropertyType 定数の配列。長さがゼロの配列は、登録済みのノードタイプがプロパティ定義を指定できないことを示します。プロパティタイプは、STRING、URI、BOOLEAN、LONG、DOUBLE、DECIMAL、BINARY、DATE、NAME、PATH、WEAKREFERENCE、REFERENCE および UNDEFINED（サポートされている場合）です。</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true は、子ノードの順序の保持をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>リポジトリベンダーの名前。</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>クエリ内の結合のサポートレベル。以下の値が指定可能です。</p>
    <ul>
     <li>query.joins.none：結合のサポートなし。クエリでは 1 つのセレクターを使用できます。</li>
     <li>query.joins.inner：内部結合のサポート。</li>
     <li>query.joins.inner.outer：内部結合と外部結合のサポート。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true は、リポジトリが XPath 1.0 クエリ言語をサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true は、XML コードをコンテンツとして読み込むことをリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true は、同じ名前の兄弟ノード（親が同じノード）をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true は、残差定義を持つ名前プロパティをリポジトリがサポートしていることを示します。サポートされている場合、項目定義の名前属性にアスタリスク（「*」）を指定できます。</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true は、ノード作成時にそのノードの子項目（ノードまたはプロパティ）の自動作成をリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true は、このリポジトリノードがクラスターのマスターノードであることを示します。</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true は、option.xml.export.support が true であり、query.languages がゼロ以外の長さであることを示します。</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true は、ファイルされていないコンテンツをリポジトリがサポートしていることを示します。ファイルされていないノードは、リポジトリ階層の一部ではありません。</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>リポジトリが実装する JCR 仕様の名前。</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true は、リポジトリが完全なバージョン管理をサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>リポジトリの名前。</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true は、リポジトリがノードのロックをサポートしていることを示します。ロックすると、他のユーザーが一時的に変更できなくなります。</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true は、リポジトリがアクティビティをサポートしていることを示します。アクティビティとは、別のワークスペースに統合されるワークスペースで実行される一連の変更のことです。</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true は、ゼロ個以上の値を指定できるノードプロパティをリポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true は、保持ポリシーをコンテンツに適用する外部保持管理アプリケーションの使用、および保持と解放を、リポジトリがサポートしていることを示します。</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true は、リポジトリがライフサイクル管理をサポートしていることを示します。</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** リポジトリ内のワークスペースの名前。読み取り専用。

**DataStoreGarbageCollectionDelay** 10 番目のノードごとにスキャンした後、ガベージコレクションがスリープする時間をミリ秒で指定します。読み取り／書き込み。

**BackupDelay** バックアップの各ステップ間でバックアッププロセスがスリープする時間（ミリ秒）です。読み取り／書き込み。

**BackupInProgress** true の値がバックアップ処理が実行されていることを示します 。読み取り専用。

**BackupProgress** 現在のバックアップについて、全ファイルのバックアップが完了した割合。読み取り専用。

**CurrentBackupTarget** 現在のバックアップの場合、バックアップファイルが保存されている ZIP ファイルです。バックアップが進行中でない場合は、値は表示されません。読み取り専用。

**BackupWasSuccessful** 値が true の場合、現在のバックアップ中にエラーが発生していないか、処理中のバックアップがありません。false は、現在のバックアップ中にエラーが発生したことを示します。読み取り専用。

**BackupResult** 現在のバックアップのステータス。次の値を指定できます。

* バックアップ中：バックアップが現在実行中です。
* バックアップキャンセル：バックアップがキャンセルされました。
* バックアップでエラー発生：バックアップ中にエラーが発生しました。エラーメッセージでは、原因に関する情報が提供されます。
* バックアップ完了：バックアップが成功しました。
* バックアップの実行なし：進行中のバックアップがありません。

読み取り専用。

**TarOptimizationRunningSince** 現在の TAR ファイル最適化プロセスの開始時刻。読み取り専用。

**TarOptimizationDelay** TAR 最適化プロセスの各ステップの合間にプロセスがスリープ状態になる時間（ミリ秒単位）。読み取り／書き込み。

**ClusterProperties** クラスターのプロパティと値を表すキーと値のペアのセット。テーブル内の各行にクラスタープロパティが 1 つずつ表示されます。読み取り専用。

**ClusterNodes** リポジトリクラスターのメンバー。

**ClusterId** このリポジトリクラスターの識別子。読み取り専用。

**ClusterMasterId** このリポジトリクラスターのマスターノードの識別子。読み取り専用。

**ClusterNodeId** リポジトリクラスターのこのノードの識別子。読み取り専用。

### 操作 {#operations-1}

**createWorkspace** このリポジトリにワークスペースを作成します。

* 引数：

   * 名前：新しいワークスペースの名前を表す String 値。

* 戻り値：なし

**runDataStoreGarbageCollection**&#x200B;リポジトリノードでガベージコレクションを実行します。

* 引数：

   * delete：未使用のリポジトリ項目を削除するかどうかを示す Boolean 値。true の値を指定すると、未使用のノードおよびプロパティが削除されます。false の値を指定すると、すべてのノードがスキャンされますが、何も削除されません。

* 戻り値：なし

**stopDataStoreGarbageCollection** 実行中のデータストアのガベージコレクションを停止します。

* 引数：なし
* 戻り値：現在のステータスの文字列表現

**startBackup** リポジトリデータを ZIP ファイルにバックアップします。

* 引数：

   * `target`：（任意）リポジトリデータをアーカイブする ZIP ファイルまたはディレクトリの名前を表す `String` 値。ZIP ファイルを使用するには、ZIP ファイル名の拡張子を含めます。ディレクトリを使用する場合は、ファイル名の拡張子を含めません。

      増分バックアップを実行するには、以前にバックアップに使用したディレクトリを指定します。

      絶対パスまたは相対パスを指定できます。相対パスは、crx-quickstart ディレクトリの親を基準とした相対パスです。

      値を指定しない場合、デフォルト値は `backup-currentdate.zip` が使用され、`currentdate` の形式は `yyyyMMdd-HHmm` となります。

* 戻り値：なし

**cancelBackup** 現在のバックアッププロセスを停止して、データのアーカイブ用にプロセスによって作成された一時アーカイブを削除します。

* 引数：なし
* 戻り値：なし

**blockRepositoryWrites**&#x200B;リポジトリデータに対する変更をブロックします。すべてのリポジトリバックアップリスナーに、ブロックが通知されます。

* 引数：なし
* 戻り値：なし

**unblockRepositoryWrites**&#x200B;リポジトリからブロックを削除します。すべてのリポジトリバックアップリスナーに、ブロックの削除が通知されます。

* 引数：なし
* 戻り値：なし

**startTarOptimization** tarOptimizationDelay のデフォルト値を使用して、TAR ファイルの最適化プロセスを開始します。

* 引数：なし
* 戻り値：なし

**stopTarOptimization** TAR ファイルの最適化を停止します。

* 引数：なし
* 戻り値：なし

**tarIndexMerge** すべての TAR セットにおける上位のインデックスファイルを結合します。上位のインデックスファイルは、複数のメジャーバージョンのファイルです。例えば、index_1_1.tar ファイル、index_2_0.tar ファイル、index_3_0.tar ファイルは、index_3_1.tar ファイルに結合されます。結合されたファイルは削除されます（前の例では、index_1_1.tar、index_2_0.tar、index_3_0.tar が削除されます）。

* 引数：

   * `background`：実行中に web コンソールを使用できるように、操作をバックグラウンドで実行するかどうかを示す Boolean 値です。値が true の場合、操作をバックグラウンドで実行します。

* 戻り値：なし

**becomeClusterMaster** このリポジトリノードをクラスターのプライマリノードとして設定します。プライマリに設定されていない場合、このコマンドは現在のプライマリインスタンスのリスナーを停止し、現在のノードのプライマリリスナーを開始します。その後、このノードがプライマリノードとして設定され、再起動されると、クラスター内の他のすべてのノード（プライマリによって制御されるノード）がこのインスタンスに接続します。

* 引数：なし
* 戻り値：なし

**joinCluster** このリポジトリを、クラスターのプライマリによって制御されるノードとしてクラスターに追加します。認証のためにユーザー名とパスワードを指定する必要があります。接続では基本認証を使用します。セキュリティ認証情報は、サーバーに送信される前に base-64 エンコードされます。

* 引数：

   * `master`：プライマリリポジトリノードを実行するコンピューターの IP アドレスまたはコンピューター名を表す文字列値。
   * `username`：クラスターでの認証に使用する名前。
   * `password`：認証に使用するパスワード。

* 戻り値：なし

**traversalCheck** 特定のノードで始まるサブツリー内の不整合をトラバースし、オプションで修正します。これについては、永続性マネージャーに関するドキュメントで詳しく説明します。

**consistencyCheck** データストアの整合性を確認し、オプションで修正します。これについては、データストアに関するドキュメントで詳しく説明します。

## リポジトリ統計（TimeSeries） {#repository-statistics-timeseries}

`org.apache.jackrabbit.api.stats.RepositoryStatistics` で定義される、各統計タイプの TimeSeries フィールドの値。

* ドメイン：`com.adobe.granite`
* 型：`TimeSeries`
* 名前：`org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum クラスの、以下のいずれかの値。

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### 属性 {#attributes-1}

報告される統計タイプごとに、以下の属性が提供されています。

* ValuePerSecond：過去 1 分間の、1 秒あたりの測定値。読み取り専用。
* ValuePerMinute：過去 1 時間の、1 分あたりの測定値。読み取り専用。
* ValuePerHour：過去 1 週間の、1 時間あたりの測定値。読み取り専用。
* ValuePerWeek：過去 3 年間の、1 週あたりの測定値。読み取り専用。

## リポジトリクエリ統計 {#repository-query-stats}

リポジトリクエリに関する統計情報。

* ドメイン：com.adobe.granite
* タイプ：QueryStat

### 属性 {#attributes-2}

**SlowQueries** 完了までの所要時間が最長だったリポジトリクエリに関する情報。読み取り専用。

**SlowQueriesQueueSize** SlowQueries リストに含めるクエリの最大数。読み取り／書き込み。

**PopularQueries** 最も多く発生したリポジトリクエリに関する情報。読み取り専用。

**PopularQueriesQueueSize** Popular Queries リスト内のクエリの最大数。読み取り／書き込み。

### 操作 {#operations-2}

**clearSlowQueriesQueue** SlowQueries リストからすべてのクエリを削除します。

* 引数：なし
* 戻り値：なし

**clearPopularQueriesQueue** PopularQueries リストからすべてのクエリを削除します。

* 引数：なし
* 戻り値：なし

## レプリケーションエージェント {#replication-agents}

レプリケーションエージェントごとにサービスを監視します。レプリケーションエージェントを作成すると、JMX コンソールにサービスが自動的に表示されます。

* **ドメイン：** com.adobe.granite.replication
* **タイプ：**&#x200B;エージェント
* **名前：**&#x200B;値なし
* **プロパティ：** {id=&quot;*Name*&quot;}。*Name* は、エージェントの名前プロパティの値です。

### 属性 {#attributes-3}

**ID** レプリケーションエージェント設定の識別情報を表す String 値。複数のエージェントが同じ設定を使用できます。読み取り専用。

**Valid** エージェントが正しく設定されているかどうかを示すブール値。

* `true`：有効な設定です。
* `false`：設定にエラーが含まれます。

読み取り専用。

**Enabled** エージェントが有効かどうかを示すブール値。

* `true`：有効。
* `false`：無効。

**QueueBlocked** キューが存在し、ブロックされているかどうかを示すブール値。

* `true`：ブロック。自動再試行は保留中です。
* `false`：ブロックされていないか、存在しません。

読み取り専用。

**QueuePaused** ジョブキューが一時停止しているかどうかを示すブール値。

* `true`：一時停止（休止）しています。
* `false`：一時停止していないか、存在しません。

読み取り／書き込み。

**QueueNumEntries** エージェントキュー内のジョブ数を表す整数値。読み取り専用。

**QueueStatusTime** 表示されているステータス値が取得されたサーバー上の時間を示す Date 値。この値は、ページが読み込まれた時刻と一致します。読み取り専用。

**QueueNextRetryTime** ブロックされたキューについて、次回の自動再試行日を示す Date 値。時間が表示されない場合、キューはブロックされません。読み取り専用。

**QueueProcessingSince** 現在のジョブの処理を開始した日を示す Date 値。時間が表示されない場合、キューはブロックされるか、アイドル状態となります。読み取り専用。

**QueueLastProcessTime** 前回のジョブの完了日を示す Date 値。読み取り専用。

### 操作 {#operations-3}

**queueForceRetry** ブロックされているキューに対して、再試行コマンドを発行します。

* 引数：なし
* 戻り値：なし

**queueClear** キューからすべてのジョブを削除します。

* 引数：なし
* 戻り値：なし

## Sling エンジン {#sling-engine}

HTTP 要求に関する統計を提供し、SlingRequestProcessor サービスのパフォーマンスを監視できるようにします。

* ドメイン：org.apache.sling
* タイプ：エンジン
* プロパティ：{service=RequestProcessor}

### 属性 {#attributes-4}

**RequestsCount** 統計が最後にリセットされた以降に発生した要求の数。

**MinRequestDurationMsec** 統計が最後にリセットされた以降に要求の処理に要した最短時間（ミリ秒単位）。

**MaxRequestDuratioMsec** 統計が最後にリセットされた以降に要求の処理に要した最長時間（ミリ秒単位）。

**StandardDeviationDurationMsec** 要求の処理に要した時間の標準偏差。標準偏差は、統計が最後にリセットされた以降のすべての要求を使用して計算されます。

**MeanRequestDurationMsec** 1 つの要求の処理に要した平均時間。平均は、統計が最後にリセットされて以降のすべての要求を使用して計算されます。

### 運用 {#operations-4}

**resetStatistics** すべての統計をゼロに設定します。特定の期間の要求処理のパフォーマンスを分析する必要があるときに統計をリセットします。

* 引数：なし
* 戻り値：なし

**id** パッケージ ID の文字列表現。

**installed** パッケージがインストールされているかどうかを示す boolean 値。

* `true`：インストールされています。
* `false`：インストールされていません。

**installedBy** パッケージを最後にインストールしたユーザーの ID。

**installedDate** パッケージが最後にインストールされた日付。

**size** パッケージのサイズ（バイト数）を保持する long 値。


## クイックスタートランチャー {#quickstart-launcher}

起動プロセスおよびクイックスタートランチャーに関する情報。

* ドメイン：com.adobe.granite.quickstart
* タイプ：ランチャー

### 運用 {#operations-5}

**log**

クイックスタートウィンドウにメッセージを表示します。

引数：

* p1： 表示するメッセージを表す `String` 値。
* 戻り値：なし

**startupFinished**

サーバーランチャーの startupFinished メソッドを呼び出します。このメソッドにより、Web ブラウザーにようこそページが開きます。

* 引数：なし
* 戻り値：なし

**startupProgress**

サーバー起動プロセスの完了値を設定します。クイックスタートウィンドウの進行状況バーが、完了値を表します。

* 引数：
   * p1：起動プロセスがどの程度完了したかを割合で表す浮動小数値。値の範囲はゼロから 1 です。例えば、0.3 は 30% 完了を示します。
* 戻り値：なし.

## サードパーティのサービス {#third-party-services}

いくつかのサードパーティのサーバーリソースでは、MBean がインストールされ、これによって属性および操作が JMX コンソールに提供されます。次の表では、サードパーティのリソースをリストし、詳細のリンクを提供します。

<table>
 <tbody>
  <tr>
   <th>ドメイン</th>
   <th>タイプ</th>
   <th>MBean クラス</th>
  </tr>
  <tr>
   <td>JMImplementation</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilation</li>
     <li>GarbageCollector</li>
     <li>メモリ</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>OperatingSystem</li>
     <li>Runtime</li>
     <li>Threading</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> パッケージ</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>framework</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> パッケージ</td>
  </tr>
 </tbody>
</table>

## JMX コンソールの使用 {#using-the-jmx-console}

JMX コンソールには、サーバー上で実行されているいくつかのサービスに関する情報が表示されます。

* 属性：設定や実行時データなどのサービスプロパティ。属性は、読み取り専用の場合と読み取り／書き込み可能な場合があります。
* 操作：サービスで呼び出し可能なコマンド。

OSGi サービスでデプロイされる MBean により、サービスの属性および操作がコンソールに公開されます。MBean は、公開される属性および操作と、属性が読み取り専用か読み取り／書き込みかを決定します。

JMX コンソールのメインページには、サービスの表が含まれます。表の行ごとに、MBean によって公開されるサービスを 1 つずつ表します。

1. Web コンソールを開いて「JMX」タブをクリックします（[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）。
2. 任意のサービスのセル値をクリックして、そのサービスの属性と操作を確認します。
3. 属性値を変更するには、値をクリックし、表示されるダイアログボックスで値を指定して、「保存」をクリックします。
4. サービスの操作を呼び出すには、操作名をクリックし、表示されるダイアログボックスで引数値を指定して、「呼び出し」をクリックします。

## 監視のための外部 JMX アプリケーションの使用 {#using-external-jmx-applications-for-monitoring}

CRX を使用すると、外部アプリケーションと Managed Bean（MBean）が [Java Management Extensions（JMX）](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html)経由でやり取りできます。[JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) のような汎用コンソールやドメイン専用の監視アプリケーションを使用すると、CRX の設定やプロパティを取得および設定したり、パフォーマンスやリソース使用状況を監視したりできます。

### JConsole を使用した CRX への接続 {#using-jconsole-to-connect-to-crx}

JConsole を使用して CRX に接続するには、次の手順に従います。

1. ターミナルウィンドウを開きます。
1. 以下のコマンドを入力します。

   `jconsole`

JConsole が起動して、JConsole ウィンドウが表示されます。

### ローカルの CRX プロセスへの接続 {#connecting-to-a-local-crx-process}

JConsole には、ローカルの Java 仮想マシンプロセスのリストが表示されます。このリストには 2 つのクイックスタートプロセスが含まれます。ローカルプロセスのリストから、クイックスタート「CHILD」プロセス（通常は PID が大きいほうのプロセス）を選択します。

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### リモートの CRX プロセスへの接続 {#connecting-to-a-remote-crx-process}

リモート CRX プロセスに接続するには、リモート CRX プロセスをホストする JVM で、リモート JMX 接続を受け入れるように有効にする必要があります。

リモート JMX 接続を有効にするには、JVM の起動時に以下のシステムプロパティを設定する必要があります。

`com.sun.management.jmxremote.port=portNum`

上記のプロパティで、`portNum` は、JMX RMI 接続を有効にするポート番号です。未使用のポート番号を必ず指定してください。ローカルアクセス用の RMI コネクターを公開する以外に、このプロパティを設定すると、既知の名前「jmxrmi」を使用して、指定したポートのプライベート読み取り専用レジストリに追加の RMI コネクターが公開されます。

デフォルトでは、リモート監視用に JMX エージェントを有効にすると、パスワードファイルに基づいたパスワード認証が使用されます。パスワードファイルは、Java VM 起動時に以下のシステムプロパティを使用して指定する必要があります。

`com.sun.management.jmxremote.password.file=pwFilePath`

パスワードファイルの設定について詳しくは、[関連する JMX のドキュメント](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html)を参照してください。

例：

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### CRX で提供される MBean の使用 {#using-the-mbeans-provided-by-crx}

クイックスタートプロセスに接続後、JConsole では、CRX が実行されている JVM に対して、様々な一般的監視ツールが提供されます。

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

CRX の内部監視および設定オプションにアクセスするには、「MBean」タブに移動して、左側にある階層型のコンテンツツリーから、属性または操作の関心のあるセクションを選択します。例えば、com.adobe.granite/Repository/Operations セクションなどです。

そのセクション内で、必要な属性または操作を左ウィンドウから選択します。

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
