---
title: アダプティブフォームのスタイル設定
description: カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの web フォントの使用について説明します。
topic-tags: introduction
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 84%

---

# アダプティブフォームのスタイル設定 {#do-not-publish-style-your-adaptive-form}

カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの web フォントの使用について説明します。

![hero-image](do-not-localize/08-style_your_adaptiveformmain.png)

これは、[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## チュートリアルについて  {#about-the-tutorial}

テーマを使用すると、アダプティブフォームに独自のアピアランスやスタイルを設定できます。アダプティブフォームエディター標準のテーマを適用することも、独自のカスタムテーマを作成することもできます。AEM [!DNL Forms] はカスタムテーマを作成するための[テーマエディター](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/themes.html)を提供します。単一のテーマで、モバイル、タブレット、デスクトップで開いた同一のアダプティブフォームに異なるアピアランスを設定できます。テーマエディターを使用する場合、CSS や LESS の予備知識は特に必要ありません。

このチュートリアルを終了すると、以下の操作を実行できるようになります。

* 標準のテーマをアダプティブフォームに適用
* テーマエディターを使用して、アダプティブフォームのテーマを作成
* 個別コンポーネントのスタイル設定
* ボーナスセクション：カスタムテーマに web フォントを使用

チュートリアルを完了すると、フォームのアピアランスは以下のようになります。

![カスタムテーマが使用されているフォーム](assets/styled-adaptive-form.png)

## 事前準備 {#before-you-start}

以下に示すヘッダースタイルとロゴの画像をローカルマシンにダウンロードします。`shipping-address-add-update-form` アダプティブフォームのヘッダーは、ヘッダースタイルとロゴの画像を使用します。ヘッダースタイルの画像はヘッダーの右側に表示されます。

[ファイルを入手](assets/header-style.png)

[ファイルを入手](assets/logo-1.png)

## 手順 1：アダプティブフォームへのテーマの適用 {#step-apply-a-theme-to-your-adaptive-form}

アダプティブフォームエディターには、すぐに使用できる複数のテーマが用意されています。アダプティブフォームにカスタムスタイルを使用しない場合は、標準のテーマを使用してアダプティブフォームを公開することもできます。テーマはアダプティブフォームから独立しています。同一のテーマを複数のアダプティブフォームに適用できます。

**テーマをアダプティブフォームに適用するには、次の手順を実行します。**

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;のプロパティを開きます。プロパティブラウザーで、**[!UICONTROL 基本]**／**[!UICONTROL アダプティブフォームのテーマ]**&#x200B;に移動します。すべての初期設定済みテーマとカスタムテーマが、「**[!UICONTROL アダプティブフォームのテーマ]**」フィールドに表示されます。デフォルトではキャンバステーマが適用されます。
1. 「**[!UICONTROL アダプティブフォームのテーマ]**」フィールドでテーマを選択します（**調査のテーマ**&#x200B;など）。選択 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 選択したテーマを適用できます。

   ![デフォルトのテーマを使用したアダプティブフォーム](assets/default-adaptive-form.png)

   **図：** *デフォルトのテーマを使用したアダプティブフォーム*

   ![調査テーマを使用したアダプティブフォーム](assets/adaptive-form-with-survey-theme.png)

   **図：** *調査テーマを使用したアダプティブフォーム*

## 手順 2：アダプティブフォームの更新 {#step-update-your-adaptive-form}

上記のデザインでは、既存のアダプティブフォームのプレースホルダーテキストとロゴを変更する必要があります。

**アダプティブフォームを更新するには、次の手順を実行します。**

1. 既存のヘッダーのロゴとテキストを変更します。ロゴを削除するには、次の手順を実行します。

   1. フォームエディターでフォームを開きます。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. でロゴイメージを選択 [!UICONTROL ヘッダー] コンポーネントと選択 ![cmppr](assets/cmppr.png) **[!UICONTROL プロパティ]**. Adobe Analytics の [!UICONTROL 画像] プロパティの上にマウスポインターを置き、「X」を選択して既存のロゴイメージを削除します。
   1. 選択 **[!UICONTROL アップロード]**、logo.png を選択し、「 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をクリックして変更を保存します。 この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。
   1. ヘッダーテキストを選択します。 `We.Retail`をクリックし、次を選択します。 ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL 編集]**. ヘッダーテキストを `we retail` に変更します。太字書式を `we retail` の `we` にのみ適用します。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. タイトルを削除してプレースホルダーテキストを追加します。

   1. 「顧客 ID 」フィールドを選択し、「 」を選択します。 ![cmppr](assets/cmppr.png) プロパティ。
   1. 「**[!UICONTROL タイトル]**」フィールドの内容を「**[!UICONTROL プレースホルダーテキスト]**」フィールドにコピーします。
   1. コンテンツを削除する **[!UICONTROL タイトル]** 「 」フィールドで「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. フォーム内のすべてのテキストボックス、数値ボックス、メールフィールドで、上記の 3 つの手順を繰り返します。

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 手順 3：アダプティブフォームのカスタムテーマの作成 {#step-create-a-custom-theme-for-your-adaptive-form}

[テーマエディター](/help/forms/using/themes.md)を使用すると、カスタムテーマを作成できます。テーマエディターは非常に強力な WYSIWYG エディターです。視覚的に確認しながら、アダプティブフォームの各種コンポーネントに CSS を適用できます。アダプティブフォームのコンポーネントやパネルのスタイルを詳細に制御できます。

アダプティブフォームと同様、テーマは独立したエンティティです。アダプティブフォームのコンポーネントとパネルのスタイル（CSS）が含まれています。スタイルには背景色、状態色、透明度、配置、サイズなどの、CSS プロパティが含まれています。テーマを適用すると、指定したスタイルがアダプティブフォームの対応コンポーネントに適用されます。

このチュートリアルでは、ヘッダー、フッター、テキストコンポーネント、数値コンポーネント、添付ファイルコンポーネント、ボタンのスタイルを設定します。まずテーマを作成することから始めましょう

### テーマの作成 {#create-a-theme}

1. AEM オーサーインスタンスにログインして、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL テーマ]**&#x200B;に移動します。デフォルトの URL は [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes) です。 
1. 選択 **[!UICONTROL 作成]** を選択し、 **[!UICONTROL テーマ]**. テーマの作成が必要なフィールドを含む「[!UICONTROL テーマを作成]」ページが表示されます。「**[!UICONTROL タイトル]**」フィールドと「**[!UICONTROL 名前]**」フィールドは入力必須です。

   * **タイトル：**&#x200B;テーマのタイトルを指定します。（**グローバルテーマ**&#x200B;など）。タイトルはテーマのリストから目的のテーマを見つけるのに役立ちます
   * **名前：**&#x200B;テーマの名前を指定します。（**グローバルテーマなど）。**&#x200B;指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。

