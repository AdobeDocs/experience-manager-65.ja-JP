---
title: サンプルページへのコメントの追加
seo-title: サンプルページへのコメントの追加
description: ページへのカスタムコメントの追加
seo-description: ページへのカスタムコメントの追加
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 56%

---


# サンプルページへのコメントの追加  {#add-comment-to-sample-page}

カスタムコメントシステムのコンポーネントがアプリケーションディレクトリ(/apps)に配置されたので、拡張コンポーネントを使用できます。 影響を受けるWebサイト内のコメントシステムのインスタンスでは、そのresourceTypeをカスタムコメントシステムに設定し、必要なすべてのクライアントライブラリを含める必要があります。

## 必要な clientlib の識別 {#identify-required-clientlibs}

デフォルトのコメントのスタイルと機能に必要なクライアントライブラリは、拡張されたコメントにも必要です。

The [Community Components Guide](/help/communities/components-guide.md) identifies the required client libraries. コンポーネントガイドを参照し、コメントコンポーネントの表示を表示します。例：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

コメントの正常なレンダリングと機能のためには、3 つのクライアントライブラリが必要です。These will need to be included where the extended Comments are referenced, and the [extended Comments&#39; client library](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`).

![chlimage_1-47](assets/chlimage_1-47.png)

### ページへのカスタムコメントの追加 {#add-custom-comments-to-a-page}

1 つのページで使用できるコメントシステムは 1 つだけなので、[サンプルページの作成](/help/communities/create-sample-page.md)のチュートリアルで説明する手順に従ってサンプルページを作成すると簡単です。

作成したら、デザインモードに切り替え、カスタムコンポーネントグループを使用可能にして、`Alt Comments` コンポーネントをページに追加できるようにします。

コメントを正しく表示し、機能させるには、コメントのクライアントライブラリをページの clientlibslist に追加する必要があります（[コミュニティコンポーネントの clientlib](/help/communities/clientlibs.md) を参照）。

#### サンプルページでのコメントの clientlib {#comments-clientlibs-on-sample-page}

![chlimage_1-48](assets/chlimage_1-48.png)

#### オーサー環境：サンプルページでの Alt Comment {#author-alt-comment-on-sample-page}

![chlimage_1-49](assets/chlimage_1-49.png)

#### オーサー環境：サンプルページでのコメントノード {#author-sample-page-comments-node}

You can verify the resourceType in CRXDE by viewing the properties of the comments node for the sample page at `/content/sites/sample/en/jcr:content/content/primary/comments`.

![chlimage_1-50](assets/chlimage_1-50.png)

#### サンプルページの公開 {#publish-sample-page}

カスタムコンポーネントをページに追加した後は、（再度）[ページを公開](/help/communities/sites-console.md#publishing-the-site)する必要もあります。

#### パブリッシュ環境：サンプルページでの Alt Comment {#publish-alt-comment-on-sample-page}

カスタムアプリとサンプルページの両方を公開した後に、コメントを入力できます。 When signed in, either with a [demo user](/help/communities/tutorials.md#demo-users) or admin, it is possible to post a comment.

aaron.mcdonald@mailinator.comコメントの投稿を次に示します。

![chlimage_1-51](assets/chlimage_1-51.png)

![chlimage_1-52](assets/chlimage_1-52.png)

拡張されたコンポーネントがデフォルトの外観で正しく機能していることがわかります。次は外観を変更します。