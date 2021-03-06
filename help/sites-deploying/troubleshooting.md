---
title: トラブルシューティング
seo-title: Troubleshooting
description: この記事では、AEM で発生する可能性のあるインストールの問題について説明します。
seo-description: This article covers some of the installation issues you might encounter with AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 100%

---

# トラブルシューティング{#troubleshooting}

ここでは、トラブルシューティングに役立つ利用可能なログに関する詳細情報と、AEM で発生する可能性のある問題について説明します。

## オーサーインスタンスのパフォーマンスのトラブルシューティング {#troubleshoot-author-performance}

パフォーマンスが低いオーサーインスタンスの分析は、非常に複雑になる場合があります。最初の手順として、どのテクノロジースタックのレベルでパフォーマンスが低下しているか把握することが必要です。

以下のフローチャートはボトルネックを絞り込む手引きになります。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本的な最適化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## ログファイルと監査ログの設定 {#configuring-log-files-and-audit-logs}

AEM では詳細ログが記録されます。これらのログは、インストールに関する問題のトラブルシューティングをおこなうために設定できます。詳しくは、[監査記録とログファイルの使用](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)を参照してください。

## Verbose オプションの使用 {#using-the-verbose-option}

AEM WCM の起動時に、コマンドラインに次のように –v（verbose）オプションを追加できます。java -jar cq-wcm-quickstart-&lt;version>.jar -v

verbose オプションによってコンソールに Quickstart ログの出力が表示されるので、その情報をトラブルシューティングに使用できます。

## 一般的なインストールの問題 {#common-installation-issues}

ここでは、インストールの問題とその解決策について説明します。

### Quickstart jar をダブルクリックしても何も起きないか、jar ファイルが別のプログラム（アーカイブマネージャーなど）で開かれる {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

通常、オペレーティングシステムのデスクトップ環境で拡張子 .jar のファイルを開く際の設定方法に問題があります。また、Java をインストールしていないか、サポートされていない Java のバージョンを使用している可能性もあります。

jar ファイルは汎用の ZIP 形式を使用しているので、一部のアーカイブプログラムによって、jar ファイルをアーカイブファイルとして開くように自動的にデスクトップが設定されることがあります。

トラブルシューティングには、次の操作をおこないます。

* Java バージョン 1.6 以降をインストールしていることを再確認します。
* AEM WCM Quickstart でコンテキストメニューを使用し（通常はマウスの右クリック）、「プログラムから開く」を選択します。
* Java または Sun Java が表示されるかを確認し、そのプログラムでの AEM WCM の実行を試みます。複数の Java バージョンがインストールされている場合は、サポートされているバージョンを選択します。

   この時点で成功した場合、常に選択したプログラムを使用して .jar ファイルを実行するためのオプションが表示されるので、そのオプションを選択します。これで、ダブルクリックによって起動できるようになります。

* サポートされている Java バージョンを再インストールすることで、適切な関連付けが復元される場合があります。
* 前述のとおり、常にコマンドラインまたは起動／停止スクリプトを使用して CRX を実行することもできます。

### CRX で動作しているアプリケーションでメモリ不足のエラーが発生する {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>[メモリの問題の分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)も参照してください。


CRX 自体は、非常に少ないメモリフットプリントで動作します。CRX 内部で実行しているアプリケーションで多くのメモリが必要とされる場合や、大量のメモリを使用する操作（長いトランザクションなど）が要求される場合、CRX が稼動する JVM インスタンスの起動時に適切なメモリ設定をおこなう必要があります。

Java コマンドオプションを使用して、JVM のメモリ設定を定義します（例えば、java -Xmx512m -jar crx*.jar の場合、ヒープサイズが 512 MB に設定されます）。

コマンドラインからの AEM WCM の起動時に、メモリ設定オプションを指定します。AEM WCM 起動／停止スクリプトまたは AEM WCM スタートアップの管理用カスタムスクリプトを修正して、必要なメモリ設定を定義することもできます。

既にヒープサイズを 512 MB として定義している場合、次の方法でヒープダンプを作成してメモリの問題を詳細に分析することができます。

メモリ不足の際にヒープダンプを自動的に作成するには、次のコマンドを使用します。

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar *.jar

このコマンドによって、プロセスがメモリ不足になったときに常にヒープダンプファイル（**java_...hprof**）が生成されます。ヒープダンプの生成後にもプロセスが実行し続ける場合もあります。通常、問題の分析には 1 つのヒープダンプファイルで十分です。

