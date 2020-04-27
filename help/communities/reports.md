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
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communities には様々なレポートがあり、オーサー環境から複数の方法でアクセスできます。

通常、レポートには以下のものがあります。

* [割り当てレポート](#assignments-report)

   For an [enablement community](/help/communities/overview.md#enablement-community), provides an overview of learners&#39; progress on their assignments, including an associated score if implementing the SCORM standard.

* [表示レポート](#views-report)

   コミュニティメンバー別のコンテンツの表示と、コミュニティサイトの訪問者別のグラフを表示します。

* [投稿レポート](#posts-report)

   コミュニティメンバー別の様々なタイプの投稿をコミュニティサイトにグラフで表示します。

[Adobe Analyticsが有効な場合](/help/communities/sites-console.md#analytics)、レポートには、有効化された各リソースの表示数、再生数、コメント数および評価数が経時的に含まれます。

表形式のレポートは .csv 形式でエクスポートして別の処理に使用できます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* From global navigation: **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** >  **[!UICONTROL Reports]**

* 次の中から選択します。

   * **[!UICONTROL 割り当てレポート]**

      * 選択したコミュニティサイト、ユーザまたはグループ、および割り当てのレポートを生成します。
   * **[!UICONTROL 投稿レポート]**

      * 選択したコミュニティサイト、コンテンツタイプ、期間のレポートを生成します。
   * **[!UICONTROL 表示レポート]**

      * 選択したコミュニティサイト、コンテンツタイプおよび期間のレポートを生成します。。



![chlimage_1-236](assets/chlimage_1-236.png)

### イネーブルメントリソースと学習パスのレポート {#reports-for-enablement-resources-and-learning-paths}

* From global navigation: **[!UICONTROL Navigation]** > **[!UICONTROL Communities]** >  **[!UICONTROL Resources]**

* 既存の有効化コミュニティサイトを選択してください：

   * Select **Report** icon to generate reports which cover all enablement resources.
   * 有効化学習パスを選択します。
   * Select **Report** icon to generate reports for:

      * 使用可能なリソースが含まれています。
      * 学習パスに割り当てられた学習者。

* 次の情報が表示されます。

   * 表データ（CSV形式でダウンロード可能）:

      * 学習者の識別
      * 彼らのステータス
      * 割り当て済みか、カタログを通じてアクセス済みか
      * コメントの数
      * 星評価

詳しくは、リソースコンソールの[レポートセクション](/help/communities/resources.md#report)を参照してください。

## 割り当てレポート {#assignments-report}

割り当てコンソールでは、イネーブルメントコミュニティサイト、ユーザー、グループおよび割り当てによってレポートをフィルタリングできます。

このレポートには、進捗状況に関する情報と、コメントや評価がある場合はそれも表示されます。

![chlimage_1-237](assets/chlimage_1-237.png)

レポートのフィルタリング条件を選択します。

* **サイト**

   有効化コミュニティサイトを選択します。

* **ユーザーまたはグループ**
   * 「ユーザー」を選択して、1人の学習者のレポートを生成します。
   * 「グループ」を選択して、学習者のグループに関するレポートを生成します。
   トンネルサービスは、発行メンバーからメンバーおよびメンバーグループにアクセス環境します。

* **代入**

   選択した学習者に割り当てられている有効化リソースの中から選択します。

「**生成**」を選択してレポートを作成します。

![chlimage_1-238](assets/chlimage_1-238.png)

## Views Report {#views-report}

表示コンソールでは、指定した期間におけるコミュニティ機能別のページ表示回数のレポートを生成できます。

![chlimage_1-239](assets/chlimage_1-239.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   「すべてのコンテンツ」を選択するか、サイトに存在する機能の1つを選択できます。

* **[!UICONTROL 期間]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

Select **[!UICONTROL Generate]** to create the report.

![chlimage_1-240](assets/chlimage_1-240.png)

## Posts Report {#posts-report}

投稿コンソールでは、指定した期間におけるコミュニティ機能への投稿数のレポートを生成できます。

![chlimage_1-241](assets/chlimage_1-241.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**

   コミュニティサイトを選択します。

* **[!UICONTROL コンテンツタイプ]**

   「すべてのコンテンツ」を選択するか、サイトに存在する機能の1つを選択できます。

* **[!UICONTROL 期間]**

   次のいずれかを選択します。

   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

Select **[!UICONTROL Generate]** to create the report.

![chlimage_1-242](assets/chlimage_1-242.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが 1 つも表示されない {#no-community-sites-listed}

コミュニティサイトが 1 つも表示されない場合は、Adobe Analytics がサイトに対して有効になっているかを確認してください。割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。

### AEM作成者インスタンスにレポートが表示されない {#reports-do-not-show-in-aem-author-instance}

レポートがAEM作成者インスタンスに表示されない場合は、発行インスタンスでのURLのマッピングなど、カスタマイズの有無を確認します。 URLのマッピングがコミュニティサイトのAEM発行インスタンスでのみ行われる場合は、サイトトレンドレポートのソーシャルコンポーネントファクトリの設定で、AEM作成者インスタンスで **同じ設定が行われている** ことを確認します。

![AEM作成者のURLマッピング](assets/sitetrend.png)