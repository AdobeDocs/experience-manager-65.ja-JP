---
title: コンポーネントの作成
description: コメントおよびコメントコンポーネントで構成されるコメントシステムを使用して、コンポーネントを拡張する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# コンポーネントの作成  {#create-the-components}

コンポーネントの拡張の例では、2 つのコンポーネントで構成されるコメントシステムを使用します。

* コメント — ページ上に配置されるコンポーネントである包括的なコメントシステム。
* コメント — 投稿されたコメントのインスタンスをキャプチャするコンポーネント。

投稿されたコメントの外観をカスタマイズする場合は特に、両方のコンポーネントを配置する必要があります。

>[!NOTE]
>
>サイトページごとに 1 つのコメントシステムのみ使用できます。
>
>多くのコミュニティ機能には既にコメントシステムが含まれています。このコメントシステムでは、resourceType を変更して拡張コメントシステムを参照できます。

## コメントコンポーネントの作成 {#create-the-comments-component}

これらの方向では、 **グループ化** 以外の値 `.hidden` そのため、コンポーネントをコンポーネントブラウザー（サイドキック）から使用できるようにします。

自動作成された JSP ファイルは、代わりにデフォルトの HBS ファイルが使用されるので、削除されます。

1. 参照先 **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. カスタムアプリケーションの場所を作成します。

   * を選択します。 `/apps` ノード

      * **フォルダーを作成** 名前付き **[!UICONTROL カスタム]**

   * を選択します。 `/apps/custom` ノード

      * **フォルダーを作成** 名前付き **[!UICONTROL コンポーネント]**

1. を選択します。 `/apps/custom/components` ノード

   * **[!UICONTROL 作成/コンポーネント…]**

      * **ラベル**: *コメント*
      * **タイトル**: *Alt コメント*
      * **説明**: *代替のコメントスタイル*
      * **スーパータイプ**: *social/commons/components/hbs/comments*
      * **グループ化**: *カスタム*

   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL OK]**

1. 作成したノードを展開します。 `/apps/custom/components/comments`
1. 選択 **[!UICONTROL すべて保存]**
1. 右クリック `comments.jsp`
1. 選択 **[!UICONTROL 削除]**
1. 選択 **[!UICONTROL すべて保存]**

![create-component](assets/create-component.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

これらの方向は設定されました **グループ化** から `.hidden` 親コンポーネントのみをページ内に含める必要があるので。

自動作成された JSP ファイルは、代わりにデフォルトの HBS ファイルが使用されるので、削除されます。

1. 次に移動： `/apps/custom/components/comments` ノード
1. ノードを右クリックします。

   * 選択 **[!UICONTROL 作成]** > **[!UICONTROL コンポーネント…]**

      * **ラベル**: *コメント*
      * **タイトル**: *代替コメント*
      * **説明**: *代替のコメントスタイル*
      * **スーパータイプ**: *social/commons/components/hbs/comments/comment*
      * **グループ**：`*.hidden*`

   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL 次へ]**
   * 選択 **[!UICONTROL OK]**

1. 作成したノードを展開します。 `/apps/custom/components/comments/comment`
1. 選択 **[!UICONTROL すべて保存]**
1. 右クリック `comment.jsp`
1. 選択 **[!UICONTROL 削除]**
1. 選択 **[!UICONTROL すべて保存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### デフォルトの HBS スクリプトをコピーして変更する {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* コピー `comments.hbs`

   * 送信者 [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 宛先 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編集 `comments.hbs` 移動先：

   * 値を `data-scf-component` 属性（20 行目以上）:

      * 送信元 `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`

   * カスタムコメントコンポーネントを含めるように変更します（75 行目まで）。

      * Replace `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * を使用 `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* コピー `comment.hbs`

   * 送信者 [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 宛先 [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編集 `comment.hbs` 移動先：

   * data-scf-component 属性の値を変更します（19 行目以降）。

      * 送信元 `social/commons/components/hbs/comments/comment`
      * To `/apps/custom/components/comments/comment`

* 選択 `/apps/custom` ノード
* 選択 **[!UICONTROL すべて保存]**

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリを含める必要がないように、デフォルトのコメントシステムの clientlib の categories 値を使用できます ( `cq.social.author.hbs.comments`) をクリックします。 ただし、この clientlib は、デフォルトコンポーネントのすべてのインスタンスに対しても含める必要があります。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* 選択 `/apps/custom/components/comments` ノード
* 選択 **[!UICONTROL ノードを作成]**

   * **名前**：`clientlibs`
   * **型**：`cq:ClientLibraryFolder`
   * 追加先 **[!UICONTROL プロパティ]** タブ：

      * **名前** `categories` **タイプ** `String` **値** `cq.social.author.hbs.comments` `Multi`
      * **名前** `dependencies` **タイプ** `String` **値** `cq.social.scf` `Multi`

* 選択 **[!UICONTROL すべて保存]**
* を使用 `/apps/custom/components/comments/clientlib`選択した s ノードに、次の 3 つのファイルを作成します。

   * **名前**：`css.txt`
   * **名前**：`js.txt`
   * **名前**: customcommentsystem.js

* 次の内容として「customcommentsystem.js」と入力します。 `js.txt`
* 選択 **[!UICONTROL すべて保存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF モデルとビューの登録 {#register-the-scf-model-view}

SCF コンポーネントを拡張（上書き）する場合、resourceType は異なります ( オーバーレイでは、検索を実行する相対検索メカニズムが使用されます `/apps` 前 `/libs` したがって、resourceType は同じままです )。 このため、カスタム resourceType の SCF JS モデルとビューを登録するために、（クライアントライブラリに）JavaScript を記述する必要があります。

次のテキストをコンテンツとして入力 `customcommentsystem.js`:

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

* 選択 **[!UICONTROL すべて保存]**

## アプリの公開 {#publish-the-app}

パブリッシュ環境で拡張コンポーネントを使用するには、カスタムコンポーネントをレプリケートする必要があります。

その方法の 1 つは次のとおりです。

* グローバルナビゲーションから、

   * 選択 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
   * 選択 **[!UICONTROL ツリーをアクティベート]**
   * `Start Path` を `/apps/custom` に設定
   * オフ **[!UICONTROL 変更済みのみ]**
   * 選択 **[!UICONTROL 有効化]** ボタン
