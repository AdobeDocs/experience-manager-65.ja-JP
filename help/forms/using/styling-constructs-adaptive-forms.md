---
title: アダプティブフォームのスタイル構成
seo-title: アダプティブフォームのスタイル構成
description: LESS フレームワークを使用して、アダプティブフォームの外観をカスタマイズすることができます。
seo-description: LESS フレームワークを使用したアダプティブフォームの外観のカスタマイズ
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 87%

---


# アダプティブフォームのスタイル設定構成{#styling-constructs-for-adaptive-forms}

## 前提条件 {#prerequisites}

CSS と LESS フレームワークに関する知識が必要になります。

## カスタマイズの対象 {#what-can-be-customized}

この記事では、公開されているアダプティブフォームの CSS クラスについて説明します。これらのクラスを活用して、アダプティブフォームの様々なコンポーネントのスタイルを設定できます。 警告を表示するダイアログやステータスバーなど、オーサリングコンポーネントのスタイル設定については、ここでは説明しません。[テーマエディター](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/themes.html)を使用してコンポーネントのスタイル設定ができない場合にのみ、これらのスタイル構造を使用してスタイル（CSS または Less）を作成してください。

## アダプティブフォームでのスタイルのカスタマイズ {#customizing-styles-in-adaptive-forms}

LESS フレームワークにより、アダプティブフォームでのスタイルのカスタマイズを簡単に行うことができます。フレームワークでは、変数や関数のセット（ミックスイン）を使用したスタイルの定義が可能です。LESS フレームワークにより、バンドルされているコードをのサイズを減らし、コードの再利用率を高めることができます。

アダプティブフォームのスタイルは、次の方法でカスタマイズすることができます。

* テーマを変更する
* コンポーネントのスタイルを変更する

## テーマを変更する {#changing-theme}

アダプティブフォームのテーマを変更して、アダプティブフォームが埋め込まれたWebページと外観が一致するようにすることができます。

テーマの変更は通常、アダプティブフォームの全体的な外観をCSS プロパティを使用して変更することにより行われます。コンポーネントのレイアウトや配置の変更など、アダプティブフォームのログ&quot;OK&amp;FEEL&quot;に対する大きな変更は、テーマの変更とは見なされません。

Web ページのテーマは、ブートストラップに基づき、次の CSS プロパティによって定義されます。

* 背景色
* ボーダー（種類、色、太さ）
* フォントカラー
* パディング
* の余白
* フォントサイズ
* 行の高さ

現在、LESS 変数は、アダプティブフォームのさまざまな要素のこれらのプロパティに対してのみ定義されています。

## コンポーネントスタイルの変更 {#changing-component-style}

要素の外観、レイアウト、配置、可視性を変更することができます。このタスクを実現するには、この記事に示すスタイル設定構成を含めるカスタム.cssファイルを作成または更新します。

アダプティブフォームにスタイルを適用するには、編集用としてアダプティブフォームを開き、アダプティブフォームコンテナのプロパティを開いて、「基本」タブでカスタム .css ファイルのパスを指定します。アダプティブフォームのデフォルトのスタイル構成は、カスタムの .css ファイル内の構成によって上書きされます。

## コンポーネント {#components}

この記事で説明されているコンポーネントには、CSS クラスが事前に定義されています。変数を編集することにより、CSS クラスでスタイルを変更することができます。または、クラス全体を書き直すこともできます。このセクションでは、変数を使って変更できるコンポーネントとスタイル内のクラスを説明します。

## コンテナのスタイル設定 {#container-styling}

コンテナは、トップレベルのコンポーネントです。 他のパネルおよびフィールドは、コンテナコンポーネントの下に位置しています。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数の説明</strong></p> </td>
   <td><p><strong>変数の説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>コンテナの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>コンテナのパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>コンテナの余白</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>コンテナのフォントカラー</p> </td>
  </tr>
 </tbody>
</table>

## フィールドのスタイル設定 {#field-styling}

アダプティブフォームには、さまざまなタイプのフィールドが含まれています。各フィールドにはユニークなクラス名があり、それがフィールドの名前となっています。The field also has a common class name `guideFieldNode`.

フィールドには、ラベル、ウィジェット、ヘルプの説明（詳細な説明および短い説明の両方）、フィールドヘルプアイコン（クエスチョンマーク）が含まれています。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>フィールドのパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>フィールドのエラーメッセージのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>フィールドのエラーメッセージのフォントサイズ</p> </td>
  </tr>
 </tbody>
