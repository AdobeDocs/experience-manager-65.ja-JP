---
title: 外観の変更
description: Adobe Experience Manager Communities で各コメントの全体的なHTMLを作成する comment.hbs スクリプトの編集方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

`comment.hbs` スクリプトは、各コメントの全体的なHTMLを作成します。

投稿された各コメントの横にアバターを表示しないようにするには：

1. `comment.hbs` を `libs` から `apps` にコピー

   1. `/libs/social/commons/components/hbs/comments/comment/comment.hbs` を選択します。
   1. 「**[!UICONTROL コピー]**」を選択します
   1. `/apps/social/commons/components/hbs/comments/comment` を選択します。
   1. 「**[!UICONTROL 貼り付け]**」を選択します

1. オーバーレイされた `comment.hbs` を開く

   * `/apps/social/commons/components/hbs/comments/comment folder` のノード `comment.hbs` をダブルクリックします

1. 次の行を見つけ、それらを削除またはコメントアウトします。

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

行を削除するか、行を `<!--` で囲んで `-->` をコメントアウトします。 また、「xxx」という文字は、アバターがどこにあるかを示す視覚的なインジケーターとして追加されています。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### オーバーレイをレプリケートする {#replicate-the-overlay}

レプリケーションツールを使用して、オーバーレイコメントコンポーネントをパブリッシュインスタンスにプッシュします。

>[!NOTE]
>
>レプリケーションのより堅牢な形式は、パッケージマネージャーでパッケージを作成し、[&#x200B; アクティブ化 &#x200B;](/help/sites-administering/package-manager.md#replicating-packages) することです。 パッケージは、書き出しとアーカイブが可能です。

グローバルナビゲーションから **[!UICONTROL ツール]**/**[!UICONTROL デプロイメント]**/**[!UICONTROL レプリケーション]** を選択し、「**[!UICONTROL ツリーをアクティベート]**」をクリックします。

「開始パス」に「`/apps/social/commons`」と入力して、「**[!UICONTROL アクティベート]**」を選択します。

![verify-content-template](assets/verify-content-template.png)

### 結果を表示 {#view-results}

パブリッシュインスタンスに管理者としてログオンします（例：https://localhost:4503/crx/deの場合）。管理者/管理者としてログオンすると、オーバーレイされたコンポーネントがあることを確認できます。

ログオフしてから `aaron.mcdonald@mailinator.com/password` としてログオンし、ページを更新すると、投稿されたコメントにアバターが表示されないことがわかります。 代わりに、単純な「xxx」が表示されます。

![create-template-component](assets/create-template-component.png)
