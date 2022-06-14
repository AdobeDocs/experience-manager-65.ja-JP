---
title: AEM のトラブルシューティング
seo-title: Troubleshooting AEM
description: AEM に関する問題のトラブルシューティングについて説明します。
seo-description: Learn about troubleshooting issues with AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 100%

---

# AEM のトラブルシューティング {#troubleshooting-aem}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>AEM のオーサリングの問題をトラブルシューティングする場合は、[オーサリング時の AEM のトラブルシューティング](/help/sites-authoring/troubleshooting.md)を参照してください。

>[!NOTE]
>
>問題が発生した場合は、そのインスタンス（リリースおよびサービスパック）の[既知の問題](/help/release-notes/release-notes.md)の一覧を確認すると役に立ちます。

## 管理者が実行するトラブルシューティングのシナリオ {#troubleshooting-scenarios-for-administrators}

次の表は、管理者がトラブルシューティングをおこなう必要のある問題の概要を示しています。

<table>
 <tbody>
  <tr>
   <td><strong>役割</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>システム管理者</td>
   <td><p>Quickstart jar をダブルクリックしても何も起きないか、jar ファイルが別のプログラム（アーカイブマネージャーなど）で開かれる</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>CRX で動作しているアプリケーションでメモリ不足のエラーが発生する</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>AEM CM Quickstart をダブルクリックした後に、ブラウザーで AEM ようこそ画面が表示されない</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>admin ユーザー</p> </td>
   <td><p>スレッドダンプの作成</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>admin ユーザー</p> </td>
   <td><p>閉じられていない JCR セッションの確認</p> </td>
  </tr>
 </tbody>
</table>

## インストールの問題 {#installation-issues}

以下のトラブルシューティングのシナリオについては、[一般的なインストールの問題](/help/sites-deploying/troubleshooting.md#common-installation-issues)を参照してください。

* Quickstart jar をダブルクリックしても何も起きないか、JAR ファイルが別のプログラム（アーカイブマネージャーなど）で開かれる。
* CRX で動作しているアプリケーションでメモリ不足のエラーが発生する。
* AEM Quickstart をダブルクリックした後に、ブラウザーで AEM ようこそ画面が表示されない。

## トラブルシューティング分析の方法 {#methods-for-troubleshooting-analysis}

### スレッドダンプの作成 {#making-a-thread-dump}

スレッドダンプは、現在アクティブなすべての Java スレッドのリストです。AEM が適切に応答しない場合は、デッドロックまたはその他の問題をスレッドダンプで特定できます。

### Sling Thread Dumper の使用 {#using-sling-thread-dumper}

1. **AEM web コンソール**&#x200B;を開きます（例：`https://localhost:4502/system/console/`）。
1. **ステータス**&#x200B;タブの下の&#x200B;**スレッド**&#x200B;を選択します。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack の使用（コマンドライン） {#using-jstack-command-line}

1. AEM Java インスタンスの PID（プロセス ID）を確認します。

   例えば、`ps -ef` や `jps` を使用できます。

1. 実行:

   `jstack <pid>`

1. スレッドダンプが表示されます。

>[!NOTE]
>
>`>>` 出力リダイレクトを使用すると、ログファイルにスレッドダンプを追加できます。
>
>`jstack <pid> >> /path/to/logfile.log`

詳しくは、[JVM からのスレッドダンプの取得方法](https://helpx.adobe.com/cq/kb/TakeThreadDump.html)を参照してください。

### 閉じられていない JCR セッションの確認 {#checking-for-unclosed-jcr-sessions}

AEM WCM 用の機能を開発する場合は、JCR セッションが開かれる可能性があります（データベース接続を開く処理に相当します）。開かれたセッションが閉じられないと、システムで以下の症状が発生する可能性があります。

* システムの速度が低下する。
* 多数の CacheManager を確認できます（ログファイル内の resizeAll エントリ）。次の数値（size=&lt;x>）はキャッシュ数を示しており、各セッションが複数のキャッシュを開きます。
* システムのメモリが不足することがある（重大度に応じて数時間後、数日後、数週間後に発生）。

閉じられていないセッションを分析して、セッションを閉じていないコードを特定するには、ナレッジベースの記事[閉じられていないセッションの分析](https://helpx.adobe.com/jp/crx/kb/AnalyzeUnclosedSessions.html)を参照してください。

### Adobe Experience Manager Web コンソールの使用 {#using-the-adobe-experience-manager-web-console}

発生する可能性のある問題の初期の兆候を OSGi バンドルのステータスで確認することもできます。

1. **AEM web コンソール**&#x200B;を開きます（例：`https://localhost:4502/system/console/`）。
1. **OSGI** タブの下の&#x200B;**バンドル**&#x200B;を選択します。
1. チェック項目:

   * バンドルのステータス。「Inactive」または「Unsatisfied」と表示されているバンドルがある場合は、そのバンドルを停止してから再起動してください。問題が解決しない場合は、他の方法を使用した詳細な調査が必要になる可能性があります。
   * いずれかのバンドルで依存関係が失われていないかどうか。個々のバンドル名（リンク）をクリックすると、詳細を確認できます（問題が発生していない場合の例を次に示します）。

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
