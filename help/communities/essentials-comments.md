---
title: コメントの基本事項
seo-title: Comments Essentials
description: コメントコンポーネントの概要
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 55%

---

# コメントの基本事項 {#comments-essentials}

このページでは、コメントシステム（コメントコンポーネント）の操作に関する基本事項と、メンバーがコメントや返信を投稿したときに生成されるユーザー生成コンテンツ (UGC) を管理するためのオプションを提供します。

個々の投稿がそれぞれ単一のコメントコンポーネントで表されるように、コメントシステムが確立されます。ページに含まれるコメントシステムです。 コメントシステムは、呼び出されると個々のコメントを作成します。

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
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs </strong></a></td>
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

### ページごとに 1 つのインスタンス {#one-instance-per-page}

ページネーションをおこなう場合、およびキャッシュやリンクのために URL を使用する場合は、コメントシステムごとに一意の URL を使用する必要があります。したがって、1 ページにつき 1 つのコメントシステムのインスタンスのみを使用できます。

その他の機能には、コメントシステムが既に含まれています。以下のとおりです。

* [ブログ](blog-developer-basics.md)
* [Calendar](calendar-basics-for-developers.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [Q&amp;A](qna-essentials.md)
* [レビュー](reviews-basics.md)

### フラグ設定理由リスト {#flag-reason-list}

フラグ設定理由リストは、アプリケーションに flagreasonlist.hbs を追加して内容を上書きすることによってカスタマイズできます。

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

これは、コメントシステムのすべての拡張コンポーネントに適用されます。

## サーバー側の基本事項 {#essentials-for-server-side}

* [コメント API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [コメントエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたコメント（UGC）へのアクセス {#accessing-posted-comments-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。
