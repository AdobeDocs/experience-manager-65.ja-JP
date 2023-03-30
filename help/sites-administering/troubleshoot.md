---
title: AEM のトラブルシューティング
seo-title: Troubleshooting AEM
description: AEMの問題のトラブルシューティングについて説明します。
seo-description: Learn about troubleshooting issues with AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 20%

---

# AEM のトラブルシューティング {#troubleshooting-aem}

次の節では、AEMの使用時に発生する可能性のあるいくつかの問題と、そのトラブルシューティング方法に関する推奨事項について説明します。

>[!NOTE]
>
>AEMでオーサリングの問題をトラブルシューティングする場合は、 [作成者向けのトラブルシューティング。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>問題が発生した場合は、リストを確認することも重要です。 [既知の問題](/help/release-notes/release-notes.md) インスタンス（リリースおよびサービスパック）の

## 管理者向けのトラブルシューティングシナリオ {#troubleshooting-scenarios-for-administrators}

管理者がトラブルシューティングできる問題の概要を次の表に示します。

<table>
 <tbody>
  <tr>
   <td><strong>役割</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>システム管理者</td>
   <td><p>クイックスタート JAR をダブルクリックしても何も起こらないか、JAR ファイルを別のプログラム（アーカイブマネージャーなど）で開く</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>CRX で実行中のアプリケーションでメモリ不足エラーが発生する</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> </td>
   <td><p>AEM CM Quickstart をダブルクリックした後、ブラウザーにAEMのようこそ画面が表示されない</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>管理者ユーザー</p> </td>
   <td><p>スレッドダンプの作成</p> </td>
  </tr>
  <tr>
   <td><p>システム管理者</p> <p>管理者ユーザー</p> </td>
   <td><p>閉じられていない JCR セッションの確認</p> </td>
  </tr>
 </tbody>
</table>

## インストールの問題 {#installation-issues}

詳しくは、 [一般的なインストールの問題](/help/sites-deploying/troubleshooting.md#common-installation-issues) 次のトラブルシューティングシナリオについては、を参照してください。

* クイックスタート JAR をダブルクリックしても効果がないか、別のプログラム（アーカイブマネージャーなど）が含まれた JAR ファイル。
* CRX で実行中のアプリケーションはメモリ不足エラーをスローします。
* AEM Quickstart をダブルクリックした後、ブラウザーにAEMのようこそ画面が表示されない。

## 分析のトラブルシューティング方法 {#methods-for-troubleshooting-analysis}

### スレッドダンプの作成 {#making-a-thread-dump}

スレッドダンプは、現在アクティブなすべての Java™スレッドのリストです。 AEMが正しく応答しない場合、スレッドダンプは、デッドロックやその他の問題を識別するのに役立ちます。

### Sling Thread Dumper の使用 {#using-sling-thread-dumper}

1. を開きます。 **AEM Web コンソール**;例： `https://localhost:4502/system/console/`.
1. **ステータス**&#x200B;タブの下の&#x200B;**スレッド**&#x200B;を選択します。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack の使用（コマンドライン） {#using-jstack-command-line}

1. AEM Java™インスタンスの PID（プロセス ID）を見つけます。

   例えば、`ps -ef` や `jps` を使用できます。

1. 実行:

   `jstack <pid>`

1. スレッドダンプを表示します。

>[!NOTE]
>
>`>>` 出力リダイレクトを使用すると、ログファイルにスレッドダンプを追加できます。
>
>`jstack <pid> >> /path/to/logfile.log`

詳しくは、[JVM からのスレッドダンプの取得方法](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=en)を参照してください。

### 閉じられていない JCR セッションの確認 {#checking-for-unclosed-jcr-sessions}

AEM WCM 用の機能が開発されている場合、JCR セッションを開くことができます（データベース接続を開く場合と同等）。 開いたセッションが閉じられない場合は、システムに次の現象が発生する可能性があります。

* システムの速度が低下します。
* CacheManager の多くは次のように表示されます。resize ログファイル内のすべてのエントリ；次の数値 (size=&lt;x>) はキャッシュの数を示し、各セッションは複数のキャッシュを開きます。
* システムのメモリが不足することがある（重大度に応じて数時間後、数日後、数週間後に発生）。

閉じられていないセッションを分析し、セッションを閉じていないコードを調べるには、ナレッジベースの記事を参照してください [閉じられていないセッションの分析](https://helpx.adobe.com/jp/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Adobe Experience Manager Web コンソールの使用 {#using-the-adobe-experience-manager-web-console}

OSGi バンドルのステータスによって、考えられる問題が早期に示される場合もあります。

1. を開きます。 **AEM Web コンソール**;例： `https://localhost:4502/system/console/`.
1. **OSGI** タブの下の&#x200B;**バンドル**&#x200B;を選択します。
1. チェック項目:

   * バンドルのステータス。 Inactive または Unsatisfied の場合は、バンドルを停止して再起動してみます。 問題が解決しない場合は、他の方法を使用してさらに調査します。
   * いずれかのバンドルに依存関係がないかどうか。 このような詳細は、個々のバンドル名（リンク）をクリックすると確認できます（次の例では問題はありません）。

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
