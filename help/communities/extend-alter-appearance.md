---
title: 外観の変更（HBS）
seo-title: 外観の変更
description: HBS スクリプトの変更
seo-description: HBS スクリプトの変更
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 58%

---


# 外観の変更 (HBS) {#alter-the-appearance-hbs}

カスタムコメントシステムのコンポーネントがアプリケーションディレクトリ（/apps）に配置され、デフォルトのコメントシステムおよびカスタムモデル／ビューを参照する resourceSuperType が登録されたので、実装を変更できるようになりました。

簡単なデモのために、ビジュアル機能（コメントを投稿するサインインユーザーについて表示されるアバター）を削除します。

>[!NOTE]
>
>この拡張機能を使用するには、影響を受けるWebサイト内のコメントシステムのインスタンス(/content)で、そのresourceTypeをカスタムコメントシステムに設定する必要があります。

## HBS スクリプトの変更 {#modify-the-hbs-scripts}

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)を開きます。

   * コメント投稿のアバターを含むタグをコメントアウトします（～行21）。

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)を開きます。

   * 次のコメントエントリ用のアバターを含むタグをコメントアウトします（～行44）。

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 「**すべて保存**」を選択します。

### カスタムアプリのレプリケート {#replicate-custom-app}

アプリケーションを変更した後で、カスタムコンポーネントを再レプリケートする必要があります。

その方法の1つは、次のとおりです。

* メインメニューから

   * **[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL レプリケーション]**&#x200B;を選択します。
   * 「**[!UICONTROL ツリーをアクティブ化]**」を選択します。
   * `Start Path`を`/apps/custom`に設定します。
   * 「**[!UICONTROL 変更済み]**&#x200B;のみ」を選択解除します。
   * **[!UICONTROL 「]**&#x200B;アクティブ化」ボタンを選択します。

### 公開済みサンプルページでの変更されたコメントの表示 {#view-modified-comment-on-published-sample-page}

パブリッシュインスタンスで[エクスペリエンスを続行](/help/communities/extend-sample-page.md#publish-sample-page)すると、同じユーザーとしてサインインしたまま、パブリッシュ環境でページを更新してアバターを削除する変更を表示できます。

![表示変更内容](assets/view-modified-content.png)

### サンプルコメント拡張パッケージ {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージが添付されています。

[ファイルを入手](assets/sample-comment-extension-6-1-fp3.zip)
