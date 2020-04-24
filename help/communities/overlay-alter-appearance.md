---
title: 外観の変更
seo-title: 外観の変更
description: スクリプトの変更
seo-description: スクリプトの変更
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# 外観の変更 {#alter-the-appearance}

## スクリプトの変更 {#modify-the-script}

comment.hbsスクリプトは、各コメントのHTML全体を作成します。

投稿された各コメントの横のアバターを表示しないようにするには：

1. コピー `comment.hbs`元の `libs`先 `apps`

   1.  `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Select **Copy**
   1.  `/apps/social/commons/components/hbs/comments/comment`
   1. Select **Paste**

1. Open the overlaid `comment.hbs`

   * 重複クリッ `comment.hbs` ク `/apps/social/commons/components/hbs/comments/comment folder`

1. 次の行を探し、削除するかコメントアウトします。

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Either delete the lines, or surround them with `<!--` and `-->` to comment them out. また、「xxx」という文字が、アバターの場所を視覚的に示すインジケーターとして追加されています。

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
>より強固なレプリケーション形式は、パッケージマネージャーでパッケージを作成し、それを[アクティベート](/help/sites-administering/package-manager.md#replicating-packages)することです。パッケージは書き出しおよびアーカイブできます。


From the global navigation, select **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** and click **[!UICONTROL Activate Tree]**.

For the Start Path enter `/apps/social/commons` and select **[!UICONTROL Activate]**.

![chlimage_1-77](assets/chlimage_1-77.png)

### 結果の表示 {#view-results}

管理者(例：https://localhost:4503/crx/de as admin/admin)として発行インスタンスにログインすると、オーバーレイされたコンポーネントが存在することを確認できます。

ログアウトして `aaron.mcdonald@mailinator.com/password` として再ログインし、ページを更新した場合は、投稿されたコメントはアバターと一緒には表示されなくなっており、代わりに単純な「xxx」が表示されることがわかります。

![chlimage_1-78](assets/chlimage_1-78.png)

