---
title: JEE上のAEM Formsサーバークラスターの設定方法とトラブルシューティング方法を教えてください。
description: JEE上のAEM Formsサーバークラスターの設定方法とトラブルシューティング方法について説明します
source-git-commit: 8502e0227819372db4120d3995fba51c7401d944
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# JEE上のAEM Formsサーバークラスターの設定とトラブルシューティング {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必要な知識 {#prerequisites}

JEE上のAEM Forms、JBoss、WebSphere、WebLogicアプリケーションサーバー、Red Hat Linux、SUSE Linux、Microsoft Windows、IBM AIX、Sun Solarisオペレーティングシステム、Oracle、IBM DB2、SQL Serverデータベースサーバー、Web環境に精通している。

## ユーザーレベル {#user-level}

詳細

JEE上のAEM Formsクラスターは、JEE上のAEM Formsがクラスターノードの障害に対して回復力を持ち、1つのノードの機能を超えてシステム容量を拡大できるように設計されたトポロジーです。 クラスターは、複数のノードをデータを共有する単一の論理システムに結合し、トランザクションを複数のノードにまたがって実行できるようにします。 クラスターは、JEE上のAEM Formsを拡張する最も一般的な方法です。ワークロードの組み合わせを処理する任意のサービスの組み合わせをサポートできます。 JEE上のAEM Formsクラスターは、必ずしもすべてのタイプのデプロイメントに最適なものではなく、特に、クラスター化されていないサーバー負荷分散アーキテクチャが多くの場合に適している可能性があります。

このドキュメントの目的は、JEE上のAEM Formsクラスターで発生する可能性のある、具体的な設定要件と潜在的な問題領域について説明することです。

## クラスターの内容 {#what-is-in-cluster}

JEE上のAEM Formsクラスターノードは相互に通信し、情報を共有して、クラスター全体で単一の一貫した設定とアプリケーション状態を持つようにします。 クラスター内での情報の共有は、異なるコンテキストで同時に使用される複数の異なる方法で行われます。 基本的な情報共有方法を次の図に示します。

![アプリケーションサーバークラスター](assets/application-server-cluster.jpg)

### アプリケーションサーバークラスター {#application-server-cluster}

JEE上のAEM Formsクラスターは、基になるアプリケーションサーバーのクラスタリング機能に依存します。 アプリケーションサーバークラスターは、クラスター構成全体を管理し、ソフトウェアコンポーネントがクラスター内で互いを見つけ合えるようにする、Java Naming and Directory Interface(JNDI)などの低レベルのクラスターサービスを提供します。 クラスターサービスの高度化と、アプリケーションサーバーが持つ基盤となる技術的依存関係は、アプリケーションサーバーに依存します。 WebSphereとWebLogicは、クラスターの高度な管理機能を備えていますが、JBossは非常に基本的なアプローチを備えています。

### GemFireキャッシュ {#gemfire-cache}

GemFireキャッシュは、各クラスターノードに実装される分散キャッシュメカニズムです。 ノードは互いを見つけ合い、ノード間で一貫性を保つ単一の論理キャッシュを構築します。 互いに見つけ合うノードは、図1でクラウドとして表示される単一の概念的キャッシュを維持するために結合されます。 GDSやデータベースとは異なり、キャッシュは純粋に概念的なエンティティです。 実際にキャッシュされたコンテンツは、メモリおよび各クラスターノードの`LC_TEMP`ディレクトリに格納されます。

### データベース {#database}

JEE上のAEM Formsデータベース（JDBCデータソースIDP_DS、EDC_DSなどを介してアクセス）は、クラスターのすべてのノードで共有されます。 進行中のトランザクション、進行中のトランザクションに関連付けられたユーザーデータ、システム設定の設定方法に関するデータなど、JEE上のAEM Formsの状態に関する永続的なデータのほとんどは、このデータベースに格納されます。

### グローバルドキュメントストレージ {#global-document-storage}

グローバルドキュメントストレージ(GDS)は、JEE上のAEM Forms内のDocument Manager（IDPDocumentクラス）で使用されるファイルシステムベースのストレージ領域です。 GDSには、クラスターのすべてのノードからアクセスできる必要がある、短時間のみ有効なファイルと長期間有効なファイルが格納されます。

### その他の項目 {#other-items}

