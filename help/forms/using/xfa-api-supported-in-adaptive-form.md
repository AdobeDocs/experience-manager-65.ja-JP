---
title: XDP ベースのアダプティブフォームにおける XFA のサポート
description: アダプティブフォームでサポートされる XFA イベント、プロパティ、スクリプト、検証を一覧表示します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '732'
ht-degree: 100%

---

# XDP ベースのアダプティブフォームにおける XFA のサポート{#xfa-support-in-xdp-based-adaptive-forms}

## はじめに {#introduction}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

アダプティブフォームでは、XDP ファイルで定義される各種 XDP イベント、プロパティ、スクリプト、検証をサポートします。サポートには次のものが含まれます。

* XDP ファイルのイベントで定義されたスクリプトの実行
* XDP ファイル内の各フィールドのデフォルトの値および動作プロパティの取得
* XDP ファイルで定義された検証スクリプトの実行

XDP ファイルに基づいてアダプティブフォームが作成されると、各種プロパティ、イベント、および検証がフォーム作成 UI に自動入力されます。ただし、フォーム作成者は、これらの要素の一部を上書きして代替エクスペリエンスを作成できます。

この記事では、アダプティブフォームでサポートされる XFA イベント、プロパティ、スクリプト、検証を一覧表示し、アダプティブフォームでこれらをオーバーライドする方法を説明します。

## アダプティブフォームでサポートされる XFA 要素およびそれらのマッピング {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### フィールド {#fields}

XDP ファイルを使用してアダプティブフォームを作成すると、XFA フィールドをアダプティブフォームにドラッグ＆ドロップできます。次の表は、XFA フィールドがアダプティブフォームのフィールドにマッピングされる方法を一覧表示したものです。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA フィールドまたはコンテナ</strong></p> </td>
   <td><p><strong>対応するアダプティブフォームのコンポーネント</strong></p> </td>
  </tr>
  <tr>
   <td><p>ボタン </p> </td>
   <td><p>ボタン</p> </td>
  </tr>
  <tr>
   <td><p>チェックボックス </p> </td>
   <td><p>チェックボックス</p> </td>
  </tr>
  <tr>
   <td><p>リストボックス </p> </td>
   <td><p>ドロップダウンリスト</p> </td>
  </tr>
  <tr>
   <td><p>日付／時間フィールド </p> </td>
   <td><p>日付選択</p> </td>
  </tr>
  <tr>
   <td><p>手書き署名</p> </td>
   <td><p>手書き署名</p> </td>
  </tr>
  <tr>
   <td><p>数値フィールド </p> </td>
   <td><p>数値ボックス</p> </td>
  </tr>
  <tr>
   <td><p>十進数フィールド</p> </td>
   <td><p>数値ボックス</p> </td>
  </tr>
  <tr>
   <td><p>テキストフィールド </p> </td>
   <td><p>テキストボックス</p> </td>
  </tr>
  <tr>
   <td><p>パスワードフィールド </p> </td>
   <td><p>パスワードボックス</p> </td>
  </tr>
  <tr>
   <td><p>画像</p> </td>
   <td><p>画像</p> </td>
  </tr>
  <tr>
   <td><p>テキスト</p> </td>
   <td><p>テキスト</p> </td>
  </tr>
  <tr>
   <td><p>サブフォーム </p> </td>
   <td><p>パネル</p> </td>
  </tr>
  <tr>
   <td><p>領域（グループ）</p> </td>
   <td><p>パネル</p> </td>
  </tr>
  <tr>
   <td><p>サブフォームセット </p> </td>
   <td><p>パネル</p> </td>
  </tr>
 </tbody>
</table>

### プロパティ {#properties}

次の表は、XDF ファイルで定義された各種 XFA スクリプトがどのようにアダプティブフォームで動作するか示したものです。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA コンポーネントのプロパティ</strong></p> </td>
   <td><p><strong>アダプティブフォームにおける対応する動作</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>アダプティブフォームのバインド参照（bindRef）プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>アダプティブフォームの Visible プロパティにマッピング済みです。表示式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>アダプティブフォームの Enabled プロパティにマッピング済みです。アクセス式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: role </p> </td>
   <td><p>アダプティブフォームの Role プロパティにマッピング済みです。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: speakPriority </p> </td>
   <td><p>アダプティブフォームの speakPriority プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: speakText</p> </td>
   <td><p>アダプティブフォームのカスタム Accessibility テキストにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>Accessibility: toolTip </p> </td>
   <td><p>アダプティブフォームの Short Description プロパティにマッピング済みです。</p> </td>
  </tr>
  <tr>
   <td><p>caption<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの Title プロパティにマッピング済みです。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの Display Pattern にマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em>（すべてのフィールドの種類）</em></p> </td>
   <td><p>アダプティブフォームの value プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>items<em>（リストボックス、チェックボックス）</em></p> </td>
   <td><p>アダプティブフォームの options プロパティにマッピング済み。オプション式を使用して上書きできます。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em>（テキストフィールド）</em></p> </td>
   <td><p>アダプティブフォームの Maximum characters allowed プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>multiline<em>（テキストフィールド）</em></p> </td>
   <td><p>アダプティブフォームの Allow multiple lines プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em>（数値フィールド、十進数フィールド）</em></p> </td>
   <td><p>アダプティブフォームの Frac digits プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em>（数値フィールド、十進数フィールド）</em></p> </td>
   <td><p>アダプティブフォームの Lead digits プロパティにマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em>（リストボックス）</em></p> </td>
   <td><p>アダプティブフォームの Allows multiple selection プロパティにマッピング済み。</p> </td>
  </tr>
 </tbody>
</table>

### スクリプト {#scripts}

次の表は、XDF ファイルで定義された各種 XFA スクリプトがどのようにアダプティブフォームで動作するか示したものです。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA スクリプトイベント</strong></p> </td>
   <td><p><strong>アダプティブフォームにおける対応する動作</strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。</p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>アダプティブフォームの Calculate 数式にマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>アダプティブフォームの Validation 数式にマッピング済み。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。</p> </td>
  </tr>
  <tr>
   <td><p>click（ボタンフィールド）</p> </td>
   <td><p>ボタンのクリック式にマッピングされる。</p> </td>
  </tr>
  <tr>
   <td><p>Support for server-side script</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。</p> </td>
  </tr>
  <tr>
   <td><p>Support for web services</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。</p> </td>
  </tr>
  <tr>
   <td><p>Change（手書きフィールド、ラジオボタン、チェックボックス）</p> </td>
   <td><p>このスクリプトは、実行時に実行され、アダプティブフォームではオーバーライドできません。</p> </td>
  </tr>
 </tbody>
</table>

### 検証 {#validations}

次の表は、アダプティブフォームで XFA 検証が検証にどのようにマッピングするかを示したものです。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA 検証</strong></p> </td>
   <td><p><strong>アダプティブフォームにおける対応する検証</strong></p> </td>
  </tr>
  <tr>
   <td><p>検証パターン（formatTest）</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>検証パターンのメッセージ（formatTestMessage）</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必須（nullTest）</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>メッセージを空にする（nullTestMessage） </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>スクリプトを検証（scriptTest）</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>検証スクリプトのメッセージ（scriptTestMessage）</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>XFA チェックボタンに連結されたアダプティブフォームのラジオボタンおよびチェックボックスの必須プロパティをオーバーライドすることはできません。
