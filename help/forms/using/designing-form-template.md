---
title: HTML5 フォーム用のフォームテンプレートのデザイン
seo-title: Designing form templates for HTML5 forms
description: AEM Forms は、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは Designer を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '485'
ht-degree: 100%

---

# HTML5 フォーム用のフォームテンプレートのデザイン{#designing-form-templates-for-html-forms}

AEM の HTML5 フォームコンポーネントは、HTML5 形式への XFA フォームテンプレートのレンダリングを提供します。フォームデザイナーは [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を使用してフォームテンプレートをデザインし、HTML5 レンダリングの機能を使用することができます。これらのフォームテンプレートはアセットとともに、AEM リポジトリやファイルシステムに配置するか、http で公開することができます。ただし、Forms Manager を使用してフォームを管理する場合には、テンプレートとアセットを AEM リポジトリに置く必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。たとえば、Adobe Reader でバーコードが PDF フォームに適用される方法が Mobile フォームとは異なったり、フォームにデジタル署名を行う方法も各形式で異なります。そのような違いについて詳しくは、[HTML5 フォームと PDF フォームの機能の違い](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)を参照してください。

一般的な XFA 機能の場合、両方の形式で機能するフォームをデザインするために、次のベストプラクティスとガイドラインを参照してください。

## ベストプラクティス {#best-practices}

スキーマバインディングやフォームロジックの記述などの、フォームテンプレートのデザインに関わるほとんどの手順は同じです。ただし、Adobe Reader とブラウザーベースの形式のようなシッククライアントのレンダリングとスクリプティングエンジンに本質的な違いがあるため、いくつかの推奨事項が「[ベストプラクティス](/help/forms/using/design-accessible-html5-forms.md)」の記事に記載されています。これらのベストプラクティスに従うと、両方の形式で期待通りに機能するようにフォームテンプレートをデザインすることができます。

### AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML のブレビュー {#preview-html}

フォームデザイナーのデザインモードに、HTML5 形式でフォームをプレビューするための「Preview HTML」タブが追加されました。AEM Forms Designer でこの機能を有効化して設定する方法について詳しくは、「[HTML のプレビュー](../../forms/using/preview-xdp-forms-html.md)」を参照してください。

#### 手書き署名 {#scribble-signature}

HTML5 フォームの主な対象はタッチデバイスです。そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。手書き署名のコントロールは、クリックしてフォームテンプレートにドラッグ＆ドロップすると設定できます。HTML5 レンディションでは手書きフィールドとしてレンダリングされるため、タッチデバイスで署名を手書きするのに使用できます。デスクトップ機器では、手書きフィールドとしてマウスのコントロールで使用できます。この機能の使用方法について詳しくは、[XFA 手書きフィールド](../../forms/using/scribble-signature.md)を参照してください。

![4](assets/4.png)

#### リッチテキスト形式 {#rich-text-format}

テキストフィールドをリッチテキストフィールドに変換できます。 テキストフィールドに書式設定オプションのリストを追加します。 変換するには、Forms Designer を開き、 **[!UICONTROL デザインビュー]**&#x200B;のテキストフィールドをタップします。「**[!UICONTROL フィールド]**」タブで、**[!UICONTROL フィールドの形式]**&#x200B;ドロップダウンリストから「**[!UICONTROL リッチテキスト]**」を選択します。これで、XFA フォームが HTML5 フォームとしてレンダリングされると、そのフィールドはリッチテキストフィールドとしてレンダリングされます。「![最大化](assets/maximize_icon.svg)」をタップして、その他の書式設定オプションを表示します。
