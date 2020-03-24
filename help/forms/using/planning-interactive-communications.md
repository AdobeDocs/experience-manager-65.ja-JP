---
title: '"チュートリアル：インタラクティブ通信の計画"'
seo-title: インタラクティブ通信の計画
description: インタラクティブ通信用の分析の計画
seo-description: インタラクティブ通信用の分析の計画
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375

---


# チュートリアル：インタラクティブ通信の計画 {#tutorial-plan-the-interactive-communication}

インタラクティブ通信用の分析の計画

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

This tutorial is a step in the [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) series. チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

インタラクティブ通信の計画の第一歩は、インタラクティブ通信の内容を確定することです。法務部門、経理部門、サポート部門、マーケティング部門などのサブジェクトマターエキスパート（SME）は、その内容を確定するのに役に立ちます。内容が確定したら、内容を分析してインタラクティブ通信の作成に必要な各種アセットタイプを特定する必要があります。

## 計画の考慮事項 {#planning-considerations}

インタラクティブ通信には、次の要素が含まれます。

* **スタティックテキスト**&#x200B;には多くの場合、すべての顧客への通信に含まれる一般的なインタラクティブ通信の一部が含まれます。例えば、ヘッダー、フッター、あいさつ文、免責事項などです。
* **バックエンドシステムが作成元のデータ（フォームデータモデル）**&#x200B;は、顧客固有で、インタラクティブ通信と動的にマージされます。例えば、ポリシー番号や住所はフォームデータモデルを使用することができます。
* 印刷および Web 版のインタラクティブ通信用の&#x200B;**レイアウトまたはテンプレート**。
* インタラクティブ通信に配置する多様なテキスト段落の&#x200B;**順序**。
* **通信を送信する前に通信をカスタマイズする最前線の従業員(エージェントUI** )が入力したデータ。 例えば、支払期日です。

* **条件付きデータ**&#x200B;は、事前定義された条件に基づいて作成されます。例えば、インタラクティブな通信が生成された日付です。
* ロゴや署名画像など&#x200B;**リポジトリに保存された画像**。会社ロゴなどの画像は、ほとんど、またはすべての通信に表示されます。
* **グラフやテーブル**&#x200B;は、インタラクティブ通信の複雑なデータ表示を簡略化する必要があります。

## インタラクティブ通信の分析 {#anatomy-of-the-interactive-communication}

インタラクティブ通信の作成に使用する内容および要素が確定したら、インタラクティブ通信の分析を作成することができます。分析には、「[計画の考慮事項](/help/forms/using/planning-interactive-communications.md#planning-considerations)」セクションに記載されている詳細が必要です。ユースケースに基づいて、通信会社が顧客に送る毎月の請求書の分析事例は次のとおりです。

分析には、次の入力モードでのデータが含まれます。

* 静的テキスト
* フォームデータモデル
* エージェント UI
* 条件付きデータ
* 画像

各セクションの太字のテキストはスタティックテキストを表します。データベースには、顧客、請求書、および通話表が含まれます。 フォームデータモデルは、これらのテーブルのいずれかのデータを受信することができます。For more information, see [Create form data model](/help/forms/using/create-form-data-model0.md).

次のテーブルに、インタラクティブ通信の分析内の各フィールドのデータソースを示します。

<table>
 <tbody>
  <tr>
   <td>セクション</td>
   <td>静的テキスト</td>
   <td>FDM </td>
   <td>エージェント UI</td>
   <td>画像</td>
  </tr>
  <tr>
   <td>請求明細</td>
   <td><p>請求書番号</p> <p>請求日</p> <p>請求期間</p> <p>計画</p> </td>
   <td><p>「<strong>計画</strong>」フィールドの値</p> <p>テーブル - お客様</p> </td>
   <td><p>次のフィールドに値を入力します。</p>
    <ul>
     <li>請求書番号</li>
     <li>請求日</li>
     <li>請求期間</li>
    </ul> <p> </p> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>顧客情報</td>
   <td><p>供給場所</p> <p>都道府県コード</p> <p>携帯電話番号</p> <p>代替電話番号</p> <p>関係番号</p> <p>接続数</p> </td>
   <td><p>次のフィールドに値を入力します。</p>
    <ul>
     <li>名前</li>
     <li>アドレス</li>
     <li>携帯電話番号</li>
     <li>代替電話番号</li>
     <li>関係番号</li>
    </ul> <p>テーブル - お客様</p> </td>
   <td><p>次のフィールドに値を入力します。</p>
    <ul>
     <li>供給場所</li>
     <li>都道府県コード</li>
     <li>接続数</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>請求内容</td>
   <td><p>繰越請求額</p> <p>支払い</p> <p>調整</p> <p>現在の請求期間の料金</p> <p>請求額</p> <p>期限</p> </td>
   <td><p>Value for the <strong>Charges current bill period </strong> field</p> <p>テーブル - 請求</p> </td>
   <td><p>次のフィールドに値を入力します。</p>
    <ul>
     <li>繰越請求額</li>
     <li>支払い</li>
     <li>調整</li>
     <li>請求額</li>
     <li>期限</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>請求概要</td>
   <td><p>通話料金</p> <p>会議通話料金</p> <p>SMS 料金 </p> <p>携帯インターネット料金</p> <p>国内ローミング料金</p> <p>国際ローミング料金</p> <p>付加価値サービス料金</p> <p>合計請求金額</p> <p>合計支払金額</p> <p>付加価値サービス料フィールドの条件</p> </td>
   <td><p>次のフィールドに値を入力します。</p>
    <ul>
     <li>通話料金</li>
     <li>会議通話料金</li>
     <li>SMS 料金 </li>
     <li>携帯インターネット料金</li>
     <li>国内ローミング料金</li>
     <li>国際ローミング料金</li>
     <li>付加価値サービス料金</li>
     <li>合計請求金額（usagecharges 計算フィールド）</li>
     <li>買掛金合計（usagecharges計算済フィールド）</li>
    </ul> <p>テーブル - 請求</p> </td>
   <td>フィールドなし</td>
   <td>--</td>
  </tr>
  <tr>
   <td>通話明細 - 発信</td>
   <td><p>列の名前：</p>
    <ul>
     <li>日付</li>
     <li>時刻</li>
     <li>番号</li>
     <li>デュレーション (ms)</li>
     <li>料金</li>
    </ul> </td>
   <td><p>すべての値</p> <p>テーブル - 通話</p> </td>
   <td>フィールドなし</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Pay Now</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>付加価値サービス</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

