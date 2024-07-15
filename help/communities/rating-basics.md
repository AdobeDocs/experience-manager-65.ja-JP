---
title: 評価の基本事項
description: Tally サブクラスの評価コンポーネントを使用して、ログインしたコミュニティメンバーが web サイト上の機能を評価する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 3%

---

# 評価の基本事項 {#rating-essentials}

評価コンポーネントは [ 集計 ](tally.md) サブクラスであり、ログインしたコミュニティメンバーが web サイト上の機能を評価できます。

同じページに投票コンポーネントの複数のインスタンスを配置できます。各インスタンスは、一意の `tally name` プロパティを使用して設定する必要があります。

評価の匿名の投稿はサポートされていません。 サイト訪問者が評価に参加するには、登録してログインする必要があります。 ログインした訪問者（メンバー）は、いつでも評価を変更できます。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> ソーシャル/集計/コンポーネント/hbs/評価</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>はい – プロパティは <i> デザイン </i> モードで編集可能です</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p><a href="rating.md"> 評価の使用 </a> を参照してください。</p> </td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [ 集計 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [ 集計エンドポイント ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿された評価へのアクセス （UGC） {#accessing-posted-ratings-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[ ユーザー生成コンテンツのモデレート ](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [ 共通ストア ](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要 ](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 ](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
