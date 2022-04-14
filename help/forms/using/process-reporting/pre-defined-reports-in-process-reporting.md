---
title: プロセスレポートの事前定義済みレポート
seo-title: Pre-defined reports in Process Reporting
description: JEE 上の AEM Forms 用にプロセスデータをクエリして、長時間実行中のプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '703'
ht-degree: 100%

---

# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

## プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting-1}

AEM Forms プロセスレポートには、次の *標準提供* レポートが付属しています。

* **[長時間実行プロセス](#long-running-processes)**：完了までに指定された時間以上かかったすべての AEM Forms プロセスのレポート
* **[プロセス期間のグラフ](#process-duration-report)**：期間別の指定した AEM Forms プロセスのレポート
* **[ワークフローボリューム](#workflow-volume-report)**：指定されたプロセスの実行中および完了したインスタンスの日付別レポート

## 長時間実行プロセス {#long-running-processes}

長時間実行プロセスレポートには、完了までに指定した時間以上かかった AEM Forms プロセスが表示されます。

### 長時間実行プロセスレポートを実行するには {#to-execute-a-long-running-process-report}

1. プロセスレポートで事前定義済レポートのリストを表示するには、**プロセスレポート**&#x200B;ツリー表示で、**レポート**&#x200B;ノードをクリックしてください。
1. **長時間実行プロセス**&#x200B;レポートノードをクリックしてください。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリー表示の右側に&#x200B;**レポートパラメーター**&#x200B;パネルが表示されます。

   ![長時間実行プロセスレポートパラメータパネル](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**（*必須*）：期間と時間の単位を指定します。 指定された期間以上実行されたすべての AEM Forms プロセスを表示します。
   * **次の日から開始**（*オプション*）：日付を選択します。指定した日付以降に開始したプロセスインスタンスを表示するように、レポートをフィルタリングします。
   * **次の日より前に開始**（*オプション*）：日付を選択します。 指定した日付以前に開始したプロセスインスタンスを表示するように、レポートをフィルタリングします。

1. 「**移動**」をクリックしてレポートを実行します。

   レポートが&#x200B;**プロセスレポート**&#x200B;ウインドウの右側の&#x200B;**レポート**&#x200B;パネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**：ストレージにある最新のデータでレポートを更新
   * **凡例のカラーを変更**：レポートの凡例のカラーを選択して変更
   * **CSV にエクスポート**：レポートのデータをコンマ区切りファイルにエクスポートしてダウンロード

## プロセス期間レポート  {#process-duration-report}

プロセス期間レポートには、Forms プロセスのインスタンス数が、各インスタンスが実行された日数別に表示されます。

### プロセス期間レポートを実行するには {#to-execute-a-process-duration-report}

1. プロセスレポートで事前定義されたレポートを表示するには、**プロセスのレポート**&#x200B;ツリー表示で、**レポート**&#x200B;ノードをクリックします。
1. **プロセス期間**&#x200B;レポートノードをクリックします。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、 ツリー表示の右側に&#x200B;**レポートパラメーター**&#x200B;パネルが表示されます。

   ![長時間実行プロセスレポートパラメータパネル](assets/process_duration_params.png)

   パラメーター:

   * **プロセスを選択**（*必須*）：AEM Forms プロセスを選択します。

1. 「**移動**」をクリックしてレポートを実行します。

   レポートがプロセスレポートウィンドウの右側にある&#x200B;**レポート**&#x200B;パネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行してください。

   * **更新**：ストレージにある最新のデータでレポートを更新
   * **凡例のカラーを変更**：レポートの凡例のカラーを選択して変更
   * **CSV にエクスポート**：レポートのデータをコンマ区切りファイルにエクスポートしてダウンロード

## ワークフローボリュームレポート {#workflow-volume-report}

ワークフローボリュームレポートには、AEM Forms プロセスの現在実行中および完了したインスタンスの数がカレンダー日別に表示されます。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report}

1. プロセスレポートで事前定義されたレポートを表示するには、**プロセスレポート**&#x200B;ツリー表示で、**レポート**&#x200B;ノードをクリックします。
1. **ワークフローボリューム**&#x200B;レポートノードをクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、 **レポートパラメーター**&#x200B;パネルがツリー表示の右側に表示されます。

   ![長時間実行されているプロセスのレポートパラメーターパネル](assets/workflow_volume_params.png)

   パラメーター:

   * **プロセスを選択**（*必須*）：AEM Forms プロセスを選択します。

   * **次の日付から開始**（*オプション*）：日付を選択します。 指定した日付の後に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

   * **次の日付より前に開始**（*オプション*）：日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. 「 **移動**」をクリックしてレポートを実行してください。

   レポートは、**プロセスレポート**&#x200B;ウィンドウの右側にある&#x200B;**レポート**&#x200B;パネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   **レポート**&#x200B;パネルの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**：ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**：レポートの凡例の色を選択および変更
   * **CSV への書き出し**：レポートのデータをコンマ区切りファイルにエクスポートしてダウンロード
