---
title: ネストされたグループの作成
seo-title: Authoring Nested Groups
description: ネストされたグループの作成
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 39%

---

# ネストされたグループの作成{#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

AEM オーサーインスタンスで、グローバルナビゲーションから次の操作を実行します。

* 選択 **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* 選択 **[!UICONTROL エンゲージフォルダー]** 開ける
* のカードを選択します。 **[!UICONTROL 入門チュートリアル]** 英語のサイト。

   * カード画像を選択します。
   * ドー *not* アイコンを選択します。

そうすると、[グループコンソール](/help/communities/groups.md)に移動します。

![create-group](assets/create-group.png)

グループ機能は、グループのインスタンスが作成されるフォルダーとして表示されます。グループフォルダーを選択して、開きます。パブリッシュ環境で作成されたグループが表示されます。

![create-new-group](assets/create-new-group.png)

## メインの Arts グループの作成 {#create-main-arts-group}

このグループを作成できるのは、engage のサイト構造にグループ機能が含まれているからです。サイトの `Reference Template` デフォルトでは、有効なグループテンプレートを選択できます。 したがって、この新しいグループ用に選択されたテンプレートは、 `Reference Group`.

これらのコンソールは、コミュニティサイトコンソールに似ています。

* 選択 **[!UICONTROL グループの作成]**

* **コミュニティグループテンプレート**：

   * **[!UICONTROL コミュニティグループのタイトル]**:Arts
   * **[!UICONTROL コミュニティグループの説明]**:様々な芸術団体の親集団
   * **[!UICONTROL コミュニティグループのルート]**: *デフォルトのままにする*
   * **[!UICONTROL 追加の利用可能なコミュニティグループの言語]**:ドロップダウンメニューを使用して、使用可能なコミュニティグループの言語を選択します。 このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。
   * **[!UICONTROL コミュニティグループ名]**:芸術
   * **[!UICONTROL テンプレート]**:ドロップダウンして選択 `Reference Group`
   * 「**[!UICONTROL 次へ]**」を選択します。

![ネストされたコミュニティグループ](assets/parent-to-nestedgroup.png)

引き続き、他のパネルで以下の値を設定します。

* **[!UICONTROL デザイン]**

   * デザインを変更するか、既定の親サイトのデザインを許可します。
   * 「**[!UICONTROL 次へ]**」を選択します。

* **[!UICONTROL 設定]**

   * **[!UICONTROL モデレート]**

      * 空のまま（親サイトから継承）。
   * **[!UICONTROL メンバーシップ]**

      * デフォルトを使用 `Optional Membership.`

      * **[!UICONTROL サムネール]**
         * `optional.*`
      * **[!UICONTROL 「次へ]**」を選択します。



* 「**[!UICONTROL 作成]**」を選択します。

### Arts グループ内でのグループのネスト {#nesting-groups-within-arts-group}

10. `groups` フォルダーに 2 つのグループが含まれるようになりました（ページを更新）。

![グループのネスト](assets/create-community-group.png)

#### グループの公開 {#publish-group}

`arts` グループ内でネストされるグループを作成する前に、`arts` カードにカーソルを合わせ、公開アイコンを選択してそのグループを公開します。

![publish-site](assets/publish-site.png)

グループが公開されたことが確認されるまで待機します。

![グループ公開済み](assets/group-published.png)

10. `arts` グループにも `groups` フォルダーです。ただし、空で、新しいグループを作成できるフォルダーです。 arts グループフォルダーに移動し、ネストされた 3 つのグループを作成し、それぞれ異なるメンバーシップ設定を持ちます。

1. **[!UICONTROL ビジュアル]**

   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート: `Reference Group`
   * メンバーシップ：select `Optional Membership`（すべてのメンバーに対して開かれるパブリックグループ）。

1. **[!UICONTROL Auditory]**

   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート: `Reference Group`
   * メンバーシップ：select `Required Membership`：メンバーが参加できる、開いたグループ。

1. **[!UICONTROL History]**

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート: `Reference Group`
   * メンバーシップ：select `Restricted Membership`：シークレット・グループ。招待されたメンバーにのみ表示されます。 例として、 [デモユーザー](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

ページを更新して、ネストされた 3 つのグループ（サブコミュニティ）すべてを表示します。

コミュニティサイトコンソールからネストされたグループに移動するには：

* 選択 **[!UICONTROL エンゲージフォルダー]**
* 選択 **[!UICONTROL はじめにチュートリアルカード]**
* 選択 **[!UICONTROL グループ]** フォルダー
* 選択 **[!UICONTROL アートカード]**
* 選択 **[!UICONTROL グループ]** フォルダー

![create-new-group2](assets/create-new-group2.png)

## グループの公開 {#publishing-groups}

![publish-site](assets/publish-site.png)

メインコミュニティサイトを公開した後：

* 各グループを個別に公開します。

   * グループが公開されたことを確認するのを待っています。

* 親グループを公開してから、次の中にネストされたグループを公開します。

   * すべてのグループは、トップダウン方式で公開する必要があります。

![グループ公開済み](assets/group-published.png)

## パブリッシュ環境でのエクスペリエンス {#experience-on-publish}

様々なグループを使用して、例えば [デモユーザー](/help/communities/tutorials.md#demo-users) 次に使用します。

* Art/History グループメンバー：emily.andrews@mailinator.com／password
   * 制限された（秘密の）グループ、arts/history が表示されます。
   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いた）グループに参加できます。

* グループマネージャー：aaron.mcdonald@mailinator.com／password

   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いた）グループに参加できます。
   * 制限付き（シークレット）グループを表示できません。

オーサー環境で Communities の[メンバーコンソールとグループコンソール](/help/communities/members.md)にアクセスすると、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加できます。
