---
title: 外観の変更（HBS）
description: HBS スクリプトを編集して、外観（HBS）を変更する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%
---
# 外観の変更（HBS） {#alter-the-appearance-hbs}

アプリケーションディレクトリ（/apps）のカスタムコメントシステムのコンポーネントが配置され、resourceSuperTypeがデフォルトのコメントシステムを参照し、カスタムモデル/ビューが登録されたので、実装を編集できます。

簡単なデモでは、ビジュアル機能である、コメントを投稿したサインインユーザーのアバターが削除されます。

>[!NOTE]
>
>この拡張機能を使用するには、影響を受けるweb サイト内のコメントシステムのインスタンス（/content）が、そのresourceTypeをカスタムコメントシステムに設定する必要があります。

## HBS スクリプトの変更 {#modify-the-hbs-scripts}

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)を使用：

* [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)を開きます

  * コメント投稿（～ 21行目）のアバターを含むタグをコメントアウトします。

    ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
    ```

* [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)を開きます

  * 次のコメントエントリ（～ 44行目）のアバターを含むタグをコメントアウトします。

    ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
    ```

* **すべて保存**&#x200B;を選択

### カスタムアプリのレプリケート {#replicate-custom-app}

アプリケーションを変更した後、カスタムコンポーネントを再レプリケートする必要があります。

そのひとつの方法は次のとおりです。

* メインメニューから

  * **[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL レプリケーション]**&#x200B;を選択します。
  * 「**[!UICONTROL ツリーをアクティブ化]**」を選択します。
  * `Start Path`を`/apps/custom`に設定します。
  * **[!UICONTROL 変更済みのみ]**&#x200B;の選択を解除します。
  * 「**[!UICONTROL アクティブ化]**」ボタンを選択します。

### 公開したサンプルページに対する変更されたコメントの表示 {#view-modified-comment-on-published-sample-page}

[&#x200B; パブリッシュインスタンスでエクスペリエンス &#x200B;](/help/communities/extend-sample-page.md#publish-sample-page)を続行し、同じユーザーとしてサインインしたまま、パブリッシュ環境でページを更新して、アバターを削除するための変更を表示できるようになりました。

![view-modified-content](assets/view-modified-content.png)

### コメント拡張機能パッケージのサンプル {#sample-comment-extension-package}

このチュートリアルで作成したカスタムコメントアプリケーションのパッケージが添付されています。

[ファイルの取得](assets/sample-comment-extension-6-1-fp3.zip)
