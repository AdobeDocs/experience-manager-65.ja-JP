---
title: CSV ファイルへの書き出し
seo-title: Export to CSV
description: ページの情報をローカルシステムの CSV ファイルに書き出します
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 100%

---

# CSV ファイルへの書き出し {#export-to-csv}

**CSV レポートの作成**&#x200B;では、ページの情報をローカルシステムの CSV ファイルに書き出すことができます。

* ダウンロードしたファイルの名前は `export.csv` になります。
* コンテンツは、選択するプロパティによって異なります。
* 書き出しのパスと深さを定義できます。

>[!NOTE]
>
>ブラウザーのダウンロード機能（およびデフォルトのダウンロード先）が使用されます。

**CSV の書き出しファイルを作成**&#x200B;ウィザードでは、次の要素を選択できます。

* 書き出すプロパティ
   * メタデータ
      * 名前
      * 変更済み
      * 公開済み
      * テンプレート
      * ワークフロー
   * 翻訳
      * 翻訳済み
   * 分析
      * ページ表示
      * 個別訪問者数
      * ページ滞在時間
* 深さ
   * 親パス
   * 直属の子要素のみ
   * 追加の子のレベル
   * レベル

生成された `export.csv` ファイルは、Excel（または互換性のあるその他のアプリケーション）で開くことができます。

![etc-01](assets/etc-01.png)

「**CSV レポート**&#x200B;の作成」オプションは、**Sites** コンソールをリストビューで参照するときに使用できる、**作成**&#x200B;ドロップダウンメニューのオプションです。

![etc-02](assets/etc-02.png)

CSV の書き出しファイルを作成するには、次の手順を実行します。

1. **サイト**&#x200B;コンソールを開き、必要に応じて必要な場所まで移動します。
1. ツールバーの「**作成**」をクリックし、「**CSV レポート**」を選択してウィザードを開きます。

   ![etc-03](assets/etc-03.png)

1. 書き出す必要があるプロパティを選択します。
1. 「**作成**」を選択します。
