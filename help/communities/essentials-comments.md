---
title: コメントの基本事項
description: コメントシステム（コメントコンポーネント）の操作と、コミュニティメンバーの投稿でのユーザー生成コンテンツ（UGC）の管理について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 5%
---
# コメントの基本事項 {#comments-essentials}

このページでは、コメントシステム（コメントコンポーネント）の操作の基本と、メンバーがコメントまたは返信を投稿したときに生成されるユーザー生成コンテンツ（UGC）を管理するためのオプションについて説明します。

コメントコンポーネントは、個々の投稿がコメントコンポーネント（単一）で表されるようにコメントシステムを確立します。 これは、ページに含まれているコメントシステムです。 コメントシステムは、呼び出されたときに個別のコメントを作成します。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> ソーシャル/コモンズ/コンポーネント/hbs/コメント</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>はい – プロパティは<i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td> <a href="comments.md"> コメントの使用</a>を参照してください</td>
  </tr>
 </tbody>
</table>

[クライアントサイドのカスタマイズ](client-customize.md)

### ページごとに1つのインスタンス {#one-instance-per-page}

ページネーションおよびURLを使用してキャッシュとリンクを行うには、URLがコメントシステムごとに一意である必要があります。 したがって、コメントシステムの1つのインスタンスのみがページごとに許可されます。

その他の機能には、コメントシステムが既に含まれています。 以下の項目が該当します。

* [ブログ](blog-developer-basics.md)
* [Calendar](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ付きの理由リストは、アプリにflagreasonlist.hbsを追加して、の内容を上書きすることでカスタマイズできます

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

これは、コメントシステムを拡張する任意のコンポーネントに適用されます。

## サーバーサイドの基本 {#essentials-for-server-side}

* [コメント API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [コメントエンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿されたコメントへのアクセス（UGC） {#accessing-posted-comments-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[&#x200B; ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