これらの主な共有リソースに加えて、Quartzなど、特定のクラスター動作を持つ他の項目もあります。 Quartzは、JEE上のAEM Formsで使用されるスケジューラーサブシステムで、データベーステーブルを使用して、スケジュールされた内容と実行されているスケジュール済みアクティビティの知識を保持します。 Quartzは、シングルノードのインストールとクラスターに対して異なる設定を行う必要があり、JEE上の他のAEM Forms設定からキューを受け取ります。

## 設定に関する一般的な問題 {#common-configuration}

JEE上のAEM Formsクラスターの保守やトラブルシューティングに関して最も不満が生じる点の1つは、クラスターが正常であることを確かに確認する場所が1つもないことです。 クラスター内のすべてが正常であることを確認するには、何らかの調査と分析を行い、クラスター構成の問題に応じて、クラスター操作にいくつかのモードの失敗があります。 次の図は、共有リソースの一部が不適切に共有される、正しく設定されていないクラスターを示しています。

![クラスターの構成が正しくありません](assets/bad-configuration-cluster.png)

注意すべき興味深く重要な点は、クラスターでJEE上のAEM Formsを実行しない場合でも、クラスター化の仕組みや、クラスター内で検索および検証する内容について理解しておく必要があることです。 これは、JEE上のAEM Formsの一部で、クラスター内の動作に関する手掛かりを誤って受け取り、予期しないクラスター動作を引き受ける可能性があるためです。

上の図の共有設定の問題は何ですか？ 次の節では、問題について説明します。

### (1) GemFireクラスター設定 {#gemfire-cluster-configuration}

Gemfireのキャッシュに問題が発生する場合があります。 次の2つのシナリオが一般的です。

* 互いに見つけ合うべきノードは、それを行うことができません。

* クラスター化されていないノードは、互いに見つけ合い、キャッシュを共有すべきではありません。

クラスター化するノードがある場合は、ネットワーク上で互いを見つけ合うことが不可欠です。 デフォルトでは、マルチキャストUDPメッセージを使用してこれを行います。 各ノードは、その存在を広告するブロードキャストメッセージを送信し、そのようなメッセージを受け取ったノードが、そのメッセージが見つけた他のノードと通信し始めます。 この種の自動検出方法は非常に一般的で、多くの種類のソフトウェアとアプライアンスがこれを行います。

自動検出のよくある問題の1つは、マルチキャストメッセージがネットワークポリシーの一部またはソフトウェアファイアウォール規則によってネットワークでフィルタリングされる場合、またはノード間に存在するネットワークを経由できない場合です。 複雑なネットワークでUDP自動検出を機能させるのは一般的に困難なので、実稼動環境のデプロイメントでは、次のような別の検出方法を使用するのが一般的です。TCPロケーター。 TCPロケーターの一般的な説明は、の参照を参照してください。

**ロケーターとUDPのどちらを使用しているかは、どうすればわかりますか。**

次のJVMプロパティは、GemFireキャッシュが他のノードを検索する際に使用するメソッドを制御します。

マルチキャスト設定：

* `adobe.cache.multicast-port`:分散システムの他のメンバーとの通信に使用されるマルチキャストポート。この値がゼロに設定されている場合、メンバーの検出と配布の両方に対してマルチキャストが無効になります。

* `gemfire.mcast-address` （オプション）:Gemfireで使用されるデフォルトのIPアドレスを上書きします。

TCPロケーターの設定：

* `adobe.cache.cluster-locators`:実行中のロケーターと通信するためにシステムメンバーが使用するすべてのロケーターのTCPロケーターのIPアドレス/ホスト名。

リストには、現在使用中のすべてのロケーターが含まれ、クラスターシステムのすべてのメンバーに対して一貫して設定する必要があります。

TCPロケーターリストが空の場合、ロケーターは使用されず、代わりにマルチキャスト方式が使用されます。

**TCPロケーターが実行中かどうかを確認するにはどうすればよいですか。**

まず、TCPロケーターが使用中の場合は、すべてのクラスターノードで、次のJVMプロパティにTCPロケーターを一覧表示する必要があります。

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

JEE上のAEM Formsクラスターノードでロケーターを実行する必要はありません。必要に応じて、クラスターとは別の他のシステムで実行できます。 複数のシステムでロケーターを実行できます。通常、ロケーターを2つの場所で実行することをお勧めします。ロケーターの1つの障害でクラスターの再起動に問題が生じる可能性はありません。 ロケーターを実行する各システムで、これらのマシンで次のコマンドを使用して実行していることを確認できる必要があります。

