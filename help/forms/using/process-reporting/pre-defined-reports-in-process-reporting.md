---
title: プロセスレポートの事前定義済みレポート
seo-title: プロセスレポートの事前定義済みレポート
description: JEE上のAEM Formsプロセスデータに対するクエリを実行し、長時間実行しているプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成します
seo-description: JEE上のAEM Formsプロセスデータに対するクエリを実行し、長時間実行しているプロセス、プロセス期間、ワークフローボリュームに関するレポートを作成します
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

## プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reportingには、次の追加設 *定不要のレポートが付属します* 。

* **[Long Running Processes](#long-running-processes)**:完了に指定時間以上かかったすべてのAEM Formsプロセスのレポート
* **[プロセス期間グラフ](#process-duration-report)**:期間別の指定されたAEM Formsプロセスのレポート
* **[Workflow Volume](#workflow-volume-report)**:指定したプロセスの実行中および完了済みインスタンスの日付別レポート

## 長時間実行するプロセス {#long-running-processes}

長時間実行中のプロセスレポートは、完了に指定時間以上かかったAEM Formsプロセスを表示します。

### 長時間実行中のプロセスレポートを実行するには {#to-execute-a-long-running-process-report}

1. プロセスレポートで事前定義されたレポートのリストを表示するには、「 **Process Reporting** 」ツリービューで、「**Reports **」ノードをクリックします。
1. 「 **Long Running Processes」レポートノードをクリックします** 。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/report_parameters_panel.png)

   パラメーター:

   * **期間**(*必須*):期間と時間の単位を指定します。 指定した期間以上実行されたすべてのAEM Formsプロセスを表示します。
   * **開始日** (オ&#x200B;*プション*):日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。
   * **以前に開始** (オ&#x200B;*プション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. 「移動 **** 」をクリックしてレポートを実行します。

   レポートは、「プロセスレポート」ウィンドウの右側の「**レポート* **** 」パネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   **Report **panelの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

## プロセス期間レポート {#process-duration-report}

プロセス期間レポートは、Formsプロセスのインスタンス数を各インスタンスが実行された日数別に表示します。

### プロセス期間レポートを実行するには {#to-execute-a-process-duration-report}

1. プロセスレポートで事前定義済みのレポートを表示するには、「 **Process Reporting** 」ツリービューで「**Reports **」ノードをクリックします。
1. 「プロセス期間」 **レポートノードをクリック** します。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/process_duration_params.png)

   パラメーター:

   * **プロセスを選択**(*必須*):AEM formsプロセスを選択します。

1. 「**Go **」をクリックして、レポートを実行します。

   レポートは、「プロセスレポート」ウィンドウの右側の**レポート**パネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   **Report **panelの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

## ワークフローの量レポート {#workflow-volume-report}

ワークフローの量レポートは、AEM Formsプロセスの現在実行中および完了したインスタンスの数をカレンダーの日別に表示します。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report}

1. プロセスレポートで事前定義されたレポートを表示するには、**プロセスレポート**ツリービューで**レポート**ノードをクリックします。
1. 「ワークフローの **量」レポートノード** をクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、ツリ **ービューの右側に[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行中のプロセスのレポートパラメーターパネル](assets/workflow_volume_params.png)

   パラメーター:

   * **プロセスを選択**(*必須*):AEM formsプロセスを選択します。

   * **開始日** (オ&#x200B;*プション*):日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。

   * **以前に開始** (オ&#x200B;*プション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するようにレポートをフィルターします。

1. 「**Go **」をクリックして、レポートを実行します。

   レポートは、「プロセスレポート」ウィンドウの右側の「**レポート* **** 」パネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   **Report **panelの右上隅にあるオプションを使用して、レポートに対して次の操作を実行します。

   * **更新**:ストレージに存在する最新のデータでレポートを更新
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータを書き出し、コンマ区切りファイルにダウンロードします

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
