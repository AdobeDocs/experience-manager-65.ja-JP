---
title: JEE 上のAEM Forms サーバークラスターの設定とトラブルシューティングの方法
description: Adobe Experience Manager（AEM）Forms on JEE サーバークラスターの設定方法とトラブルシューティング方法について説明します。
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '3945'
ht-degree: 100%

---

# JEE サーバークラスター上の AEM Forms の設定とトラブルシューティング {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必要な知識 {#prerequisites}

JEE、JBoss®、WebSphere®、Webogic アプリケーションサーバー、Red Hat® Linux®、SUSE® Linux®、Microsoft® Windows、IBM® AIX®、Sun Solaris™ オペレーティングシステム、Oracle、IBM® DB2® または SQL Server データベースサーバー、web 環境での Adobe Experience Manager (AEM) Form に精通している必要があります。

## ユーザーレベル {#user-level}

詳細

JEE 上のAEM Forms クラスターは、JEE 上のAEM Forms がクラスターの障害に対して回復力を持つように設計されたトポロジです。また、このトポロジを使用して、単一のノードの機能を超えてシステム容量を拡張することもできます。クラスターは、複数のノードをデータを共有する単一の論理システムに組み合わせ、トランザクションを複数のノードにまたがって実行します。クラスターは、JEE 上の AEM Forms を拡張する最も一般的な方法です。どのようなワークロードの組み合わせも処理するサービスの組み合わせもサポートできます。JEE 上のAEM Forms クラスターは、すべてのタイプのデプロイメントに最適であるとは限りません。場合によっては、非クラスター型サーバーの負荷分散アーキテクチャが適切です。

このドキュメントでは、JEE 上のAEM Forms クラスターで発生する可能性のある、具体的な設定要件と潜在的な問題の領域について説明します。

## クラスターには何がありますか。 {#what-is-in-cluster}

JEE 上の AEM Forms クラスターノードは相互に通信し、情報を共有して、クラスター全体で単一の一貫性のある設定とアプリケーション状態を持つようにします。クラスター内での情報の共有は、異なるコンテキストで同時に使用される、複数の異なる方法で実行されます。基本的な情報共有方法を次の図に示します。

![アプリケーションサーバークラスター](assets/application-server-cluster.jpg)

### アプリケーションサーバークラスター {#application-server-cluster}

JEE 上の AEM Forms クラスターは、基になるアプリケーションサーバーのクラスタリング機能に依存しています。アプリケーションサーバークラスターは、クラスター設定全体を一括で管理し、Java™ Naming and Directory Interface（JNDI）などの下位レベルのクラスターサービスを提供し、ソフトウェアコンポーネントがクラスター内で互いを検索できるようにします。クラスターサービスの高度化と、アプリケーションサーバーが持つ基本的な技術依存関係は、アプリケーションサーバーによって異なります。WebSphere® と WebLogic にはクラスター用の高度な管理機能がありますが、JBoss® には非常に基本的なアプローチがあります。

### GemFire キャッシュ {#gemfire-cache}

GemFire キャッシュは、各クラスターノードに実装される分散キャッシュメカニズムです。ノードは互いを検索し合い、ノード間で一貫性を保つ単一の論理キャッシュを構築します。互いに検索するノードは、図 1 でクラウドとして表示される単一の概念的なキャッシュを維持するために結合されます。GDS やデータベースとは異なり、キャッシュは純粋に概念的なエンティティです。実際にキャッシュされたコンテンツは、メモリおよび各クラスターノード上の `LC_TEMP` ディレクトリに保存されます。

### データベース {#database}

JEE 上のAEM Forms データベース（JDBC データソース IDP_DS、EDC_DS などを介してアクセスされる）は、クラスターのすべてのノードで共有されます。JEE 上のAEM Forms の状態に関する最も永続的なデータ（処理中のトランザクション、進行中のトランザクションに関連付けられたユーザーデータ、システム設定の設定方法に関するデータなど）はこのデータベースにあります。

### グローバルドキュメントストレージ {#global-document-storage}

グローバルドキュメントストレージ（GDS）は、JEE 上の AEM Forms 内の Document Manager（IDPDocument クラス）で使用される、ファイルシステムベースのストレージ領域です。GDS には、クラスターのすべてのノードからアクセス可能で必要がある、有効期間の短いファイルと有効期間の長いファイルが格納されています。

### その他の項目 {#other-items}

