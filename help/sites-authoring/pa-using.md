---
title: ページ分析データの表示によるページコンテンツの効果の測定
description: ページ分析データを使用すると、ページコンテンツの効果を測定できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '638'
ht-degree: 100%

---

# ページ分析データの表示 {#seeing-page-analytics-data}

ページ分析データを使用して、ページコンテンツの効果を測定します。

## コンソールに表示できる分析結果 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

ページ分析データは、Sites コンソールの[リスト表示](/help/sites-authoring/basic-handling.md#list-view)に表示されます。ページがリスト形式で表示されている場合、デフォルトで次の列が表示されます。

* ページ表示
* ユニーク訪問者
* ページ滞在時間

各列には現在のレポート期間の値が表示され、その値が前のレポート期間以降に増加したか減少したかも示されます。表示されるデータは 12 時間ごとに更新されます。

>[!NOTE]
>
>更新期間を変更するには、[読み込み間隔を設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)します。

1. **Sites** コンソールを開きます（例：[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)）。
1. ツールバーの右端（右上隅）で、アイコンをクリックして、「**リスト表示**」（表示されるアイコンは、[現在の表示](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)によって異なる）を選択します。

1. もう一度、ツールバーの右端（右上隅）でアイコンをクリックして、「**表示設定**」を選択します。**列を構成**&#x200B;ダイアログが開きます。必要な変更を加えて、「**更新**」で確定します。

   ![aa-04](assets/aa-04.png)

### レポート期間の選択 {#selecting-the-reporting-period}

Sites コンソールに表示される分析データのレポート期間を次の中から選択します。

* 過去 30 日間のデータ
* 過去 90 日間のデータ
* 今年のデータ

現在のレポート期間が Sites コンソールのツールバー（上部のツールバーの右側）に表示されます。ドロップダウンを使用して、必要なレポート期間を選択します。
![aa-05](assets/aa-05.png)

### 表示可能なデータ列の設定 {#configuring-available-data-columns}

analytics-administrators ユーザーグループのメンバーは、作成者に追加の分析列が表示されるように Sites コンソールを設定することができます。

>[!NOTE]
>
>様々な Adobe Analytics クラウド設定に関連付けられている子がページのツリーに含まれている場合、そのページで表示できるデータ列を設定することはできません。

1. リスト表示で、表示セレクター（ツールバーの右側）を使用し、「**表示設定**」、「**カスタム Analytics データを追加**」の順に選択します。

   ![aa-15](assets/aa-15.png)

1. Sites コンソールで作成者に表示する指標を選択し、「**追加**」をクリックします。

   表示される列は Adobe Analytics から取得されます。

   ![aa-16](assets/aa-16.png)

### Sites からコンテンツインサイトを開く {#opening-content-insights-from-sites}

Sites コンソールから「[コンテンツインサイト](/help/sites-authoring/content-insights.md)」を開き、ページの効果をさらに分析できます。

1. コンテンツインサイトを表示するページを Sites コンソールで選択します。
1. ツールバーで、Analytics と Recommendations アイコンをクリックします。

   ![Analytics と Recommendations アイコン](do-not-localize/chlimage_1-16a.png)

## ページエディターに表示できる分析結果（Activity Map） {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>これは、[Activity Map が Web サイト用に設定](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map)されている場合に表示されます。

>[!NOTE]
>
>Activity Map のデータは Adobe Analytics から取得されます。

Web サイトが [Adobe Analytics 用に設定されている](/help/sites-administering/adobeanalytics-connect.md)場合は、[Activity Map モード](/help/sites-authoring/author-environment-tools.md#page-modes)を使用して関連データを表示できます。次に例を示します。

![aa-07](assets/aa-07.png)

### Activity Map へのアクセス {#accessing-the-activity-map}

[Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) モードを選択すると、Adobe Analytics の認証情報を入力するよう求められます。

![aa-03](assets/aa-03.png)

**Analytics** のフローティングツールバーが表示されます。ここでは以下を行えます。

* 二重矢印（**>>**）を使用してツールバーの形式を変更する
* ページの詳細を切り替える（目のアイコン）
* Activity Map を設定する（歯車アイコン）
* 表示する分析を選択する（様々なドロップダウンセレクター）
* Activity Map を終了し、ツールバーを閉じる（x）

![aa-09](assets/aa-09.png)

### 表示する分析の選択 {#selecting-the-analytics-to-show}

表示する分析データを選択できます。また、以下の様々な条件を使用して、表示方法も選択できます。

* **標準**／**ライブ**

* イベントタイプ
* ユーザーグループ
* **バブル**／**グラデーション**／**勝者と敗者**／**オフ**

* 表示期間

![aa-13](assets/aa-13.png)

### Activity Map の設定 {#configuring-the-activity-map}

「**設定を表示**」アイコンを使用して、**Activity Map 設定**&#x200B;ダイアログを開きます。

![aa-04-1](assets/aa-04-1.png)

**Activity Map 設定**&#x200B;ダイアログでは、次の 3 つのタブに様々なオプションが用意されています。

![aa-06](assets/aa-06.png)

* 一般

   * レポートスイート
   * ページ名
   * 言語
   * ラベルのオーバーレイ
   * ラベルのフォントサイズ
   * グラデーションカラー
   * バブルカラー
   * カラーグラデーションの基準
   * グラデーションの透明度

* 標準

   * 表示（タイプとリンク数）
   * ヒットのなかったリンクのオーバーレイを非表示

* ライブ

   * 上に表示（勝者または敗者）
   * 下位を除外（％）
   * 自動更新（データと期間）
