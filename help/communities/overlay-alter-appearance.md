---
title: 外観の変更
description: Adobe Experience Manager Communities で各コメントの全体的なHTMLを作成する comment.hbs スクリプトを編集する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

The `comment.hbs` スクリプトは、各コメントの全体的なHTMLを作成します。

投稿された各コメントの横にアバターを表示しないには、次の手順を実行します。

1. コピー `comment.hbs`から `libs`から `apps`

   1. `/libs/social/commons/components/hbs/comments/comment/comment.hbs` を選択します。
   1. 選択 **[!UICONTROL コピー]**
   1. `/apps/social/commons/components/hbs/comments/comment` を選択します。
   1. 選択 **[!UICONTROL 貼り付け]**

1. オーバーレイを開く `comment.hbs`

   * ノードをダブルクリック `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. 次の行を探し、削除するかコメントアウトします。

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

線を削除するか、それらを囲みます。 `<!--` および `-->` コメントアウトします。 また、アバターがあった場所を視覚的に示すインジケーターとして、文字「xxx」が追加されています。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### オーバーレイの複製 {#replicate-the-overlay}

レプリケーションツールを使用して、オーバーレイされたコメントコンポーネントをパブリッシュインスタンスにプッシュします。

>[!NOTE]
>
>より堅牢なレプリケーション形式は、パッケージマネージャーでパッケージを作成し、 [アクティブ化](/help/sites-administering/package-manager.md#replicating-packages) その通り。 パッケージはエクスポートおよびアーカイブできます。

グローバルナビゲーションで、「 」を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]** をクリックします。 **[!UICONTROL ツリーをアクティベート]**.

「開始パス」に、と入力します。 `/apps/social/commons` を選択し、 **[!UICONTROL 有効化]**.

![verify-content-template](assets/verify-content-template.png)

### 結果を表示 {#view-results}

パブリッシュインスタンスに管理者としてログオンした場合 ( 例えば、 https://localhost:4503/crx/deを admin/admin としてログオンした場合 ) は、オーバーレイされたコンポーネントが存在することを確認できます。

ログオフし、次のようにしてログオンする場合 `aaron.mcdonald@mailinator.com/password` ページを更新すると、アバターが投稿されたコメントと共に表示されないことがわかります。 代わりに、単純な「xxx」が表示されます。

![create-template-component](assets/create-template-component.png)
