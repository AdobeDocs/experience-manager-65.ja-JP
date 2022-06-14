---
title: 外観の変更
seo-title: Alter the Appearance
description: スクリプトの変更
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 41%

---

# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

comment.hbs スクリプトは、各コメントの全体的なHTMLを作成します。

投稿された各コメントの横のアバターを表示しないようにするには：

1. コピー `comment.hbs`から `libs`から `apps`

   1. 選択 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 選択 **[!UICONTROL コピー]**
   1. 選択 `/apps/social/commons/components/hbs/comments/comment`
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

### オーバーレイのレプリケート {#replicate-the-overlay}

レプリケーションツールを使用して、オーバーレイされたコメントコンポーネントをパブリッシュインスタンスにプッシュします。

>[!NOTE]
>
>より強固なレプリケーション形式は、パッケージマネージャーでパッケージを作成し、それを[アクティベート](/help/sites-administering/package-manager.md#replicating-packages)することです。パッケージはエクスポートおよびアーカイブできます。

グローバルナビゲーションから、 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]** をクリックし、 **[!UICONTROL ツリーをアクティベート]**.

「開始パス」に、と入力します。 `/apps/social/commons` を選択し、 **[!UICONTROL 有効化]**.

![verify-content-template](assets/verify-content-template.png)

### 結果の表示 {#view-results}

パブリッシュインスタンスに管理者 ( https://localhost:4503/crx/deなど ) としてログインした場合は、オーバーレイされたコンポーネントが存在することを確認できます。

ログアウトして `aaron.mcdonald@mailinator.com/password` として再ログインし、ページを更新した場合は、投稿されたコメントはアバターと一緒には表示されなくなっており、代わりに単純な「xxx」が表示されることがわかります。

![create-template-component](assets/create-template-component.png)
