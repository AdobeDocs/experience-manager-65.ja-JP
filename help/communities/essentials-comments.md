---
title: コメントの基本事項
description: コメントシステム（コメントコンポーネント）の操作と、コミュニティメンバーの投稿でのユーザー生成コンテンツ (UGC) の管理について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 5%

---

# コメントの基本事項 {#comments-essentials}

このページでは、コメントシステム（コメントコンポーネント）の操作の基本と、メンバーがコメントや返信を投稿したときに生成されるユーザー生成コンテンツ (UGC) を管理するためのオプションについて説明します。

コメントコンポーネントは、個々の投稿がコメントコンポーネント（単数）で表されるようにコメントシステムを確立します。 ページに含まれるコメントシステムです。 コメントシステムは、呼び出されると、個々のコメントを作成します。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td>
   <td>はい — でプロパティを編集できます <i>デザイン </i>mode</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
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
   <td> 詳しくは、 <a href="comments.md">コメントの使用</a></td>
  </tr>
 </tbody>
</table>

[クライアント側のカスタマイズ](client-customize.md)

### 1 ページにつき 1 つのインスタンス {#one-instance-per-page}

ページネーションおよびキャッシュやリンクに URL を使用する場合、コメントシステムごとに一意の URL を指定する必要があります。 したがって、1 ページにつき 1 つのコメントシステムのインスタンスのみを使用できます。

その他の機能には、既にコメントシステムが含まれています。 以下の項目が該当します。

* [ブログ](blog-developer-basics.md)
* [Calendar](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ設定の理由リストは、アプリに flagreasonlist.hbs を追加して、内の内容を上書きすることでカスタマイズできます。

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

これは、コメントシステムを拡張するすべてのコンポーネントに適用されます。

## サーバー側の基本事項 {#essentials-for-server-side}

* [コメント API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [コメントエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたコメント (UGC) へのアクセス {#accessing-posted-comments-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils のリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。
