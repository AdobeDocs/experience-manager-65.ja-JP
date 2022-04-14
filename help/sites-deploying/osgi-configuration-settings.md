---
title: OSGi 設定
seo-title: OSGi Configuration Settings
description: この記事では、プロジェクトの実装に関連する OSGi 設定（バンドルに従ってリストされます）について説明します。このリストはガイドラインの役割を果たすものであり、完全ではありません。
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 9a3f26b6709461a911e833f7e340d11c759c7dae
workflow-type: tm+mt
source-wordcount: '3558'
ht-degree: 98%

---

# OSGi 設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEM の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます&#x200B;*。*

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント ( [OSGi の仕様](https://www.osgi.org/Specifications/HomePage)を参照) は、様々なバンドルの 1 つに含まれています。 AEM で作業する場合、このようなバンドルの構成設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

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
>OSGi 設定の差分ツール（[AEM ツール](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)の一部）を使用して、デフォルトの OSGi 設定のリストを表示できます。

>[!NOTE]
>
>AEM 内の機能の特定の領域では、さらに多くのバンドルが必要な場合があります。この場合、設定の詳細は、該当する機能の関連ページで確認できます。

**AEM レプリケーションイベントリスナー**&#x200B;設定：

* **実行モード**：レプリケーションイベントがリスナーに配信されます。 例えば、オーサーとして定義されている場合、これはレプリケーションを「開始」するシステムです。

* プロジェクトコードがパブリッシュ環境でレプリケーションイベント（リバースレプリケーション）を処理する場合は、実行モード&#x200B;**公開**&#x200B;を追加する必要があります。 例えば、Dispatcher を使用してパブリッシュ環境からフラッシュする場合や、他のパブリッシュインスタンスへの標準レプリケーションが発生する場合などです。

**AEM リポジトリ変更リスナー**&#x200B;設定：

* **パス**：配布準備が整ったリポジトリイベントをリッスンする場所

**CRX Sling クライアントリポジトリ** 基になるコンテンツリポジトリへのアクセスを設定します。

* **管理者パスワード**&#x200B;をインストール後に変更して、インスタンスの [セキュリティ](/help/sites-administering/security-checklist.md) を確保してください。
* その他の変更は必要ありません。また、リポジトリへのアクセスに影響を与える可能性があるので、注意が必要です。

**Wiki メールサービス** Wiki から送信されるメールの設定をします。

**Apache Felix OSGi 管理コンソール**&#x200B;設定：

* **Plugins**：**Apache Felix Web Management Console** で最上位のメニュー項目として使用できる、メインのナビゲーション項目（コンソールプラグイン）です。それぞれ容量とリソースが必要なので、不要なものは無効にしてください。

>[!CAUTION]
>
>必ず以下を設定してください。
>
>**ユーザー名**&#x200B;と&#x200B;**パスワード**：Apache Felix web 管理コンソールにアクセスするための資格情報です。
>インスタンスの[セキュリティ](/help/sites-administering/security-checklist.md)を確保するには、最初のインストールの後にパスワードを変更する必要があります。

>[!NOTE]
>
>この設定は起動時に必要なので、リポジトリが使用可能になる前に、Felix コンソールを使用して設定する必要があります。

**Apache Sling Customizable Request Data Logger** 設定：

* **ロガー名**&#x200B;と&#x200B;**ログ形式**：リクエストおよびアクセスのログの場所と形式を設定します（デフォルト：`request.log`）。このログファイルは、パフォーマンスを分析する際や、web チェーンに関連する機能をデバッグする際に必須です。
これは [Apache Sling Request Logger](#apacheslingrequestlogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Eventing Thread Pool** 設定：

* **Min Pool Size** および **Max Pool Size**：イベントスレッドを保持するために使用するプールのサイズ。

* **Queue Size**：プールを使い果たした場合のスレッドキューの最大サイズ。推奨値は `-1` です（キューが無制限に設定されます）。制限を設定すると、その制限を超えた場合にスレッドが失われる可能性があります。

* これらの設定を変更すると、イベント数が非常に多い状況（例：AEM DAM またはワークフローの使用頻度が高い場合）におけるパフォーマンスの強化に役立ちます。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定はインスタンスのパフォーマンスに影響を及ぼす可能性があるので、変更の際は十分な理由と検討が必要です。

**Apache Sling GET Servlet**&#x200B;レンダリングの一部の要素を設定します。

* **Auto Index**：閲覧のためのディレクトリのレンダリングを有効または無効にします。
* **Enable**（または Disable）：デフォルトのレンディション（**HTML**、**Plain Text**、**JSON**、**XML** など）を有効または無効にします。JSON を無効にしないでください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Java Script Handler** .java ファイルのコンパイルを、スクリプト（サーブレット）として設定します。

特定の設定がパフォーマンスに影響を及ぼす可能性があります。可能な場合（特に、実稼動インスタンスの場合）は、それらを無効にしてください。

* **Source VM** および **Target VM**：ランタイム JVM として使用する JDK バージョンを定義します。

* 実稼動インスタンスの場合：

   * 「**デバッグ情報の生成**」を無効化

**Apache Sling JCR Installer** 多くの場合、これらのパラメーターの設定は必要ありませんが、設定を理解しておくと開発時やデバッグ時に役立ちます。例えば、インストールフォルダーはパッケージのチェックイン／チェックアウトまたは作成に役立つ場合があります。

* **Installation folders name regexp** および **Max hierarchy depth of install folders**：インストールするリソースを検索するリポジトリフォルダーとその階層の深さを指定します。ワイルドカードを&#42;/install) すべての適切な一致が検索されます。例： `/libs/sling/install` および `/libs/cq/core/install`.

* **Search Path**：インストールするリソースを jcrinstall が検索するパスのリストです。そのパスの重み付け係数を示す数値も表示されます。

**Apache Sling Job Event Handler** ジョブのスケジュール設定を管理するパラメーターを設定します。

* **再試行間隔**、**再試行の最大回数**、**並列ジョブの最大数**、**待機時間の確認**&#x200B;など。

* これらの設定を変更すると、多数のジョブが存在するシナリオのパフォーマンスが向上します。例えば、AEM DAM とワークフローの使用頻度が高い場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定は理由なく変更しないでください。十分に検討してから変更してください。

**Apache Sling JSP Script Handler** JSP スクリプトハンドラーのパフォーマンス関連の設定を行います。 パフォーマンスを向上するには、可能な限り設定を無効にしてください。

特に、実稼動インスタンスの場合は、次の設定を無効にします。

* 「**デバッグ情報の生成**」を無効化
* **Keep Generated Java**
* 「**マッピングされたコンテンツ**」を無効化
* **Display Source Fragments**

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Logging Configuration** 設定：

* **Log Level** および **Log File**：主要なログ設定（error.log）の場所とログレベルを定義します。`DEBUG`、`INFO`、`WARN`、`ERROR` および `FATAL` のいずれかのレベルを設定できます。

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

**Apache Sling Main Servlet** 設定：

* **Number of Calls per Request** および **Recursion Depth**：無限再帰および過度のスクリプトの呼び出しからシステムを保護します。

**Apache Sling MIME Type Service** 設定：

* **MIME Types**：プロジェクトで必要な MIME タイプをシステムに追加します。これにより、ファイルに対する `GET` 要求において、ファイル形式とアプリケーションをリンクするための適切な content-type ヘッダーを設定できます。

**Apache Sling Referrer Filter** CRX WebDAV および Apache Sling の Cross-Site Request Forgery（CSRF）に関する既知のセキュリティ問題に対応するには、リファラーフィルターを設定する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* フィルター処理する HTTP メソッド
* 空のリファラーヘッダーを使用できるかどうか
* サーバーホスト以外に許可されるサーバーのリスト

詳しくは、[「セキュリティチェックリスト」のクロスサイトのリクエスト偽造に関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。

>[!NOTE]
>
>Apache Sling Referrer Filter はクイックフィックスパッケージのインストールに依存します。

**Apache Sling Request Logger** 設定：

* 要求をログに記録する方法を定義するための様々なパラメーター。
* **Enable Request Log**：有効または無効にします。

* **Enable Access Log**：有効または無効にします。

これは [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Resource Resolver Factory** Sling リソースの解決の主要な要素を設定します。

* **Resource Search Path**：プロジェクト固有のパスを追加します（ただし、`/libs` または `/apps` は削除しないでください）。

* **Virtual URLs**：バニティー URL のマッピングを定義します。

* **URL Mappings**：エイリアスを定義します（例：`/content` から `/` へのマッピング）。

* **Mapping Location**：`/etc/map` で外面化されるマッパー設定です。

* ローカルインストール（例えば、`https://localhost:4502/system/console/jcrresolver`）を使用して、どのリソースリゾルバーがアクティブかを判断します。

詳しくは、[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution) を参照してください。

>[!CAUTION]
>
>具体的には、これらのオプションはリポジトリで設定する必要があります。
>
>そうしないと、Felix コンソールでおこなった「**URL Mappings**」に対する変更が、次回の起動時に AEM によって上書きされる可能性があります。

**Apache Sling Servlet／Script Resolver and Error Handler** Sling サーブレットとスクリプトリゾルバーには、次の複数のタスクがあります。

1. `ServletResolver` として使用され、要求を処理するために呼び出す Servlet または Script を選択します。

1. `SlingScriptResolver` として機能します。

1. エラー処理を管理します。そのためには、要求処理のサーブレット／スクリプトの解決に使用するのと同じアルゴリズムを使用してエラー処理のサーブレット／スクリプトを選択する `ErrorHandler` インターフェイスを実装します。

次のような様々なパラメーターを設定できます。

* **Execution Paths**：実行可能なスクリプトを検索するパスを表示します。特定のパスを設定することで、実行可能なスクリプトを制限できます。パスを設定しない場合は、デフォルト値（`/`=ルート）が使用され、すべてのスクリプトの実行が許可されます。

設定したパス値がスラッシュで終わる場合は、サブツリー全体が検索されます。末尾にスラッシュを指定しないと、完全一致の場合にのみスクリプトが実行されます。

* **Script User**：このオプションのプロパティでは、スクリプトの読み取りに使用するリポジトリユーザーアカウントを指定できます。アカウントを指定しない場合は、`admin` ユーザーがデフォルトで使用されます。

* **Default Extensions**：デフォルトの動作が使用される拡張子のリストです。つまり、リソースタイプの最後のパスセグメントをスクリプト名として使用できます。

**Day Commons GFX Font Helper** グラフィックのレンダリング時に、DrawText を使用してテキストを埋め込むことができます。 そのために、独自のフォントをインストールすることも可能です。

* プロジェクト固有のフォントを検索する「**Font Path**」を定義します。
例えば、`/apps/myapp/fonts` と指定します。

**Apache HTTP Components Proxy Configuration** Apache HTTP クライアントを使用するすべてのコード用のプロキシ設定です。HTTP の作成時（レプリケーション時など）に使用されます。

新しい設定を作成する際は、工場出荷時の設定に変更を加える代わりに、設定マネージャー（**https://localhost:4502/system/console/configMgr/**）を使用してこのコンポーネントの新しい工場出荷時の設定を作成してください。このプロキシ設定は、**org.apache.http.proxyconfigurator** で利用できます。

>[!NOTE]
>
>AEM 6.0 以前のリリースでは、プロキシは Day Commons HTTP Client で設定されていました。AEM 6.1 以降のリリースでは、プロキシ設定は、「Day Commons HTTP Client」設定ではなく、「Apache HTTP Components Proxy Configuration」に移動されました。

**Day CQ Antispam** 使用するスパム対策サービス （Akismet）を設定します。 次の項目を登録する必要があります。

* **プロバイダー**
* **API キー**
* **登録済みの URL**

**Adobe Granite HTML Library Manager**：クライアントライブラリ（css または js）の処理（例えば、基盤となる構造の表示形式）を制御するために設定します。

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
>「**Minify**」または「**Gzip**」の設定を変更する場合は、`/var/clientlibs` の内容も削除する必要があります。これはキャッシュバージョンの clientlibs であり、次回の要求時に再構築されます。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ HTTP Header Authentication Handler**：HTTP リクエストの基本的な認証方法に関するシステム全体の設定です。

[閉じられたユーザーグループ](/help/sites-administering/cug.md)を使用すると、（特に）以下を設定できます。

* **HTTP レルム**
* **デフォルトのログインページ**

**Day CQ Link Checker Service**：必要に応じて、次の項目を設定します。

* **Scheduler Period**：外部リンクを自動的にチェックする間隔を定義します。

* **Bad Link Tolerance Interval**：失敗した外部リンクが無効と見なされるまでの期間を指定します。
* **Link Check Override Patterns**：リンクチェックから除外するパスを定義します。

**Day CQ Link Checker Task**：単一のリンクチェッカータスク（外部リンクを確認するタスク）の設定を指定します。

* **Good Link Test Interval** および **Bad Link Test Interval で定義されている間隔をチェックします。** 

* リンクをチェックする際に外部アクセスのために必要な、インターネットアクセスおよび NTLM 用のプロキシに関連する様々なパラメーターを設定します。

**Day CQ Mail Service**：メールサーバーのホスト名とアクセスの詳細を設定します。 「メールサービスの設定」の節を参照してください。

**Day CQ MCM Newsletter**：ニュースレターで使用する様々な設定を指定します。

**Day CQ Root Mapping**：以下の項目を設定します。

* **Target Path**：「`/`」に対するリクエストのリダイレクト先を定義します。

AEM では次の 2 つの UI を使用できます。

* タッチ操作対応 UI が標準の UI です。
* 廃止されたクラシック UI も引き続き完全に機能します。

AEM ルートマッピングを使用すると、希望する UI を、インスタンスのデフォルトとして設定できます。

* タッチ操作対応 UI をデフォルトの UI にするには、**Target Path** を次のように指定します。

   ```
      /projects.html
   ```

* クラシック UI をデフォルトの UI とするには、**ターゲットパス**&#x200B;を次のように指定します。

   ```
      /welcome.html
   ```

>[!NOTE]
>
>標準インストールでは、タッチ操作向け UI がデフォルトの UI です。

**Adobe Granite SSO Authentication Handler**：シングルサインオン（SSO）の詳細を設定します。この詳細情報は、企業の作成者の設定や、LDAP との連動で必要となることが多くあります。

様々な設定プロパティがあります。

* **Path**&#x200B;この認証ハンドラーをアクティブにする対象のパス。このパラメーターを空のままにすると、認証ハンドラーは無効になります。例えば、/ というパスを指定すると、認証ハンドラーはリポジトリ全体に対して使用されます。

* **サービスランキング**
OSGi フレームワークサービスランキングの値は、このサービスの呼び出しに使用する順序を示すために使用されます。これは 
`int` 値で、値が大きいほど優先度が高くなります。
デフォルト値は `0` です。

* **Header Names**
ユーザー ID を含む可能性のあるヘッダーの名前です。

* **Cookie Names**
ユーザー ID を含む可能性のある cookie の名前です。

* **Parameter Names**
ユーザー ID を指定する可能性のある要求パラメーターの名前です。

* **ユーザーマップ**
選択したユーザーについて、HTTP リクエストから抽出されたユーザー名を、認証情報オブジェクト内の別のユーザー名に置き換えることができます。マッピングはここで定義します。ユーザー名  
`admin` がマップの両側に表示される場合、マッピングは無視されます。 「=」文字を使用する場合は、先頭に「\」を付けてエスケープする必要があります。

* **Format**
ユーザー ID を指定する際の形式を示します。次のいずれかを使用します。

   * `Basic`：ユーザー ID が HTTP Basic 認証形式でエンコードされている場合
   * `AsIs`：ユーザー ID がプレーンテキストで指定されている場合や、正規表現が適用されている値をそのまま、または正規表現として使用する必要がある場合

**Day CQ WCM Debug Filter** ページへのアクセス時に ?debug=layout などのサフィックスを使用できるので、開発時に便利です。 例えば、https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout は開発者が関心を持つ可能性のあるレイアウト情報を提供します。

* パフォーマンスとセキュリティを確保するために、実稼動インスタンスではこれを無効にします。

**Day CQ WCM Filter**：以下の項目を設定します。

* **WCM Mode ** デフォルトモードを定義します。
* オーサーインスタンスには、`edit`、`disable,preview` または `analytics` を使用できます。
その他のモードは、サイドキックからアクセスできます。またはサフィックス `?wcmmode=disabled` を使用して実稼動環境をエミュレートできます。

* パブリッシュインスタンスでは、`disabled` に設定して、その他のモードにアクセスできないようにする必要があります。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ WCM Link Checker Configurator**：以下の項目を設定します。

* **書き換え設定のリスト**：コンテンツベースのリンクチェックツール設定の場所のリストを指定します。設定は実行モードに基づくことができます。これはオーサー環境とパブリッシュ環境を区別するために重要です。それぞれの環境でリンクチェッカーの設定が異なる場合があるからです。

**Day CQ WCM Page Manager Factory** 設定：

* **ページサブツリーのアクティベーションチェック** （レプリケーション権限を持たない）ユーザーが（ページがアクティベートされていない場合でも）ページを削除または移動できるようにするため。

**Day CQ WCM Page Processor**：以下の項目を設定します。

* **パス**：システムが `jcr:Event` をトリガーする前にページの変更をリッスンする場所のリストです。

**Adobe Page Impressions Tracker**：オーサーインスタンスの場合は、次のように設定します。

* **sling.auth.requirements**：このプロパティの値を `-/libs/wcm/stats/tracker` に設定します

>[!CAUTION]
>
>この設定では、トラッキングサービスへの匿名リクエストが許可されます。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Page Statistics**：パブリッシュインスタンスの場合は、次のように設定します。

* **URL to send data**：ページ統計の追跡に使用する URL を設定します（トラッカー要求が Dispatcher を経由する場合は必須）。例えば、デフォルトは `https://localhost:4502/libs/wcm/stats/tracker` です。

* **Tracking script enabled**：ページ上の追跡スクリプトのインクルードを有効化（`true`）または無効化（`false`）します。デフォルト値は `false` です。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Version Manager**：システム内でバージョンを管理するかどうか、および管理方法を制御します。

* **Create Version on Activation**：標準インストールで有効になります。
* **Enable Purging**

* **Purge Paths**：検索アクションで検索するパス。
* **Implicit Versioning Paths**：暗黙のバージョン管理がアクティブなパス。

* **Max Version Age**：バージョンの最長有効期間（日数）。

* **Max Number Versions**：保存するバージョンの最大数。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。

**Day CQ Workflow Email Notification Service**：ワークフローから送信されるメール通知を設定します。

**CQ Rewriter HTML Parser Factory**

CQ リライターの HTML パーサーを制御します。

* **Additional Tags to Process** - パーサーで処理する HTML タグを追加または削除できます。デフォルトで処理されるタグは、A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD です。
* **キャメルケースを保持** - デフォルトでは、HTML パーサーによってキャメルケース（例：eBay）の属性が小文字（例：ebay）に変換されます。キャメルケースの属性を保持するには、これをオフにします。これは、Angular 2 などのフロントエンドフレームワークを使用する際に役立ちます。

**Day Commons JDBC Connections Pool**：コンテンツのソースとして使用される外部データベースへのアクセスを設定します。

これはファクトリ設定なので、複数のインスタンスを設定できます。

**Adobe CQ Media DPS Sessions Service**：パブリケーションで使用する DPS セッションを管理します。

具体的には、`dps.session.service.url.name`、を定義できます。デフォルトは [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions) に設定されています。

**CDN Rewriter**：AEM と CDN の間の通信では、アセットやバイナリが安全な方法でエンドユーザーに配信されるようにする必要があります。この方法では 2 つのタスクをおこないます。

* 最初（またはキャッシュ内のリソースが期限切れになった後）に、CDN を介して AEM からリソースにアクセスします。
* CDN にリソースがキャッシュされた後は、CDN にキャッシュされたリソースに安全にアクセスします。要求は AEM に送信されず、そのリソースにアクセスできるすべてのユーザーの処理は CDN でおこなわれます。

AEM は、内部アセットの URL を外部の CDN URL に書き直すリライターを提供しています。これにより、JWS 署名および有効期限を含む、CDN に渡すリンクが書き直され、アセットに安全にアクセスできるようになります。この機能は、オーサーインスタンスで使用されます。

全体的なフローは次のとおりです。

1. ユーザーが AEM で認証をおこない、アセットを含むページを要求します。
1. リクエストされたページには、`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png` に類似したアセットが含まれます
1. リライターは、リンクを、JWS 署名を含む CDN URL に変換します。
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. ユーザーのブラウザーによって、CDN サーバーにアセット要求が転送されます。
1. 要求が `cdn_sign` パラメーターと共に AEM に転送されるように、CDN を設定する必要があります。
1. 認証ハンドラーによって `cdn_sign` パラメーターが検証され、CDN にアセットが返された後、アセットがユーザーに配信されます。

次の図に、ユーザーのブラウザー、CDN および AEM の間のフローを示します。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>現在、この機能は、AEM オーサーインスタンスでのみ使用できます。

**CDNConfigServiceImpl**：CDN 設定を指定します。

CDN の書き直し機能を使用できるようにするには、com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl の設定に **CDN 配布ドメイン名**&#x200B;を入力します。

また、このサービスには、CDN 書き直しの有効化／無効化、CDN 書き直しが実行されるパスのプレフィックス、TTL 値、プロトコル（HTTP または HTTPS）など、その他の設定オプションも含まれます。

**CDNRewriter**：内部画像の URL を CDN URL に書き直すリライターです。

com.adobe.cq.cdn.rewriter.impl.CDNRewriter の&#x200B;**タグ属性**&#x200B;値は、選択した画像のリンクのみが書き直されるように定義できます。