### AEM Quickstart をダブルクリックした後に、ブラウザーで AEM ようこそ画面が表示されない {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

特定の状況で、リポジトリ自体が正常に動作していても、AEM WCM ようこそ画面が自動的に表示されないことがあります。オペレーティングシステムの設定、ブラウザーの設定などの要因が考えられます。

一般的な兆候として、AEM WCM Quickstart ウィンドウに「AEM WCM を起動中、サーバーの起動を待機中」と表示されます。このメッセージが比較的長い時間表示される場合は、AEM WCM URL をブラウザーウィンドウに手動で入力してください。その際には、デフォルトの 4502 ポートか、インスタンスが稼動しているポートを使用します（例：http://localhost:4502/）。

また、ブラウザーが起動しない原因がログによってわかることがあります。

AEM WCM Quickstart ウィンドウに「AEM WCM が http://localhost:port/ で実行中です」というメッセージが表示され、ブラウザーが自動的に起動しない場合もあります。その場合は、AEM WCM Quickstart ウィンドウの URL（ハイパーリンク）をクリックするか、手動でブラウザーに URL を入力します。

その他のエラーが発生する場合は、ログをチェックして状況を確認してください。

### Java 11 で Web サイトが読み込まれない、または断続的に失敗する {#the-website-does-not-load-or-fails-intermittently-with-java11}

Java 11 上でAEM 6.5 を実行している場合、web サイトの読み込みまたは断続的な失敗が発生する可能性がある既知の問題があります。

この場合は、次の回避策に従ってください。

1. `crx-quickstart/conf/` フォルダー下の `sling.properties` ファイルを開きます。
1. 次の行を探します。

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. 以下のように置換します。

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. インスタンスを再起動します。

## アプリケーションサーバーによるインストールのトラブルシューティング {#troubleshooting-installations-with-an-application-server}

### geometrixx-outdoor ページを要求すると「Page Not Found」が返される {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**WebLogic 10.3.5 および JBoss 5.1 に適用**

geometrixx-outdoors/en ページを要求すると 404（Page Not Found）が返される場合は、これらの特定のアプリケーションサーバーに必要になる、sling.properties ファイルの追加の sling プロパティを設定しているかを再確認してください。

詳しくは、「*AEM Web アプリケーションのデプロイ*」の手順を参照してください。

### 応答のヘッダーサイズが 4 Kb を超える場合がある {#response-header-size-can-be-greater-than-kb}

Web サーバーが AEM HTTP 応答ヘッダーのサイズを処理できないときに 502 エラーが返されることがあります。AEM は、4 Kb を超えるサイズの Cookie を含む HTTP 応答ヘッダーを生成します。最大応答ヘッダーサイズが 4 kb を超えられるようにサーブレットコンテナを設定してください。

例えば、Tomcat 7.0 の場合、[HTTP コネクター](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html)の maxHttpHeaderSize 属性によりヘッダーサイズの上限を調整します。

## Adobe Experience Manager のアンインストール {#uninstalling-adobe-experience-manager}

AEM は単一のディレクトリにインストールされるので、アンインストールユーティリティは必要ありません。インストールディレクトリ全体を削除するだけでアンインストールできます。ただし、AEM のアンインストール方法は、その目的および使用している永続ストレージによって変わります。

例えば、デフォルトの TarPM インストールなど、永続ストレージがインストールディレクトリに埋め込まれている場合、フォルダーを削除するとデータも削除されます。

>[!NOTE]
>
>AEM を削除する前にリポジトリをバックアップすることを強く推奨します。&lt;cq-installation-directory> 全体を削除すると、リポジトリも削除されます。削除する前にリポジトリのデータを保管する場合は、&lt;cq-installation-directory>/crx-quickstart/repository フォルダーを他の場所に移動またはコピーしてから、その他のフォルダーを削除するようにしてください。

例えば、データベースサーバーなど、AEM のインストールが外部ストレージを使用している場合、フォルダーを削除してもデータは自動的には削除されませんが、ストレージ設定が削除されるので、JCR コンテンツの復元は困難になります。

### JSP ファイルが JBoss でコンパイルされない {#jsp-files-are-not-compiled-on-jboss}

JSP ファイルを JBoss の Experience Manager にインストールまたは更新したものの、対応するサーブレットがコンパイルされない場合は、JBoss JSP コンパイラが正しく設定されているかを確認します。詳しくは、[JBoss での JSP コンパイルの問題](https://helpx.adobe.com/jp/experience-manager/kb/jsps-dont-compile-jboss.html)に関する記事を参照してください。