`netstat -an | grep 22345`

期待される応答は次のようになります。

`tcp 0 0 *.22345 *.* LISTEN`

もう1つの検証コマンドは次のとおりです。

`ps -ef | grep gemfire`

期待される応答は次のようになります。

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**GemFireがクラスター内で考えるノードを確認する方法を教えてください。**

GemFireは、GemFireキャッシュで見つかり、採用されたクラスターメンバーを診断するために使用できるログ情報を生成します。 これを使用して、正しいクラスターメンバーがすべて見つかり、余分なまたは誤ったクラスターノードの検出がおこなわれていないことを確認できます。 GemFireのログファイルは、設定済みのJEE上のAEM Forms一時ディレクトリにあります。

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

`adobeZZ_`の後の数値文字列はサーバノードに固有なので、一時ディレクトリの実際の内容を検索する必要があります。 `adobe`の後の2文字は、アプリケーションのサーバーの種類に応じて異なります。`wl`、`jb`、または`ws`。

次のサンプルログは、2ノードのクラスターが自分自身を見つけた場合の動作を示しています。

最初のノードで、AP-HP8:

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

もう1つのノードで、AP-HP7:

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**GemFireが、それがすべきでないノードを見つける場合はどうなりますか？**

企業ネットワークを共有する個々のクラスターは、TCPロケーターが使用されている場合は個別のTCPロケーターのセットを、マルチキャストUDP設定が使用されている場合は別のUDPポート番号を使用する必要があります。 UDP自動検出はJEE上のAEM Formsのデフォルト設定で、同じデフォルトポート33456が複数のクラスターで使用されている場合があるので、通信を試みないクラスターは予期せず別の状態に保たれ、UDPマルチキャストを介して相互に接続できます。

GemFireが不適切にクラスタリングされているネットワーク内の重複ポートを検出する可能性がある最も一般的な状況は、クラスターのブートストラップ中です。 明確な原因がなくてもブートストラッププロセスが失敗することが分かるかもしれません。 通常、次のようなエラーが発生します。

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

この場合、ブートストラッパーはGemFireと連携して必要なテーブルにアクセスし、JDBCを通じてアクセスするテーブルと、基になるデータベースが異なる別のクラスターから返されるGemFireのキャッシュされたテーブル情報との間に矛盾があります。

ブートストラップ中に重複ポートが明らかになることが多いが、他のクラスタのブートストラップが発生した後にクラスタが再起動した場合、またはネットワーク構成が変更され、以前に分離されたクラスタが相互に見えるようになる場合は、この状況が後で現れる。

これらの状況を診断するには、GemFireログを確認し、期待されるノードのみが見つかるかどうかを慎重に検討することをお勧めします。 問題を修正するには、

`adobe.cache.multicast-port`

プロパティを1つまたは両方のクラスターで異なる値に設定します。

### 2) GDSの共有 {#gds-sharing}

GDS共有は、JEE上のAEM Formsの外部（O/Sレベル）で設定されます。このレベルでは、同じ共有ディレクトリ構造を、すべてのクラスターノードで使用できるように配置する必要があります。 Windowsタイプのシステムでは、通常、ファイル共有を1つのノードから別のノードに、またはNASアプライアンスなどのリモート・ファイル・システムからすべてのノードに設定することで、これを実現します。 UNIXシステムでは、GDSの共有は通常、NFSファイル共有を介して、ノード間、またはNASアプライアンスから行われます。

クラスターの障害モードとして、このリモートファイル共有が利用できなくなった場合や、微妙な問題が発生した場合が考えられます。 ネットワークの問題、セキュリティ設定、または構成の誤りが原因で、リモートマウントが失敗する場合があります。 システムを再起動すると、何日も前から何週間も前に行われた構成変更が反映され、これによって予期しない事態が生じる可能性があります。

**NFS共有がマウントに失敗した場合、どうなりますか。**

UNIXでは、NFSマウントがディレクトリ構造にマッピングされる方法により、マウントに失敗した場合でも、明らかに使用可能なGDSディレクトリを使用できます。 次の点を考慮してください。

* NASサーバ：NFS共有フォルダー/u01/iapply/livecycle_gds
* ノード1:次の場所にある共有フォルダー（DBサーバー上でホストされる）へのマウントポイント。/u01/iapply/livecycle_gds
* ノード2:次の場所にある共有フォルダー（DBサーバー上でホストされる）へのマウントポイント。/u01/iapply/livecycle_gds

