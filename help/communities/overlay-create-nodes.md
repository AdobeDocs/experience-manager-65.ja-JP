---
title: ノードの作成
description: /libs から必要最小限の数のファイルをコピーし、/apps で編集することで、コメントシステムをカスタムバージョンでオーバーレイする方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

# ノードの作成 {#create-nodes}

必要最小限の数のファイルをからコピーして、コメントシステムをカスタムバージョンでオーバーレイします。 `/libs` into `/apps` を編集し、 `/apps`.

>[!CAUTION]
>
>/libs フォルダーの内容は編集されません。再インストールまたはアップグレードを行うと、/apps フォルダーの内容が変更されないまま、/libs フォルダーが削除または置き換えられる可能性があります。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) オーサーインスタンスで、まず、/libs フォルダー内のオーバーレイされたコンポーネントへのパスと同じパスを/apps フォルダーに作成します。

複製するパスは次のとおりです。

* `/libs/social/commons/components/hbs/comments/comment`

パス内の一部のノードはフォルダーで、一部はコンポーネントです。

1. 参照先 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 作成 `/apps/social` （まだ存在しない場合）
   * 選択 `/apps` ノード
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力: `social`
1. 選択 `social` ノード
   * **[!UICONTROL 作成]** > **[!UICONTROL フォルダー]**
      * 名前を入力: `commons`
1. 選択 `commons` ノード
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力: `components`
1. 選択 `components` ノード
   * **[!UICONTROL 作成/フォルダー]**.
      * 名前を入力: `hbs`
1. 選択 `hbs` ノード
   * **[!UICONTROL 作成]** > **[!UICONTROL コンポーネントを作成]**
      * ラベルを入力： `comments`
      * タイトルを入力： `Comments`
      * 説明を入力: `List of comments without showing avatars`
      * スーパータイプ：`social/commons/components/comments`
      * グループを入力： `Communities`
      * クリック **[!UICONTROL 次へ]** 次まで **[!UICONTROL OK]**
1. 選択 `comments` ノード

   * **[!UICONTROL 作成]** > **[!UICONTROL コンポーネントを作成]**

      * ラベルを入力： `comment`
      * タイトルを入力： `Comment`
      * 説明を入力: `A comment instance without avatars`
      * スーパータイプ：`social/commons/components/comments/comment`
      * グループを入力： `.hidden`
      * クリック **[!UICONTROL 次へ]** 次まで **[!UICONTROL OK]**
   * 選択 **[!UICONTROL すべて保存]**
1. デフォルトを削除 `comments.jsp`
   * ノードを選択 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選択 **[!UICONTROL 削除]**
1. デフォルトの comment.jsp を削除します。
   *  ノードを選択します`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選択 **[!UICONTROL 削除]**
   * 選択 **[!UICONTROL すべて保存]**

>[!NOTE]
>
>継承チェーンを保持するには、 `Super Type` （プロパティ） `sling:resourceSuperType`) がオーバーレイコンポーネントの `Super Type` オーバーレイされるコンポーネント（この場合は：）
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

オーバーレイ自体 `Type`（プロパティ） `sling:resourceType`) は、/apps に見つからないコンテンツが/libs 内で検索されるように、相対的な自己参照である必要があります。
* 名前：`sling:resourceType`
* タイプ：`String`
* 値：`social/commons/components/hbs/comments`

1. 緑を選択 `[+] Add`
   * 名前：`sling:resourceType`
   * タイプ：`String`
   * 値：`social/commons/components/hbs/comments/comment`
1. 緑を選択 `[+] Add`
   * 選択 **[!UICONTROL すべて保存]**

![create-nodes](assets/create-nodes.png)
