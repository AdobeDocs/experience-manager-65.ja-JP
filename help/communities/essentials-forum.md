---
title: フォーラムの基本事項
description: Adobe Experience Manager Communities のフォーラム機能を使用するための基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 622cf6ca-f119-4310-ad14-537576bd6f6d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# フォーラムの基本事項 {#forum-essentials}

このページでは、フォーラム機能の操作に関する重要な情報を提供します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>ソーシャル/フォーラム/コンポーネント/hbs/フォーラム<br /> ソーシャル/フォーラム/コンポーネント/hbs/トピック<br /> ソーシャル/フォーラム/コンポーネント/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>含める</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="forum.md">フォーラム機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [Forum API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [フォーラムエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### フォーラム機能 {#forum-function}

を含むコミュニティサイト構造 [フォーラム機能](functions.md#forum-function)、設定済みのを含む `forum` コンポーネントと、モデレート、タグ付け、翻訳に影響する設定。

### フォーラム投稿へのアクセス（UGC） {#accessing-forum-posts-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
参照： [ユーザー作成コンテンツのモデレート](moderate-ugc.md).

Adobe Experience Manager 6.1 Communities での使用 [共通店舗](working-with-srp.md) （UGC の場合、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます）。

**リポジトリ内の UGC の場所と形式は、警告なしに変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングガイドライン
* [SocialUtils のリファクタリング](socialutils.md)  – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする。
