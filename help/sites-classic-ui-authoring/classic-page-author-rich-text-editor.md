---
title: リッチテキストエディター
description: リッチテキストエディターは、AEM にテキストコンテンツを入力するための基本的な構成要素です。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 88%

---

# リッチテキストエディター {#rich-text-editor}

リッチテキストエディターは、AEM にテキストコンテンツを入力するための基本的な構成要素です。以下を含む、様々なコンポーネントの基礎を形成します。

* テキスト
* テキスト画像
* テーブル

## リッチテキストエディター {#rich-text-editor-1}

WYSIWYG 編集ダイアログは、様々な機能を提供します。

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>利用できる機能は、個別のプロジェクトごとに設定できるので、インストールによって異なる可能性があります。

## インプレース編集 {#in-place-editing}

ダイアログベースのリッチテキスト編集モードに加えて、AEM には、ページのレイアウトどおりに表示されたテキストを直接編集できる、インプレース編集モードも用意されています。

段落を 2 回クリック（ゆっくりダブルクリック）して、インプレース編集モードに切り替えます（コンポーネントのボーダーがオレンジになります）。

ページ上のテキストを、ダイアログウィンドウ内ではなく直接編集できます。変更を行うと、その内容は自動的に保存されます。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>コンテンツファインダーを開いている場合、上記のように、RTE フォーマットオプションを含むツールバーがタブの上部に表示されます。
>
>コンテンツファインダーを開いていない場合は、ツールバーは表示されません。

現在、インプレース編集モードは、**テキスト**&#x200B;および&#x200B;**タイトル**&#x200B;コンポーネントで生成されたページ要素に対して有効です。

>[!NOTE]
>
>[!UICONTROL タイトル]コンポーネントは、改行がない短いテキストを含むものとして設計されています。インプレース編集モードでタイトルを編集する場合、改行を入力すると、新しい **テキスト** コンポーネントをタイトルの下に追加します。

## リッチテキストエディターの機能 {#features-of-the-rich-text-editor}

リッチテキストエディターには様々な機能があり、機能は個々のコンポーネントの[設定によって異なります](/help/sites-administering/rich-text-editor.md)。これらの機能は、タッチ操作向け UI とクラシック UI の両方で利用できます。

### 基本文字書式 {#basic-character-formats}

![文字書式ツールバー](do-not-localize/cq55_rte_basicchars.png)

以下に、選択した（ハイライト表示された）文字に適用できる書式を示します。ショートカットキーのあるオプションもあります。

* 太字（Ctrl + B）
* イタリック（Ctrl + I）
* 下線（Ctrl + U）
* 下付き文字
* 上付き文字

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

すべてオン／オフ切り替えとして動作するので、再選択すると書式が削除されます。

### 事前定義済みのスタイルおよび書式 {#predefined-styles-and-formats}

![cq55_rte_stylesparagraph](assets/cq55_rte_stylesparagraph.png)

事前定義済みのスタイルおよび書式をお使いのインストールに含めることができます。これらは、 **[!UICONTROL スタイル]** および **[!UICONTROL 形式]** ドロップダウンリストと、選択したテキストに適用できます。

スタイルは、特定の文字列に対して適用できます（スタイルは CSS に関連付けられます）。

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

これに対して、書式はテキストの段落全体に適用されます（書式は HTML ベースです）。

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

個別の書式は変更のみ可能です（デフォルトは「**[!UICONTROL 段落]**」です）。

スタイルは削除できます。スタイルが適用されたテキスト内にカーソルを置き、次の削除アイコンをクリックします。

>[!CAUTION]
>
>スタイルを適用したテキストを実際に再選択しないでください。再選択すると、アイコンがアクティベート解除されます。

### 切り取り、コピー、貼り付け {#cut-copy-paste}

![切り取り、コピー、貼り付けツールバー](do-not-localize/cq55_rte_cutcopypaste.png)

「**[!UICONTROL 切り取り]**」および「**[!UICONTROL コピー]**」の標準的な機能が利用できます。「**[!UICONTROL 貼り付け]**」には、書式の違いに対応するためにいくつかの種類があります。

* 切り取り（Ctrl+X）
* コピー（Ctrl + C）
* 貼り付け
コンポーネント用のデフォルトの貼り付けメカニズム（Ctrl+V）です。追加設定なしのインストールでは、これには、「[!UICONTROL Word から貼り付け]」が設定されます。

* テキストとして貼り付け：すべてのスタイルおよび書式を削除して、プレーンテキストのみを貼り付けます。

* Word から貼り付け：HTML としてコンテンツを貼り付けます（必要に応じて書式が再設定されます）。

### 取り消し、やり直し {#undo-redo}

![取り消し、やり直しツールバー](do-not-localize/cq55_rte_undoredo.png)

AEM では、現在のコンポーネントでの直近 50 個の操作を記録し、時系列で保持します。必要に応じて、これらの操作を完全に元に戻す（その後、やり直す）ことができます。

