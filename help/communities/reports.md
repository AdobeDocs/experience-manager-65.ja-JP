---
title: レポートコンソール
seo-title: レポートコンソール
description: レポートのアクセス方法について説明します
seo-description: レポートのアクセス方法について説明します
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Administrator
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 39%

---

# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communities には様々なレポートがあり、オーサー環境から複数の方法でアクセスできます。

通常、レポートには以下のものがあります。

* [割り当てレポート](#assignments-report)

   [イネーブルメントコミュニティ](/help/communities/overview.md#enablement-community)の場合、は、SCORM標準を実装する場合に関連するスコアを含む、学習者の割り当ての進捗状況の概要を提供します。

* [表示レポート](#views-report)

   コミュニティサイトのコミュニティメンバーとサイト訪問者別に、コンテンツのビュー数のグラフを表示します。

* [投稿レポート](#posts-report)

   コミュニティメンバーがコミュニティサイトに投稿した様々なタイプの投稿のグラフを表示します。

[Adobe Analyticsが有効](/help/communities/sites-console.md#analytics)の場合、レポートには各イネーブルメントリソースの表示数、再生数、コメント数、評価数が経時的に表示されます。

表形式のレポートは .csv 形式でエクスポートして別の処理に使用できます。

## レポートコンソール  {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから：**[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL レポート]**

* 次の中から選択：

   * **[!UICONTROL 割り当てレポート]**

      * 選択したコミュニティサイト、ユーザーまたはグループ、および割り当てに関するレポートを生成します。
   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間に関するレポートを生成します。
   * **[!UICONTROL 表示レポート]**

      * 選択したコミュニティサイト、コンテンツタイプおよび期間のレポートを生成します。。



![レポート](assets/reports1.png)

### イネーブルメントリソースと学習パスのレポート {#reports-for-enablement-resources-and-learning-paths}

* グローバルナビゲーションから：**[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL リソース]**

* 既存のイネーブルメントコミュニティサイトを選択します。

   * **レポート**&#x200B;アイコンを選択して、すべてのイネーブルメントリソースを対象とするレポートを生成します。
   * イネーブルメント学習パスを選択します。
   * **レポート**&#x200B;アイコンを選択して、次のレポートを生成します。

      * 付属のイネーブルメントリソース。
      * 学習パスに割り当てられた学習者。

* 以下のレポートが表示されます。

   * テーブルデータ（CSVとしてダウンロード可能）:

      * 学習者の識別
      * ステータス
      * カタログを通じて割り当てるかアクセスするか
      * 作成されたコメントの数
      * 星評価

詳しくは、リソースコンソールの[レポートセクション](/help/communities/resources.md#report)を参照してください。

## 割り当てレポート  {#assignments-report}

割り当てコンソールでは、イネーブルメントコミュニティサイト、ユーザー、グループおよび割り当てによってレポートをフィルタリングできます。

このレポートには、進捗状況に関する情報と、コメントや評価がある場合はそれも表示されます。

![割り当てレポート](assets/assignment-report.png)

レポートのフィルタリング条件を選択します。

* **サイト**

   イネーブルメントコミュニティサイトを選択します。

* **ユーザーまたはグループ**
   * 「ユーザー」を選択して、1人の学習者のレポートを生成します。
   * 「グループ」を選択して、学習者のグループに関するレポートを生成します。

   トンネルサービスは、パブリッシュ環境からメンバーとメンバーグループにアクセスします。

* **代入**

   選択した学習者に割り当てられているイネーブルメントリソースの中から選択します。

「**生成**」を選択してレポートを作成します。

![generate-report](assets/generate-assignment-report.png)

## Views Report {#views-report}

表示コンソールでは、指定した期間におけるコミュニティ機能別のページ表示回数のレポートを生成できます。

![view-report](assets/view-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   [すべてのコンテンツ]を選択するか、サイトに存在する機能の1つを選択します。

* **[!UICONTROL 時間枠]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択してレポートを作成します。

![generate-views](assets/generate-views.png)

## Posts Report {#posts-report}

投稿コンソールでは、指定した期間におけるコミュニティ機能への投稿数のレポートを生成できます。

![posts-report](assets/posts-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   [すべてのコンテンツ]を選択するか、サイトに存在する機能の1つを選択します。

* **[!UICONTROL 時間枠]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択してレポートを作成します。

![generate-report](assets/generate-posts-report.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが 1 つも表示されない  {#no-community-sites-listed}

コミュニティサイトが 1 つも表示されない場合は、Adobe Analytics がサイトに対して有効になっているかを確認してください。割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。

### AEMオーサーインスタンス{#reports-do-not-show-in-aem-author-instance}にレポートが表示されない

レポートがAEMオーサーインスタンスに表示されない場合は、パブリッシュインスタンスでのURLマッピングなど、カスタマイズ内容を確認します。 URLマッピングがコミュニティサイトのAEMパブリッシュインスタンスでのみ実行される場合は、**サイトトレンドレポートのソーシャルコンポーネントファクトリ**&#x200B;設定のAEMオーサーインスタンスで同じ設定がおこなわれていることを確認します。

![AEMオーサーでのURLマッピング](assets/sitetrend.png)
