---
title: OSGi 設定
seo-title: OSGi Configuration Settings
description: この記事では、プロジェクトの実装に関連する OSGi 設定（バンドルに従って一覧表示）について詳しく説明します。 このリストはガイドラインとして機能し、完全なものではありません。
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
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 47%

---

# OSGi 設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEM の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

OSGi &quot;*は、小さく、再利用可能で、協調的なコンポーネントを使用してアプリケーションを構築できる、標準化されたプリミティブを提供します。これらのコンポーネントは、アプリケーションに組み込み、デプロイできます*&quot;.

この機能により、バンドルを個別に停止、インストール、開始できるので、バンドルを容易に管理できます。 相互依存関係は自動的に処理されます。各 OSGi コンポーネント（[OSGi の仕様](https://www.osgi.org/Specifications/HomePage)を参照）は、各種バンドルの 1 つに含まれています。AEMを操作する場合、このようなバンドルの設定を管理する方法はいくつかあります。参照 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を参照してください。

次の OSGi 設定（バンドルに従ったリスト）は、プロジェクトの実装に関連しています。すべての設定に調整が必要なわけではなく、一部の設定は AEM の動作を説明する目的で言及されています。

>[!CAUTION]
>
>このリストは、ガイドラインとしての役割を果たすことを目的としており、すべてを網羅したものではありません。 一部のバンドルが一覧表示されるわけではありません。また、存在する一部のバンドルのすべてのパラメータも表示されません。
>
>必要な設定は、プロジェクトによって異なります。
>
>使用する値とパラメーターの詳細については、 Web コンソールを参照してください。

>[!NOTE]
>
>OSGi 設定の差分ツール（[AEM ツール](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=en)の一部）を使用して、デフォルトの OSGi 設定のリストを表示できます。

>[!NOTE]
>
>AEM 内の機能の特定の領域では、さらに多くのバンドルが必要な場合があります。この場合、設定の詳細は、該当する機能の関連ページで確認できます。

**AEM レプリケーションイベントリスナー**&#x200B;設定：

* この **実行モード**：レプリケーションイベントがリスナーに配布されます。 例えば、author として定義された場合、レプリケーションを「開始」するシステムです。

* 実行モードの追加 **公開** プロジェクトコードがパブリッシュ環境でレプリケーションイベント（リバースレプリケーション）を処理する場合。 例えば、Dispatcher を使用してパブリッシュ環境からフラッシュする場合や、他のパブリッシュインスタンスへの標準レプリケーションが発生する場合などです。

**AEM リポジトリ変更リスナー**&#x200B;設定：

* **パス**：配布準備が整ったリポジトリイベントをリッスンする場所

**CRX Sling クライアントリポジトリ**：基になるコンテンツリポジトリへのアクセスを設定します。

* **管理者パスワード**&#x200B;をインストール後に変更して、インスタンスの [セキュリティ](/help/sites-administering/security-checklist.md) を確保してください。
* その他の変更は必要ありません。また、リポジトリへのアクセスに影響を与える可能性があるので、注意が必要です。

**Apache Felix OSGi 管理コンソール**&#x200B;設定：

* **プラグイン**、 **Apache Felix Web Management Console** を最上位のメニュー項目として使用する。 各にはスペースとリソースが必要なので、不要な項目を無効にします。

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
これはとペアになっています [Apache Sling Request Logger](#apacheslingrequestlogger).

詳しくは、 [AEM Logging](/help/sites-deploying/configure-logging.md) および [Sling Logging](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Eventing Thread Pool** 設定：

* **Min Pool Size** および **Max Pool Size**：イベントスレッドを保持するために使用するプールのサイズ。

* **Queue Size**：プールを使い果たした場合のスレッドキューの最大サイズ。推奨される値は次のとおりです。 `-1` キューを無制限に設定するからです。 制限を設定すると、制限を超えた場合に損失が発生する可能性があります。

* これらの設定を変更すると、多数のイベントが発生する状況でのパフォーマンスが向上します。例えば、AEM DAM やワークフローの使用量が多い場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定はインスタンスのパフォーマンスに影響を及ぼす可能性があるので、変更の際は十分な理由と検討が必要です。

**Apache Sling GET Servlet**：レンダリングの一部の要素を設定します。

* **Auto Index**：閲覧のためのディレクトリのレンダリングを有効または無効にします。
* **有効にする** デフォルトのレンディション ( **HTML**, **プレーンテキスト**, **JSON**&#x200B;または **XML**.
JSON を無効にしないでください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling JavaScript Handler** .java ファイルのコンパイルの設定を、スクリプト（サーブレット）として構成します。

特定の設定がパフォーマンスに影響を与える場合があります。 これらの設定は、可能な限り（特に実稼動インスタンスの場合）無効にします。

* **ソース VM** および **ターゲット VM**：ランタイム JVM として使用する JDK バージョンを定義します。

* 本番インスタンスの場合：

   * 「**デバッグ情報の生成**」を無効化

**Apache Sling JCR Installer**：多くの場合、これらのパラメーターの設定は必要ありませんが、設定を理解しておくと開発時やデバッグ時に役立ちます。例えば、インストールフォルダーは、チェックインやチェックアウト、パッケージの作成に役立ちます。

* **Installation folders name regexp** および **Max hierarchy depth of install folders**：インストールするリソースを検索するリポジトリフォルダーとその階層の深さを指定します。ワイルドカードを&#42;/install) 適切なすべての一致が検索されます。例： `/libs/sling/install` および `/libs/cq/core/install`.

* **Search Path**：インストールするリソースを jcrinstall が検索するパスのリストです。そのパスの重み付け係数を示す数値も表示されます。

**Apache Sling Job Event Handler**：ジョブのスケジュール設定を管理するパラメーターを設定します。

* **再試行間隔**, **再試行の最大数**, **並列ジョブの最大数**, **待機時間の確認**&#x200B;など。

* これらの設定を変更すると、多数のジョブが存在するシナリオのパフォーマンスが向上します。例えば、AEM DAM とワークフローの使用頻度が高い場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定は理由なく変更しないでください。十分に検討してから変更してください。

**Apache Sling JSP Script Handler**：JSP スクリプトハンドラーのパフォーマンス関連の設定を行います。パフォーマンスを向上させるには、できるだけ無効にする必要があります。

特に、本番インスタンスの場合は、次の手順に従います。

* 「**デバッグ情報の生成**」を無効化
* 無効 **生成済み Java™を保持**
* 「**マッピングされたコンテンツ**」を無効化
* 無効 **ソースフラグメントを表示**

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Logging Configuration** 設定：

* **Log Level** および **Log File**：主要なログ設定（error.log）の場所とログレベルを定義します。レベルは、次のいずれかに設定できます。 `DEBUG`, `INFO`, `WARN`, `ERROR`、および `FATAL`.

* **ログファイルの数** および **ログファイルのしきい値** ：ログファイルのサイズとバージョンの回転を定義します。

* **メッセージパターン** ログメッセージの形式を定義します。

詳しくは、 [AEM Logging](/help/sites-deploying/configure-logging.md#global-logging) および [Sling Logging](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Logging Logger Configuration（ファクトリ設定）** 設定：

* **Log Level**、**Log File** および **Message Format**：ログファイルとメッセージの詳細を定義します。

* **Logger**：カテゴリを定義します（例：com.day.cq のログのみ）。

* 次を使用： **ファクトリ設定**&#x200B;を使用すると、必要な様々なログレベルやカテゴリに応じて、任意の数の設定を追加できます。
* このような設定は開発時に役立ちます。例えば、特定のサービスのTRACEメッセージを特定のログファイルに記録する場合などです。
* このような設定は、実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個々のログファイルに記録して、監視を容易にする場合などです。

詳しくは、 [AEM Logging](/help/sites-deploying/configure-logging.md) および [Sling Logging](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Logging Writer Configuration（ファクトリ設定）** 設定：

* **Log File**：ログファイルの有無を定義します。
* **Number of Log Files**：バージョンのローテーションを定義します。

* このライターは、 **Apache Sling Logging Logger Configuration** 設定。

* このような設定は開発時に役立ちます。例えば、特定のサービスのTRACEメッセージを特定のログファイルに記録する場合などです。
* このような設定は、実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個々のログファイルに記録して、監視を容易にする場合などです。

詳しくは、 [AEM Logging](/help/sites-deploying/configure-logging.md) および [Sling Logging](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Main Servlet** 設定：

* **Number of Calls per Request** および **Recursion Depth**：無限再帰および過度のスクリプトの呼び出しからシステムを保護します。

**Apache Sling MIME Type Service** 設定：

* **MIME タイプ** プロジェクトで必要なタイプをシステムに追加する場合。 これにより、 `GET` ファイルに対して、ファイルタイプとアプリケーションをリンクするための正しい content-type ヘッダーを設定するようリクエストします。

**Apache Sling Referrer Filter** CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ (CSRF) に関する既知のセキュリティ問題に対処するには、リファラーフィルターを設定する必要があります。

リファラーフィルターサービスは、次の設定が可能な OSGi サービスです。

* どの http メソッドをフィルターするか
* 空のリファラーヘッダーを使用できるかどうか
* サーバーホスト以外に許可されるサーバーのリスト

詳しくは、[「セキュリティチェックリスト」のクロスサイトのリクエスト偽造に関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。

>[!NOTE]
>
>Apache Sling Referrer Filter は、クイックフィックスパッケージのインストールによって異なります。

**Apache Sling Request Logger** 設定：

* 要求をログに記録する方法を定義するための様々なパラメーター。
* **リクエストログを有効にする**、を有効または無効にします。

* **アクセスログを有効にする**、を有効または無効にします。

とペア [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

詳しくは、 [AEM Logging](/help/sites-deploying/configure-logging.md) および [Sling Logging](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Resource Resolver Factory**：Sling リソースの解決の主要な要素を設定します。

* **リソース検索パス**、プロジェクト固有のパスを追加します（ただし、削除はしません）。 `/libs` または `/apps`) をクリックします。

* **Virtual URLs**：バニティー URL のマッピングを定義します。

* **URL マッピング** エイリアスを定義する。例： `/content` から `/`.

* **Mapping Location**：`/etc/map` で外面化されるマッパー設定です。

* ローカルインストール（例えば、`https://localhost:4502/system/console/jcrresolver`）を使用して、どのリソースリゾルバーがアクティブかを判断します。

詳しくは、 [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>これらのオプションをリポジトリで設定します。
>
>それ以外の場合は、 **URL マッピング** Felix コンソールを使用すると、次回の起動時にAEMによって上書きされる場合があります。

**Apache Sling Servlet／Script Resolver and Error Handler** Sling サーブレットとスクリプトリゾルバーには、次の複数のタスクがあります。

1. `ServletResolver` として使用され、要求を処理するために呼び出す Servlet または Script を選択します。

1. `SlingScriptResolver` として機能します。

1. エラー処理を管理します。そのためには、要求処理のサーブレット／スクリプトの解決に使用するのと同じアルゴリズムを使用してエラー処理のサーブレット／スクリプトを選択する `ErrorHandler` インターフェイスを実装します。

次のような様々なパラメーターを設定できます。

* **実行パス**  — 実行可能スクリプトを検索するパスをリストします。 特定のパスを設定することで、実行可能なスクリプトを制限できます。 パスが設定されていない場合は、デフォルトのが使用されます ( `/` = root) で、すべてのスクリプトを実行できます。
設定されたパス値がスラッシュで終わる場合、サブツリー全体が検索されます。 末尾にスラッシュを付けないと、スクリプトは完全に一致する場合にのみ実行されます。

* **スクリプトユーザ**  — このオプションのプロパティは、スクリプトの読み取りに使用するリポジトリユーザーアカウントを指定できます。 アカウントが指定されていない場合、 `admin` ユーザーはデフォルトで使用されています。

* **デフォルトの拡張機能**  — デフォルトの動作が使用される拡張機能のリスト。 リソースタイプの最後のパスセグメントは、スクリプト名として使用できます。

**Apache HTTP コンポーネントプロキシ設定** - Apache HTTP クライアントを使用するすべてのコードのプロキシ設定。HTTP の作成時に使用されます。 例えば、レプリケーション時などです。

設定を作成する際は、ファクトリ設定を変更しないでください。 代わりに、次の場所にある設定マネージャーを使用して、このコンポーネントのファクトリ設定を作成します。 **https://localhost:4502/system/console/configMgr/**. このプロキシ設定は、**org.apache.http.proxyconfigurator** で利用できます。

>[!NOTE]
>
>AEM 6.0 以前のリリースでは、プロキシは Day Commons HTTP Client で設定されていました。 AEM 6.1 以降のリリースでは、プロキシ設定は「Day Commons HTTP Client」設定ではなく「Apache HTTP Components Proxy Configuration」に移動されました。

**Day CQ Antispam**：使用するスパム対策サービス （Akismet）を設定します。この機能を使用するには、以下を登録する必要があります。

* **プロバイダー**
* **API キー**
* **登録済みの URL**

**AdobeGraniteHTMLライブラリマネージャー** を設定して、基になる構造の表示方法など、クライアントライブラリ（css または js）の処理を制御します。

* 本番インスタンスの場合：

   * 有効 **縮小** （CRLF 文字と空白文字を削除）。
   * 有効 **Gzip** （1 回の要求でファイルを gzip で圧縮してアクセスできるようにする）。
   * 無効 **デバッグ**
   * 無効 **タイミング**

* JS 開発の場合（特に Firebugging/デバッグの場合）:

   * 無効 **縮小**
   * 有効 **デバッグ** を使用して、デバッグ用にファイルを分割し、firebug と共に使用します。
   * 有効 **タイミング** タイミングに興味があれば
   * 有効 **デバッグ** コンソールを使用して、JS コンソールのログメッセージを確認します。

>[!CAUTION]
>
>次のいずれかの設定を変更する場合 **縮小** または **Gzip**、clientlibs キャッシュのコンテンツを削除します。 詳しくは、 [ナレッジベース記事](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=en) 」を参照してください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ HTTP Header Authentication Handler**：HTTP リクエストの基本的な認証方法に関するシステム全体の設定です。

を使用する場合 [閉じられたユーザーグループ](/help/sites-administering/cug.md)を使用すると、次の設定を行うことができます。

* **HTTP 領域**
* **デフォルトのログインページ**

**Day CQ Link Checker Service**：必要に応じて、次の項目を設定します。

* **Scheduler Period**：外部リンクを自動的にチェックする間隔を定義します。

* チェック **不正なリンク許容間隔** 失敗した外部リンクが無効と見なされるまでの期間。
* **リンクチェック上書きパターン**：リンクチェックから除外するパスを定義します。

**Day CQ Link Checker Task**：単一のリンクチェッカータスク（外部リンクを確認するタスク）の設定を指定します。

* **Good Link Test Interval** および **Bad Link Test Interval で定義されている間隔をチェックします。** 

* リンクをチェックする際に外部アクセスのために必要な、インターネットアクセスおよび NTLM 用のプロキシに関連する様々なパラメーターを設定します。

**Day CQ Mail Service**：メールサーバーのホスト名とアクセスの詳細を設定します。メールサービスの設定の節を参照してください。

**Day CQ MCM Newsletter**：ニュースレターで使用する様々な設定を指定します。

**Day CQ Root Mapping**：以下の項目を設定します。

* **ターゲットパス** を定義します。 `/`」はにリダイレクトされます。

AEM では次の 2 つの UI を使用できます。

* タッチ操作対応 UI が標準の UI です。
* 非推奨のクラシック UI も引き続き問題なく機能します

AEM ルートマッピングを使用すると、希望する UI を、インスタンスのデフォルトとして設定できます。

* タッチ操作対応 UI をデフォルトの UI にするには、 **ターゲットパス** は次を指す必要があります。

   ```shell
      /projects.html
   ```

* クラシック UI をデフォルトの UI にするには、 **ターゲットパス** は次を指す必要があります。

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>標準インストールでは、タッチ操作向け UI がデフォルトの UI です。

**AdobeGranite SSO 認証ハンドラー** - SSO（シングルサインオン）の詳細を設定します。 これらの詳細は、多くの場合、エンタープライズオーサー設定で必要になります。多くの場合、LDAP で必要です。

様々な設定プロパティがあります。

* **パス**
この認証ハンドラーがアクティブなパス。 このパラメーターが空のままの場合、認証ハンドラーは無効になります。 例えば、パス/を指定すると、認証ハンドラーがリポジトリ全体に使用されます。

* **サービスランキング**
OSGi Framework Service Ranking 値は、このサービスの呼び出しに使用される順序を示すために使用されます。 この値は 
`int` 値で、値が大きいほど優先度が高くなります。
デフォルト値は `0` です。

* **ヘッダー名**
ユーザー ID を含む可能性のあるヘッダーの名前。

* **cookie 名**
ユーザー ID を含む可能性のある Cookie の名前。

* **パラメーター名**
ユーザー ID を提供する可能性のあるリクエストパラメーターの名前。

* **User Map**：選択したユーザーについて、HTTP リクエストから抽出されたユーザー名を、認証情報オブジェクト内の別のユーザー名に置き換えることができます。マッピングはここで定義します。ユーザー名  
`admin` はマップのどちらかの側に表示され、マッピングは無視されます。 「=」文字は、先頭に「\」を付けてエスケープする必要があります。

* **Format**：ユーザー ID を指定する際の形式を示します。次のいずれかを使用します。

   * `Basic`：ユーザー ID が HTTP Basic 認証形式でエンコードされている場合
   * `AsIs`：ユーザー ID がプレーンテキストで指定されている場合や、正規表現が適用されている値をそのまま、または正規表現として使用する必要がある場合

**Day CQ WCM Debug Filter**：ページへのアクセス時に ?debug=layout などのサフィックスを使用できるので、開発時に便利です。例えば、https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layoutは、開発者が興味を持つ可能性のあるレイアウト情報を提供します。

* パフォーマンスとセキュリティを確保するには、本番インスタンスでを無効にします。

**Day CQ WCM Filter**：以下の項目を設定します。

* **WCM モード** をクリックしてデフォルトのモードを定義します。
* オーサーインスタンスでは、このモードは `edit`, `disable,preview`または `analytics`.
その他のモードは、サイドキックからアクセスできます。またはサフィックス `?wcmmode=disabled` を使用して実稼動環境をエミュレートできます。

* パブリッシュインスタンスでは、このモードを `disabled` をクリックして、他のモードにアクセスできないようにします。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ WCM Link Checker Configurator**：以下の項目を設定します。

* **書き換え設定のリスト** ：コンテンツベースのリンクチェッカー設定の場所のリストを指定します。 設定は、実行モードに基づいておこなうことができます。 リンクチェッカーの設定が異なる場合があるので、この事実はオーサー環境とパブリッシュ環境を区別するために重要です。

**Day CQ WCM Page Manager Factory**：以下の項目を設定します。

* **ページサブツリーのアクティベーションチェック**：（レプリケーション権限を持たない）ユーザーが（ページがアクティベートされていない場合でも）ページを削除または移動できるかをチェックします。

**Day CQ WCM Page Processor**：以下の項目を設定します。

* **パス**：システムが `jcr:Event` をトリガーする前にページの変更をリッスンする場所のリストです。

**Adobeページインプレッショントラッカー** オーサーインスタンスの場合は、次のようにを設定します。

* **sling.auth.requirements**：このプロパティの値を `-/libs/wcm/stats/tracker` に設定します

>[!CAUTION]
>
>この設定により、トラッキングサービスに対する匿名リクエストが許可されます。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Page Statistics**：パブリッシュインスタンスの場合は、次のように設定します。

* **データを送信する URL** ページ統計の追跡に使用する URL を設定するには（トラッカーリクエストが Dispatcher を通過する場合は不可欠です）、例えば、デフォルトは `https://localhost:4502/libs/wcm/stats/tracker`.

* **Tracking script enabled**：ページ上の追跡スクリプトのインクルードを有効化（`true`）または無効化（`false`）します。デフォルト値は `false` です。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Version Manager**：システム内でバージョンを管理するかどうか、および管理方法を制御します。

* **Create Version on Activation**：標準インストールで有効になります。
* **Enable Purging**

* **パージパス**：検索アクションで検索するパス。
* **Implicit Versioning Paths**：暗黙のバージョン管理がアクティブなパス。

* **Max Version Age**：バージョンの最長有効期間（日数）。

* **Max Number Versions**：保存するバージョンの最大数。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。

**Day CQ Workflow Email Notification Service**：ワークフローから送信されるメール通知を設定します。

**CQ RewriterHTMLパーサーファクトリ**

CQ リライターのHTMLパーサーを制御します。

* **処理する追加のタグ**  — パーサーで処理するHTMLタグを追加または削除できます。 デフォルトでは、次のタグが処理されます。A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD
* **キャメルケースを保持**  — デフォルトでは、HTMLパーサーはキャメルケースで属性を変換します ( 例えば、 `eBay`) を小文字 ( 例： `ebay`) をクリックします。 この設定をオフにして、キャメルケースの属性を保持することができます。 この設定は、Angular2 などのフロントエンドフレームワークを使用する場合に役立ちます。

**Day Commons JDBC Connections Pool**：コンテンツのソースとして使用される外部データベースへのアクセスを設定します。

ファクトリ設定のため、複数のインスタンスを設定できます。

**CDN Rewriter** アセットやバイナリが安全な方法でエンドユーザーに配信されるように、AEMと CDN 間の通信を確保する必要があります。 このプロセスには、次の 2 つのタスクが含まれます。

* CDN を介して（またはキャッシュで期限切れになった後に）AEMからリソースに初めてアクセスする。
* リソースが CDN にキャッシュされた後はAEMに送信されず、そのリソースにアクセスできるすべてのユーザーは CDN から提供される必要があるので、CDN にキャッシュされたリソースに安全にアクセスできます。

AEMは、内部アセットの URL を外部 CDN の URL に書き換えるリライターを提供します。 JWS 署名を含む CDN に渡されるリンクを書き換え、アセットに安全にアクセスできるようにするための有効期限を設定します。 この機能は、オーサーインスタンスで使用されます。

全体的なフローは次のとおりです。

1. ユーザーがAEMで認証し、アセットを含むページを要求します。
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
>この機能は、AEMオーサーインスタンスに対してのみ有効です。

**CDNConfigServiceImpl**：CDN 設定を指定します。

CDN の書き直し機能を使用できるようにするには、com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl の設定に **CDN 配布ドメイン名**&#x200B;を入力します。

また、このサービスには、CDN 書き直しの有効化／無効化、CDN 書き直しが実行されるパスのプレフィックス、TTL 値、プロトコル（HTTP または HTTPS）など、その他の設定オプションも含まれます。

**CDNRewriter**：内部画像の URL を CDN URL に書き直すリライターです。

com.adobe.cq.cdn.rewriter.impl.CDNRewriter の&#x200B;**タグ属性**&#x200B;値は、選択した画像のリンクのみが書き直されるように定義できます。
