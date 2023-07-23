---
title: アダプティブフォームのレイアウトの機能
seo-title: Layout capabilities of adaptive forms
description: 様々なデバイスでのアダプティブフォームのレイアウトと外観は、レイアウト設定で管理できます。 各種レイアウトとレイアウトの適用方法について説明します。
seo-description: Layout and appearances of adaptive forms on various devices are governed by the layout settings. Understand the various layouts and how to apply them.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
feature: Adaptive Forms
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 64%

---

# アダプティブフォームのレイアウトの機能{#layout-capabilities-of-adaptive-forms}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/layout-capabilities-adaptive-forms.html) |
| AEM 6.5 | この記事 |



Adobe Experience Manager(AEM) を使用すると、使いやすいアダプティブフォームを作成して、エンドユーザーにダイナミックなエクスペリエンスを提供できます。 フォームレイアウトは、アダプティブフォームでの項目やコンポーネントの表示方法を制御します。

## 必要な知識 {#prerequisite-knowledge}

アダプティブフォームの各種レイアウト機能を学習する前に、次の記事を参照してアダプティブフォームの詳細を理解してください。

[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)

[フォーム作成の概要](../../forms/using/introduction-forms-authoring.md)

## レイアウトのタイプ {#types-of-layouts}

アダプティブフォームでは、次のタイプのレイアウトが提供されます。

**パネルレイアウト**&#x200B;は、パネル内の項目やコンポーネントをデバイス上で表示する方法をコントロールします。

**モバイルレイアウト**&#x200B;は、モバイルデバイスでのフォームのナビゲーションをコントロールします。デバイスの幅が 768 ピクセル以上の場合、レイアウトはモバイルと判断され、モバイルデバイス向けに最適化されます。

**ツールバーレイアウト**&#x200B;は、フォーム内のツールバーまたはパネルツールバーのアクションボタンの配置をコントロールします。

これらのすべてのパネルレイアウトは次の場所で定義されます。

`/libs/fd/af/layouts`。

>[!NOTE]
>
>アダプティブフォームのレイアウトを変更する場合、AEM でオーサリングモードを使用してください。

![CRX リポジトリ内のレイアウトの格納場所](assets/layouts_location_in_crx.png)

## パネルレイアウト {#panel-layout}

フォーム作成者は、ルートパネルを含むアダプティブフォームの各パネルにレイアウトを関連付けることができます。

パネルレイアウトは `/libs/fd/af/layouts/panel` の場所で利用できます。

![アダプティブフォームのルートパネルに使用できるパネルレイアウトのリスト](assets/layouts.png)

アダプティブフォームのパネルレイアウトのリスト

### レスポンシブ - ナビゲーションなしですべてを 1 ページに {#responsive-everything-on-one-page-without-navigation-br}

このパネルレイアウトを使用すると、特別なナビゲーションなしでレイアウトをデバイスの画面サイズに合うように調整するレスポンシブレイアウトを作成できます。

このレイアウトを使用すると、複数の&#x200B;**[!UICONTROL パネルのアダプティブフォーム]**&#x200B;コンポーネントをパネル内に順番に配置することができます。

![レスポンシブレイアウトを使用したフォームの小画面での表示例](assets/responsive_layout_seen_on_small_screen.png)

レスポンシブレイアウトを使用したフォームの小画面での表示例

![レスポンシブレイアウトを使用したフォームの大画面での表示例](assets/responsive_layout_seen_on_large_screen.png)

レスポンシブレイアウトを使用したフォームの大画面での表示例

### ウィザード — 複数の手順を 1 つずつ表示するフォーム {#wizard-a-multi-step-form-showing-one-step-at-a-time}

このパネルレイアウトを使用すると、フォーム上にガイド付きのナビゲーションが提供できます。例えば、ユーザーを 1 手順ずつガイドしながらフォーム内の必須情報を取得したい場合、このレイアウトを使用します。

`Panel adaptive form` コンポーネントを使用して、パネル内のステップバイステップのナビゲーションを提供します。このレイアウトを使用すると、現在の手順を完了しない限りユーザーは次の手順に進めません。

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![複数手順フォームのウィザードレイアウトでのステップ完了の式](assets/layout-sidebar.png)

複数手順フォームのウィザードレイアウトでのステップ完了の式

![ウィザードレイアウトを使用したフォーム](assets/wizard-layout.png)

ウィザードを使用したフォーム

### アコーディオンデザインのレイアウト {#layout-for-accordion-design}

このレイアウトを使用すると、アコーディオンスタイルのナビゲーションを備えたパネルに `Panel adaptive form` コンポーネントを配置できます。また、このレイアウトを使用すると、繰り返し可能なパネルを作成できます。繰り返し可能なパネルを使用すれば、必要に応じて動的にパネルを追加したり削除することができます。パネルの繰り返しの最小数、最大数を定義することができます。また、パネル内の項目に入力される情報に応じて動的にパネルのタイトルを決定することができます。

最小化したパネルのタイトルにエンドユーザーが提供した値を表示するために、サマリ式を使用することができます。

![アコーディオンレイアウトを使用したアダプティブフォームの繰り返し可能なパネル](assets/repeatable_panels_using_accordion_layout.png)

アコーディオンレイアウトを使用して作成された繰り返し可能なパネル

