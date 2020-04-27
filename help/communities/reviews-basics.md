---
title: レビューの基本事項
seo-title: レビューの基本事項
description: レビューとレビューの概要コンポーネント
seo-description: レビューとレビューの概要コンポーネント
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# レビューの基本事項 {#reviews-essentials}

この機能は、連携して動作する 2 つのコンポーネント（レビューとレビュー概要）で構成されます。

Reviews is a composite component based on a [comment system](essentials-comments.md) which contains one or more [rating](rating-basics.md) (tally) components.

匿名でのレビュー投稿はサポートされていません。サイト訪問者は、レビューを追加するには登録し、サインインする必要があります。 サインインした訪問者（メンバー）は、いつでもレビューを更新できます。

## クライアント側の基本事項 {#essentials-for-client-side}

### レビュー {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>はい - プロパティは<i>デザイン</i>モードで編集可能</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>See <a href="reviews.md">Using Reviews</a></td>
  </tr>
 </tbody>
</table>

### レビュー概要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**インクルード可能&#x200B;**](scf.md#add-or-include-a-communities-component) | はい — プロパティは*design *modeで編集可能 |
| [**clientllibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **テンプレート** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **プロパティ** | See [Using Reviews](reviews.md) |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [レビュー API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [レビューエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたレビュー（UGC）へのアクセス {#accessing-posted-reviews-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダの概要](srp.md) — 概要とリポジトリの使用方法の概要
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md) - Coding Guidelinesを使用したUGCへのアクセス
* [SocialUtilsリファクタリング](socialutils.md) — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。

