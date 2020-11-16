---
title: Adobe Experience Managerでコンテンツをオーサリングするようにリッチテキストエディタを設定します。
description: Adobe Experience Managerでコンテンツを作成するためのAdobe Experience Managerリッチテキストエディターの設定について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 430994c8e9951500378e0a4d56c8004e7e81c24f
workflow-type: tm+mt
source-wordcount: '3022'
ht-degree: 79%

---


# リッチテキストエディターの設定 {#configure-the-rich-text-editor}

リッチテキストエディター（RTE）には、テキストコンテンツの編集に使用できる幅広い機能が用意されています。アイコン、選択ボックス、ツールバーおよびメニューを使用して、テキストを WYSIWYG で編集できます。

RTE 機能をオーサリングに使用する方法については、[リッチテキストエディターをオーサリングに使用](/help/sites-authoring/rich-text-editor.md)を参照してください。RTE の設定をおこなうことで、オーサリングコンポーネント内で使用可能な機能を有効化、無効化および拡張できます。次のワークフローは、Experience ManagerでRTE設定タスクを完了する際の推奨順序を示しています。

![RTEの設定方法を学ぶ手順のシーケンス](assets/rte_workflow_v1.png)

*図：RTEの設定方法を学ぶ手順のシーケンス*

## タッチ操作 UI とクラシック UI について {#understand-touch-enabled-ui-and-classic-ui}

タッチ対応UIは、Experience Manager用の標準的なユーザーインターフェイスです。 Adobeでは、オーサリング環境用のレスポンシブデザインを含むタッチ対応UIが導入され [ました](/help/sites-authoring/responsive-layout.md) 。 タッチ対応UIは、タッチ対応とデスクトップデバイス向けに設計されています。 このインターフェイスは、元のクラシックUIとは大きく異なります。

![タッチ対応ユーザーインターフェイスのリッチテキストエディターツールバー](assets/chlimage_1-35.png)

*図：タッチ対応UIのリッチテキストエディターツールバー*

![クラシック UI のリッチテキストエディターツールバー](assets/rtedefault.png)

*図：クラシックUIのリッチテキストエディタツールバー*

