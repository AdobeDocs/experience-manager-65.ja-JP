---
title: 集計の基本事項
description: Tally は、メンバーが特定の製品やサービスをどのように評価するかに関するフィードバックを収集する標準的な方法を提供する抽象クラスです。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 1%

---

# 集計の基本事項 {#tally-essentials}

集計は、メンバーが特定の製品やサービスをどのように評価するかに関するフィードバックを収集する標準的な方法を提供する抽象クラスです。 匿名フィードバックはサポートされていません。 サイト訪問者がフィードバックを変更するには、登録してサインインし、参加してサインインする必要があります。 サインインする必要があるので、モデレートが容易になり、複数の投稿を防ぐことで、フィードバックの価値が高まります。

カスタム集計コンポーネントは、抽象集計クラスを拡張して作成できます。

[いいね！](essentials-liking.md) は、肯定的な意見を単純に表現する集計の実装です。

[投票](essentials-voting.md) は、肯定的または否定的な意見を単純に表す集計の実装です。

[評価](rating-basics.md) は、星系を使用して、肯定的な意見から否定的な意見まで様々な意見を表現する集計の実装です。

AEM 6.1 以降、ポーリングコンポーネントは使用できなくなりました。

[レビュー](reviews-basics.md) は、 [コメント](essentials-comments.md) および [評価](rating-basics.md).

## クライアント側の基本事項 {#essentials-for-client-side}

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿済み集計 (UGC) へのアクセス {#accessing-posted-tallies-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils のリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。
