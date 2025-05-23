---
title: アダプティブフォームコンポーネントのインラインスタイリング
description: アダプティブフォームではカスタムスタイルを適用することができますが、アダプティブフォームの個々のコンポーネントにインライン CSS プロパティを適用することもできます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 100%

---

# アダプティブフォームコンポーネントのインラインスタイリング {#inline-styling-of-adaptive-form-components}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html?lang=ja) |
| AEM 6.5 | この記事 |

アダプティブフォームの全体的な外観とスタイルは、[テーマエディター](../../forms/using/themes.md)でスタイルを指定して定義できます。また、アダプティブフォームの個々のコンポーネントにインライン CSS スタイルを適用し、即座に変更をプレビューすることもできます。インラインスタイルは、テーマで設定されたスタイルよりも優先されます。

## インライン CSS プロパティを適用 {#apply-inline-css-properties}

コンポーネントにインラインスタイルを追加するには、次の手順を実行します。

1. フォームエディターからフォームを開き、モードをスタイルモードに変更します。モードをスタイルモードに変更するには、ページツールバーで ![canvas-drop-down](assets/canvas-drop-down.png)／**スタイル**&#x200B;を選択します。
1. ページ内のコンポーネントを選択し、編集ボタン ![edit-button](assets/edit-button.png) を選択します。サイドバーにスタイルのプロパティが開きます。

   サイドバーのフォーム階層ツリーからコンポーネントを選択することもできます。フォーム階層ツリーは、サイドバーのフォームオブジェクトとして使用できます。

   サイドバーからコンポーネントを選択することもできます。スタイルモードでは、フォームオブジェクトの下にコンポーネントが表示されます。ただし、サイドバーのフォームオブジェクトリストにはフィールドやパネルなどのコンポーネントが表示されます。フィールドとパネルは、テキストボックスやラジオボタンなどのコンポーネントを含めることができる汎用的なコンポーネントです。

   サイドバーからコンポーネントを選択すると、選択したコンポーネントのすべてのサブコンポーネントのリストと選択したコンポーネントのプロパティが表示されます。特定のサブコンポーネントを選択して、そのスタイルを設定できます。

1. サイドバーのタブをクリックして、CSS プロパティを指定します。次のようなプロパティを指定できます。

   * 寸法と位置（表示設定、パディング、高さ、幅、余白、位置、z インデックス、フロート、クリア、オーバーフロー）
   * テキスト（フォントファミリー、太さ、色、サイズ、行の高さ、整列）
   * 背景（画像とグラデーション、背景色）
   * 境界線（幅、スタイル、色、半径）
   * 効果（シャドウ、透明度）
   * 詳細（コンポーネントのカスタム CSS を作成できます）

1. 同様に、コンポーネントの他の部分（ウィジェット、キャプション、ヘルプなど）のスタイルを適用できます。
1. 「**完了**」を選択して変更を確定するか、または「**キャンセル**」を選択して変更を破棄します。

## 例：フィールドコンポーネントのインラインスタイル {#example-inline-styles-for-a-field-component}

以下の図は、インラインスタイルが適用される前後のテキストフィールドを示しています。

![インラインスタイルが適用される前のテキストボックスコンポーネント](assets/no-style.png)

インラインスタイルプロパティを適用する前のテキストボックスコンポーネント

次の図に示すように、以下の CSS プロパティを適用した後のテキストボックススタイルの変化に注目してください。

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
   <td><p>フィールドの周囲に黒色の 2px 幅の境界線を作成</p> </td>
  </tr>
  <tr>
   <td><p>テキストボックス</p> </td>
   <td><p>背景色</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>背景色を CornflowerBlue （#6495ED）に変更</p> <p>メモ：値フィールドでは、色の名前やその進数コードを指定することができます。</p> </td>
  </tr>
  <tr>
   <td><p>ラベル</p> </td>
   <td><p>寸法と位置／幅</p> </td>
   <td><p>100px</p> </td>
   <td><p>ラベルの幅を 100px に固定</p> </td>
  </tr>
  <tr>
   <td>フィールドヘルプアイコン</td>
   <td>テキスト／フォントカラー</td>
   <td>#2ECC40</td>
   <td>ヘルプアイコンの表面の色を変更します。</td>
  </tr>
  <tr>
   <td><p>詳細な説明</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中央</p> </td>
   <td><p>長いヘルプ説明を中央揃えにする</p> </td>
  </tr>
 </tbody>
</table>

![インラインスタイルが適用された後のテキストボックスのスタイル](assets/applied-style.png)

インラインスタイルプロパティを適用した後のテキストボックスコンポーネント

上述の手順に従って、他のコンポーネント（パネル、送信ボタン、ラジオボタンなど）を選択し、そのスタイルを設定できます。

>[!NOTE]
>
>スタイルのプロパティは、選択したコンポーネントにより異なります。
