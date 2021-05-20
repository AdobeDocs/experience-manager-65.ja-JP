---
title: ネストされたグループの作成
seo-title: ネストされたグループの作成
description: ネストされたグループの作成
seo-description: ネストされたグループの作成
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 39%

---

# ネストされたグループの作成{#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

AEMオーサーインスタンスで、グローバルナビゲーションから次の操作を実行します。

* **[!UICONTROL コミュニティ]**/**[!UICONTROL サイト]**&#x200B;を選択します。
* **[!UICONTROL フォルダー]**&#x200B;を開きます。
* **[!UICONTROL Getting Started Tutorial]**&#x200B;英語のサイトのカードを選択します。

   * カード画像を選択します。
   * アイコンを&#x200B;*選択しないで*&#x200B;ください。

そうすると、[グループコンソール](/help/communities/groups.md)に移動します。

![create-group](assets/create-group.png)

グループ機能は、グループのインスタンスが作成されるフォルダーとして表示されます。グループフォルダーを選択して、開きます。パブリッシュ環境で作成されたグループが表示されます。

![create-new-group](assets/create-new-group.png)

## メインの Arts グループの作成 {#create-main-arts-group}

このグループを作成できるのは、engage のサイト構造にグループ機能が含まれているからです。サイトの`Reference Template`での機能の設定は、デフォルトで、有効なグループテンプレートを選択できるようになっています。 したがって、この新しいグループに対して選択されるテンプレートは`Reference Group`です。

これらのコンソールは、コミュニティサイトコンソールに似ています。

* 「**[!UICONTROL グループを作成]**」を選択します。

* **コミュニティグループテンプレート**：

   * **[!UICONTROL コミュニティグループのタイトル]**:芸術。
   * **[!UICONTROL コミュニティグループの説明]**:様々な芸術グループの親グループ。
   * **[!UICONTROL コミュニティグループのルート]**: *をデフォルトのままにします*。
   * **[!UICONTROL 追加の利用可能なコミュニティグループの言語]**:ドロップダウンメニューを使用して、使用可能なコミュニティグループの言語を選択します。このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。
   * **[!UICONTROL コミュニティグループ名]**:芸術
   * **[!UICONTROL テンプレート]**:ドロップダウンして選択  `Reference Group.`
   * 「**[!UICONTROL 次へ]**」を選択します。

![ネストされたコミュニティグループ](assets/parent-to-nestedgroup.png)

引き続き、他のパネルで以下の値を設定します。

* **[!UICONTROL デザイン]**

   * デザインを変更するか、既定の親サイトのデザインを許可します。
   * 「**[!UICONTROL 次へ]**」を選択します。

* **[!UICONTROL 設定]**

   * **[!UICONTROL モデレート]**

      * 空のままにします（親サイトから継承）。
   * **[!UICONTROL メンバーシップ]**

      * デフォルトの`Optional Membership.`を使用

      * **[!UICONTROL サムネール]**
         * `optional.*`
      * **[!UICONTROL 「次へ]**」を選択します。



* 「**[!UICONTROL 作成]**」を選択します。

### Arts グループ内でのグループのネスト {#nesting-groups-within-arts-group}

`groups`フォルダーに2つのグループが含まれるようになりました（ページを更新）。

![グループのネスト](assets/create-community-group.png)

#### グループの公開 {#publish-group}

`arts` グループ内でネストされるグループを作成する前に、`arts` カードにカーソルを合わせ、公開アイコンを選択してそのグループを公開します。

![publish-site](assets/publish-site.png)

グループが公開されたことが確認されるまで待機します。

![グループ公開済み](assets/group-published.png)

`arts`グループには`groups`フォルダーも含める必要がありますが、フォルダーは空で、新しいグループを作成できます。 artsグループフォルダーに移動し、ネストされた3つのグループを作成し、それぞれ異なるメンバーシップ設定を持ちます。

1. **[!UICONTROL ビジュアル]**

   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Optional Membership`（パブリック・グループ）を選択し、すべてのメンバーに対して開きます。

1. **[!UICONTROL Auditory]**

   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Required Membership`を選択します。開いたグループは、メンバーが参加できます。

1. **[!UICONTROL History]**

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Restricted Membership`を選択します。これは、招待されたメンバーにのみ表示される秘密グループです。 例えば、[デモユーザー](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`を招待します。

ページを更新して、ネストされた 3 つのグループ（サブコミュニティ）すべてを表示します。

コミュニティサイトコンソールからネストされたグループに移動するには：

* **[!UICONTROL engage folder]**&#x200B;を選択します。
* **[!UICONTROL Getting Started Tutorial card]**&#x200B;を選択します。
* **[!UICONTROL Groups]**&#x200B;フォルダーを選択します
* **[!UICONTROL arts card]**&#x200B;を選択します。
* **[!UICONTROL Groups]**&#x200B;フォルダーを選択します

![create-new-group2](assets/create-new-group2.png)

## グループの公開 {#publishing-groups}

![publish-site](assets/publish-site.png)

メインコミュニティサイトを公開した後：

* 各グループを個別に公開する：

   * グループが公開されたことを確認するのを待っています。

* 次の中にネストされたグループを公開する前に、親グループを公開する：

   * すべてのグループは、トップダウン方式で公開する必要があります。

![グループ公開済み](assets/group-published.png)

## パブリッシュ環境でのエクスペリエンス {#experience-on-publish}

サインイン時に様々なグループを体験できます。例えば、次の用途に[demo users](/help/communities/tutorials.md#demo-users)を使用します。

* Art/History グループメンバー：emily.andrews@mailinator.com／password
   * 制限された（秘密の）グループ、arts/historyが表示されます。
   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いた）グループに参加できます。

* グループマネージャー：aaron.mcdonald@mailinator.com／password

   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いた）グループに参加できます。
   * 制限付き（シークレット）グループを表示できません。

オーサー環境で Communities の[メンバーコンソールとグループコンソール](/help/communities/members.md)にアクセスすると、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加できます。
