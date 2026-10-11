---
title: 外観の変更
description: Adobe Experience Manager Communitiesで各コメントのHTML全体を作成する役割を担うcomment.hbs スクリプトを編集する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 3%
---
# 外観の変更 {#alter-the-appearance}

## スクリプトを修正 {#modify-the-script}

`comment.hbs` スクリプトは、各コメントのHTML全体を作成する責任があります。

投稿された各コメントの横にアバターを表示しない場合：

1. `comment.hbs`を`libs`から`apps`にコピー

   1. `/libs/social/commons/components/hbs/comments/comment/comment.hbs` を選択します。
   1. **[!UICONTROL コピー]**&#x200B;を選択
   1. `/apps/social/commons/components/hbs/comments/comment` を選択します。
   1. **[!UICONTROL 貼り付け]**&#x200B;を選択

1. オーバーレイ `comment.hbs`を開きます

   * `/apps/social/commons/components/hbs/comments/comment folder`のノード `comment.hbs`をダブルクリックします

1. 次の行を見つけ、削除またはコメントアウトします。

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

行を削除するか、`<!--`と`-->`で囲んでコメントアウトします。 また、「xxx」という文字は、アバターがどこにあったかを視覚的に示す指標として追加されています。

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
>より堅牢なレプリケーション形式は、パッケージをPackage Managerに作成し、それを[activate](/help/sites-administering/package-manager.md#replicating-packages)することです。 パッケージはエクスポートおよびアーカイブできます。

グローバルナビゲーションから、**[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL レプリケーション]**&#x200B;を選択し、**[!UICONTROL ツリーをアクティブ化]**&#x200B;をクリックします。

開始パスに「`/apps/social/commons`」と入力し、「**[!UICONTROL アクティブ化]**」を選択します。

![verify-content-template](assets/verify-content-template.png)

### 結果を表示 {#view-results}

管理者としてパブリッシュインスタンスにログオンする場合（例：https://localhost:4503/crx/de as admin/admin）、オーバーレイされたコンポーネントが存在することを確認できます。

ログオフして`aaron.mcdonald@mailinator.com/password`としてログオンし、ページを更新すると、投稿されたコメントでアバターが表示されないことがわかります。 代わりに、単純な「xxx」が表示されます。

![create-template-component](assets/create-template-component.png)