これらの主な共有リソースに加えて、Quartz など、特定のクラスター動作を持つ他の項目もあります。Quartz は、JEE 上の AEM Forms で使用されるスケジューラーサブシステムで、データベーステーブルを使用して、スケジュールされた内容と実行されている予定アクティビティに関する知識を保持します。Quartz は、シングルノードのインストールとクラスターに対して異なる設定を行う必要があり、JEE 上の他の AEM Forms 設定からキューを受け取ります。

## 設定に関する一般的な問題 {#common-configuration}

JEE 上の AEM Forms クラスターの保守やトラブルシューティングに関して最も不満が生じる点の 1 つは、クラスターが正常であることを確認する場所が 1 つもないことです。クラスター内のすべてが正常であることを確認するには、何らかの調査と分析を行い、クラスター構成の問題に応じて、クラスター操作には、いくつかの失敗モードがあります。次の図は、誤って設定されたクラスターを示しています。この場合は、共有リソースの一部が不適切に共有されています。

![クラスターの設定が正しくない場合](assets/bad-configuration-cluster.png)

JEE 上の AEM Forms をクラスターで実行する予定がない場合でも、クラスターの動作の仕組みと、クラスター内で検索および検証すべき項目について理解しておく必要があります。これは、JEE 上の AEM Forms の一部でクラスターでの動作に関する情報を誤って取得し、予期しないクラスター動作を示す可能性があるためです。

上の図の共有設定の問題は何ですか。次のセクションでは、問題について説明します。

### （1）GemFire クラスター設定 {#gemfire-cluster-configuration}

Gemfire のキャッシュに問題が発生する場合があります。次の 2 つの典型的なシナリオがあります。

* お互いを見つけることができるはずのノードが、お互いを見つけることができません。

* クラスター化されたノードは相互に検出し、必要のない場合でもキャッシュを共有する可能性があります。

ノード群をクラスター化する場合は、ネットワーク上で各ノードが互いを検出し合う必要があります。デフォルトでは、マルチキャスト UDP メッセージを使用してこれを行います。各ノードは、その存在を通知するブロードキャストメッセージを送信し、メッセージを受信したすべてのノードは、検出した他のノードとの通信を開始します。この種の自動検出方法は一般的で、多くのタイプのソフトウェアやアプライアンスで採用されています。

自動検出に関するよくある問題の 1 つは、マルチキャストメッセージがネットワークでフィルタリングされる可能性がある点です。これは、ネットワークポリシーの一部であるか、ソフトウェアファイアウォールルールが原因であるか、ノード間に存在するネットワークを介してルーティングできないことが原因である可能性があります。複雑なネットワークで UDP 自動検出を実行するのは一般的に困難なため、実稼動環境では、別の検出方法として TCP ロケーターを使用するのが一般的です。TCP ロケーターについては、一般的な説明を参照してください。

**ロケーターと UDP のどちらを使用しているかを知る方法**

次の JVM プロパティで、GemFire キャッシュが他のノードの検索に使用するメソッドを制御しています。

マルチキャスト設定：

* `adobe.cache.multicast-port`：分散システムの他のメンバーとの通信に使用するマルチキャストポート。ゼロに設定すると、メンバーの検出と配信の両方についてマルチキャストが無効になります。

* `gemfire.mcast-address`（オプション）：Gemfire で使用されるデフォルトの IP アドレスを上書きします。

TCP ロケーター設定：

* `adobe.cache.cluster-locators`：TCP ロケーターの IP アドレスとホスト名、および、実行中のロケーターとの通信にシステムメンバーが使用する、全ロケーター用の TCP ロケーター ポート。

このリストには、現在使用中のすべてのロケーターを含める必要があり、クラスターシステムのすべてのメンバーに対して一貫性のある設定を行う必要があります。

TCP ロケーターリストが空の場合、ロケーターは使用されず、代わりにマルチキャストメソッドが使用されます。

**TCP ロケーターが実行中かどうかを確認する方法**

TCP ロケーターを使用している場合は、すべてのクラスターノードの次の JVM プロパティに TCP ロケーターが一覧表示されるはずです。

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

AEM Forms on JEE のクラスターノードでロケーターを実行する必要はありません。必要に応じて、クラスターとは別の他のシステムで実行することもできます。複数のシステムでロケーターを実行できます。また、ロケーターの 1 つで障害が発生するとクラスターの再起動時に問題を引き起こす可能性があるため、ロケーターを 2 つの場所で実行しておくのがベストプラクティスです。ロケーターを実行する各システムでは、次のコマンドを各マシン上で使用して、ロケーターが実行されていることを確認できる必要があります。

