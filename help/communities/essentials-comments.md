---
title: コメントの基本事項
seo-title: コメントの基本事項
description: コメントコンポーネントの概要
seo-description: コメントコンポーネントの概要
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# コメントの基本事項 {#comments-essentials}

このページでは、コメントシステム（コメントコンポーネント）と、メンバーがコメントや返信を投稿する際に生成されるユーザー生成コンテンツ(UGC)を管理するためのオプションを操作する際の基本的な作業を提供します。

個々の投稿がそれぞれ単一のコメントコンポーネントで表されるように、コメントシステムが確立されます。ページに含まれるコメントシステムです。 コメントシステムを呼び出すと、個々のコメントが作成されます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>はい - プロパティは<i>デザイン</i>モードで編集可能</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>Clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td> See <a href="comments.md">Using Comments</a></td>
  </tr>
 </tbody>
</table>

[クライアント側のカスタマイズ](client-customize.md)

### ページごとに 1 つのインスタンス {#one-instance-per-page}

ページネーションをおこなう場合、およびキャッシュやリンクのために URL を使用する場合は、コメントシステムごとに一意の URL を使用する必要があります。したがって、1ページにつき1つのコメントシステムのインスタンスのみが許可されます。

その他の機能には、コメントシステムが既に含まれています。以下のとおりです。

* [ブログ](blog-developer-basics.md)
* [カレンダー](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ設定理由リストは、アプリケーションに flagreasonlist.hbs を追加して内容を上書きすることによってカスタマイズできます。

* /libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs

これは、コメントシステムのすべての拡張コンポーネントに適用されます。

## サーバー側の基本事項 {#essentials-for-server-side}

* [コメント API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [コメントエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたコメント（UGC）へのアクセス {#accessing-posted-comments-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージ・リソース・プロバイダの概要](srp.md) — 概要とリポジトリの使用状況の概要
* [SRPとUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例
* [SRPを使用したUGCへのアクセス](accessing-ugc-with-srp.md) — コーディングガイドライン
* [SocialUtilsリファクタリング](socialutils.md) — 廃止されたユーティリティメソッドを現在のSRPユーティリティメソッドにマッピング

