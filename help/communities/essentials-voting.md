---
title: 投票の基本事項
description: 投票コンポーネントの使用方法を説明します。このコンポーネントを使用すると、メンバーは上矢印または下矢印を選択して意見を示し、特定のコンテンツを評価できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# 投票の基本事項 {#voting-essentials}

投票コンポーネント、 [集計](tally.md) サブクラスは、メンバーが上または下の矢印をクリックするだけで自分の意見を示すことで、コンテンツの特定の部分を評価できる便利なツールです。

同じページに投票コンポーネントの複数のインスタンスを配置できます。各インスタンスは、一意のインスタンスを設定する必要があります `tally name` プロパティ。

投票の匿名の投稿はサポートされていません。 サイト訪問者が投票に参加するには、一度だけ登録してログインする必要があります。 ログインした訪問者（メンバー）は、いつでも投票を変更できます。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/集計/コンポーネント/hbs/投票</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>はい – プロパティはで編集可能です。 <i>デザイン </i>モード</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>参照： <a href="voting.md">投票の使用</a></p> </td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [集計 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿された投票（UGC）へのアクセス {#accessing-posted-voting-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
参照： [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 現在、の使用 [共通店舗](working-with-srp.md) （UGC の場合、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます）。

**リポジトリ内の UGC の場所と形式は、警告なしに変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングのガイドライン
* [SocialUtils のリファクタリング](socialutils.md)  – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする。
