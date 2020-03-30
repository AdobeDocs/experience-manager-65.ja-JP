---
title: ワークマネージャーとスロットリング
seo-title: ワークマネージャーとスロットリング
description: ここでは、ワークマネージャーに関する背景について、およびワークマネージャーのスロットリングオプションを設定する場合の手順について説明します。
seo-description: ここでは、ワークマネージャーに関する背景について、およびワークマネージャーのスロットリングオプションを設定する場合の手順について説明します。
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# ワークマネージャーとスロットリング{#work-manager-and-throttling}

AEM Forms（および以前のバージョン）では、非同期に操作を実行するために JMS キューを使用していました。AEM Forms では、JMS キューはワークマネージャーに置き換えられました。ここでは、ワークマネージャーに関する背景について、およびワークマネージャーのスロットリングオプションを設定する場合の手順について説明します。

## 有効期間が長い（同期）操作について {#about-long-lived-asynchronous-operations}

AEM Forms では、サービスによって実行される操作には、有効期間が短い（同期）操作または有効期間が長い（非同期）操作があります。有効期間が短い操作は、呼び出された同じスレッドで同期して完了します。また、応答が完了してから続行します。

有効期間が長い操作は、複数のシステムにまたがったり、さらには組織を越えて展開したりします。例えば、複数の自動タスクおよび手動タスクを統合する大規模なソリューションの一部として、顧客がローン申し込みフォームに入力して送信する場合などです。このような操作は応答を待つ間続きます。有効期間が長い操作は、基礎となる作業を非同期に実行し、本来であれば完了まで待つ必要があったリソースの実行を可能にします。有効期間が短い操作とは異なり、有効期間が長い操作が呼び出されると、ワークマネージャーはその完了を考慮しません。システムが同じサービス上の別の操作を要求したり、ユーザーがフォームを送信したりするなど、別の外部のトリガーによって操作の完了が発生します。

## ワークマネージャーについて {#about-work-manager}

AEM Forms（および以前のバージョン）では、非同期に操作を実行するために JMS キューを使用していました。AEM Forms では、ワークマネージャーを使用して、非同期操作をスケジュールし、管理されたスレッドを介して操作を実行します。

非同期操作は次の方法で処理されます。

1. ワークマネージャーで、実行予定の作業項目が受信されます。
1. ワークマネージャーは作業項目をデータベースのテーブルに保存し、固有の識別子を作業項目に割り当てます。データベースレコードには、作業項目の実行に必要なすべての情報が含まれます。
1. ワークマネージャースレッドは、スレッドが空いたときに作業項目を取得します。作業項目を取得する前に、必要なサービスが開始されているかどうか、次の作業項目を取得するために十分なヒープサイズがあるかどうか、作業項目を処理するために十分な CPU サイクルがあるかどうかがスレッドによってチェックされます。また、ワークマネージャーでは作業項目のスケジュール時に作業項目の属性（優先度など）も評価されます。

AEM forms 管理者は、ヘルスモニターを使用してワークマネージャーの統計情報（キュー内の作業項目数やそのステータスなど）を調べることができます。また、ヘルスモニターは、作業項目の一時停止、再開、再試行または削除にも使用できます（[ワークマネージャーに関連する統計情報の表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)を参照）。

## ワークマネージャーのスロットリングオプションの設定 {#configuring-work-manager-throttling-options}

ワークマネージャーのスロットリングは、使用できるメモリリソースが十分にある場合にのみ作業項目をスケジュールするように設定できます。スロットリングを設定するには、アプリケーションサーバーで次の JVM オプションを設定します。

<table>
 <thead>
  <tr>
   <th><p>プロパティ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>キュー内の新しい項目をチェックするときにワークマネージャーが使用する間隔（ミリ秒）を指定します。</p><p>このオプションの値は整数です。デフォルト値は <code>1000</code> ミリ秒（1 秒）です。 </p><p>非同期の呼び出しの量が少ない場合、この値を増やすことができます。例えば、2,000～5,000（2～5 秒）の数値まで増やすことができます。 </p><p>非同期呼び出しの量が多い場合はデフォルト値で十分ですが、必要に応じて低い値を使用することもできます。この値を減らしすぎると（例えば 50 未満にすると 1 秒に 20 回のポーリング頻度になります）、システムのオーバーヘッドが大幅に増加します。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>このオプションを <code>true</code> に設定するとデバッグモードが有効になり、false を設定すると無効になります。 </p><p>デバッグモードでは、ワークマネージャーのポリシー違反およびワークマネージャーの一時停止／再開アクションに関するメッセージがログに記録されます。このオプションはトラブルシューティングの場合にのみ true に設定します。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>このオプションを <code>true</code> に設定すると、後述するメモリ制御設定に基づいてスロットリングが有効になります。<code>false</code> に設定するとスロットリングが無効になります。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>ワークマネージャーが受信ジョブをスロットリング処理する前に、使用状態にすることができるメモリの最大比率を指定します。</p><p>このオプションのデフォルト値は <code>95</code> です。この値はほとんどのシステムに適しています。最大容量までシステムを実行する必要がある場合にのみ、値を増やしてください。ただし、この値を増やすときは、メモリ不足の問題が発生するリスクも増える点に注意してください。</p><p>クラスター環境で AEM Forms を実行している場合、クラスターのノードごとにメモリ制御の制限設定を変えることもできます。例えば、インタラクティブな作業用にロードバランサーでプログラミングしたノード A と B に対して低い上限を設定し、ロードバランサーからは使用せず、非同期作業に予約されているノード C と D には高い上限を設定することができます。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>ワークマネージャーが受信ジョブのスロットリングを停止する前に、使用状態にすることができるメモリの最大比率を指定します。</p><p>このオプションのデフォルト値は <code>20</code> です。この値はほとんどのシステムに適しています。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>ワークマネージャーの最大バッチサイズを指定します。デフォルトのバッチサイズは 10 です。</p><p>タスクが終了した後もワークマネージャーのプロセスのステータスが更新されない場合は、バッチサイズを 1 に設定します。</p></td>
  </tr>
 </tbody>
</table>

**JBoss への Java オプションの追加**

1. JBoss アプリケーションサーバーを停止します。
1. Open the *[appserver root]*/bin/run.bat (Windows) or run.sh (Linux or UNIX) in an editor and add any of the Java options as required, in the format `-Dproperty=value`.
1. サーバーを再起動します。

**WebLogic への Java オプションの追加**

1. Start the WebLogic Administration Console by typing `https://[host name]:[port]/console` in a web browser.
1. WebLogic Server ドメインに対して作成したユーザー名とパスワードを入力し、「Log In」をクリックします。「Change Center」で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、Environment／Servers をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「Configuration」タブ／「Server Start」タブをクリックします。
1. 「Arguments」ボックスで、現在の内容の末尾に必要な引数を付加します。例えば、ヘルスモニターを無効にするには、

   `-Dadobe.healthmonitor.enabled=false` ヘルスモニターを無効にします。

1. 「Save」をクリックし、「Activate Changes」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

**WebSphere への Java オプションの追加**

1. WebSphere Administrative Console のナビゲーションツリーで、Servers／Server Types／WebSphere application servers をクリックします。
1. 右側のウィンドウで、サーバー名をクリックします。
1. 「Server Infrastructure」で、Java and forms workflow／Process Definition をクリックします。
1. 「Additional Properties」で、「Java Virtual Machine」をクリックします。
1. 「Generic JVM arguments」ボックスに、必要な引数を入力します。
1. 「OK」または「Apply」をクリックし、「Save directly to the master configuration」をクリックします。

