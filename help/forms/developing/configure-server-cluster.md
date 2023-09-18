---
title: JEE 上のAEM Formsサーバークラスターの設定とトラブルシューティングの方法
description: JEE 上のAdobe Experience Manager(AEM)Formsサーバークラスターの設定とトラブルシューティングの方法について説明します。
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '3959'
ht-degree: 45%

---

# JEE サーバークラスター上の AEM Forms の設定とトラブルシューティング {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必要な知識 {#prerequisites}

JEE 上のAdobe Experience Manager(AEM)Forms、JBoss®、WebSphere®、WebLogic アプリケーションサーバー、Red Hat® Linux®、SUSE® Linux®、Microsoft® Windows、IBM® AIX®、または Sun Solaris™オペレーティングシステム、Oracle、IBMDB2、または OR に精通してい®る SQL Server データベースサーバーと Web 環境

## ユーザーレベル {#user-level}

詳細

JEE 上のAEM Formsクラスターは、JEE 上のAEM Formsがクラスターの障害に対して回復力を持つように設計されたトポロジです。 また、トポロジは、単一のノードの機能を超えてシステム容量を拡張することもできます。 クラスターは、複数のノードをデータを共有する単一の論理システムに組み合わせ、トランザクションを複数のノードにまたがって実行します。クラスターは、JEE 上の AEM Forms を拡張する最も一般的な方法です。どのようなワークロードの組み合わせも処理するサービスの組み合わせもサポートできます。JEE 上のAEM Formsクラスターは、すべてのタイプのデプロイメントに最適なものではなく、クラスター化されていないサーバー負荷分散アーキテクチャが適切な場合があります。

このドキュメントでは、JEE 上のAEM Formsクラスターで発生する可能性のある、具体的な設定要件と問題の領域について説明します。

## クラスターには何がありますか。 {#what-is-in-cluster}

JEE 上の AEM Forms クラスターノードは相互に通信し、情報を共有して、クラスター全体で単一の一貫性のある設定とアプリケーション状態を持つようにします。クラスター内での情報の共有は、異なるコンテキストで同時に使用される、複数の異なる方法で実行されます。基本的な情報共有方法を次の図に示します。

![アプリケーションサーバークラスター](assets/application-server-cluster.jpg)

### アプリケーションサーバークラスター {#application-server-cluster}

JEE 上の AEM Forms クラスターは、基になるアプリケーションサーバーのクラスタリング機能に依存しています。アプリケーションサーバークラスターは、クラスター構成全体を管理し、Java™ Naming and Directory Interface(JNDI) などの低レベルのクラスターサービスを提供し、ソフトウェアコンポーネントがクラスター内で互いを見つけ出せるようにします。 クラスターサービスの高度化と、アプリケーションサーバーが持つ基盤となる技術的依存関係は、アプリケーションサーバーによって異なります。 WebSphere®および WebLogic は、クラスター用の高度な管理機能を備えていますが、JBoss®は基本的なアプローチを備えています。

### GemFire キャッシュ {#gemfire-cache}

GemFire キャッシュは、各クラスターノードに実装される分散キャッシュメカニズムです。ノードは互いを検索し合い、ノード間で一貫性を保つ単一の論理キャッシュを構築します。互いに見つけ合うノードは、図 1 に示すクラウドとして表示される単一の概念的キャッシュを維持するために結合します。 GDS やデータベースとは異なり、キャッシュは純粋に概念的なエンティティです。実際にキャッシュされたコンテンツは、メモリおよび各クラスターノード上の `LC_TEMP` ディレクトリに保存されます。

### データベース {#database}

JEE 上のAEM Formsデータベース（JDBC データソース IDP_DS、EDC_DS などを介してアクセス）は、クラスターのすべてのノードで共有されます。 JEE 上のAEM Formsの状態に関する最も永続的なデータ（処理中のトランザクション、進行中のトランザクションに関連付けられたユーザーデータ、システム設定の設定方法に関するデータなど）がこのデータベースに格納されます。

### グローバルドキュメントストレージ {#global-document-storage}

グローバルドキュメントストレージ (GDS) は、JEE 上のAEM Forms内の Document Manager（IDPDocument クラス）で使用される、ファイルシステムベースのストレージ領域です。 GDS には、クラスターのすべてのノードからアクセスできる必要がある、短時間のみ有効なファイルと長時間有効なファイルが格納されています。

