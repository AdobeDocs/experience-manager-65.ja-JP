---
title: Adobe Classifications
seo-title: Adobe Classifications
description: Adobe Classifications について説明します。
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '600'
ht-degree: 100%

---

# Adobe Classifications{#adobe-classifications}

Adobe Classifications は、分類データをスケジュールに従って [Adobe Analytics](/help/sites-administering/adobeanalytics.md) にエクスポートします。SAINT Exporter は、**com.adobe.cq.scheduled.exporter.Exporter** の実装です。

これを設定するには：

1. **ナビゲーション**&#x200B;を使用して、**ツール**、**クラウドサービス**&#x200B;を選択し、**従来のクラウドサービス**&#x200B;を選択します。
1. **Adobe Analytics** までスクロールして、**設定を表示**&#x200B;を選択します。
1. 「Adobe Analytics 設定」の横にある **[+]** リンクをクリックします。

1. **フレームワークを作成**&#x200B;ダイアログで、次の操作を実行します。

   * 「**タイトル**」を指定します。
   * オプションで、リポジトリにフレームワークの詳細を保存するノードの&#x200B;**名前**&#x200B;を指定できます。
   * 「**Adobe Analytics Classifications**」を選択します。

   「**作成**」をクリックします。

   ![フレームワークを作成ダイアログ](assets/aa-25.png)

1. **分類設定**&#x200B;ダイアログが開き、編集できます。

   ![分類設定ダイアログ](assets/aa-classifications-settings.png)

   プロパティには、次が含まれています。

   | **フィールド** | **説明** |
   |---|---|
   | 有効 | 「**はい**」を選択すると、Adobe Classifications の設定が有効になります。 |
   | 競合時に上書き | 「**はい**」を選択すると、データの競合が上書きされます。デフォルトでは、これは「**いいえ**」に設定されています。 |
   | 削除処理 | 「**はい**」に設定すると、書き出された後に処理したノードが削除されます。デフォルトは、「**False**」です。 |
   | ジョブの書き出しに関する説明 | Adobe Classifications ジョブの説明を入力します。 |
   | 通知電子メール | Adobe Classifications の通知用のメールアドレスを入力します。 |
   | レポートスイート | 読み込みジョブを実行するレポートスイートを入力します。 |
   | データセット | 読み込みジョブを実行するデータセット関連 ID を入力します。 |
   | 変換サービス | ドロップダウンメニューから、変換サービスの実装を選択します。 |
   | データソース | データコンテナのパスに移動します。 |
   | スケジュールを書き出し | 書き出すスケジュールを選択します。デフォルトは 30 分ごとです。 |

1. 「**OK**」をクリックして設定を保存します。

## ページサイズの変更 {#modifying-page-size}

レコードは、ページで処理されます。デフォルトでは、Adobe Classifications はページサイズが 1,000 のページを作成します。

Adobe Classifications の定義に従い、ページの最大サイズは 25,000 に設定ができます（Felix コンソールから変更可）。エクスポート中に、Adobe Classifications はソースノードをロックして、同時変更を防ぎます。ノードは、書き出し後、エラー時またはセッション終了時にロックを解除されます。

ページサイズを変更するには：

1. **https://&lt;host>:&lt;port>/system/console/configMgr** にある OSGI コンソールに移動し、「**Adobe AEM Classifications Exporter**」を選択します。

   ![aa-26](assets/aa-26.png)

1. 「**書き出しページサイズ**」を必要に応じて更新し、**保存**&#x200B;をクリックします。

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe Classifications は、以前は SAINT Exporter と呼ばれていました。

SAINT Exporter は、変換サービスを使用して、書き出しデータを特別な形式に変換できます。Adobe Classifications では、Transformer インターフェイスを実装するサブインターフェイス `SAINTTransformer<String[]>` が提供されています。このインターフェイスは、データタイプを SAINT API で使用される `String[]` に制限し、マーカーインターフェイスで対応するサービスを検索して選択するために使用されます。

デフォルト実装の SAINTDefaultTransformer では、書き出しソースの子リソースは、keys というプロパティ名と values というプロパティ値を持つレコードとして扱われます。**キー**&#x200B;列は、最初の列として自動的に追加され、その値がノード名になります。名前空間プロパティ（`:` を含む）は無視されます。

*ノード構造：*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = ﻿﻿My Product Name (String)
      * Price = 120.90 (String)
      * Size = M (String)
      * Color = black (String)
      * Color^Code = 101 (String)

**SAINT ヘッダーおよびレコード：**

| **キー** | **製品** | **価格** | **サイズ** | **カラー** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | My Product Name | 120.90 | M | 黒 | 101 |

プロパティには、次が含まれています。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティのパス</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>transformer</td>
   <td>SAINTTransformer 実装のクラス名</td>
  </tr>
  <tr>
   <td>email</td>
   <td>通知用の電子メールアドレス。</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>読み込みジョブを実行するレポートスイート ID。 </td>
  </tr>
  <tr>
   <td>dataset</td>
   <td>読み込みジョブを実行するデータセット関連 ID。 </td>
  </tr>
  <tr>
   <td>description</td>
   <td>ジョブの説明。<br /> </td>
  </tr>
  <tr>
   <td>overwrite</td>
   <td>データの競合を上書きするためのフラグ。デフォルトは <strong>false</strong> です。</td>
  </tr>
  <tr>
   <td>checkdivisions</td>
   <td>レポートスイートの互換性をチェックするためのフラグ。デフォルトは <strong>true</strong> です。</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>処理したノードを書き出し後に削除するためのフラグ。デフォルトは <strong>false</strong> です。</td>
  </tr>
 </tbody>
</table>

## Adobe Classifications による書き出しの自動化 {#automating-adobe-classifications-export}

独自のワークフローを作成することで、新しい読み込みのたびにそのワークフローが開始され、構造の正しい適切なデータが **/var/export/** に作成されて Adobe Classifications に書き出すことができるようになります。
