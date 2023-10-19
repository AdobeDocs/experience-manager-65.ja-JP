---
title: サンプルページへのコメントの追加
description: Web サイトのコメントシステムのインスタンスで、resourceType をカスタムコメントシステムに設定し、必要なクライアントライブラリをすべて含める方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 3%

---

# サンプルページへのコメントの追加  {#add-comment-to-sample-page}

カスタムコメントシステムのコンポーネントがアプリケーションディレクトリ (/apps) に配置されたので、拡張コンポーネントを使用できます。 影響を受ける Web サイト内のコメントシステムのインスタンスでは、resourceType をカスタムコメントシステムに設定し、必要なクライアントライブラリをすべて含める必要があります。

## 必要な clientlib の特定 {#identify-required-clientlibs}

デフォルトのコメントのスタイルと機能に必要なクライアントライブラリも、拡張コメントに必要です。

The [コミュニティコンポーネントガイド](/help/communities/components-guide.md) 必要なクライアントライブラリを識別します。 コンポーネントガイドを参照し、次に例を示します。

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

コメントが正しくレンダリングおよび機能するために必要な 3 つのクライアントライブラリに注意してください。 これらは、拡張されたコメントの参照先と、 [拡張コメントのクライアントライブラリ](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`) をクリックします。

![comments-component1](assets/comments-component1.png)

### ページにカスタムコメントを追加する {#add-custom-comments-to-a-page}

1 ページにつき 1 つのコメントシステムしか存在しないので、簡単にサンプルページを作成できます。詳しくは、 [サンプルページの作成](/help/communities/create-sample-page.md) チュートリアル

作成したら、デザインモードに入り、カスタムコンポーネントグループを使用可能にして、 `Alt Comments` ページに追加するコンポーネント。

コメントが正しく表示され、機能するには、コメント用のクライアントライブラリをページの clientlibslist に追加する必要があります ( [コミュニティコンポーネントの clientlib](/help/communities/clientlibs.md)) をクリックします。

#### サンプルページのコメント clientlibs {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作成者：サンプルページでの Alt Comment {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 作成者：ページコメントノードの例 {#author-sample-page-comments-node}

CRXDE で resourceType を確認するには、サンプルページ ( ) の comments ノードのプロパティを表示します。 `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### サンプルページを公開 {#publish-sample-page}

カスタムコンポーネントをページに追加した後は、次の操作もおこなう必要があります（再度追加する）。 [ページを公開する](/help/communities/sites-console.md#publishing-the-site).

#### 公開：サンプルページでの代替コメント {#publish-alt-comment-on-sample-page}

カスタムアプリケーションとサンプルページの両方を公開した後に、コメントを入力できます。 サインイン時に、 [デモユーザー](/help/communities/tutorials.md#demo-users) または管理者は、コメントを投稿できます。

aaron.mcdonald@mailinator.comはコメントを投稿しています：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

拡張コンポーネントがデフォルトの外観で正しく動作しているように見えたので、外観を変更する時が来ます。
