---
title: ヘルスモニターのパフォーマンスに関する微調整
seo-title: ヘルスモニターのパフォーマンスに関する微調整
description: ヘルスモニターのパフォーマンスを微調整する方法について説明します。
seo-description: ヘルスモニターのパフォーマンスを微調整する方法について説明します。
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# ヘルスモニターのパフォーマンスに関する微調整{#fine-tuning-health-monitor-performance}

ヘルスモニターに表示するためにシステム統計を収集すると、AEM Forms 環境のパフォーマンスに多少の影響があります。お使いのアプリケーションサーバーで以下に示す Java オプションを設定すると、この影響を抑制できます。

<table>
 <thead>
  <tr>
   <th><p>プロパティ</p></th>
   <th><p>目的</p></th>
   <th><p>デフォルト値</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>ヘルスモニターのスレッドの有効化または無効化</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Gemfire のキャッシュの有効化または無効化。</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>ヘルスモニターのスレッドで統計情報を収集する間隔（ミリ秒単位）。</p></td>
   <td><p>10 分（600,000 ミリ秒）</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>分散システムの他のメンバーとの通信に使用するマルチキャストポート。ゼロに設定すると、メンバーの検出と配信の両方についてマルチキャストが無効になります。 </p><p>注意：異なる分散システムには、異なるマルチキャストアドレスとポートを選択します。アドレスのみ異なる構成は使用しないでください。</p></td>
   <td><p>デフォルト値はありません。有効な値は、0 ～ 65535 です。</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>統計情報がサンプリングされる頻度（ミリ秒単位）。オペレーティングシステムの統計情報は、サンプリングが行われるときにのみ更新されます。</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>このプロパティでは、ワークマネージャーの統計情報（ジョブ数や作業項目数など）の収集を有効または無効にします。</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## JBoss への Java オプションの追加 {#add-java-options-to-jboss}

1. JBoss アプリケーションサーバーを停止します。
1. Open the *[appserver root]*/bin/run.bat (Windows) or run.sh (Linux or UNIX) in an editor and add any of the Java options as required.
1. サーバーを再起動します。

## WebLogic への Java オプションの追加 {#add-java-options-to-weblogic}

1. Start the WebLogic administration console by typing https://[host name]:&#39;port&#39;/console in the URL line of a web browser.
1. WebLogic Server ドメインに対して作成したユーザー名とパスワードを入力し、「Log In」をクリックします。「Change Center」で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、Environment／Servers をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「Configuration」タブ／「Server Start」タブをクリックします。
1. 「Arguments」ボックスで、現在の内容の末尾に必要な引数を付加します。For example, adding - `Dadobe.healthmonitor.enabled=false` disables Health Monitor.
1. 「Save」をクリックし、「Activate Changes」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

## WebSphere への Java オプションの追加 {#add-java-options-to-websphere}

1. WebSphere Administrative Console のナビゲーションツリーで、アプリケーションサーバーに対して次の操作を実行します。

   （WebSphere 6.x）Servers／Application servers をクリックします。

   （WebSphere 7.x）Servers／Server Types／WebSphere application servers をクリックします。

1. 右側のウィンドウで、サーバー名をクリックします。
1. 「Server Infrastructure」で、Java and forms workflow／Process Definition をクリックします。
1. 「Additional Properties」で、「Java Virtual Machine」をクリックします。
1. 「Generic JVM arguments」ボックスに、必要な引数を入力します。
1. 「OK」または「Apply」をクリックし、「Save directly to the master configuration」をクリックします。

