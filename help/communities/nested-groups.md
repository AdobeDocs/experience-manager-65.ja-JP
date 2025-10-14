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

* **[!UICONTROL Communities]**/**[!UICONTROL サイト]** を選択します。
* **[!UICONTROL engage フォルダー]** を選択して開きます。
* 英語サイト **[!UICONTROL はじめる前に]** チュートリアル）のカードを選択します。

   * カード画像を選択します。
   * アイコンを選択し *い* でください。

その結果、[&#x200B; グループコンソール &#x200B;](/help/communities/groups.md) にアクセスできます。

![create-group](assets/create-group.png)

groups 関数は、グループのインスタンスが作成されるフォルダーとして表示されます。 開くには、グループ フォルダーを選択します。 Publishで作成されたグループが表示されます。

![create-new-group](assets/create-new-group.png)

## メイン アート グループの作成 {#create-main-arts-group}

このグループを作成できるのは、エンゲージメントのためのサイト構造にグループの機能が含まれているからです。 サイトの `Reference Template` の関数の設定はデフォルトで、有効なグループテンプレートを選択できます。 したがって、この新しいグループ用に選択したテンプレートは `Reference Group` です。

これらのコンソールは、Communities サイトコンソールに似ています。

* 「**[!UICONTROL グループを作成]**」を選択します。

* **コミュニティ グループ テンプレート**:

   * **[!UICONTROL コミュニティグループのタイトル]**：アート
   * **[!UICONTROL コミュニティグループ説明]**：様々な芸術団体の親グループ
   * **[!UICONTROL コミュニティグループルート]**:*デフォルトのままにします*
   * **[!UICONTROL 追加の使用可能なコミュニティグループ言語]**：ドロップダウンメニューを使用して、使用可能なコミュニティグループ言語を選択します。 メニューには、親コミュニティサイトが作成されたすべての言語が表示されます。 ユーザーは、これらの言語から選択して、この単一の手順で複数のロケールでグループを作成できます。 同じグループが、それぞれのコミュニティサイトのグループコンソールで複数の指定された言語で作成されます。
   * **[!UICONTROL コミュニティグループ名]**: arts
   * **[!UICONTROL テンプレート]**：テンプレートを選択するためのドロップダウ `Reference Group`
   * 「**[!UICONTROL 次へ]**」を選択します。

![&#x200B; ネストされたコミュニティグループ &#x200B;](assets/parent-to-nestedgroup.png)

次の設定で他のパネルを続行します。

* **[!UICONTROL Design]**

   * デザインを変更するか、既定の親サイトのデザインを許可します。
   * 「**[!UICONTROL 次へ]**」を選択します。

* **[!UICONTROL 設定]**

   * **[!UICONTROL モデレート]**

      * 空のままにします（親サイトから継承）。

   * **[!UICONTROL 加入]**

      * デフォルトの `Optional Membership.` を使用

      * **[!UICONTROL サムネール]**
         * `optional.*`

      * **[!UICONTROL 「次へ」を選択します]**。

* 「**[!UICONTROL 作成]**」を選択します。

### アーツグループ内のグループのネスト {#nesting-groups-within-arts-group}

`groups` フォルダーに 2 つのグループが含まれるようになりました（ページを更新します）。

![&#x200B; グループのネスト &#x200B;](assets/create-community-group.png)

#### Publishグループ {#publish-group}

`arts` グループ内にネストされたグループを作成する前に、`arts` カードにカーソルを置いて「公開」アイコンを選択し、公開します。

![publish-site](assets/publish-site.png)

グループが公開されたことを確認します。

![&#x200B; グループ公開済み &#x200B;](assets/group-published.png)

`arts` のグループには、`groups` のフォルダーも含める必要がありますが、空のフォルダーで、新しいグループを作成できるフォルダーです。 アーツ グループ フォルダに移動し、ネストされた 3 つのグループを作成します。各グループには異なるメンバーシップ設定があります。

1. **[!UICONTROL ビジュアル]**

   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート：`Reference Group`
   * メンバーシップ：`Optional Membership` （パブリック グループ）を選択すると、すべてのメンバーに対して公開されます。

1. **[!UICONTROL 聴覚]**

   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート：`Reference Group`
   * メンバーシップ：メンバーが参加できる開かれたグループ「`Required Membership`」を選択します。

1. **[!UICONTROL 履歴]**

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート：`Reference Group`
   * メンバーシップ：招待メンバーにのみ表示される秘密グループ「`Restricted Membership`」を選択します。 例えば、[&#x200B; デモユーザー &#x200B;](/help/communities/tutorials.md#demo-users)`emily.andrews@mailinator.com` を招待します。

ネストされた 3 つのグループ（サブコミュニティ）がすべて表示されるように、ページを更新します。

Communities サイト コンソールからネストされたグループに移動するには：

* **[!UICONTROL engage フォルダー]** を選択します。
* **[!UICONTROL 入門チュートリアルカード]** を選択します
* **[!UICONTROL グループ]** フォルダーを選択します
* **[!UICONTROL アート カード]** を選択
* **[!UICONTROL グループ]** フォルダーを選択します

![create-new-group2](assets/create-new-group2.png)

## グループの公開 {#publishing-groups}

![publish-site](assets/publish-site.png)

メインコミュニティサイトを公開した後：

* 各グループを個別にPublishする：

   * グループが公開されたかどうかの確認を待っています。

* 以下の場所にネストされているグループを公開する前に、親グループをPublishします。

   * すべてのグループは、トップダウン方式で公開する必要があります。

![&#x200B; グループ公開済み &#x200B;](assets/group-published.png)

## Publishでのエクスペリエンス {#experience-on-publish}

次の目的で使用される [&#x200B; デモユーザー &#x200B;](/help/communities/tutorials.md#demo-users) などを使用して、ログイン時に様々なグループを体験できます。

* アート/履歴グループ メンバー：`emily.andrews@mailinator.com/password`
   * 制限付き（秘密）グループの arts/history は次のように表示されます。
   * オプションの（パブリック）グループを表示できます。
   * 制限された（開いている）グループに参加できます。

* グループ マネージャー：`aaron.mcdonald@mailinator.com/password`

   * オプションの（パブリック）グループを表示できます。
   * 制限された（開いている）グループに参加できます。
   * 制限付き（秘密）グループを表示できません。

作成者のコミュニティ [&#x200B; メンバーコンソールとグループコンソール &#x200B;](/help/communities/members.md) にアクセスして、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加します。
