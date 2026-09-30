---
title: フォーラムの基本事項
description: Adobe Experience Manager Communitiesのフォーラム機能を操作する際の基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 622cf6ca-f119-4310-ad14-537576bd6f6d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 3%
---
# フォーラムの基本事項 {#forum-essentials}

このページでは、フォーラム機能の操作に必要な情報を提供します。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="forum.md"> フォーラム機能</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [フォーラム API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [フォーラムエンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### フォーラム機能 {#forum-function}

[&#x200B; フォーラム関数](functions.md#forum-function)を含むコミュニティサイト構造には、設定済みの`forum` コンポーネントと、モデレーション、タグ付け、翻訳に影響を与える設定が含まれています。

### フォーラム投稿へのアクセス（UGC） {#accessing-forum-posts-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[&#x200B; ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

Adobe Experience Manager 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
