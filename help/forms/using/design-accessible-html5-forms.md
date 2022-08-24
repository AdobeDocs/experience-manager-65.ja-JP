---
title: アクセス可能な HTML5 フォームの設計
seo-title: Designing accessible HTML5 forms
description: HTML5 フォームは ARIA HTML5 アクセシビリティ標準を使用します。これらのフォームはタブナビゲーションをサポートし、一般的なスクリーンリーダーに対応するように認定されています。
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 100%

---

# アクセス可能な HTML5 フォームの設計 {#designing-accessible-html-forms}

HTML5 フォームは ARIA HTML5 アクセシビリティ標準を基に、アクセシビリティを備えた HTML フォームを生成します。これらのフォームは、タブナビゲーション（Mozilla FireFox を除く）をサポートし、一般的な画面読み上げアプリケーションと互換性があります。優れたアクセシビリティの機能を備えた HTML5 フォームを生成するには、何らかの基本的なデザインガイドラインに基づいて XFA フォームをデザインします。デザインガイドラインには正しいタブ順序の設定、および各フォームコントロールのために読み上げテキストコンテンツの提供などが含まれます。AEM Forms Designer ではこれらのフォームコントロール属性を設定し、アクセシビリティを備えた PDF フォームおよび HTML5 フォームを生成できます。

*注意：タブナビゲーションは、値の合計を表示する計算フィールドなどの保護付きフィールドには適用されません。スクリーンリーダーが保護フィールドの値を読み取れるようにするには、空の読み取り専用フィールドを保護フィールドの上、または横のいずれかに配置します。保護フィールドの値を新しい読み取り専用フィールドに割り当てます。スクリーンリーダーやタブナビゲーションはこの読み取り専用フィールドを選択し、保護フィールドの値として読み上げることができます。*

AEM Forms Designer にはスクリーンリーダーに渡すことが可能な多数の読み上げテキストオプションが含まれています。フォーム内の各オブジェクトごとに、スクリーンリーダーテキストに関する次のいずれかの設定を選択できます。

* カスタムスクリーンリーダーテキスト（アクセシビリティパレットの使用で設定可能）。作成者はボタンとフィールドの名前に加え、その目的について注釈を付けることができます。
* ツールヒント（アクセシビリティパレットで設定可能）。
* フォーム上のフィールドのキャプション。
* オブジェクトの名前（「連結」タブの「名前」オプションで指定）。

![アクセシビリティ](assets/accessibility.png)

ツールヒント、スクリーンリーダーテキスト、およびキャプションなど、複数のオプションがフォームコントロールで使用可能なとき、スクリーンリーダーはこれらのプロパティを 1 つだけ使用します。デフォルト順序はカスタムスクリーンリーダーテキスト、ツールヒント、キャプション、名前です。デフォルト順序はアクセシビリティパレットにある「**スクリーンリーダーの優先順位**」オプションを使用してオーバーライドできます。