>[!MORELIKETHIS]
>
>* [UI 推奨事項（英語）](/help/sites-deploying/ui-recommendations.md)
>* About deprecating the Classic UI, see [Experience Manager 6.5 release notes](/help/release-notes/deprecated-removed-features.md)
>* For difference between the UIs, see [Touch UI and Classic UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* To understand the Touch-enabled UI in detail, see [Concepts of Experience Manager Touch UI](/help/sites-developing/touch-ui-concepts.md)


## 各種編集モード {#editingmodes}

Experience Manager では、コンポーネントの各種モードを使用して、テキストコンテンツを作成および編集できます。コンテンツを作成およびフォーマットするためのツールバーオプションと、各種編集モードにおける RTE 対応コンポーネントのユーザーエクスペリエンスは、RTE 設定によって異なります。

| 編集モード | 編集領域 | 有効化が推奨される機能 | タッチ UI | クラシック UI |
|--- |--- |--- |--- |--- |
| インライン | 小さな編集をすばやくおこなうのに適したインプレース編集。ダイアログボックスを開かないフォーマット | 最小限の RTE 機能 | ○ | ○ |
| RTE フルスクリーン | ページ全体に広がる | 必要なすべての RTE 機能 | ○ | × |
| ダイアログ | ページコンテンツの上面にダイアログボックスが表示されるが、ページ全体に広がらない | クラシック UI の場合、必要なすべての RTE 機能。タッチ UI の場合、必要に応じて機能を有効化／無効化 | ○ | ○ |
| ダイアログ（フルスクリーン） | フルスクリーンモードと同じ。RTE の横にダイアログのフィールドを含む | 必要なすべての RTE 機能 | ○ | × |

>[!NOTE]
>
>タッチ対応UIのインライン編集モードでは、ソース編集機能は使用できません。 フルスクリーンモードでは画像をドラッグできません。その他の機能はすべて全モードで使用できます。

### インライン編集 {#inline-editing}

（ゆっくりしたダブルタップ／ダブルクリックで）開いた場合、コンテンツはページ内で編集できます。非常に基本的なオプションを備えたコンパクトツールバーが表示されます。

![タッチ操作 UI の基本ツールバーを使用したインライン編集](assets/chlimage_1-36.png)

*図：タッチ対応UIの基本ツールバーを使用したインライン編集*

クラシック UI では、コンポーネントをゆっくりダブルクリックするとインライン編集が可能になり、オレンジ色の輪郭でコンテンツが強調表示されます。コンテンツファインダーが開くと、使用可能な RTE フォーマットオプションを備えたツールバーがウィンドウ上部に表示されます。コンテンツファインダーが開かない場合は、フォーマットオプションは表示されず、基本的なテキスト編集のみおこなうことができます。

### 全画面表示での編集 {#full-screen-editing}

Experience Managerコンポーネントは、ページコンテンツを非表示にし、利用可能な画面を占めるフルスクリーン表示で開くことができます。 フルスクリーン編集には最も多くの編集オプションがあるので、インライン編集の詳細版と考えてください。フルスクリーン編集を開くには、インライン編集モードの使用中にコンパクトツールバーから ![rte_fullscreen](assets/rte_fullscreen.png) をクリックします。

ダイアログフルスクリーンモードでは、詳細な RTE ツールバーのほかに、ダイアログ内で使用可能なオプションとコンポーネントも提供されます。このモードは、他のコンポーネントと共に RTE を含むダイアログにのみ適用されます。

![タッチ操作 UI のフルスクリーンモードで編集するときに表示される、詳細な RTE ツールバー](assets/chlimage_1-37.png)

*図：タッチ対応UIのフルスクリーンモードでの編集時の詳細なRTEツールバー*

### ダイアログ編集 {#dialog-editing}

コンポーネントをダブルクリックすると、コンテンツ編集用のダイアログボックスが開きます。既存のページの上面に開きます。一部のシナリオでは、ポップアップウィンドウとして開くこともあります。例えば、複数列から成るページレイアウト内の列の一部がテキストコンポーネントで、ダイアログ用の領域が少ない場合などです。

![タッチ操作向け UI のダイアログ編集モード](assets/dialog_editing_modetouchui.png)

*図：タッチ対応UIのダイアログ編集モード*

![編集用の詳細なツールバーを含む、クラシック UI のダイアログボックス](assets/chlimage_1-38.png)

*図：編集用の詳細なツールバーが含まれるクラシックUIのダイアログボックス*

## RTE プラグインと関連機能について {#aboutplugins}

この機能は、一連のプラグインを介して使用可能になります。各プラグインには以下が含まれます。

* プロパティ `features` :

   * プラグインの基本機能をアクティベートまたはアクティベート解除するために使用
   * 標準化された手順を使用して設定可能

* 必要に応じて、追加のプロパティやオプションに特別な設定が必要です。

RTE の基本機能は、該当するプラグインのノードにある `features` プロパティの値によって、アクティベートまたはアクティベート解除されます。

以下の表に最新のプラグインを示します。

* API ドキュメントへのリンクを含むプラグイン ID。ID は、[プラグインをアクティベート](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)するときにノード名として使用されます。
* `features` プロパティの許可されている値。
* プラグインが提供する機能の説明。

| プラグイン ID | 機能 | 説明 |
|--- |--- |--- |
| edit | cut copy paste-default paste-plaintext paste-wordhtml | [切り取り、コピーおよび 3 つの貼り付けモード](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | find replace | 検索と置換。 |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | bold italic underline | [基本的なテキストフォーマット](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles)。 |
| [image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | 画像 | 基本的な画像サポート（コンテンツまたはコンテンツファインダーからのドラッグ）。ブラウザーの種類に応じて、様々なサポート機能が提供されます |
| [keys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | この値を定義するには、[タブサイズ](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize)を参照してください。 |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | justifyleft justifycenter justifyright | 段落の整列。 |
| [links](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | modifylink unlink anchor | [ハイパーリンクおよびアンカー](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles)。 |
| [lists](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | ordered unordered indent outdent | このプラグインは、[インデントとリスト](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin)（ネストされたリストを含む）の両方を制御します。 |
| [misctools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | 各種ツールを使用して、[特殊文字](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar)の入力や HTML ソースの編集をおこなうことができます。また、独自のリストを定義する場合は、[特殊文字の範囲](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar)全体を追加できます。 |
| Paraformat | paraformat | `<h2>`デフォルトの段落形式は、段落、見出し 1、見出し 2 および見出し 3（`<p>`、`<h1>`、`<h3>`）です。[他の段落フォーマットを追加](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats)したり、リストを拡張したりできます。 |
| spellcheck | checktext | [言語ごとのスペルチェッカー](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict)。 |
| styles | styles | CSS クラスを使用したスタイル設定のサポート。テキストで使用するスタイルの範囲を独自に追加（または拡張）する場合は、[新しいテキストスタイルを追加](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles)します。 |
| subsuperscript | subscript superscript | 下付き文字や上付き文字を追加して基本的なフォーマットを拡張。 |
| table | table removetable insertrow removerow insertcolumn removecolumn cellprops mergecells splitcell selectrow selectcolumns | テーブル全体または個々のセルに独自のスタイルを追加する場合は、[テーブルスタイルの設定](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)を参照してください。 |
| undo | undo redo | [取り消しおよびやり直し](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory)操作の履歴サイズ。 |

>[!NOTE]
>
>フルスクリーンプラグインは、ダイアログモードではサポートされません。Use of the `dialogFullScreen` setting to configure the toolbar for full screen mode.

## 設定パスと設定の場所について {#understand-the-configuration-paths-and-locations}

作成者に提供する [RTE 編集のモード（および UI）](#editingmodes)によって、[RTE プラグインをアクティベート](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin)するときの設定詳細の場所が決まります。

| 編集モード | タッチ UI の場所 | クラシック UI の場所 |
|---|---|---|
| インライン | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| フルスクリーン | `cq:editConfig/cq:inplaceEditing` | 適用なし |
| ダイアログ | `cq:dialog` | `dialog` |
| フルスクリーンダイアログ | `cq:dialog` | 適用なし |

>[!NOTE]
>
>`cq:inplaceEditing` の下のノードの名前を `config` にしないでください。`cq:inplaceEditing` ノードで、以下のプロパティを定義します。
>* **名前**：`configPath`
>* **型**：`String`
>* **値**：実際の設定を含むノードのパス

>
>
RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

ダイアログ編集モードで適用される次のプロパティを設定します（タッチ UI のみ）。

* `useFixedInlineToolbar`：RTE ツールバーをフロートではなく固定にするには、RTE ノード（sling:resourceType= `cq/gui/components/authoring/dialog/richtext` のもの）に定義されているこのブール値プロパティを `True` に設定します。

    このプロパティが true のときは、デフォルト動作により、リッチテキスト編集が「foundation-contentloaded」イベントで開始します。

   これを防ぐには、`customStart` プロパティを `True` に設定し、「rte-start」イベントを呼び出して RTE の編集を開始するようにします。このプロパティが true のときは、デフォルトの動作（クリック時に RTE が開始する）が機能しません。

* `customStart`：RTE を開始するタイミングを `True` イベントの呼び出しによって制御するには、RTE ノードに定義されているこのブール値プロパティを `rte-start` に設定します。

* `rte-start`：このイベントを RTE の `contenteditable-div`（RTE の編集を開始するタイミング）で呼び出します。これは、`customStart` が true に設定されている場合にのみ機能します。

タッチ操作ダイアログで RTE を使用する場合は、問題の発生を避けるために、プロパティ `useFixedInlineToolbar` に true を設定する必要があります。

## インプレイス編集のカスタマイズ {#customizing-in-place-editing}

次のプロパティを設定して、どのHTMLセレクターにテキストエディターの開始を定義できます。

* **`editElementQuery`**  — 定義のオン `cq:InplaceEditingConfig`では、このプロパティは、テキストコンポーネントのインライン編集を開始するHTML要素のセレクターを指定するために使用されます。 指定しなかった場合、インライン編集はテキストコンポーネントのHTMLで直接開始されます。
* **`textPropertyName`**  — このプロパティ `cq:InplaceEditingConfig`は、で定義され、インライン編集後にテキストコンポーネントのHTML値が保持されるコンテンツノードに保存されるプロパティの名前を指定するために使用されます。

ダイアログモードの対応するプロパティはで `name`す。

## プラグインのアクティベートによる RTE 機能の有効化 {#enable-rte-functionalities-by-activating-plug-ins}

リッチテキストエディター（RTE）の各機能は一連のプラグインから使用でき、それぞれに features プロパティがあります。features プロパティを設定することで、各プラグインの各種機能を有効化または無効化できます。

RTE プラグインの設定について詳しくは、[RTE プラグインのアクティベートおよび設定方法に関する説明](/help/sites-administering/configure-rich-text-editor-plug-ins.md)を参照してください。

**サンプル**:RTEの設定方法を説明する [サンプル設定](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) （英語のみ）をダウンロードしてください。 このパッケージではすべての機能が有効になっています。

>[!NOTE]
>
>テンプレートエディターで[コアコンポーネントのテキストコンポーネント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)を利用すると、技術的な設定をおこなうことなく、GUI で多くの RTE プラグインをコンテンツポリシーとして設定できます。コンテンツポリシーは、このドキュメントで説明するように RTE UI 設定と連携させることができます。
>
>詳しくは、このドキュメントの [RTE UI 設定とコンテンツポリシー](/help/sites-administering/rich-text-editor.md)のセクション、[ページテンプレートの作成](/help/sites-authoring/templates.md)および[コアコンポーネント開発者のドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/developing.html)を参照してください。

>[!NOTE]
>
>参照用として、デフォルトのテキストコンポーネント（標準インストールの一環として提供）が次の場所に用意されています。
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
独自のテキストコンポーネントを作成するには、上記のコンポーネントを直接編集するのではなく、コピーしてください。

## RTE ツールバーの設定 {#dialogfullscreen}

AEM では、リッチテキストエディターのインターフェイスを編集モードごとに異なる設定にできます。デフォルト設定を以下に示します。これらの設定を必要に応じて上書きできます。作成者に提供するツールバー機能のみをカスタマイズします。すべてのツールバー設定を指定する必要はありません。

`dialogFullScreen` 用のツールバーを設定するには、次のサンプル設定を使用します。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

インラインモードとフルスクリーンモードでは別の UI 設定が使用されます。ツールバープロパティは、ツールバーのボタンの指定に使用します。

For example, if the button is itself a feature (for example, `Bold`), it is specified as `PluginName#FeatureName` (for example, `links#modifylink`).

If the button is a popover (containing some features of a plug-in), it is specified as `#PluginName` (for example, `#format`).

Separators (`|`) between a group of buttons can be specified with `-`.

インラインまたはフルスクリーンモードのポップアップノードには、使用するポップオーバーのリストが含まれます。「popovers」ノードの下の各子ノードは、プラグインの名前を取って名付けられます（例：format）。プラグインの機能のリストが含まれるプロパティ「items」があります（例：format#bold）。

## RTE ユーザーインターフェイス設定とコンテンツポリシー {#rtecontentpolicies}

管理者は、上述のような設定をおこなわなくても、コンテンツポリシーを使用して RTE オプションを制御することができます。コンテンツポリシーでは、[編集可能テンプレート](/help/sites-authoring/templates.md)の一部として使用されるコンポーネントのデザインプロパティが定義されます。例えば、RTE を使用するテキストコンポーネントが編集可能テンプレートで使用される場合は、コンテンツポリシーの定義によって、太字オプションやいくつかの段落フォーマットオプションを使用可能にできます。コンテンツポリシーは再利用が可能であり、複数のテンプレートに対して適用できます。

RTE フローで使用可能なオプションに関するユーザーインターフェイス設定がコンテンツポリシーに影響します。

* ユーザーインターフェイス設定では、コンテンツポリシーで使用可能なオプションを定義します。
* RTE のユーザーインターフェイス設定が削除されたか、どの項目も有効にしていない場合、コンテンツポリシーではその設定ができません。
* 作成者は、ユーザーインターフェイス設定およびコンテンツポリシーによって使用可能となっている機能にのみアクセスできます。

例については、[テキストコアコンポーネントのドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/components/text.translate.html#the-text-component-and-the-rich-text-editor)を参照してください。

## ツールバーアイコンとコマンドのマッピングのカスタマイズ {#iconstoolbar}

RTE ツールバーに表示される Coral アイコンと使用可能なコマンドとのマッピングをカスタマイズできます。Coral アイコンに加えて他のアイコンを使用することはできません。

1. `icons` の下に、`uiSettings/cui` という名前のノードを作成します。

1. そのノードの下に、各アイコンのノードを作成します。
1. 個々のアイコンノードで、Coral アイコンとそのアイコンにマッピングするコマンドを指定します。

以下に、`textItalic` という名前の Coral アイコンにコマンド「Bold」をマッピングするサンプルスニペットを示します。

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## CoralUI 2 リッチテキストエディターへの切り替え {#switch-to-coralui-rich-text-editor}

ページに、CoralUI 2 RTE clientlibまたはCoralUI 3 RTE clientlibを含めることができます。 デフォルトでは、リッチテキストエディターには CoralUI 3 RTE clientlib が含まれています。CoralUI 2 RTE に切り替えるには、次の手順を実行します。

>[!NOTE]
>
>この方法は、ベストプラクティスとしてお勧めするものではありません。CoralUI 2 RTE への切り替えは最後の手段です。CoralUI 2 RTE用のカスタムプラグインは、プラグインがクラスなどのRTE内部に依存しない場合、CoralUI 3 RTEで機能します。
>
>CoralUI RTE のカスタムプラグインを使用する場合は、`rte.coralui3`3 ライブラリを使用してください。


1. ノードを下にオーバーレイし `/libs/cq/gui/components/authoring/editors/clientlibs/core``/apps`、次の操作を行います。

   * Replace `rte.coralui3` with `rte.coralui2` for the dependencies property.
   * Replace `cq.authoring.editor.core.inlineediting.rte.coralui3` with `cq.authoring.editor.core.inlineediting.rte.coralui2` for the embed property.
   * Replace `cq.authoring.rte.coralui3` with `cq.authoring.rte.coralui2` for the embed property.

1. ノードをオーバーレイし、ノード `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` の下 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` に重ね `/apps`ます。

   からカテゴリ `cq.authoring.dialog` を削除 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` し、に追加し `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`ます。

1. ページに含まれている他の依存関係を `rte.coralui3` から `rte.coralui2` に変更します。For example, after overlaying the node `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` under `/apps`, change any dependency on it from `rte.coralui3` to `rte.coralui2`.

1. Overlay the node `cq/ui/widgets` under `/apps`. ノード `cq.rte` の依存関係をに置き換え `/apps/cq/ui/widgets` ま `cq.coralui2.rte`す。

>[!NOTE]
>
>CoralUI 2 RTE は、プラグインダイアログのハンドルバーテンプレートを使用します。そのため、CoralUI 2 RTE clientlib は、ハンドルバー clientlib に対して依存関係があります。CoralUI 3 RTE は、ハンドルバーテンプレートを使用しないので、関連する依存関係はありません。カスタムプラグインがハンドルバーテンプレートを使用する場合、Web ページにハンドルバー clientlib を含めます。

## その他の情報 {#further-information}

RTE の設定について詳しくは、[AEM ウィジェット API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) リファレンスを参照してください。

特に、使用可能なプラグインおよび関連オプションを確認するには、以下を参照してください。

* [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) コンポーネントは、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドを提供します。リッチテキストフォームに使用可能なすべてのパラメーターについては、「設定オプション」を参照してください。
* The RichText component provides a wide range of functionality using plug-ins listed under [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). For each plug-in:

   * 有効化（または無効化）が可能な機能の詳細については「機能」を参照してください。
   * 該当するプラグインの詳細設定に使用可能なすべてのパラメーターについては、「設定オプション」を参照してください。

* リンクの HTML ルールに関する詳細も参照できます。

これらは、独自のRTEを拡張およびカスタマイズするために使用できます。 例えば、リンク作成時にページで使用できるアンカーをリストするために、`LinkPlugin` を独自に実装できます。

## 既知の制限事項 {#known-limitations}

AEM RTE 機能には次の制限があります。

* RTE 機能は AEM コンポーネントダイアログでのみサポートされます。RTE は、ウィザードやタッチ操作向け UI の基盤フォーム（[ページプロパティ](/help/sites-developing/page-properties-views.md)や[基礎モード](/help/sites-authoring/scaffolding.md)など）ではサポートされません。

* AEM は[ハイブリッドデバイス](/help/release-notes/known-issues.md)では機能しません。

* RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ有効になり、グループ `content-author` のユーザーに対して有効になりません。

* RTE は、コンテンツを埋め込むインラインフレームまたは iframe をサポートしていません。

## ベストプラクティスとヒント {#best-practices-and-tips}

* フローティングダイアログのポップアップを表示しない場合は、プラグインのみを有効にします。 ポップアップなしのプラグインはサイズが小さく、フローティングダイアログに最適です。
* `Paste` プラグインなど、大きめのポップアップがあるプラグインは、フルスクリーンダイアログモードまたはフルスクリーンモードでのみ有効にします。大きなポップアップがあるプラグインは、優れたオーサリング環境を提供するために、より多くのスクリーンスペースを必要とします。
* CoralUI RTE のカスタムプラグインを使用する場合は、`rte.coralui3`3 ライブラリを使用してください。

## RTEに関する頻繁な問題のトラブルシューティング {#troubleshoot-issues-with-aem-rich-text-editor}

**複数のテーブルセルを選択する方法を教えてください。**

To select multiple cells in a table, press `Ctrl` or `Cmd` key and then click the table cells one-by-one.

選択したセルのプロパティを設定するなどして操作を実行します。

**「設定」ボタンを使用してコンポーネントを編集すると、ハイパーリンクが失われてしまう**

「設定」ボタンを使用してテキストコンポーネントを編集することによって、ハイパーリンクを追加します。もう一度編集して、再びハイパーリンクを検証すると、ハイパーリンクが失われることがあります。

回避策は、編集ダイアログが 2 度目に表示されたときに、テキストコンポーネントをクリックしてから、リンク検証を実行します。

この問題は AEM 6.3 以降で解決されています。

**ソース編集モードで追加された HTML コンテンツが失われてしまう**

XSS が発生しやすい HTML を追加しないでください。RTE ではなく AEM は、XSS AntiSamy ルールに準拠するために HTML コンテンツを削除することがあります。

貼り付けた HTML が保存されていることを確認するには、（コンテンツノードの）CRXDE で保存されたコンテンツを確認します。

保存されていない場合、HTML は RTE の規則に準拠していなかったため、RTEによって削除されたということです。

If saved in CRXDE but not rendered on the Page (to check rendering, see page&#39;s [preview](/help/sites-authoring/editing-content.md#preview-mode), it is removed by AEM XSS rules.

**マルチフィールドコンポーネントが期待どおりに機能しない**

マルチフィールドコンポーネントを作成するには、CoralUI 3 のみを使用してください。CoralUI 2 コンポーネントダイアログを使用しないでください。

また、マルチフィールド実装コードとノード構造が正しいことを確認してください。

**管理者が利用できる設定を、作成者が利用できない**

インターフェイス設定の更新が管理者には反映されているが作成者アカウントには反映されていない場合、設定ノードに `config` という名前が付けられていないか確認してください。Use the [`configPath` property](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [RTE プラグインの設定](configure-rich-text-editor-plug-ins.md)
>* [リッチテキストエディターをオーサリングに使用](../sites-authoring/rich-text-editor.md)
>* [RTE をアクセス可能なサイト用に設定](rte-accessible-content.md)
>* [タッチ UI とクラシック UI 機能の類似点](../release-notes/touch-ui-features-status.md)
>* [複合マルチフィールドコンポーネントを作成するためのチュートリアルサンプル](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