>[!CAUTION]
>
>履歴は、現在の編集セッションに対してのみ保持されます。コンポーネントを開いて編集するたびに再開します。

>[!NOTE]
>
>デフォルトのタスク数は 50 です。これは、お使いのインストールによって異なる場合があります。

### 整列 {#alignment}

![整列ツールバー](do-not-localize/cq55_rte_alignment.png)

テキストは、左揃え、中央揃えまたは右揃えにできます。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### インデント {#indentation}

![インデントツールバー](do-not-localize/cq55_rte_indent.png)

段落のインデントは増減できます。選択した段落はインデントされ、新しいテキストが入力されると、現在のインデントレベルが保持されます。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### リスト {#lists}

![リストツールバー](do-not-localize/cq55_rte_lists.png)

テキスト内には、箇条書きリストと番号付きリストの両方を作成できます。リストの種類を選択してから入力を開始するか、変換するテキストをハイライト表示します。どちらの場合も、改行によって新しいリスト項目が始まります。

1 つ以上のリスト項目をインデントすることで、リストをネストできます。

リストのスタイルは、リスト内にカーソルを置き、他のスタイルを選択するだけで変更できます。サブリストに、親リストと異なるスタイルを設定することもできます。スタイルは、サブリストの作成後に（インデント別に）適用できます。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### リンク {#links}

![リンクツールバー](do-not-localize/cq55_rte_links.png)

URL（Web サイト内または外部の場所）へのリンクは、必要なテキストをハイライト表示し、ハイパーリンクアイコンをクリックすることで生成されます。

![ハイパーリンクアイコン](do-not-localize/chlimage_1-9.png)

ダイアログで、ターゲット URL を指定できます。また、新しいウィンドウで開く必要があるかどうかも指定できます。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

以下の操作を実行できます。

* URI を直接入力する
* Web サイト内のページを選択するためにサイトマップを使用する
* URI を入力し、ターゲットアンカー（例： ）を追加します。 `www.TargetUri.org#AnchorName`
* アンカーのみを入力します（「現在のページ」を参照する場合）（例：`#anchor`）
* コンテンツファインダーでページを検索し、ページアイコンをハイパーリンクダイアログにドラッグ＆ドロップします

>[!NOTE]
>
>URI の先頭には、インストールで設定された任意のプロトコルを付加できます。標準的なインストールの場合、`https://`、`ftp://` および `mailto:` です。インストール用に設定されていないプロトコルは拒否され、無効としてマークされます。

リンクを解除するには、リンクテキスト内の任意の場所にカーソルを置き、次の[!UICONTROL リンク解除]アイコンをクリックします。

![リンク解除アイコン](do-not-localize/chlimage_1-10.png)

### アンカー {#anchors}

![アンカーツールバー](do-not-localize/cq55_rte_anchor.png)

アンカーは、テキスト内のどこにでも作成できます。カーソルを置くか、テキストを選択します。**アンカー**&#x200B;アイコンをクリックしてダイアログを開きます。

アンカーの名前を入力し、「**OK**」をクリックして保存します。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

アンカーは、コンポーネントの編集中に表示され、リンクのターゲットとして使用できます。

![chlimage_1-104](assets/chlimage_1-104.png)

### 検索と置換 {#find-and-replace}

![検索と置換ツールバー](do-not-localize/cq55_rte_findreplace.png)

AEM には、**検索**&#x200B;および&#x200B;**置換**&#x200B;の両方の機能（「検索と置換」）があります。

どちらにも「**次を検索**」ボタンがあり、開いているコンポーネントに対して、指定したテキストを検索します。また、大文字／小文字が一致する必要があるかどうかも指定できます。

検索は、常に、テキスト内の現在のカーソル位置から開始します。コンポーネントの最後に達したら、次の検索処理がコンポーネントの最初から開始されることを示すメッセージが表示されます。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

The **置換** オプションを使用すると、 **検索文字列**&#x200B;を、 **置換** 指定したテキストを持つ個々のインスタンス、または **すべてを置換** 現在のコンポーネントのインスタンス。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 画像 {#images}

画像は、コンテンツファインダーからドラッグしてテキストに追加できます。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM では、さらに詳細な画像設定のための専用コンポーネントも提供しています。例えば、 **画像** および **テキスト画像** コンポーネントを使用できます。

### スペルチェッカー {#spelling-checker}

![スペルチェッカー](do-not-localize/cq55_rte_spellchecker.png)

スペルチェッカーは、現在のコンポーネントのすべてのテキストをチェックします。

正しくないスペルは、次のようにハイライト表示されます。

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>スペルチェッカーは、サブツリーの言語プロパティを取得するか、URL から言語を抽出することにより、web サイトの言語で動作します。例えば、 `en` ブランチで英語がチェックされ、 `de` ドイツ語の支店。

