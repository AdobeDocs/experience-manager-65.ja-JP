---
title: レビューの基本事項
description: AEM Communitiesのレビューが、1つ以上の評価（集計）コンポーネントを含むコメントシステムに基づく複合コンポーネントである方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%
---
# レビューの基本事項 {#reviews-essentials}

この機能は、レビューとレビューの概要という2つのコンポーネントで構成されています。

レビューは、[ コメントシステム ](essentials-comments.md)に基づく複合コンポーネントで、1つ以上の[評価](rating-basics.md) （集計）コンポーネントを含みます。

レビューの匿名への投稿はサポートされていません。 レビューを追加するには、サイト訪問者が登録してログインする必要があります。 ログインした訪問者（メンバー）は、いつでもレビューを更新できます。

## クライアントサイドの基本 {#essentials-for-client-side}

### レビュー {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/レビュー/コンポーネント/hbs/レビュー</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>はい – プロパティは<i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="reviews.md"> レビューの使用</a>を参照してください</td>
  </tr>
 </tbody>
</table>

### レビューの概要 {#review-summary}

| **resourceType** | ソーシャル/レビュー/コンポーネント/hbs/概要 |
|---|---|
| [**包含可能**](scf.md#add-or-include-a-communities-component) | はい – プロパティは*design *モードで編集可能です |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **テンプレート** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **プロパティ** | [ レビューの使用](reviews.md)を参照してください |

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [APIを確認](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [エンドポイントの確認](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿されたレビューへのアクセス（UGC） {#accessing-posted-reviews-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[ ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス ](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
