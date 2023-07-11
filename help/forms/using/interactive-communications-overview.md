---
title: インタラクティブ通信の概要
seo-title: Interactive Communications Overview
description: この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 61%

---


# インタラクティブ通信の概要 {#interactive-communications-overview}

この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。

![hero-image](do-not-localize/correspondence-management.png)

インタラクティブ通信を使用すると、業務上の書簡、ドキュメント、取引明細書、給付金通知、マーケティング用メール、請求書、ウェルカムキットなど、様々な通信記録の作成と配信を、カスタマイズされた安全な方法で一元的に管理できます。

## 主な機能 {#key-capabilities}

インタラクティブ通信の主な機能は次のとおりです。

- すぐに使用できるフォームデータモデルとの統合により、バックエンドデータベースや MS® Dynamics などの他の CRM システムへのアクセスを簡単かつ合理化できます。
- 印刷チャネルと Web チャネル用の統合オーサリングインターフェイス。印刷チャネルから Web チャネルを自動生成できます。
- 印刷や Web で、分かりやすい視覚的な形式で情報を表示するグラフ
- ドキュメントフラグメントは、ルールエディターとフォームデータモデルをサポートしています
- エージェント UI で、インタラクティブ通信の印刷プレビューと web プレビューを表示できます。
- ドラッグアンドドロップ操作でコンポーネントを配置し、印刷チャネルと Web チャネルを短時間で作成することができます。

## インタラクティブ通信の作成 {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### ワークフロー {#workflow}

インタラクティブ通信を作成するには、インタラクティブ通信の[構築ブロック](#buildingblocks)を準備してから、以下の手順を実行する必要があります。

1. 「[インタラクティブ通信の作成](/help/forms/using/create-interactive-communication.md)」を選択します。

1. [フォームデータモデル](/help/forms/using/data-integration.md)、事前入力サービス、[印刷チャネルと Web チャネルのテンプレート](/help/forms/using/web-channel-print-channel.md)を指定します。プリントチャンネルから web チャンネルを生成することもできます。

1. 必要に応じて[ドラッグ＆ドロップ方式のインターフェイス](/help/forms/using/introduction-interactive-communication-authoring.md)を使用して、ドキュメントフラグメント、画像、コンポーネントを、インタラクティブ通信のプリントチャンネルと web チャンネルに追加します。
1. 挿入されるコンポーネントのプロパティを設定します。次に例を示します。

   1. [画像](/help/forms/using/create-interactive-communication.md#step2)
   1. [テーブル](/help/forms/using/create-interactive-communication.md#tables)（レイアウトフラグメントを含む）
   1. [グラフ](/help/forms/using/chart-component-interactive-communications.md)
   1. [ドキュメントフラグメント](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 印刷チャネルと Web チャネルのプレビューを表示し、必要に応じてインタラクティブ通信を編集します。
1. エージェントはエージェント UI を使用して [インタラクティブ通信の準備](/help/forms/using/prepare-send-interactive-communication.md) 受信者/後処理に送信するために使用します。

### 構築ブロック {#buildingblocks}

インタラクティブ通信の作成に必要な構築ブロックを次に示します。

- [フォームデータモデル](/help/forms/using/data-integration.md)
- [印刷チャネルと Web チャネルのテンプレート](/help/forms/using/web-channel-print-channel.md)
- [ドキュメントフラグメント](/help/forms/using/document-fragments.md)
- 画像
- Web チャンネル用の[テーマ](/help/forms/using/themes.md)

## インタラクティブ通信と Correspondence Management の比較 {#interactive-communications-vs-correspondence-management}

インタラクティブ通信は、顧客通信を作成するためのデフォルトの方法です。顧客通信を作成する場合は、インタラクティブ通信を使用することをお勧めします。AEM 6.3 Forms または AEM 6.2 Forms で作成したレターを引き続き使用する場合は、[互換性パッケージをインストールする必要があります](/help/forms/using/compatibility-package.md)。以下の表に、インタラクティブ通信の機能とレターの機能の違いを示します。

<table>
 <tbody>
  <tr>
   <td><strong>機能</strong></td>
   <td><strong>インタラクティブコミュニケーション</strong></td>
   <td><strong>レター</strong></td>
  </tr>
  <tr>
   <td>出力</td>
   <td>印刷出力と Web 出力</td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>Schema</td>
   <td>フォームデータモデル </td>
   <td>データディクショナリ </td>
  </tr>
  <tr>
   <td>ローカリゼーション</td>
   <td>フォームデータモデルではサポートされていません</td>
   <td>データディクショナリでサポートされています</td>
  </tr>
  <tr>
   <td>ルールエディター</td>
   <td>
    <ul>
     <li>インライン条件を作成するためのテキストおよび条件サポートのルールエディター</li>
     <li>インタラクティブ通信エディターは、Web チャネルのコンポーネントに対するルールの適用をサポートしています</li>
    </ul> </td>
   <td>条件式を作成するための UI がありません</td>
  </tr>
  <tr>
   <td>オーサリング</td>
   <td>印刷チャネルと Web チャネルを構築するためのドラッグ&amp;ドロップインターフェイス</td>
   <td>ドラッグ＆ドロップ機能はない </td>
  </tr>
  <tr>
   <td>グラフ</td>
   <td>印刷チャネルと Web チャネルでサポートされるグラフ</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>テーマ</td>
   <td>テーマを使用して Web チャネルのスタイルを設定</td>
   <td>テーマをサポートしていません</td>
  </tr>
   <tr>
   <td>ドラフト</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
   <tr>
   <td>送信</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
  <tr>
   <td>監査</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
   <tr>
   <td>バージョン管理</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
   <td>バッチ処理</td>
   <td>サポート対象 </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>エージェント署名</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>リモート関数</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
 </tbody>
</table>
