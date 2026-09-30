---
title: 評価の基本事項
description: 評価コンポーネントであるTally サブクラスを使用して、サインインしたコミュニティメンバーがweb サイト上の機能を評価する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 2%
---
# 評価の基本事項 {#rating-essentials}

評価コンポーネント [tally](tally.md) サブクラスを使用すると、サインイン済みのコミュニティ メンバーは、web サイト上の機能を評価できます。

同じページに投票コンポーネントの複数のインスタンスを配置することは許可されています。各インスタンスは一意の`tally name` プロパティで設定する必要があります。

評価の匿名での投稿はサポートされていません。 サイト訪問者が評価に参加するには、登録とログインが1回のみ必要です。 サインインした訪問者（メンバー）は、いつでも評価を変更できます。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> ソーシャル/集計/コンポーネント/hbs/評価</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>はい – プロパティは<i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p><a href="rating.md">評価の使用</a>を参照してください</p> </td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [APIの合計](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### UGC （Posted Ratings）へのアクセス {#accessing-posted-ratings-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[ ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md)を使用したUGCへのアクセス – コーディング ガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