`netstat -an | grep 22345`

期待される応答は次のようになります。

`tcp 0 0 *.22345 *.* LISTEN`

もう 1 つの検証コマンドは次のとおりです。

`ps -ef | grep gemfire`

期待される応答は次のようになります。

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**GemFire がクラスター内にあると認識しているノードを確認する方法**

GemFire が生成するログ情報を使用すると、どのクラスターメンバーが GemFire キャッシュで見つかり、採用されたかを診断することができます。これを使用すると、正しいクラスターメンバーがすべて検出され、余分なクラスターノードや誤ったクラスターノードが検出されていないことを確認できます。GemFire のログファイルは、設定済みの JEE 上の AEM Forms の一時ディレクトリにあります。

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

`adobeZZ_` の後の数値文字列はサーバーノードに固有なので、一時ディレクトリの実際のコンテンツを検索する必要があります。`adobe` の後の 2 文字は、アプリケーションサーバーのタイプに応じて異なり、`wl`、`jb` または `ws` のいずれかです。

次のサンプルログは、2 ノードのクラスターが自身を検出した場合の動作を示しています。

1 つ目のノードで、AP-HP8：

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

もう 1 つのノードで、AP-HP7：

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**GemFire が余計なノードを見つけている場合**

企業ネットワークを共有する個別の各クラスターは、TCP ロケーターを使用する場合、別々の TCP ロケーターを使用する必要があります。または、マルチキャスト UDP 設定を使用する場合、別々の UDP ポート番号を使用する必要があります。JEE 上の AEM Forms では UDP 自動検出がデフォルトで設定されており、同じデフォルトポート 33456 が複数のクラスターで使用されているので、通信を試行すべきでないクラスターが予期せず通信を行う可能性があります。例えば、実稼動クラスターと QA クラスターは分離したままにする必要がありますが、UDP マルチキャストを介して相互に接続する場合があります。

GemFire が不適切にクラスタリングしているネットワーク内で重複ポートが発見される最も一般的な状況は、クラスターのブートストラップ中です。ブートストラッププロセスが明確な原因なしに失敗する場合があります。通常、次のようなエラーが発生します。

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

この場合、ブートストラップは GemFire と連携して必要なテーブルにアクセスします。また、JDBC 経由でアクセスされるテーブルと、GemFire によって返されるキャッシュされたテーブル情報との間には不一致があります。この情報は、基になるデータベースが異なる別のクラスターからのものです。

ポートの重複はブートストラップ中に明らかになることが多いですが、この状況が後で判明する可能性もあります。これは、あるクラスターのブートストラップが実行された際に、別のクラスターが停止して再起動されると発生する可能性があります。また、ネットワーク設定が変更されて、マルチキャスト目的で以前に分離されたクラスターが互いに認識可能になった場合にも発生する可能性があります。

このような状況を診断するには、GemFire ログを調べ、想定されるノードだけが検出されているかどうかを慎重に確認します。問題を修正するには、`adobe.cache.multicast-port` プロパティを、クラスターの一方または両方で異なる値に変更する必要があります。

### 2) GDS 共有 {#gds-sharing}

GDS 共有は、JEE 上の AEM Forms の外側で、O/S レベルで設定します。その際、すべてのクラスターノードで同じ共有ディレクトリ構造を使用できように調整する必要があります。Windows タイプのシステムでは、ファイル共有を 1 つのノードから別のノードに、または NAS アプライアンスなどのリモートファイルシステムからすべてのノードに設定することで、この処理を行います。UNIX® システムでは、GDS 共有は通常、NFS ファイル共有を介して、1 つのノードから別のノードに行うか、NAS アプライアンスから行われます。

このリモートファイル共有が利用できなくなった場合や、微妙な問題が発生した場合に、クラスターの障害モードが発生します。ネットワークの問題、セキュリティ設定、誤った設定が原因で、リモートマウントが失敗する場合があります。システムを再起動すると、数日または数週間前に行われた設定変更が反映される場合があり、これにより予期しない事態が生じる場合があります。

**NFS 共有がマウントに失敗した場合**

UNIX® では、NFS マウントがディレクトリ構造にマッピングされる方法により、マウントが失敗した場合でも、使用可能に見える GDS ディレクトリを利用できるようになります。次の点を考慮してください。

