---
title: 集計の基本事項
description: Tally が、メンバーから特定の製品やサービスの価値をどのように評価するかについてのフィードバックを収集する標準的な方法を提供する抽象クラスであることを説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# 集計の基本事項 {#tally-essentials}

Tally は、メンバーが特定の製品やサービスをどのように評価しているかに関するフィードバックを収集するための標準的な方法を提供する抽象クラスです。 匿名フィードバックはサポートされていません。 サイト訪問者が参加するには登録してログインし、フィードバックを変更するにはログインする必要があります。 ログインする必要があるため、モデレートが容易になり、複数の投稿を防ぐことでフィードバックの価値が高まります。

抽象的な集計クラスを拡張することで、カスタムの集計コンポーネントを作成できます。

[お気に入り](essentials-liking.md) は、肯定的な意見を表現する単純な形式の集計の実装です。

[投票](essentials-voting.md) は、肯定的または否定的な意見を表現する単純な形式の集計の実装です。

[評価](rating-basics.md) は、正から負の意見の範囲を表現するために星系を使用する計数の実装です。

AEM 6.1 以降、ポーリングコンポーネントは使用できなくなりました。

[レビュー](reviews-basics.md) は、のハイブリッドである SCF コンポーネントです [コメント](essentials-comments.md) および [格付け](rating-basics.md).

## クライアントサイドの基本事項 {#essentials-for-client-side}

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [集計 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿済みテーブルへのアクセス（UGC） {#accessing-posted-tallies-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
参照： [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 現在、の使用 [共通店舗](working-with-srp.md) （UGC の場合、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます）。

**リポジトリ内の UGC の場所と形式は、警告なしに変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングガイドライン
* [SocialUtils のリファクタリング](socialutils.md)  – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする。
