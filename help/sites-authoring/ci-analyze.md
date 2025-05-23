---
title: ページパフォーマンスの分析
description: コンテンツインサイトページを使用して、作成中のページのパフォーマンスを分析する
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 100%

---

# ページパフォーマンスの分析 {#analyzing-page-performance}

[コンテンツインサイト](/help/sites-authoring/content-insights.md)ページを開き、作成中のページのパフォーマンスを分析します。レポート期間を設定して、分析に焦点を当てます。

## ページの「分析とレコメンデーション表示」を開く {#opening-analytics-and-recommendations-for-a-page}

次の手順を使用して、ページの分析とレコメンデーションを表示します。

1. 分析するページに移動します。
1. ツールバーで、「**分析と推奨表示**」をクリックします。

   >[!NOTE]
   >
   >ページの「分析とレコメンデーション表示」は、AEM で [Adobe Analytics との統合](/help/sites-administering/adobeanalytics-connect.md)を設定している場合にのみ表示されます。

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### レポート期間の変更 {#changing-the-reporting-period}

次の分析レポートの期間に関する側面を変更します。

* レポートの対象となる期間。
* データの精度。

レポートの時間に関連する側面を変更するツールは、コンテンツインサイトページの上部に表示されます。![chlimage_1-126](assets/chlimage_1-126.png)

#### レポート期間の変更 {#changing-the-reporting-period-1}

コンテンツインサイトページのレポート期間を変更して、ページアクティビティの分析を特定の期間に絞り込みます。レポート期間を変更すると、レポートは自動的に更新されます。期間の影付きの領域は、レポート対象期間を表します。期間の日付は、左から右に増加します。

![chlimage_1-127](assets/chlimage_1-127.png)

コンテンツインサイトページのレポート期間を変更するには、次の手順を実行します。

1. ページの上部にタイムフレームが表示されない場合は、タイムフレームを切り替えアイコンをクリックします。

   ![タイムフレームを切り替え](do-not-localize/chlimage_1-22.png)

1. レポート期間の開始日を変更するには、影付きの領域の左側に表示される円を目的の開始日までドラッグします。

   影付きの領域の左側が表示されない場合は、スクロールバーを使用して表示します。

1. レポート期間の終了日を変更するには、影付きの領域の右側に表示される円を目的の終了日までドラッグします。

#### レポート期間の精度の変更 {#changing-the-granularity-of-the-reporting-period}

各データポイントがレポート内で占める時間を変更します。例えば、週の精度が選択されている場合、表示回数レポートの各データポイントは 1 週間の閲覧数を表します。

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

精度は、閲覧数レポートやページでアクションが実行された平均時間（分）レポートなど、時間に対するデータのグラフを表示するレポートに影響します。精度は期間のスケールにも影響します。

1. 精度コントロールが表示されない場合は、精度を切り替えアイコンをクリックします。

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 目的の精度をクリックします。選択すると、レポートが自動的に更新され、精度が反映されます。

### SEO レコメンデーションのタスクの割り当て {#assigning-tasks-for-seo-recommendations}

SEO レコメンデーションレポートを使用して、検索エンジンでのページの表示性を改善するタスクを作成します。チェックマークの付いていないレポート内のレコメンデーションごとに、必要な作業を実行するためにユーザーに割り当てるタスクを作成できます。

![chlimage_1-129](assets/chlimage_1-129.png)

SEO のレコメンデーションのステータスは、タスクが作成されたものの、まだ完了していないことを示します。

![chlimage_1-130](assets/chlimage_1-130.png)

作成されると、タスクがユーザーのタスクリストに表示されます。タスクについては、[タスクの使用](/help/sites-authoring/task-content.md)を参照してください。

次の手順を使用して、SEO のレコメンデーションのタスクを作成します。

1. SEO の推奨の情報アイコンをクリックします。

   ![情報アイコン](do-not-localize/chlimage_1-23.png)

1. 情報アイコンの横に表示される、囲まれた三角形のアイコンをクリックします。

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. 表示されるフォームフィールドに入力し、「作成」を選択します。

   * プロジェクト：タスクを作成するプロジェクトを選択します。
   * 名前：タスクを識別する名前。デフォルト名は、SEO のレコメンデーションのタイトルです。
   * 割り当て先：タスクを割り当てるユーザーを選択します。リストをフィルタリングするには、ユーザーの名前を入力し始めます。
   * 説明：タスクの完了に必要なアクティビティの説明。デフォルトの説明は、SEO のレコメンデーションに付随する情報です。
   * タスクの優先度：タスクの優先度。
   * 期限：タスクを完了する必要がある日付。

   **注意 :**&#x200B;作成されるタスクには、SEO のレコメンデーションが適用されるページへのパスも含まれます。

1. 「完了」をクリックして、「タスクを作成しました」のメッセージを閉じます。
