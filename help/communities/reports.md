---
title: レポートコンソール
seo-title: Reports Console
description: レポートへのアクセス方法を説明します
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
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 11%

---

# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communitiesの場合、オーサー環境から様々な方法でアクセスできるレポートがあります。

一般に、様々なレポートは次のようになります。

* [表示レポート](#views-report)

   コミュニティサイトのコミュニティメンバーおよびサイト訪問者によるコンテンツのビュー数のグラフを表示します。

* [投稿レポート](#posts-report)

   コミュニティメンバーがコミュニティサイトに投稿した様々なタイプの投稿のグラフを表示します。

表形式のレポートは、後で処理するために.csv 形式で書き出すことができます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** >  **[!UICONTROL レポート]**

* 次から選択：

   * **[!UICONTROL 割り当てレポート]**

      * 選択したコミュニティサイト、ユーザーまたはグループ、および割り当てに関するレポートを生成します。
   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間に関するレポートを生成します。
   * **[!UICONTROL 表示レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間のレポートを生成します。



![レポート](assets/reports1.png)

## 表示レポート {#views-report}

表示コンソールを使用すると、特定の期間、コミュニティ機能別にページビューにレポートを生成できます。

![ビューレポート](assets/view-report.png)

レポートの条件を選択します。

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

投稿コンソールを使用すると、一定期間にコミュニティ機能に対する投稿数に関するレポートを生成できます。

![posts-report](assets/posts-report.png)

レポートの条件を選択します。

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

### コミュニティサイトが一覧に表示されていません {#no-community-sites-listed}

コミュニティサイトが表示されない場合は、Adobe Analyticsがサイトに対して有効になっていることを確認します。 割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。

### AEM オーサーインスタンスにレポートが表示されない {#reports-do-not-show-in-aem-author-instance}

AEM オーサーインスタンスにレポートが表示されない場合は、パブリッシュインスタンス上の URL マッピングなどのカスタマイズを確認します。 URL マッピングがコミュニティサイトの AEM パブリッシュインスタンスでのみ行われる場合は、AEM オーサーインスタンスで同じ設定が行われていることを確認します ( **サイトトレンドレポートソーシャルコンポーネントファクトリ** 設定。

![AEM オーサーでの URL マッピング](assets/sitetrend.png)
