---
title: フォームのフィールドのための文脈依存ヘルプの作成
description: AEM Forms では、文脈依存ヘルプをテキストまたはビデオなどのリッチメディアの形でアダプティブフォームフィールドやパネルに追加することができます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 95%
---
# フォームのフィールドのための文脈依存ヘルプの作成{#authoring-in-context-help-for-form-fields}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。 これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。 この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

## はじめに {#introduction}

エンドユーザーがフォームに記入しているときに、特定のフォームフィールドへの記入方法がわからない場合があります。 そのような問題を解決するために、アダプティブフォームでは、テキストのまたは高度な文脈依存ヘルプをフォームフィールドに追加できるようにしています。 これにより、フォーム入力エクスペリエンスを向上し、エンドユーザーにとっての曖昧さを回避することができます。

この記事では、フォーム作成者がアダプティブフォームの作成中に文脈依存ヘルプを追加する方法を説明します。

## 文脈依存ヘルプを追加 {#add-in-context-help}

文脈依存ヘルプは、サイドバーにある「プロパティ」タブの「ヘルプコンテンツ」セクションで、以下のオプションを利用して指定できます。

* [簡単な説明](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [詳細な説明](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![フォームのフィールドのための文脈依存ヘルプ](assets/descriptions.png)

>[!NOTE]
>
>詳細な説明は簡単な説明をオーバーライドします。 両方を指定した場合は、詳細な説明のみが表示されます。

### 簡単な説明 {#short-description}

簡単な説明フィールドは、フォームフィールドの記入に関する短く簡単なヒントを提供するためにあります。 「簡単な説明」フィールド内で指定されたテキストは、フィールドの上にカーソルを移動させると、ツールチップとして表示されます。

![フォームフィールドへの文脈依存ヘルプの追加の簡単な説明](assets/tooltip.png)

>[!NOTE]
>
>ヘルプテキストを常にフィールドの下に表示するには、「**簡単な説明を常に表示する**」を選択します。

![フィールドの下に永久的に表示される簡単な文脈依存ヘルプ](assets/short1.png)

### 詳細な説明 {#long-description}

「詳細な説明」フィールドを使って、文脈依存ヘルプに長いテキストを指定したり、ビデオなどのリッチメディアコンテンツを埋め込んだりすることができます。 例えば、次の画像では文脈依存ヘルプとしてビデオを埋め込む方法を示しています。

![フォームフィールドのための文脈依存ヘルプとしてのリッチメディアの追加](assets/long-descriptions.png)

長い説明を追加すると、**?**&#x200B;が表示されます フィールドの横にあるアイコン。 アイコンをクリックすると、「詳細な説明」セクションに追加されたコンテンツが表示されます。

![リッチメディアを使用した文脈依存ヘルプの例](assets/photoshop.png)

### パネルレベルのヘルプ {#panel-level-help}

フォームフィールドの文脈依存ヘルプに加え、パネル編集ダイアログの「ヘルプコンテンツ」タブから、パネルレベルでヘルプを指定することができます。

![フォームパネルへの文脈依存ヘルプの追加](assets/panel-level-help.png)

パネルにヘルプを追加すると、**?**&#x200B;が表示されます パネルの説明の横にあるアイコン。 アイコンをクリックすると、パネル編集ダイアログの「ヘルプコンテンツ」セクションに追加されたコンテンツが表示されます。

![フォームパネルレベルでの文脈依存ヘルプの例](assets/photoshop-1.png)
