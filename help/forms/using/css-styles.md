---
title: HTML5 フォームのための CSS スタイルの作成
description: HTMLフォーム要素に関連付けられた CSS クラスを変更して、HTML5 フォームの外観を変更する方法を説明します。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 33%

---

# HTML5 フォームのための CSS スタイルの作成 {#creating-css-styles-for-html-forms}

XFA ベースのフォームテンプレートのHTML5 レンディションは、複数のHTML要素で構成されます。 これらの要素は、順に並べられます。 すべての要素には、適切に定義された CSS クラスがあります。 これらの CSS クラスを使用して、要素の外観を選択および変更できます。

>[!NOTE]
>
>CSS クラスで、width、height、border-thickness、top、left、right、bottom、padding、margin、およびその他の position 属性と size 属性の値を変更しないでください。 位置およびサイズの属性を変更すると、フォームのレイアウトが変更されます。

## 要素の CSS クラス  {#css-classes-nbsp-for-elements-nbsp}

すべての要素には、適切に定義された CSS クラスが含まれています。 これらのクラスを変更して、要素の外観を変更できます。 フィールド要素と描画要素を除くすべての要素は、2 つの CSS クラス（Type クラスと Name クラス）を持ちます。

* **Type クラス**&#x200B;は XFA フィールドのタイプを表します。`type` クラスをオーバーライドして、特定タイプのすべての要素のスタイルを変更できます。

* **Name クラス**&#x200B;は XFA フィールドの名前に対応します。`name` クラスをオーバーライドして、スタイルを変更しカスタムスタイルを要素に適用できます。

>[!NOTE]
>
>一部の XFA 要素には名前がありません。 このようなコンポーネントのスタイルを変更するには、その特定のタイプのすべてのコンポーネントを修正します。

AEM Forms Designer で名前が指定されていないページの場合、HTML5 フォームのページの名前は、ページ番号の増加順に付けられます。 例えば、2 ページからなる HTML5 フォームの場合、ページは Page1 および Page2 と名付けられます。

## フィールド要素 {#field-element}

field 要素には、widget と caption の 2 つのネストされた要素が含まれています。

**Widget 要素**

widget 要素には、ユーザーとやり取りするためのユーザーインターフェイス要素が含まれています。 それには 3 つの CSS クラスがあります。

* **Widget**：すべてのウィジェットにこのクラスがあります。
* **name**：AEM とともに出荷されたすべてのウィジェットにはウィジェット名のクラスがあります。カスタムウィジェットでは、ウィジェット開発者がウィジェット名のクラスを提供します。
* **type**：すべてのウィジェットにはユーザーインターフェイス要素があります。このクラスはユーザーインターフェイス要素のタイプを定義します。

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

type クラスと name クラスの他に、フィールドコンポーネントにも、という名前の追加の CSS クラスが含まれます。 **亜型**. サブタイプは、どのフィールドのタイプかを示します（例： NumericField、DateField、TextField）。 subtype クラスをオーバーライドして、subtype 型のすべてのフィールドのスタイル設定を変更できます。

## 異なるコンポーネントの CSS クラス {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>名前</strong></td>
  </tr>
  <tr>
   <td>ページ</td>
   <td>ページ</td>
   <td>ユーザー定義名<br /> または<br /> ページ&lt;pagenumber&gt; （デフォルト）</td>
  </tr>
  <tr>
   <td>コンテンツ領域</td>
   <td>contentarea</td>
   <td>ユーザー定義名</td>
  </tr>
  <tr>
   <td>サブフォーム</td>
   <td>subform</td>
   <td>ユーザー定義名</td>
  </tr>
  <tr>
   <td>除外グループ</td>
   <td>exclgroup</td>
   <td>ユーザー定義名</td>
  </tr>
  <tr>
   <td>図面</td>
   <td>draw</td>
   <td>ユーザー定義名</td>
  </tr>
  <tr>
   <td>フィールド</td>
   <td>field</td>
   <td>ユーザー定義名</td>
  </tr>
  <tr>
   <td>キャプション</td>
   <td>caption</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>ウィジェット</td>
   <td>widget</td>
   <td>ウィジェット開発者が定義します（ユーザー定義のウィジェットの場合は、次の節の表を参照してください）。</td>
  </tr>
 </tbody>
</table>

## 異なるフィールドに対する CSS クラス {#css-classes-for-different-fields}

AEM Forms Designer は、NumericField、DecimalField、Date Field など、様々な種類のフィールドをフォームでサポートしています。 HTML内のこれらのフィールドには、上記の CSS クラスがすべて含まれています。 また、フィールドのタイプに応じて、いくつかの追加のクラスが含まれます。

各フィールドには、UI 要素を表す関連ウィジェットがあります。 各フィールドのクラスと各フィールドに関連付けられたウィジェットを以下に示します。

<table>
 <tbody>
  <tr>
   <td><strong>フィールドタイプ</strong></td>
   <td><strong>サブタイプ</strong></td>
   <td><strong>ウィジェット名</strong></td>
   <td><strong>ウィジェットタイプ</strong></td>
   <td><strong>HTML UI タグ</strong></td>
  </tr>
  <tr>
   <td>ボタン<br type="_moz" /> </td>
   <td>該当なし</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>選択</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>ラジオボタン<br type="_moz" /> </td>
   <td>radiofield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>inputtype = text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 異なる Draw 要素に対する CSS クラス {#css-classes-for-different-draw-elements}

AEM Forms Designer を使用して、テキストや画像などの静的な描画要素を挿入できます。 各描画要素に対して、別々の CSS クラスがその要素に関連付けられます。 描画要素の CSS クラスのリストを以下に示します。 すべての描画要素には、それに関連付けられた描画クラスがあります。

| **描画タイプ** | **CSS クラス** |
|---|---|
| テキスト | text |
| 画像 | image |
| 長方形 | 長方形 |
| Line | 線 |

## フォームの他の部分のスタイル設定 {#styling-other-parts-of-the-form}

HTML フォームでの UI コンポーネントの外観の以外に、インラインエラー、インライン警告および検証エラーのあるフィールドなどの要素のスタイルを変更できます。

`Styling Inline Errors`

フィールドの検証でエラーが発生した場合、フィールドがアクティブなときにインラインエラーが表示されます。 インラインエラーのスタイルを変更するには、CSS ID を上書きします **error-msg**.

`Styling Inline Warnings`

フィールドの検証で警告が発生した場合、フィールドがアクティブなときはインライン警告が表示されます。 これらのインライン警告のスタイルを変更するには、CSS ID を上書きします **warning-msg**.

`Styling Fields with Validation Errors`

フィールドの検証に失敗すると、ウィジェットのスタイルが変更されます。このスタイルの変更はウィジェットコンポーネントに **widgetError **&#x200B;の CSS クラスを適用することにより実施されます。デフォルトのスタイル設定を変更するには、**widgetError** クラスをオーバーライドします。