### その他の項目 {#other-items}

これらの主な共有リソースに加えて、Quartz など、特定のクラスター動作を持つ他の項目もあります。Quartz は、JEE 上の AEM Forms で使用されるスケジューラーサブシステムで、データベーステーブルを使用して、スケジュールされた内容と実行されている予定アクティビティに関する知識を保持します。Quartz は、シングルノードのインストールとクラスターに対して異なる設定を行う必要があり、JEE 上の他の AEM Forms 設定からキューを受け取ります。

## 設定に関する一般的な問題 {#common-configuration}

JEE クラスター上のAEM Formsの保守やトラブルシューティングに関して最も不満が生じる点の 1 つは、クラスターが正常であることを確かに確認する場所が 1 つもないことです。 クラスター内のすべてが正常であることを確認するには、何らかの調査と分析を行い、クラスター構成の問題に応じて、クラスター操作には、いくつかの失敗モードがあります。次の図は、誤って設定されたクラスターを示しています。この場合は、共有リソースの一部が不適切に共有されています。

![クラスターの設定が正しくない場合](assets/bad-configuration-cluster.png)

クラスターで JEE 上のAEM Formsを実行する予定がない場合でも、クラスターの動作の仕組みと、クラスター内で検索および検証できることの種類を理解します。 これは、JEE 上のAEM Formsの一部で、クラスター内の動作に関する手掛かりを正しく得ず、予期しないクラスター動作を引き受ける可能性があるためです。

上の図の共有設定の問題は何ですか。次のセクションでは、問題について説明します。

### （1）GemFire クラスター設定 {#gemfire-cluster-configuration}

Gemfire のキャッシュに問題が発生する場合があります。次の 2 つの典型的なシナリオがあります。

* お互いを見つけることができるはずのノードが、お互いを見つけることができません。

* クラスター化されたノードは、互いに見つけ合い、キャッシュを共有する必要がある場合があります。

クラスター化するノードがある場合は、ネットワーク上で互いを見つけ合う必要があります。 デフォルトでは、マルチキャスト UDP メッセージを使用してこれを行います。 各ノードは、自分が存在することを広告するブロードキャストメッセージを送信し、メッセージを受信したすべてのノードは、検出した他のノードとの通信を開始します。この種の自動検出方法は一般的で、多くの種類のソフトウェアやアプライアンスがこれを行います。

自動検出に関するよくある問題の 1 つは、マルチキャストメッセージがネットワークでフィルタリングされる可能性がある点です。 これは、ネットワークポリシーの一部であるか、ソフトウェアファイアウォール規則が原因であるか、ノード間に存在するネットワークを経由できないためです。 複雑なネットワークで UDP 自動検出を実行するのは一般的に困難なため、実稼動環境では、別の検出方法として TCP ロケーターを使用するのが一般的です。TCP ロケーターについては、一般的な説明を参照してください。

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

AEM Forms on JEE のクラスターノードでロケーターを実行する必要はありません。必要に応じて、クラスターとは別の他のシステムで実行することもできます。複数のシステムがロケーターを実行できます。 また、ロケーターを 2 つの場所で実行することをお勧めします。ロケーターの 1 つの障害がクラスターの再起動で問題が発生する可能性はありません。 ロケーターを実行する各システムでは、次のコマンドを各マシン上で使用して、ロケーターが実行されていることを確認できる必要があります。

`netstat -an | grep 22345`

期待される応答は次のようになります。

`tcp 0 0 *.22345 *.* LISTEN`

もう 1 つの検証コマンドは次のとおりです。

`ps -ef | grep gemfire`

期待される応答は次のようになります。

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**GemFire がクラスター内にあると認識しているノードを確認する方法**

GemFire が生成するログ情報を使用すると、どのクラスターメンバーが GemFire キャッシュで見つかり、採用されたかを診断することができます。これを使用して、正しいクラスターメンバーがすべて見つかり、余分なまたは間違ったクラスターノードの検出がおこなわれていないことを確認できます。 GemFire のログファイルは、設定済みの JEE 上のAEM Forms一時ディレクトリにあります。

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