</table>

## ラベルのスタイル設定 {#label-styling}

The HTML element **label** used for the field includes the classes **left** or **top** depending on whether the label is at the top or left.

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>フィールドラベルのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>フィールドラベルのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>フィールドラベルに対するCSSの行の高さのプロパティ </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>フィールドラベルに対するCSSフォント重み付けプロパティ </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>フィールドラベルの余白</p> </td>
  </tr>
 </tbody>
</table>

The CSS rules for the label are applied using the **guideFieldLabel** label. カスタム変更を見えるようにするには、作成者がこのルールを上書きする必要があります。

## ウィジェットのスタイル設定 {#widgets-styling}

タイプによっては、ウィジェットにもクラスが含まれています。一般的に、ウィジェットには `guideFieldWidget` クラスが含まれています。HTML に付属のウィジェットは通常、標準の HTML 要素 input と select を使用しています。スタイル設定は、それに応じて行われます。変数を変更することによって、カスタムウィジェットのスタイル設定を行うことはできません。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 <code></code></strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>ウィジェットの背景色（チェックボックスとラジオボタンには適用されません）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>ウィジェットのボーダーのカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>ウィジェットのボーダーのサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>ウィジェットのボーダーの半径</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>ウィジェットのボーダーのタイプ</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>ウィジェットのボーダーのフォーカスタイプ</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>ウィジェットのボーダーの統合されたスタイル</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>ウィジェットの中のテキストの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>ウィジェットの中のテキストのサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>ウィジェットのCSS行の高さのプロパティ </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>ウィジェットに対する CSS のパディングのプロパティ</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>ウィジェットがフォーカスされたときのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>必須フィールドのウィジェットのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必須フィールドのウィジェットの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>フィールドが無効になっているときのウィジェットの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>フィールドが無効になっているときのウィジェットのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>フィールドが無効になっているときのウィジェットのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>ウィジェットの高さ（チェックボックスとラジオボタンには適用されません）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>チェックボックスおよびラジオボタンの高さ</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>複数選択のドロップダウンの最大の高さ</p> </td>
  </tr>
 </tbody>
</table>

### ウィジェットのスタイル設定における制限事項 {#limitations-in-widget-styling}

変数を使用したフォーカス時、必須、無効フィールドのスタイル設定には制限があります。ただし、スタイルをオーバーライドすることにより変更することができます。変数の使用における制限は、主に変数の数を抑えるために設けられています。制限は、フィールドの外観が大幅に変化する場合に緩和できます。これは、フィールドが前述の状態のいずれかにあるためです。

## ヘルプの説明 {#help-description}

作成者は、短い説明と詳細な説明のコンポーネントを使用することにより、ヘルプコンテンツを指定することができます。Both components have a common class `.guideHelpDescription` and another class `.long`/ `.short`, depending on the type of description. ヘルプコンテンツは、説明のスタイル設定をオーバーライドする段落要素で囲まれています。ヘルプの説明（詳細な説明と短い説明の両方）は、次の表で説明されるとおり、widgetshelp で始まる変数を使用して変更されます。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>ウィジェットの詳細なヘルプの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>ウィジェットの詳細なヘルプのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>ウィジェットの詳細なヘルプの左のインジケーターのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>ウィジェットの短いヘルプの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>ウィジェットの短いヘルプのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>ウィジェットの短いツールヒントのヘルプの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>ウィジェットの短いツールヒントのヘルプのフォントカラー</p> </td>
  </tr>
 </tbody>
</table>

## 利用条件 {#terms-and-conditions}

利用条件 (TnC`` ``) ウィジェットでは、利用条件を指定することができます。このウィジェットは、次の表で説明する変数を使ってカスタマイズすることができます。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>未訪問の TnC リンクのフォントカラー</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>訪問済みの TnC リンクのフォントカラー</td>
  </tr>
 </tbody>
</table>

## ボタン {#button}

ボタンもウィジェットのひとつです。ただし、そのスタイル設定はウィジェットとは多少異なります。アダプティブフォームでは、次のいずれかを含んでいればボタンと見なされます。

* [inputtype = text]
* button
* .button のクラスを持つ要素

