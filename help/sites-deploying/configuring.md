---
title: 設定の基本概念
description: Adobe Experience Managerの設定方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 28%

---

# 設定の基本概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM) は、すべてのパラメーターのデフォルト設定と共にインストールされ、その設定を「標準」で実行できます。 ただし、独自の要件に合わせてAEMを設定することもできます。

設定できるAEMには、様々な側面があります。

* 一部は [すべてのプロジェクトのインストールで共通に設定](#primary-configuration-considerations) を確認して、プロジェクトに適用できるかどうかを確認する必要があります。
* [その他の設定](#further-configuration-considerations) 必須ではないにもかかわらず、一般的な場合もあります。機能、またはシステムのパフォーマンスと安定性に関連する
* AEMの特定のオプション機能に対してのみ必要な機能もあります（これらは適切な機能と共に記載されています）。

特定の設定に応じて、次のいずれかを使用して変更を加えることができます。

* **Adobe CQ web コンソール**

  これは、OSGi バンドルおよびサービスを設定するための標準的な場所です。

  詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)の詳細と推奨プラクティスを参照してください。

* **リポジトリ**

  OSGi 設定のサブセットは、リポジトリで使用できます。 これにより、リポジトリのコンテンツをコピー（レプリケート）して、同じ設定を再作成できます。 実行モードに応じて、独自の設定をリポジトリに追加することもできます。

  詳しくは、[リポジトリでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)、特に[リポジトリへの新しい設定の追加](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)を参照してください。

* **ファイルシステム**

  ファイルシステム内にはいくつかの設定ファイルが存在します。

* **AEM WCM**

  AEM WCM 内で様々な設定をおこなえます。多くは、レプリケーションエージェントなどの[ツール](/help/sites-administering/tools-consoles.md)コンソールを使用します。

>[!NOTE]
>
>Adobe Experience Manager で作業をする際には、いくつかの方法で OSGi サービスの設定を管理できます（コンソールまたはリポジトリノード）。
>
>詳しくは、 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) 詳細はこちら。

>[!NOTE]
>
>AEMの設定は簡単です。 ただし、特定の変更がアプリケーションに大きな影響を与える可能性があることに注意してください。 このため、AEMの設定を開始する前に、必要な経験と知識を持っていることを確認し、必要な変更を加えてください。 OSGi コンソールを使用して行った変更は、次のとおりです **即時** 実行中のシステムに適用されます（再起動は不要です）。

## プライマリ設定に関する考慮事項 {#primary-configuration-considerations}

このリストでは、すべての新規プロジェクトで一般的に設定される主な領域について詳しく説明します。 すべてが必要とは限りませんが、プロジェクトに適した内容を確認するには、リストを読み取り、確認する必要があります。

リストには、各設定の概要と、詳細を提供するページへのリンクが表示されます。

### セキュリティチェックリスト {#security-checklist}

設定に関するいくつかの主要な問題については、 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md). 必ずこの内容を読み、インストールに必要なアクションを実行してください。

### デフォルト UI の設定 — タッチ操作向け UI またはクラシック UI {#configuring-the-default-ui-touch-optimized-or-classic}

AEMでは、次の 2 つの UI を使用できます。

* タッチ操作向け UI
* クラシック UI

必要な UI を、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md)を使用して設定できます。

>[!NOTE]
>
>UI の選択について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### IPv4 と IPv6 {#ipv-and-ipv}

AEMのすべての要素（リポジトリ、Dispatcher など）は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定が必要ないので、操作はシームレスです。必要に応じて、ネットワークの種類に適した形式で IP アドレスを指定するだけで済みます。

つまり、IP アドレスを指定する必要がある場合、（必要に応じて）次の中から選択できます。

* IPv6 アドレス

  例：`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 アドレス

  例：`https://123.1.1.4:4502`

* サーバー名

  例：`https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストールで解釈されます

  例：`http://localhost:4502`

### バージョンのパージ {#version-purging}

標準インストールでは、（コンテンツの更新後に）ページをアクティベートするたびに、AEMはページまたはノードのバージョンを作成します。 また、リクエストに応じて、 **バージョン管理** サイドキックのタブ これらのバージョンはすべてリポジトリに保存され、必要に応じて復元できます。