`adobeZZ_` の後の数値文字列はサーバーノードに固有なので、一時ディレクトリの実際のコンテンツを検索する必要があります。の後の 2 文字 `adobe` アプリケーションのサーバータイプに応じて、次のいずれかを実行します。 `wl`, `jb`または `ws`.

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

企業ネットワークを共有する個別の各クラスターは、TCP ロケーターを使用する場合、別々の TCP ロケーターを使用する必要があります。または、マルチキャスト UDP 設定を使用する場合、別々の UDP ポート番号を使用する必要があります。UDP 自動検出は JEE 上のAEM Formsのデフォルト設定で、同じデフォルトポート33456が複数のクラスターで使用されているので、通信を試みるべきでないクラスターが予期せず使用される可能性があります。 たとえば、実稼動クラスタと QA クラスタは別々の状態に保つ必要がありますが、UDP マルチキャストを介して相互に接続する場合があります。

GemFire が不適切にクラスタリングしているネットワーク内の重複ポートを検出する可能性がある最も一般的な状況は、クラスタのBootstrap中です。 明確な原因がなく、Bootstrap・プロセスが失敗することが分かる場合があります。 通常、次のようなエラーが発生します。

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

この場合、ブートストラッパーは GemFire と連携して必要なテーブルにアクセスしています。また、JDBC を通じてアクセスするテーブルと、GemFire から返されるキャッシュされたテーブル情報との間に矛盾があります。GemFire は、基になるデータベースが異なる別のクラスターから取得されます。

Bootstrap中に重複したポートが明らかになることが多いですが、この状況が後で表示される可能性があります。 これは、他のクラスタのBootstrapが発生したときに、停止した後にクラスタが再起動された場合に発生する可能性があります。 または、ネットワーク構成が変更されて、マルチキャスト目的で以前に分離されたクラスタが互いに認識されるようになった場合にも使用できます。

これらの状況を診断するには、GemFire ログを調べ、期待されるノードのみが見つかるかどうかを慎重に検討します。 問題を修正するには、 `adobe.cache.multicast-port` プロパティを 1 つまたは両方のクラスターで異なる値に設定する。

### 2) GDS 共有 {#gds-sharing}

GDS 共有は、O/S レベルで JEE 上のAEM Formsの外部で設定されます。O/S レベルでは、同じ共有ディレクトリ構造をすべてのクラスターノードで使用できるように配置する必要があります。 Windows タイプのシステムでは、ファイル共有を 1 つのノードから別のノードに、または NAS アプライアンスなどのリモート・ファイル・システムからすべてのノードに設定することで、これを実現します。 UNIX®システムでは、GDS 共有は通常、NFS ファイル共有を通じて、1 つのノードから別のノードに、または NAS アプライアンスから行われます。

このリモートファイル共有が利用できなくなった場合や、微妙な問題が発生した場合に、クラスターの障害モードが発生します。ネットワークの問題、セキュリティ設定、または構成の誤りが原因で、リモートマウントが失敗する場合があります。 システムを再起動すると、数日または数週間前に行われた設定変更が反映される場合があり、これにより予期しない事態が生じる場合があります。

**NFS 共有がマウントに失敗した場合**

UNIX®では、NFS マウントをディレクトリ構造にマッピングする方法により、マウントに失敗した場合でも、明らかに使用可能な GDS ディレクトリを使用できます。 次の点を考慮してください。

* NAS サーバー：NFS 共有フォルダー /u01/iapply/livecycle_gds
* ノード 1：次の場所にある共有フォルダー（DB サーバー上でホスト）へのマウントポイント：/u01/iapply/livecycle_gds
* ノード 2：次の場所にある共有フォルダー（DB サーバー上でホスト）へのマウントポイント：/u01/iapply/livecycle_gds

* LCES は GDS への次のパスを指定します：/u01/iapply/livecycle_gds

ノード 1 でのマウントに失敗した場合、ディレクトリ構造にはパスが含まれます `/u01/iapply/livecycle_gds` を空のマウントポイントに設定すると、ノードが正しく実行されているように見えます。 ただし、GDS コンテンツは実際には他のノードと共有されていないので、クラスターは正しく動作しません。 これは発生する可能性があり、実際に発生します。その結果、クラスターに不可解な障害が発生します。

