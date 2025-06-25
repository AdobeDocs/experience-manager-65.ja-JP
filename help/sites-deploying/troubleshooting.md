---
title: AEM のインストールに関する問題のトラブルシューティング
description: この記事では、AEM で発生する可能性のあるインストールの問題について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: ht
source-wordcount: '1182'
ht-degree: 100%

---

# AEM のインストールに関する問題のトラブルシューティング{#troubleshooting}

このセクションでは、トラブルシューティングに利用できるログに関する詳細情報と、AEM で発生する可能性のあるいくつかの問題について説明します。

## オーサーパフォーマンスのトラブルシューティング {#troubleshoot-author-performance}

パフォーマンスが低いオーサーインスタンスの分析は、複雑になる場合があります。最初のステップとして、パフォーマンスが低下しているテクノロジースタックのレベルを把握する必要があります。

以下のフローチャートはボトルネックを絞り込む手引きになります。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本的な最適化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## ログファイルと監査ログの設定 {#configuring-log-files-and-audit-logs}

AEM が記録する詳細なログは、インストールに関する問題のトラブルシューティング用に設定することができます。詳しくは、[監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)の節を参照してください。

## Verbose オプションの使用 {#using-the-verbose-option}

AEM WCM の起動時に、コマンドラインに次のように –v（verbose）オプションを追加できます。java -jar cq-wcm-quickstart-&lt;version>.jar -v

verbose オプションを指定するとコンソールに Quickstart ログの出力が表示されるので、その情報をトラブルシューティングに利用できます。

## 一般的なインストールの問題 {#common-installation-issues}

以下のセクションでは、インストールに関するいくつかの問題とその解決策について説明します。

### Quickstart jar をダブルクリックしても何も起きないか、jar ファイルが別のプログラム（アーカイブマネージャーなど）で開く {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

この問題は、通常、拡張子が.jar のファイルを開くためのオペレーティングシステムのデスクトップ環境の設定に問題があることを示しています。Java™ がインストールされていないか、サポートされていないバージョンの Java™ を使用していることを示している場合もあります。

jar ファイルは汎用の ZIP 形式を使用しているので、一部のアーカイブプログラムによって、jar ファイルをアーカイブファイルとして開くように自動的にデスクトップが設定されることがあります。

トラブルシューティングを行うには、次の手順を実施します。

* Java™ バージョン 1.6 以降がインストールされていることを再確認します。
* AEM WCM Quickstart でコンテキストメニューを使用（通常はマウスの右クリック）し、「プログラムから開く」を選択します。
* Java™ または Sun Java™ が表示されているかを確認し、それを使用して AEM WCM を実行します。複数のバージョンの Java™ がインストールされている場合は、サポートされているバージョンを選択します。

  この時点で成功した場合、選択したプログラムを常に使用して .jar ファイルを実行するためのオプションが表示されるので、そのオプションを選択します。これで、ダブルクリックによって起動できるようになります。

* サポートされている Java™ バージョンを再インストールすると、正しい関連付けが復元される場合があります。
* このドキュメントで前述したように、コマンドラインまたは起動／停止スクリプトを使用して、常に CRX を実行することができます。

### CRX で実行中のアプリケーションでメモリ不足エラーが発生する {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>[メモリの問題の分析](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-17482)も参照してください。


CRX 自体は、少ないメモリ使用量で動作します。CRX 内で実行するアプリケーションが大きなメモリを必要とする場合や、メモリ負荷の高い操作（大規模なトランザクションなど）を要求する場合、CRX が稼動する JVM インスタンスを適切なメモリ設定で起動する必要があります。

Java™ コマンドオプションを使用して、JVM のメモリ設定を定義します（例えば、java -Xmx512m -jar crx&amp;ast;.jar の場合、ヒープサイズが 512 MB に設定されます）。

コマンドラインから AEM WCM を起動する際に、メモリ設定オプションを指定します。AEM WCM 起動／停止スクリプトまたは AEM WCM スタートアップの管理用カスタムスクリプトを修正して、必要なメモリ設定を定義することもできます。

既にヒープサイズを 512 MB に定義している場合、次の方法でヒープダンプを作成してメモリの問題を詳細に分析することができます。

メモリ不足の際にヒープダンプを自動的に作成するには、次のコマンドを使用します。

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar *.jar

このメソッドによって、プロセスがメモリ不足になったときは常にヒープダンプファイル（**java_...hprof**）が生成されます。ヒープダンプが生成された後も、プロセスが引き続き実行される場合があります。

多くの場合、問題を分析するには、一定期間にわたって収集された 3 つのヒープダンプファイルが必要になります。

