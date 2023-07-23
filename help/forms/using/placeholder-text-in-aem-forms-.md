---
title: AEM Forms のプレースホルダーテキスト
seo-title: Placeholder text in AEM Forms
description: プレースホルダーテキストは、コントロールに値がない場合にユーザーがデータ入力を容易にするためのものです。 値の例や、期待される形式の簡単な説明を指定できます。
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 51%

---

# AEM Forms のプレースホルダーテキスト {#placeholder-text-in-aem-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

プレースホルダーテキストは、単語または短いフレーズを表します。 これは、コントロールに値がない場合に、ユーザーのデータ入力を支援するためのものです。 プレースホルダーテキストには、サンプル値や、必要な形式の簡単な説明を指定できます。 プレースホルダーテキストはユーザーが値を入力する前に表示され、ユーザーが値を入力または選択すると削除されます。

>[!NOTE]
>
>プレースホルダーテキストを指定する場合、改行文字を含まない値にする必要があります。

![プレースホルダーテキストを伴う／伴わない日付コンポーネント](assets/dat-picker-place-holder-text.png)

**A.** プレースホルダーテキストを伴う日付コンポーネント **B.** プレースホルダーテキストを伴わない日付コンポーネント

AEM Forms では、パスワードボックス、日付選択、数値ボックス、テキストボックスフィールドでプレースホルダーテキストを使用できます。\
プレースホルダーテキストはネイティブの HTML5 日付ウィジェットには対応していません。プレースホルダーテキストを指定するには、以下のようにします。

1. プレースホルダーテキストをサポートするコンポーネントを右クリックし、 **編集**. コンポーネントを編集ダイアログボックスが表示されます。

1. 「**タイトルとテキスト**」タブを開きます。
1. **プレースホルダーテキストボックス**&#x200B;に単語または短い語句を指定します。「**OK**」をクリックします。

>[!NOTE]
>
>プレースホルダーテキストは Microsoft Internet Explorer 9 ではサポートされていません。
