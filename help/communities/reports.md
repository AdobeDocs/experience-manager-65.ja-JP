---
title: レポートコンソール
seo-title: Reports Console
description: レポートのアクセス方法について説明します
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 39%

---

# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communities には様々なレポートがあり、オーサー環境から複数の方法でアクセスできます。

通常、レポートには以下のものがあります。

* [割り当てレポート](#assignments-report)

   の [実施可能コミュニティ](/help/communities/overview.md#enablement-community)には、SCORM 標準を実装した場合の関連スコアを含む、学習者の割り当ての進行状況の概要が表示されます。

* [表示レポート](#views-report)

   コミュニティサイトのコミュニティメンバーおよびサイト訪問者によるコンテンツのビュー数のグラフを表示します。

* [投稿レポート](#posts-report)

   コミュニティメンバーがコミュニティサイトに投稿した様々なタイプの投稿のグラフを表示します。

条件 [Adobe Analyticsが有効](/help/communities/sites-console.md#analytics)のレポートには、各イネーブルメントリソースの表示数、再生数、コメント数、評価数が経時的に表示されます。

表形式のレポートは .csv 形式でエクスポートして別の処理に使用できます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** >  **[!UICONTROL レポート]**

* 次から選択：

   * **[!UICONTROL 割り当てレポート]**

      * 選択したコミュニティサイト、ユーザーまたはグループ、および割り当てに関するレポートを生成します。
   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間に関するレポートを生成します。
   * **[!UICONTROL 表示レポート]**

      * 選択したコミュニティサイト、コンテンツタイプおよび期間のレポートを生成します。。



![レポート](assets/reports1.png)

### イネーブルメントリソースと学習パスのレポート {#reports-for-enablement-resources-and-learning-paths}

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** >  **[!UICONTROL リソース]**

* 既存のイネーブルメントコミュニティサイトを選択します。

   * 選択 **レポート** アイコンを使用して、すべてのイネーブルメントリソースをカバーするレポートを生成します。
   * イネーブルメント学習パスを選択します。
   * 選択 **レポート** アイコン：

      * に含まれているイネーブルメントリソース。
      * 学習パスに割り当てられた学習者。

* 以下のレポートが表示されます。

   * テーブルデータは CSV としてダウンロード可能：

      * 学習者の識別
      * ステータス
      * カタログを通じて割り当てるかアクセスするか
      * 行われたコメント数
      * 与えられた星評価

詳しくは、リソースコンソールの[レポートセクション](/help/communities/resources.md#report)を参照してください。

## 割り当てレポート {#assignments-report}

割り当てコンソールでは、イネーブルメントコミュニティサイト、ユーザー、グループおよび割り当てによってレポートをフィルタリングできます。

このレポートには、進捗状況に関する情報と、コメントや評価がある場合はそれも表示されます。

![割り当てレポート](assets/assignment-report.png)

レポートのフィルタリング条件を選択します。

* **サイト**

   イネーブルメントコミュニティサイトを選択します。

* **ユーザーまたはグループ**
   * 「ユーザー」を選択して、1 人の学習者に関するレポートを生成します。
   * 「グループ」を選択して、学習者グループのレポートを生成します。

   トンネルサービスは、パブリッシュ環境からメンバーおよびメンバーグループにアクセスします。

* **代入**

   選択した学習者に割り当てられたイネーブルメントリソースの中から選択します。

「**生成**」を選択してレポートを作成します。

![generate-report](assets/generate-assignment-report.png)

## 表示レポート {#views-report}

表示コンソールでは、指定した期間におけるコミュニティ機能別のページ表示回数のレポートを生成できます。

![ビューレポート](assets/view-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   [ すべてのコンテンツ ] を選択するか、サイトに存在する機能の 1 つを選択します。

* **[!UICONTROL 期間]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

選択 **[!UICONTROL 生成]** をクリックして、レポートを作成します。

![generate-views](assets/generate-views.png)

## 投稿レポート {#posts-report}

投稿コンソールでは、指定した期間におけるコミュニティ機能への投稿数のレポートを生成できます。

![posts-report](assets/posts-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   [ すべてのコンテンツ ] を選択するか、サイトに存在する機能の 1 つを選択します。

* **[!UICONTROL 期間]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

選択 **[!UICONTROL 生成]** をクリックして、レポートを作成します。

![generate-report](assets/generate-posts-report.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが 1 つも表示されない {#no-community-sites-listed}

コミュニティサイトが 1 つも表示されない場合は、Adobe Analytics がサイトに対して有効になっているかを確認してください。割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。

### AEM オーサーインスタンスにレポートが表示されない {#reports-do-not-show-in-aem-author-instance}

AEM オーサーインスタンスにレポートが表示されない場合は、パブリッシュインスタンス上の URL マッピングなどのカスタマイズを確認します。 URL マッピングがコミュニティサイトの AEM パブリッシュインスタンスでのみ行われる場合は、AEM オーサーインスタンスで同じ設定が行われていることを確認します ( **サイトトレンドレポートソーシャルコンポーネントファクトリ** 設定。

![AEM オーサーでの URL マッピング](assets/sitetrend.png)