* エラー発生前
* エラー発生中 1
* エラー発生中 2
* *イベント解決後の情報収集もお勧めします。*

これらを比較して、変更やオブジェクトでメモリがどのように使用されているかを確認できます。

>[!NOTE]
>
>このような情報を定期的に収集している場合、またはヒープダンプを読み取った経験がある場合は、ヒープダンプファイルが 1 つあれば問題を適切に分析できます。

### AEM Quickstart をダブルクリックした後に、ブラウザーで AEM のようこそ画面が表示されない {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

特定の状況で、リポジトリ自体が正常に実行されているにもかかわらず、AEM WCM のようこそ画面が自動的に表示されない場合があります。この問題は、オペレーティングシステムの設定、ブラウザーの設定などの要因が考えられます。

通常の症状は、AEM WCM Quickstart ウィンドウに「AEM WCM を起動中、サーバーの起動を待機中」と表示されます。このメッセージが比較的長い時間表示される場合は、AEM WCM URL をブラウザーウィンドウに手動で入力してください。その際には、デフォルトの 4502 ポートまたはインスタンスが稼動しているポートを使用します（例：http://localhost:4502/）。

また、ブラウザーが起動しない原因がログによってわかることがあります。

AEM WCM Quickstart ウィンドウに「AEM WCM が http://localhost:port/ で実行中です」というメッセージが表示され、ブラウザーが自動的に起動しない場合もあります。この場合、AEM WCM クイックスタートウィンドウで URL（ハイパーリンク）をクリックするか、ブラウザーに URL を手動で入力します。

その他のエラーが発生する場合は、ログをチェックして状況を確認してください。

### Java™ 11 で web サイトが読み込まれない、または断続的に失敗する {#the-website-does-not-load-or-fails-intermittently-with-java11}

Java™ 11 上で AEM 6.5 を実行している場合、web サイトの読み込みまたは断続的な失敗が発生する可能性がある既知の問題があります。

この問題が発生する場合は、次の手順を実行します。

1. `crx-quickstart/conf/` フォルダー下の `sling.properties` ファイルを開きます。
1. 次の行を探します。

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 以下のように置換します。

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. インスタンスを再起動します。

## アプリケーションサーバーを使用したインストールのトラブルシューティング {#troubleshooting-installations-with-an-application-server}

### geometrixx-outdoor ページのリクエスト時に「Page Not Found」が返される {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**WebLogic 10.3.5 および JBoss® 5.1 に適用**

geometrixx-outdoors/en ページを要求すると 404（Page Not Found）が返される場合は、これらの特定のアプリケーションサーバーに必要になる、sling.properties ファイルの追加の sling プロパティを設定しているかを再確認してください。

詳しくは、*AEM Web アプリケーションのデプロイ*&#x200B;の手順を参照してください。

### 応答ヘッダーサイズが 4 KB を超える場合がある {#response-header-size-can-be-greater-than-kb}

Web サーバーが AEM HTTP 応答ヘッダーのサイズを処理できないときに 502 エラーが返されることがあります。AEM は、4 KB を超えるサイズの Cookie を含む HTTP 応答ヘッダーを生成できます。最大応答ヘッダーサイズが 4 KB を超えるようにサーブレットコンテナが設定されていることを確認します。

例えば、Tomcat 7.0 の場合、[HTTP コネクター](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)の maxHttpHeaderSize 属性によりヘッダーサイズの上限を調整します。

## Adobe Experience Manager のアンインストール {#uninstalling-adobe-experience-manager}

AEM は単一のディレクトリにインストールされるので、アンインストールユーティリティは必要ありません。インストールディレクトリ全体を削除するだけでアンインストールできます。ただし、AEM のアンインストール方法は、その目的および使用している永続ストレージによって変わります。

例えば、デフォルトの TarPM インストールなど、永続ストレージがインストールディレクトリに埋め込まれている場合、フォルダーを削除するとデータも削除されます。

>[!NOTE]
>
>Adobe では、AEM を削除する前にリポジトリをバックアップすることをお勧めします。&lt;cq-installation-directory> 全体を削除すると、リポジトリも削除されます。削除する前にリポジトリのデータを保管する場合は、&lt;cq-installation-directory>/crx-quickstart/repository フォルダーを他の場所に移動またはコピーしてから、その他のフォルダーを削除するようにしてください。

例えば、データベースサーバーなど、AEM のインストールが外部ストレージを使用している場合、フォルダーを削除してもデータは自動的には削除されませんが、ストレージ設定が削除されるので、JCR コンテンツの復元は困難になります。