ボタンの HTML コード

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>ボタンのアイコンを指定します</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>ボタンのラベルまたはキャプションのスタイルを設定します</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 <code></code></strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>ボタンのボーダーのサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>ボーダーのタイプ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>ボタンに対する CSS のパディングのプロパティ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>ボタンのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>ボタンの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>ボタンのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>ボタンのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>大きいボタン（.buttonlarge クラスを持ったボタン）のパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大きいボタンのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小さいボタン（.buttonsmall クラスを持ったボタン）のパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小さいボタンのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>情報ボタン（.buttoninformative クラスを持ったボタン）の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>情報ボタンのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>情報ボタンのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告スタイルのボタン（.buttonwarning クラスを持ったボタン）の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告スタイルのボタンのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告スタイルのボタンのボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>通知ボタン（.buttonalert クラスを持ったボタン）の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>通知ボタンのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>通知ボタンのボーダーの色</p> </td>
  </tr>
 </tbody>
</table>

## 疑問符 {#question-mark}

ウィジェットでは、ヘルプコンテンツで詳細な説明が追加されたときに疑問符が表示されます。ブートストラップで指定されているデフォルトのアイコンが使用されます。カスタムアイコンを使用したい場合には、ブートストラップのアイコンをカスタマイズすることができます。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>アイコンの色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>カーソルをアイコンの上に移動させたときのアイコンの色</p> </td>
  </tr>
 </tbody>
</table>

## テーブル {#table}

テーブル内のヘッダーおよびボディ行のカラーテーマは、次の変数を使用して変更することができます。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>ヘッダー行の背景色The default value is <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>奇数のボディ行の背景色デフォルト値は <code>rgb(255, 255, 255)</code> です。</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶数のボディ行の背景色デフォルト値は <code>#eee</code> です。</p> </td>
  </tr>
 </tbody>
</table>

## 添付ファイル {#file-attachment}

アダプティブフォームの添付ファイルウィジェットでは、ファイルをアップロードすることができます。変数を使ってウィジェットをカスタマイズすることもできます。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>ウィジェットに表示されるファイルのパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>ファイルアイテムの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>上のボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>ファイルアイテムのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>ウィジェットのプレビューアイコン（ブートストラップのアイコン）の色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>ファイルアイテムのコメントの高さ</p> </td>
  </tr>
 </tbody>
</table>

## ナビゲーターのスタイル {#navigator-styles}

ナビゲータータブには 4 種類あります。これらに’は、左側および上部のタブ、ウィザード、アコーディオンが含まれています。各ナビゲーターには、異なるクラスが割当られています。

<table>
 <tbody>
  <tr>
   <td><p><strong>ナビゲーター</strong></p> </td>
   <td><p><strong>CSS クラス</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

次に示すのは、タブナビゲーター要素（ブートストラップタブに類似する）のHTML コードです。

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

**子孫** セレクターで要素を選択する CSS ルールを使い、ナビゲーターのスタイル設定を変更することができます。例えば、アンカータグにテキスト装飾スタイルを追加するには：

上部のタブナビゲーター：

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

さらに、入れ子のナビゲーターの有無に基づいて、タブナビゲーター（左側と上部の両方）のスタイル設定を行うためのクラスがあります。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス</strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>入れ子ナビゲーターを持つタブナビゲーター（左側と上部の両方）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>入れ子ナビゲーターを持たないタブナビゲーター（左側と上部の両方）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon クラスで、タブナビゲーター（左側と上部の両方）およびウィザードナビゲーターにデフォルトのアイコンを指定することができます。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>オーサリング中にパネルに CSS クラス（例：&lt;CLASS_NAME>）を指定することで、特定のナビゲーターのアイコンを変更することができます。ナビゲーターのアイコンに **&lt;CLASS_NAME>_nav** を追加します。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>タブナビゲーター</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>タブナビゲーター全体の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>タブの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>タブのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>カーソルが置かれたときのタブの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>カーソルが置かれたときのタブのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>パネルがフォーカスされた（アクティブな）ときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>パネルがフォーカスされたときのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>パネルの完了式が true を返したときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>パネルの完了式が true を返したときのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>パネルが一度フォーカスされたが、パネルの完了式がfalseを返したときの背景色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>パネルが一度フォーカスされたが、パネルの完了式がfalseを返したときのフォントカラー </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>タブのボーダーのカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>タブのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>タブのパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>タブの余白</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直タブの余白</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>タブのボーダーのサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>タブの最小の高さ</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>入れ子タブのインデント</p> </td>
  </tr>
  <tr>
   <td><p><strong>ウィザードナビゲーション</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>ウィザードナビゲーター全体の背景色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>ウィザードの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>ウィザードのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>パネルがフォーカスされた（アクティブな）ときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>パネルがフォーカスされたときのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>パネルの完了式が true を返したときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>パネルの完了式が true を返したときのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>パネルが一度フォーカスされたが、パネルの完了式が false を返したときの背景色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>パネルが一度フォーカスされたが、パネルの完了式が false を返したときのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>ウィザードの色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>ウィザードのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>ウィザードのパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>ウィザードのボーダーのサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>ウィザードナビゲーターの行頭文字（キャプション/ラベルの前に付ける）のボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>ウィザードナビゲーターのプログレスバーの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>プログレスバーの塗りつぶしの色</p> </td>
  </tr>
  <tr>
   <td><p><strong>アコーディオンナビゲーター</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>アコーディオンのパディング</p> </td>
  </tr>
 </tbody>
