---
title: 集計の基本事項
description: メンバーが特定の製品やサービスをどのように評価しているかについて、メンバーからフィードバックを収集する標準的な方法を提供する抽象クラスであるTallyについて説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%
---
# 集計の基本事項 {#tally-essentials}

Tallyは、メンバーが特定の製品やサービスをどのように評価しているかについて、メンバーからフィードバックを収集する標準的な方法を提供する抽象クラスです。 匿名フィードバックはサポートされていません。 サイト訪問者がフィードバックを変更するには、登録してログインし、参加してログインする必要があります。 ログインが必要なため、モデレーションが容易になり、複数の投稿を防ぐことによってフィードバックの価値が向上します。

カスタム集計コンポーネントは、抽象集計クラスを拡張して作成できます。

[いいね](essentials-liking.md)は、肯定的な意見を簡単に表現できる集計の実装です。

[投票](essentials-voting.md)は、肯定的または否定的な意見を表明する単純な形式の集計の実装です。

[評価](rating-basics.md)は、肯定的から否定的な意見の範囲を表現するために星系を使用する集計の実装です。

AEM 6.1以降、ポーリングコンポーネントは使用できなくなりました。

[ レビュー](reviews-basics.md)は、[ コメント ](essentials-comments.md)と[評価](rating-basics.md)のハイブリッドであるSCF コンポーネントです。

## クライアントサイドの基本 {#essentials-for-client-side}

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [APIの合計](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### UGC （投稿済み集計）へのアクセス {#accessing-posted-tallies-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[ ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス ](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