* NAS サーバー：NFS 共有フォルダー /u01/iapply/livecycle_gds
* ノード 1：次の場所にある共有フォルダー（DB サーバー上でホスト）へのマウントポイント：/u01/iapply/livecycle_gds
* ノード 2：次の場所にある共有フォルダー（DB サーバー上でホスト）へのマウントポイント：/u01/iapply/livecycle_gds

* LCES は GDS への次のパスを指定します：/u01/iapply/livecycle_gds

ノード 1 でのマウントが失敗した場合でも、ディレクトリ構造には空のマウントポイントへのパス `/u01/iapply/livecycle_gds` が含まれ、ノードが正しく実行されているように見えます。ただし、GDS のコンテンツは実際には他のノードと共有されていないので、クラスターは正常に動作しません。これは起こり得ることで、実際に発生しています。その結果、クラスターに不可解な障害が発生します。

ベストプラクティスは、Linux® マウントポイントが GDS のルートとして使用されるのではなく、その中の一部のディレクトリが GDS のルートとして使用されるように配置することです。

* NFS サーバーがある場合は、次のディレクトリが存在する可能性があります：/some/storage/lc_cluster_dev/LC_GDS
* また、クラスターノードには、次のマウントポイントがあります：/u01/iapply/shared
* nfs_server のマウント：/some/storage/lc_cluster_dev/u01/iapply/shared
* GDS を /u01/iapply/shared/LC_GDS に指定します

何らかの理由でマウントが成功しなかった場合、ベアマウントポイントには LC_GDS ディレクトリが含まれず、GDS がまったく見つからないので、クラスターは予想どおりに失敗します。

**すべてのノードが同じ GDS を参照し、権限を持っていることを確認する方法**

GDS のアクセスと共有を検証する最適な方法は、各ノードにインタラクティブユーザーとしてアクセスすることです。これを行うには、SSH または telnet 経由で UNIX® ノードにアクセスするか、リモートデスクトップ経由で Windows システムにアクセスします。各ノードで設定済みの GDS ディレクトリまたはファイルシステムに移動して、他のすべてのノードに表示されるすべてのノードからテストファイルを作成できるようになります。

JEE 上の AEM Forms が動作するユーザー ID に注意してください。Windows 自動インストールの場合は、ローカル管理者として機能します。UNIX® の場合は、起動スクリプトまたはアプリケーションサーバー設定で設定された、特定のサービスユーザーとして使用される場合があります。このユーザー ID を使用して、すべてのノードの GDS ファイルの作成と操作を均等に行うことが重要です。

UNIX® システムでは、NFS 設定のデフォルトで、ファイルやオブジェクトに対するルート所有権またはルートアクセス権を信用しないように設定されていることが多くあります。アプリケーションサーバーをルートユーザーとして実行している場合は、NFS サーバー、ファイルをマウントするノードのいずれかまたは両方で、オプションを指定する必要があります。これにより、あるノードが作成し、別のノードがアクセスするファイルの、双方向のアクセスと制御が可能になります。

### (3) データベース共有 {#database-sharing}

クラスターが正しく機能するためには、すべてのクラスターメンバーが同じデータベースを共有する必要があります。これを間違える範囲は、大まかに以下のようになります。

* IDP_DS、EDC_DS、AdobeDefaultSA_DS またはその他の必要なデータソースを別々のクラスターノード上で誤って設定し、ノードが異なるデータベースを指すようにします。
* データベースを共有すべきでない場合に、データベースを共有するように複数の個別ノードを誤って設定します。

アプリケーションサーバーによっては、JDBC 接続がクラスタースコープで定義されるのが自然な場合があるため、ノードごとに異なる定義を行うことはできません。ただし、JBoss® では、IDP_DS などのデータソースがノード 1 上では 1 つのデータベースを指し、ノード 2 上では別の何かを指すように設定しても問題ありません。

逆の問題が、より一般的です。つまり、JEE 上の複数のスタンドアロン（またはクラスター）の AEM Forms ノードが、意図されていないときに誤って同じスキーマを指している場合です。これが最も多く発生するのは、DBA が JEE 上の AEM Forms データベースの接続情報を DEV と QA の両方のセットアップチームに対して無意識に提供する場合です。どちらのチームも、DEV インスタンスと QA インスタンスに別々のデータベースが必要であることを認識していません。

## アプリケーションサーバークラスター {#application-server-cluster-1}

