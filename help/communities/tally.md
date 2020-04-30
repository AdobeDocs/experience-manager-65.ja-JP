---
title: 集計の基本事項
seo-title: 集計の基本事項
description: 集計クラスの概要
seo-description: 集計クラスの概要
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 集計の基本事項 {#tally-essentials}

Tallyは抽象クラスで、メンバーが特定の製品やサービスをどのように評価するかに関する標準的なフィードバック収集方法を提供します。 匿名フィードバックはサポートされていません。 サイト訪問者は、登録してサインインし、参加してフィードバックを変更する必要があります。 サインインする必要があると、モデレートが容易になり、複数の投稿を防ぎ、フィードバックの価値を高めることができます。

抽象集計クラスを拡張することによってカスタム集計コンポーネントを作成できます。

[「いいね!」の設定](essentials-liking.md)は、肯定的な意見を単純な形式で表す集計実装です。

[投票](essentials-voting.md)は、肯定的な意見または否定的な意見を単純な形式で表す集計実装です。

[評価](rating-basics.md)は、肯定的な意見から否定的な意見まで幅広い意見を星制度で表す集計実装です。

AEM 6.1以降、ポーリングコンポーネントは使用できなくなります。

[レビュー](reviews-basics.md) は、コメントと評価のハイブリッドであるSCFコ [ンポーネ](essentials-comments.md) ント [](rating-basics.md)。

## クライアント側の基本事項 {#essentials-for-client-side}

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [集計 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [集計エンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### 投稿された集計（UGC）へのアクセス {#accessing-posted-tallies-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダの概要](srp.md) — 概要とリポジトリの使用方法の概要
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md) - Coding Guidelinesを使用したUGCへのアクセス
* [SocialUtilsリファクタリング](socialutils.md) — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。

