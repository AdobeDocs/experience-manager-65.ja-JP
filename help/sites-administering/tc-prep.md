---
title: 翻訳するコンテンツの準備
description: Adobe Experience Managerで翻訳するコンテンツを準備する方法を説明します。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 69%

---

# 翻訳するコンテンツの準備{#preparing-content-for-translation}

通常、多言語の web サイトでは、ある程度の量のコンテンツを複数の言語で提供します。サイトは 1 つの言語で作成されてから、他の言語に翻訳されます。一般に、多言語サイトはページの分岐で構成され、各分岐には異なる言語のサイトのページが含まれます。

サンプルのGeometrixxデモサイトには、複数の言語ブランチが含まれ、次の構造を使用します。

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

サイトの各言語分岐は、言語コピーと呼ばれます。言語コピーのルートフォルダー（言語ルート）が、言語コピー内のコンテンツの言語を識別します。例えば、`/content/geometrixx/fr` は、フランス語の言語コピー用の言語ルートです。言語コピーでは [正しく設定された言語ルート](/help/sites-administering/tc-prep.md#creating-a-language-root) したがって、ソースサイトの翻訳の実行時に正しい言語がターゲットになります。

サイトのコンテンツを最初にオーサリングするための言語コピーが言語マスターです。言語マスターは、他の言語に翻訳されるソースです。

翻訳するサイトを準備するには、次の手順を使用します。

1. 言語マスターの言語ルートを作成します。例えば、英語の Geometrixx Demo Site の言語ルートは /content/geometrixx/en です。[言語ルートの作成](/help/sites-administering/tc-prep.md#creating-a-language-root)に記載の情報に従って言語ルートが正しく設定されていることを確認してください。
1. 言語マスターのコンテンツをオーサリングします。
1. サイトの各言語コピーの言語ルートを作成します。例えば、Geometrixxサンプルサイトのフランス語の言語コピーは/content/geometrixx/fr です。

翻訳するコンテンツの準備が完了したら、言語コピーおよび関連する翻訳プロジェクトの不足ページを自動的に作成できます（[翻訳プロジェクトの作成](/help/sites-administering/tc-manage.md)を参照）。AEM のコンテンツ翻訳プロセスの概要については、[多言語サイトのコンテンツの翻訳](/help/sites-administering/translation.md)を参照してください。

## 言語ルートの作成 {#creating-a-language-root}

コンテンツの言語を識別する言語コピーのルートページとして言語ルートを作成します。言語ルートを作成したら、その言語コピーを含む翻訳プロジェクトを作成できます。

言語ルートを作成するには、ページを作成し、「名前」プロパティの値として ISO 言語コードを使用します。言語コードは次のどちらかの形式にしてください。

* `<language-code>`サポートされている言語コードは、ISO-639-1 で定義されている 2 文字のコードです。例： `en`.

* `<language-code>_<country-code>` または `<language-code>-<country-code>`サポートされている国コードは、ISO 3166 で定義されている小文字または大文字の 2 文字コードです。例： `en_US`, `en_us`, `en_GB`, `en-gb`.

グローバルサイト用に選択した構造に従って、どちらかの形式を使用できます。例えば、Geometrixx サイトのフランス語の言語コピーのルートページの「名前」プロパティは `fr` になります。Name プロパティは、リポジトリ内のページノードの名前として使用されるので、ページのパスを決定します。 (http://localhost:4502/content/geometrixx/fr.html)

次の手順では、タッチ操作向け UI を使用して、Web サイトの言語コピーを作成します。 クラシック UI の使用手順については、 [クラシック UI を使用した言語ルートの作成](/help/sites-administering/tc-lroot-classic.md).

1. Sites に移動します。
1. 言語コピーを作成するサイトをクリックまたはタップします。

   例えば、Geometrixx Outdoorsサイトの言語コピーを作成するには、「Geometrixx Outdoorsサイト」をクリックまたはタップします。

1. 「作成」をクリックまたはタップして、「ページを作成」をクリックまたはタップします。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. ページテンプレートを選択して、「次へ」をクリックまたはタップします。
1. 「名前」フィールドに、の形式で国コードを入力します。 `<language-code>` または `<language-code>_<country-code>`例： `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. ページのタイトルを入力します。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 「作成」をクリックまたはタップします。確認のダイアログボックスで、「**完了**」をクリックまたはタップして Sites コンソールに戻ります。または「**開く**」をクリックまたはタップして言語コピーを開きます。

## 言語ルートのステータスの確認 {#seeing-the-status-of-language-roots}

タッチ操作向け UI には参照パネルがあり、作成された言語ルートのリストが表示されます。

![chlimage_1-23](assets/chlimage_1-23a.png)

次の手順では、タッチ操作向け UI を使用してページの参照パネルを開きます。

1. サイトコンソールで、サイトのページを選択し、「**参照**」をクリックまたはタップします。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. 参照パネルで、「**言語コピー**」をクリックまたはタップします。Web サイトの言語コピーが言語コピーパネルに表示されます。
