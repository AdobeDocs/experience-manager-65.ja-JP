---
title: 外観の変更（HBS）
description: HBS スクリプトを編集して外観（HBS）を変更する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# 外観の変更（HBS） {#alter-the-appearance-hbs}

これで、アプリケーションディレクトリ（/apps）内のカスタムコメントシステムのコンポーネントが配置され、resourceSuperType がデフォルトのコメントシステムを参照し、カスタムモデル/ビューが登録されたので、実装を編集できます。

簡単なデモの場合、コメントを投稿するログイン ユーザーのアバター（視覚的機能）が削除されます。

>[!NOTE]
>
>この拡張機能を使用するには、影響を受ける web サイト内のコメントシステムのインスタンス（/content）が、その resourceType をカスタムコメントシステムに設定する必要があります。

## HBS スクリプトの変更 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 開く [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * コメント投稿のアバターを含むタグをコメントアウトします（21 行目まで）。

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* 開く [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 次のコメントエントリのアバターを含むタグをコメントアウトします（44 行目まで）。

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* を選択 **すべて保存**

### カスタムアプリをレプリケート {#replicate-custom-app}

アプリケーションを変更したら、カスタムコンポーネントを再度レプリケートする必要があります。

その方法の 1 つは次のとおりです。

* メインメニューから

   * を選択 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL 複製]**.
   * を選択 **[!UICONTROL ツリーのアクティベート]**.
   * を設定 `Start Path` 対象： `/apps/custom`.
   * 選択を解除 **[!UICONTROL 変更済みのみ]**.
   * を選択 **[!UICONTROL Activate]** ボタン。

### 公開されたサンプルページでの変更されたコメントの表示 {#view-modified-comment-on-published-sample-page}

[エクスペリエンスの継続](/help/communities/extend-sample-page.md#publish-sample-page) 同じユーザーとしてログインしているパブリッシュインスタンスで、パブリッシュ環境のページを更新して、変更を表示し、アバターを削除できるようになりました。

![view-modified-content](assets/view-modified-content.png)

### コメント拡張機能パッケージのサンプル {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージを添付しました。

[ファイルを入手](assets/sample-comment-extension-6-1-fp3.zip)
