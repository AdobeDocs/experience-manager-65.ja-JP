---
title: 国際化対応オプションの設定
description: フォームのレンダリングに使用するロケールを指定する方法、および出力ストリームのエンコードに使用する文字セットを指定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 32%

---

# 国際化対応オプションの設定{#setting-internationalization-options}

## フォームのレンダリングに使用するロケールを指定します {#specify-the-locale-used-to-render-forms}

ロケールフォームのレンダリング時に使用するロケールをPDFできます。 PDFフォーム上のフィールドは、指定されたロケールを使用してデータを表示します。 例えば、ロケールがドイツ語に設定されている場合、フォームでは数値にドイツ語の小数点区切り文字が使用されます。 また、ロケールは、Web ブラウザーなどのクライアントデバイスに検証メッセージを、HTML変換の一部として送信する場合にも使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「国際化対応」の「言語」リストで、フォームのレンダリングに使用するロケールを選択します。 デフォルト値は英語（米国）です。
1. 「保存」をクリックします。

## 出力ストリームのエンコードに使用する文字セットを指定します {#specify-the-character-set-used-to-encode-the-output-stream}

1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、renderHTMLForm または renderPDFForm のどちらかで、使用される API によって異なります。 リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   HTML の変換について AEM Forms で使用できるエンコーディング値は、`java.nio.charset` パッケージで定義されています。sFormPreference が PDFForm の場合は、特定の文字セットのみがサポートされます。文字セットは、有効な正規名である必要があります。 デフォルト値は ISO-8859-1 です。

1. 「保存」をクリックします。
