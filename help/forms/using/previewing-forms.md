---
title: フォームのプレビュー
seo-title: フォームのプレビュー
description: 発行またはアクティベートする前にフォームをプレビューして、期待通りになっていることを確認します。プレビューのオプションは、サポートされているフォームタイプにより異なる場合があります。
seo-description: 発行またはアクティベートする前にフォームをプレビューして、期待通りになっていることを確認します。プレビューのオプションは、サポートされているフォームタイプにより異なる場合があります。
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 89%

---


# フォームのプレビュー {#previewing-a-form}

## 概要 {#overview}

AEM Forms では、リポジトリ内にあるフォームやドキュメントをプレビューできます。プレビューを使用すると、フォームがエンドユーザーにリリースされる際にどのように見え、作動するのかを明確に理解できます。

フォームをプレビューすると、フォームはインタラクティブインターフェイスでレンダリングされ、ユーザーはフォームにデータを入力できます。ドキュメントをプレビューすると、ドキュメントは非インタラクティブモードでレンダリングされ、ユーザーはドキュメントのみを見ることができます。フォームの場合、カスタムプレビューの追加オプションが使用できます。このオプションを使用すると、XML ファイルのデータを使用してフォームをプレビューできます。プレビューしているフォームのフィールドの一部またはすべてにデータが入力されます。

下表に、サポートされているフォームのタイプごとに使用できるプレビューオプションを示します。

<table>
 <tbody>
  <tr>
   <td><strong>アセットタイプ</strong><br /> </td>
   <td><strong>使用できるプレビューオプション</strong><br /> </td>
  </tr>
  <tr>
   <td>ドキュメント</td>
   <td>PDF プレビュー</td>
  </tr>
  <tr>
   <td>PDF フォーム</td>
   <td>PDF プレビューとデータを使用してプレビュー<br /> </td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>HTML プレビューとデータを使用して HTML プレビュー</td>
  </tr>
  <tr>
   <td>フォームテンプレート</td>
   <td>PDF プレビュー、データを使用して PDF プレビュー、HTML プレビュー、データを使用して HTML プレビュー<br /> </td>
  </tr>
 </tbody>
</table>

## フォームのプレビュー {#previewing-a-form-1}

1. Select an asset you want to preview, and click Preview ![aem6forms_preview](assets/aem6forms_preview.png) in the actions toolbar.

   >[!NOTE]
   >
   >アセットを選択するには、デフォルトのカードビューをリストビューに切り替えます。「 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 」または「 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 」をクリックして表示を切り替えます。

1. プレビューをクリックすると、選択されているアセットタイプで使用できるプレビューオプションが表示されます。必要なオプションをクリックすると、選択されているアセットが新しいタブにレンダリングされます。

   次のオプションがあります。

   * HTML としてプレビュー
   * データを使用してプレビュー
   * PDF でプレビュー（フォームテンプレートから選択可能）

## データを使用してプレビュー {#preview-with-data}

「**データを使用してプレビュー**」を選択すると、実際のデータが入力された状態でフォームの様子を見ることができます。データを使用してプレビューオプションでは、サンプルユーザーデータを含めた XML をアップロードできます。サンプルユーザーデータを使用して、選択したフォーマットでプレビューフォームに自動入力します。

1. Select an asset, click Preview ![aem6forms_preview](assets/aem6forms_preview.png), and select **Preview with Data**.
1. フォームのプレビューダイアログで、FormData を XML ファイルとして指定します。プレビューをクリックして、XML からのマージされたデータでフォームをレンダリングします。

