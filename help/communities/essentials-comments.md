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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 6%

---

# コメントの基本事項 {#comments-essentials}

このページでは、コメント・システム（コメント・コンポーネント）の操作の基本と、メンバーがコメントまたは返信を投稿する際に生成されるユーザー生成コンテンツ（UGC）を管理するためのオプションについて説明します。

コメントコンポーネントは、個々の投稿がコメントコンポーネント（単数）で表されるようにコメントシステムを確立します。 ページに掲載されているのはコメントシステムです。 コメントシステムは、呼び出されたときに個々のコメントを作成します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 次を含む </strong></a></td>
   <td>はい – プロパティは <i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br />cq.social.hbs.comments<br />cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td> <a href="comments.md"> コメントの使用 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

[クライアントサイドのカスタマイズ](client-customize.md)

### ページごとに 1 つのインスタンス {#one-instance-per-page}

ページネーションと、キャッシュおよびリンクに URL を使用するには、URL がコメントシステムごとに一意である必要があります。 したがって、コメントシステムのインスタンスは、1 ページにつき 1 つしか使用できません。

その他の機能には、既にコメントシステムが含まれています。 以下の項目が該当します。

* [ブログ](blog-developer-basics.md)
* [Calendar](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ設定された理由のリストは、flagreasonlist.hbs をアプリに追加して内容を上書きすることでカスタマイズできます

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

これは、コメントシステムを拡張するすべてのコンポーネントに適用されます。

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [Comments API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [&#x200B; コメントエンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿されたコメントへのアクセス （UGC） {#accessing-posted-comments-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[&#x200B; ユーザー作成コンテンツのモデレート &#x200B;](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [&#x200B; 共通ストア &#x200B;](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 &#x200B;](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