ベストプラクティスは、Linux®マウントポイントが GDS のルートとして使用されるのではなく、その中の一部のディレクトリが GDS のルートとして使用されるように配置することです。

* NFS サーバーがある場合は、次のディレクトリが存在する可能性があります：/some/storage/lc_cluster_dev/LC_GDS
* また、クラスターノードには、次のマウントポイントがあります：/u01/iapply/shared
* nfs_server のマウント：/some/storage/lc_cluster_dev/u01/iapply/shared
* GDS を /u01/iapply/shared/LC_GDS に指定します

これで、何らかの理由でマウントが成功しなかった場合、ベアマウントポイントに LC_GDS ディレクトリが含まれず、GDS が見つからないため、クラスターが予測可能に失敗します。

**すべてのノードが同じ GDS を参照し、権限を持っていることを確認する方法**

GDS のアクセスと共有の検証は、各ノードにインタラクティブユーザーとしてアクセスすることで最善をなします。 これは、SSH または UNIX®ノードに Telnet を介して行うか、Windows システムにリモートデスクトップを介して行うかのどちらかで行うことができます。 各ノードで設定済みの GDS ディレクトリまたはファイルシステムに移動して、他のすべてのノードに表示されるすべてのノードからテストファイルを作成できるようになります。

JEE 上の AEM Forms が動作するユーザー ID に注意してください。Windows 自動インストールの場合は、ローカル管理者として機能します。UNIX®の場合は、起動スクリプトまたはアプリケーションサーバー設定で設定された特定のサービスユーザーとして使用できます。 このユーザー ID を使用して、すべてのノードの GDS ファイルの作成と操作を均等に行うことが重要です。

UNIX®システムでは、NFS 構成は、多くの場合、ファイルやオブジェクトに対するルート所有権やルートアクセス権を不信にするようにデフォルト設定されます。 アプリケーション・サーバーをルート・ユーザーとして実行している場合は、NFS サーバー、ファイルをマウントするノード、またはその両方にオプションを指定する必要があります。 これにより、あるノードで作成され、別のノードがアクセスしたファイルに対して、二国間のアクセスと制御が可能になります。

### (3) データベース共有 {#database-sharing}

クラスターが正しく動作するには、同じデータベースをすべてのクラスターメンバーで共有する必要があります。 これを間違える範囲は、大まかに以下のようになります。

* IDP_DS、EDC_DS、AdobeDefaultSA_DS またはその他の必要なデータソースを別々のクラスターノード上で誤って設定し、ノードが異なるデータベースを指すようにします。
* 誤って複数のノードを別々に設定して、データベースを共有する必要がない場合に、データベースを共有します。

アプリケーションサーバーによっては、JDBC 接続がクラスタースコープで定義されるのが自然な場合があるため、ノードごとに異なる定義を行うことはできません。ただし、JBoss®では、IDP_DS などのデータソースがノード 1 上の 1 つのデータベースを指し、ノード 2 上の他のデータベースを指すように、何かを設定することは完全に可能です。

逆の問題はより一般的です。 つまり、意図していない場合に、JEE 上の複数のスタンドアロン（またはクラスター）のAEM Formsノードが誤って同じスキーマを指してしまう状況です。 これは、ほとんどの場合、DBA が無意識に JEE 上のAEM Formsデータベースの接続情報を DEV と QA の両方のセットアップチームに提供する場合に発生します。 どちらのチームも、DEV インスタンスと QA インスタンスに別々のデータベースが必要であることに気付いていません。

## アプリケーションサーバークラスター {#application-server-cluster-1}

JEE 上のAEM Formsクラスターを正常に稼働させるには、アプリケーションサーバーを設定し、クラスターとして適切に動作させる必要があります。 WebSphere®および WebLogic では、これは明確に文書化された簡単なプロセスです。 JBoss®では、クラスターの設定は少し手を加えるもので、ノードがクラスターとして機能し、実際に相互に検索して通信するように設定するのは、課題となります。 JBoss®は JGroups に内部的に依存し、UDP マルチキャストを使用してピアノードを検索し、調整します。 GemFire で言及されている問題の一部は、必要なときにノードが互いに見つからない、または必要でないときに互いに見つけ合うなど、発生する可能性があります。

