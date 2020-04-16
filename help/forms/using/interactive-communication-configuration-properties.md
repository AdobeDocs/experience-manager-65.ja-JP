---
title: インタラクティブ通信の設定プロパティ
seo-title: インタラクティブ通信の設定プロパティ
description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
seo-description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# インタラクティブ通信の設定プロパティ{#interactive-communications-configuration-properties}

インタラクティブ通信には、[AEM Forms アドオン](../../forms/using/installing-configuring-aem-forms-osgi.md)パッケージのインストール後に自動的に設定されるプロパティが含まれています。インタラクティブ通信の作成者は、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを使用して、これらのデフォルトの設定プロパティを編集できます。

Open the **Adobe Experience Manager Web Console Configuration** page using the following URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

設定プロパティには次のものが含まれます。

* [ドキュメントフラグメントの設定](#document-fragments-configuration)
* [通信設定の作成](#create-correspondence-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## ドキュメントフラグメントの設定 {#document-fragments-configuration}

**Adobe Experience Manager Web Console Configuration** ( **Adobe Experience Manager Web Console Configuration** )ページで「ドキュメントフラグメントの設定」をタップし、ドキュメントフラグメントの設定プロパティを表示します。

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>データの表示形式</td> 
   <td>印刷およびWebチャネル用のInteractive Communicationを作成する際に使用できる、フィールド、変数およびフォームデータモデル要素のロケール固有の表示形式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FRおよびja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>インデント</td> 
   <td>リストドキュメントフラグメント内のテキストに適用される単一ユニットのインデント幅。</td> 
   <td>12.7 mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅のローマ数字</td> 
   <td>リストドキュメントフラグメント内でローマ数字を使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。 </td> 
   <td>12.7 mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅の数字</td> 
   <td>リストドキュメントフラグメント内でローマ数字以外の番号付きリストを使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。</td> 
   <td>8.0 mm</td> 
   <td>数値</td> 
  </tr> 
 </tbody> 
</table>

## 通信設定の作成 {#create-correspondence-configuration}

Tap **Create Correspondence Configuration** on the **Adobe Experience Manager Web Console Configuration** page to view the configuration properties for Agent UI.

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>編集用に解決されたコンテンツの表示</td> 
   <td>エージェント UI 上でテキストモジュールを編集する際に、チェックボックスを選択して、解決されたコンテンツ（プレースホルダーではなく実際の値）を表示します。</td> 
   <td>未選択</td> 
   <td>適用なし</td> 
  </tr> 
  <tr> 
   <td>プレビュー時に透かしの適用</td> 
   <td>チェックボックスを選択して、インタラクティブ通信の印刷チャネルのプレビュー表示に透かしを適用します。</td> 
   <td>未選択</td> 
   <td>適用なし</td> 
  </tr> 
  <tr> 
   <td>PDFへのフォントの埋め込みを有効にする</td> 
   <td><p>PDFオプションにフォントを埋め込む場合は、このチェックボックスをドキュメントします。 このオプションを選択した後、エージェントUIを使用してPDFフォントを生成またはプレビューした後に、新しいドキュメントを埋め込むことができます。 Interactive Communicationの印刷チャネルを使用して、PDF画像を生成し、プレビューします。</p> <p>PDFの生成に使用され、PDFにアクセスするクライアントコンピューターで使用できないフォントがある場合、PDFドキュメントにフォントを埋め込むと便利です。</p> <p>フォントの埋め込みについて詳しくは、テキストエディターのカスタ <a href="../../forms/using/customize-text-editor.md" target="_blank">マイズを参照してくださ</a>い。</p> </td> 
   <td>未選択</td> 
   <td>該当なし</td> 
  </tr> 
 </tbody> 
</table>

## アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

Tap **Adaptive Form and Interactive Communication Web Channel Configuration** on the **Adobe Experience Manager Web Console Configuration** page to view the configuration properties for Adaptive Forms and Interactive Communications Web channel. 次のテーブルに、インタラクティブ通信に関連するプロパティを示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| プレースホルダーを表示 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に含まれているフィールドのプレースホルダー表示を有効にします。 | 選択 | 適用なし |
| 最大キャッシュエントリ数 | キャッシュメモリを使用して取得できるアダプティブフォームおよびインタラクティブ通信の最大数を設定します。 | 100 | 数値 |
| 一意のファイル名を作成 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に添付ファイルとして含まれているファイルに一意の名前を付けます。 | 未選択 | 該当なし |

## アダプティブフォームおよびインタラクティブ通信 Web チャネルテーマの設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Tap **Adaptive Form and Interactive Communication Web Channel Theme Configuration** on the **Adobe Experience Manager Web Console Configuration** page to view the configuration properties for Adaptive Forms and Interactive Communications Web channel themes.

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>フォントリスト名</td> 
   <td>フォントの一覧は、アダプティブフォームおよびインタラクティブ通信を作成する際に使用できるようになります。</td> 
   <td><p>グルジア</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影響</p> <p>Palatino Linotype</p> </td> 
   <td>すべての有効な Adobe サーバーフォント</td> 
  </tr> 
 </tbody> 
</table>

