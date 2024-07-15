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

`/libs` から `/apps` に必要な最小限のファイルをコピーし、`/apps` で変更することで、コメントシステムにカスタムバージョンをオーバーレイします。

>[!CAUTION]
>
>/libs フォルダーの内容は編集されません。/apps フォルダーの内容はそのままの状態で、再インストールやアップグレードをおこなうと、/libs フォルダーが削除または置き換えられる可能性があるからです。

オーサーインスタンスで ](../../help/sites-developing/developing-with-crxde-lite.md)0}CRXDE Lite} を使用する場合は、まず/apps フォルダーに、/libs フォルダーのオーバーレイされたコンポーネントへのパスと同じパスを作成します。[

複製されるパスは次のとおりです。

* `/libs/social/commons/components/hbs/comments/comment`

パスのノードには、フォルダーやコンポーネントなどがあります。

1. [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) を参照します
1. `/apps/social` を作成（まだ存在しない場合）
   * ノード `/apps` 選択
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力：`social`
1. ノード `social` 選択
   * **[!UICONTROL 作成]**/**[!UICONTROL フォルダー]**
      * 名前を入力：`commons`
1. ノード `commons` 選択
   * **[!UICONTROL 作成/フォルダー]**
      * 名前を入力：`components`
1. ノード `components` 選択
   * **[!UICONTROL 作成/フォルダー]** を選択します。
      * 名前を入力：`hbs`
1. ノード `hbs` 選択
   * **[!UICONTROL 作成]**/**[!UICONTROL コンポーネントを作成]**
      * ラベルを入力：`comments`
      * タイトルを入力：`Comments`
      * 説明を入力：`List of comments without showing avatars`
      * スーパータイプ：`social/commons/components/comments`
      * グループを入力：`Communities`
      * **[!UICONTROL OK]** まで **[!UICONTROL 次へ]** をクリックします
1. ノード `comments` 選択

   * **[!UICONTROL 作成]**/**[!UICONTROL コンポーネントを作成]**

      * ラベルを入力：`comment`
      * タイトルを入力：`Comment`
      * 説明を入力：`A comment instance without avatars`
      * スーパータイプ：`social/commons/components/comments/comment`
      * グループを入力：`.hidden`
      * **[!UICONTROL OK]** まで **[!UICONTROL 次へ]** をクリックします
   * 「**[!UICONTROL すべて保存]**」を選択します。
1. デフォルトの `comments.jsp` を削除
   * ノード `/apps/social/commons/components/hbs/comments/comments.jsp` を選択
   * 「**[!UICONTROL 削除]**」を選択します。
1. デフォルトの comment.jsp を削除します
   * ノード `/apps/social/commons/components/hbs/comments/comment/comment.jsp` を選択
   * 「**[!UICONTROL 削除]**」を選択します。
   * 「**[!UICONTROL すべて保存]**」を選択します。

>[!NOTE]
>
>継承チェーンを維持するために、オーバーレイコンポーネントの `Super Type` （プロパティ `sling:resourceSuperType`）は、オーバーレイされるコンポーネントの `Super Type` と同じ値に設定されます。この場合は、次のようになります。
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

オーバーレイ自体の `Type` （プロパティ `sling:resourceType`）は、/apps に見つからないコンテンツが/libs で検索されるように、相対自己参照である必要があります。
* 名前：`sling:resourceType`
* タイプ：`String`
* 値：`social/commons/components/hbs/comments`

1. 緑の `[+] Add` を選択します
   * 名前：`sling:resourceType`
   * タイプ：`String`
   * 値：`social/commons/components/hbs/comments/comment`
1. 緑の `[+] Add` を選択します
   * 「**[!UICONTROL すべて保存]**」を選択します。

![create-nodes](assets/create-nodes.png)