1. 「**[!UICONTROL 作成]**」を選択します。テーマが作成され、フォームを編集用に開くためのダイアログが表示されます。選択 **[!UICONTROL 開く]** をクリックして、新しく作成したテーマを新しいタブで開きます。 テーマエディターでテーマが開きます。テーマエディターでは、スタイル設定に AEM に付属している標準提供のアダプティブフォームを使用します。[!DNL Forms]

   テーマエディター UI の使用について詳しくは、[テーマエディターについて](/help/forms/using/themes.md#aboutthethemeeditor)を参照してください。

1. 選択 **[!UICONTROL テーマオプション]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 設定]**. Adobe Analytics の **[!UICONTROL フォームをプレビュー]** フィールドで、 **shipping-address-add-update-form** アダプティブフォーム、「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)を選択します。 **[!UICONTROL 保存]**. テーマエディターで、デフォルトのアダプティブフォームではなく独自のアダプティブフォームを使用できるようになります。選択 **[!UICONTROL キャンセル]** をクリックして、テーマエディターに戻ります。

   ![カスタムテーマ](assets/custom-theme.png)

   **図：** *shipping-address-add-update-form アダプティブフォームを使用したテーマエディター*

   ![テーマの作成](assets/create-a-theme.png)

   **図：** *デフォルトのフォームを使用したアダプティブフォーム*

### ヘッダーとフッターのスタイル設定 {#style-header-and-footer}

