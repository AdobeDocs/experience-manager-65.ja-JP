---
title: アダプティブフォームのレイアウトの機能
description: 各種デバイスごとのアダプティブフォームのレイアウトと外観はレイアウト設定で管理できます。各種レイアウトとレイアウトの適用方法について説明します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 100%

---

# アダプティブフォームのレイアウトの機能{#layout-capabilities-of-adaptive-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/layout-capabilities-adaptive-forms.html?lang=ja) |
| AEM 6.5 | この記事 |


Adobe Experience Manager（AEM）では、簡単に使用できるアダプティブフォームを作成でき、エンドユーザーに動的なエクスペリエンスを提供します。フォームのレイアウトは、アダプティブフォームでの各項目やコンポーネントの表示方法をコントロールします。

## 必要な知識 {#prerequisite-knowledge}

アダプティブフォームの各種レイアウト機能を学習する前に、次の記事を参照してアダプティブフォームの詳細を理解してください。

[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)

[フォーム作成の概要](../../forms/using/introduction-forms-authoring.md)

## レイアウトのタイプ {#types-of-layouts}

アダプティブフォームは次のタイプのレイアウトを提供します。

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

フォーム作成者は、ルートパネルを含めたアダプティブフォームの各パネルにレイアウトを関連付けることができます。

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

### ウィザード - 複数の手順を 1 つずつ表示するフォーム {#wizard-a-multi-step-form-showing-one-step-at-a-time}

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

パネルの上に表示されているタブ

## モバイルレイアウト {#mobile-layouts}

モバイルレイアウトはモバイルデバイスの比較的小さい画面で、ユーザーが容易にナビゲーションできるようにします。モバイルレイアウトでは、フォームのナビゲーションにタブ付きスタイルまたはウィザードスタイルを使用します。モバイルレイアウトを適用するとフォーム全体を単一のレイアウトで表示します。

このレイアウトでは、ナビゲーションバーとナビゲーションメニューを使用してナビゲーションをコントロールします。ナビゲーションバーで、**進む**&#x200B;と&#x200B;**戻る**&#x200B;のナビゲーションステップはそれぞれ **&lt;** と **>** のアイコンで示されます。

モバイルレイアウトは`/libs/fd/af/layouts/mobile/`から使用できます。アダプティブフォームでは、デフォルトで次のモバイルレイアウトを使用できます。

![アダプティブフォームのモバイルレイアウトのリスト](assets/mobile-navigation.png)

アダプティブフォームのモバイルレイアウトのリスト

モバイルレイアウトを使用する場合、![aem6forms_form_menu](assets/aem6forms_form_menu.png) アイコンをタップすると、各種フォームパネルにアクセスできるフォームメニューを使用できます。

### フォームのヘッダー部分にパネルタイトルを表示するレイアウト {#layout-with-panel-titles-in-the-form-header}

レイアウトの名称の通り、このレイアウトはナビゲーションメニューおよびナビゲーションバーと併せてパネルのタイトルを表示します。また、このレイアウトではナビゲーションに「進む」アイコンと「戻る」アイコンを使用します。

![フォームのヘッダー部分にパネルタイトルを表示するモバイルレイアウト](assets/mobile_layout_with.png)

フォームのヘッダー部分にパネルタイトルを表示するモバイルレイアウト

### フォームのヘッダー部分にパネルタイトルを表示しないレイアウト {#layout-without-panel-titles-in-the-form-header}

レイアウトの名称の通り、このレイアウトはナビゲーションメニューおよびナビゲーションバーのみ表示し、パネルのタイトルは表示しません。また、このレイアウトではナビゲーションに「進む」アイコンと「戻る」アイコンを使用します。

![フォームのヘッダー部分にパネルタイトルを表示しないモバイルレイアウト](assets/mobile_layout_without.png)

フォームのヘッダー部分にパネルタイトルを表示しないモバイルレイアウト

## ツールバーレイアウト {#toolbar-layouts}

ツールバーレイアウトはアダプティブフォームに追加するアクションボタンの配置および表示をコントロールします。このレイアウトはフォームレベルまたは各パネルレベルで追加できます。

![ボタンのレイアウトをコントロールするアダプティブフォームのツールバーレイアウトのリスト](assets/toolbar-layouts.png)

アダプティブフォームのツールバーレイアウトのリスト

ツールバーレイアウトは `/libs/fd/af/layouts/toolbar` の場所で使用できます。アダプティブフォームではデフォルトで次のツールバーレイアウトを使用できます。

### ツールバーのデフォルトレイアウト {#default-layout-for-toolbar}

アダプティブフォームでアクションボタンを追加したときに、デフォルトレイアウトとしてこのレイアウトが選択されます。このレイアウトを選択すると、デスクトップおよびモバイルの両デバイスで同一のレイアウトを表示します。

また、このレイアウトで設定されたアクションボタンを含むツールバーを複数追加できます。アクションボタンはフォームのコントロールに関連付けられます。ツールバーはパネルの前または後に設定できます。

![ツールバーのデフォルト表示](assets/toolbar_layout_default.png)

ツールバーのデフォルト表示

### ツールバーをモバイルに最適化したレイアウト {#mobile-fixed-layout-for-toolbar}

このレイアウトを選択すると、デスクトップデバイスとモバイルデバイスで異なるレイアウトが表示されます。

デスクトップレイアウトでは、特定のラベルを使用してアクションボタンを追加できます。このレイアウトで設定できるツールバーは 1 つのみです。このレイアウトでツールバーを 1 つ以上設定した場合、モバイルデバイス上でツールバーが重なり、表示されるのはそのうち 1 つのみです。例えば、ツールバーを表示できるのはフォームの下部か上部、またはフォームのパネルの前か後のどれか 1 つに限られます。

モバイルレイアウトでは、アイコンを使用してアクションボタンを追加できます。

![ツールバーをモバイルに最適化したレイアウト](assets/toolbar_layout_mobile_fixed.png)

ツールバーをモバイルに最適化したレイアウト
