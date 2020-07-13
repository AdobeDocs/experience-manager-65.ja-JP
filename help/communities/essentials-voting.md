---
title: 投票の基本事項
seo-title: 投票の基本事項
description: 投票コンポーネントの概要
seo-description: 投票コンポーネントの概要
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 58%

---


# 投票の基本事項 {#voting-essentials}

[集計](tally.md)のサブクラスである投票コンポーネントは、各メンバーが上下の矢印を選択して意見を示すだけで特定のコンテンツを評価できる便利なツールです。

Placing multiple instances of a voting component on the same page is allowed; each instance must be configured with an unique `tally name` property.

匿名での投票投稿はサポートされていません。サイト訪問者が投票に参加するには、一度だけ登録してサインインする必要があります。サインインした訪問者（会員）は、いつでも投票を変更できます。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>はい - プロパティは<i>デザイン</i>モードで編集可能</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs </strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><p>See <a href="voting.md">Using Voting</a></p> </td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿された投票（UGC）へのアクセス {#accessing-posted-voting-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要.
* [SRPとUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス](accessing-ugc-with-srp.md) — コーディングガイドライン。
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係.

