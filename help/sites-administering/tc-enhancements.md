---
title: 翻訳の機能強化
seo-title: Translation Enhancements
description: AEM の翻訳の機能強化です。
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 1be3d394283493f7c282ea4c3d794458d88e1ac3
workflow-type: ht
source-wordcount: '681'
ht-degree: 100%

---

# 翻訳の機能強化{#translation-enhancements}

ここでは、AEM 翻訳管理機能に対する増分的機能強化と調整について説明します。

## 翻訳プロジェクトの自動化 {#translation-project-automation}

翻訳開始の自動促進や削除、翻訳プロジェクトの反復実行のスケジュール化など、翻訳プロジェクトの生産性を向上させるためのオプションが追加されました。

1. 翻訳プロジェクトで、「**翻訳の概要**」タイルの下部にある省略記号をクリックまたはタップします。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 「**詳細**」タブに切り替えます。下部で、「**翻訳開始を自動的に促進**」を選択します。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. オプションで、翻訳済みコンテンツを受信後、翻訳開始を自動的に促したり削除したりすることを選択できます。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 翻訳プロジェクトの反復実行を選択するには、「**翻訳を繰り返す**」の下のドロップダウンで頻度を選択します。プロジェクトの反復実行は、指定した間隔で翻訳ジョブを自動的に作成および実行します。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多言語翻訳プロジェクト {#multilingual-translation-projects}

翻訳プロジェクトで複数のターゲット言語を設定して、作成される翻訳プロジェクトの総数を減らすことができます。

1. 翻訳プロジェクトで、「**翻訳の概要**」タイルの下部にある省略記号をクリックまたはタップします。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 「**詳細**」タブに切り替えます。**ターゲット言語**&#x200B;に複数の言語を追加できます。

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. または、Sites の参照レールで翻訳を開始している場合、言語を追加して、「**多言語翻訳プロジェクトを作成**」を選択します。

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. すべてのターゲット言語について、プロジェクトの翻訳ジョブが作成されます。プロジェクト内で 1 つずつ開始することも、プロジェクト管理でプロジェクトをグローバルに実行することで一度にすべてを開始することもできます。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻訳メモリの更新 {#translation-memory-updates}

翻訳済みコンテンツを手動で編集すると、翻訳管理システム（TMS）に同期し直され、翻訳メモリに反映されます。

1. Sites コンソールから、翻訳済みページのテキストコンテンツを更新した後、「**翻訳メモリを更新**」を選択します。

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. リストビューでは、編集されたすべてのテキストコンポーネントについて、ソースと翻訳が横に並んで比較表示されます。翻訳メモリに同期する必要がある翻訳の更新を選択して、「**メモリを更新**」を選択します。

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM は、設定済みの TMS の翻訳メモリ内の既存の文字列の翻訳を更新します。

* このアクションは、設定済みの TMS の翻訳メモリ内の既存の文字列の翻訳を更新します。
* 新しい翻訳ジョブは作成されません。
* AEM 翻訳 API を介して、翻訳を TMS に返します（以下を参照）。

この機能を使用するには：

* AEM で使用するように TMS を設定する必要があります。
* コネクターはメソッド [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html) を実装する必要があります。
   * このメソッド内のコードは、翻訳メモリの更新リクエストの処理を決定します。
   * AEM 翻訳フレームワークは、このメソッドの実装を通じて、文字列の値のペア（元の翻訳と更新された翻訳）を TMS に返します。

独自の翻訳メモリを使用している場合、翻訳メモリの更新をインターセプトして、独自の宛先に送信できます。

## 複数のレベルの言語コピー {#language-copies-on-multiple-levels}

言語ルートは、言語コピーのルートを認識できる状態で、ノード（地域など）の下にグループ化できるようになりました。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>1 レベルのみ許可されます。例えば、次の場合、「es」ページを言語コピーとして解釈できません。
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>この `es` 言語コピーは、`en` ノードから 2 レベル離れている（americas/central-america）ので、検出されません。

>[!NOTE]
>
>言語ルートは、言語の ISO コードだけでなく、任意のページ名を持つことができます。AEM は常に最初にパスと名前を確認しますが、ページ名で言語が識別されない場合は、ページの cq:language プロパティを確認して言語を識別します。

## 翻訳ステータスのレポート {#translation-status-reporting}

ページが翻訳済みである、翻訳中である、またはまだ翻訳されていないことを示すプロパティが、Sites のリストビューで選択できるようになりました。プロパティを表示するには：

1. Sites で、**リストビュー**&#x200B;に切り替えます。

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. **設定を表示**&#x200B;をクリックまたはタップします。

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 「**翻訳**」の下の「**翻訳済み**」チェックボックスをオンにして、「**更新**」をタップまたはクリックします。

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

**翻訳済み**&#x200B;列にページの翻訳ステータスが表示されているのを確認できます。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
