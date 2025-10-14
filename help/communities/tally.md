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

[&#x200B; 好き &#x200B;](essentials-liking.md) は、肯定的な意見を表現するための単純な形式の集計の実装です。

[&#x200B; 投票 &#x200B;](essentials-voting.md) は、肯定的または否定的な意見を表現する単純な形の集計の実装です。

[&#x200B; レーティング &#x200B;](rating-basics.md) とは、星評価を用いてポジティブからネガティブまで幅広い意見を表現する集計の実装です。

AEM 6.1 以降、ポーリングコンポーネントは使用できなくなりました。

[&#x200B; レビュー &#x200B;](reviews-basics.md) は、[&#x200B; コメント &#x200B;](essentials-comments.md) と [&#x200B; 評価 &#x200B;](rating-basics.md) のハイブリッドである SCF コンポーネントです。

## クライアントサイドの基本事項 {#essentials-for-client-side}

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [&#x200B; 集計 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [&#x200B; 集計エンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### 投稿済みテーブルへのアクセス（UGC） {#accessing-posted-tallies-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[&#x200B; ユーザー生成コンテンツのモデレート &#x200B;](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [&#x200B; 共通ストア &#x200B;](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 &#x200B;](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
