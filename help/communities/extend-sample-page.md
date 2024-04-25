---
title: サンプルページへのコメントの追加
description: Web サイトのコメントシステムのインスタンスで、resourceType をカスタムコメントシステムに設定し、必要なすべてのクライアントライブラリを含める方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%

---

# サンプルページへのコメントの追加  {#add-comment-to-sample-page}

カスタムコメントシステムのコンポーネントがアプリケーションディレクトリ（/apps）に配置されたので、拡張コンポーネントを使用できます。 影響を受ける web サイトのコメントシステムのインスタンスは、resourceType をカスタムコメントシステムに設定し、必要なすべてのクライアントライブラリを含める必要があります。

## 必要な Clientlib の特定 {#identify-required-clientlibs}

デフォルトコメントのスタイルと機能に必要なクライアントライブラリは、拡張コメントにも必要です。

この [コミュニティコンポーネントガイド](/help/communities/components-guide.md) は、必要なクライアントライブラリを識別します。 コンポーネントガイドを参照し、コメントコンポーネントを確認します。次に例を示します。

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

コメントがレンダリングされて正しく機能するには、3 つのクライアントライブラリが必要であることに注意してください。 これらは、拡張コメントが参照される場所に含める必要があり、 [拡張コメントのクライアントライブラリ](/help/communities/extend-create-components.md#create-a-client-library-folder) （ `apps.custom.comments`）に設定します。

![comments-component1](assets/comments-component1.png)

### ページへのカスタムコメントの追加 {#add-custom-comments-to-a-page}

コメントシステムはページごとに 1 つだけなので、簡単にサンプルページを作成できます。詳しくは、を参照してください [サンプルページの作成](/help/communities/create-sample-page.md) チュートリアル。

作成したら、デザインモードに切り替えて、カスタムコンポーネントグループを使用して、以下を許可できます。 `Alt Comments` ページに追加するコンポーネント。

コメントが表示されて正しく機能するには、コメント用のクライアントライブラリをページの clientlibslist に追加する必要があります（ [コミュニティコンポーネントの clientlib](/help/communities/clientlibs.md)）に設定します。

#### サンプルページのコメント Clientlib {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作成者：サンプルページの代替コメント {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 作成者：サンプルページコメントノード {#author-sample-page-comments-node}

CRXDE で resourceType を確認するには、次の場所にあるサンプルページのコメントノードのプロパティを表示します `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### サンプルページを公開 {#publish-sample-page}

カスタムコンポーネントをページに追加した後、 [ページを公開します](/help/communities/sites-console.md#publishing-the-site).

#### 公開：サンプルページに対する代替コメント {#publish-alt-comment-on-sample-page}

カスタムアプリケーションとサンプルページの両方を公開した後、コメントを入力できます。 ログイン時に、次のいずれかを使用 [デモユーザー](/help/communities/tutorials.md#demo-users) または、管理者は、コメントを投稿できます。

aaron.mcdonald@mailinator.comがコメントを投稿しています。

![公開 – 代替 – コメント](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

これで、拡張コンポーネントがデフォルトの外観で正しく動作しているように見えるので、次に外観を変更します。
