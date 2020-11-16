---
title: テストツールおよび追跡ツール
seo-title: テストツールおよび追跡ツール
description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
seo-description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 62%

---


# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEM には次の機能があります。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストおよびデバッグ用メカニズム](/help/sites-developing/developer-mode.md)

オープンソースのテストツールには、次の 2 つがあります。

**Selenium**

Selenium は、ブラウザーでの 1 人のユーザーによる 1 アクティビティごとの機能テストに使用します。テスト手順（クリック数）をHTMLテーブルまたはJavaクラスとして記録します。

For more information see [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter は、要求の追跡に使用します。機能テスト、パフォーマンステスト、ストレステストに使用できます。

For more information see [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

テストの自動化やテスト計画管理のための専用ツールも数多く存在します。

### 追跡 {#tracking}

以下のツールは簡単に入手できます。 ただし、どのような場合でも重要な問題は、プロジェクトチームのすべてのメンバー（パートナーやお客様）に対してデータを利用できることです。

**Bugzilla**

独自の要件に合わせて設定できるバグ追跡システムです。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています。**

これらを追跡に使用する場合：

* 簡単にしておくべきだ。
* 個々のスプレッドシートの数は最小限に抑える必要があります。
* スプレッドシートは定期的に更新します。
* 1 つのマスターコピーだけを維持し、すべての関係者にマスターコピーの保存場所を通知します。
* プロジェクトメンバー全員がアクセスできるようにします。
* セキュリティの問題が(多くの場合は大きな会社で発生)、共通のアクセスが不可能な場合は、コピーがコピーであり更新できないことを全員が理解していれば、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
