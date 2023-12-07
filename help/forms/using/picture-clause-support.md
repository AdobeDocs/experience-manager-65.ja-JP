---
title: HTML5 フォームにおけるパターン形式文字列サポート
description: HTML5 フォームでは、日付、テキスト、数値の記号の表示値と形式設定された値に対する XFA パターン形式文字列をサポートしています。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 12%

---

# HTML5 フォームにおけるパターン形式文字列サポート {#picture-clause-support-for-html-forms}

HTML5 フォームでは、日付、テキスト、数値の記号の表示値と形式設定された値に対する XFA パターン形式文字列をサポートしています。 次のパターン形式文字列の式がサポートされています。

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>現在、Mobiles Formsはパターン形式文字列の編集をサポートしていません。 また、DateTime と Time のパターン形式文字列の記号もサポートされていません。

## サポートされている日付フィールドの記号 {#supported-date-field-symbols}

日付のパターン形式文字列でサポートされる式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{ 日付のパターン形式文字列の記号 }

>[!NOTE]
>
>picture 句のデフォルトのパターンは {MMM D, YYYY} パターンです。 パターンが適用されない場合は、デフォルトのパターンが使用されます。

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th>解釈</th>
  </tr>
  <tr>
   <td>D</td>
   <td>月の日付を 1 桁または 2 桁の数値 (1 ～ 31) で表します。</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>ゼロで埋められた 2 桁の月の日 (01 ～ 31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>月を 1 桁または 2 桁の数値 (1 ～ 12) で表します。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>月を 2 桁の数値 (01 ～ 12) で表します。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>現在のロケールの月名を略して表します。<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>現在のロケールの完全な月名<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>現在のロケールの略された曜日名<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>現在のロケールの完全な平日名<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2 桁の年。00 = 2000、29 = 2029、30 = 1930、99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4 桁の年<br /> </td>
  </tr>
 </tbody>
</table>

## 数値のパターン形式文字列 {#numeric-picture-clause}

HTML5 フォームは、数値の図の記号をサポートしています。 ただし、サポートには、PDF formsとHTMLFormsの間に違いがあります。

In **PDF forms**&#x200B;の場合、Picture 句の記号数に関係なく数値が書式設定されます

In **HTMLForms**&#x200B;の場合、数値が Picture 句の記号数よりも小さい桁数の場合にのみ、数値が形式設定されます。

**例**:Picture 句 num{zzz,zzz,zz9} について考えます。

数値 **10000** 次の形式で書式設定されます： **10,000** との両方のHTMLとPDF forms。

数値1000000は、1,000,000 形式で表されます (PDF forms単位 )。 ただし、HTMLFormsでは、数値の形式は1000000のままです。

**HTML フォーム**&#x200B;においてサポートされている数値のパターン形式文字列の式は次の通りです。

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{ 数値のパターン形式文字列の記号 }

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th><strong>解釈</strong></th>
   <th>入力の解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>出力の書式設定</strong>:1 桁の数字。 または、入力データが空の場合や、対応する位置のスペースの場合は、0 桁の数値。<br /> </td>
   <td>1 桁の数値</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>出力の書式設定</strong>:1 桁の数字。 スペースの場合は、対応する位置の入力データが空、スペース、または 0 桁の場合。<br /> </td>
   <td>1 桁の数字またはスペース</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>出力の書式設定</strong>:1 桁の数字。 または、対応する位置の入力データが空、スペース、ゼロ桁の場合は何も使用しません。<br /> </td>
   <td>1 桁または何も指定しない</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>出力の書式設定</strong>：指数記号 (E) で構成される浮動小数点数の指数部分。 オプションのプラス記号またはマイナス記号が続きます。 指数値が続きます。<br /> </td>
   <td>出力の形式設定と同じ</td>
  </tr>
  <tr>
   <td>CR または cr<br /> </td>
   <td>負の数の場合はクレジット記号 (CR)。 それ以外は何もありません。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S または s<br /> </td>
   <td>出力の形式：負の数の場合はマイナス記号。 それ以外の場所。<br /> </td>
   <td>負の数の場合はマイナス記号。 正の数の場合はプラス記号</td>
  </tr>
  <tr>
   <td>V</td>
   <td>現行のロケールの小数点。 入力の解析時に小数点を暗黙化する。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>現行のロケールの小数点。 入力の解析および出力のフォーマット設定時に小数点を暗黙化する。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>現行のロケールの小数点。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>現行のロケールのグループセパレータ。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>現行のロケールの通貨記号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>現行のロケールのパーセント記号</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>負の数の場合は左括弧。 それ以外の場所。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>負の数の場合は右括弧。 それ以外の場所。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>タブ文字</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## テキストのパターン形式文字列 {#text-picture-clause}

HTML5 フォームは、以下のテキストのパターン形式文字列の式をサポートしています。

* text{テキストのパターン形式文字列の記号}

| **記号** | **解釈** |
|---|---|
| A | 英字 1 文字。 |
| X | 1 文字。 |
| O | 英数字 1 文字。 |
| 0 （ゼロ） | 英数字 1 文字。 |
| 9 | 1 桁の数値。 |