リファレンス：

* [JBoss®クラスタを介した高可用性エンタープライズサービス](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [OracleWebLogic Server-Using クラスター](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### JBoss®が正しくクラスタリングされていることを確認する方法を教えてください。 {#check-jboss-clustering}

JBoss®の起動時に、クラスターメンバーが検出されると、クラスターに参加するノードに関する INFO レベルのメッセージがログファイル/コンソールに記録されます。

実行時に —g コマンドラインオプションを使用してクラスタ名を指定した場合は、次のようなメッセージが表示されます。

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### クォーツスケジューラー {#quartz-scheduler}

一般に、JEE 上のAEM Formsでは、クラスター内で Quartz スケジューラーを使用する場合、JEE 上のAEM Formsのグローバルクラスター設定に自動的に従うことを意図しています。 ただし、Gemfire での自動検出にマルチキャストでなく TCP ロケーターを使用している場合、Quartz の自動クラスター設定が失敗するバグ #2794033 があります。この場合、Quartz は非クラスターモードで誤って実行されます。 これにより、Quartz テーブルでデッドロックとデータの破損が発生します。 この不具合はバージョン 9.0 よりも 8.2.x の方が顕著です。Quartz はあまり使用されなくなったものの、まだ存在しています。

この問題に対して、8.2.1.2 QF2.143 および 9.0.0.2 QF2.44 で修正を行いました。

次の回避策もあり、2 つのプロパティをいずれも設定します。

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

1 つの設定では「cluster」と「locators」の間のピリオドを使用し、もう 1 つはハイフンを使用します。 ソフトウェアパッチを適用するよりも簡単に実装でき、リスクも低くなりますが、紛らわしい名前の追加設定を人為的に作成する必要があります。

### Quartz が単一ノードとクラスターのどちらで稼働しているかを確認する方法 {#check-quartz}

Quartz の設定内容を確認するには、起動時に JEE 上の AEM Forms の スケジューラーサービスが生成するメッセージを確認する必要があります。これらのメッセージは重大度が INFO で生成されるため、メッセージを取得するには、場合によってはログレベルを調整して再起動する必要があります。JEE 上の AEM Forms の起動シーケンス内で、Quartz の初期化は次の行で始まります。

情報  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad ログでこの最初の行を見つけることが重要です。 原因は、一部のアプリケーションサーバーでも Quartz が使用されるので、Quartz インスタンスを、JEE 上のAEM Formsスケジューラーサービスで使用されているインスタンスと混同しないでください。 スケジューラーサービスが起動中であることを示し、それに続く行は、クラスター化モードで正しく起動しているかどうかを示します。 このシーケンスには複数のメッセージが表示されます。Quartz の設定を示しているのは、最後の「started」メッセージです。

Quartz インスタンスの名前は次のように表示されます。 `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. スケジューラーの Quartz インスタンスの名前は、常に文字列で始まります `IDPSchedulerService_$_`. この末尾に追加される文字列は、Quartz がクラスターモードで実行されているかどうかを示します。 ノードのホスト名と長い数字の文字列から生成される、長い一意の ID（ここでは `ap-hp8.ottperflab.adobe.com1312883903975`）は、クラスターで動作していることを示します。1 つのノードとして動作する場合、識別子は 2 桁の数値 (「20」) になります。

INFO `[org.quartz.core.QuartzScheduler]` Scheduler `IDPSchedulerService_$_20` started.（スケジューラーが起動しました）
各ノードのスケジューラは、クラスタモードで動作するかどうかを別々に決定するので、このチェックはすべてのクラスタノードで個別に行う必要があります。

### Quartz を間違ったモードで実行している場合に発生する問題 {#quartz-running-in-wrong-mode}

Quartz が単一のノードとして実行するように設定されているが、クラスター内で実行され、Quartz データベーステーブルを他のノードと共有している場合、JEE 上のAEM Forms Scheduler サービスの動作が信頼できなくなります。 そして、多くの場合、データベースのデッドロックが伴います。 次のスタックトレースは、このような状況で見られる典型的なものです。

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
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

クラスタがスムーズに動作するには、すべてのクラスタノードのクロックを密接に同期させる必要があります。 これは手作業では十分に行えず、定期的に実行される何らかの形式の時間同期サービスで行う必要があります。 すべてのノードのクロックは、互いに 1 秒以内である必要があります。ベストプラクティスでは、クラスターノードだけでなく、ロードバランサー、データベースサーバー、GDS NAS サーバー、およびその他のコンポーネントもすべて同期することが求められます。

Windows では、ドメインコントローラーに対して時刻同期を行う傾向があります。UNIX®システムは、NTP を使用して別のタイム・ソースに同期する場合があります。 可能であれば、JEE 上のAEM Formsノードと他のシステムコンポーネントの両方のシステムが、同じソースに同期する場合に最適です。

最も一時的なテスト環境でも、ノードにクロックを手動で設定するのに十分ではありません。 手動でクロックを設定しても、正確な同期は行われず、1 日の間でも、2 つのノード上のクロックは必然的に相対的にドリフトします。 高い信頼性でクラスターを運用するには、能動的に時刻を同期するメカニズムが不可欠です。

### ロードバランサー {#load-balancer}

ユーザーインタラクティブサービスを提供するクラスターの一般的な要件は、クラスター全体で HTTP 要求を分散する HTTP ロードバランサーです。 JEE 上の AEM Forms のクラスターでロードバランサーを正常に使用するには、次の設定が必要です。

* スティッキーセッション

* URL 書き換えルール

* ノードのヘルスチェック

### ロードバランサーのヘルスチェック機能で行うこと {#load-balancer-health-check}

一部のロードバランサーは、負荷分散するノードに対して定期的にヘルスチェックを行うように設定できます。通常、これはロードバランサーがアクセスを試みるアプリケーション関数への URL です。 URL の読み込みに成功した場合、ノードは正常であると見なされ、ロードバランスするセットに保持されます。URL の読み込みに失敗した場合、ノードは異常であると見なされ、セットから外されます。一般的に、ヘルスチェック URL は JEE 上のAEM Formsの AdminUI ログインページに接続されます。 これは、クラスターメンバーに対する理想的なヘルスチェックではないので、短時間のみ有効なプロセスを実装し、REST API URL をヘルスチェック機能として使用する方が効果的です。

## 一時ファイルパスと類似のクラスター設定 {#temporary-file-path-cluster-settings}

JEE 上の AEM Forms 内の特定のファイルパス設定は、クラスター全体で確立され、各ノードで有効な設定は同じですが、ローカルファイルを参照するために各ノードで個別に解釈されます。考慮すべき重要な点は、フォントパス設定と一時ディレクトリ設定です。AdminUI コア設定画面に移動します（ホーム／設定／コアシステム／コア設定）。

次の設定を確認する必要があります。

1. 一時ディレクトリの場所
1. Adobe Server フォントディレクトリの場所
1. カスタマーフォントディレクトリの場所
1. システムフォントディレクトリの場所
1. データサービス設定ファイルの場所

クラスターには、これらの構成設定ごとに 1 つのパス設定のみが用意されています。例えば、Temp ディレクトリの場所は次のようになります。 `/home/project/QA2/LC_TEMP`. クラスターでは、各ノードが実際にこの特定のパスにアクセスできる必要があります。あるノードに予期された一時ファイルパスが指定され、別のノードに指定されていない場合、指定されていないノードは正しく機能しません。

これらのファイルとパスは、ノード間で共有することも、別々に配置することも、リモート・ファイル・システム上で共有することもできますが、ローカル・ノードのディスク・ストレージ上のローカル・コピーにすることをお勧めします。

特に、一時ディレクトリのパスは、ノード間で共有しないでください。GDS を使用して一時ディレクトリが共有されていないことを検証するために説明した手順と同様の手順です。 各ノードに移動し、パス設定で示されるパスに一時ファイルを作成し、他のノードがファイルを共有しないことを確認します。 一時ディレクトリパスは、可能な限り各ノード上のローカルディスクストレージを参照し、チェックする必要があります。

各パス設定に対して、JEE 上の AEM Forms が実行される有効な使用 ID を使用して、パスが実際に存在し、クラスター内の各ノードからアクセスできることを確認します。フォントディレクトリの内容は読み取り可能である必要があります。一時ディレクトリは、読み取り、書き込み、制御を許可する必要があります。
