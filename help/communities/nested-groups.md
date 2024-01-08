---
title: ネストされたグループの作成
description: Adobe Experience Manager Communities サイト用にネストされたグループを作成する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 3%

---

# ネストされたグループの作成{#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

AEMオーサーインスタンスで、グローバルナビゲーションから次の操作を実行します。

* 選択 **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* 選択 **[!UICONTROL エンゲージフォルダー]** をクリックして開きます。
* のカードを選択します。 **[!UICONTROL 入門チュートリアル]** 英語のサイト。

   * カードの画像を選択します。
   * 実行 *not* アイコンを選択します。

その結果、 [グループコンソール](/help/communities/groups.md):

![create-group](assets/create-group.png)

グループ機能は、グループのインスタンスが作成されるフォルダーとして表示されます。 開くには、グループフォルダーを選択します。 「公開」で作成したグループが表示されます。

![create-new-group](assets/create-new-group.png)

## メインアートグループを作成 {#create-main-arts-group}

このグループは、をエンゲージするためのサイト構造にグループの機能が含まれているので作成できます。 サイトの `Reference Template` デフォルトでは、有効なグループテンプレートを選択できます。 したがって、この新しいグループ用に選択されたテンプレートは、 `Reference Group`.

これらのコンソールは、コミュニティサイトコンソールに似ています。

* 選択 **[!UICONTROL グループを作成]**

* **コミュニティグループテンプレート**:

   * **[!UICONTROL コミュニティグループのタイトル]**: Arts
   * **[!UICONTROL コミュニティグループの説明]**：様々なアートグループの親グループ
   * **[!UICONTROL コミュニティグループのルート]**: *デフォルトのままにする*
   * **[!UICONTROL 追加の利用可能なコミュニティグループの言語]**：ドロップダウンメニューを使用して、使用可能なコミュニティグループの言語を選択します。 親コミュニティサイトが作成されたすべての言語がメニューに表示されます。 ユーザーは、この 1 つの手順で、複数のロケールでグループを作成するために、これらの言語の中から選択できます。 各コミュニティサイトのグループコンソールで、指定した複数の言語で同じグループが作成されます。
   * **[!UICONTROL コミュニティグループ名]**: arts
   * **[!UICONTROL テンプレート]**：選択するドロップダウン `Reference Group`
   * 選択 **[!UICONTROL 次へ]**

![ネストされたコミュニティグループ](assets/parent-to-nestedgroup.png)

次の設定を使用して、他のパネルも引き続き表示します。

* **[!UICONTROL Design]**

   * デザインを変更するか、既定の親サイトのデザインを許可します。
   * 「**[!UICONTROL 次へ]**」を選択します。

* **[!UICONTROL 設定]**

   * **[!UICONTROL モデレート]**

      * 空のままにします（親サイトから継承）。

   * **[!UICONTROL メンバーシップ]**

      * デフォルトを使用 `Optional Membership.`

      * **[!UICONTROL サムネール]**
         * `optional.*`

      * **[!UICONTROL 次を選択]**.

* 「**[!UICONTROL 作成]**」を選択します。

### Arts Group 内のグループのネスト {#nesting-groups-within-arts-group}

The `groups` フォルダーに 2 つのグループが含まれるようになりました（ページを更新）。

![グループのネスト](assets/create-community-group.png)

#### グループを公開 {#publish-group}

内にネストされたグループを作成する前に、 `arts` グループの上にマウスポインターを置き、 `arts` カードを選択し、公開アイコンを選択して公開します。

![publish-site](assets/publish-site.png)

グループが公開されたことを確認するまで待ちます。

![group-published](assets/group-published.png)

The `arts` グループには、 `groups` フォルダー内に作成されますが、空で新しいグループを作成できるフォルダー内に作成されます。 arts グループフォルダーに移動し、それぞれ異なるメンバーシップ設定を持つ、ネストされた 3 つのグループを作成します。

1. **[!UICONTROL ビジュアル]**

   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート： `Reference Group`
   * メンバーシップ： select `Optional Membership`：すべてのメンバーに対して開かれる公開グループ。

1. **[!UICONTROL 聴覚]**

   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート： `Reference Group`
   * メンバーシップ： select `Required Membership`：メンバーが参加できる、開いたグループ。

1. **[!UICONTROL 履歴]**

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート： `Reference Group`
   * メンバーシップ： select `Restricted Membership`：シークレットグループ。招待されたメンバーにのみ表示されます。 例として、を [デモユーザー](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

ページを更新して、3 つのネストされたグループ（サブコミュニティ）をすべて表示します。

コミュニティサイトコンソールからネストされたグループに移動するには、次の手順を実行します。

* を選択します。 **[!UICONTROL エンゲージフォルダー]**
* 選択 **[!UICONTROL はじめにチュートリアルカード]**
* を選択します。 **[!UICONTROL グループ]** フォルダー
* 選択 **[!UICONTROL アートカード]**
* を選択します。 **[!UICONTROL グループ]** フォルダー

![create-new-group2](assets/create-new-group2.png)

## 発行グループ {#publishing-groups}

![publish-site](assets/publish-site.png)

メインコミュニティサイトを公開した後：

* 各グループを個別に公開する：

   * グループが公開されたことを確認するのを待っています。

* 以下の中にネストされたグループを公開する前に、親グループを公開します。

   * すべてのグループは、トップダウン方式で公開する必要があります。

![group-published](assets/group-published.png)

## 公開時のエクスペリエンス {#experience-on-publish}

様々なグループがサインイン時に、例えば [デモユーザー](/help/communities/tutorials.md#demo-users) 次に使用：

* アート/履歴グループのメンバー： `emily.andrews@mailinator.com/password`
   * 制限された（秘密の）グループ、arts/history が表示されます。
   * オプション（公開）のグループを表示できます。
   * 制限された（開いた）グループに参加できます。

* グループマネージャー： `aaron.mcdonald@mailinator.com/password`

   * オプション（公開）のグループを表示できます。
   * 制限された（開いた）グループに参加できます。
   * 制限された（秘密の）グループを表示できません。

コミュニティにアクセス [メンバーコンソールとグループコンソール](/help/communities/members.md) オーサー環境で、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加します。
