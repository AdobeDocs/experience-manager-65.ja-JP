---
title: HTML5 フォーム用のフォームテンプレートのデザイン
description: AEM Formsは XFA フォームテンプレートをHTML5 形式にレンダリングできます。 フォームデザイナーは、Designer を使用してフォームテンプレートをデザインし、HTML5 のレンディション機能を使用できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 53%

---

# HTML5 フォーム用のフォームテンプレートのデザイン{#designing-form-templates-for-html-forms}

AEMのHTML5 フォームコンポーネントは、XFA フォームテンプレートをHTML5 形式にレンダリングできます。 フォームデザイナーは、 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) とは、HTML5 のレンディション機能を使用します。 これらのフォームテンプレートは、アセットと共に、AEMリポジトリやファイルシステムに配置することも、http 経由で公開することもできます。 ただし、Forms Manager を使用してフォームを管理する場合には、テンプレートとアセットを AEM リポジトリに置く必要があります。

HTML5 フォームの動作は、その大部分が PDF フォームの動作に一致していますが、両方の形式には他方の形式で適用されない機能がいくつかあります。たとえば、Adobe Reader でバーコードが PDF フォームに適用される方法が Mobile フォームとは異なったり、フォームにデジタル署名を行う方法も各形式で異なります。そのような違いについて詳しくは、[HTML5 フォームと PDF フォームの機能の違い](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)を参照してください。

XFA の一般的な機能については、次のベストプラクティスとガイドラインを参照して、両方の形式で機能するフォームをデザインします。

## ベストプラクティス {#best-practices}

スキーマのバインディングやフォームのロジックの記述など、フォームテンプレートのデザインに関するほとんどの手順は同じです。 ただし、Adobe Readerやブラウザーベースのフォームなどのシッククライアントのレンダリングとスクリプティングエンジンには固有の違いがあるので、 [ベストプラクティス](/help/forms/using/design-accessible-html5-forms.md) 記事。 これらのベストプラクティスに従うと、両方の形式で期待通りに機能するようにフォームテンプレートをデザインすることができます。

### AEM Forms Designer の HTML5 フォーム向けの機能 {#capabilities-in-aem-forms-designer-for-html-forms}

#### プレビューHTML {#preview-html}

フォームデザイナーのデザインモードに「プレビューHTML」タブが追加され、デザインプロセス中にHTML5 形式でフォームをプレビューできます。 AEM Forms Designer でこの機能を有効にして設定する方法について詳しくは、 [プレビューHTML](../../forms/using/preview-xdp-forms-html.md).

#### 手書き署名 {#scribble-signature}

HTML5 フォームの主なターゲットはタッチデバイスです。 そのため、AEM Forms Designer に新しい手書き署名コントロールが追加されました。 手書き署名のコントロールは、クリックしてフォームテンプレートにドラッグ＆ドロップすると設定できます。HTML5 レンディションでは手書きフィールドとしてレンダリングされるため、タッチデバイスで署名を手書きするのに使用できます。デスクトップ機器では、手書きフィールドとしてマウスのコントロールで使用できます。この機能の使用方法について詳しくは、[XFA 手書きフィールド](../../forms/using/scribble-signature.md)を参照してください。

![4](assets/4.png)

#### リッチテキスト形式 {#rich-text-format}

テキストフィールドをリッチテキストフィールドに変換できます。テキストフィールドに書式設定オプションのリストを追加します。変換するには、Forms Designer を開き、 **[!UICONTROL デザインビュー]**. 「**[!UICONTROL フィールド]**」タブで、**[!UICONTROL フィールドの形式]**&#x200B;ドロップダウンリストから「**[!UICONTROL リッチテキスト]**」を選択します。これで、XFA フォームが HTML5 フォームとしてレンダリングされると、そのフィールドはリッチテキストフィールドとしてレンダリングされます。選択 ![最大化](assets/maximize_icon.svg) をクリックして、その他の書式設定オプションを表示します。
