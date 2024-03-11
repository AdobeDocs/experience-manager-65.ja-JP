---
title: 設定の基本概念
description: 独自の要件に合わせた Adobe Experience Manager の設定方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '2093'
ht-degree: 99%

---

# 設定の基本概念{#basic-configuration-concepts}

Adobe Experience Manager（AEM）は、すべてのパラメーターがデフォルトで設定されてインストールされるので、「すぐに」で実行できます。ただし、独自の要件に合わせて AEM を設定することもできます。

AEM では様々な設定を行えます。

* 一部は[すべてのプロジェクトのインストールに対して共通に設定されており](#primary-configuration-considerations)、プロジェクトに適用できるかどうかの確認が必要なものがあります。
* 機能やシステムのパフォーマンスおよび安定性に関しては、[さらなる設定](#further-configuration-considerations)を行うのが一般的ですが、必須ではありません。
* その他は、AEM の一定のオプション機能用にのみ必要です（これらについては該当する機能と合わせて説明します）。

具体的な設定に応じて、これらの変更には次のいずれかを使用できます。

* **Adobe CQ web コンソール**

  これは、OSGi バンドルおよびサービスを設定するための標準的な場所です。

  詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)の詳細と推奨プラクティスを参照してください。

* **リポジトリ**

  リポジトリ内で OSGi 設定のサブセットが利用可能です。そのため、リポジトリのコンテンツをコピーまたはレプリケートすることにより、同一の設定を再作成できます。実行モードに応じて、独自の設定をリポジトリに追加することもできます。

  詳しくは、[リポジトリでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)、特に[リポジトリへの新しい設定の追加](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)を参照してください。

* **ファイルシステム**

  ファイルシステム内にはいくつかの設定ファイルが存在します。

* **AEM WCM**

  AEM WCM 内で様々な設定をおこなえます。多くは、レプリケーションエージェントなどの[ツール](/help/sites-administering/tools-consoles.md)コンソールを使用します。

>[!NOTE]
>
>Adobe Experience Manager で作業をする際には、いくつかの方法で OSGi サービスの設定を管理できます（コンソールまたはリポジトリノード）。
>
>詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

>[!NOTE]
>
>AEM の設定は簡単です。ただし、変更の内容によってはアプリケーションに大きな影響を与える可能性があります。このため、AEM の設定を開始する前に、必要な経験と知識を持っていることを確認し、必要であると分かっている変更のみを加えてください。OSGi コンソールを使用して行った変更は、実行中のシステムに&#x200B;**すぐに**&#x200B;適用されます（再起動は不要です）。

## プライマリ設定に関する考慮事項 {#primary-configuration-considerations}

このリストでは、すべての新規プロジェクトで一般的に設定される主な領域について詳しく説明します。すべてが必要とは限りませんが、プロジェクトに適した内容を確認するには、リストを読み取り、確認する必要があります。

このリストには、各設定の概要と、詳細を提供するページへのリンクが表示されます。

### セキュリティチェックリスト {#security-checklist}

設定に関するいくつかの主要な問題について詳しくは、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。必ずこの内容を読み、インストールに必要なアクションを実行してください。

### デフォルト UI の設定 - タッチ操作向け UI またはクラシック UI {#configuring-the-default-ui-touch-optimized-or-classic}

AEM では次の 2つの UI を使用できます。

* タッチ操作向け UI
* クラシック UI

必要な UI を、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md)を使用して設定できます。

>[!NOTE]
>
>UI の選択について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### IPv4 と IPv6 {#ipv-and-ipv}

AEM のすべての要素（例：リポジトリ、Dispatcher）は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定が必要ないので、操作はシームレスです。必要に応じて、ネットワークの種類に適した形式で IP アドレスを指定するだけで済みます。

つまり、IP アドレスを指定する必要がある場合、次の中から（必要に応じて）選択できます。

* IPv6 アドレス

  例：`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 アドレス

  例：`https://123.1.1.4:4502`

* サーバー名

  例：`https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストールで解釈されます

  例：`http://localhost:4502`

