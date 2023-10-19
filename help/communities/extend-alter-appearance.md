---
title: 外観の変更（HBS）
description: HBS スクリプトを編集して外観 (HBS) を変更する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 3%

---

# 外観の変更（HBS） {#alter-the-appearance-hbs}

アプリケーションディレクトリ (/apps) 内のカスタムコメントシステムのコンポーネントが配置され、resourceSuperType がデフォルトのコメントシステムを参照し、カスタムのモデル/ビューが登録された状態で、実装を編集できます。

シンプルなデモの場合、ビジュアル機能（コメントを投稿するサインインユーザーに表示されるアバター）は削除されます。

>[!NOTE]
>
>この拡張機能を使用するには、影響を受ける Web サイト内のコメントシステムのインスタンス (/content) で、その resourceType をカスタムコメントシステムに設定する必要があります。

## HBS スクリプトの変更 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 開く [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * コメント投稿のアバターを含むタグをコメントアウトします（21 行目前後）。

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* 開く [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 次のコメントエントリのアバターを含むタグをコメントアウトします（44 行目前後）。

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* 選択 **すべて保存**

### カスタムアプリをレプリケート {#replicate-custom-app}

アプリケーションを変更した後、カスタムコンポーネントを再レプリケートする必要があります。

その方法の 1 つは次のとおりです。

* メインメニューから

   * 選択 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL レプリケーション]**.
   * 選択 **[!UICONTROL ツリーをアクティベート]**.
   * 設定 `Start Path` から `/apps/custom`.
   * 選択を解除 **[!UICONTROL 変更済みのみ]**.
   * 選択 **[!UICONTROL 有効化]** 」ボタンをクリックします。

### 公開済みサンプルページで変更済みコメントを表示 {#view-modified-comment-on-published-sample-page}

[エクスペリエンスの継続](/help/communities/extend-sample-page.md#publish-sample-page) パブリッシュインスタンスでは、同じユーザーとしてサインインしたままで、パブリッシュ環境でページを更新して、アバターを削除するための変更を表示できます。

![view-modified-content](assets/view-modified-content.png)

### サンプルコメント拡張パッケージ {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージが添付されています。

[ファイルを入手](assets/sample-comment-extension-6-1-fp3.zip)
