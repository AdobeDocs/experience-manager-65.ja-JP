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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 39%

---


# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communities には様々なレポートがあり、オーサー環境から複数の方法でアクセスできます。

通常、レポートには以下のものがあります。

* [割り当てレポート](#assignments-report)

   [イネーブルメントコミュニティ](/help/communities/overview.md#enablement-community)に対して、SCORM標準を実装する場合の関連スコアを含む、学習者の割り当てに対する進行状況の概要を提供します。

* [表示レポート](#views-report)

   コミュニティメンバーや任意のコミュニティサイトのサイト訪問者別に、コンテンツの表示のグラフを表示します。

* [投稿レポート](#posts-report)

   コミュニティメンバー別の様々なタイプの投稿を、任意のコミュニティサイトにグラフで表示します。

[Adobe Analyticsが有効](/help/communities/sites-console.md#analytics)の場合、レポートには、有効化された各リソースの表示数、再生数、コメント数、評価数が時間の経過と共に含まれます。

表形式のレポートは .csv 形式でエクスポートして別の処理に使用できます。

## レポートコンソール  {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから：**[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL レポート]**

* 次の中から選択します。

   * **[!UICONTROL 割り当てレポート]**

      * 選択したコミュニティサイト、ユーザーまたはグループ、割り当てに関するレポートを生成します。
   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間のレポートを生成します。
   * **[!UICONTROL 表示レポート]**

      * 選択したコミュニティサイト、コンテンツタイプおよび期間のレポートを生成します。。



![レポート](assets/reports1.png)

### イネーブルメントリソースと学習パスのレポート {#reports-for-enablement-resources-and-learning-paths}

* グローバルナビゲーションから：**[!UICONTROL ナビゲーション]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL リソース]**

* 既存の有効化コミュニティサイトを選択してください：

   * **レポート**&#x200B;アイコンを選択して、すべての有効化リソースを対象としたレポートを生成します。
   * 有効化の学習パスを選択します。
   * **レポート**&#x200B;アイコンを選択して、次のレポートを生成します。

      * 付属の有効化リソース。
      * 学習パスに割り当てられた学習者。

* これらのレポートには、次の機能があります。

   * 表データ（CSV形式でダウンロード可能）:

      * 学習者の識別
      * 彼らの地位
      * カタログを使用して割り当てるか、アクセスするか
      * コメントの数
      * 与えられた星評価

詳しくは、リソースコンソールの[レポートセクション](/help/communities/resources.md#report)を参照してください。

## 割り当てレポート  {#assignments-report}

割り当てコンソールでは、イネーブルメントコミュニティサイト、ユーザー、グループおよび割り当てによってレポートをフィルタリングできます。

このレポートには、進捗状況に関する情報と、コメントや評価がある場合はそれも表示されます。

![譲渡報告](assets/assignment-report.png)

レポートのフィルタリング条件を選択します。

* **サイト**

   有効化コミュニティサイトを選択します。

* **ユーザーまたはグループ**
   * 「ユーザー」を選択して、1人の学習者のレポートを生成します。
   * 「グループ」を選択して、学習者のグループに関するレポートを生成します。

   トンネルサービスは、パブリッシュ環境からメンバーとメンバーグループにアクセスします。

* **代入**

   選択した学習者に割り当てられている有効化リソースの中から選択します。

「**生成**」を選択してレポートを作成します。

![生成レポート](assets/generate-assignment-report.png)

## Views Report {#views-report}

表示コンソールでは、指定した期間におけるコミュニティ機能別のページ表示回数のレポートを生成できます。

![表示報告](assets/view-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   「すべてのコンテンツ」を選択するか、サイトに存在する機能の1つを選択します。

* **[!UICONTROL 時間枠]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択して、レポートを作成します。

![generate-表示](assets/generate-views.png)

## Posts Report {#posts-report}

投稿コンソールでは、指定した期間におけるコミュニティ機能への投稿数のレポートを生成できます。

![posts-report](assets/posts-report.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   「すべてのコンテンツ」を選択するか、サイトに存在する機能の1つを選択します。

* **[!UICONTROL 時間枠]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択して、レポートを作成します。

![生成レポート](assets/generate-posts-report.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが 1 つも表示されない {#no-community-sites-listed}

コミュニティサイトが 1 つも表示されない場合は、Adobe Analytics がサイトに対して有効になっているかを確認してください。割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造にあることを確認します。

### AEM作成者インスタンス{#reports-do-not-show-in-aem-author-instance}にレポートが表示されない

レポートがAEM作成者インスタンスに表示されない場合は、発行インスタンスでのURLのマッピングなど、カスタマイズ内容を確認します。 URLのマッピングがコミュニティサイトのAEM Publishインスタンスでのみ行われる場合は、**サイトトレンドレポートのソーシャルコンポーネントファクトリ**&#x200B;の設定のAEM Authorインスタンスでも同じ設定が行われていることを確認します。

![AEM作成者でのURLマッピング](assets/sitetrend.png)