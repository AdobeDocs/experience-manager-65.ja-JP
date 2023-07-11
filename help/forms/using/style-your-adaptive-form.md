---
title: アダプティブフォームのスタイル設定
seo-title: Style your adaptive form
description: カスタムテーマの作成、個々のコンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 67%

---

# アダプティブフォームのスタイル設定 {#do-not-publish-style-your-adaptive-form}

カスタムテーマの作成、個々のコンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します

![hero-image](do-not-localize/08-style_your_adaptiveformmain.png)

これは、[最初のアダプティブフォームを作成する](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)シリーズを構成するチュートリアルです。チュートリアルの使用例全体を理解、実行、デモするために、シリーズを時系列に沿って実施することをお勧めします。

## チュートリアルについて  {#about-the-tutorial}

テーマを使用して、アダプティブフォームに独自の外観とスタイルを設定することができます。 アダプティブフォームエディターに付属している標準のテーマを適用することも、独自のカスタムテーマを作成することもできます。 AEM [!DNL Forms] はカスタムテーマを作成するための[テーマエディター](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/themes.html)を提供します。1 つのテーマで、モバイル、タブレット、デスクトップで開いた同じアダプティブフォームに異なる外観を提供できます。 CSS または LESS に関する事前の知識は、テーマエディターを使用する必要はありませんが、これは必須です。

このチュートリアルを最後まで学習すると、次の内容を習得できます。

* 標準搭載のテーマをアダプティブフォームに適用する
* テーマエディターを使用してアダプティブフォームのテーマを作成する
* 個々のコンポーネントのスタイル設定
* ボーナスセクション：カスタムテーマでの Web フォントの使用

このチュートリアルを完了すると、フォームは次のようになります。

![カスタムテーマが使用されているフォーム](assets/styled-adaptive-form.png)

## 事前準備 {#before-you-start}

以下に示すヘッダースタイルとロゴの画像をローカルマシンにダウンロードします。 `shipping-address-add-update-form` アダプティブフォームのヘッダーは、ヘッダースタイルとロゴの画像を使用します。ヘッダースタイルの画像はヘッダーの右側に表示されます。

[ファイルを入手](assets/header-style.png)

[ファイルを入手](assets/logo-1.png)

## 手順 1:アダプティブフォームにテーマを適用する {#step-apply-a-theme-to-your-adaptive-form}

アダプティブフォームエディターには、すぐに使用できる複数のテーマが用意されています。 アダプティブフォームでカスタムスタイルを使用しない場合は、標準のテーマを持つアダプティブフォームを発行することもできます。 テーマはアダプティブフォームとは独立しています。 同じテーマを複数のアダプティブフォームに適用することができます。 テーマをアダプティブフォームに適用するには：

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. のプロパティを開く **[!UICONTROL アダプティブフォームコンテナ]**. プロパティブラウザーで、に移動します。 **[!UICONTROL 基本]** > **[!UICONTROL アダプティブフォームのテーマ]**. すべての初期設定済みテーマとカスタムテーマが、「**[!UICONTROL アダプティブフォームのテーマ]**」フィールドに表示されます。デフォルトではキャンバステーマが適用されます。
1. テーマを **[!UICONTROL アダプティブフォームのテーマ]** フィールドに入力します。 例： **調査テーマ**. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップして、選択したテーマを適用します。

   ![デフォルトのテーマを使用したアダプティブフォーム](assets/default-adaptive-form.png)

   **図：** *デフォルトのテーマを使用したアダプティブフォーム*

   ![調査テーマを使用したアダプティブフォーム](assets/adaptive-form-with-survey-theme.png)

   **図：** *調査テーマを使用したアダプティブフォーム*

## 手順 2:アダプティブフォームの更新 {#step-update-your-adaptive-form}

上記のデザインでは、既存のアダプティブフォームのプレースホルダーテキストとロゴを変更する必要があります。 必要な変更を行うには、次の手順を実行します。

