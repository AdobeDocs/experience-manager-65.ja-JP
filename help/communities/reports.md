---
title: レポートコンソール
description: Adobe Experience Manager オーサー環境から複数の方法でアクセスできる様々なレポートの使用方法について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communitiesの場合、オーサー環境からいくつかの方法でアクセスできる様々なレポートがあります。

一般的に、様々なレポートは次のとおりです。

* [ ビュー数レポート ](#views-report)

  任意のコミュニティサイトについて、コミュニティメンバーおよびサイト訪問者ごとにコンテンツのビューのグラフを提供します。

* [ 投稿レポート ](#posts-report)

  コミュニティメンバーがコミュニティサイトに投稿した様々なタイプのグラフを提供します。

表形式のレポートは、.csv 形式で書き出し、後続の処理で使用できます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから：**[!UICONTROL ナビゲーション]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL レポート]**

* 次の中から選択します。

   * **[!UICONTROL 割り当て報告書]**

      * 選択したコミュニティ サイト、ユーザーまたはグループ、および割り当てに関するレポートを生成します。

   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティ サイト、コンテンツ タイプ、および期間に関するレポートを生成します。

   * **[!UICONTROL ビュー数レポート]**

      * 選択したコミュニティ サイト、コンテンツ タイプ、および期間に関するレポートを生成します。

![ 報告書 ](assets/reports1.png)

## 表示レポート {#views-report}

ビューコンソールを使用すると、特定の期間、コミュニティ機能ごとにページビューに関するレポートを生成できます。

![view-report](assets/view-report.png)

レポートの条件を選択します。

* **[!UICONTROL サイト]**

  コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

  すべてのコンテンツを選択するか、サイトに存在する機能の 1 つを選択できます。

* **[!UICONTROL 時間枠]**

  次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択して、レポートを作成します。

![generate-views](assets/generate-views.png)

## 投稿レポート {#posts-report}

投稿コンソールを使用すると、特定の期間におけるコミュニティ機能への投稿数に関するレポートを生成できます。

![posts-report](assets/posts-report.png)

レポートの条件を選択します。

* **[!UICONTROL サイト]**

  コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

  すべてのコンテンツを選択するか、サイトに存在する機能の 1 つを選択できます。

* **[!UICONTROL 時間枠]**

  次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択して、レポートを作成します。

![generate-report](assets/generate-posts-report.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトがリストされていません {#no-community-sites-listed}

コミュニティサイトがリストされていない場合は、サイトに対してAdobe Analyticsが有効になっていることを確認します。 割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造にあることを確認します。

### レポートがAEM オーサーインスタンスに表示されない {#reports-do-not-show-in-aem-author-instance}

AEM オーサーインスタンスにレポートが表示されない場合は、Publish インスタンスでの URL マッピングなど、カスタマイズの有無を確認してください。 URL マッピングが Communities サイトのAEM Publish インスタンスでのみ行われている場合は、AEM オーサーインスタンスで **Site Trend Report Social Component Factory** 設定に同じことが設定されていることを確認します。

![AEM オーサーの URL マッピング ](assets/sitetrend.png)
