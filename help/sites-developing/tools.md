---
title: テストツールおよび追跡ツール
seo-title: Testing and Tracking Tools
description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 100%

---

# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEM では以下が提供されます。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストおよびデバッグ用メカニズム](/help/sites-developing/developer-mode.md)

オープンソースのテストツールには、次の 2 つがあります。

**Selenium**

Selenium は、ブラウザーでの 1 人のユーザーによる 1 アクティビティごとの機能テストに使用します。テスト手順（クリック）を HTML テーブルまたは Java クラスとして記録します。

詳しくは、[https://www.seleniumhq.org/](https://www.seleniumhq.org/) を参照してください。

**JMeter**

JMeter は、要求の追跡に使用します。機能テスト、パフォーマンステスト、ストレステストに使用できます。

詳しくは、[https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter) を参照してください。

テストの自動化やテスト計画管理のための専用ツールも数多く存在します。

### 追跡 {#tracking}

以下のツールを簡単に利用できます。ただし、どの場合でも大切なポイントは、プロジェクトチームのすべてのメンバー（パートナーやお客様を含む）がデータを利用できることです。

**Bugzilla**

独自の要件に合わせて設定できるバグ追跡システムです。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています&#x200B;*。*

これらをトラッキングに使用する場合は、次のポイントに留意します。

* シンプルを心がける。
* 個々のスプレッドシートの数は、最小限に抑える必要があります。
* スプレッドシートは定期的に更新します。
* 1 つのマスターコピーだけを維持し、すべての関係者にマスターコピーの保存場所を通知します。
* プロジェクトメンバー全員がアクセスできるようにします。
* セキュリティが問題で（多くの場合、大企業で発生）、共通のアクセスを確立できない場合は、これらがコピーであり更新できないことを全員が理解している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
