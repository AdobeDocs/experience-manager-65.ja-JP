---
title: 翻訳機能の強化
description: AEM翻訳管理機能の段階的な機能強化と絞り込み。
topic-tags: site-features
content-type: reference
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 73%

---

# 翻訳の機能強化{#translation-enhancements}

このページでは、AEM翻訳管理機能の段階的な機能強化と絞り込みについて説明します。

## 翻訳プロジェクトの自動化 {#translation-project-automation}

翻訳開始の自動促進や削除、翻訳プロジェクトの反復実行のスケジュール化など、翻訳プロジェクトの生産性を向上させるためのオプションが追加されました。

1. 翻訳プロジェクトで、 **翻訳の概要** タイル。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 「**詳細**」タブに切り替えます。下部で、「**翻訳開始を自動的に促進**」を選択します。

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. オプションで、翻訳済みコンテンツを受信後、翻訳開始を自動的に促したり削除したりすることを選択できます。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 翻訳プロジェクトの反復実行を選択するには、「**翻訳を繰り返す**」の下のドロップダウンで頻度を選択します。プロジェクトの反復実行は、指定した間隔で翻訳ジョブを自動的に作成および実行します。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多言語翻訳プロジェクト {#multilingual-translation-projects}

翻訳プロジェクトで複数のターゲット言語を設定して、作成される翻訳プロジェクトの総数を減らすことができます。

1. 翻訳プロジェクトで、 **翻訳の概要** タイル。

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

1. リスト表示では、編集されたすべてのテキストコンポーネントについて、ソースと翻訳が横に並んで比較表示されます。翻訳メモリに同期する必要がある翻訳の更新を選択して、「**メモリを更新**」を選択します。

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

言語ルートは、ノード（例えば、地域）の下にグループ化できるようになりましたが、言語コピーのルートとして認識されます。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>1 レベルのみ許可されます。例えば、次の場合は、「es」ページで言語コピーを解決できません。
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>この `es` 言語コピーは、`en` ノードから 2 レベル離れている（americas/central-america）ので、検出されません。

>[!NOTE]
>
>言語ルートには、言語の ISO コードだけでなく、任意のページ名を含めることができます。 AEMは常に最初にパスと名前を確認しますが、ページ名が言語を識別しない場合は、AEMはページの cq:language プロパティで言語識別を確認します。

## 翻訳ステータスのレポート {#translation-status-reporting}

ページが翻訳済みか、翻訳中か、またはまだ翻訳されていないかを示すプロパティをサイトリスト表示で選択できるようになりました。 プロパティを表示するには：

1. Sites で、**リスト表示**&#x200B;に切り替えます。

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. クリック **設定を表示**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. チェック **翻訳済み** 下のチェックボックス **翻訳** をクリックします。 **更新**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

**翻訳済み**&#x200B;列にページの翻訳ステータスが表示されているのを確認できます。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
