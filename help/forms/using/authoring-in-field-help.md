---
title: フォームのフィールドのための文脈依存ヘルプの作成
description: AEM Formsを使用すると、アダプティブフォームのフィールドやパネルに文脈依存ヘルプを、テキストまたはビデオなどのリッチメディアとして追加できます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 90%

---

# フォームのフィールドのための文脈依存ヘルプの作成{#authoring-in-context-help-for-form-fields}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

## はじめに {#introduction}

エンドユーザーがフォームに記入しているときに、特定のフォームフィールドへの記入方法がわからない場合があります。このような問題に対処するため、アダプティブフォームでは、テキストの追加や、豊富な文脈依存ヘルプをフォームフィールドに追加する機能を提供しています。 これにより、フォーム入力エクスペリエンスを向上し、エンドユーザーにとっての曖昧さを回避することができます。

この記事では、アダプティブフォームのオーサリング中に文脈依存ヘルプを追加する方法について説明します。

## コンテキストヘルプの追加 {#add-in-context-help}

文脈依存ヘルプは、サイドバーにある「プロパティ」タブの「ヘルプコンテンツ」セクションで次のオプションを使用して指定できます。

* [簡単な説明](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [詳細な説明](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![フォームのフィールドのための文脈依存ヘルプ](assets/descriptions.png)

>[!NOTE]
>
>詳細な説明は簡単な説明をオーバーライドします。両方を指定した場合は、詳細な説明のみが表示されます。

### 簡単な説明 {#short-description}

簡単な説明フィールドは、フォームフィールドの記入に関する短く簡単なヒントを提供するためにあります。簡単な説明内で指定されたテキストは、フィールドの上にカーソルを移動させると、ツールヒントとして表示されます。

![フォームフィールドへの文脈依存ヘルプの追加の簡単な説明](assets/tooltip.png)

>[!NOTE]
>
>ヘルプテキストを常にフィールドの下に表示するには、「**簡単な説明を常に表示する**」を選択します。

![フィールドの下に永久的に表示される簡単な文脈依存ヘルプ](assets/short1.png)

### 詳細な説明 {#long-description}

「詳細な説明」フィールドを使って、文脈依存ヘルプに長いテキストを指定したり、ビデオなどのリッチメディアコンテンツを埋め込んだりすることができます。例えば、次の画像では文脈依存ヘルプとしてビデオを埋め込む方法を示しています。

![フォームフィールドのための文脈依存ヘルプとしてのリッチメディアの追加](assets/long-descriptions.png)

詳細な説明を追加すると、**が表示されますか？** アイコンがフィールドの隣に表示されます。アイコンをクリックすると、詳細な説明セクションに追加されたコンテンツが表示されます。

![リッチメディアを使用した文脈依存ヘルプの例](assets/photoshop.png)

### パネルレベルのヘルプ {#panel-level-help}

フォームフィールドの文脈依存ヘルプに加え、パネル編集ダイアログの「ヘルプコンテンツ」タブから、パネルレベルでヘルプを指定することができます。

![フォームパネルへの文脈依存ヘルプの追加](assets/panel-level-help.png)

パネルにヘルプを追加すると、**が表示されますか？** アイコンがパネルの説明の隣に表示されます。このアイコンをクリックすると、パネル編集ダイアログの「ヘルプコンテンツ」セクションに、追加されたコンテンツが表示されます。

![フォームパネルレベルでの文脈依存ヘルプの例](assets/photoshop-1.png)
