---
title: HTML5 フォームにおけるパターン形式文字列サポート
seo-title: HTML5 フォームにおけるパターン形式文字列サポート
description: HTML5 フォームは、日付、テキスト、および数値記号の表示値と形式設定された値の XFA パターン形式文字列をサポートしています。
seo-description: HTML5 フォームは、日付、テキスト、および数値記号の表示値と形式設定された値の XFA パターン形式文字列をサポートしています。
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5 フォームにおけるパターン形式文字列サポート {#picture-clause-support-for-html-forms}

HTML5 フォームは、日付、テキスト、および数値記号の表示値と形式設定された値の XFA パターン形式文字列をサポートしています。次のパターン形式文字列の式がサポートされています。

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>現在 Mobiles Forms はパターン形式文字列の編集をサポートしていません。また、日付時刻と時刻のパターン形式文字列の記号はサポートされていません。

## サポートされている日付フィールドの記号 {#supported-date-field-symbols}

サポートされている日付のパターン形式文字列の式

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{日付のパターン形式文字列の記号}

>[!NOTE]
>
>picture clause のデフォルトパターンは {MMM D, YYYY} パターンです。パターンが適用されなかった場合は、デフォルトパターンが使用されます。

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th>解釈</th>
  </tr>
  <tr>
   <td>D</td>
   <td>1 桁または 2 桁の月の日付（1 ～ 31）</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>ゼロで埋められた 2 桁の月の日付（01 ～ 31）。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1 桁または 2 桁の年の月（1 ～ 12）<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>ゼロで埋められた 2 桁の年の月（1 ～ 12）。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>現在のロケールの略された月名<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>現在のロケールの完全な月名<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>現在のロケールの略された曜日<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>現在のロケールの完全な曜日<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2 桁の年、00 = 2000、29 = 2029、30 = 1930、および 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4 桁の月<br /> </td>
  </tr>
 </tbody>
</table>

## 数値のパターン形式文字列 {#numeric-picture-clause}

HTML5 フォームは、数値のパターン形式文字列の記号をサポートしています。ただし、PDF フォームと HTML フォームの間でサポートに違いがあります。

**PDF フォーム**&#x200B;では、パターン形式文字列の記号の数に関わらず数字が形式設定されます。

**HTML フォーム**&#x200B;では、パターン形式文字列の記号の数より数値の桁数が少ない場合のみ、数値が形式設定されます。

**例**：次のパターン形式文字列を検討します。num{zzz,zzz,zz9}。

**10000** の数値は HTML と PDF フォームの両方で **10,000** 形式設定されます。

PDF フォームでは 1000000 の数値は 1,000,000 として形式設定されます。ただし、HTML フォームではその数値は 1000000 として形式設定されていないままになります。

**HTMLフォームでサポートされる数値のパターン形式文字列の式** :

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{数値のパターン形式文字列の記号}

<table>
 <tbody>
  <tr>
   <th><strong>記号</strong></th>
   <th><strong>解釈</strong></th>
   <th>入力の解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または、対応する位置にある入力データが空またはスペースの場合は 0 で桁埋め。<br /> </td>
   <td>1 桁の数値</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または、対応する位置にある入力データが空、スペース、または 0 の桁の場合はスペース。<br /> </td>
   <td>1 桁の数値またはスペース</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>出力の形式設定</strong>：1 桁の数値。または対応する位置にある入力データが空、スペース、または 0 の桁の場合は空。<br /> </td>
   <td>1 桁の数値または空</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>出力の形式設定</strong>：指数の記号（E）から成る浮動小数点値の指数の部分。オプションのプラスまたはマイナス記号が後に続きます。指数値が後に続きます。<br /> </td>
   <td>出力の形式設定と同じ</td>
  </tr>
  <tr>
   <td>CR または cr<br /> </td>
   <td>負の数の場合は貸方記号（CR）。そうでない場合は空。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S または s<br /> </td>
   <td>出力の形式設定：負の数の場合はマイナス記号。そうでない場合はスペース。<br /> </td>
   <td>負の数の場合はマイナス記号。正の数の場合はプラス記号。</td>
  </tr>
  <tr>
   <td>V</td>
   <td>現行のロケールの小数点。入力の解析時に小数点</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>現行のロケールの小数点。入力を解析、および出力を形式設定するときに小数点を暗黙なものとします。</td>
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
   <td>負の数の場合は左括弧。そうでない場合はスペース。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>負の数の場合は右括弧。そうでない場合はスペース。</td>
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

HTML5 フォームは、次のテキストのパターン形式文字列の式をサポートしています。

* text{テキストのパターン形式文字列の記号}

| **記号** | **解釈** |
|---|---|
| A | 英字 1 文字。 |
| X | 1 文字。 |
| O | 英数字 1 文字。 |
| 0（ゼロ） | 英数字 1 文字。 |
| 9 | 1 桁の数値. |