</table>

## パネルのスタイル設定 {#panel-styling}

パネルには、オプションのツールバーとそのコンテンツが含まれます。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>パネルの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>パネルテキストのフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>パネルテキストのフォントカラー<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>パネル内のパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>パネルの説明のフォントサイズ</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>パネルの説明のパディング</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>パネルのヘルプの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>パネルのヘルプのインジケーターのボーダーの色</p> </td>
  </tr>
 </tbody>
</table>

パネルノードは、ナビゲーターとコンテンツに分けられています。コンテンツ用の別のスタイル設定コンポーネントはありません。`` ``説明された変数は、コンテンツだけでなくナビゲーターにも適用されます。

The topmost panel (RootPanel) doesn&#39;t have this class.

## モバイルのスタイル設定 {#mobile-styling}

## ヘッダーバー {#header-bar}

これらの変数は、ヘッダーバーに影響します。ヘッダーバーは、モバイルデバイスまたは画面の小さいデバイスに表示され、パネルタイトルおよび次へ/前へのナビゲーターを含むバーのことです。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>ヘッダーバーの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>ヘッダーバーの中のテキストのフォントカラー</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>ヘッダーバーのパディング</p> </td>
  </tr>
 </tbody>
</table>

## スクロールインジケーター {#scroll-indicator}

これらの変数は、スクロールインジケーターに影響します。スクロールインジケーターとは、モバイルデバイスまたは画面の小さいデバイスに表示されるオレンジの矢印のことです。スクロールインジケーターは、画面で表示されている部分以外にコンテンツがあることを示しています。下方向にスクロールすると表示されます。矢印は、コンテンツの一番下に到達すると消えます。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>スクロールインジケーターの下からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>スクロールインジケーターの右からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>スクロールインジケーターの幅</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>スクロールインジケーターの高さ</p> </td>
  </tr>
 </tbody>
</table>

## モバイル固定ツールバーのレイアウト固有の変数 {#mobile-fixed-toolbar-layout-specific-variables}

次の表に示すこれらの変数は、モバイル固定ツールバーのレイアウトに影響します。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS クラス </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーの下からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーの上からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーの左からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーの右からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーのボタンアイコンの上からの固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーのボタンアイコンの幅</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーのボタンアイコンの高さ</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>モバイルデバイス上でのツールバーの背景色</p> </td>
  </tr>
 </tbody>
</table>

## テーマ固有の変数 {#theme-specific-variable}

The **Simple enrollment** theme at /etc/clientlibs/fd/af/guidetheme/simpleEnrollment and the category `guide.theme.simpleEnrollment` also introduce a few variables. シンプルな登録を強化するテーマを作成する場合は、次の「追加の変数」を使用できます。

<table>
 <tbody>
  <tr>
   <td><p><strong>変数 </strong></p> </td>
   <td><p><strong>説明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>ボタンがフォーカスされたときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>ボタンにカーソルが置かれたときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>ボタンの半径</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>ナビゲーションボタン（前へ/次へ）の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>カーソルが置かれたときのナビゲーションボタン（前へ/次へ）の背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>ウィザードナビゲーターと対応するプログレスバーが最初にレンダリングされたときの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>現在/アクティブなウィザードナビゲーターと対応するプログレスバーの背景色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>訪問済みのウィザードナビゲーターと対応するプログレスバーの背景色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>ナビゲーターとパネルにコンテナを分岐するボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>タブと左側にあるタブ（タブナビゲーター）を分ける下のボーダーの色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>ナビゲーターの入れ子ナビゲーターの背景色</p> </td>
  </tr>
 </tbody>
</table>

