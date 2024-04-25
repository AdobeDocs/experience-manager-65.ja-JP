---
title: ネストされたグループの作成
description: Adobe Experience Manager Communities サイト用にネストされたグループのを作成する方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 3%

---

# ネストされたグループの作成{#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

AEM オーサーインスタンスで、グローバルナビゲーションから：

* を選択 **[!UICONTROL コミュニティ]** > **[!UICONTROL Sites]**.
* を選択 **[!UICONTROL engage フォルダー]** をクリックして開きます。
* のカードを選択 **[!UICONTROL 入門チュートリアル]** 英語サイト。

   * カード画像を選択します。
   * 実行 *ではない* アイコンを選択します。

結果は、に到達します。 [グループコンソール](/help/communities/groups.md):

![create-group](assets/create-group.png)

groups 関数は、グループのインスタンスが作成されるフォルダーとして表示されます。 開くには、グループ フォルダーを選択します。 パブリッシュ環境で作成されたグループが表示されます。

![create-new-group](assets/create-new-group.png)

## メイン アート グループの作成 {#create-main-arts-group}

このグループを作成できるのは、エンゲージメントのためのサイト構造にグループの機能が含まれているからです。 サイトの機能の設定 `Reference Template` デフォルトではに設定されており、有効なグループテンプレートを選択できます。 したがって、この新しいグループ用に選択されたテンプレートは `Reference Group`.

これらのコンソールは、Communities サイトコンソールに似ています。

* を選択 **[!UICONTROL グループを作成]**

* **コミュニティグループテンプレート**:

   * **[!UICONTROL コミュニティグループタイトル]**：アーツ
   * **[!UICONTROL コミュニティグループの説明]**：様々なアーツグループの親グループ
   * **[!UICONTROL コミュニティグループのルート]**: *デフォルトのままにする*
   * **[!UICONTROL その他の使用可能なコミュニティグループ言語]**：ドロップダウンメニューを使用して、使用可能なコミュニティグループ言語を選択します。 メニューには、親コミュニティサイトが作成されたすべての言語が表示されます。 ユーザーは、これらの言語から選択して、この単一の手順で複数のロケールでグループを作成できます。 同じグループが、それぞれのコミュニティサイトのグループコンソールで複数の指定された言語で作成されます。
   * **[!UICONTROL コミュニティグループ名]**：アーツ
   * **[!UICONTROL Template]**：選択するドロップダウン `Reference Group`
   * を選択 **[!UICONTROL 次]**

![ネストされたコミュニティグループ](assets/parent-to-nestedgroup.png)

次の設定で他のパネルを続行します。

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

      * **[!UICONTROL 次へを選択]**.

* 「**[!UICONTROL 作成]**」を選択します。

### アーツグループ内のグループのネスト {#nesting-groups-within-arts-group}

この `groups` フォルダーに 2 つのグループが含まれるようになりました（ページを更新します）。

![グループのネスト](assets/create-community-group.png)

#### グループを公開 {#publish-group}

内にネストされたグループを作成する前に `arts` グループ化し、 `arts` カードを選択し、「公開」アイコンをクリックして公開します。

![publish-site](assets/publish-site.png)

グループが公開されたことを確認します。

![group-published](assets/group-published.png)

この `arts` グループにはも含める必要があります `groups` ただし、空で、新しいグループを作成できるフォルダーです。 アーツ グループ フォルダに移動し、ネストされた 3 つのグループを作成します。各グループには異なるメンバーシップ設定があります。

1. **[!UICONTROL ビジュアル]**

   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート： `Reference Group`
   * メンバーシップ：選択 `Optional Membership`：公開グループで、すべてのメンバーに公開されています。

1. **[!UICONTROL 聴覚]**

   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート： `Reference Group`
   * メンバーシップ：選択 `Required Membership`：メンバーが参加できる開かれたグループ。

1. **[!UICONTROL 履歴]**

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート： `Reference Group`
   * メンバーシップ：選択 `Restricted Membership`：招待されたメンバーにのみ表示される秘密鍵グループ。 例として、invite を指定します。 [デモユーザー](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

ネストされた 3 つのグループ（サブコミュニティ）がすべて表示されるように、ページを更新します。

Communities サイト コンソールからネストされたグループに移動するには：

* 「」を選択します **[!UICONTROL engage フォルダー]**
* を選択 **[!UICONTROL 入門チュートリアルカード]**
* 「」を選択します **[!UICONTROL グループ]** フォルダー
* を選択 **[!UICONTROL アーツカード]**
* 「」を選択します **[!UICONTROL グループ]** フォルダー

![create-new-group2](assets/create-new-group2.png)

## グループの公開 {#publishing-groups}

![publish-site](assets/publish-site.png)

メインコミュニティサイトを公開した後：

* 各グループを個別に公開します。

   * グループが公開されたかどうかの確認を待っています。

* 以下の場所にネストされているグループを公開する前に、親グループを公開します。

   * すべてのグループは、トップダウン方式で公開する必要があります。

![group-published](assets/group-published.png)

## パブリッシュ環境でのエクスペリエンス {#experience-on-publish}

ログイン時に様々なグループを体験することが可能です（例： [デモユーザー](/help/communities/tutorials.md#demo-users) 使用目的：

* アート/履歴グループ メンバー： `emily.andrews@mailinator.com/password`
   * 制限付き（秘密）グループの arts/history は次のように表示されます。
   * オプションの（パブリック）グループを表示できます。
   * 制限された（開いている）グループに参加できます。

* グループ マネージャー： `aaron.mcdonald@mailinator.com/password`

   * オプションの（パブリック）グループを表示できます。
   * 制限された（開いている）グループに参加できます。
   * 制限付き（秘密）グループを表示できません。

Communities へのアクセス [メンバーコンソールとグループコンソール](/help/communities/members.md) オーサーインスタンス上で、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加します。
