---
title: 検索
description: AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 50%

---

# 検索 {#searching}

AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。

>[!NOTE]
>
>オーサー環境の外部では、検索用のメカニズム ( [Query Builder](/help/sites-developing/querybuilder-api.md) および [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## 検索の基本 {#search-basics}

検索パネルにアクセスするには、該当するコンソールの左側のパネルの上部にある「**検索**」タブをクリックします。

![chlimage_1-101](assets/chlimage_1-101.png)

検索パネルを使用すると、すべての web サイトページにわたって検索できます。次のフィールドとウィジェットが含まれます。

* **Fulltext**:指定したテキストを検索
* **前後に変更**:特定の日付の間に変更されたページのみを検索します
* **テンプレート**:指定したテンプレートに基づくページのみを検索
* **タグ**:指定したタグを持つページのみを検索

>[!NOTE]
>
>インスタンスが [Lucene 検索](/help/sites-deploying/queries-and-indexing.md)用に設定されていると、次を&#x200B;**フルテキスト**&#x200B;で使用できます。
>
>* [ワイルドカード](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [ブール演算子](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [正規表現](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [フィールドグループ](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [ブースト](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>


「 **検索** をクリックします。 クリック **リセット** をクリックして、検索条件をクリアします。

## フィルター {#filter}

様々な場所でフィルターを設定（およびクリア）して、表示をドリルダウンして絞り込むことができます。

![chlimage_1-102](assets/chlimage_1-102.png)

## 検索と置換 {#find-and-replace}

内 **Web サイト** コンソールを **検索と置換** メニューオプションを使用すると、web サイトの特定のセクション内で、1 つの文字列を複数インスタンスで検索および置換できます。

1. 検索および置換アクションを実行するルートページまたはフォルダーを選択します。
1. 選択 **ツール** その後 **検索と置換**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. この **検索と置換** ダイアログでは次の操作を実行します。

   * 検索アクションを開始するルートパスを確認します。
   * 見つかる用語を定義します
   * 置き換える用語を定義します。
   * 検索で大文字と小文字を区別する必要があるかどうかを示します
   * 単語全体のみを検出するかどうかを示します（それ以外の場合は、部分文字列も検索されます）。

   「**プレビュー**」リストをクリックすると、語句が見つかった場所が表示されます。特定のインスタンスを選択／選択解除して置換できます。

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. クリック **置換** すべてのインスタンスを実際に置き換える この操作の確認が求められます。

検索と置換のサーブレットのデフォルトスコープには、次のプロパティが含まれています。

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

このスコープは、Apache Felix Web Management Console（例：`https://localhost:4502/system/console/configMgr`）を使用して変更できます。`CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` を選択し、必要に応じてスコープを設定します。

>[!NOTE]
>
>標準のAEMインストールでは、検索と置換は Lucene を検索機能に使用します。
>
>Lucene は最大 16 k の文字列プロパティのインデックスを作成します。 これを超える文字列は検索されません。
