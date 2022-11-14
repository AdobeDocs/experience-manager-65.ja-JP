---
title: AEM Forms のプレースホルダーテキスト
seo-title: Placeholder text in AEM Forms
description: プレースホルダーテキストは、コントロールに値がない場合に、ユーザーのデータ入力を支援するためのものです。これはサンプルの値にすることも、使用する形式に関する簡単な説明にすることもできます。
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 100%

---

# AEM Forms のプレースホルダーテキスト {#placeholder-text-in-aem-forms}

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
