---
title: HTML5 フォーム用のフォームテンプレートのデザイン
seo-title: HTML5 フォーム用のフォームテンプレートのデザイン
description: AEM Forms は、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは Designer を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。
seo-description: AEM Forms は、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは Designer を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 58%

---


# HTML5 フォーム用のフォームテンプレートのデザイン{#designing-form-templates-for-html-forms}

AEM の HTML5 フォームコンポーネントは、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。これらのフォームテンプレートはアセットとともに、AEM リポジトリやファイルシステムに配置するか、http で公開することができます。ただし、Formsマネージャーを使用してフォームを管理する場合は、テンプレートとアセットをAEMリポジトリに置く必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。例えば、Adobe ReaderのPDFフォームにバーコードが適用される方法は、Mobileフォームとは異なります。また、フォームの電子署名の方法も、形式によって異なります。 そのような違いについて詳しくは、[HTML5フォームとPDF formsの機能の違い](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)を参照してください。

一般的な XFA 機能の場合、両方の形式で機能するフォームをデザインするために、次のベストプラクティスとガイドラインを参照してください。

## ベストプラクティス {#best-practices}

スキーマバインディングやフォームロジックの記述などの、フォームテンプレートのデザインに関わるほとんどの手順は同じです。ただし、Adobe Reader とブラウザーベースの形式のようなシッククライアントのレンダリングとスクリプティングエンジンに本質的な違いがあるため、いくつかの推奨事項が「[ベストプラクティス](/help/forms/using/design-accessible-html5-forms.md)」の記事に記載されています。これらのベストプラクティスは、両方の形式で期待どおりに機能するようにフォームテンプレートをデザインする際に役立ちます。

### AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML のブレビュー {#preview-html}

フォームデザイナーのデザインモードに、HTML5 形式でフォームをプレビューするための「Preview HTML」タブが追加されました。AEM Forms Designer でこの機能を有効化して設定する方法について詳しくは、「[HTML のプレビュー](../../forms/using/preview-xdp-forms-html.md)」を参照してください。

#### 手書きの署名 {#scribble-signature}

HTML5 フォームの主な対象はタッチデバイスです。そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。手書き署名コントロールをクリックまたはドラッグ&amp;ドロップして、フォームテンプレートに設定できます。 HTML5レンダリングでは手書きフィールドとしてレンダリングされ、タッチデバイスで手書き署名を行うのに使用できます。 デスクトップマシンでは、それはマウスコントロールの使用により手書きフィールドとして使用できます。この機能の使用方法について詳しくは、[XFA手書きフィールド](../../forms/using/scribble-signature.md)を参照してください。

![4](assets/4.png)

#### リッチテキスト形式{#rich-text-format}

テキストフィールドは、リッチテキストフィールドに変換できます。 書式設定オプションのリストがテキストフィールドに追加されます。 変換するには、Formsデザイナーを開き、**[!UICONTROL デザイン表示]**&#x200B;のテキストフィールドをタップします。 「**[!UICONTROL フィールド]**」タブで、「**[!UICONTROL フィールド形式]**」ドロップダウンリストから「**[!UICONTROL リッチテキスト]**」を選択します。 現在は、XFAフォームがHTML5フォームとしてレンダリングされるとき、フィールドはリッチテキストフィールドとしてレンダリングされます。 「![最大化](assets/maximize_icon.svg)」をタップして、追加の書式設定オプションを表示します。
