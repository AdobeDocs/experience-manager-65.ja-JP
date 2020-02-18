---
title: オーサリング
seo-title: オーサリング
description: AEM でのオーサリングの概念です
seo-description: AEM でのオーサリングの概念です
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# オーサリング{#authoring}

## Concept of Authoring (and Publishing) {#concept-of-authoring-and-publishing}

AEM には次の 2 種類の環境があります。

* オーサー
* パブリッシュ

これらの環境が相互に影響することで、コンテンツが Web サイト上に公開され、訪問者が閲覧できるようになります。

オーサー環境は、コンテンツを作成および更新し、実際にコンテンツを公開する前にレビューするためのメカニズムを提供します。

* 作成者は、コンテンツを作成およびレビューします（ページ、アセット、パブリケーションなどの様々な種類のコンテンツがあります）。
* このコンテンツが、ある時点で Web サイトに公開されます。

![chlimage_1-132](assets/chlimage_1-132.png)

オーサー環境では、AEM の機能は 2 種類の UI により利用できます。パブリッシュ環境では、ユーザーに公開するインターフェイスの全体的なルックアンドフィールをデザインします。

>[!NOTE]
>
>この AEM のドキュメント作成に、AEM 自体が使用されています。
>
>AEM は Dispatcher と共に、公開にも使用されています。

### オーサー環境 {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

>[!NOTE]
>
>コンテンツの作成、編集または公開のための適切なアクセス権限を持つアカウントが必要です。

使用しているインスタンスや、個人のアクセス権限の設定に合わせて、コンテンツに対して次をはじめとする多くのタスクを実行できます。

* ページに対して新しいコンテンツの生成や既存のコンテンツの編集をおこないます。
* あらかじめ定義されたテンプレートを使用して、新しいコンテンツページを作成します。
* アセットやコレクションを作成、編集および管理します。
* パブリケーションを作成、編集および管理します。
* キャンペーンや関連リソースを開発します。
* コミュニティサイトを開発および管理します。
* コンテンツページ、アセットなどを移動、コピーまたは削除します。
* ページ、アセットなどを公開（または非公開に）します。

さらに、コンテンツの管理に役立つ次のような管理タスクがあります。

* 変更の管理方法を制御するワークフロー（パブリケーション前でのレビューの適用など）
* 個々のタスクを調整するプロジェクト

>[!NOTE]
>
>また、AEM は、大部分のタスクについてオーサー環境から[管理](/help/sites-administering/home.md)されます。

#### パブリッシュ環境 {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. ここでは、デザインされたインターフェイスのルック&amp;フィールに従って、Webサイトのページが対象の閲覧者に提供されます。

通常、パブリッシュ環境は保護解除された領域（DMZ）内に配置されます。つまり、インターネットで使用できますが、内部ネットワークの完全保護下にはありません。

AEM サイトが[コミュニティサイト](/help/communities/overview.md)の場合、または [Communities コンポーネント](/help/communities/author-communities.md)を含む場合、サインインしたサイト訪問者（メンバー）は、Communities の機能を利用できます。例えば、フォーラムに投稿したり、コメントを投稿したり、他のメンバーに従ったりできます。 メンバーには、通常、作成者環境に限定されたアクティビティ(新しいページ（コミュニティグループ）の作成、ブログ記事の作成、他のメンバーの投稿のモデレートなど)を実行する権限が与えられます。

>[!NOTE]
>
>用語が一部重複して使用されている場合があります。この状況は次の用語で発生しています。
>
>* **発行／非公開**
   >  コンテンツを公開環境で公開できる（または公開できない）アクションの主な用語は次のとおりです。
   >
   >
* **アクティブ化/非アクティブ化**
   >  これらの用語は、発行/非公開と同義語です。
   >
   >
* **レプリケート／レプリケーション**
   >  これらは、ある環境から別の環境へのデータの移動（ページのコンテンツ、ファイル、コード、ユーザーコメントなど）を示すために使用される技術用語です。例えば、ユーザーコメントの発行時や逆複製時など。
>



#### Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