アダプティブフォームでは、ヘッダーとフッターを使用して一貫性のある外観を独自に作成できます。通常、ヘッダーには組織のロゴと名前が含まれ、フッターには著作権情報が含まれます。これらは組織の複数のフォーム間で統一されます。shipping-address-add-update-form アダプティブフォームのヘッダーとフッターのスタイルを設定するには、次の手順を実行します。

1. セレクターパネルで&#x200B;**[!UICONTROL ヘッダー]**／**[!UICONTROL テキスト]**&#x200B;オプションに移動します。セレクターパネルはテーマエディターの左側にあります。パネルが表示されない場合は、「 ![toggle-side-panel](assets/toggle-side-panel.png) サイドパネルを切り替えます。

1. 次のプロパティを **[!UICONTROL テキスト]** アコーディオンと選択 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | プロパティ | 値 |
   |---|---|
   | フォントファミリー | Arial® |
   | フォントカラー | FFFFFF |
   | フォントサイズ | 54 px |

1. を選択します。 [!UICONTROL ヘッダー] ウィジェットと選択 **[!UICONTROL ヘッダー]**. ヘッダーウィジェットのスタイルを設定するオプションが左側に表示されます。を展開します。 **[!UICONTROL Dimensionと位置]** アコーディオン、 **[!UICONTROL 高さ]** から `120px`をクリックし、次を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. ヘッダーウィジェットの「**[!UICONTROL 背景]**」アコーディオンを展開し、「**[!UICONTROL 背景色]**」を「`F6921E.`」に設定します。

   カーソルを合わせる **[!UICONTROL 画像とグラデーション]** > **[!UICONTROL +追加]**&#x200B;を選択します。 **[!UICONTROL 画像]**. 次のプロパティを設定し、「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | プロパティ | 値 |
   |---|---|
   | 画像 | header-style.png をアップロードします。この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。 |
   | 位置 | 右下 |
   | タイリング | 繰り返しなし |

1. テーマエディターで、ヘッダーのロゴを選択し、「 」をクリックします。 **[!UICONTROL ヘッダーロゴ]**. 「Dimensionと位置」アコーディオンを展開し、次のプロパティを設定して、「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
        <li>上：1.5 rem</li> 
        <li>下：-35 px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>ヒント：</strong> を選択します。 <img src="assets/link.png"> リンクアイコンを使用して、各フィールドに異なる値を指定します。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高さ</td> 
      <td>4.75 rem</td> 
     </tr> 
    </tbody> 
   </table>

1. フッターウィジェットを選択し、「 」を選択します。 **[!UICONTROL フッター]**. を展開します。 **[!UICONTROL 背景]** アコーディオン、 **[!UICONTROL 背景色]** から `F6921E`をクリックし、次を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### データ取得コンポーネントのスタイル設定とアダプティブフォームの背景の適用 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

アダプティブフォームでは複数のコンポーネントを使用してデータを取得できます。例えば、テキストボックスや数値ボックスなどです。すべてのデータ取得コンポーネントに同じスタイルを設定することも、コンポーネントごとに異なるスタイルを設定することもできます。このチュートリアルでは、数値ボックス（顧客 ID、郵便番号）とテキストボックス（顧客 ID、名前、発送先住所、状態、メール）に同じスタイルを適用します。データ取得コンポーネントのスタイルを設定するには、次の手順を実行します。

1. を選択します。 **[!UICONTROL 顧客 ID]** フィールドに値を入力し、 **[!UICONTROL フィールドウィジェット]** オプション。 次のプロパティを設定し、「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
      <td>Arial®</td> 
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
        <li>左：10 rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 上の空の領域を選択 **[!UICONTROL 顧客 ID]** 「 」フィールドで「 」を選択します。 **[!UICONTROL レスポンシブパネルコンテナ]**. **[!UICONTROL 背景]**／**[!UICONTROL 背景色]**&#x200B;を F1F2F2 に設定します。選択 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![レスポンシブパネルコンテナ](do-not-localize/responsive-panel-container.png)

### ボタンのスタイル設定 {#style-the-buttons}

カスタムテーマを使用すると、アダプティブフォームのすべてのボタンに同じスタイルを適用することも、特定のボタンに[インラインスタイル設定](/help/forms/using/inline-style-adaptive-forms.md)を適用することもできます。ボタンのスタイルを設定するには、次の手順を実行します。