### タブ付きレイアウト - タブを左側に表示 {#tabbed-layout-tabs-appear-on-the-left}

このレイアウトを使用すると、タブ付きナビゲーションのパネルに `Panel adaptive form` コンポーネントを配置できます。タブはパネルコンテンツの左側に配置されます。

![タブ付きレイアウトでタブ左側表示](assets/tabbed_layout_left.png)

パネルの左側にタブ表示

### タブ付きレイアウト - タブを上に表示 {#tabbed-layout-tabs-appear-on-the-top}

このレイアウトを使用すると、タブ付きナビゲーションのパネルに `Panel adaptive form` コンポーネントを配置できます。タブはパネルコンテンツの上に配置されます。

![タブを上に表示したアダプティブフォームのタブ付きレイアウト](assets/tabbed_layout_top.png)

パネルの上に表示されるタブ

## モバイルレイアウト {#mobile-layouts}

モバイルレイアウトを使用すると、比較的小さい画面でモバイルデバイス上でわかりやすいナビゲーションが可能になります。 モバイルレイアウトでは、フォームのナビゲーションにタブ付きスタイルまたはウィザードスタイルを使用します。 モバイルレイアウトを適用すると、フォーム全体に対して 1 つのレイアウトが提供されます。

このレイアウトは、ナビゲーションバーとナビゲーションメニューを使用してナビゲーションを制御します。 ナビゲーションバーで、**進む**&#x200B;と&#x200B;**戻る**&#x200B;のナビゲーションステップはそれぞれ **&lt;** と **>** のアイコンで示されます。

モバイルレイアウトは`/libs/fd/af/layouts/mobile/`から使用できます。アダプティブフォームでは、デフォルトで次のモバイルレイアウトを使用できます。

![アダプティブフォームのモバイルレイアウトのリスト](assets/mobile-navigation.png)

アダプティブフォームのモバイルレイアウトのリスト

モバイルレイアウトを使用する場合、![aem6forms_form_menu](assets/aem6forms_form_menu.png) アイコンをタップすると、各種フォームパネルにアクセスできるフォームメニューを使用できます。

### フォームのヘッダー部分にパネルタイトルを表示するレイアウト {#layout-with-panel-titles-in-the-form-header}

このレイアウトは、名前が示すように、ナビゲーションメニューおよびナビゲーションバーと共にパネルタイトルを表示します。 このレイアウトでは、ナビゲーション用に「次へ」アイコンと「前へ」アイコンも表示されます。

![フォームのヘッダー部分にパネルタイトルを表示するモバイルレイアウト](assets/mobile_layout_with.png)

フォームのヘッダー部分にパネルタイトルを表示するモバイルレイアウト

### フォームのヘッダー部分にパネルタイトルを表示しないレイアウト {#layout-without-panel-titles-in-the-form-header}

このレイアウトは、名前が示すように、ナビゲーションメニューとナビゲーションバーのみを表示し、パネルタイトルは表示されません。 このレイアウトでは、ナビゲーション用に「次へ」アイコンと「前へ」アイコンも表示されます。

![フォームのヘッダー部分にパネルタイトルを表示しないモバイルレイアウト](assets/mobile_layout_without.png)

フォームのヘッダー部分にパネルタイトルを表示しないモバイルレイアウト

## ツールバーレイアウト {#toolbar-layouts}

ツールバーレイアウトはアダプティブフォームに追加するアクションボタンの配置および表示をコントロールします。このレイアウトはフォームレベルまたは各パネルレベルで追加できます。

![ボタンのレイアウトをコントロールするアダプティブフォームのツールバーレイアウトのリスト](assets/toolbar-layouts.png)

アダプティブフォームのツールバーレイアウトのリスト

ツールバーレイアウトは `/libs/fd/af/layouts/toolbar` の場所で使用できます。アダプティブフォームではデフォルトで次のツールバーレイアウトを使用できます。

### ツールバーのデフォルトのレイアウト {#default-layout-for-toolbar}

このレイアウトは、アダプティブフォームにアクションボタンを追加したときにデフォルトのレイアウトとして選択されます。 このレイアウトを選択すると、デスクトップとモバイルの両方のデバイスで同じレイアウトが表示されます。

また、このレイアウトで設定したアクションボタンを含む複数のツールバーを追加できます。 アクションボタンは、フォームコントロールに関連付けられています。 ツールバーは、パネルの前または後に設定できます。

![ツールバーのデフォルト表示](assets/toolbar_layout_default.png)

ツールバーのデフォルト表示

### ツールバーをモバイルに最適化したレイアウト {#mobile-fixed-layout-for-toolbar}

このレイアウトを選択すると、デスクトップとモバイルデバイスの代替レイアウトが表示されます。

デスクトップレイアウトでは、特定のラベルを使用してアクションボタンを追加できます。 このレイアウトで設定できるツールバーは 1 つだけです。 このレイアウトで複数のツールバーが設定されている場合、モバイルデバイスでは重複があり、1 つのツールバーのみが表示されます。 例えば、ツールバーをフォームの下部や上部に配置したり、パネルの前後に配置したりできます。

モバイルレイアウトの場合、アイコンを使用してアクションボタンを追加できます。

![ツールバーをモバイルに最適化したレイアウト](assets/toolbar_layout_mobile_fixed.png)

ツールバーをモバイルに最適化したレイアウト
