---
title: コンポーネントの作成
seo-title: Create the Components
description: コメントコンポーネントの作成
seo-description: Create the Comments component
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 56%

---

# コンポーネントの作成  {#create-the-components}

コンポーネントを拡張する例では、実際には次の 2 つのコンポーネントで構成されるコメントシステムを使用します。

* コメント — ページ上に配置されるコンポーネントである包括的なコメントシステム。
* コメント — 投稿されたコメントのインスタンスをキャプチャするコンポーネント。

投稿されたコメントの外観をカスタマイズする場合は特に、両方のコンポーネントを配置する必要があります。

>[!NOTE]
>
>1 つのサイトページで使用できるコメントシステムは 1 つのみです。
>
>多くのコミュニティ機能には、拡張されたコメントシステムを参照するように resourceType を変更できるコメントシステムが既に含まれています。

## コメントコンポーネントの作成 {#create-the-comments-component}

これらの方向は、 **グループ** 以外の値 `.hidden` そのため、コンポーネントをコンポーネントブラウザー（サイドキック）から使用できるようにします。

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. **CRXDE Lite**（[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)）を表示します。

1. カスタムアプリケーションの場所を作成します。

   * を選択します。 `/apps` ノード

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL custom]** という名前のフォルダーを作成します。
   * を選択します。 `/apps/custom` ノード

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL components]** という名前のフォルダーを作成します。


1. を選択します。 `/apps/custom/components` ノード

   * **[!UICONTROL 作成／コンポーネント...]** を選択します。

      * **ラベル**: *コメント*
      * **タイトル**：Alt Comments **
      * **説明**：Alternative comments style **
      * **スーパータイプ**：social/commons/components/hbs/comments **
      * **グループ**：Custom **
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。


1. 作成したノードを展開します。 `/apps/custom/components/comments`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. 右クリック `comments.jsp`
1. 選択 **[!UICONTROL 削除]**
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-component](assets/create-component.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

これらの方向は設定されました **グループ** から `.hidden` 親コンポーネントのみをページ内に含める必要があるので。

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. 次に移動： `/apps/custom/components/comments` ノード
1. ノードを右クリックします。

   * 選択 **[!UICONTROL 作成]** > **[!UICONTROL コンポーネント…]**

      * **ラベル**：comment **
      * **タイトル**：Alt Comment **
      * **説明**：Alternative comment style **
      * **スーパータイプ**：social/commons/components/hbs/comments/comment **
      * **グループ**：`*.hidden*`
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。


1. 作成したノードを展開します。 `/apps/custom/components/comments/comment`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. 右クリック `comment.jsp`
1. 選択 **[!UICONTROL 削除]**
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### デフォルトの HBS スクリプトのコピーと変更 {#copy-and-modify-the-default-hbs-scripts}

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* コピー `comments.hbs`

   * 送信者 [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * 宛先 [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* 編集 `comments.hbs` 移動先：

   * 値を `data-scf-component` 属性（20 行目以上）:

      * 送信元 `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * カスタムコメントコンポーネントを含めるように変更します（75 行目まで）。

      * Replace `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * を次のタグに置換します。`{{include this resourceType='/apps/custom/components/comments/comment'}}`


* コピー `comment.hbs`

   * 送信者 [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * 宛先 [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* 編集 `comment.hbs` 移動先：

   * data-scf-component 属性の値を変更します（19 行目前後）。

      * 送信元 `social/commons/components/hbs/comments/comment`
      * 宛先 `/apps/custom/components/comments/comment`

* 選択 `/apps/custom` ノード
* 「**[!UICONTROL すべて保存]**」を選択します。

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリを明示的に含めなくても済むように、デフォルトのコメントシステムの clientlib の categories 値（`cq.social.author.hbs.comments`）を使用できますが、これを使用すると、デフォルトのコンポーネントのすべてのインスタンスについても、この clientlib が含まれるようになります。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* 選択 `/apps/custom/components/comments` ノード
* 選択 **[!UICONTROL ノードを作成]**

   * **名前**：`clientlibs`
   * **型**：`cq:ClientLibraryFolder`
   * 追加先 **[!UICONTROL プロパティ]** タブ：

      * **名前** `categories` **タイプ** `String` **値** `cq.social.author.hbs.comments` `Multi`
      * **名前** `dependencies` **タイプ** `String` **値** `cq.social.scf` `Multi`

* 「**[!UICONTROL すべて保存]**」を選択します。
* を使用 `/apps/custom/components/comments/clientlib`選択した s ノード、3 つのファイルを作成します。

   * **名前**：`css.txt`
   * **名前**：`js.txt`
   * **名前**：customcommentsystem.js

* 次の内容を&#39;customcommentsystem.js&#39;と入力します。 `js.txt`
* 「**[!UICONTROL すべて保存]**」を選択します。

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF モデルおよびビューの登録 {#register-the-scf-model-view}

SCF コンポーネントを拡張（上書き）する場合、resourceType は異なります（オーバーレイは、検索を実行する相対検索メカニズムを利用します） `/apps` 前 `/libs` したがって、resourceType は同じままです )。 このため、カスタム resourceType の SCF JS モデルとビューを登録するために、（クライアントライブラリに）JavaScript を記述する必要があります。

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

* 「**[!UICONTROL すべて保存]**」を選択します。

## アプリの公開 {#publish-the-app}

拡張されたコンポーネントをパブリッシュ環境で確認するには、カスタムコンポーネントをレプリケートする必要があります。

その方法の 1 つは次のとおりです。

* グローバルナビゲーションから、

   * 選択 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]**
   * 選択 **[!UICONTROL ツリーをアクティベート]**
   * `Start Path` を `/apps/custom` に設定
   * オフ **[!UICONTROL 変更済みのみ]**
   * 選択 **[!UICONTROL 有効化]** ボタン