1. ヘッダーの既存のロゴおよびテキストを変更します。 ロゴを削除するには：

   1. フォームをフォームエディターで開きます。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. [!UICONTROL ヘッダー]コンポーネントでロゴの画像をタップし、![cmppr](assets/cmppr.png) 「**[!UICONTROL プロパティ]**」をタップします。[!UICONTROL 画像]のプロパティで X をタップし、既存のロゴの画像を削除します。
   1. 「**[!UICONTROL アップロード]**」をタップして、logo.png を選択し、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップして変更を保存します。この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。
   1. ヘッダーテキスト `We.Retail` をタップしてから、 ![aem_6_3_edit](assets/aem_6_3_edit.png) 「**[!UICONTROL 編集]**」をタップします。ヘッダーテキストを `we retail` に変更します。太字書式を `we retail` の `we` にのみ適用します。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. タイトルを削除してプレースホルダーテキストを追加します。

   1. 「顧客 ID」フィールドをタップし、![cmppr](assets/cmppr.png)「プロパティ」をタップします。
   1. 「**[!UICONTROL タイトル]**」フィールドの内容を「**[!UICONTROL プレースホルダーテキスト]**」フィールドにコピーします。
   1. 「**[!UICONTROL タイトル]**」 フィールドのコンテンツを削除して、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップします。
   1. フォーム内のすべてのテキストボックス、数値ボックス、メールフィールドで、上記の 3 つの手順を繰り返します。

      ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 手順 3:アダプティブフォームのカスタムテーマの作成 {#step-create-a-custom-theme-for-your-adaptive-form}

以下を使用できます。 [テーマエディター](/help/forms/using/themes.md) をクリックしてカスタムテーマを作成します。 テーマエディターは、WYSIWYG の全機能を備えたエディターです。 これは、アダプティブフォームの様々なコンポーネントに CSS を適用する視覚的な方法です。 アダプティブフォームのコンポーネントやパネルのスタイルをより細かく制御できます。

テーマは、アダプティブフォームと同様、個別のエンティティです。 アダプティブフォームのコンポーネントやパネルのスタイル (CSS) が含まれています。 スタイルには、背景色、状態色、透明度、整列、サイズなどの CSS プロパティが含まれます。 テーマを適用すると、指定したスタイルがアダプティブフォームの対応するコンポーネントに適用されます。

このチュートリアルでは、ヘッダーとフッター、テキストと数値のコンポーネント、添付ファイルコンポーネント、ボタンのスタイルを設定します。 まずテーマを作成することから始めましょう。

### テーマの作成 {#create-a-theme}

1. AEM オーサーインスタンスにログインして、**[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL Forms]**／**[!UICONTROL テーマ]**&#x200B;に移動します。デフォルトの URL は [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes) です。 
1. 「**[!UICONTROL 作成]**」をタップし、「**[!UICONTROL テーマ]**」を選択します。テーマの作成が必要なフィールドを含む「[!UICONTROL テーマを作成]」ページが表示されます。「**[!UICONTROL タイトル]**」フィールドと「**[!UICONTROL 名前]**」フィールドは入力必須です。

   * **タイトル：**&#x200B;テーマのタイトルを指定します。例： **グローバルテーマ。** タイトルを指定すると、テーマのリストからテーマを特定しやすくなります。
   * **名前：**&#x200B;テーマの名前を指定します。例： **グローバルテーマ**&#x200B;指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。

1. 「**[!UICONTROL 作成]**」をタップします。テーマが作成され、フォームを編集用に開くためのダイアログが表示されます。「**[!UICONTROL 開く]**」をタップし、新規作成されたテーマを新しいタブで開きます。テーマがテーマエディターで開きます。スタイル設定には、AEM に付属している標準提供のアダプティブフォームがテーマエディターにより使用されます。[!DNL Forms]

   テーマエディター UI の使用について詳しくは、「[テーマエディターについて](/help/forms/using/themes.md#aboutthethemeeditor)」を参照してください。

1. **[!UICONTROL テーマオプション]** ![theme-options](assets/theme-options.png)／**[!UICONTROL 設定]**&#x200B;をタップします。「**[!UICONTROL フォームのプレビュー]**」フィールドで **shipping-address-add-update-form** アダプティブフォームを選択し、 「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」、「 **[!UICONTROL 保存]**」の順にタップします。テーマエディターで、デフォルトのアダプティブフォームではなく独自のアダプティブフォームを使用できるようになります。テーマエディターに戻るには、「**[!UICONTROL キャンセル]**」をタップします。

   ![カスタムテーマ](assets/custom-theme.png)

   **図：** *shipping-address-add-update-form アダプティブフォームを使用したテーマエディター*

   ![テーマの作成](assets/create-a-theme.png)

   **図：** *デフォルトのフォームを使用したアダプティブフォーム*

### ヘッダーとフッターのスタイル設定 {#style-header-and-footer}

ヘッダーとフッターを使用すると、アダプティブフォームの外観が一貫して独特になります。 通常、ヘッダーには組織のロゴと名前が含まれ、フッターには著作権情報が含まれます。また、これらは組織の複数の形式で同じままです。 shipping-address-add-update-form アダプティブフォームのヘッダーとフッターのスタイルを設定するには、次の手順を実行します。

1. 次に移動： **[!UICONTROL ヘッダー]** > **[!UICONTROL テキスト]** 」オプションが表示されます。 セレクターパネルは、テーマエディターの左側に表示されます。 パネルが表示されない場合は、「 ![サイドパネルを切り替え](assets/toggle-side-panel.png)」をタップします。

1. 「**[!UICONTROL テキスト]**」アコーディオンで以下のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   | プロパティ | 値 |
   |---|---|
   | フォントファミリー | Arial |
   | フォントカラー | FFFFFF |
   | フォントサイズ | 54 px |

1. [!UICONTROL ヘッダー]ウィジェットをタップし、「**[!UICONTROL ヘッダー]**」をタップします。ヘッダーウィジェットのスタイルを設定するオプションが左側に表示されます。「**[!UICONTROL 寸法と位置]**」アコーディオンを展開し、「**[!UICONTROL 高さ]** 」を `120px`に設定して、 「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。
1. ヘッダーウィジェットの「**[!UICONTROL 背景]**」アコーディオンを展開し、「**[!UICONTROL 背景色]**」を「`F6921E.`」に設定します。

   **[!UICONTROL 画像とグラデーション]**／**[!UICONTROL + 追加]**&#x200B;にポインターを合わせ、 「**[!UICONTROL 画像]**」をタップします。以下のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   | プロパティ | 値 |
   |---|---|
   | 画像 | header-style.png をアップロードします。 この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。 |
   | 位置 | 右下 |
   | タイル | 繰り返しなし |

1. テーマエディターで、ヘッダーのロゴをタップし、「**[!UICONTROL ヘッダーロゴ]**」をタップします。「寸法と位置」アコーディオンを展開し、次のプロパティを設定して、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

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
        <li>下：-35px</li> 
        <li>左：1rem<strong><br /> </strong></li> 
       </ul> <p><strong>ヒント：</strong> フィールドごとに異なる値を設定するには、<img src="assets/link.png"> リンクアイコンをタップします。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高さ</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. フッターウィジェットをタップし、「**[!UICONTROL フッター]**」をタップします。「**[!UICONTROL 背景]**」アコーディオンを展開し、「**[!UICONTROL 背景色]**」を「`F6921E` 」に設定して、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

### データ取得コンポーネントのスタイルを設定し、アダプティブフォームに背景を適用する {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

アダプティブフォーム内の複数のコンポーネントを使用して、データを取り込むことができます。 例えば、テキストボックスや数値ボックスなどです。 すべてのデータ取得コンポーネントに同じスタイルを設定することも、コンポーネントごとに異なるスタイルを設定することもできます。このチュートリアルでは、数値ボックス（顧客 ID、郵便番号）とテキストボックス（顧客 ID、名前、発送先住所、状態、メール）に同じスタイルを適用します。データ取得コンポーネントのスタイルを設定するには、次の手順を実行します。

1. 「**[!UICONTROL 顧客 ID]**」フィールドをタップし、「**[!UICONTROL フィールドウィジェット]**」オプションをタップします。次のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   <table> 
    <tbody> 
     <tr> 
      <td><b>アコーディオン</b></td> 
      <td><b>プロパティ</b></td> 
      <td><b>値</b></td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>枠色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の半径 </td> 
      <td> 
       <ul> 
        <li>上：7px<br /> </li> 
        <li>右：7px<br /> </li> 
        <li>下：7px<br /> </li> 
        <li>左：7px<br /> </li> 
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

1. 「**[!UICONTROL 顧客 ID]**」フィールドの上部で空白領域をタップし、「**[!UICONTROL レスポンシブパネルコンテナ]**」をタップします。**[!UICONTROL 背景]**／**[!UICONTROL 背景色]**&#x200B;を F1F2F2 に設定します。「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   ![](do-not-localize/responsive-panel-container.png)

### ボタンのスタイル設定 {#style-the-buttons}

カスタムテーマを使用すると、アダプティブフォームのすべてのボタンに同じスタイルを適用することも、特定のボタンに[インラインスタイル設定](/help/forms/using/inline-style-adaptive-forms.md)を適用することもできます。ボタンのスタイルを設定するには、次の手順を実行します。

1. 「**[!UICONTROL 送信]**」ボタンをタップし、「**[!UICONTROL ボタン]**」オプションをタップします。次のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

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
      <td>枠色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>境界線の半径 </td> 
      <td> 
       <ul> 
        <li>上：7px<br /> </li> 
        <li>右：7px<br /> </li> 
        <li>下：7px<br /> </li> 
        <li>左：7px</li> 
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

1. [カスタムテーマの適用](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)、グローバルテーマをアダプティブフォームに適用します。 スタイルがアダプティブフォームに反映されない場合は、ブラウザーのキャッシュを削除した後、もう一度実行してください。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 手順 4:個々のコンポーネントのスタイル設定 {#step-style-individual-components}

一部のスタイルは、特定のコンポーネントにのみ適用されます。 このようなコンポーネントは、アダプティブフォームエディターでスタイル設定されます。

1. アダプティブフォームを編集用に開きます。[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 上部バーで「**[!UICONTROL スタイル]**」オプションを選択します。

   ![style-option](assets/style-option.png)

1. 「**[!UICONTROL 添付]**」ボタンをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。「**[!UICONTROL 寸法と位置]**」アコーディオンで以下のプロパティを設定します。

   | プロパティ | 値 |
   |---|---|
   | 浮動小数 | Left |
   | 幅 | 10% |

1. 「**[!UICONTROL Government approved address proof]**」オプションをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。次のプロパティを設定します。

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
      <td>Left</td> 
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
        <li>左：10px</li> 
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
      <td>枠色</td> 
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

1. 「**[!UICONTROL 送信]**」ボタンをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。次のプロパティを設定します。

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
      <td>右</td> 
     </tr> 
     <tr> 
      <td>寸法と位置</td> 
      <td>余白</td> 
      <td> 
       <ul> 
        <li>上：5rem</li> 
        <li>右：14rem</li> 
        <li>下：20px</li> 
        <li>左：20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>境界線</td> 
      <td>枠色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 手順 5:ボーナスセクション：カスタムテーマでの Web フォントの使用 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

様々なフォントを使用して、アダプティブフォームをデザインすることができます。 アダプティブフォームが表示されるすべてのデバイスに、アダプティブフォームのデザインに使用されるフォントがない場合があります。 Web フォントサービスを使用すると、必要なフォントを目的のデバイスで使用できます。

[!DNL Adobe Fonts] は web フォントサービスです。アダプティブフォームでこのサービスを設定、使用できます。[!DNL Adobe Fonts] をアダプティブフォームで使用するには：

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] の現在の名称は Adobe Fonts であり、Creative Cloud や他のサブスクリプションサービスに含まれています。[詳細情報](https://fonts.adobe.com/)を参照してください。

1. [Adobe Fonts](https://typekit.com/) アカウントを作成し、キットを作成します。次に、Myriad Pro フォントをキットに追加してキットを発行し、キット ID を取得します。アダプティブフォームでは [!DNL Adobe Fonts]（web フォント）を使用する必要があります。
1. AEM [!DNL Forms] サーバーで、![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]**／**[!UICONTROL ツール]** ![ハンマー](assets/hammer.png)／**[!UICONTROL Adobe Fonts]** に移動します。次に、設定フォルダーを開きます。既に設定が使用可能な場合は、「**[!UICONTROL 作成]**」ボタンをクリックして新しいインスタンスを作成します。

   設定を作成ダイアログで、新しい設定の「**タイトル**」を指定し、「**[!UICONTROL 作成]**」をクリックします。設定ページにリダイレクトされます。[!UICONTROL コンポーネントを編集]ダイアログが表示されるので、**キット ID** を入力して「**[!UICONTROL OK]**」をクリックします。

1. [!DNL Adobe Fonts] 設定を使用するようにテーマを設定します。オーサーインスタンスで、テーマエディターを使用して「**[!UICONTROL グローバルテーマ]**」を開きます。テーマエディターで、**[!UICONTROL テーマオプション]** ![theme-options](assets/theme-options.png)／**[!UICONTROL 設定]**&#x200B;に移動します。「**[!UICONTROL Adobe Fonts 設定]**」フィールドで、キットを選択して「**[!UICONTROL 保存]**」をクリックします。

   **[!UICONTROL Adobe Fonts]** に追加したフォントは、すべてのコンポーネントの「**[!UICONTROL テキスト]**」アコーディオンで選択できます。
