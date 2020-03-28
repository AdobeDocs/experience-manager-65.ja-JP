---
title: コンポーネントの作成
seo-title: コンポーネントの作成
description: コメントコンポーネントの作成
seo-description: コメントコンポーネントの作成
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# コンポーネントの作成  {#create-the-components}

コンポーネントを拡張する例では、実際には次の 2 つのコンポーネントで構成されるコメントシステムを使用します。

* コメント — ページに配置されるコンポーネントである包括コメントシステム。
* コメント — 投稿されたコメントのインスタンスをキャプチャするコンポーネント。

投稿されたコメントの外観をカスタマイズする場合は特に、両方のコンポーネントを配置する必要があります。

>[!NOTE]
>
>1 つのサイトページで使用できるコメントシステムは 1 つのみです。
>
>多くのコミュニティ機能には、拡張されたコメントシステムを参照するように resourceType を変更できるコメントシステムが既に含まれています。

## コメントコンポーネントの作成 {#create-the-comments-component}

These directions specify a **Group** value other than `.hidden` so the component may be made available from the component browser (sidekick).

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. **CRXDE Lite**（[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)）を表示します。

1. カスタムアプリケーションの場所の作成：

   * Select the `/apps` node

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL custom]** という名前のフォルダーを作成します。
   * Select the `/apps/custom` node

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL components]** という名前のフォルダーを作成します。


1. Select the `/apps/custom/components` node

   * **[!UICONTROL 作成／コンポーネント...]** を選択します。

      * **ラベル**:コメン *ト*
      * **タイトル**：Alt Comments **
      * **説明**：Alternative comments style **
      * **スーパータイプ**：social/commons/components/hbs/comments **
      * **グループ**：Custom **
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。


1. Expand the node just created: `/apps/custom/components/comments`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. Right-click `comments.jsp`
1. Select **[!UICONTROL Delete]**
1. 「**[!UICONTROL すべて保存]**」を選択します。

![chlimage_1-70](assets/chlimage_1-70.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

These directions set **Group** to `.hidden` as only the parent component should be included within a page.

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. ノードに移動しま `/apps/custom/components/comments` す。
1. ノードを右クリック

   * **[!UICONTROL 作成／コンポーネント...]** を選択します。

      * **ラベル**：comment **
      * **タイトル**：Alt Comment **
      * **説明**：Alternative comment style **
      * **スーパータイプ**：social/commons/components/hbs/comments/comment **
      * **グループ**: `*.hidden*`
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。


1. Expand the node just created: `/apps/custom/components/comments/comment`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. Right-click `comment.jsp`
1. Select **[!UICONTROL Delete]**
1. 「**[!UICONTROL すべて保存]**」を選択します。

![chlimage_1-71](assets/chlimage_1-71.png)![chlimage_1-72](assets/chlimage_1-72.png)

### デフォルトの HBS スクリプトのコピーと変更 {#copy-and-modify-the-default-hbs-scripts}

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* コピー `comments.hbs`

   * From [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * To [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編集 `comments.hbs` 先：

   * Change the value of the `data-scf-component` attribute (~line 20):

      * 送信元 `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * カスタムコメントコンポーネント（～75行目）を含めるように変更します。

      * 置換 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * を次のタグに置換します。`{{include this resourceType='/apps/custom/components/comments/comment'}}`


* コピー `comment.hbs`

   * From [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * To [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編集 `comment.hbs` 先：

   * data-scf-component属性の値の変更（～行19）

      * 送信元 `social/commons/components/hbs/comments/comment`
      * To `/apps/custom/components/comments/comment`

* ノードを `/apps/custom` 選択
* 「**[!UICONTROL すべて保存]**」を選択します。

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリを明示的に含めなくても済むように、デフォルトのコメントシステムの clientlib の categories 値（`cq.social.author.hbs.comments`）を使用できますが、これを使用すると、デフォルトのコンポーネントのすべてのインスタンスについても、この clientlib が含まれるようになります。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* ノードを `/apps/custom/components/comments` 選択
* Select **[!UICONTROL Create Node]**

   * **名前**: `clientlibs`
   * **Type**: `cq:ClientLibraryFolder`
   * Add to **[!UICONTROL Properties]** tab:

      * **Name** Type `categories` Value ****`String` net ****`cq.social.author.hbs.comments` , `Multi`
      * **Name** Type `dependencies` Value ****`String` net ****`cq.social.scf` , `Multi`

* 「**[!UICONTROL すべて保存]**」を選択します。
* sノード `/apps/custom/components/comments/clientlib`を選択し、次の3つのファイルを作成します。

   * **名前**: `css.txt`
   * **名前**: `js.txt`
   * **名前**：customcommentsystem.js

* Enter &#39;customcommentsystem.js&#39; as the content of `js.txt`
* 「**[!UICONTROL すべて保存]**」を選択します。

![chlimage_1-73](assets/chlimage_1-73.png)

## SCF モデルおよびビューの登録 {#register-the-scf-model-view}

When extending (overriding) an SCF component, the resourceType is different (overlaying makes use of the relative search mechanism that searches through `/apps` before `/libs` so that the resourceType remains the same). このため、カスタムresourceTypeのSCF JSモデルと表示を登録するために、JavaScriptを（クライアントライブラリで）作成する必要があります。

Enter the following text as the content of `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* 「**[!UICONTROL すべて保存]**」を選択します。

## アプリの公開 {#publish-the-app}

拡張されたコンポーネントをパブリッシュ環境で確認するには、カスタムコンポーネントをレプリケートする必要があります。

その一つの方法は

* グローバルナビゲーションから

   * Select **[!UICONTROL Tools > Deployment > Replication]**
   *  `Activate Tree`
   * 設定 `Start Path`:to `/apps/custom`
   * Uncheck `Only Modified`
   * 選択ボ `Activate`タン

