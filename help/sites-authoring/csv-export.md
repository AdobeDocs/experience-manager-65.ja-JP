---
title: CSV ファイルへの書き出し
description: ページの情報をローカルシステムの CSV ファイルに書き出す
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 81%

---

# CSV ファイルへの書き出し {#export-to-csv}

**CSV レポートの作成**&#x200B;では、ページの情報をローカルシステムの CSV ファイルに書き出すことができます。

* ダウンロードしたファイルの名前は `export.csv` になります。
* コンテンツは、選択するプロパティによって異なります。
* 書き出しのパスと深さを定義できます。

>[!NOTE]
>
>ブラウザーのダウンロード機能（およびデフォルトのダウンロード先）が使用されます。

**CSV 書き出しを作成**&#x200B;ウィザードでは、以下を選択できます。

* 書き出すプロパティ
   * メタデータ
      * 名前
      * 変更
      * 公開済み
      * テンプレート
      * ワークフロー
   * 翻訳
      * 翻訳済み
   * 分析
      * ページ表示
      * ユニーク訪問者
      * ページ滞在時間
* 深さ
   * 親パス
   * 直属の子要素のみ
   * 追加の子のレベル
   * レベル

生成された `export.csv` ファイルは、Excel（または互換性のあるその他のアプリケーション）で開くことができます。

![etc-01](assets/etc-01.png)

作成 **CSV レポート** オプションは、 **Sites** コンソール（リスト表示）：これは、 **作成** ドロップダウンメニュー：

![etc-02](assets/etc-02.png)

CSV の書き出しファイルを作成するには、次の手順を実行します。

1. を開きます。 **Sites** コンソールで、必要に応じて必要な場所に移動します。
1. ツールバーの「**作成**」をクリックし、「**CSV レポート**」を選択してウィザードを開きます。

   ![etc-03](assets/etc-03.png)

1. 書き出す必要のあるプロパティを選択します。
1. 「**作成**」を選択します。
