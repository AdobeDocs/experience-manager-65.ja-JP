---
title: アダプティブフォームコンポーネントのインラインスタイリング
seo-title: Inline CSS properties for adaptive form components
description: アダプティブフォームにカスタムスタイルを適用することができますが、アダプティブフォームの個々のコンポーネントにインライン CSS プロパティを適用することもできます。
seo-description: While you can apply custom styles on an adaptive form, you can also apply inline CSS properties on individual components of an adaptive form.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Adaptive Forms
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 39%

---

# アダプティブフォームコンポーネントのインラインスタイリング {#inline-styling-of-adaptive-form-components}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象 [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用してアダプティブFormsを作成する古い方法について説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html) |
| AEM 6.5 | この記事 |

アダプティブフォームの全体的な外観とスタイルは、 [テーマエディター](../../forms/using/themes.md). また、アダプティブフォームの個々のコンポーネントにインライン CSS スタイルを適用し、変更をその場でプレビューすることもできます。 インラインスタイルは、テーマで設定されたスタイルよりも優先されます。

## インライン CSS プロパティを適用 {#apply-inline-css-properties}

コンポーネントにインラインスタイルを追加するには、次の手順を実行します。

1. フォームエディターでフォームを開き、モードをスタイルモードに変更します。 モードをスタイルモードに変更するには、ページツールバーで ![canvas-drop-down](assets/canvas-drop-down.png)／**スタイル**&#x200B;をタップします。
1. ページ内のコンポーネントを選択し、編集ボタン ![edit-button](assets/edit-button.png) をタップします。スタイル設定プロパティがサイドバーに開きます。

   サイドバーのフォーム階層ツリーからコンポーネントを選択することもできます。 フォーム階層ツリーは、サイドバーでフォームオブジェクトとして使用できます。

   サイドバーからコンポーネントを選択することもできます。 スタイルモードでは、フォームオブジェクトの下にコンポーネントが表示されます。ただし、サイドバーのフォームオブジェクトリストには、フィールドやパネルなどのコンポーネントが一覧表示されます。 フィールドとパネルは、テキストボックスやラジオボタンなどのコンポーネントを含むことができる汎用コンポーネントです。

   サイドバーからコンポーネントを選択すると、リストに表示されたすべてのサブコンポーネントと、選択したコンポーネントのプロパティが表示されます。 特定のサブコンポーネントを選択してスタイルを設定できます。

1. サイドバーのタブをクリックして、CSS プロパティを指定します。 次のようなプロパティを指定できます。

   * 寸法と位置（表示設定、パディング、高さ、幅、余白、位置、z インデックス、フロート、クリア、オーバーフロー）
   * テキスト（フォントファミリー、太さ、色、サイズ、行の高さ、整列）
   * 背景（画像とグラデーション、背景色）
   * 境界線（幅、スタイル、色、半径）
   * 効果（影、透明度）
   * 詳細（コンポーネントのカスタム CSS を作成できます）

1. 同様に、コンポーネントの他の部分（ウィジェット、キャプション、ヘルプなど）のスタイルを適用できます。
1. 「**完了**」をクリックして変更を確定するか、または「**キャンセル**」をクリックして変更を破棄します。

## 例：フィールドコンポーネントのインラインスタイル {#example-inline-styles-for-a-field-component}

以下の図は、インラインスタイルが適用される前後のテキストフィールドを示しています。

![インラインスタイルが適用される前のテキストボックスコンポーネント](assets/no-style.png)

インラインスタイルプロパティを適用する前のテキストボックスコンポーネント

次の画像に示すように、次の CSS プロパティを適用した後のテキストボックススタイルの変更に注意してください。

<table>
 <tbody>
  <tr>
   <td><p>セレクター</p> </td>
   <td><p>CSS プロパティ</p> </td>
   <td><p>値</p> </td>
   <td><p>効果</p> </td>
  </tr>
  <tr>
   <td><p>フィールド</p> </td>
   <td><p>境界線</p> </td>
   <td><p>境界線の幅=2px</p> <p>境界線のスタイル=実線</p> <p>境界線のカラー=#1111</p> </td>
   <td><p>フィールドの周囲に黒い 2px 幅の境界線を作成します</p> </td>
  </tr>
  <tr>
   <td><p>テキストボックス</p> </td>
   <td><p>背景色</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>背景色を CornflowerBlue (#6495ED) に変更します。</p> <p>注意：値フィールドには、カラー名またはその 16 進コードを指定できます。</p> </td>
  </tr>
  <tr>
   <td><p>ラベル</p> </td>
   <td><p>寸法と位置/幅</p> </td>
   <td><p>100 px</p> </td>
   <td><p>ラベルの幅を 100 px に固定します</p> </td>
  </tr>
  <tr>
   <td>フィールドヘルプアイコン</td>
   <td>テキスト/フォントカラー</td>
   <td>#2ECC40</td>
   <td>ヘルプアイコンの色を変更します。</td>
  </tr>
  <tr>
   <td><p>詳細な説明</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中央</p> </td>
   <td><p>ヘルプの長い説明を中央に揃えます</p> </td>
  </tr>
 </tbody>
</table>

![インラインスタイルが適用された後のテキストボックスのスタイル](assets/applied-style.png)

インラインスタイルプロパティを適用した後のテキストボックスコンポーネント

上記の手順に従って、パネル、送信ボタン、ラジオボタンなど、他のコンポーネントを選択してスタイルを設定できます。

>[!NOTE]
>
>スタイルのプロパティは、選択したコンポーネントにより異なります。
