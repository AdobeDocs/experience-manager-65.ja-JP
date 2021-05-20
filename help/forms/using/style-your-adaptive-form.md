---
title: 'アダプティブフォームのスタイル設定 '
seo-title: 'アダプティブフォームのスタイル設定 '
description: 'カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します。 '
seo-description: 'カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します。 '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: アダプティブフォーム
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 65%

---

# アダプティブフォームのスタイル設定 {#do-not-publish-style-your-adaptive-form}

カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します。

![](do-not-localize/08-style_your_adaptiveformmain.png)

これは、「[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて   {#about-the-tutorial}

テーマを使用すると、アダプティブフォームに独自の外観やスタイルを設定できます。アダプティブフォームエディターの初期設定済みテーマを適用することも、独自のカスタムテーマを作成することもできます。AEM [!DNL Forms]には、カスタムテーマを作成するための[テーマエディター](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/themes.html)が用意されています。 単一のテーマを使用すると、モバイル、タブレット、デスクトップで開いた同一のアダプティブフォームに異なる外観を設定できます。テーマエディターを使用する場合、CSS や LESS の予備知識は特に必要ありません。

このチュートリアルを終了すると、以下の操作を実行できるようになります。

* 初期設定済みテーマをアダプティブフォームに適用する
* テーマエディターを使用して、アダプティブフォームのテーマを作成する
* 個別コンポーネントのスタイルを設定する
* オプション：カスタムテーマに Web フォントを使用する

チュートリアルを完了すると、フォームの外観は以下のようになります。

![カスタムテーマが使用されているフォーム](assets/styled-adaptive-form.png)

## 事前準備 {#before-you-start}

以下に示すヘッダースタイルとロゴの画像をローカルマシンにダウンロードします。`shipping-address-add-update-form` アダプティブフォームのヘッダーは、ヘッダースタイルとロゴの画像を使用します。ヘッダースタイルの画像はヘッダーの右側に表示されます。

[ファイルを入手](assets/header-style.png)

[ファイルを入手](assets/logo-1.png)

## 手順 1：アダプティブフォームへのテーマの適用 {#step-apply-a-theme-to-your-adaptive-form}

アダプティブフォームエディターは多数の初期設定済みテーマを提供します。アダプティブフォームにカスタムスタイルを使用する場合は、初期設定済みテーマを使用してアダプティブフォームを発行することもできます。テーマはアダプティブフォームから独立しています。同一のテーマを複数のアダプティブフォームに適用できます。テーマをアダプティブフォームに適用するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;のプロパティを開きます。プロパティブラウザーで、**[!UICONTROL 基本]**／**[!UICONTROL アダプティブフォームのテーマ]**&#x200B;に移動します。すべての初期設定済みテーマとカスタムテーマが、「**[!UICONTROL アダプティブフォームのテーマ]**」フィールドに表示されます。デフォルトではキャンバステーマが適用されます。
1. 「**[!UICONTROL アダプティブフォームのテーマ]**」フィールドでテーマを選択します（**調査テーマ**&#x200B;など）。![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップして、選択したテーマを適用します。

   ![デフォルトのテーマを使用したアダプティブフォーム](assets/default-adaptive-form.png)

   **図：** *デフォルトテーマを使用したアダプティブフォーム*

   ![調査テーマを使用したアダプティブフォーム](assets/adaptive-form-with-survey-theme.png)

   **図：** *調査テーマを使用したアダプティブフォーム*

## 手順 2：アダプティブフォームの更新 {#step-update-your-adaptive-form}

上記のデザインでは、既存のアダプティブフォームのプレースホルダーテキストとロゴを変更する必要があります。必要な変更を行うには、次の手順を実行します。

1. ヘッダーの既存のロゴとテキストを変更します。ロゴを削除するには、次の手順を実行します。

   1. フォームエディターでフォームを開きます。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. [!UICONTROL header]コンポーネントでロゴ画像をタップし、![cmppr](assets/cmppr.png) **[!UICONTROL properties]**&#x200B;をタップします。 [!UICONTROL image]プロパティで、「 X 」をタップして既存のロゴ画像を削除します。
   1. **[!UICONTROL upload]**&#x200B;をタップし、logo.pngを選択して![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップし、変更を保存します。 画像は、[「](/help/forms/using/style-your-adaptive-form.md#before-you-start)を起動する前に」セクションにダウンロードされました。
   1. ヘッダーテキスト`We.Retail`をタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**&#x200B;をタップします。 ヘッダーテキストを`we retail`に変更します。 `we retail`の`we`にのみ太字書式を適用します。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. タイトルを削除してプレースホルダーテキストを追加します。

   1. 「顧客ID」フィールドをタップし、![cmppr](assets/cmppr.png)プロパティをタップします。
   1. 「**[!UICONTROL タイトル]**」フィールドの内容を「**[!UICONTROL プレースホルダーテキスト]**」フィールドにコピーします。
   1. 「**[!UICONTROL タイトル]**」フィールドの内容を削除し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。
   1. フォーム内のすべてのテキストボックス、数値ボックス、電子メールフィールドで、上記の 3 つの手順を繰り返します。

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 手順 3：アダプティブフォームのカスタムテーマの作成 {#step-create-a-custom-theme-for-your-adaptive-form}

[テーマエディター](/help/forms/using/themes.md)を使用すると、カスタムテーマを作成できます。テーマエディターは非常に強力な WYSIWYG エディターです。視覚的に確認しながら、アダプティブフォームの各種コンポーネントに CSS を適用できます。アダプティブフォームのコンポーネントやパネルのスタイルを詳細にコントロールできます。

アダプティブフォームと同様、テーマは独立したエンティティです。アダプティブフォームのコンポーネントとパネルのスタイル（CSS）が含まれています。スタイルには背景色、状態色、透明度、配置、サイズなど、CSS プロパティが含まれています。テーマを適用すると、指定したスタイルがアダプティブフォームの対応するコンポーネントに適用されます。

このチュートリアルでは、ヘッダー、フッター、テキストコンポーネント、数値コンポーネント、添付ファイルコンポーネント、ボタンのスタイルを設定します。まずテーマを作成することから始めましょう。

### テーマを作成する {#create-a-theme}

1. AEMオーサーインスタンスにログインし、**[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL Forms]** / **[!UICONTROL テーマ]**&#x200B;に移動します。 デフォルトのURLは[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)です。
1. 「**[!UICONTROL 作成]**」をタップし、「**[!UICONTROL テーマ]**」を選択します。テーマの作成に必要なフィールドを含む[!UICONTROL テーマを作成]ページが表示されます。 「**[!UICONTROL タイトル]**」フィールドと「**[!UICONTROL 名前]**」フィールドは入力必須です。

   * **タイトル：** テーマのタイトルを指定します。（**グローバルテーマ**&#x200B;など）。タイトルはテーマのリストから目的のテーマを見つけるのに役立ちます。
   * **名前：** テーマの名前を指定します。（**グローバルテーマ**&#x200B;指定された名前を持つノードがリポジトリに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。

1. 「**[!UICONTROL 作成]**」をタップします。テーマが作成され、フォームを編集用に開くためのダイアログが表示されます。**[!UICONTROL 開く]**&#x200B;をタップして、新しく作成したテーマを新しいタブで開きます。 テーマがテーマエディターで開きます。スタイル設定の場合、テーマエディターはAEM [!DNL Forms]に付属している標準のアダプティブフォームを使用します。

   テーマエディターのUIの使用について詳しくは、「[テーマエディターについて](/help/forms/using/themes.md#aboutthethemeeditor)」を参照してください。

1. **[!UICONTROL テーマのオプション]** ![テーマのオプション](assets/theme-options.png) > **[!UICONTROL 設定]**&#x200B;をタップします。 「**[!UICONTROL フォームのプレビュー]**」フィールドで、**shipping-address-add-update-form**&#x200B;アダプティブフォームを選択し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップして、「**[!UICONTROL 保存]**」をタップします。 テーマエディターで、デフォルトのアダプティブフォームではなく独自のアダプティブフォームを使用できるようになります。テーマエディターに戻るには、「**[!UICONTROL キャンセル]**」をタップします。

   ![カスタムテーマ](assets/custom-theme.png)

   **図：shipping-address-add-update-formアダプティブフォームを使用した** *テーマエディター*

   ![create-a-theme](assets/create-a-theme.png)

   **図：** *デフォルトフォームを使用したアダプティブフォーム*

### ヘッダーとフッターのスタイル設定 {#style-header-and-footer}

ヘッダーとフッターをアダプティブフォームで使用すると、独特な外観を作成できます。通常、ヘッダーには組織のロゴと名前が含まれ、フッターには著作権情報が含まれます。これらは組織の複数のフォーム間で統一されます。shipping-address-add-update-form アダプティブフォームのヘッダーとフッターのスタイルを設定するには、次の手順を実行します。

1. セレクターパネルで&#x200B;**[!UICONTROL ヘッダー]**／**[!UICONTROL テキスト]**&#x200B;オプションに移動します。セレクターパネルはテーマエディターの左側にあります。パネルが表示されない場合は、「![切り替えサイドパネル](assets/toggle-side-panel.png)切り替えサイドパネル」をタップします。

1. 「**[!UICONTROL テキスト]**」アコーディオンで次のプロパティを設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   | プロパティ | 値 |
   |---|---|
   | フォントファミリー | Arial |
   | フォントカラー | FFFFFF |
   | フォントサイズ | 54 px |

1. [!UICONTROL ヘッダー]ウィジェットをタップし、**[!UICONTROL ヘッダー]**&#x200B;をタップします。 ヘッダーウィジェットのスタイルを設定するオプションが左側に表示されます。「**[!UICONTROL Dimensionと位置]**」アコーディオンを展開し、「**[!UICONTROL 高さ]**」を「`120px`」に設定して、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。
1. ヘッダーウィジェットの「**[!UICONTROL 背景]**」アコーディオンを展開し、「**[!UICONTROL 背景色]**」を「`F6921E.`」に設定します。

   **[!UICONTROL 画像とグラデーション]** > **[!UICONTROL +追加]**&#x200B;の上にマウスポインターを置き、**[!UICONTROL 画像]**&#x200B;をタップします。 次のプロパティを設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   | プロパティ | 値 |
   |---|---|
   | 画像 | header-style.png をアップロードします。画像は、[「](/help/forms/using/style-your-adaptive-form.md#before-you-start)を起動する前に」セクションにダウンロードされました。 |
   | 位置 | 右下 |
   | タイル | 繰り返しなし |

1. テーマエディターで、ヘッダーのロゴをタップし、「**[!UICONTROL ヘッダーロゴ]**」をタップします。「Dimensionと位置」アコーディオンを展開し、次のプロパティを設定して![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   <table> 
    <tbody> 
     <tr> 
      <td><b>余白</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>余白</td> 
      <td> 
       <ul> 
        <li>上：1.5rem</li> 
        <li>下：-35 px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>ヒント：</strong> フィールドごとに異なる値を設定するには、<img src="assets/link.png"> リンクアイコンをタップします。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高さ</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. フッターウィジェットをタップし、「**[!UICONTROL フッター]**」をタップします。「**[!UICONTROL 背景]**」アコーディオンを展開し、「**[!UICONTROL 背景色]**」を`F6921E`に設定して、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

### データ取得コンポーネントのスタイル設定とアダプティブフォームの背景の適用 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

アダプティブフォームでは複数のコンポーネントを使用してデータを取得できます。例えば、テキストボックスと数値ボックスを使用できます。すべてのデータ取得コンポーネントと同じスタイルを指定することも、コンポーネントごとに別々のスタイルを指定することもできます。 このチュートリアルでは、数値ボックス（顧客 ID、郵便番号）とテキストボックス（顧客 ID、名前、発送先住所、状態、電子メール）に同じスタイルを適用します。データ取得コンポーネントのスタイルを設定するには：

1. 「**[!UICONTROL 顧客ID]**」フィールドをタップし、「**[!UICONTROL フィールドウィジェット]**」オプションをタップします。 次のプロパティを設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の半径 </td> 
      <td> 
       <ul> 
        <li>上：7 px<br /> </li> 
        <li>右：7 px<br /> </li> 
        <li>下：7 px<br /> </li> 
        <li>左：7 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントファミリー</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントカラー</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントサイズ</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>幅</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>余白</td> 
      <td> 
       <ul> 
        <li>左：10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. **[!UICONTROL 顧客ID]**&#x200B;フィールドの上の空の領域をタップし、**[!UICONTROL レスポンシブパネルコンテナ]**&#x200B;をタップします。 **[!UICONTROL 背景]**／**[!UICONTROL 背景色]**&#x200B;を F1F2F2 に設定します。![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   ![](do-not-localize/responsive-panel-container.png)

### ボタンのスタイル設定 {#style-the-buttons}

カスタムテーマを使用して、アダプティブフォームのすべてのボタンに同じスタイルを適用し、[インラインスタイル](/help/forms/using/inline-style-adaptive-forms.md)を使用して特定のボタンにスタイルを適用することができます。 ボタンのスタイルを設定するには、次の手順を実行します。

1. 「**[!UICONTROL 送信]**」ボタンをタップし、「**[!UICONTROL ボタン]**」オプションをタップします。次のプロパティを設定し、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>境界線<br /> </td> 
      <td>境界線の色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の半径 </td> 
      <td> 
       <ul> 
        <li>上：7 px<br /> </li> 
        <li>右：7 px<br /> </li> 
        <li>下：7 px<br /> </li> 
        <li>左：7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>テキスト<br /> </td> 
      <td>フォントファミリー</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントカラー</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントサイズ</td> 
      <td>18 px</td> 
     </tr> 
    </tbody> 
   </table>

1. アダプティブフォームに[カスタムテーマを適用](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)するか、グローバルテーマを適用します。スタイルがアダプティブフォームに反映されない場合は、ブラウザーのキャッシュを消去して、もう一度やり直してください。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 手順 4：個別コンポーネントのスタイル設定 {#step-style-individual-components}

一部のスタイルは特定のコンポーネントのみに適用されます。このようなコンポーネントのスタイルは、アダプティブフォームエディターで設定します。

1. アダプティブフォームを編集用に開きます。[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 上部バーで「**[!UICONTROL スタイル]**」オプションを選択します。

   ![style-option](assets/style-option.png)

1. 「**[!UICONTROL 添付]**」ボタンをタップし、「![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをタップします。 **[!UICONTROL Dimensionと位置]**&#x200B;アコーディオンで次のプロパティを設定します。

   | プロパティ | 値 |
   |---|---|
   | 浮動小数 | Left |
   | 幅 | 10% |

1. 「**[!UICONTROL 政府が承認した住所の配達確認]**」オプションをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png)アイコンをタップします。 次のプロパティを設定します。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>浮動小数</td> 
      <td>左</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>幅</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>パディング</td> 
      <td> 
       <ul> 
        <li>左：10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>高さ</td> 
      <td>40 px</td> 
     </tr> 
     <tr> 
      <td>寸法と位置<br /> </td> 
      <td>余白</td> 
      <td><br /> 
       <ul> 
        <li>右：2rem</li> 
        <li>左：10rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の幅</td> 
      <td>1 px</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線のスタイル</td> 
      <td>実線</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の半径</td> 
      <td>7 px</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントファミリー</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントカラー</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>フォントサイズ</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>テキスト</td> 
      <td>行の高さ</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 「**[!UICONTROL 送信]**」ボタンをタップし、「![aem_6_3_edit](assets/aem_6_3_edit.png)」アイコンをタップします。 次のプロパティを設定します。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>浮動小数</td> 
      <td>Right</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>余白</td> 
      <td> 
       <ul> 
        <li>上：5rem</li> 
        <li>右：14rem</li> 
        <li>下：20 px</li> 
        <li>左：20 px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 手順 5：オプション：カスタムテーマでの Web フォントの使用 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

アダプティブフォームは各種フォントを使用してデザインできます。アダプティブフォームのデザインに使用するフォントが、アダプティブフォームを表示するデバイスに存在しない場合があります。Webフォントサービスを使用して、必要なフォントをターゲットデバイスに配信できます。

[!DNL Adobe Fonts] は、webフォントサービスです。アダプティブフォームでこのサービスを設定、使用できます。アダプティブフォームで[!DNL Adobe Fonts]を使用するには：

>[!NOTE]
>
>![typekit-to-adobe-fontsは、現在はAdobe Fontsと呼ばれ、](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] Creative Cloudやその他のサブスクリプションに含まれています。[詳細情報](https://fonts.adobe.com/)を参照してください。

1. [Adobe Fonts](https://typekit.com/)アカウントを作成し、キットを作成し、キットにMyriad Proフォントを追加して、キットを公開し、キットIDを取得します。 アダプティブフォームで[!DNL Adobe Fonts]（Webフォント）を使用する必要があります。
1. AEM [!DNL Forms]サーバーで、![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** / **[!UICONTROL ツール]** ![ハンマー](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**&#x200B;に移動します。 次に、設定フォルダーを開きます。 設定が既に使用可能な場合は、「**[!UICONTROL 作成]**」ボタンをクリックして、新しいインスタンスを作成します。

   設定を作成ダイアログで、設定の&#x200B;**タイトル**&#x200B;を指定し、「**[!UICONTROL 作成]**」をクリックします。 設定ページにリダイレクトされます。表示される[!UICONTROL コンポーネントを編集]ダイアログで、**キットID**&#x200B;を入力し、**[!UICONTROL OK]**&#x200B;をクリックします。

1. [!DNL Adobe Fonts]設定を使用するようにテーマを設定します。 オーサーインスタンスで、テーマエディターで&#x200B;**[!UICONTROL グローバルテーマ]**&#x200B;を開きます。 テーマエディターで、**[!UICONTROL テーマオプション]** ![theme-options](assets/theme-options.png)／**[!UICONTROL 設定]**&#x200B;に移動します。「**[!UICONTROL Adobe Fonts Configuration]**」フィールドでキットを選択し、「**[!UICONTROL Save]**」をクリックします。

   **[!UICONTROL Adobe Fonts]**&#x200B;に追加されたフォントは、すべてのコンポーネントの「**[!UICONTROL テキスト]**」アコーディオンで選択できます。
