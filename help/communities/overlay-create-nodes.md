---
title: ノードの作成
description: /libs から必要な最小限のファイル数をコピーして/apps で編集することで、コメントシステムをカスタムバージョンでオーバーレイする方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 6%

---

# ノードの作成 {#create-nodes}

必要な最小限のファイルをコピーして、コメントシステムをカスタムバージョンでオーバーレイします。 `/libs` 対象 `/apps` および内で修正する `/apps`.

>[!CAUTION]
>
>/libs フォルダーの内容は編集されません。/apps フォルダーの内容はそのままの状態で、再インストールやアップグレードをおこなうと、/libs フォルダーが削除または置き換えられる可能性があるからです。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) オーサーインスタンスでは、まず/apps フォルダーに、/libs フォルダーのオーバーレイコンポーネントへのパスと同じパスを作成します。

複製されるパスは次のとおりです。

* `/libs/social/commons/components/hbs/comments/comment`

パスのノードには、フォルダーやコンポーネントなどがあります。

1. を参照 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 作成 `/apps/social` （まだ存在しない場合）
   * を選択 `/apps` ノード
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力： `social`
1. を選択 `social` ノード
   * **[!UICONTROL 作成]** > **[!UICONTROL フォルダー]**
      * 名前を入力： `commons`
1. を選択 `commons` ノード
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力： `components`
1. を選択 `components` ノード
   * **[!UICONTROL 作成/フォルダー]**.
      * 名前を入力： `hbs`
1. を選択 `hbs` ノード
   * **[!UICONTROL 作成]** > **[!UICONTROL コンポーネントを作成]**
      * ラベルを入力： `comments`
      * タイトルを入力： `Comments`
      * 説明を入力： `List of comments without showing avatars`
      * スーパータイプ：`social/commons/components/comments`
      * グループを入力： `Communities`
      * クリック **[!UICONTROL 次]** まで **[!UICONTROL OK]**
1. を選択 `comments` ノード

   * **[!UICONTROL 作成]** > **[!UICONTROL コンポーネントを作成]**

      * ラベルを入力： `comment`
      * タイトルを入力： `Comment`
      * 説明を入力： `A comment instance without avatars`
      * スーパータイプ：`social/commons/components/comments/comment`
      * グループを入力： `.hidden`
      * クリック **[!UICONTROL 次]** まで **[!UICONTROL OK]**
   * を選択 **[!UICONTROL すべて保存]**
1. デフォルトを削除 `comments.jsp`
   * ノードを選択 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 「**[!UICONTROL 削除]**」を選択します。
1. デフォルトの comment.jsp を削除します
   * ノードを選択 `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 「**[!UICONTROL 削除]**」を選択します。
   * を選択 **[!UICONTROL すべて保存]**

>[!NOTE]
>
>継承チェーンを保持するには、 `Super Type` （プロパティ `sling:resourceSuperType`）を選択します。選択したコンポーネントと同じ値に設定されます。 `Super Type` オーバーレイされるコンポーネントのうち、この場合は次のようになります。
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

オーバーレイ独自の `Type`（プロパティ `sling:resourceType`）は、/apps に見つからないコンテンツが/libs で検索されるように、相対自己参照である必要があります。
* 名前：`sling:resourceType`
* タイプ：`String`
* 値：`social/commons/components/hbs/comments`

1. グリーンを選択 `[+] Add`
   * 名前：`sling:resourceType`
   * タイプ：`String`
   * 値：`social/commons/components/hbs/comments/comment`
1. グリーンを選択 `[+] Add`
   * を選択 **[!UICONTROL すべて保存]**

![create-nodes](assets/create-nodes.png)
