---
title: アクセス可能な HTML5 フォームの設計
description: HTML5 フォームは ARIA HTML5 アクセシビリティ標準を使用します。 これらのフォームはタブナビゲーションをサポートし、一般的なスクリーンリーダーに対応するように認定されています。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 95%
---
# アクセス可能な HTML5 フォームの設計 {#designing-accessible-html-forms}

HTML5 フォームは ARIA HTML5 アクセシビリティ標準を基に、アクセシビリティを備えた HTML フォームを生成します。 これらのフォームは、タブナビゲーション（Mozilla FireFox を除く）をサポートし、一般的な画面読み上げアプリケーションと互換性があります。 優れたアクセシビリティの機能を備えた HTML5 フォームを生成するには、何らかの基本的なデザインガイドラインに基づいて XFA フォームテンプレートをデザインします。 デザインガイドラインには正しいタブ順序の設定、および各フォームコントロールのために読み上げテキストコンテンツの提供などが含まれます。 AEM Forms Designer ではこれらのフォームコントロール属性を設定し、アクセシビリティを備えた PDF フォームおよび HTML5 フォームを生成できます。

*注:Tabbed ナビゲーションでは、値の合計を表示する計算フィールドなど、保護されたフィールドはカバーされません。 スクリーンリーダーが保護フィールドの値を読み取れるようにするには、空の読み取り専用フィールドを保護フィールドの上、または横のいずれかに配置します。 保護フィールドの値を新しい読み取り専用フィールドに割り当てます。 スクリーンリーダーやタブナビゲーションはこの読み取り専用フィールドを選択し、保護フィールドの値として読み上げることができます。*

AEM Forms Designer にはスクリーンリーダーに渡すことが可能ないくつかの読み上げテキストオプションが含まれています。 フォーム内の各オブジェクトごとに、スクリーンリーダーテキストに関する次のいずれかの設定を選択できます。

* カスタムスクリーンリーダーテキスト（アクセシビリティパレットの使用で設定可能）。 作成者はボタンとフィールドの名前に加え、その目的について注釈を付けることができます。
* ツールヒント（アクセシビリティパレットで設定可能）。
* フォーム上のフィールドのキャプション。
* オブジェクトの名前（「連結」タブの「名前」オプションで指定）。

![アクセシビリティ](assets/accessibility.png)

ツールヒント、スクリーンリーダーテキスト、およびキャプションなど、複数のオプションがフォームコントロールで使用可能なとき、スクリーンリーダーはこれらのプロパティを 1 つだけ使用します。 デフォルト順序はカスタムスクリーンリーダーテキスト、ツールヒント、キャプション、および名前です。 デフォルト順序はアクセシビリティパレットにある「**スクリーンリーダーの優先順位**」オプションを使用してオーバーライドできます。
