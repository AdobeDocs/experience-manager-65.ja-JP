---
title: AEM Forms のプレースホルダーテキスト
description: プレースホルダーテキストは、コントロールに値がない場合にユーザーがデータ入力を容易にするためのものです。 値の例や、期待される形式の簡単な説明を指定できます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: 6dbec0f41396c2b41d5324c4ecf6f1f33b1d0780
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 69%

---

# AEM Forms のプレースホルダーテキスト {#placeholder-text-in-aem-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

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
