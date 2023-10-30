---
title: HTML5 フォームと PDF フォームの機能の違い
description: HTML5 のフォームとPDF formsの違いについて説明します。
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 39%

---

# HTML5 フォームと PDF フォームの機能の違い {#feature-differentiation-between-html-forms-and-pdf-forms}

次の表に、HTML5 のフォームとPDF formsでサポートされる機能を示します。

<table>
 <tbody>
  <tr>
   <th>機能</th>
   <th>HTML5 のフォーム</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>バーコード<br /> </td>
   <td>ユーザーインターフェイスレベルでは使用できません。 </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>署名フィールド<br /> </td>
   <td><strong>電子署名</strong> はサポートされていませんが、新しい <strong>手書き署名</strong> 紙のような署名用にフィールドが追加されます。 フォーム上の署名は、 <strong>手書き署名</strong> フィールドに入力します。 署名はフォーム上に画像として保存されます。 位置情報は、 <strong>手書き署名</strong> フィールドに入力します。</td>
   <td>以下で使用可能な署名フィールド： <strong>電子署名</strong>.</td>
  </tr>
  <tr>
   <td>データの結合</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>画像</td>
   <td>データ URI スキームは、画像の表示に使用されます。 最新バージョンのブラウザーはすべてこのスキームをサポートしていますが、各ブラウザーがサポートする画像形式の範囲に違いがあります。<br /> </td>
   <td>.gif、.png、.jpeg、.bmp、および .tiff 形式がサポートされています。</td>
  </tr>
  <tr>
   <td>ページネーション<br /> </td>
   <td><p>HTML5 フォームは、PDF formsと同様に見えるように、パネルとボックスに分割されています。 ページのサイズは動的に計算されます。 HTML5 フォーム内のページのすべてのコンテンツが削除または非表示とマークされた場合、空白ページは非表示になり、空白ページの上と下のページの間に空白（空白スペース）は表示されません。</p> <p>data-merge または scripts がコンテンツをページに追加する場合、新しく追加されたコンテンツが表示されるようにページの長さが拡張されます。 新しく追加されたコンテンツに対応する新しいページはフォームに追加されません。 </p> <p><strong>注意：</strong>HTML5 フォームにおけるページのすべてのコンテンツが削除されたか非表示としてマークされた場合、1 ページ目と 2 ページ目の間にある空白のページ（空白スペース）は表示されますが、その他のページ間にある空白のページ（空白スペース）は表示されません。</p> </td>
   <td>PDF でのページネーションは、結合したデータコンテンツまたはユーザーコンテンツに依存し、ページ数はそのどちらかにもとづいて増減します。</td>
  </tr>
  <tr>
   <td>ヘッダー／フッター </td>
   <td>サポート対象<br /> <br /> HTML5 モバイルフォームは改ページをサポートしていないため、ヘッダーとフッターが表示されるのは 1 度のみになります。ただし、モバイルフォームプレビューの複数の場所に表示するように、レイアウトで設定することはできます。<br /> </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>カスタムウィジェット</td>
   <td>ウィジェットをカスタマイズして、モバイルデバイスでのユーザーエクスペリエンスを向上させることができます。<br /> </td>
   <td>すべてのウィジェットがロックダウンされ、カスタムウィジェットはプラグインできません。<br /> </td>
  </tr>
  <tr>
   <td>XFA スクリプト API</td>
   <td>最もよく使用される XFA スクリプト構成をサポートします。サポートされている構成要素の詳しい一覧については、<a href="/help/forms/using/scripting-support.md">スクリプティングのサポート</a>を参照してください。</td>
   <td>すべての XFA スクリプトの構成要素をサポートします。</td>
  </tr>
  <tr>
   <td>Acrobat スクリプト API </td>
   <td>HTML5 フォームは、最もよく使用される API をサポートしています。詳しくは、<a href="/help/forms/using/scripting-support.md">スクリプティングのサポート</a>を参照してください。</td>
   <td>PDF ファイルを Acrobat または Reader で開く場合、Acrobat が提供するすべてのスクリプト API もサポートします。</td>
  </tr>
  <tr>
   <td>右から左に筆記する言語のサポート </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
