---
title: HTML5 フォームのための CSS スタイルの作成
seo-title: HTML5 フォームのための CSS スタイルの作成
description: HTML フォーム要素と関連付けられている CSS クラスを変更して、HTML5 フォームの外観を変更する方法について説明します。
seo-description: HTML フォーム要素と関連付けられている CSS クラスを変更して、HTML5 フォームの外観を変更する方法について説明します。
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5 フォームのための CSS スタイルの作成 {#creating-css-styles-for-html-forms}

XFA ベースのフォームテンプレートの HTML5 レンダリングは、さまざまな HTML 要素で構成されています。これらの要素は一定の順序で整列されます。すべての要素には、適切に定義された CSS クラスがあります。これらの CSS クラスを使用して、要素の外観を選択し変更することができます。

>[!NOTE]
>
>CSS クラスで、幅、高さ、境界線厚さ、上、左、右、下、パディング、マージン、およびその他の位置とサイズの属性は変更しないでください。位置とサイズの属性を変更すると、フォームのレイアウトが変わります。

## 要素の CSS クラス {#css-classes-nbsp-for-elements-nbsp}

すべての要素には、適切に定義された CSS クラスがあります。これらのクラスを変更して、要素の外観を変更することができます。フィールド要素と描画要素を除くすべての要素は、2 つの CSS クラス（Type クラスと Name クラス）を持ちます。

* **Type クラス**&#x200B;は XFA フィールドのタイプを表します。`type` クラスをオーバーライドして、特定タイプのすべての要素のスタイルを変更できます。

* **Name クラス**&#x200B;は XFA フィールドの名前に対応します。`name` クラスをオーバーライドして、スタイルを変更しカスタムスタイルを要素に適用できます。

>[!NOTE]
>
>一部の XFA 要素には名前がありません。そのようなコンポーネントのスタイルを変更するには、その特定タイプのすべてのコンポーネントを変更してください。

AEM Forms Designer で名付けられていないページでは、HTML5 フォームのページはページ番号順に名付けられます。例えば、2 ページからなる HTML5 フォームの場合、ページは Page1 および Page2 と名付けられます。

## Field 要素 {#field-element}

Field 要素にはネストされた要素が 2 つ（widget と caption）あります。

**Widget 要素**

Widget 要素にはユーザーとやりとりするためのユーザーインターフェイス要素が含まれています。CSSクラスは3つあります。

* **ウィジェット**:すべてのウィジェットにこのクラスがあります。
* **name**:AEMに付属するすべてのウィジェットには、ウィジェット名のクラスが含まれます。 カスタムウィジェットの場合、ウィジェット開発者はウィジェット名のクラスを提供します。
* **type**:すべてのウィジェットにはユーザインターフェイス要素があります。 このクラスは、ユーザーインターフェイス要素のタイプを定義します。

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

type と name クラスの他に、フィールドコンポーネントにも **subtype** という名前の追加の CSS クラスがあります。subtype はそれがどのフィールドのタイプであるかを識別します。例：NumericField、DateField、TextField。subtype クラスはオーバーライドして、subtype のタイプであるすべてのフィールドのスタイル設定を変更できます。

## 異なるコンポーネントに対する CSS クラス {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>コンポーネント</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>名前</strong></td>
  </tr>
  <tr>
   <td>ページ</td>
   <td>page</td>
   <td>ユーザー定義の名前<br />または<br />Page&lt;pageNumber&gt;（デフォルト）</td>
  </tr>
  <tr>
   <td>コンテンツ領域</td>
   <td>contentarea</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>サブフォーム</td>
   <td>サブフォーム</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>排他グループ</td>
   <td>exclgroup</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>図面</td>
   <td>draw</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>フィールド</td>
   <td>field</td>
   <td>ユーザー定義の名前</td>
  </tr>
  <tr>
   <td>キャプション</td>
   <td>caption</td>
   <td>該当なし</td>
  </tr>
  <tr>
   <td>ウィジェット</td>
   <td>widget</td>
   <td>ウィジェット開発者が定義します（ユーザー定義のウィジェットに関しては、以下のセクションの表を参照してください）</td>
  </tr>
 </tbody>
</table>

## 異なるフィールドに対する CSS クラス {#css-classes-for-different-fields}

AEM Forms Designer はフォームで NumericField、DecimalField、および Date Field などの異なるタイプのフィールドをサポートしています。HTML ですべてのこれらのフィールドには上記の CSS クラスがあります。また、それらにはフィールドのタイプによっては、いくつかの追加のクラスがあります。

すべてのフィールドには UI 要素を示す、関連するウィジェットがあります。各フィールドのクラス、および各フィールドに関連するウィジェットを以下に示します。

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
   <td>チェックボタン<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日付フィールド<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日時フィールド<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>10 進数フィールド<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>ドロップダウンリスト<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>リストボックス<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>数値フィールド<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>パスワードフィールド<br type="_moz" /> </td>
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
   <td>テキストフィールド<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>時間フィールド<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 異なる Draw 要素に対する CSS クラス {#css-classes-for-different-draw-elements}

AEM Forms Designer を使用して、テキスト、画像など、スタティックの描画要素を挿入できます。それぞれの描画要素に対し、別の CSS クラスがそれらの要素に関連しています。描画要素の CSS クラスのリストを以下に示します。それぞれの描画要素には、それに関連する draw クラスがあります。

| **描画タイプ** | **CSS クラス** |
|---|---|
| テキスト | text |
| 画像 | 画像 |
| 長方形 | rectangle |
| 線 | line |

## フォームにおける他の部分のスタイル設定 {#styling-other-parts-of-the-form}

HTMLフォームでのUIコンポーネントの外観に加え、インラインエラー、インライン警告、検証エラーのあるフィールドなどの要素のスタイルを変更できます。

`Styling Inline Errors`

フィールドの検証によりエラーが発生した場合、フィールドがアクティブのときにインラインエラーが表示されます。インラインエラーのスタイルを変更するには、CSS ID **error-msg** をオーバーライドします。

`Styling Inline Warnings`

フィールドの検証により警告が発生した場合、フィールドがアクティブのときにインライン警告が表示されます。これらのインライン警告のスタイルを変更するには、CSS ID **warning-msg** をオーバーライドします。

`Styling Fields with Validation Errors`

フィールドの検証に失敗すると、ウィジェットのスタイルが変更されます。This style change is done by applying a CSS class **widgetError** on the widget component. To modify the default styling, override the **widgetError** class.