* LCESはGDSへのパスを指定します。/u01/iapply/livecycle_gds

ノード1でのマウントが失敗した場合でも、ディレクトリ構造には空のマウントポイントへのパス/u01/iapply/livecycle_gdsが含まれ、ノードは正しく実行されているように見えます。 ただし、GDSコンテンツは実際に他のノードと共有されていないので、クラスターは正しく動作しません。 これは起こりうるし、起こる結果、クラスターは神秘的な方法で失敗します。

ベストプラクティスは、LinuxマウントポイントをGDSのルートとして使用せず、その中の一部のディレクトリをGDSのルートとして使用するように配置することです。

* NFSサーバーがある場合は、次のディレクトリが存在する可能性があります。/some/storage/lc_cluster_dev/LC_GDS
* また、クラスターノードにマウントポイントがあります。/u01/iapply/shared
* nfsサーバーのマウント(_S):/some/storage/lc_cluster_dev/u01/iapply/shared
* GDSを/u01/iapply/shared/LC_GDSに設定します。

何らかの理由でマウントが成功しない場合、ベアマウントポイントにLC_GDSディレクトリが含まれず、クラスタはGDSを全く見つけられないので、予測可能に失敗します。

**すべてのノードが同じGDSを参照し、権限を持っていることを確認するには、どうすればよいですか？**

GDSアクセスと共有の検証は、SSHまたはUNIXノードへのTelnet経由、またはリモートデスクトップ経由でWindowsシステムに対して、各ノードに対してインタラクティブユーザーとしてアクセスすることで最も効果的です。 各ノードで設定済みのGDSディレクトリまたはファイルシステムに移動し、他のすべてのノードに表示されるすべてのノードからテストファイルを作成できるはずです。

JEE上のAEM Formsが動作するユーザーIDに注意してください。 Windowsの自動インストールでは、ローカル管理者として機能します。 UNIXの場合は、起動スクリプトまたはアプリケーションサーバー設定で設定された特定のサービスユーザーとして使用できます。 このユーザーIDは、すべてのノードでGDSファイルの作成と操作を同じように行うことが重要です。

UNIXシステムでは、NFS構成は、多くの場合、ルート所有権やファイルやオブジェクトへのルートアクセス権を不信にするようにデフォルト設定されます。 rootユーザーとしてアプリケーションサーバーを実行する場合は、NFSサーバー、ファイルをマウントするノード、またはその両方で、あるノードが作成し、別のノードがアクセスするファイルの双務アクセスと制御を許可するオプションを指定する必要があります。

### (3)データベース共有 {#database-sharing}

クラスターが正しく動作するには、同じデータベースをすべてのクラスターメンバーで共有する必要があります。 これを誤る範囲は、大まかに次のとおりです。

* 別々のクラスターノード上で誤ってIDP_DS、EDC_DS、AdobeDefaultSA_DSまたはその他の必要なデータソースを設定し、ノードが別々のデータベースを指すように誤って設定してしまう。
* 誤って複数のノードを設定して、データベースを共有する必要がない場合に

アプリケーションサーバーによっては、JDBC接続がクラスタースコープで定義され、異なるノードで異なる定義が可能にならないのが自然な場合があります。 ただし、IDP_DSなどのデータソースがノード1上の1つのデータベースを指し、ノード2上の他のデータベースを指すように、JBOSS上では設定が完全に可能です。

逆の問題は、実際にはより一般的です。つまり、JEE上の複数のスタンドアロン（またはクラスター）のAEM Formsノードが、意図していないときに誤って同じスキーマを指す場合です。 これは、多くの場合、DBAがJEE上のAEM Formsデータベースの接続情報をDEVとQAの両方の設定チームに知らずに1つ提供し、DEVとQAのインスタンスに別々のデータベースが必要なことを認識しない場合に発生します。

## アプリケーションサーバークラスター {#application-server-cluster-1}

JEE上のAEM Formsクラスターを正常に実行するには、アプリケーションサーバーをクラスターとして適切に設定および動作させる必要があります。 WebSphereおよびWeblogicでは、これは明確に文書化されたプロセスです。 Jbossでは、クラスター設定は少し多くの実践が必要です。ノードがクラスターとして機能し、実際に互いを見つけて通信するように設定されていることを確認するのは、難しいことです。 JBossはUDPマルチキャストを使用してピアノードを検索し、調整するJGroupに内部的に依存しています。GemFireで言及されている問題の一部は、必要な場合にノードが互いに見つからない場合や、必要でない場合に互いに見つかる場合などに発生します。

