---
title: インタラクティブ通信の概要
description: この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '487'
ht-degree: 100%

---


# インタラクティブ通信の概要 {#interactive-communications-overview}

この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。

![hero-image](do-not-localize/correspondence-management.png)

インタラクティブ通信を使用すると、業務上の書簡、ドキュメント、取引明細書、給付金通知、マーケティング用メール、請求書、ウェルカムキットなど、様々な通信記録の作成と配信を、カスタマイズされた安全な方法で一元的に管理できます。

## 主な機能 {#key-capabilities}

以下に、インタラクティブ通信の主要な機能を示します。

- すぐに使用できる、フォームデータモデルとの統合機能が付属しています。この機能により、バックエンドのデータベースと、MS® Dynamics などの CRM システムに簡単にアクセスすることができます。
- 印刷チャネルと web チャネル用の統合オーサリングインターフェイスが用意されています。このインターフェイスにより、印刷チャネルから web チャネルを自動的に生成することができます。
- 印刷チャネルと web チャネルでグラフを使用して、視覚的に分かりやすい形式で情報を表現することができます。
- ドキュメントフラグメントで、ルールエディターとフォームデータモデルを使用することができます。
- エージェント UI で、インタラクティブ通信の印刷プレビューと web プレビューを表示できます。
- ドラッグアンドドロップ操作でコンポーネントを配置し、印刷チャネルと Web チャネルを短時間で作成することができます。

## インタラクティブ通信の作成 {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### ワークフロー {#workflow}

インタラクティブ通信を作成するには、インタラクティブ通信の[構築ブロック](#buildingblocks)を準備してから、以下の手順を実行する必要があります。

1. 「[インタラクティブ通信の作成](/help/forms/using/create-interactive-communication.md)」を選択します。

1. [フォームデータモデル](/help/forms/using/data-integration.md)、事前入力サービス、[印刷チャネルと Web チャネルのテンプレート](/help/forms/using/web-channel-print-channel.md)を指定します。プリントチャンネルから web チャンネルを生成することもできます。

1. 必要に応じて[ドラッグ＆ドロップ方式のインターフェイス](/help/forms/using/introduction-interactive-communication-authoring.md)を使用して、ドキュメントフラグメント、画像、コンポーネントを、インタラクティブ通信のプリントチャンネルと web チャンネルに追加します。
1. 追加したコンポーネントのプロパティを設定します。例えば、以下のようなコンポーネントがあります。

   1. [画像](/help/forms/using/create-interactive-communication.md#step2)
   1. [テーブル](/help/forms/using/create-interactive-communication.md#tables)（レイアウトフラグメントを含む）
   1. [グラフ](/help/forms/using/chart-component-interactive-communications.md)
   1. [ドキュメントフラグメント](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 印刷チャネルと web チャネルのプレビューを表示し、必要に応じてインタラクティブ通信を編集します。
1. エージェントはエージェント UI を使用して、インタラクティブ通信を受信者または後処理に送信するための[準備](/help/forms/using/prepare-send-interactive-communication.md)を行います。

### 構築ブロック {#buildingblocks}

インタラクティブ通信を作成するために必要な構築ブロックを以下に示します。

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
   <td>フォームデータモデルではサポートされていない</td>
   <td>データディクショナリでサポートされている</td>
  </tr>
  <tr>
   <td>ルールエディター</td>
   <td>
    <ul>
     <li>テキストと条件でルールエディターを使用して、インライン条件を作成できる</li>
     <li>インタラクティブ通信エディターで、web チャネルのコンポーネントにルールを適用できる</li>
    </ul> </td>
   <td>条件式を作成するための UI はない</td>
  </tr>
  <tr>
   <td>オーサリング</td>
   <td>ドラッグ＆ドロップ方式のインターフェイスを使用して、印刷チャネルと web チャネルを作成できる</td>
   <td>ドラッグ＆ドロップ機能はない </td>
  </tr>
  <tr>
   <td>グラフ</td>
   <td>印刷チャネルと web チャネルでグラフがサポートされている</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>テーマ</td>
   <td>テーマを使用して web チャネルのスタイルを設定できる</td>
   <td>テーマはサポートされていない</td>
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
