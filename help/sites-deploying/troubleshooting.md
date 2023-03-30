---
title: トラブルシューティング
seo-title: Troubleshooting
description: この記事では、AEMで発生する可能性のあるインストールの問題の一部を説明します。
seo-description: This article covers some of the installation issues you might encounter with AEM.
uuid: 2ca898c3-b074-4ccd-a383-b92f226e6c14
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 5542de4e-6262-4300-9cf8-0eac79ba4f9a
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 11%

---

# トラブルシューティング{#troubleshooting}

この節では、トラブルシューティングに役立つログに関する詳細情報と、AEMで発生する可能性のある問題の一部に関する情報を示します。

## オーサーパフォーマンスのトラブルシューティング {#troubleshoot-author-performance}

オーサリングインスタンスでの低速パフォーマンスの分析が複雑になる場合があります。 最初のステップとして、パフォーマンスが低下しているテクノロジースタックのレベルを把握する必要があります。

次のデシジョンツリーは、ボトルネックを絞り込むためのガイダンスを提供します。

![chlimage_1-75](assets/chlimage_1-75.png)

## 基本的な最適化 {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## ログファイルと監査ログの設定 {#configuring-log-files-and-audit-logs}

AEMは、インストールに関する問題のトラブルシューティングに設定する必要がある詳細なログを記録します。 詳しくは、 [監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 」セクションに入力します。

## Verbose オプションの使用 {#using-the-verbose-option}

AEM WCM の起動時に、コマンドラインに次のように –v（verbose）オプションを追加できます。java -jar cq-wcm-quickstart-&lt;version>.jar -v

verbose オプションを指定すると、クイックスタートログの出力の一部がコンソールに表示されるので、トラブルシューティングに使用できます。

## 一般的なインストールの問題 {#common-installation-issues}

次の節では、インストールに関するいくつかの問題とその解決策について説明します。

### クイックスタート JAR をダブルクリックしても効果がないか、別のプログラム（アーカイブマネージャーなど）で jar ファイルが開きます。 {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

この問題は通常、拡張子が.jar のファイルを開くようにオペレーティングシステムのデスクトップ環境が設定されている方法に問題があることを示しています。 また、Java™がインストールされていない、またはサポートされていないバージョンの Java™を使用していることを示している場合もあります。

jar ファイルがユビキタス ZIP 形式を使用するので、一部のアーカイブプログラムは、jar ファイルをアーカイブファイルとして開くようにデスクトップを自動的に設定する場合があります。

トラブルシューティングをおこなうには、次の手順を実行します。

* 少なくとも Java™バージョン 1.6 がインストールされていることを再確認します。
* AEM WCM Quickstart でコンテキストメニュー（通常はマウスの右クリック）を試し、「次で開く…」を選択します。.&quot;
* Java™または Sun Java™が表示されているかどうかを確認し、それを使用してAEM WCM を実行してみます。 複数の Java™バージョンがインストールされている場合は、サポートされているバージョンを選択します。

   この手順で成功し、オペレーティングシステムで常に選択したプログラムを使用して.jar ファイルを実行するオプションが提供されている場合は、そのプログラムを選択します。 これからダブルクリックが機能します。

* サポートされている Java™バージョンを再インストールすると、正しい関連付けが復元される場合があります。
* このドキュメントで前述したように、常にコマンドラインまたは開始/停止スクリプトを使用して CRX を実行できます。

### CRX で実行中のアプリケーションでメモリ不足エラーが発生する {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>[メモリの問題の分析](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=en)も参照してください。


CRX 自体にはメモリフットプリントが少ない。 CRX 内で動作するアプリケーションが大きなメモリ要件を持つ場合、またはメモリ負荷の高い操作（大きなトランザクションなど）を要求する場合は、CRX が実行される JVM インスタンスを適切なメモリ設定で起動する必要があります。

Java™コマンドオプションを使用して、JVM のメモリ設定を定義します（例えば、java -Xmx512m -jar crx&amp;ast;.jar を使用して heapsize を 512 MB に設定します）。

コマンドラインからAEM WCM を起動する際に、メモリ設定オプションを指定します。 AEM WCM の起動/停止スクリプトまたはAEM WCM の起動を管理するカスタムスクリプトを変更して、必要なメモリ設定を定義することもできます。

既にヒープサイズを 512 MB として定義している場合、次の方法でヒープダンプを作成してメモリの問題を詳細に分析することができます。

メモリ不足の際にヒープダンプを自動的に作成するには、次のコマンドを使用します。

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar *.jar

このメソッドは、ヒープダンプファイル (**java_...hprof**) を返します。 ヒープダンプが生成された後も、プロセスが引き続き実行される場合があります。 通常、1 つのヒープダンプファイルで問題を分析できます。

### AEM Quickstart をダブルクリックした後、ブラウザーにAEMのようこそ画面が表示されない {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

特定の状況で、リポジトリ自体が正常に実行されているにもかかわらず、AEM WCM のようこそ画面が自動的に表示されない場合があります。 この問題は、オペレーティングシステムの設定、ブラウザーの設定、その他の要因によって異なります。

通常の症状は、AEM WCM Quickstart ウィンドウに「AEM WCM startup, waiting for server startup...」と表示されることです。.&quot; そのメッセージが比較的長い時間表示される場合は、デフォルトの 4502 ポートまたはインスタンスが実行されているポートを使用して、ブラウザーウィンドウにAEM WCM URL を手動で入力します。http://localhost:4502/.

また、ログには、ブラウザーが起動しない理由が示される場合があります。

AEM WCM Quickstart ウィンドウに「http://localhost:port/でAEM WCM が実行中」というメッセージが表示され、ブラウザーが自動的に起動しない場合があります。 この場合、AEM WCM Quickstart ウィンドウ（ハイパーリンク）で URL をクリックするか、ブラウザーに URL を手動で入力します。

それ以外のすべてが失敗した場合は、ログを調べて、何が起きたかを確認します。

### Java™ 11 で Web サイトが読み込まれない、または断続的に失敗する {#the-website-does-not-load-or-fails-intermittently-with-java11}

Java™ 11 上でAEM 6.5 を実行している場合、Web サイトの読み込みがおこなわれず、断続的に失敗する可能性がある既知の問題があります。

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

geometrixx-outdoors/en ページへのリクエストが 404(Page Not Found) を返した場合は、これらの特定のアプリケーションサーバーに必要な sling.properties ファイルに追加の sling プロパティが設定されていることを再確認してください。

詳しくは、「*AEM Web アプリケーションのデプロイ*」の手順を参照してください。

### 応答ヘッダーのサイズは 4 KB を超える場合があります {#response-header-size-can-be-greater-than-kb}

502 エラーは、Web サーバーがAEM HTTP 応答ヘッダーのサイズを処理できないことを示す場合があります。 AEMでは、4 KB を超えるサイズの Cookie を含む HTTP 応答ヘッダーを生成できます。 応答ヘッダーの最大サイズが 4 KB を超えるようにサーブレットコンテナが設定されていることを確認します。

例えば、Tomcat 7.0 の場合、 [HTTP コネクタ](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) ヘッダーサイズの制限を制御します。

## Adobe Experience Managerのアンインストール {#uninstalling-adobe-experience-manager}

AEMは単一のディレクトリにインストールされるので、アンインストールユーティリティは必要ありません。 AEMのアンインストール方法は、実行する内容と使用する永続的なストレージによって異なりますが、インストールディレクトリ全体を削除するのと同じくらい簡単にアンインストールできます。

例えば、デフォルトの TarPM インストールで永続的なストレージがインストールディレクトリに埋め込まれている場合、フォルダを削除すると、データも削除されます。

>[!NOTE]
>
>Adobeでは、AEMを削除する前にリポジトリをバックアップすることをお勧めします。 を削除すると、 &lt;cq-installation-directory>を使用してリポジトリを削除することもできます。 削除する前にリポジトリデータを保持するには、 &lt;cq-installation-directory>/crx-quickstart/repository フォルダーを別の場所に移動してから、他のフォルダーを削除します。

AEMのインストールで外部ストレージ（データベースサーバーなど）を使用している場合、フォルダーを削除してもデータは自動的には削除されませんが、ストレージ設定は削除されるので、JCR コンテンツの復元が困難です。

### JSP ファイルが JBoss®でコンパイルされない {#jsp-files-are-not-compiled-on-jboss}

JBoss®上で JSP ファイルをExperience Managerにインストールまたは更新し、対応するサーブレットがコンパイルされていない場合は、JBoss® JSP コンパイラーが正しく設定されていることを確認します。 詳しくは、
[JBoss®での JSP コンパイルの問題](https://helpx.adobe.com/jp/experience-manager/kb/jsps-dont-compile-jboss.html) 記事。
