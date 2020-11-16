---
title: プロセスレポートの事前定義済みレポート
seo-title: プロセスレポートの事前定義済みレポート
description: JEE上のAEM Formsのプロセスデータを使用して、長時間実行しているプロセス、プロセス期間、ワークフローの量に関するレポートを作成するクエリ
seo-description: JEE上のAEM Formsのプロセスデータを使用して、長時間実行しているプロセス、プロセス期間、ワークフローの量に関するレポートを作成するクエリ
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting}

## プロセスレポートの事前定義済みレポート {#pre-defined-reports-in-process-reporting-1}

AEM Formsプロセスレポートには、次 *の既成のレポートが付属しています* 。

* **[Long Running Processes](#long-running-processes)**:完了に指定時間以上かかったすべてのAEM Formsプロセスのレポート
* **[プロセス期間グラフ](#process-duration-report)**:期間別の特定AEM Formsプロセスのレポート
* **[ワークフローの量](#workflow-volume-report)**:日付別に指定されたプロセスの実行中および完了インスタンスのレポート

## 長時間実行するプロセス {#long-running-processes}

長時間実行中のプロセスレポートには、完了に指定時間以上かかったAEM Formsのプロセスが表示されます。

### 「Long Running Process」レポートを実行するには {#to-execute-a-long-running-process-report}

1. プロセスレポートで事前定義済みのレポートのリストを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **Long Running Processes** 」レポートノードをクリックします。

   ![long_running_node](assets/long_running_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/report_parameters_panel.png)

   パラメーター:

   * **期間** (*必須*):期間と単位を指定します。 指定した期間を超えて実行されたすべてのAEM Formsプロセスを表示します。
   * **開始後** (*オプション*):日付を選択します。 レポートをフィルターして、指定した日付以降に開始したプロセスインスタンスを表示します。
   * **以前に開始** (*オプション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するように、レポートをフィルターします。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートは、 **プロセスレポート** ( **Process Management** )ウィンドウの右側のレポートパネルに表示されます。

   ![long_running_processes](assets/long_running_processes.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**:ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする

## プロセス期間レポート  {#process-duration-report}

プロセス期間レポートは、Formsプロセスのインスタンス数を、各インスタンスが実行された日数別に表示します。

### プロセス期間レポートを実行するには {#to-execute-a-process-duration-report}

1. プロセスレポートで事前定義済みのレポートを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **プロセス期間** 」レポートノードをクリックします。

   ![process_duration_node](assets/process_duration_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/process_duration_params.png)

   パラメーター:

   * **Select Process** (*必須*):AEM Formsプロセスを選択します。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートがプロセスレポートウィンドウの右側の **レポート** パネルに表示されます。

   ![process_duration_report](assets/process_duration_report.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**:ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする

## ワークフローボリュームレポート {#workflow-volume-report}

ワークフローの量レポートには、現在実行中の、および完了したAEM Formsプロセスのインスタンス数がカレンダーの日別に表示されます。

### ワークフローボリュームレポートを実行するには {#to-execute-a-workflow-volume-report}

1. プロセスレポートで事前定義済みのレポートを表示するには、 **プロセスレポート** ツリー表示で、 **レポート** ノードをクリックします。
1. 「 **ワークフローボリューム** 」レポートノードをクリックします。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   レポートを選択すると、ツリー表示の右側に **[レポートパラメータ** ]パネルが表示されます。

   ![長時間実行プロセスレポートパラメーター](assets/workflow_volume_params.png)

   パラメーター:

   * **Select Process** (*必須*):AEM Formsプロセスを選択します。

   * **開始後** (*オプション*):日付を選択します。 指定した日付以降に開始したプロセスインスタンスを表示するフィルターをレポートに追加します。

   * **以前に開始** (*オプション*):日付を選択します。 指定した日付より前に開始したプロセスインスタンスを表示するフィルターをレポートに追加します。

1. 「 **移動** 」をクリックしてレポートを実行します。

   レポートは、 **プロセスレポート** ( **Process Management** )ウィンドウの右側のレポートパネルに表示されます。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   レポートパネルの右上隅にあるオプションを使用して、 **レポートに対して次の操作を実行します** 。

   * **更新**:ストレージ内の最新データを使用してレポートを更新します
   * **凡例の色を変更**:レポートの凡例の色を選択して変更する
   * **CSVにエクスポート**:レポートからデータをエクスポートし、コンマ区切りファイルにダウンロードする
