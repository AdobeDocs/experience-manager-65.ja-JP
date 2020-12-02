---
title: ページ分析データの表示
seo-title: ページ分析データの表示
description: ページ分析データを使用すると、ページコンテンツの効果を測定できます。
seo-description: ページ分析データを使用すると、ページコンテンツの効果を測定できます。
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 84%

---


# ページ分析データの表示{#seeing-page-analytics-data}

ページ分析データを使用すると、ページコンテンツの効果を測定できます。

## コンソールに表示できる分析結果  {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

ページ分析データはサイトコンソールの[リスト表示](/help/sites-authoring/basic-handling.md#list-view)に表示されます。ページがリスト形式で表示されているとき、デフォルトでは次の列が表示されます。

* ページ表示
* 個別訪問者数
* ページ滞在時間

各列には現在のレポート期間の値が表示され、前回のレポート期間と比較して値が増加したか減少したかも示されます。表示されるデータは 12 時間ごとに更新されます。

>[!NOTE]
>
>更新期間を変更するには、[読み込み間隔を設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)します。

1. **サイト**&#x200B;コンソールを開きます。例：[https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. ツールバーの右端（右上隅）で、アイコンをクリックまたはタップして、「**リスト表示**」（表示されるアイコンは、[現在の表示](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)によって異なる）を選択します。

1. もう一度、ツールバーの右端（右上隅）で、アイコンをクリックまたはタップして、「**設定を表示**」を選択します。**列を構成**&#x200B;ダイアログが開きます。必要な変更を加えて、「**更新**」で確定します。

   ![spad-02](assets/spad-02.png)

### レポート期間の選択 {#selecting-the-reporting-period}

サイトコンソールに表示される分析データのレポート期間を次の中から選択します。

* 過去 30 日間 データ
* 過去 90 日間のデータ
* 今年のデータ

現在のレポート期間がサイトコンソールのツールバー（上部のツールバーの右側）に表示されます。ドロップダウンを使用して、必要なレポート期間を選択します。

![aa-05](assets/aa-05.png)

### 利用できるデータ列の設定 {#configuring-available-data-columns}

analytics-administrators ユーザーグループのメンバーは、作成者が追加の分析列を確認できるようにサイトコンソールを設定できます。

>[!NOTE]
>
>ページのツリーに異なる Adobe Analytics のクラウド設定に関連付けられている子ページがある場合は、そのページで利用できるデータ列を設定できません。

1. リスト表示で、表示セレクター（ツールバーの右）を使用し、「**表示設定**」を選択し、「**カスタム解析データ追加**」を選択します。

   ![spad-03](assets/spad-03.png)

1. サイトコンソールで作成者に表示する指標を選択し、「**追加**」をクリックします。

   表示される列は、Adobe Analyticsから取得されます。

   ![aa-16](assets/aa-16.png)

### サイトからコンテンツインサイトを開く {#opening-content-insights-from-sites}

ページの効果をさらに調べるには、サイトコンソールから「[Content Insight](/help/sites-authoring/content-insights.md)」を開きます。

1. サイトコンソールで、コンテンツインサイトを表示するページを選択します。
1. ツールバーで、分析と推奨表示アイコンをクリックします。

   ![](do-not-localize/chlimage_1-14.png)

## ページエディターに表示できる分析結果（Activity Map）  {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。
>
>現在は、Adobe Analytics](https://docs.adobe.com/content/help/ja-JP/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.translate.html)が提供する[ActivityMapプラグインを使用する必要があります。
