---
title: OSGi 設定
seo-title: OSGi 設定
description: この記事では、プロジェクトの実装に関連する OSGi 設定（バンドルに従ってリストされます）について説明します。このリストはガイドラインの役割を果たすものであり、完全ではありません。
seo-description: この記事では、プロジェクトの実装に関連する OSGi 設定（バンドルに従ってリストされます）について説明します。このリストはガイドラインの役割を果たすものであり、完全ではありません。
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: 設定
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: ca66c0655bcd878644e275fc8f7a41b38110beae
workflow-type: tm+mt
source-wordcount: '3561'
ht-degree: 60%

---

# OSGi 設定{#osgi-configuration-settings}

[](https://www.osgi.org/) OSGは、AEMのテクノロジースタックの基本要素です。AEMの複合バンドルとその設定を制御するために使用されます。

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。**

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各OSGiコンポーネント（[OSGi仕様](https://www.osgi.org/Specifications/HomePage)を参照）は、様々なバンドルの1つに含まれています。 AEMを使用する場合、このようなバンドルの設定を管理する方法はいくつかあります。詳細および推奨プラクティスについては、[OSGi](/help/sites-deploying/configuring-osgi.md)の設定を参照してください。

次の OSGi 設定（バンドルに従ったリスト）は、プロジェクトの実装に関連しています。すべての設定に調整が必要なわけではなく、一部の設定は AEM の動作を説明する目的で言及されています。

>[!CAUTION]
>
>このリストはガイドラインの役割を果たすものであり、完全ではありません。すべてのバンドルがリストされているわけではなく、リストされているバンドルに関しても、すべてのパラメーターがリストされているわけではありません。
>
>必要な設定は、プロジェクトによって異なります。
>
>使用する値およびパラメーターの詳細は、Web コンソールを確認してください。

>[!NOTE]
>
>[AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)の一部であるOSGi Configuration Diffツールを使用して、デフォルトのOSGi設定をリストできます。

>[!NOTE]
>
>AEM 内の機能の特定の領域では、さらに多くのバンドルが必要な場合があります。この場合、設定の詳細は、該当する機能の関連ページで確認できます。

**AEMレプリケーションイベン** トListenerConfigure:

* **実行モード**。このモードでは、レプリケーションイベントがリスナーに配布されます。 例えば、オーサーとして定義された場合、これはレプリケーションを「開始」するシステムです。

* プロジェクトコードがパブリッシュ環境でレプリケーションイベント（リバースレプリケーション）を処理する場合は、実行モード&#x200B;**publish**&#x200B;を追加する必要があります。 例えば、Dispatcherを使用してパブリッシュ環境からフラッシュする場合や、他のパブリッシュインスタンスへの標準レプリケーションが発生する場合などです。

**AEMリポジトリ変更** リスナー：

* **パス**：配布準備が整ったリポジトリイベントをリッスンする場所。

**CRX Sling Client Repository基にな** るコンテンツリポジトリへのアクセスを設定します。

* **Admin Password**&#x200B;は、インスタンスの[セキュリティ](/help/sites-administering/security-checklist.md)を確実にするために、インストール後に変更する必要があります。
* その他の変更は必要ありません。リポジトリへのアクセスに影響を与える可能性があるので、注意が必要です。

**Wikiメールサ** ービスWikiから送信される電子メールの電子メール設定を構成します。

**Apache Felix OSGi Management ConsoleConfigure:** 

* **Plugins**：**Apache Felix Web Management Console** で最上位のメニュー項目として使用できる、メインのナビゲーション項目（コンソールプラグイン）です。それぞれ容量とリソースが必要なので、不要なものは無効にしてください。

>[!CAUTION]
>
>必ず以下を設定してください。
>
>**ユー** ザー名と **パスワード**:Apache Felix Web Management Console自体にアクセスするための資格情報です。
>インスタンスの[セキュリティ](/help/sites-administering/security-checklist.md)を確保するために、最初のインストール後にパスワードを変更する必要があります。

>[!NOTE]
>
>この設定は起動時に必要なので、リポジトリが使用可能になる前に、Felix コンソールを使用して設定する必要があります。

**Apache Sling Customizable Request Data LoggerConfigure:** 

* **ロガー** 名とロ **グ** 形式：要求とアクセスログの場所と形式を設定します(デフォルト： `request.log`)をクリックします。 このログファイルは、Webチェーンに関連するパフォーマンスやデバッグ機能を分析する際に不可欠です。これは [Apache Sling Request Logger](#apacheslingrequestlogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Eventing Thread PoolConfigure:** 

* **Min Pool Size** および **Max Pool Size**：イベントスレッドを保持するために使用するプールのサイズ。

* **Queue Size**：プールを使い果たした場合のスレッドキューの最大サイズ。推奨値は`-1`です。これは、キューを無制限に設定します。制限を設定すると、制限を超えた場合に損失が発生する可能性があります。

* これらの設定を変更すると、イベント数が非常に多い状況（例：AEM DAM またはワークフローの使用頻度が高い場合）におけるパフォーマンスの強化に役立ちます。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定はインスタンスのパフォーマンスに影響を及ぼす可能性があるので、変更の際は十分な理由と検討が必要です。

**Apache SlingGETサーブレ** ットレンダリングのいくつかの側面を設定します。

* **Auto Index**：閲覧のためのディレクトリのレンダリングを有効または無効にします。
* **Enable**（または Disable）：デフォルトのレンディション（**HTML**、**Plain Text**、**JSON**、**XML** など）を有効または無効にします。JSON を無効にしないでください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Java Script Handler.javaファ** イルをスクリプト（サーブレット）としてコンパイルするための設定。

特定の設定がパフォーマンスに影響を及ぼす可能性があります。可能な場合（特に、実稼動インスタンスの場合）は、それらを無効にしてください。

* **Source VM** および **Target VM**：ランタイム JVM として使用する JDK バージョンを定義します。

* 実稼動インスタンスの場合：

   * 「**Generate Debug Info**」を無効化

**Apache Sling JCR Installerこれらのパ** ラメーターは、おそらく設定は必要ありませんが、開発やデバッグを行う際に知っておくと役に立ちます。例えば、インストールフォルダーはパッケージのチェックイン／チェックアウトまたは作成に役立つ場合があります。

* **インストールフォルダー名** regexpand  **Max hierarchy depth of install folders**  — インストールするリソースを検索するリポジトリフォルダーの場所と深さを指定します。ワイルドカードを使用する場合（のように）。*/install)適切な一致がすべて検索されます（例：`/libs/sling/install`と`/libs/cq/core/install`）。

* **Search Path**：インストールするリソースを jcrinstall が検索するパスのリストです。そのパスの重み付け係数を示す数値も表示されます。

**Apache Sling Job Event Handlerジョブスケジュ** ールを管理する次のパラメーターを設定します。

* **再試行間隔**、 **再試行の最大回数**、 **並列ジョブの最大数**、 **待機時間の確認**&#x200B;など。

* これらの設定を変更すると、多数のジョブが存在するシナリオのパフォーマンスが向上します。例えば、AEM DAMとワークフローを大量に使用する場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定は理由なく変更しないでください。変更する前に考慮してください。

**Apache Sling JSP Script Handler JSPスクリプ** トハンドラーのパフォーマンス関連の設定を設定します。パフォーマンスを向上するには、可能な限り設定を無効にしてください。

特に、実稼動インスタンスの場合は、次の設定を無効にします。

* 「**Generate Debug Info**」を無効化
* **Keep Generated Java**
* **Mapped Content**
* **Display Source Fragments**

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Logging ConfigurationConfigure:** 

* **Log Level** および **Log File**：主要なログ設定（error.log）の場所とログレベルを定義します。レベルは、`DEBUG`、`INFO`、`WARN`、`ERROR`、`FATAL`のいずれかに設定できます。

* **Number of Log Files** および **Log File Threshold**：ログファイルのサイズとバージョンのローテーションを定義します。

* **Message Pattern**：ログメッセージの形式を定義します。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md#global-logging)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Logging Logger Configuration（ファクトリ設定）** 設定：

* **Log Level**、**Log File** および **Message Format**：ログファイルとメッセージの詳細を定義します。

* **Logger**：カテゴリを定義します（例：com.day.cq のログのみ）。

* 「**Factory Configurations**」を使用することにより、必要とされる様々なログレベルとカテゴリに応じて、任意の数の設定を追加できます。
* このような設定は開発時に役立ちます。例えば、特定のログファイルで、特定のサービスのトレースメッセージをログに記録する場合などです。
* このような設定は実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個々のログファイルに記録して、簡単に監視できるようにする場合などです。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Logging Writer Configuration（ファクトリ設定）** 設定：

* **Log File**：ログファイルの有無を定義します。
* **Number of Log Files**：バージョンのローテーションを定義します。

* ライターは **Apache Sling Logging Logger Configuration** 設定で使用できます。

* このような設定は開発時に役立ちます。例えば、特定のログファイルで、特定のサービスのトレースメッセージをログに記録する場合などです。
* このような設定は実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個々のログファイルに記録して、簡単に監視できるようにする場合などです。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Main** ServletConfigure:

* **Number of Calls per Request** および **Recursion Depth**：無限再帰および過度のスクリプトの呼び出しからシステムを保護します。

**Apache Sling MIME Type** ServiceConfigure:

* **MIME Types**：プロジェクトで必要な MIME タイプをシステムに追加します。これにより、ファイルに対する `GET` 要求において、ファイル形式とアプリケーションをリンクするための適切な content-type ヘッダーを設定できます。

**Apache Sling Referrer FilterCRX WebDAVお** よびApache Slingのクロスサイトリクエストフォージェリ(CSRF)に関する既知のセキュリティ問題に対処するには、リファラーフィルターを設定する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* フィルター処理する HTTP メソッド
* 空のリファラーヘッダーを使用できるかどうか
* と、サーバホストに加えて許可されるサーバのリスト。

詳しくは、[「セキュリティチェックリスト」のクロスサイトのリクエスト偽造に関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。

>[!NOTE]
>
>Apache Sling Referrer Filter はクイックフィックスパッケージのインストールに依存します。

**Apache Sling Request** LoggerConfigure:

* 要求をログに記録する方法を定義するための様々なパラメーター。
* **Enable Request Log**：有効または無効にします。

* **Enable Access Log**：有効または無効にします。

これは [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Resource Resolver FactorySlingリソ** ース解決の主要な側面を設定します。

* **リソース検索パス**&#x200B;を追加します(ただし、削除や削除はしな `/libs` いでくだ `/apps`さい)。

* **Virtual URLs**：バニティー URL のマッピングを定義します。

* **エイリアス** を定義するURLマッピング例えば、からに変 `/content` 更しま `/`す。

* **マッピング場所**：で外部化されたマッパー設定 `/etc/map`。

* ローカルインストールを使用して（例えば、`https://localhost:4502/system/console/jcrresolver`を使用して）、どのResource Resolverがアクティブかを判断します。

詳しくは、[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution) を参照してください。

>[!CAUTION]
>
>具体的には、これらのオプションはリポジトリで設定する必要があります。
>
>そうしないと、Felix コンソールでおこなった「**URL Mappings**」に対する変更が、次回の起動時に AEM によって上書きされる可能性があります。

**Apache Sling Servlet/Script Resolver and Error** Handler Sling ServletとScript Resolverには複数のタスクがあります。

1. `ServletResolver` として使用され、要求を処理するために呼び出す Servlet または Script を選択します。

1. `SlingScriptResolver`として機能します。

1. エラー処理を管理します。そのためには、要求処理のサーブレット／スクリプトの解決に使用するのと同じアルゴリズムを使用してエラー処理のサーブレット／スクリプトを選択する `ErrorHandler` インターフェイスを実装します。

次のような様々なパラメーターを設定できます。

* **Execution Paths**：実行可能なスクリプトを検索するパスを表示します。特定のパスを設定することで、実行可能なスクリプトを制限できます。パスを設定しない場合は、デフォルト(`/` = root)が使用され、すべてのスクリプトを実行できます。

設定したパス値がスラッシュで終わる場合は、サブツリー全体が検索されます。末尾にスラッシュを指定しないと、完全一致の場合にのみスクリプトが実行されます。

* **Script User**：このオプションのプロパティでは、スクリプトの読み取りに使用するリポジトリユーザーアカウントを指定できます。アカウントを指定しない場合は、`admin` ユーザーがデフォルトで使用されます。

* **Default Extensions**：デフォルトの動作が使用される拡張子のリストです。つまり、リソースタイプの最後のパスセグメントをスクリプト名として使用できます。

**Day Commons GFX Font Helperグラフィックのレ** ンダリング時に、DrawTextを使用してテキストを埋め込むことができます。そのために、独自のフォントをインストールすることも可能です。

* プロジェクト固有のフォントを検索する&#x200B;**フォントパス**を定義します。
例：`/apps/myapp/fonts`。

**Apache HTTPコンポーネントプ** ロキシConfigurationProxy HTTPクライアントを使用するすべてのコードの設定（HTTPの作成時に使用）例えば、レプリケーション時などです。

新しい設定を作成する場合は、ファクトリ設定を変更せずに、次の場所にある設定マネージャーを使用して、このコンポーネントの新しいファクトリ設定を作成します。**https://localhost:4502/system/console/configMgr/**. プロキシ設定は、 **org.apache.http.proxyconfigurator.**&#x200B;で使用できます。

>[!NOTE]
>
>AEM 6.0 以前のリリースでは、プロキシは Day Commons HTTP Client で設定されていました。AEM 6.1 以降のリリースでは、プロキシ設定は、「Day Commons HTTP Client」設定ではなく、「Apache HTTP Components Proxy Configuration」に移動されました。

**Day CQ** Antispam使用するスパム対策サービス(Akismet)を設定します。次の項目を登録する必要があります。

* **プロバイダー**
* **API キー**
* **登録済みの URL**

**AdobeGranite HTMLライブラリマ** ネージャークライアントライブラリ（cssまたはjs）の処理を制御するように設定します。例えば、基になる構造の表示方法を含みます。

* 実稼動インスタンスの場合：

   * 「**Minify**」を有効化（CRLF および空白文字を削除）
   * 「**Gzip**」を有効化（1 回の要求でファイルを gzip してアクセスするため）
   * 「**Debug**」を無効化
   * 「**Timing**」を無効化

* JS 開発の場合（特に、Firebug を使用するか、デバッグをおこなう場合）：

   * 「**Minify**」を無効にします。
   * 「**Debug**」を有効にして、デバッグ用のファイルを分離し、Firebug で使用します。
   * 「**Timing**」を有効にします（タイミングに関する設定をおこなう場合）。
   * **Debug** コンソールを有効にして、JS コンソールのログメッセージを確認します。

>[!CAUTION]
>
>**Minify**&#x200B;または&#x200B;**Gzip**&#x200B;の設定を変更する場合は、`/var/clientlibs`の内容も削除する必要があります。これは、キャッシュされたバージョンのclientlibで、次回の要求時に再構築されます。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ HTTP Header Authentication HandlerSystem** wide HTTPリクエストの基本認証方法の設定。

[閉じられたユーザーグループ](/help/sites-administering/cug.md)を使用すると、（特に）以下を設定できます。

* **HTTP レルム**
* **デフォルトのログインページ**

**Day CQ Link Checker ServiceCheckおよび必要に** 応じて次の設定をおこないます。

* **Scheduler Period**：外部リンクを自動的にチェックする間隔を定義します。

* **Bad Link Tolerance Interval**：失敗した外部リンクが無効と見なされるまでの期間を指定します。
* **Link Check Override Patterns**：リンクチェックから除外するパスを定義します。

**Day CQ Link Checker Task単一のリ** ンクチェックタスク（外部リンクをチェックするタスク）の設定：

* **Good Link Test Interval** および **Bad Link Test Interval で定義されている間隔をチェックします。** 

* リンクをチェックする際に外部アクセスのために必要な、インターネットアクセスおよび NTLM 用のプロキシに関連する様々なパラメーターを設定します。

**Day CQ Mail Serviceメールサ** ーバーのホスト名とアクセスの詳細を設定します。メールサービスの設定の節を参照してください。

**Day CQ MCM Newsletterニュース** レターで使用する様々な設定を指定します。

**Day CQ Root** MappingConfigure:

* **Target** Path :「 」への要求のリダイレクト先を `/`定義します。

AEM では次の 2 つの UI を使用できます。

* タッチ操作対応 UI が標準の UI です。
* 廃止されたクラシック UI も引き続き完全に機能します。

AEM ルートマッピングを使用すると、希望する UI を、インスタンスのデフォルトとして設定できます。

* タッチ操作対応UIをデフォルトのUIとして使用するには、**Target Path**&#x200B;で次を指す必要があります。

   ```
      /projects.html
   ```

* クラシックUIをデフォルトのUIにするには、**ターゲットパス**&#x200B;で次を指す必要があります。

   ```
      /welcome.html
   ```

>[!NOTE]
>
>標準インストールでは、タッチ操作向け UI がデフォルトの UI です。

**AdobeGranite SSO Authentication** Handlerシングルサインオン(SSO)の設定の詳細多くの場合、エンタープライズオーサーの設定で、多くの場合、LDAPと組み合わせて必要になります。

様々な設定プロパティがあります。

* **Path**&#x200B;この認証ハンドラーをアクティブにする対象のパス。このパラメーターを空のままにすると、認証ハンドラーは無効になります。例えば、/ というパスを指定すると、認証ハンドラーはリポジトリ全体に対して使用されます。

* **Service RankingOSGi Framework Service Ranking値**
は、このサービスの呼び出しに使用される順序を示すために使用されます。これは、 
`int` 値が大きいほど優先順位が高くなります。デフォルト値は `0` です。

* **Header Names**
ユーザー ID を含む可能性のあるヘッダーの名前です。

* **Cookie Names**
ユーザー ID を含む可能性のある cookie の名前です。

* **Parameter Names**
ユーザー ID を指定する可能性のある要求パラメーターの名前です。

* **User**
Map選択したユーザーの場合、HTTPリクエストから抽出されたユーザー名を、credentialsオブジェクト内の別のユーザー名に置き換えることができます。マッピングはここで定義します。ユーザー名 
`admin` はマップの両側に表示され、マッピングは無視されます。「=」文字は、先頭に「\」を付けてエスケープする必要があります。

* **Format**
ユーザー ID を指定する際の形式を示します。次のいずれかを使用します。

   * `Basic`：ユーザー ID が HTTP Basic 認証形式でエンコードされている場合
   * `AsIs`：ユーザー ID がプレーンテキストで指定されている場合や、正規表現が適用されている値をそのまま、または正規表現として使用する必要がある場合

**Day CQ WCM Debug Filterページにア** クセスする際に？debug=layoutなどのサフィックスを使用できるので、開発時に役立ちます。例えば、https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layoutは、開発者が興味を持つ可能性のあるレイアウト情報を提供します。

* パフォーマンスとセキュリティを確保するために、実稼動インスタンスではこれを無効にします。

**Day CQ WCM FilterConfigure:** 

* **WCM Mode **：デフォルトモードを定義します。
* オーサーインスタンスでは、`edit`、`disable,preview`、`analytics`のいずれかになります。
その他のモードは、サイドキックからアクセスするか、サフィックス`?wcmmode=disabled`を使用して実稼動環境をエミュレートできます。

* パブリッシュインスタンスでは、`disabled` に設定して、その他のモードにアクセスできないようにする必要があります。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ WCM Link Checker ConfiguratorConfigurator** 設定：

* **書き換え設定のリスト**：コンテンツベースのリンクチェックツール設定の場所のリストを指定します。設定は実行モードに基づくことができます。これはオーサー環境とパブリッシュ環境を区別するために重要です。それぞれの環境でリンクチェッカーの設定が異なる場合があるからです。

**Day CQ WCM Page** ProcessorConfigure:

* **パス**：システムが `jcr:Event` をトリガーする前にページの変更をリッスンする場所のリストです。

**Adobeページインプ** レッショントラッカーオーサーインスタンスの場合は、次の設定をおこないます。

* **sling.auth.requirements**:このプロパティの値をに設定します。  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>この設定では、トラッキングサービスへの匿名リクエストが許可されます。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Page** StatisticsFor a publish instance設定：

* **URL to send data**：ページ統計の追跡に使用する URL を設定します（トラッカー要求が Dispatcher を経由する場合は必須）。例えば、デフォルトは `https://localhost:4502/libs/wcm/stats/tracker` です。

* **Tracking script enabled**：ページ上の追跡スクリプトのインクルードを有効化（`true`）または無効化（`false`）します。デフォルト値は `false` です。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Version ManagerControlは、シ** ステム内でバージョンを管理する場合と方法を示します。

* **Create Version on Activation**：標準インストールで有効になります。
* **Enable Purging**

* **Purge Paths**：検索アクションで検索するパス。
* **Implicit Versioning Paths**：暗黙のバージョン管理がアクティブなパス。

* **Max Version Age**：バージョンの最長有効期間（日数）。

* **Max Number Versions**：保存するバージョンの最大数。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。

**Day CQ Workflow Email Notification Serviceワークフ** ローから送信される通知の電子メール設定を指定します。

**CQ Rewriter HTML Parser Factory**

CQ リライターの HTML パーサーを制御します。

* **Additional Tags to Process** - パーサーで処理する HTML タグを追加または削除できます。デフォルトで処理されるタグは、A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD です。
* **キャメルケースを保持**  — デフォルトでは、HTMLパーサーはキャメルケース（eBayなど）の属性を小文字（ebayなど）に変換します。キャメルケースの属性を保持するには、これをオフにします。これは、Angular 2 などのフロントエンドフレームワークを使用する際に役立ちます。

**Day Commons JDBC Connections Poolコンテンツのソ** ースとして使用される外部データベースへのアクセスを設定します。

これはファクトリ設定なので、複数のインスタンスを設定できます。

**Adobe CQ Media DPS Sessions Serviceパブリケーシ** ョンで使用するDPSセッションを管理します。

具体的には、`dps.session.service.url.name`、  を定義できます。デフォルトは [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions) に設定されています。

**アセッ** ト/バイナリが安全な方法でエンドユーザーに配信されるように、AEMとCDN間のCDN RewriterCommunicationを確保する必要があります。この方法では 2 つのタスクをおこないます。

* 最初（またはキャッシュ内のリソースが期限切れになった後）に、CDN を介して AEM からリソースにアクセスします。
* CDN にリソースがキャッシュされた後は、CDN にキャッシュされたリソースに安全にアクセスします。要求は AEM に送信されず、そのリソースにアクセスできるすべてのユーザーの処理は CDN でおこなわれます。

AEM は、内部アセットの URL を外部の CDN URL に書き直すリライターを提供しています。これにより、JWS 署名および有効期限を含む、CDN に渡すリンクが書き直され、アセットに安全にアクセスできるようになります。この機能は、オーサーインスタンスで使用されます。

全体的なフローは次のとおりです。

1. ユーザーが AEM で認証をおこない、アセットを含むページを要求します。
1. 要求されたページに`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`のようなアセットが含まれています
1. リライターは、リンクをJWS署名を含むCDN URLに変換します。
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. ユーザーのブラウザーによって、CDN サーバーにアセット要求が転送されます。
1. 要求が `cdn_sign` パラメーターと共に AEM に転送されるように、CDN を設定する必要があります。
1. 認証ハンドラーによって `cdn_sign` パラメーターが検証され、CDN にアセットが返された後、アセットがユーザーに配信されます。

次の図に、ユーザーのブラウザー、CDN および AEM の間のフローを示します。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>現在、この機能は、AEM オーサーインスタンスでのみ使用できます。

**** CDNConfigServiceImpl CDN設定を提供します

CDNの書き換え機能は、com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImplの設定に&#x200B;**CDN配布ドメイン名**&#x200B;を指定することで有効にできます。

また、このサービスには、CDN 書き直しの有効化／無効化、CDN 書き直しが実行されるパスのプレフィックス、TTL 値、プロトコル（HTTP または HTTPS）など、その他の設定オプションも含まれます。

**** CDNRewriterA内部画像URLをCDN URLに書き換えるリライター

com.adobe.cq.cdn.rewriter.impl.CDNRewriterの&#x200B;**タグ属性**&#x200B;値を定義して、選択した画像リンクのみが書き換えられるようにすることができます。
