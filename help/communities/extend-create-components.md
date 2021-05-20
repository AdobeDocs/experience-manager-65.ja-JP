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
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 56%

---

# コンポーネントの作成   {#create-the-components}

コンポーネントを拡張する例では、実際には次の 2 つのコンポーネントで構成されるコメントシステムを使用します。

* コメント — ページに配置されるコンポーネントである包括的なコメントシステム。
* コメント — 投稿されたコメントのインスタンスをキャプチャするコンポーネント。

投稿されたコメントの外観をカスタマイズする場合は特に、両方のコンポーネントを配置する必要があります。

>[!NOTE]
>
>1 つのサイトページで使用できるコメントシステムは 1 つのみです。
>
>多くのコミュニティ機能には、拡張されたコメントシステムを参照するように resourceType を変更できるコメントシステムが既に含まれています。

## コメントコンポーネントの作成  {#create-the-comments-component}

これらの手順では、`.hidden`以外の&#x200B;**Group**&#x200B;値を指定し、コンポーネントをコンポーネントブラウザー（サイドキック）から使用できるようにします。

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. **CRXDE Lite**（[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)）を表示します。

1. カスタムアプリケーションの場所の作成：

   * `/apps`ノードを選択します。

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL custom]** という名前のフォルダーを作成します。
   * `/apps/custom`ノードを選択します。

      * 「**フォルダーを作成**」を選択し、**[!UICONTROL components]** という名前のフォルダーを作成します。


1. `/apps/custom/components`ノードを選択します。

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


1. 作成したノードを展開します。`/apps/custom/components/comments`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. `comments.jsp`を右クリック
1. **[!UICONTROL 削除]**&#x200B;を選択します。
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-component](assets/create-component.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

親コンポーネントのみをページ内に含める必要があるので、これらの方向は&#x200B;**Group**&#x200B;を`.hidden`に設定します。

デフォルトの HBS ファイルを代わりに使用するので、自動的に作成された JSP ファイルは削除します。

1. `/apps/custom/components/comments`ノードに移動します。
1. ノードを右クリックします。

   * **[!UICONTROL 作成]** > **[!UICONTROL コンポーネントを選択します。]**

      * **ラベル**：comment **
      * **タイトル**：Alt Comment **
      * **説明**：Alternative comment style **
      * **スーパータイプ**：social/commons/components/hbs/comments/comment **
      * **グループ**: `*.hidden*`
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。


1. 作成したノードを展開します。`/apps/custom/components/comments/comment`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. `comment.jsp`を右クリック
1. **[!UICONTROL 削除]**&#x200B;を選択します。
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### デフォルトの HBS スクリプトのコピーと変更 {#copy-and-modify-the-default-hbs-scripts}

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* コピー `comments.hbs`

   * [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)から
   * [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)へ

* `comments.hbs`を編集して次の操作を行います。

   * `data-scf-component`属性の値を変更します（20行目前後）。

      * 送信元 `social/commons/components/hbs/comments`
      * To `/apps/custom/components/comments`
   * カスタムコメントコンポーネントを含めるように変更します（75行目前後）。

      * 置換 `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * を次のタグに置換します。`{{include this resourceType='/apps/custom/components/comments/comment'}}`


* コピー `comment.hbs`

   * [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)から
   * 宛先： [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* `comment.hbs`を編集して次の操作を行います。

   * data-scf-component属性の値を変更します（19行目前後）。

      * 送信元 `social/commons/components/hbs/comments/comment`
      * `/apps/custom/components/comments/comment`へ

* `/apps/custom`ノードを選択
* 「**[!UICONTROL すべて保存]**」を選択します。

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリを明示的に含めなくても済むように、デフォルトのコメントシステムの clientlib の categories 値（`cq.social.author.hbs.comments`）を使用できますが、これを使用すると、デフォルトのコンポーネントのすべてのインスタンスについても、この clientlib が含まれるようになります。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* `/apps/custom/components/comments`ノードを選択
* 「**[!UICONTROL ノードを作成]**」を選択します。

   * **名前**：`clientlibs`
   * **型**：`cq:ClientLibraryFolder`
   * **[!UICONTROL 「プロパティ]**」タブに追加：

      * **** `categories` **** `String` **NameTypeValue** `cq.social.author.hbs.comments` `Multi`
      * **** `dependencies` **** `String` **NameTypeValue** `cq.social.scf` `Multi`

* 「**[!UICONTROL すべて保存]**」を選択します。
* `/apps/custom/components/comments/clientlib`ノードを選択し、3つのファイルを作成します。

   * **名前**：`css.txt`
   * **名前**：`js.txt`
   * **名前**：customcommentsystem.js

* `js.txt`の内容として「customcommentsystem.js」と入力します。
* 「**[!UICONTROL すべて保存]**」を選択します。

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF モデルおよびビューの登録 {#register-the-scf-model-view}

SCFコンポーネントを拡張（上書き）する場合、resourceTypeは異なります（オーバーレイでは、`/libs`の前に`/apps`を検索する相対検索メカニズムを使用して、resourceTypeを同じままにします）。 このため、（クライアントライブラリ内の）JavaScriptを記述して、SCF JSモデルとカスタムresourceTypeのビューを登録する必要があります。

`customcommentsystem.js`の内容として次のテキストを入力します。

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

その方法の1つは次のとおりです。

* グローバルナビゲーションから、

   * **[!UICONTROL ツール]** / **[!UICONTROL デプロイ]** / **[!UICONTROL レプリケーション]**&#x200B;を選択します。
   * 「**[!UICONTROL ツリーをアクティブ化]**」を選択します。
   * `Start Path`を`/apps/custom`に設定します。
   * **[!UICONTROL 変更済み]**&#x200B;のみをオフにします
   * 「**[!UICONTROL アクティブ化]**」ボタンを選択します。
