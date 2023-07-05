---
title: ライブコピーの概要コンソール
seo-title: Live Copy Overview Console
description: ライブコピーの概要コンソールの基本について説明します。
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 785d4897263bfeae6a0cd235abca3c96f2231392
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 42%

---

# ライブコピーの概要コンソール{#live-copy-overview-console}

この **ライブコピーの概要** では、次のことが可能です。

* サイト全体での継承の表示/管理：

   * ブループリントツリーと対応するライブコピー構造を、継承ステータスと共に表示します
   * 継承ステータスを変更する。例：休止、再開
   * ブループリントおよびライブコピーのプロパティを表示

* ロールアウトアクションの実行

## ライブコピーの概要を開く {#opening-the-live-copy-overview}

ライブコピーの概要は、以下から開くことができます。

* [ブループリントページの参照サイドパネル（Sites コンソール）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [ブループリントページのプロパティ](#opening-live-copy-overview-properties-of-a-blueprint-page)

### ライブコピーの概要を開く - ブループリントページの参照 {#opening-live-copy-overview-references-for-a-blueprint-page}

「**ライブコピーの概要**」は、**Sites** コンソールの&#x200B;**参照**&#x200B;サイドパネルから開くことができます。

1. 内 **サイト** コンソール [ブループリントページに移動して選択します。](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. を開きます。 **[参照](/help/sites-authoring/basic-handling.md#references)** パネルと選択 **ライブコピー**.

   ![参照パネル — ライブコピー](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >最初に「参照」を開いてから、ブループリントを選択することもできます。

1. 選択 **ライブコピーの概要** 選択したブループリントに関連するすべてのライブコピーの概要を表示および使用します。
1. 「**閉じる**」を使用して終了し、**Sites** コンソールに戻ります。

### ライブコピーの概要を開く — ブループリントページのプロパティ {#opening-live-copy-overview-properties-of-a-blueprint-page}

この **ライブコピーの概要** は、ブループリントページのプロパティの表示時に開くことができます。

1. 開く **プロパティ** 適切なブループリントページ用の
1. を開きます。 **ブループリント** タブ — **ライブコピーの概要** オプションが上部のツールバーに表示されます。

   ![「ブループリント」タブ — ライブコピーの概要](assets/chlimage_1-360.png)

1. 「**ライブコピーの概要**」を選択して、現在のブループリントに関連するすべてのライブコピーの概要を表示および使用します。

   >[!NOTE]
   >
   >詳しくは、ナレッジベースの記事も参照してください。 [ライブコピーのステータスメッセージ — 最新/緑/同期](https://helpx.adobe.com/jp/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 「**閉じる**」を使用して終了し、**Sites** コンソールに戻ります。

## ライブコピーの概要の使用 {#using-the-live-copy-overview}

この **ライブコピーの概要** ライブコピーに対してアクションを実行する場合にも使用できます。

1. **ライブコピーの概要**&#x200B;を開きます。
1. 必要なブループリントまたはライブコピーページを選択します。ツールバーが更新され、使用可能なアクションが表示されます。 この [アクション](/help/sites-administering/msm.md#terms-used) 使用可能かは、 [ブループリント](#actions-for-a-blueprint-page) または [ライブコピー](#actions-for-a-live-copy-page) ページ：

### ブループリントページのアクション {#actions-for-a-blueprint-page}

ブループリントページを選択した場合は、以下のアクションを使用できます。

![ブループリントが選択されました — 使用可能なアクション](assets/chlimage_1-361.png)

* 編集

   * ブループリントページを編集用に開きます。

* [ロールアウト](/help/sites-administering/msm.md#rollout-and-synchronize)

   * ロールアウトを実行して、ソースからライブコピーに変更をプッシュします。

### ライブコピーページのアクション {#actions-for-a-live-copy-page}

ライブコピーページを選択すると、次のアクションを使用できます。

![ライブコピーページが選択されました — 使用可能なアクション](assets/chlimage_1-362.png)

* 編集

   * 編集用にライブコピーページを開きます。

* [関係ステータス](#relationship-status)

   * ステータスおよび継承に関する情報を表示します。

* [同期](/help/sites-administering/msm.md#rollout-and-synchronize)

   * ライブコピーを同期して、ソースからライブコピーに変更内容をプルします。

* [リセット](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * ライブコピーページをリセットして、すべての継承のキャンセルを削除し、ソースページと同じ状態にページを戻します。

* [休止](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * ライブコピーとそのブループリントページの間のライブ関係を一時的にアクティベート解除します。

* [再開](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 再開によって、休止状態の関係を復帰できます。

* [分離](/help/sites-administering/msm.md#detaching-a-live-copy)

   * ライブコピーとそのブループリントページの間のライブ関係を永続的に削除します。

## 関係ステータス {#relationship-status}

この **関係ステータス** コンソールには、様々な機能を提供する 2 つのタブがあります。

* [関係ステータス情報](#relationship-status-information)
* [ライブコピー情報](#live-copy-information)

### 関係ステータス情報 {#relationship-status-information}

このタブには、ブループリントとライブコピーとの関係のステータスに関する詳細情報が表示されます。

![関係ステータス情報](assets/chlimage_1-363.png)

### ライブコピー情報 {#live-copy-information}

このタブでは、ライブコピーの設定を表示および編集できます。

![ライブコピー情報](assets/chlimage_1-364.png)