1. を選択します。 **[!UICONTROL 送信]** ボタンをクリックし、 **[!UICONTROL ボタン]** オプション。 次のプロパティを設定し、「 」を選択します。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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
      <td>Arial®</td> 
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

1. アダプティブフォームに[カスタムテーマを適用](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)するか、グローバルテーマを適用します。スタイルがアダプティブフォームに反映されない場合は、ブラウザーのキャッシュを削除した後、もう一度実行してください。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 手順 4：個別コンポーネントのスタイル設定 {#step-style-individual-components}

一部のスタイルは特定のコンポーネントのみに適用されます。このようなコンポーネントのスタイルは、アダプティブフォームエディターで設定します。

1. アダプティブフォームを編集用に開きます。[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 上部バーで「**[!UICONTROL スタイル]**」オプションを選択します。

   ![style-option](assets/style-option.png)

1. を選択します。 **[!UICONTROL 添付]** ボタンをクリックし、 ![aem_6_3_edit](assets/aem_6_3_edit.png)アイコン。 「**[!UICONTROL 寸法と位置]**」アコーディオンで以下のプロパティを設定します。

   | プロパティ | 値 |
   |---|---|
   | 浮動小数点数 | 左 |
   | 幅 | 10% |

1. を選択します。 **[!UICONTROL 政府が承認した住所の配達確認]** オプションを選択し、 ![aem_6_3_edit](assets/aem_6_3_edit.png)アイコン。 次のプロパティを設定します。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>浮動小数点数</td> 
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
        <li>右：2 rem</li> 
        <li>左：10 rem </li> 
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
      <td>Arial®</td> 
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

1. を選択します。 **[!UICONTROL 送信]** ボタンをクリックし、 ![aem_6_3_edit](assets/aem_6_3_edit.png) アイコン。 次のプロパティを設定します。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>浮動小数点数</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>余白</td> 
      <td> 
       <ul> 
        <li>上：5 rem</li> 
        <li>右：14 rem</li> 
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

## 手順 5：オプション：カスタムテーマでの web フォントの使用 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

アダプティブフォームは各種フォントを使用してデザインできます。アダプティブフォームのデザインに使用するフォントが、アダプティブフォームを表示するデバイスに存在しない場合があります。Web フォントサービスを使用すると、必要なフォントを目的のデバイスで使用できます。

[!DNL Adobe Fonts] は web フォントサービスです。アダプティブフォームでこのサービスを設定、使用できます。[!DNL Adobe Fonts] をアダプティブフォームで使用するには：

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] の現在の名称は Adobe Fonts であり、Creative Cloud や他のサブスクリプションサービスに含まれています。[詳細情報](https://fonts.adobe.com/)を参照してください。

1. [Adobe Fonts](https://fonts.adobe.com/?ref=tk.com) アカウントを作成し、キットを作成します。次に、Myriad Pro フォントをキットに追加してキットを発行し、キット ID を取得します。アダプティブフォームでは [!DNL Adobe Fonts]（web フォント）を使用する必要があります。
1. AEM [!DNL Forms] サーバーで、![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL Adobe Fonts]** に移動します。次に、設定フォルダーを開きます。既に設定が使用可能な場合は、「**[!UICONTROL 作成]**」ボタンをクリックしてインスタンスを作成します。

   設定を作成ダイアログで、新しい設定の「**タイトル**」を指定し、「**[!UICONTROL 作成]**」をクリックします。設定ページにリダイレクトされます。[!UICONTROL コンポーネントを編集]ダイアログが表示されるので、**キット ID** を入力して「**[!UICONTROL OK]**」をクリックします。

1. [!DNL Adobe Fonts] 設定を使用するようにテーマを設定します。オーサーインスタンスで、テーマエディターを使用して「**[!UICONTROL グローバルテーマ]**」を開きます。テーマエディターで、**[!UICONTROL テーマオプション]** ![theme-options](assets/theme-options.png)／**[!UICONTROL 設定]**&#x200B;に移動します。「**[!UICONTROL Adobe Fonts 設定]**」フィールドで、キットを選択して「**[!UICONTROL 保存]**」をクリックします。

   **[!UICONTROL Adobe Fonts]** に追加したフォントは、すべてのコンポーネントの「**[!UICONTROL テキスト]**」アコーディオンで選択できます。