参照:

* [JBossクラスターを介した高可用性エンタープライズサービス](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [OracleWebLogic Server — クラスターの使用](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### JBossが正しくクラスタリングされていることを確認する方法を教えてください。 {#check-jboss-clustering}

JBossの起動時に、クラスターメンバーが検出されると、クラスターに参加するノードに関するINFOレベルのメッセージがログファイル/コンソールに記録されます。

実行時に —gコマンドラインオプションを使用してクラスタ名が指定された場合は、次のようなメッセージが表示されます。

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartzスケジューラ {#quartz-scheduler}

ほとんどの場合、JEE上のAEM Formsでは、クラスター内で内部Quartzスケジューラーを使用して、一般に、JEE上のAEM Formsのグローバルクラスター設定に自動的に従います。 ただし、Quartzの自動検出ではなくGemfireにTCPロケーターを使用している場合、Quartzの自動クラスター設定が失敗するバグ#2794033があります。 この場合、非クラスターモードではQuartzが正しく実行されません。 これにより、Quartzテーブルにデッドロックとデータ破損が発生します。 Quartzはあまり使用されていないが、まだ存在するので、バージョン8.2.xは9.0よりも悪い副作用です。

この問題に関しては、次の修正が行われました。8.2.1.2 QF2.143および9.0.0.2 QF2.44。

また、次の両方のプロパティを設定するための回避策もあります。

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

一方の設定では「cluster」と「locators」の間のピリオドを使用し、もう一方の設定ではハイフンを使用します。 これは、実装が簡単で、ソフトウェアパッチを適用するよりもリスクが低くなりますが、名前が間違っている、わかりにくい追加の設定を人為的に作成する必要があります。

### Quartzが単一のノードまたはクラスターとして実行されていることを確認する方法を教えてください。 {#check-quartz}

Quartzの設定方法を確認するには、起動時にJEE上のAEM Formsスケジューラーサービスによって生成されたメッセージを確認する必要があります。 これらのメッセージはINFOの重大度で生成され、メッセージを取得するには、ログレベルを調整し、再起動する必要が生じる場合があります。 JEE上のAEM Formsの起動シーケンス内で、Quartzの初期化は次の行で開始されます。

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
一部のアプリケーションサーバーでもQuartzを使用するので、ログの最初の行を見つけることが重要です。Quartzのインスタンスを、JEE上のAEM Formsスケジューラーサービスで使用されているインスタンスと混同しないでください。 これは、スケジューラーサービスが起動中で、それに続く行が、適切にクラスターモードで起動しているかどうかを示します。 このシーケンスには複数のメッセージが表示されます。Quartzの設定方法を示す最後の「開始済み」メッセージです。

Quartzインスタンスの名前は次のとおりです。`IDPSchedulerService_$_ap-hp8.ottperflab.corp.adobe.com1312883903975`. スケジューラーのQuartzインスタンスの名前は、常に文字列`IDPSchedulerService_$_`で始まります。 この末尾に追加される文字列は、Quartzがクラスターモードで実行されているかどうかを示します。 ノードのホスト名と長い数字の文字列（ここでは`ap-hp8.ottperflab.corp.adobe.com1312883903975`）から生成される長い一意の識別子は、クラスター内で動作していることを示します。 1つのノードとして動作する場合、識別子は2桁の数値(「20」)になります。

INFO `[org.quartz.core.QuartzScheduler]`スケジューラ`IDPSchedulerService_$_20`が開始されました。
各ノードのスケジューラーは、クラスターモードで動作するかどうかを独立して決定するので、このチェックは、すべてのクラスターノードで個別に行う必要があります。

### Quartzが誤ったモードで実行されている場合、どのような問題が発生しますか？ {#quartz-running-in-wrong-mode}

Quartzが単一のノードとして実行するように設定されているが、実際にクラスターで実行され、Quartzデータベーステーブルを他のノードと共有している場合、JEE上のAEM Formsスケジューラーサービスの動作が信頼できず、通常はデータベースのデッドロックが伴います。 これは、この状況で見られるかもしれない典型的なスタックトレースです。

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

### クラスター内のシステムクロックを同期する方法を教えてください。 {#ynchronize-system-clocks-cluster}

クラスターがスムーズに動作するには、すべてのクラスターノード上のクロックを密接に同期させる必要があります。 これは手作業では適切に行えず、非常に定期的に実行される何らかの形の時間同期サービスで行う必要があります。 すべてのノードのクロックは、互いに1秒以内である必要があります。 ベストプラクティスでは、クラスターノードだけでなく、ロードバランサー、データベースサーバー、GDS NASサーバー、その他のコンポーネントもすべて同期する必要があります。

Windowsの時刻同期は、ドメインコントローラーに対しておこなわれる傾向があります。 UNIXシステムは、NTPを使用して別のタイムソースに同期する場合があります。 可能であれば、すべてのシステム(JEE上のAEM Formsノードと他のシステムコンポーネントの両方)を同じソースに同期することをお勧めします。

ほとんどの一時的なテスト環境でも、ノードにクロックを手動で設定するだけでは、完全に不十分です。 手動でクロックを設定しても十分な同期が得られず、1日でも2つのノード上のクロックが互いに相対的にドリフトします。 信頼性の高いクラスター動作には、アクティブタイム同期メカニズムが不可欠です。

### ロードバランサー {#load-balancer}

ユーザーインタラクティブサービスを提供するクラスターの一般的な要件は、HTTP要求をクラスター全体に分散させるHTTPロードバランサーです。 JEE上のAEM Formsクラスターでロードバランサーを正常に使用するには、次の設定が必要です。

* セッション定着

* URL書き換えルール

* ノードヘルスチェック

### ロードバランサーのヘルスチェック機能を使用するには、どうすればよいですか？ {#load-balancer-health-check}

ロードバランサーによっては、負荷分散を行うノードに対して定期的なヘルスチェックを実行するように設定できる場合があります。 通常、これはロードバランサーがアクセスを試みるアプリケーション関数へのURLです。 読み込みが成功した場合、ノードは正常であると見なされ、ロードバランシングセットに保持されます。 URLの読み込みに失敗した場合、ノードが誤っていると見なされ、セットから削除されます。 一般的に、ヘルスチェックURLは、JEE上のAEM FormsのAdminUIログインページに接続するだけです。 これは、クラスターメンバーに対する理想的なヘルスチェックではないので、短時間のみ有効なプロセスを実装し、REST API URLをヘルスチェック機能として使用する方が良いでしょう。

## 一時ファイルパスと類似のクラスター設定 {#temporary-file-path-cluster-settings}

JEE上のAEM Forms内の特定のファイルパス設定は、クラスター全体で確立され、各ノードで同じ有効な設定を持ちますが、ローカルファイルを参照するために各ノードで個別に解釈されます。 考慮すべき重要な点は、フォントパス設定と一時ディレクトリ設定です。 AdminUIコア設定画面に移動します（ホーム/設定/コアシステム/コア設定）。

次の設定をオンにする必要があります。

1. 一時ディレクトリの場所
1. Adobe Server フォントディレクトリの場所
1. カスタマーフォントディレクトリの場所
1. システムフォントディレクトリの場所
1. データサービス設定ファイルの場所

クラスターには、これらの構成設定ごとに1つのパス設定のみがあります。 例えば、Tempディレクトリの場所は`/home/project/QA2/LC_TEMP`です。 クラスターでは、各ノードが実際にこの特定のパスにアクセスできる必要があります。 あるノードに予期された一時ファイルパスがあり、別のノードに予期された一時ファイルパスがない場合、が正しく機能しません。

これらのファイルとパスは、ノード間で共有することも、別々に配置することも、リモート・ファイル・システム上で共有することもできますが、通常は、ローカル・ノードのディスク・ストレージ上のローカル・コピーにすることをお勧めします。

特に、一時ディレクトリのパスは、ノード間で共有しないでください。 GDSを検証するために説明した手順と同様の手順を使用して、一時ディレクトリが共有されていないことを検証する必要があります。各ノードに移動し、パス設定で示されるパスに一時ファイルを作成し、他のノードがファイルを共有しないことを確認します。 一時ディレクトリパスは、可能な限り各ノード上のローカルディスクストレージを参照し、チェックする必要があります。

各パス設定に対して、JEE上のAEM Formsが実行される有効な使用IDを使用して、パスが実際に存在し、クラスター内の各ノードからアクセスできることを確認します。 フォントディレクトリの内容は読み取り可能である必要があります。 一時ディレクトリでは、読み取り、書き込み、制御を許可する必要があります。
