### テーブル {#tables}

表は、次のどちらかの方法によって利用できます。

* **テーブル**&#x200B;コンポーネントとして

  ![テーブルコンポーネント](assets/chlimage_1-105.png)

* **テキスト**&#x200B;コンポーネント内から

  ![テキストツールバー](do-not-localize/chlimage_1-11.png)

  >[!NOTE]
  >
  >テーブルは RTE で使用できますが、テーブルの作成時は&#x200B;**テーブル**&#x200B;コンポーネントを使用することをお勧めします。

テーブル機能は、**テキスト**&#x200B;コンポーネントと&#x200B;**テーブル**&#x200B;コンポーネントの両方において、テーブル内で（通常、マウスの右ボタンを）クリックして表示されるコンテキストメニューから利用できます。以下に例を示します。

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>**テーブル**&#x200B;コンポーネントでは、様々な標準的なリッチテキストエディター機能、およびテーブルに特有の機能のサブセットを含む専用のツールバーも使用できます。

テーブルに特有の機能を以下に示します。

* [テーブルのプロパティ](#table-properties)
* [セルのプロパティ](#cell-properties)
* [行の追加または削除](#add-or-delete-rows)
* [列の追加または削除](#add-or-delete-columns)
* [すべての行またはすべての列の選択](#selecting-entire-rows-or-columns)
* [セルの統合](#merge-cells)
* [セルの分割](#split-cells)
* [ネストされたテーブル](#creating-nested-tables)
* [テーブルの削除](#remove-table)

#### テーブルのプロパティ {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

テーブルの基本的なプロパティを設定できます。その後、「**OK**」をクリックして保存します。

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **幅**：テーブル全体の幅です。

* **高さ**：テーブル全体の高さです。

* **ボーダー**：テーブルのボーダーのサイズです。

* **セル内の余白**：セルコンテンツとそのボーダーの間の空白を定義します。

* **セルの間隔**：セル間の距離を定義します。

>[!NOTE]
>
>幅や高さなど、一部のセルプロパティは、ピクセルまたはパーセンテージで定義できます。

>[!CAUTION]
>
>テーブルの幅を定義することをお勧めします。

#### セルのプロパティ {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

次に示すように、特定のセルまたは一連のセルのプロパティを設定できます。

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **幅**
* **高さ**
* **水平方向の位置揃え** - 左、中央または右
* **垂直方向の位置揃え** - 上、中央、下またはベースライン
* **セルのタイプ** - データまたはヘッダー
* **適用先：** 単一のセル、行全体、列全体

#### 行の追加または削除 {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

行は、現在の行の上または下に追加できます。

現在の行を削除することもできます。

#### 列の追加または削除 {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

列は、現在の列の左または右に追加できます。

現在の列を削除することもできます。

#### すべての行またはすべての列の選択 {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

現在の行全体または列全体を選択します。その後、特定のアクション（結合など）を使用できます。

#### セルの統合 {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* セルのグループを選択した場合は、それらを 1 つに結合できます。
* セルを 1 つだけを選択した場合は、選択したセルを右または下のセルと結合できます。

#### セルの分割 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

1 つのセルを選択して分割します。

* セルを左右に分割すると、現在の列内で、現在のセルの右に新しいセルが生成されます。
* セルを上下に分割すると、現在の行内で、現在のセルの下に新しいセルが生成されます。

#### ネストされたテーブルの作成 {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

ネストされた表を作成すると、現在のセル内に自己完結型の表が作成されます。

>[!NOTE]
>
>その他の特定の動作は、ブラウザーによって異なります。
>
>* Windows IE：Ctrl キーを押しながらマウスの主ボタン（通常は左）をクリックして、複数のセルを選択します。
>* Firefox：ポインターをドラッグして、セルの範囲を選択します。

#### テーブルの削除 {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

**[!UICONTROL Text]** コンポーネント内からテーブルを削除するオプションを使用します。

### 特殊文字 {#special-characters}

![特殊文字ツールバー](do-not-localize/cq55_rte_specialchars.png)

リッチテキストエディターで特殊文字を使用できるように設定できます。使用できる特殊文字は、お使いのインストールによって異なる場合があります。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

マウスオーバーを使用して文字を拡大表示し、クリックしてテキストの現在の位置に文字を含めます。

### ソース編集モード {#source-editing-mode}

![ソース編集モードのツールバー](do-not-localize/cq55_rte_sourceedit.png)

ソース編集モードを使用すると、コンポーネントの基になるHTMLを表示および編集できます。

例えば、次のテキストを入力します。

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

ソースモードでは次のように表示されます（多くの場合、ソースは長くなるので、スクロールする必要があります）。

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>ソースモードを終了する際に、AEM では特定の検証チェックが実行されます（テキストがブロック内に適切に含まれているか、ネストされているかなどを確認します）。これにより、編集内容が変更される場合があります。
