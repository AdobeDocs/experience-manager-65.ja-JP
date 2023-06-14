---
title: テストツールおよび追跡ツール
description: AEMは、コンポーネント UI のテスト用のフレームワークと、コンポーネントのテストとデバッグをおこなうためのメカニズムを提供します
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 36%

---

# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEMには次の機能があります。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストとデバッグを行うメカニズム](/help/sites-developing/developer-mode.md).

次の 2 つのオープンソーステストツールを示します。

**Selenium**

Selenium は、アクティビティごとに 1 人のユーザーでブラウザーの機能テストに使用されます。 テスト手順（クリック）をHTMLテーブルまたは Java™クラスとして記録します。

詳しくは、 [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter は、リクエストの追跡に使用され、機能、パフォーマンス、および応力のテストに使用できます。

詳しくは、 [https://jmeter.apache.org/](https://jmeter.apache.org/).

また、テストを自動化し、テスト計画を管理するための独自のツールも多数用意されています。

### トラッキング {#tracking}

以下のツールを簡単に利用できます。ただし、どの場合でも大切なポイントは、プロジェクトチームのすべてのメンバー（パートナーやお客様を含む）がデータを利用できることです。

**バグジラ**

独自の要件に合わせて設定できるバグ追跡システム。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています&#x200B;*。*

これらのスプレッドシートを追跡に使用する場合は、次の手順に従います。

* シンプルを心がける。
* 個々のスプレッドシートの数は、最小限に抑える必要があります。
* 定期的に更新する必要があります。
* 1 つのプライマリ・コピーのみを管理し、すべてのユーザーがプライマリ・コピーの場所を把握する必要があります。
* すべてのプロジェクトメンバーがアクセスできるようにする必要があります。
* セキュリティが問題（多くの場合、大企業で発生）であり、共通のアクセスが不可能な場合は、全員がこれらのスプレッドシートがコピーであり、更新できないことを理解している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
