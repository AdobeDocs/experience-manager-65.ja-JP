---
title: フォームのプレビュー
seo-title: Previewing a form
description: 発行またはアクティベートする前にフォームをプレビューし、期待通りにフォームが動作することを確認できます。 プレビューオプションは、サポートされているフォームタイプによって異なる場合があります。
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 39%

---

# フォームのプレビュー {#previewing-a-form}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

## 概要 {#overview}

AEM Formsでは、リポジトリ内に存在するフォームとドキュメントをプレビューできます。 プレビューを使用すると、フォームがエンドユーザーにリリースされたときの外観と動作を正確に把握できます。

フォームをプレビューすると、フォームはインタラクティブインターフェイスでレンダリングされ、ユーザーはフォームにデータを入力できます。 ドキュメントをプレビューすると、ドキュメントは非インタラクティブモードでレンダリングされ、ユーザーはドキュメントの表示のみ可能です。 フォームの場合は、カスタムプレビューの追加オプションを使用できます。 このオプションを使用すると、XML ファイルのデータを使用してフォームをプレビューできます。 プレビュー中のフォームの一部またはすべてのフィールドにデータが入力されます。

次の表に、サポートされているフォームのタイプごとに使用できるプレビューオプションを示します。

<table>
 <tbody>
  <tr>
   <td><strong>アセットタイプ</strong><br /> </td>
   <td><strong>使用できるプレビューオプション</strong><br /> </td>
  </tr>
  <tr>
   <td>ドキュメント</td>
   <td>PDFプレビュー</td>
  </tr>
  <tr>
   <td>PDFフォーム</td>
   <td>PDF プレビューとデータを使用したプレビュー<br /> </td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>HTML プレビューとデータを使用した HTML プレビュー</td>
  </tr>
  <tr>
   <td>フォームテンプレート</td>
   <td>PDF プレビュー、データを使用した PDF プレビュー、HTML プレビュー、データを使用した HTML プレビュー<br /> </td>
  </tr>
 </tbody>
</table>

## フォームのプレビュー {#previewing-a-form-1}

1. プレビューするアセットを選択し、アクションツールバーのプレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックします。

   >[!NOTE]
   >
   >アセットを選択するには、デフォルトのカード表示をリスト表示に切り替えます。![aem6forms_viewlist](assets/aem6forms_viewlist.png) または ![aem6forms_viewcard](assets/aem6forms_viewcard.png) をクリックして、表示を切り替えます。

1. 「プレビュー」をクリックすると、選択したアセットタイプで使用できるプレビューオプションが表示されます。 目的のオプションをクリックして、選択したアセットを新しいタブでレンダリングします。

   以下のオプションがあります。

   * HTML としてプレビュー
   * データを使用したプレビュー
   * PDF としてプレビュー（フォームテンプレートから選択可能）

## データを使用してプレビュー {#preview-with-data}

「**データを使用したプレビュー**」を選択すると、実際のデータが入力された状態でフォームの様子を見ることができます。データを使用したプレビューオプションでは、サンプルユーザーデータを含めた XML をアップロードできます。サンプルのユーザーデータを使用して、選択した形式でプレビューフォームに入力します。

1. アセットを選択し、プレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックし、「**データを使用してプレビュー**」を選択します。
1. フォームをプレビューダイアログで、FormData を XML ファイルとして指定します。 XML からマージされたデータでフォームをレンダリングするには、「プレビュー」をクリックします。
