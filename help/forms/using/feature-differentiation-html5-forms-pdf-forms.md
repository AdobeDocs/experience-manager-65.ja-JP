---
title: HTML5 フォームと PDF フォーム の機能の違い
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: HTML5 フォームと PDF フォームでサポートされている機能
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '444'
ht-degree: 100%

---

# HTML5 フォームと PDF フォーム の機能の違い {#feature-differentiation-between-html-forms-and-pdf-forms}

次の表では、HTML5 フォームと PDF フォームでサポートされている機能について説明します。

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
   <td><strong>電子署名</strong>はサポートされてませんが、紙上のような署名のために新しい「<strong>Scribble Signature</strong>」フィールドが追加されました。「<strong>Scribble Signature</strong>」フィールドを使用し、フォームに署名を手で書くことができます。署名はフォーム上で画像として保存されます。「<strong>Scribble Signature</strong>」フィールドには位置情報を保存できます。</td>
   <td><strong>電子署名</strong>用の署名フィールドが使用可能。</td>
  </tr>
  <tr>
   <td>データの結合</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>画像</td>
   <td>データ URI スキームは画像の表示に使用されます。すべてのブラウザーの最新バージョンはこのスキームをサポートしていますが、それぞれのブラウザーでサポートされる画像形式の範囲に違いがあります。<br /> </td>
   <td>.gif、.png、.jpeg、.bmp、および .tiff 形式がサポートされています。</td>
  </tr>
  <tr>
   <td>ページネーション<br /> </td>
   <td><p>HTML5 フォームは、PDF フォームと同様の外観を提供するためにパネルとボックスに分けられています。ページのサイズは動的に計算されます。HTML5 フォーム内のページのすべてのコンテンツが削除されたか非表示としてマークされた場合、空白ページは非表示になり、ページ間にある空白ページの空白スペースは表示されません。</p> <p>データをマージするかスクリプトのコンテンツをページに追加した場合、新しく追加したコンテンツを取り込めるようにページの長さが拡張されます。新しく追加したコンテンツを取り込むために新しいページがフォームに追加されることはありません。 </p> <p><strong>注意：</strong>HTML5 フォームにおけるページのすべてのコンテンツが削除されたか非表示としてマークされた場合、1 ページ目と 2 ページ目の間にある空白のページ（空白スペース）は表示されますが、その他のページ間にある空白のページ（空白スペース）は表示されません。</p> </td>
   <td>PDF でのページネーションは、結合したデータコンテンツまたはユーザーコンテンツに依存し、ページ数はそのどちらかにもとづいて増減します。</td>
  </tr>
  <tr>
   <td>ヘッダー／フッター </td>
   <td>サポート対象 <br /> <br /> HTML5 モバイルフォームは改ページをサポートしていないため、ヘッダーとフッターが表示されるのは 1 度のみになります。ただし、レイアウトを設定することにより、モバイルフォームプレビュー内の複数の場所に表示させることができます。<br /> </td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>カスタムウィジェット</td>
   <td>モバイルデバイスでのユーザーエクスペリエンスを強化するために、ウィジェットをカスタマイズすることができます。<br /> </td>
   <td>すべてのウィジェットはロックダウンされ、カスタムウィジェットはプラグインできない。<br /> </td>
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
