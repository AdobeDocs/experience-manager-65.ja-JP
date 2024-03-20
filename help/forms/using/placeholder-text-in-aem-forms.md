---
title: AEM Forms のプレースホルダーテキスト
description: プレースホルダーテキストは、コントロールに値がない場合に、ユーザーのデータ入力を支援するためのものです。これはサンプルの値にすることも、使用する形式に関する簡単な説明にすることもできます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---

# AEM Forms のプレースホルダーテキスト {#placeholder-text-in-aem-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

プレースホルダーテキストは単語または短い文章を表示します。これは、コントロールに値がない場合に、ユーザーのデータ入力を支援するためのものです。プレースホルダーテキストはサンプルの値にすることも、使用する形式に関する簡単な説明にすることもできます。プレースホルダーテキストはユーザーが値を入力する前に表示され、ユーザーが値を入力または選択すると削除されます。

>[!NOTE]
>
>プレースホルダーテキストを指定する場合、改行文字を含まない値にする必要があります。

![プレースホルダーテキストを伴う／伴わない日付コンポーネント](assets/dat-picker-place-holder-text.png)

**A.** プレースホルダーテキストを伴う日付コンポーネント **B.** プレースホルダーテキストを伴わない日付コンポーネント

AEM Forms では、パスワードボックス、日付選択、数値ボックス、テキストボックスフィールドでプレースホルダーテキストを使用できます。\
プレースホルダーテキストはネイティブの HTML5 日付ウィジェットには対応していません。プレースホルダーテキストを指定するには、以下のようにします。

1. プレースホルダーテキストをサポートするコンポーネントを右クリックして、「**編集**」をクリックします。コンポーネントを編集ダイアログボックスが表示されます。

1. 「**タイトルとテキスト**」タブを開きます。
1. **プレースホルダーテキストボックス**&#x200B;に単語または短い語句を指定します。「**OK**」をクリックします。

>[!NOTE]
>
>プレースホルダーテキストは Microsoft Internet Explorer 9 ではサポートされていません。
