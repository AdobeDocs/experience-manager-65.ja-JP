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
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 52%

---

# レビューの基本事項 {#reviews-essentials}

この機能は、連携して動作する 2 つのコンポーネント（レビューとレビュー概要）で構成されます。

レビューは、[コメントシステム](essentials-comments.md)に基づく複合コンポーネントで、[評価](rating-basics.md)（集計）コンポーネントが1つ以上含まれます。

匿名でのレビュー投稿はサポートされていません。サイト訪問者は、レビューを追加するには、登録してサインインする必要があります。 サインインした訪問者（メンバー）は、いつでもレビューを更新できます。

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
   <td><a href="reviews.md">レビューの使用</a>を参照</td>
  </tr>
 </tbody>
</table>

### レビュー概要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**インクルード可能**](scf.md#add-or-include-a-communities-component) | はい — プロパティは*デザイン*モードで編集可能 |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **テンプレート** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **プロパティ** | [レビューの使用](reviews.md)を参照 |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [レビュー API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [レビューエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿されたレビュー(UGC)へのアクセス{#accessing-posted-reviews-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  — 概要とリポジトリの使用方法の概要。
* [SRPとUGCの基本事項](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRPによるUGCへのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン
* [SocialUtilsのリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。