JEE 上の AEM Forms クラスターを正常に稼働させるには、アプリケーションサーバーをクラスターとして正しく設定し動作させる必要があります。WebSphere® および WebLogic では、これは明確に文書化されたプロセスです。JBoss® では、クラスター設定は少し実践的で、ノードがクラスターとして機能し、実際に相互に検索して通信するように設定されていることを確認するのは難しい場合があります。JBoss® は内部的に JGroups に依存しており、UDP マルチキャストを使用してピアノードを検索し、調整します。GemFire では、ノードが必要な場合に互いを見つけられないことや、不必要な場合に互いを見つけるなどの既知の問題があります。

リファレンス：

* [JBoss® クラスターを介した高可用性エンタープライズサービス](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Oracle WebLogic Server - クラスターの使用](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### JBoss® が正しくクラスター化されていることを確認する方法 {#check-jboss-clustering}

JBoss® の起動時に、クラスターメンバーが検出されると、クラスターに参加しているノードに関する情報（INFO）レベルのメッセージが、ログファイル／コンソールに記録されます。

実行時に -g コマンドラインオプションを使用してクラスター名を指定した場合は、次のようなメッセージが表示されます。

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartz スケジューラー {#quartz-scheduler}

ほとんど場合、クラスターで JEE 上の AEM Forms の内部 Quartz スケジューラーを使用すると、JEE 上の AEM Forms の一般的なグローバルクラスター設定に自動的に従います。ただし、Gemfire での自動検出にマルチキャストでなく TCP ロケーターを使用している場合、Quartz の自動クラスター設定が失敗するバグ #2794033 があります。この場合、非クラスター化モードで Quartz が正しく実行されません。この結果、Quartz テーブルでデッドロックとデータの破損が発生します。この不具合はバージョン 9.0 よりも 8.2.x の方が顕著です。Quartz はあまり使用されなくなったものの、まだ存在しています。

この問題に対して、8.2.1.2 QF2.143 および 9.0.0.2 QF2.44 で修正を行いました。

次の回避策もあり、2 つのプロパティをいずれも設定します。

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

一方の設定では「cluster」と「locators」の間にピリオドを使用し、もう一方の設定ではハイフンを使用します。ソフトウェアパッチを適用するよりも簡単に実装でき、リスクも低くなりますが、紛らわしい名前の追加設定を人為的に作成する必要があります。

### Quartz が単一ノードとクラスターのどちらで稼働しているかを確認する方法 {#check-quartz}

Quartz の設定内容を確認するには、起動時に JEE 上の AEM Forms の スケジューラーサービスが生成するメッセージを確認する必要があります。これらのメッセージは重大度が INFO で生成されるため、メッセージを取得するには、場合によってはログレベルを調整して再起動する必要があります。JEE 上の AEM Forms の起動シーケンス内で、Quartz の初期化は次の行で始まります。

INFO  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
ログでこの開始行を見つけることが重要です。一部のアプリケーションサーバーでも Quartz が使用されることがあり、その Quartz インスタンスが、JEE 上の AEM Forms のスケジューラーサービスで使用されているインスタンスと混同されないようにする必要があるからです。これはスケジューラーサービスが起動中であることを示しており、これに続く行で、クラスターモードで正しく開始しているかどうかを示しています。このシーケンスには複数のメッセージが表示されます。Quartz の設定を示しているのは、最後の「」メッセージです。

ここでは、Quartz インスタンスの名前は、`IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975` です。スケジューラーの Quartz インスタンスの名前は、常に文字列 `IDPSchedulerService_$_` で始まります。この末尾に追加される文字列が、Quartz がクラスターモードで実行されているかどうかを示しています。ノードのホスト名と長い数字の文字列から生成される、長い一意の ID（ここでは `ap-hp8.ottperflab.adobe.com1312883903975`）は、クラスターで動作していることを示します。1 つのノードとして動作している場合、この ID は 2 桁の数字「20」になります。

INFO `[org.quartz.core.QuartzScheduler]` Scheduler `IDPSchedulerService_$_20` started.（スケジューラーが起動しました）
各ノードのスケジューラーは独立してクラスターモードで実行するかどうかを決定するので、このチェックはすべてのクラスターノードで個別に行う必要があります。

### Quartz を間違ったモードで実行している場合に発生する問題 {#quartz-running-in-wrong-mode}

Quartz が単一ノードで実行するように設定されていながら、クラスターで実行され、Quartz データベーステーブルを他のノードと共有している場合、この結果として、JEE 上の AEM Forms のスケジューラーサービスの動作が不安定になります。そして、多くの場合、データベースのデッドロックが伴います。次のスタックトレースは、このような状況で見られる典型的なものです。

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Could not remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### クラスター内のシステムクロックを同期する方法 {#synchronize-system-clocks-cluster}

クラスターがスムーズに動作するには、すべてのクラスターノードのクロックが正確に同期している必要があります。この同期は手動では適切に行うことはできず、定期的に実行される何らかの形式の時刻同期サービスで行う必要があります。すべてのノードのクロックは、互いに 1 秒以内である必要があります。ベストプラクティスでは、クラスターノードだけでなく、ロードバランサー、データベースサーバー、GDS NAS サーバー、その他のコンポーネントもすべて同期することが求められます。

Windows では、ドメインコントローラーに対して時刻同期を行う傾向があります。UNIX® システムでは、NTP を使用して別のタイムソースに同期する場合があります。可能であれば、すべてのシステム（JEE 上の AEM Forms ノードと、他のシステムコンポーネントの両方）を同じソースに同期することをお勧めします。

ごく一時的なテスト環境であっても、ノードのクロックを手動で設定するだけでは不十分です。手動でクロックを設定すると、十分な精度で同期できず、1 日経っただけでも、2 つのノードのクロックはどうしても相対的にずれてしまいます。高い信頼性でクラスターを運用するには、能動的に時刻を同期するメカニズムが不可欠です。

### ロードバランサー {#load-balancer}

ユーザーにインタラクティブなサービスを提供するクラスターでは、HTTP ロードバランサーでクラスター全体に HTTP リクエストを分散させることが一般的に求められます。JEE 上の AEM Forms のクラスターでロードバランサーを正常に使用するには、次の設定が必要です。

* スティッキーセッション

* URL 書き換えルール

* ノードのヘルスチェック

### ロードバランサーのヘルスチェック機能で行うこと {#load-balancer-health-check}

一部のロードバランサーは、負荷分散するノードに対して定期的にヘルスチェックを行うように設定できます。通常、ロードバランサーがアクセスを試みるアプリケーション機能の URL に対して行われます。URL の読み込みに成功した場合、ノードは正常であると見なされ、ロードバランスするセットに保持されます。URL の読み込みに失敗した場合、ノードは異常であると見なされ、セットから外されます。通常、ヘルスチェック URL で接続する先は、JEE 上の AEM Forms の AdminUI ログインページです。これは、クラスターメンバーに対する理想的なヘルスチェックではないので、短時間のみ有効なプロセスを実装し、REST API URL をヘルスチェック機能として使用する方が効果的です。

## 一時ファイルパスと類似のクラスター設定 {#temporary-file-path-cluster-settings}

JEE 上の AEM Forms 内の特定のファイルパス設定は、クラスター全体で確立され、各ノードで有効な設定は同じですが、ローカルファイルを参照するために各ノードで個別に解釈されます。考慮すべき重要な点は、フォントパス設定と一時ディレクトリ設定です。AdminUI コア設定画面に移動します（ホーム／設定／コアシステム／コア設定）。

次の設定を確認する必要があります。

1. 一時ディレクトリの場所
1. Adobe Server フォントディレクトリの場所
1. カスタマーフォントディレクトリの場所
1. システムフォントディレクトリの場所
1. データサービス設定ファイルの場所

クラスターには、これらの構成設定ごとに 1 つのパス設定のみが用意されています。例えば、一時ディレクトリの場所は `/home/project/QA2/LC_TEMP` のようになります。クラスターでは、各ノードが実際にこの特定のパスにアクセスできる必要があります。あるノードに予期した一時ファイルパスが指定され、別のノードに指定されていない場合、指定されていないノードは正しく機能しません。

これらのファイルやパスは、ノード間で共有されたり、別々に配置されたり、リモートファイルシステム上に配置されたりする場合がありますが、ローカルノードのディスクストレージ上にローカルコピーすることがベストプラクティスです。

特に、一時ディレクトリのパスは、ノード間で共有しないでください。一時ディレクトリが共有されていないことを確認するには、GDS の検証に関して説明した手順と同様の手順を使用します。それぞれのノードに移動し、パス設定で示されるパスに一時ファイルを作成し、他のノードがファイルを共有しないことを確認します。一時ディレクトリパスは、可能な限り各ノード上のローカルディスクストレージを参照し、チェックする必要があります。

各パス設定に対して、JEE 上の AEM Forms が実行される有効な使用 ID を使用して、パスが実際に存在し、クラスター内の各ノードからアクセスできることを確認します。フォントディレクトリの内容は読み取り可能である必要があります。一時ディレクトリは、読み取り、書き込み、制御を許可する必要があります。
