---
title: テストツールおよび追跡ツール
description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%
---
# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEM には次の機能があります。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストおよびデバッグ用メカニズム](/help/sites-developing/developer-mode.md)

オープンソースのテストツールには、次の 2 つがあります。

**Selenium**

Selenium は、ブラウザーでの 1 人のユーザーによる 1 アクティビティごとの機能テストに使用します。 テスト手順（クリック）を HTML テーブルまたは Java™ クラスとして記録します。

詳しくは、[https://www.selenium.dev/](https://www.selenium.dev/) を参照してください。

**JMeter**

JMeter は、リクエストの追跡に使用します。機能テスト、パフォーマンステスト、ストレステストに使用できます。

詳しくは、[https://jmeter.apache.org/](https://jmeter.apache.org/) を参照してください。

テストの自動化やテスト計画管理のための専用ツールも数多くあります。

### トラッキング {#tracking}

以下のツールを簡単に利用できます。 ただし、どの場合でも大切なポイントは、プロジェクトチームのすべてのメンバー（パートナーやお客様を含む）がデータを利用できることです。

**Bugzilla**

独自の要件に合わせて設定できるバグトラッキングシステムです。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています&#x200B;*。*

これらのスプレッドシートをトラッキングに使用する場合は、次のポイントに留意します。

* シンプルを心がける。
* 個々のスプレッドシートの数は、最小限に抑える必要があります。
* スプレッドシートは定期的に更新します。
* 1 つのプライマリコピーだけを維持し、すべての関係者にプライマリコピーの保存場所を通知します。
* プロジェクトメンバー全員がアクセスできるようにします。
* セキュリティに問題があり（大企業でよく起こります）、共通のアクセスが不可能な場合は、これらのスプレッドシートがコピーであり更新できないことを全員が理解している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件をトラッキングするための専用ツールは数多くあります。
