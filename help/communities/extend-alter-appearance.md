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
source-git-commit: 618464d1e01986786a47a4e9c6ecce87e2a77ec3
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

* Open [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * コメント投稿のアバターを含むタグをコメントアウトします（～行21）。

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Open [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

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

   * Select **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**.
   * Select **[!UICONTROL Activate Tree]**.
   * に設定 `Start Path` し `/apps/custom`ます。
   * 「変更 **[!UICONTROL 済みのみ]**」の選択を解除します。
   * Select **[!UICONTROL Activate]** button.

### 公開済みサンプルページでの変更されたコメントの表示 {#view-modified-comment-on-published-sample-page}

パブリッシュインスタンスで[エクスペリエンスを続行](/help/communities/extend-sample-page.md#publish-sample-page)すると、同じユーザーとしてサインインしたまま、パブリッシュ環境でページを更新してアバターを削除する変更を表示できます。

![chlimage_1-81](assets/chlimage_1-81.png)

### サンプルコメント拡張パッケージ {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージが添付されています。

[ファイルを入手](assets/sample-comment-extension-6-1-fp3.zip)