### バージョンのパージ {#version-purging}

標準インストールでは、AEM はコンテンツを更新後、ページを有効にする時にページまたはノードのバージョンを作成します。サイドキックの「**バージョン管理**」タブを使用すると、リクエスト時に追加のバージョンを作成することもできます。これらのバージョンはすべてリポジトリーに保存され、必要に応じて復元できます。

これらのバージョンはパージされることがなく、時間の経過と共にリポジトリーのサイズが大きくなるので、管理が必要です。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。特に、新しいバージョンが作成されたときに古いバージョンをパージするように AEM を設定する方法については、[バージョンマネージャー](/help/sites-deploying/version-purging.md#version-manager)を参照してください。

### ログ {#logging}

AEM では、以下の設定が可能です。

* 中央のログサービスのグローバルパラメーター
* リクエストデータのログ（リクエスト情報用の特殊なログ設定）
* 個々のサービスに特有の設定（個々のログファイルおよびログメッセージの書式など）

詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

### 実行モード {#run-modes}

実行モードを使用すると、特定の目的に合わせて AEM インスタンスを調整できます。例えば、オーサーまたはパブリッシュ、テスト、開発、イントラネットなどです。

これは、各実行モードに対して設定パラメーターのコレクションを定義することで行われます。すべての実行モードに対して基本的な設定パラメーターのセットが適用され、特定の環境の目的に合わせて追加のセットを調整できます。これらは必要に応じて適用されます。

設定はすべて 1 つのリポジトリに格納され、**実行モード**&#x200B;を設定することによってアクティベートされます。

詳しくは、[実行モード](/help/sites-deploying/configure-runmodes.md)を参照してください。

### シングルサインオン {#single-sign-on}

シングルサインオン（SSO）では、ユーザーが認証の資格情報（ユーザー名、パスワードなど）を一度入力すると、複数のシステムにアクセスできるようになります。別個のシステム（信頼された認証と呼ばれます）が認証を実行し、Experience Manager にユーザーの資格情報を提供します。Experience Manager は、ユーザーのアクセス権限を確認および強制します（つまり、ユーザーがアクセスできるリソースを決定します）。

詳しくは、[シングルサインオン](/help/sites-deploying/single-sign-on.md)を参照してください。

### リソースマッピング {#resource-mapping}

リソースマッピングは、AEM のリダイレクト、バニティ URL および仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへの要求がすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

詳しくは、[リソースマッピング](/help/sites-deploying/resource-mapping.md)を参照してください。

### レプリケーション、リバースレプリケーションおよびレプリケーションエージェント {#replication-reverse-replication-and-replication-agents}

レプリケーションエージェントは AEM の中核であり、次の目的で使用されます。

* オーサー環境からパブリッシュ環境へコンテンツを[公開（アクティベート）](/help/sites-authoring/publishing-pages.md)
* ディスパッチャーキャッシュからコンテンツを明示的にフラッシュ
* ユーザー入力（フォーム入力など）をパブリッシュ環境からオーサー環境（オーサー環境の制御下）に戻す。

詳しくは、[レプリケーション](/help/sites-deploying/replication.md)を参照してください。

### OSGi 設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEM の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)で、プロジェクトの実装に関連する様々なバンドルのリスト（バンドルでリストされています）を参照してください。リストされているすべての設定を調整する必要はありませんが、AEM の動作を理解するのに役立つ設定もいくつか記載されています。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### LDAP の設定 {#configuring-ldap}

LDAP 認証は、Active Directory などの（中央の）LDAP ディレクトリに格納されているユーザーを認証するために必要です。これにより、ユーザーアカウントの管理に必要な労力が軽減されます。

LDAP 認証はリポジトリレベルでおこなわれるので、リポジトリによって直接処理されます。詳しくは、[AEM での LDAP の設定](/help/sites-administering/ldap-config.md)を参照してください。

AEM 内のユーザー管理（アクセス権の割り当てを含む）について詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

### Dispatcher の設定 {#configuring-the-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュ、ロードバランシングまたはその両方を行うツールです。エンタープライズクラスの web サーバーで使用できます。

詳しくは、[Dispatcher ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。特に、設定の詳細については、[Dispatcher の設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja)を参照してください。

### AEM LiveCycle Connector の設定 {#configuring-aem-livecycle-connector}

AEM ドキュメントサービスおよび AEM ドキュメントセキュリティのリリースにより、LiveCycle ドキュメントサービスを呼び出して XFA フォームをレンダリングしたり、ドキュメントを PDF に変換したり、ドキュメントをポリシー保護したりできるようになりました。詳しくは、[AEM LiveCycle コネクタ](https://helpx.adobe.com/jp/livecycle/help/aem/aem-livecycle-connector.html)を参照してください。

### ジョブのオフロードとトポロジの管理 {#job-offloading-and-topology-administration}

[オフロードによって、トポロジ内の Experience Manager インスタンス間で処理タスクが配布されます。](/help/sites-deploying/offloading.md)オフロードを使用すると、特定の Experience Manager インスタンスを使用して特定のタイプの処理を実行できます。特殊化した処理により、使用可能なサーバーリソースの使用を最大限に活用できます。

トポロジは、オフロードに参加している疎結合Experience Managerクラスタです。 クラスターは、1 つ以上の Experience Manager サーバーインスタンスで構成されます（1 つのインスタンスがクラスターと見なされます）。

トポロジのメンバーシップを表示または変更する方法について詳しくは、「[トポロジの管理](/help/sites-deploying/offloading.md#administering-topologies)」セクションを参照してください。

### ようこそコンソールの設定 {#configuring-the-welcome-console}

クラシック UI のようこそコンソールには、AEM 内の様々なコンソールおよび機能へのリンクのリストが表示されます。

表示されるリンクを設定することもできます。詳しくは、[ようこそコンソールの設定](/help/sites-developing/customizing-the-welcome-console.md)を参照してください。

### パフォーマンスの設定 {#configuring-for-performance}

[パフォーマンス](/help/sites-deploying/configuring-performance.md)はプロジェクトの鍵です。パフォーマンスを最適化するために AEM（および基盤となるリポジトリ）の特定の要素を設定できます。

詳しくは、[パフォーマンスの設定](/help/sites-deploying/configuring-performance.md#configuring-for-performance)を参照してください。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共有データストア {#shared-data-store}

リポジトリのデータストアは、サイズの大きいバイナリのストレージを適切なリポジトリから別の領域にオフロードするために使用します。これによって、リポジトリツリー内の同じバイナリ（画像など）の複数のインスタンスは 1 回だけ格納されます。

この「1 回の格納で複数回参照する」機能を拡張し、それぞれのデータストアが共有ファイルシステムの同じ場所を参照するように設定すると、単一のリポジトリツリーだけでなく、完全に別々の複数のリポジトリにも対応できます。

このようなデータストアは、同じクラスター内の異なるノード間、同じインストール内の異なるパブリッシュインスタンスやオーサーインスタンス間、または異なるインストール内の完全に別々のインスタンス間で共有できます。

詳しくは、[データストアとノードストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

## 設定に関するその他の考慮事項 {#further-configuration-considerations}

### HTTP over SSL の有効化 {#enabling-http-over-ssl}

HTTP over SSL を有効にして、サーバーへの接続のセキュリティを強化できます。

詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### AEM ポータルとポートレット {#aem-portals-and-portlets}

ポータルとは、パーソナライズ機能、シングルサインオン、様々なソースからのコンテンツ統合を提供し、情報システムのプレゼンテーションレイヤーをホストする web アプリケーションです。ポートレットコンポーネントによって、ページにポートレットを埋め込むことができます。CQ5 WCM が提供するコンテンツにアクセスするには、ポータルサーバーに CQ5 Portal Director ポートレットを取り付けます。これを行うには、ポータルページにポートレットをインストール、設定、追加します。

詳しくは、[ポータルとポートレット](/help/sites-administering/aem-as-portal.md)を参照してください。

### 静的オブジェクトの有効期限 {#expiration-of-static-objects}

静的オブジェクト（アイコンなど）は変更されません。そのため、（ある程度の期間は）有効期限が切れないようにシステムを設定し、不要なトラフィックを減らす必要があります。

詳しくは、[静的オブジェクトの有効期限](/help/sites-deploying/expiration-static-objects.md)を参照してください。

### Java™ プロセスでファイルを開く {#open-files-in-the-java-process}

各 Java™ プロセスはファイルにアクセスすることがありますが、これにはシステムリソースが必要です。このため、各プロセスが同時にアクセスできるファイル数には上限が定義されます。この値を超えると、例外エラーが発生する場合があります。

AEM プロセスがこの上限を超えると、「`too many open files`」というメッセージが `error.log` に表示されます。

このような例外を回避するには、次の手順を実行します。

1. 開いているファイルのうち、AEM プロセスで使用されているファイルの数をチェックします。

   このチェックは、インスタンスが実行されているプラットフォームに応じて異なります。lsof（UNIX）や Process Explorer（Windows）などのユーティリティを使用できます。

   この値は以下の目的で開発およびテスト中に監視する必要があります。

   * ファイルが必要に応じて閉じられていることを確認するため
   * 様々な状況下での必要な最大値を特定するため

1. 許容される最大値を設定します。

   新しい値は、現在のニーズと今後のピークの両方に対応する必要があるので、現在のニーズの 2 倍の値を設定することをお勧めします。

   デフォルトでは、`serverctl` は `CQ_MAX_OPEN_FILES` を `8192` に設定します。ほとんどの場合はこれで十分です。

### リッチテキストエディターの設定 {#configuring-the-rich-text-editor}

**リッチテキストエディター**（**RTE**）では、テキストコンテンツを編集するための多彩な[機能](/help/sites-authoring/rich-text-editor.md)が提供されており、アイコン、選択ボックス、メニューで WYSIWYG エクスペリエンスを実現できます。

詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。

### ページ編集の取り消しの設定 {#configuring-undo-for-page-editing}

ページを編集する際の取り消しおよびやり直しコマンドの動作を制御するプロパティはいくつかあります。これらは設定について詳しくは、[ページ編集の取り消しの設定](/help/sites-administering/config-undo.md)を参照してください。

### ビデオコンポーネントの設定 {#configuring-the-video-component}

[ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video)を使用すると、事前に定義された標準搭載のビデオアセットをページに配置できます。

適切なトランスコーディングを行うには、管理者が個別に [FFmpeg をインストール](/help/sites-administering/config-video.md#install-ffmpeg)する必要があります。HTML5 要素で使用するために[ビデオプロファイルを設定](/help/sites-administering/config-video.md#configure-video-profiles)することもできます。

### レポートの設定とカスタマイズ {#configuring-and-customizing-reports}

インスタンスの状態を監視および分析しやすいように、CQ ではデフォルトのレポートが提供されており、個々の要件に合わせて設定できます。

詳しくは、[レポートのカスタマイズの基本](/help/sites-administering/reporting.md#the-basics-of-report-customization)を参照してください。

### メール通知の設定 {#configuring-email-notification}

CQ は、次のようなユーザーにメール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある。
* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要がある。

詳しくは、[メール通知の設定](/help/sites-administering/notification.md)を参照してください。

### ページインプレッションの有効化 {#enabling-page-impressions}

ページインプレッションは、クラシック UI のサイト管理コンソールの&#x200B;**インプレッション数**&#x200B;列に表示されます。ページインプレッションの取得を有効にするには、次の設定を行います。

* パブリッシュインスタンス上：

   * [Day CQ WCM Page Statistics](/help/sites-deploying/osgi-configuration-settings.md)

* オーサーインスタンス上：

   * [Adobe Page Impressions Tracker](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>オーサー環境で Adobe Page Impressions Tracker を設定すると、トラッキングサービスへの匿名リクエストが可能になります。
