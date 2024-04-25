---
title: コンポーネントの作成
description: コメントおよびコメントコンポーネントで構成されるコメントシステムを使用してコンポーネントを拡張する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 4%

---

# コンポーネントの作成  {#create-the-components}

コンポーネントを拡張する例では、2 つのコンポーネントで構成されるコメントシステムを使用しています。

* コメント – ページに配置されるコンポーネントを含むコメントシステム。
* コメント – 投稿されたコメントのインスタンスをキャプチャするコンポーネント。

特に、投稿されたコメントの外観をカスタマイズする場合は、両方のコンポーネントを配置する必要があります。

>[!NOTE]
>
>サイト ページごとに 1 つのコメントシステムのみが許可されます。
>
>Communities の多くの機能には既に、拡張コメントシステムを参照するように resourceType を変更できるコメントシステムが含まれています。

## コメントコンポーネントの作成 {#create-the-comments-component}

これらの方向は、 **グループ** 以外の値 `.hidden` そのため、コンポーネントはコンポーネントブラウザー（サイドキック）から使用できるようになります。

自動作成された JSP ファイルは、デフォルトの HBS ファイルが代わりに使用されるので、削除されます。

1. を参照 **CRXDE|Lite** （[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)）

1. カスタムアプリケーションの場所を作成します。

   * 「」を選択します `/apps` ノード

      * **フォルダーを作成** 名前付き **[!UICONTROL custom]**

   * 「」を選択します `/apps/custom` ノード

      * **フォルダーを作成** 名前付き **[!UICONTROL components]**

1. 「」を選択します `/apps/custom/components` ノード

   * **[!UICONTROL 作成/ コンポーネント…]**

      * **ラベル**: *コメント*
      * **タイトル**: *代替コメント*
      * **説明**: *代替コメントのスタイル*
      * **スーパータイプ**: *social/commons/components/hbs/comments*
      * **グループ**: *カスタム*

   * を選択 **[!UICONTROL 次]**
   * を選択 **[!UICONTROL 次]**
   * を選択 **[!UICONTROL 次]**
   * 「**[!UICONTROL OK]**」を選択します。

1. 作成したノードを展開します。 `/apps/custom/components/comments`
1. を選択 **[!UICONTROL すべて保存]**
1. 右クリック `comments.jsp`
1. 「**[!UICONTROL 削除]**」を選択します。
1. を選択 **[!UICONTROL すべて保存]**

![create-component](assets/create-component.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

これらの指示はセットされる **グループ** 対象： `.hidden` 親コンポーネントのみをページ内に含める必要があるからです。

自動作成された JSP ファイルは、デフォルトの HBS ファイルが代わりに使用されるので、削除されます。

1. に移動します。 `/apps/custom/components/comments` ノード
1. ノードを右クリックします

   * を選択 **[!UICONTROL 作成]** > **[!UICONTROL コンポーネント…]**

      * **ラベル**: *コメント*
      * **タイトル**: *代替コメント*
      * **説明**: *代替コメントスタイル*
      * **スーパータイプ**: *social/commons/components/hbs/comments/comment*
      * **グループ**：`*.hidden*`

   * を選択 **[!UICONTROL 次]**
   * を選択 **[!UICONTROL 次]**
   * を選択 **[!UICONTROL 次]**
   * 「**[!UICONTROL OK]**」を選択します。

1. 作成したノードを展開します。 `/apps/custom/components/comments/comment`
1. を選択 **[!UICONTROL すべて保存]**
1. 右クリック `comment.jsp`
1. 「**[!UICONTROL 削除]**」を選択します。
1. を選択 **[!UICONTROL すべて保存]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### デフォルトの HBS スクリプトのコピーと変更 {#copy-and-modify-the-default-hbs-scripts}

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* コピー `comments.hbs`

   * 送信元 [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 終了 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編集 `comments.hbs` コピー先：

   * の値を `data-scf-component` 属性（～20 行目）:

      * 送信元 `social/commons/components/hbs/comments`
      * 終了 `/apps/custom/components/comments`

   * を変更してカスタムコメントコンポーネントを含めます（75 行目まで）。

      * 置換 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * （を使用） `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* コピー `comment.hbs`

   * 送信元 [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 終了 [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編集 `comment.hbs` コピー先：

   * data-scf-component 属性の値を変更します（～行 19）

      * 送信元 `social/commons/components/hbs/comments/comment`
      * 終了 `/apps/custom/components/comments/comment`

* を選択 `/apps/custom` ノード
* を選択 **[!UICONTROL すべて保存]**

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリをインクルードする必要をなくすために、デフォルトのコメントシステムの clientlib の categories 値を使用できます（ `cq.social.author.hbs.comments`）に設定します。 ただし、この clientlib は、デフォルトコンポーネントのすべてのインスタンスにも含める必要があります。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* を選択 `/apps/custom/components/comments` ノード
* を選択 **[!UICONTROL ノードを作成]**

   * **名前**：`clientlibs`
   * **型**：`cq:ClientLibraryFolder`
   * 追加先 **[!UICONTROL プロパティ]** タブ：

      * **名前** `categories` **タイプ** `String` **値** `cq.social.author.hbs.comments` `Multi`
      * **名前** `dependencies` **タイプ** `String` **値** `cq.social.scf` `Multi`

* を選択 **[!UICONTROL すべて保存]**
* （を使用） `/apps/custom/components/comments/clientlib`s ノードを選択し、次の 3 つのファイルを作成します。

   * **名前**：`css.txt`
   * **名前**：`js.txt`
   * **名前**:customcommentsystem.js

* コンテンツとして「customcommentsystem.js」を入力 `js.txt`
* を選択 **[!UICONTROL すべて保存]**

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF モデルとビューの登録 {#register-the-scf-model-view}

SCF コンポーネントを拡張（オーバーライド）する場合、resourceType は異なります（オーバーレイでは、を検索する相対検索メカニズムを使用します） `/apps` 次の前 `/libs` そのため、resourceType は変わりません）。 そのため、SCF JS モデルを登録してカスタム resourceType を表示するには、（クライアントライブラリに） JavaScript を記述する必要があります。

次のテキストをコンテンツとして入力します `customcommentsystem.js`:

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

* を選択 **[!UICONTROL すべて保存]**

## アプリの公開 {#publish-the-app}

パブリッシュ環境で拡張コンポーネントを使用するには、カスタムコンポーネントをレプリケートする必要があります。

その方法の 1 つは次のとおりです。

* グローバルナビゲーションから

   * を選択 **[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL 複製]**
   * を選択 **[!UICONTROL ツリーのアクティベート]**
   * `Start Path` を `/apps/custom` に設定
   * Uncheck **[!UICONTROL 変更済みのみ]**
   * を選択 **[!UICONTROL Activate]** ボタン
