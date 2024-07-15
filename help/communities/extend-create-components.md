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

これらの方向で `.hidden` 以外の **グループ** 値を指定すると、コンポーネントをコンポーネントブラウザー（サイドキック）から使用できるようになります。

自動作成された JSP ファイルは、デフォルトの HBS ファイルが代わりに使用されるので、削除されます。

1. **CRXDE|Lite** （[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)）を参照します

1. カスタムアプリケーションの場所を作成します。

   * `/apps` ノードを選択します。

      * **custom** という名前の **[!UICONTROL フォルダーを作成]**

   * `/apps/custom` ノードを選択します。

      * **フォルダーを作成** という名前 **[!UICONTROL components]**

1. `/apps/custom/components` ノードを選択します。

   * **[!UICONTROL 作成/コンポーネント…]**

      * **ラベル**: *comments*
      * **タイトル**: *代替コメント*
      * **説明**: *代替コメントのスタイル*
      * **スーパータイプ**:*social/commons/components/hbs/comments*
      * **グループ**: *カスタム*

   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。

1. 作成したノードを展開します：`/apps/custom/components/comments`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. `comments.jsp` を右クリック
1. 「**[!UICONTROL 削除]**」を選択します。
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-component](assets/create-component.png)

### 子コメントコンポーネントの作成 {#create-the-child-comment-component}

これらの方向は、親コンポーネントのみをページ内に含める必要があるので、**グループ** を `.hidden` に設定します。

自動作成された JSP ファイルは、デフォルトの HBS ファイルが代わりに使用されるので、削除されます。

1. `/apps/custom/components/comments` ノードに移動します
1. ノードを右クリックします

   * **[!UICONTROL 作成]**/**[!UICONTROL コンポーネント…]** を選択します。

      * **ラベル**: *comment*
      * **タイトル**: *代替コメント*
      * **説明**: *代替コメントスタイル*
      * **スーパータイプ**:*social/commons/components/hbs/comments/comment*
      * **グループ**：`*.hidden*`

   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL 次へ]**」を選択します。
   * 「**[!UICONTROL OK]**」を選択します。

1. 作成したノードを展開します：`/apps/custom/components/comments/comment`
1. 「**[!UICONTROL すべて保存]**」を選択します。
1. `comment.jsp` を右クリック
1. 「**[!UICONTROL 削除]**」を選択します。
1. 「**[!UICONTROL すべて保存]**」を選択します。

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### デフォルトの HBS スクリプトのコピーと変更 {#copy-and-modify-the-default-hbs-scripts}

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用：

* コピー `comments.hbs`

   * [/libs/social/commons/components/hbs/comments から ](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * [/apps/custom/components/comments に追加するには ](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* `comments.hbs` を次のように編集します。

   * `data-scf-component` 属性の値を変更します（～20 行目）。

      * `social/commons/components/hbs/comments` から
      * `/apps/custom/components/comments` へ

   * を変更してカスタムコメントコンポーネントを含めます（75 行目まで）。

      * Replace `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * （`{{include this resourceType='/apps/custom/components/comments/comment'}}` を使用）

* コピー `comment.hbs`

   * [/libs/social/commons/components/hbs/comments/comment から ](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* `comment.hbs` を次のように編集します。

   * data-scf-component 属性の値を変更します（～行 19）

      * `social/commons/components/hbs/comments/comment` から
      * `/apps/custom/components/comments/comment` へ

* ノード `/apps/custom` 選択
* 「**[!UICONTROL すべて保存]**」を選択します。

## クライアントライブラリフォルダーの作成 {#create-a-client-library-folder}

このクライアントライブラリをインクルードする必要をなくすために、デフォルトのコメントシステムの clientlib の categories 値を使用できます（`cq.social.author.hbs.comments`）。 ただし、この clientlib は、デフォルトコンポーネントのすべてのインスタンスにも含める必要があります。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) を使用：

* ノード `/apps/custom/components/comments` 選択
* 「**[!UICONTROL ノードを作成]**」を選択します。

   * **名前**：`clientlibs`
   * **型**：`cq:ClientLibraryFolder`
   * **[!UICONTROL プロパティ]** タブに追加：

      * **名前** `categories` **タイプ** `String` **値** `cq.social.author.hbs.comments` `Multi`
      * **名前** `dependencies` **タイプ** `String` **値** `cq.social.scf` `Multi`

* 「**[!UICONTROL すべて保存]**」を選択します。
* `/apps/custom/components/comments/clientlib`s ノードを選択した状態で、次の 3 つのファイルを作成します。

   * **名前**：`css.txt`
   * **名前**：`js.txt`
   * **名前**:customcommentsystem.js

* `js.txt` のコンテンツとして「customcommentsystem.js」と入力します
* 「**[!UICONTROL すべて保存]**」を選択します。

![comments-clientlibs](assets/comments-clientlibs.png)

## SCF モデルとビューの登録 {#register-the-scf-model-view}

SCF コンポーネントを拡張（上書き）する場合、resourceType は異なります（オーバーレイでは、resourceType が同じままになるように、`/libs` 前に `/apps` を検索する相対検索メカニズムを使用します）。 そのため、SCF JS モデルを登録してカスタム resourceType を表示するには、（クライアントライブラリに）JavaScriptを記述する必要があります。

`customcommentsystem.js` のコンテンツとして次のテキストを入力します。

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

## アプリのPublish {#publish-the-app}

パブリッシュ環境で拡張コンポーネントを使用するには、カスタムコンポーネントをレプリケートする必要があります。

その方法の 1 つは次のとおりです。

* グローバルナビゲーションから

   * **[!UICONTROL ツール]**/**[!UICONTROL 導入]**/**[!UICONTROL レプリケーション]** を選択します。
   * **[!UICONTROL ツリーのアクティブ化]** を選択します。
   * `Start Path` を `/apps/custom` に設定
   * 「**[!UICONTROL 変更済みのみ]**」をオフにします
   * 「**[!UICONTROL アクティベート]**」ボタンを選択します