これらのバージョンはパージされないので、リポジトリのサイズは時間の経過と共に大きくなるので、管理する必要があります。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。特に、新しいバージョンが作成されたときに古いバージョンをパージするように AEM を設定する方法については、[バージョンマネージャー](/help/sites-deploying/version-purging.md#version-manager)を参照してください。

### ログ {#logging}

AEMでは、次の項目を設定できます。

* central ログサービスのグローバルパラメーター
* リクエストデータログ；要求情報用の特別なログ設定
* 個々のサービス固有の設定例えば、個々のログファイルとログメッセージの形式などです。

詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

### 実行モード {#run-modes}

実行モードを使用すると、特定の目的に合わせてAEMインスタンスを調整できます。 例えば、オーサーまたはパブリッシュ、テスト、開発、イントラネットなどです。

これは、各実行モードに対して設定パラメーターのコレクションを定義することでおこなわれます。 すべての実行モードに対して基本的な設定パラメーターのセットが適用され、特定の環境の目的に合わせて追加のセットを調整できます。これらは必要に応じて適用されます。

すべての設定は 1 つのリポジトリに保存され、 **実行モード**.

詳しくは、 [実行モード](/help/sites-deploying/configure-runmodes.md) 詳細はこちら。

### シングルサインオン {#single-sign-on}

シングルサインオン (SSO) を使用すると、ユーザーは認証資格情報（ユーザー名やパスワードなど）を 1 回入力した後で、複数のシステムにアクセスできます。 別のシステム（信頼された認証子）が認証を実行し、Experience Managerにユーザーの資格情報を提供します。 Experience Managerは、ユーザーのアクセス権限を確認および強制します（つまり、ユーザーがアクセスできるリソースを決定します）。

詳しくは、 [シングルサインオン](/help/sites-deploying/single-sign-on.md) 詳しくは、を参照してください。

### リソースマッピング {#resource-mapping}

リソースマッピングは、AEMのリダイレクト、バニティー URL および仮想ホストを定義するために使用されます。

例えば、これらのマッピングを使用して、次のことをおこなうことができます。

* すべてのリクエストに `/content` というプレフィックスを付けて、web サイトの訪問者に内部構造が表示されないようにする。
* Web サイトの `/content/en/gateway` ページへの要求がすべて `https://gbiv.com/` にリダイレクトされるように、リダイレクトを定義する。

詳しくは、 [リソースマッピング](/help/sites-deploying/resource-mapping.md) 詳しくは、を参照してください。

### レプリケーション、リバースレプリケーション、レプリケーションエージェント {#replication-reverse-replication-and-replication-agents}

レプリケーションエージェントは、次の目的で使用されるメカニズムとしてAEMの中心となります。

* [公開（アクティベート）](/help/sites-authoring/publishing-pages.md) オーサー環境からパブリッシュ環境にコンテンツを書き込むことができます。
* Dispatcher キャッシュからコンテンツを明示的にフラッシュします。
* パブリッシュ環境からオーサー環境（オーサー環境の制御下）にユーザー入力（フォーム入力など）を返します。

詳しくは、 [レプリケーション](/help/sites-deploying/replication.md).

### OSGi 設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEM の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

詳しくは、 [OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md) ：プロジェクトの実装に関連する様々なバンドルのリスト（バンドルに従って表示）。 一覧に表示されるすべての設定を調整する必要はありません。AEMの動作を理解するのに役立つ設定もいくつか記載されています。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### LDAP の設定 {#configuring-ldap}

LDAP 認証は、Active Directory などの（中央の）LDAP ディレクトリに格納されたユーザーを認証するために必要です。 これにより、ユーザーアカウントの管理に必要な作業を削減できます。

LDAP 認証はリポジトリレベルでおこなわれるので、リポジトリによって直接処理されます。詳しくは、[AEM での LDAP の設定](/help/sites-administering/ldap-config.md)を参照してください。

AEM内でのユーザー管理（アクセス権の割り当てを含む）については、 [ユーザー管理とセキュリティ](/help/sites-administering/security.md).

### Dispatcher の設定 {#configuring-the-dispatcher}

Dispatcher は、Adobe Experience Managerのキャッシュ、ロードバランシング、またはその両方を実行するツールです。 エンタープライズクラスの Web サーバーで使用できます。

詳しくは、[Dispatcher ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。特に、設定の詳細については、[Dispatcher の設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja)を参照してください。

### AEM LiveCycle Connector の設定 {#configuring-aem-livecycle-connector}

AEM Doc Services とAEM Doc Security のリリースに伴い、AEMはLiveCycleドキュメントサービスを呼び出して XFA フォームをレンダリングし、ドキュメントをPDFに変換してドキュメントをポリシー保護する機能を持つようになりました。 詳しくは、 [AEMLiveCycleコネクタ](https://helpx.adobe.com/jp/livecycle/help/aem/aem-livecycle-connector.html) を参照してください。

### ジョブのオフロードとトポロジの管理 {#job-offloading-and-topology-administration}

[オフロードによって、トポロジ内の Experience Manager インスタンス間で処理タスクが配布されます。](/help/sites-deploying/offloading.md)オフロードを使用すると、特定のExperience Managerインスタンスを使用して特定のタイプの処理を実行できます。 特殊な処理により、使用可能なサーバーリソースの使用を最大限に活用できます。

トポロジは、オフロードに参加している疎結合Experience Managerクラスタです。 クラスタは、1 つ以上のExperience Managerサーバーインスタンスで構成されます（1 つのインスタンスがクラスターと見なされます）。

トポロジメンバーシップの表示または変更方法の詳細については、 [トポロジの管理](/help/sites-deploying/offloading.md#administering-topologies) 」セクションに入力します。

### ようこそコンソールの設定 {#configuring-the-welcome-console}

クラシック UI のようこそコンソールには、AEM内の様々なコンソールおよび機能へのリンクのリストが表示されます。

表示されるリンクを設定できます。詳しくは、 [ようこそコンソールの設定](/help/sites-developing/customizing-the-welcome-console.md) 詳しくは、を参照してください。

### パフォーマンスの設定 {#configuring-for-performance}

[パフォーマンス](/help/sites-deploying/configuring-performance.md) がプロジェクトの鍵となります。 パフォーマンスを最適化するために AEM（および基盤となるリポジトリ）の特定の要素を設定できます。

詳しくは、[パフォーマンスの設定](/help/sites-deploying/configuring-performance.md#configuring-for-performance)を参照してください。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共有データストア {#shared-data-store}

リポジトリのデータストアは、サイズの大きいバイナリのストレージを適切なリポジトリから別の領域にオフロードするために使用します。これによって、リポジトリツリー内の同じバイナリ（画像など）の複数のインスタンスは 1 回だけ格納されます。

この「1 回のみ、参照 — 多回」機能は、1 つのリポジトリツリーだけでなく、完全に別々のリポジトリに対応するように拡張できます。それには、各データストアを同じ共有ファイルシステムの場所を参照するように設定します。

このようなデータストアは、同じクラスター内の異なるノード間、同じインストール内の異なるパブリッシュインスタンスやオーサーインスタンス間、または異なるインストール内の完全に別々のインスタンス間で共有できます。

詳しくは、 [データストアとノードストアの設定](/help/sites-deploying/data-store-config.md).

## その他の設定に関する考慮事項 {#further-configuration-considerations}

### HTTP over SSL の有効化 {#enabling-http-over-ssl}

HTTP over SSL を有効にして、サーバーへのより安全な接続を使用できます。

詳しくは、 [HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md) 詳しくは、を参照してください。

### AEM ポータルとポートレット {#aem-portals-and-portlets}

ポータルとは、パーソナライズ機能、シングルサインオン、様々なソースからのコンテンツ統合を提供し、情報システムのプレゼンテーションレイヤーをホストする Web アプリケーションです。 ポートレットコンポーネントを使用して、ページにポートレットを埋め込むこともできます。 CQ5 WCM が提供するコンテンツにアクセスするには、ポータルサーバーに CQ5 Portal Director Portlet を取り付けます。 これをおこなうには、ポータルページにポートレットをインストール、設定、追加します。

詳しくは、[ポータルとポートレット](/help/sites-administering/aem-as-portal.md)を参照してください。

### 静的オブジェクトの有効期限 {#expiration-of-static-objects}

静的オブジェクト（アイコンなど）は変更されません。 したがって、期限が切れない（妥当な期間）ように、不要なトラフィックを減らすように、システムを設定する必要があります。

詳しくは、 [静的オブジェクトの有効期限](/help/sites-deploying/expiration-static-objects.md) 詳しくは、を参照してください。

### Java™プロセスでファイルを開く {#open-files-in-the-java-process}

各 Java™プロセスがファイルにアクセスする場合があります。この場合は、システムリソースが必要です。 このため、各プロセスが同時にアクセスできるファイル数の上限が定義されます。 この値を超えると、例外エラーが発生する場合があります。

AEMプロセスがこの最大値を超える場合、「 `too many open files`」が `error.log`.

このような例外を回避するには、次の手順を実行します。

1. AEMプロセスで使用している開いているファイルの数を確認します。

   このチェックは、インスタンスが実行されているプラットフォームに応じて異なります。 lsof(UNIX®) や Process Explorer(Windows) などのユーティリティを使用できます。

   この値は以下の目的で開発およびテスト中に監視する必要があります。

   * ファイルが必要に応じて閉じられていることを確認するため
   * 様々な状況下での必要な最大値を特定するため

1. 許容される最大値を設定します。

   新しい値は、現在のニーズと今後のピークの両方に対応する必要があるので、現在のニーズを 2 倍にすることをお勧めします。

   デフォルトでは、`serverctl` は `CQ_MAX_OPEN_FILES` を `8192` に設定します。ほとんどの場合はこれで十分です。

### リッチテキストエディターの設定 {#configuring-the-rich-text-editor}

この **リッチテキストエディター** (**RTE**) は、様々な種類の [機能](/help/sites-authoring/rich-text-editor.md) テキストの内容を編集する場合に使用します。アイコン、選択ボックスおよびメニューを提供して、WYSIWYG 環境で使用できます。

詳しくは、 [リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md) 詳しくは、を参照してください。

### ページ編集のための取り消しの設定 {#configuring-undo-for-page-editing}

ページを編集する際の取り消しおよびやり直しコマンドの動作を制御するプロパティはいくつかあります。 これらは設定できます。詳しくは、 [ページ編集の取り消しの設定](/help/sites-administering/config-undo.md) 詳しくは、を参照してください。

### ビデオコンポーネントの設定 {#configuring-the-video-component}

この [ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video) では、事前に定義された標準提供ビデオ要素をページに配置できます。

適切なトランスコードをおこなうには、管理者が [FFmpeg のインストール](/help/sites-administering/config-video.md#install-ffmpeg) 個別に。 また、 [ビデオプロファイルの設定](/help/sites-administering/config-video.md#configure-video-profiles) html5 要素で使用する場合。

### レポートの設定とカスタマイズ {#configuring-and-customizing-reports}

インスタンスの状態を監視および分析するのに役立つように、CQ では、個々の要件に合わせて設定できるデフォルトのレポートを選択できます。

詳しくは、 [レポートのカスタマイズの基本](/help/sites-administering/reporting.md#the-basics-of-report-customization) 詳しくは、を参照してください。

### メール通知の設定 {#configuring-email-notification}

CQ は次のユーザーに電子メール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある
* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要がある。

詳しくは、 [電子メール通知の設定](/help/sites-administering/notification.md) 詳しくは、を参照してください。

### ページインプレッション数の有効化 {#enabling-page-impressions}

ページインプレッション数は、 **Impressions** クラシック UI siteadmin コンソールの列。 ページインプレッション数のキャプチャを有効にするには、以下を設定します。

* パブリッシュインスタンスで、以下の手順を実行します。

   * [Day CQ WCM Page Statistics](/help/sites-deploying/osgi-configuration-settings.md)

* オーサーインスタンス上：

   * [Adobeページインプレッショントラッカー](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>オーサー環境でAdobeページインプレッショントラッカーを設定すると、トラッキングサービスに対する匿名リクエストが許可されます。
