---
title: レビューの基本事項
description: AEM Communitiesのレビューが、1 つ以上の評価（集計）コンポーネントを含んだコメントシステムに基づく複合コンポーネントである方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# レビューの基本事項 {#reviews-essentials}

この機能は、レビューとレビューの概要という、連携して機能する 2 つのコンポーネントで構成されます。

レビューは、1 つ以上の [ 評価 ](essentials-comments.md) （集計）コンポーネントを含む [ コメントシステム ](rating-basics.md) ベースの複合コンポーネントです。

レビューの匿名投稿はサポートされていません。 サイト訪問者がレビューを追加するには、登録してログインする必要があります。 ログインした訪問者（メンバー）は、いつでもレビューを更新できます。

## クライアントサイドの基本事項 {#essentials-for-client-side}

### レビュー {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/レビュー/コンポーネント/hbs/レビュー</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>はい – プロパティは <i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="reviews.md"> レビューの使用 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

### レビューの概要 {#review-summary}

| **resourceType** | ソーシャル/レビュー/コンポーネント/hbs/概要 |
|---|---|
| [**含む**](scf.md#add-or-include-a-communities-component) | 対応 – プロパティは*design*モードで編集可能です |
| [**clientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **プロパティ** | [ レビューの使用 ](reviews.md) を参照してください。 |

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [API を確認 ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [ エンドポイントを確認 ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿されたレビュー（UGC）へのアクセス {#accessing-posted-reviews-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[ ユーザー生成コンテンツのモデレート ](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [ 共通ストア ](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要 ](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 ](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
