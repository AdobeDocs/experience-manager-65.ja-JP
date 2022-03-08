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
ht-degree: 59%

---

# OSGi 設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEMのテクノロジースタックの基本要素です。AEMの複合バンドルとその設定を制御するために使用されます。

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。**

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント ( [OSGi の仕様](https://www.osgi.org/Specifications/HomePage)) は、様々なバンドルの 1 つに含まれています。 AEMを操作する場合、このようなバンドルの設定を管理する方法がいくつかあります。参照 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を参照してください。

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
>OSGi 設定の差分ツール ( [AEMツール](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)を使用して、デフォルトの OSGi 設定のリストを表示できます。

>[!NOTE]
>
>AEM 内の機能の特定の領域では、さらに多くのバンドルが必要な場合があります。この場合、設定の詳細は、該当する機能の関連ページで確認できます。

**AEMレプリケーションイベントリスナー** 設定：

* この **実行モード**：レプリケーションイベントがリスナーに配信されます。 例えば、author と定義されている場合、これはレプリケーションを「開始」するシステムです。

* 実行モード **公開** プロジェクトコードがパブリッシュ環境でレプリケーションイベント（リバースレプリケーション）を処理する場合は、追加する必要があります。 例えば、Dispatcher を使用してパブリッシュ環境からフラッシュする場合や、他のパブリッシュインスタンスへの標準レプリケーションが発生する場合などです。

**AEM Repository Change Listener** 設定：

* この **パス**：配布準備が整ったリポジトリイベントをリッスンする場所。

**CRX Sling Client Repository** 基になるコンテンツリポジトリへのアクセスを設定します。

* この **管理者パスワード** インストール後にを変更して、 [セキュリティ](/help/sites-administering/security-checklist.md) インスタンスの
* その他の変更は必要ありません。また、リポジトリへのアクセスに影響を与える可能性があるので、注意が必要です。

**Wiki メールサービス** Wiki から送信される電子メールの設定を構成します。

**Apache Felix OSGi Management Console** 設定：

* **Plugins**：**Apache Felix Web Management Console** で最上位のメニュー項目として使用できる、メインのナビゲーション項目（コンソールプラグイン）です。それぞれ容量とリソースが必要なので、不要なものは無効にしてください。

>[!CAUTION]
>
>必ず以下を設定してください。
>
>**ユーザー名** および **パスワード**:Apache Felix Web Management Console にアクセスするための資格情報。
>最初のインストール後にパスワードを変更して、 [セキュリティ](/help/sites-administering/security-checklist.md) インスタンスの

>[!NOTE]
>
>この設定は起動時に必要なので、リポジトリが使用可能になる前に、Felix コンソールを使用して設定する必要があります。

**Apache Sling Customizable Request Data Logger** 設定：

* **ロガー名** および **ログ形式** 要求およびアクセスログの場所と形式を設定するには、次の手順に従います ( デフォルト： `request.log`) をクリックします。 このログファイルは、Web チェーンに関連するパフォーマンスやデバッグ機能を分析する際に不可欠です。
これは [Apache Sling Request Logger](#apacheslingrequestlogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/site/logging.html)に関するページを参照してください。

**Apache Sling Eventing Thread Pool** 設定：

* **Min Pool Size** および **Max Pool Size**：イベントスレッドを保持するために使用するプールのサイズ。

* **Queue Size**：プールを使い果たした場合のスレッドキューの最大サイズ。推奨される値は次のとおりです。 `-1` これにより、キューは無制限に設定されます。制限を設定すると、制限を超えた場合に損失が発生する可能性があります。

* これらの設定を変更すると、イベント数が非常に多い状況（例：AEM DAM またはワークフローの使用頻度が高い場合）におけるパフォーマンスの強化に役立ちます。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定はインスタンスのパフォーマンスに影響を及ぼす可能性があるので、変更の際は十分な理由と検討が必要です。

**Apache SlingGETサーブレット** レンダリングのいくつかの側面を設定します。

* **Auto Index**：閲覧のためのディレクトリのレンダリングを有効または無効にします。
* **Enable**（または Disable）：デフォルトのレンディション（**HTML**、**Plain Text**、**JSON**、**XML** など）を有効または無効にします。JSON を無効にしないでください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Java Script Handler** .java ファイルのコンパイルの設定を、スクリプト（サーブレット）として構成します。

特定の設定がパフォーマンスに影響を及ぼす可能性があります。可能な場合（特に、実稼動インスタンスの場合）は、それらを無効にしてください。

* **Source VM** および **Target VM**：ランタイム JVM として使用する JDK バージョンを定義します。

* 実稼動インスタンスの場合：

   * 「**Generate Debug Info**」を無効化

**Apache Sling JCR Installer** これらのパラメーターは、おそらく設定が必要ないものですが、開発やデバッグの際に知っておくと役に立ちます。 例えば、インストールフォルダーはパッケージのチェックイン／チェックアウトまたは作成に役立つ場合があります。

* **インストールフォルダー名の正規表現** および **インストールフォルダーの最大階層深度**  — インストールするリソースを検索するリポジトリフォルダーの場所と深さを指定します。ワイルドカードを使用する場合（のように）。*/install) 適切なすべての一致が検索されます。例： `/libs/sling/install` および `/libs/cq/core/install`.

* **Search Path**：インストールするリソースを jcrinstall が検索するパスのリストです。そのパスの重み付け係数を示す数値も表示されます。

**Apache Sling Job Event Handler** ジョブのスケジュール設定を管理するパラメーターを設定します。

* **再試行間隔**, **再試行の最大数**, **並列ジョブの最大数**, **待機時間の確認**&#x200B;など。

* これらの設定を変更すると、多数のジョブが存在するシナリオのパフォーマンスが向上します。例えば、AEM DAM とワークフローが多く使用されている場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定は理由なく変更しないでください。適切な検討の後にのみ変更してください。

**Apache Sling JSP Script Handler** JSP スクリプトハンドラーのパフォーマンス関連の設定を行います。 パフォーマンスを向上するには、可能な限り設定を無効にしてください。

特に、実稼動インスタンスの場合は、次の設定を無効にします。

* 「**Generate Debug Info**」を無効化
* **Keep Generated Java**
* **Mapped Content**
* **Display Source Fragments**

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Logging Configuration** 設定：

* **Log Level** および **Log File**：主要なログ設定（error.log）の場所とログレベルを定義します。レベルは、次のいずれかに設定できます。 `DEBUG`, `INFO`, `WARN`, `ERROR` および `FATAL`.

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

**Apache Sling Referrer Filter** CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ (CSRF) に関する既知のセキュリティ問題に対処するには、リファラーフィルターを設定する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* フィルター処理する HTTP メソッド
* 空のリファラーヘッダーを使用できるかどうか
* と、サーバーホストに加えて許可されるサーバーのリスト。

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

**Apache Sling Resource Resolver Factory** Sling リソース解決の中心要素を設定します。

* **リソース検索パス**(s) プロジェクト固有のパスを追加します（ただし、削除しません） `/libs` または `/apps`) をクリックします。

* **Virtual URLs**：バニティー URL のマッピングを定義します。

* **URL マッピング** エイリアスを定義するには、以下を実行します。例： `/content` から `/`.

* **マッピング場所**（で外部化されたマッパー設定） `/etc/map`.

* ローカルインストールを使用します ( 例： `https://localhost:4502/system/console/jcrresolver`) を使用して、どのリソースリゾルバーがアクティブかを判断します。

詳しくは、[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution) を参照してください。

>[!CAUTION]
>
>具体的には、これらのオプションはリポジトリで設定する必要があります。
>
>そうしないと、Felix コンソールでおこなった「**URL Mappings**」に対する変更が、次回の起動時に AEM によって上書きされる可能性があります。

**Apache Sling Servlet/Script Resolver and Error Handler** Sling Servlet と Script Resolver には、次の複数のタスクがあります。

1. `ServletResolver` として使用され、要求を処理するために呼び出す Servlet または Script を選択します。

1. これは、 `SlingScriptResolver`.

1. エラー処理を管理します。そのためには、要求処理のサーブレット／スクリプトの解決に使用するのと同じアルゴリズムを使用してエラー処理のサーブレット／スクリプトを選択する `ErrorHandler` インターフェイスを実装します。

次のような様々なパラメーターを設定できます。

* **Execution Paths**：実行可能なスクリプトを検索するパスを表示します。特定のパスを設定することで、実行可能なスクリプトを制限できます。パスが設定されていない場合は、デフォルトのが使用されます ( `/` = root) の場合は、すべてのスクリプトを実行できます。

設定したパス値がスラッシュで終わる場合は、サブツリー全体が検索されます。末尾にスラッシュを指定しないと、完全一致の場合にのみスクリプトが実行されます。

* **Script User**：このオプションのプロパティでは、スクリプトの読み取りに使用するリポジトリユーザーアカウントを指定できます。アカウントを指定しない場合は、`admin` ユーザーがデフォルトで使用されます。

* **Default Extensions**：デフォルトの動作が使用される拡張子のリストです。つまり、リソースタイプの最後のパスセグメントをスクリプト名として使用できます。

**Day Commons GFX Font Helper** グラフィックのレンダリング時に、DrawText を使用してテキストを埋め込むことができます。 そのために、独自のフォントをインストールすることも可能です。

* 次を定義： **フォントパス** プロジェクト固有のフォントを検索します。例： `/apps/myapp/fonts`.

**Apache HTTP コンポーネントプロキシ設定** Apache HTTP クライアントを使用するすべてのコードのプロキシ設定。HTTP の作成時に使用されます。例えば、レプリケーション時に。

新しい設定を作成する場合は、ファクトリ設定を変更せずに、次の場所にある Configuration Manager を使用して、このコンポーネントの新しいファクトリ設定を作成します。 **https://localhost:4502/system/console/configMgr/**. プロキシ設定は、で使用できます。 **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>AEM 6.0 以前のリリースでは、プロキシは Day Commons HTTP Client で設定されていました。AEM 6.1 以降のリリースでは、プロキシ設定は、「Day Commons HTTP Client」設定ではなく、「Apache HTTP Components Proxy Configuration」に移動されました。

**Day CQ Antispam** 使用するスパム対策サービス (Akismet) を設定します。 次の項目を登録する必要があります。

* **プロバイダー**
* **API キー**
* **登録済みの URL**

**AdobeGraniteHTMLライブラリマネージャー** クライアントライブラリ（css または js）の処理を制御するには、これを設定します。例えば、基になる構造の表示方法を含みます。

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
>次のいずれかの設定を変更する場合 **縮小** または **Gzip** また、 `/var/clientlibs`.これは clientlibs のキャッシュバージョンで、次回の要求時に再構築されます。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ HTTP Header Authentication Handler** HTTP 要求の基本認証方式のシステム全体の設定です。

[閉じられたユーザーグループ](/help/sites-administering/cug.md)を使用すると、（特に）以下を設定できます。

* **HTTP レルム**
* **デフォルトのログインページ**

**Day CQ Link Checker Service** 必要に応じて、次の項目を設定します。

* **Scheduler Period**：外部リンクを自動的にチェックする間隔を定義します。

* **Bad Link Tolerance Interval**：失敗した外部リンクが無効と見なされるまでの期間を指定します。
* **Link Check Override Patterns**：リンクチェックから除外するパスを定義します。

**Day CQ Link Checker Task** 単一のリンクチェッカータスク（外部リンクを確認するタスク）の設定を指定します。

* **Good Link Test Interval** および **Bad Link Test Interval で定義されている間隔をチェックします。** 

* リンクをチェックする際に外部アクセスのために必要な、インターネットアクセスおよび NTLM 用のプロキシに関連する様々なパラメーターを設定します。

**Day CQ Mail Service** メールサーバーのホスト名とアクセスの詳細を設定します。 メールサービスの設定の節を参照してください。

**Day CQ MCM ニュースレター** ニュースレターで使用する様々な設定を行います。

**Day CQ Root Mapping** 設定：

* **ターゲットパス** を定義します。 `/`」がリダイレクトされます。

AEM では次の 2 つの UI を使用できます。

* タッチ操作対応 UI が標準の UI です。
* 廃止されたクラシック UI も引き続き完全に機能します。

AEM ルートマッピングを使用すると、希望する UI を、インスタンスのデフォルトとして設定できます。

* タッチ操作対応 UI をデフォルトの UI にするには、 **ターゲットパス** は次を指す必要があります。

   ```
      /projects.html
   ```

* クラシック UI をデフォルトの UI にするには、 **ターゲットパス** は次を指す必要があります。

   ```
      /welcome.html
   ```

>[!NOTE]
>
>標準インストールでは、タッチ操作向け UI がデフォルトの UI です。

**AdobeGranite SSO 認証ハンドラー** シングルサインオン (SSO) の詳細を設定します。多くの場合、エンタープライズオーサーの設定で必要になります。多くの場合、LDAP と組み合わせて使用されます。

様々な設定プロパティがあります。

* **Path**&#x200B;この認証ハンドラーをアクティブにする対象のパス。このパラメーターを空のままにすると、認証ハンドラーは無効になります。例えば、/ というパスを指定すると、認証ハンドラーはリポジトリ全体に対して使用されます。

* **サービスランキング**
OSGi Framework Service Ranking 値は、このサービスの呼び出しに使用される順序を示すために使用されます。これは 
`int` 値が大きいほど、優先度が高くなります。
デフォルト値は `0` です。

* **Header Names**
ユーザー ID を含む可能性のあるヘッダーの名前です。

* **Cookie Names**
ユーザー ID を含む可能性のある cookie の名前です。

* **Parameter Names**
ユーザー ID を指定する可能性のある要求パラメーターの名前です。

* **ユーザーマップ**
選択したユーザーの場合、HTTP リクエストから抽出されたユーザー名を、credentials オブジェクト内の別のユーザー名に置き換えることができます。マッピングはここで定義します。ユーザー名 
`admin` はマップの両側に表示され、マッピングは無視されます。 「=」文字は、先頭に「\」を付けてエスケープする必要があります。

* **Format**
ユーザー ID を指定する際の形式を示します。次のいずれかを使用します。

   * `Basic`：ユーザー ID が HTTP Basic 認証形式でエンコードされている場合
   * `AsIs`：ユーザー ID がプレーンテキストで指定されている場合や、正規表現が適用されている値をそのまま、または正規表現として使用する必要がある場合

**Day CQ WCM Debug Filter** ページへのアクセス時に？debug=layout などのサフィックスを使用できるので、開発時に便利です。 例えば、https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layoutは開発者が興味を持つ可能性のあるレイアウト情報を提供します。

* パフォーマンスとセキュリティを確保するために、実稼動インスタンスではこれを無効にします。

**Day CQ WCM Filter** 設定：

* **WCM Mode **：デフォルトのモードを定義します。
* オーサーインスタンスでは、次のようになります。 `edit`, `disable,preview` または `analytics`.
その他のモードは、サイドキックまたはサフィックスからアクセスできます `?wcmmode=disabled` を使用して実稼動環境をエミュレートできます。

* パブリッシュインスタンスでは、`disabled` に設定して、その他のモードにアクセスできないようにする必要があります。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ WCM Link Checker Configurator** 設定：

* **書き換え設定のリスト**：コンテンツベースのリンクチェックツール設定の場所のリストを指定します。設定は実行モードに基づくことができます。これはオーサー環境とパブリッシュ環境を区別するために重要です。それぞれの環境でリンクチェッカーの設定が異なる場合があるからです。

**Day CQ WCM Page Manager Factory** 設定：

* **ページサブツリーのアクティベーションチェック** （レプリケーション権限を持たない）ユーザーが（ページがアクティベートされていない場合でも）ページを削除または移動できるようにするため。

**Day CQ WCM Page Processor** 設定：

* **パス**：システムが `jcr:Event` をトリガーする前にページの変更をリッスンする場所のリストです。

**Adobeページインプレッショントラッカー** オーサーインスタンスの場合は、次のように設定します。

* **sling.auth.requirements**:このプロパティの値をに設定します。 `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>この設定では、トラッキングサービスへの匿名リクエストが許可されます。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Page Statistics** パブリッシュインスタンスの場合は、次の設定をおこないます。

* **URL to send data**：ページ統計の追跡に使用する URL を設定します（トラッカー要求が Dispatcher を経由する場合は必須）。例えば、デフォルトは `https://localhost:4502/libs/wcm/stats/tracker` です。

* **Tracking script enabled**：ページ上の追跡スクリプトのインクルードを有効化（`true`）または無効化（`false`）します。デフォルト値は `false` です。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Version Manager** システム内でバージョンを管理するかどうか、および管理する方法を制御します。

* **Create Version on Activation**：標準インストールで有効になります。
* **Enable Purging**

* **Purge Paths**：検索アクションで検索するパス。
* **Implicit Versioning Paths**：暗黙のバージョン管理がアクティブなパス。

* **Max Version Age**：バージョンの最長有効期間（日数）。

* **Max Number Versions**：保存するバージョンの最大数。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。

**Day CQ Workflow Email Notification Service** ワークフローから送信される通知の電子メールを設定します。

**CQ Rewriter HTML Parser Factory**

CQ リライターの HTML パーサーを制御します。

* **Additional Tags to Process** - パーサーで処理する HTML タグを追加または削除できます。デフォルトで処理されるタグは、A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD です。
* **キャメルケースを保持**  — デフォルトでは、HTMLパーサはキャメルケース（eBay など）の属性を小文字（ebay など）に変換します。 キャメルケースの属性を保持するには、これをオフにします。これは、Angular 2 などのフロントエンドフレームワークを使用する際に役立ちます。

**Day Commons JDBC Connections Pool** コンテンツのソースとして使用される外部データベースへのアクセスを設定します。

これはファクトリ設定なので、複数のインスタンスを設定できます。

**Adobe CQ Media DPS Sessions Service** パブリケーションで使用する DPS セッションを管理します。

具体的には、`dps.session.service.url.name`、  を定義できます。デフォルトは [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions) に設定されています。

**CDN Rewriter** アセットやバイナリが安全な方法でエンドユーザーに配信されるように、AEMと CDN 間の通信を確保する必要があります。 この方法では 2 つのタスクをおこないます。

* 最初（またはキャッシュ内のリソースが期限切れになった後）に、CDN を介して AEM からリソースにアクセスします。
* CDN にリソースがキャッシュされた後は、CDN にキャッシュされたリソースに安全にアクセスします。要求は AEM に送信されず、そのリソースにアクセスできるすべてのユーザーの処理は CDN でおこなわれます。

AEM は、内部アセットの URL を外部の CDN URL に書き直すリライターを提供しています。これにより、JWS 署名および有効期限を含む、CDN に渡すリンクが書き直され、アセットに安全にアクセスできるようになります。この機能は、オーサーインスタンスで使用されます。

全体的なフローは次のとおりです。

1. ユーザーが AEM で認証をおこない、アセットを含むページを要求します。
1. リクエストされたページには、 `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. リライターは、リンクを JWS 署名を含む CDN URL に変換します。
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. ユーザーのブラウザーによって、CDN サーバーにアセット要求が転送されます。
1. 要求が `cdn_sign` パラメーターと共に AEM に転送されるように、CDN を設定する必要があります。
1. 認証ハンドラーによって `cdn_sign` パラメーターが検証され、CDN にアセットが返された後、アセットがユーザーに配信されます。

次の図に、ユーザーのブラウザー、CDN および AEM の間のフローを示します。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>現在、この機能は、AEM オーサーインスタンスでのみ使用できます。

**CDNConfigServiceImpl** CDN 設定を提供します

CDN の書き換え機能は、 **CDN 配布ドメイン名** com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl の設定で、

また、このサービスには、CDN 書き直しの有効化／無効化、CDN 書き直しが実行されるパスのプレフィックス、TTL 値、プロトコル（HTTP または HTTPS）など、その他の設定オプションも含まれます。

**CDNRewriter** 内部画像 URL を CDN URL に書き換えるためのリライター

この **タグ属性** com.adobe.cq.cdn.rewriter.impl.CDNRewriter の値を定義して、選択した画像リンクのみが書き換えられるようにすることができます。
