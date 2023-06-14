---
title: xtype の使用（クラシック UI）
description: AEMで使用できるすべての xtype について説明します
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 74%

---

# xtype の使用（クラシック UI）{#using-xtypes-classic-ui}

このページでは、Adobe Experience Manager(AEM) で使用できるすべての xtype について説明します。

ExtJS 言語では、xtype はクラスに付与されるシンボル名です。xtype とその使用方法について詳しくは、[ExtJS 2 の概要](https://www.sencha.com/learn/overview-of-extjs-2)の「Component XTypes」の段落を参照してください。

AEM で利用できるすべてのウィジェットの完全な情報については、[ウィジェット API のドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)を参照してください。

AEM で特定の xtype が使用されるコンポーネントを探すには、CRXDE で次の Xpath クエリを使用します。その際、「checkbox」を検索する xtype に置き換えます。

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>このページでは、クラシック UI での ExtJS xtype の使用方法について説明します。
>
>アドビでは、[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)および[Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components)に基づく標準の最新の[タッチ対応UI](/help/sites-developing/touch-ui-concepts.md)を活用することをお勧めします。

## xtypes {#xtypes}

以下に、Adobe Experience Managerで使用可能な xtype のリストを示します。

* 注釈

  [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

  Dialog は、ボディにフォーム、フッターにボタングループを備える特殊なウィンドウです。通常はコンテンツの編集に使用されますが、情報の表示にも使用できます。

* arraystore

  [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

  以前は「SimpleStore」と呼ばれていました。

  作成する小さなヘルパークラス [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)は、より簡単に配列データから取得できます。 ArrayStore は [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

  [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

  DAM 管理画面で使用されるアセットエディターです。

* assetreferencesearchdialog

  [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

  AssetReferenceSearchDialog は、ページがアセットまたはタグを参照する場合にポップアップ表示されるダイアログです。

* blueprintconfig

  [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

  BlueprintConfig は、ブループリントのライブコピーを表示したり、このブループリントのプロパティ（同期トリガーと同期操作）を編集したりするパネルを提供します。

* blueprintstatus

  [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

  BlueprintStatus は、ブループリントとライブコピーの関係を表示および編集できるパネルを提供します。参照は [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree)、 [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) および [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

  [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

  任意のの基本クラス [コンポーネント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) 幅と高さを使用して、ボックスとしてサイズを設定する

  BoxComponent は、サイズと位置の調整を自動的に行うボックスモデルを提供し、コンポーネントレンダリングモデル内で正しく機能します。

* browsedialog

  [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

  BrowseDialog により、ユーザーはパスを選択するためにリポジトリを参照できます。通常、 [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

  [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

  **非推奨：代わりに [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) を使用**

* bulkeditor

  [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

  BulkEditor は、検索エンジンと、検索結果を編集するためのグリッドを提供します。

  BulkEditor は、インポート機能で必要なHTMLフォームに挿入する必要があります。 これは、 [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

  [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

  BulkEditorForm は、HTML フォームで囲まれた [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) を提供します。これは、のスタンドアロンバージョンです [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)、読み込みボタンにはHTMLフォームが必要です。

* button

  [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

  シンプルな Button クラス

* buttongroup

  [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

  ボタングループのためのコンテナ。

* chart

  [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

  CQ.Ext.chart パッケージは、Flash ベースのグラフを使用したデータの視覚化を実現します。各グラフは、CQ.Ext.data.Store に直接バインドされ、グラフの自動更新が可能です。 グラフの外観を変更するには、 [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) および [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) 設定オプション。

* チェックボックス

  [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

  単一チェックボックスフィールド。従来のチェックボックスフィールドの直接置き換えとして使用できます。

* checkboxgroup

  [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

  のグループ化コンテナ [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) コントロール

* clearcombo

  [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

  ClearableComboBox は、値を消去するトリガーを持つ、編集できないコンボボックスです。

* colorfield

  [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

  ColorField は、ユーザーが直接または[CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu)を使用して色の hex 値を入力できるようにします。

* colorlist

  [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   ColorList は、ユーザーが編集可能なリストから色を選択できるようにします。

* colormenu

  [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

  を含むメニュー [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) コンポーネント。

* colorpalette

  [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

  色を選択するためのシンプルなカラーパレットクラス。パレットはどのコンテナにもレンダリングできます。

* combo

  [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

  オートコンプリート、リモート読み込み、ページング、その他の多くの機能をサポートするコンボボックスコントロール。

  ComboBox は、従来のHTMLと同様の方法で動作します &lt;select> フィールドに入力します。 違いは、 [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)を指定する場合は、 [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) 非表示の入力を作成します。

* component

  [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

  すべての Ext コンポーネントの基本クラス。 コンポーネントのすべてのサブクラスは、 [コンテナ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) クラス。 コンポーネントは、 [項目](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) config オプションを使用します。

* componentextractor

  [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

  ComponentExtractor は、ユーザーが web サイト／ページからコンポーネントを抽出できるようにします。

* componentselector

  [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

  グループ化され、順序付けされた利用可能なコンポーネント群。

* componentstyles

  [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

  [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

  1 つのフォームフィールドまたはフォームフィールドのグループを含む、パネルをベースとした複雑なフォームフィールドの基本クラス。

* container

  [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

  任意のの基本クラス [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) 他のコンポーネントを含む可能性がある コンテナは、項目を含む基本的な動作（項目の追加、挿入、削除）を処理します。

  最も一般的に使用される Container クラスは、 [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) および [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

  [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

  ContentFinder は特殊な 2 列です [ビューポート](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) これには、実際のコンテンツファインダーが左側に、コンテンツフレームが右側に含まれています。

* contentfindertab

  [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

  ContentFinderTab は、 [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). 通常、検索フォーム（クエリボックス）と、検索を表示するデータビューが特徴です。

* cq.workflow.model.combo

  [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

  WorkflowModelCombo は、利用できるワークフローモデルのリストを表示する、カスタマイズされた [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) です。

* cq.workflow.model.selector

  [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

  WorkflowModelSelector は、WorkflowModelCombo を、ワークフローのサムネール画像のほか、ワークフローモデルの作成および編集のためのボタンと組み合わせたものです。

* createsitewizard

  [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

  CreateSiteWizard は、（MSM）サイトを作成するためのステップバイステップ方式のウィザードです。

* createversiondialog

  [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

  CreateVersionDialog は、新しいバージョンのページを作成できるダイアログです。

* customcontentpanel

  [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

  CustomContentPanel は、[CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) で使用するための特殊なパネルです。CustomContentPanel のコンテンツは、ダイアログ内のその他のフィールドとは異なる URL から取得および送信されます。

* cycle

  [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

  [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) 要素のメニューを含む専用の SplitButton。このボタンは、アクティブなメニューアイテムに対してボタンの [change](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) イベントを生成しながら（または指定されている場合は、ボタンの [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) 関数を呼び出しながら）、クリックで各メニューアイテムを循環します。

* dataview

  [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

  カスタムレイアウトテンプレートと書式設定を使用してデータを表示するメカニズム。DataView は、内部テンプレートのメカニズムとして [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) を使用し、[CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) にバインドされます。ストア内のデータが変更されると、ビューは変更を反映して自動的に更新されます。

* datefield

  [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) ドロップダウンと自動日付検証機能を備えた日付入力フィールドを提供します。

* datemenu

  [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

  次を含むメニュー： [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) コンポーネント。

* datepicker

  [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

  ポップアップの日付選択。 このクラスは、 [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) クラスを使用して、有効な日付の参照と選択を許可します。

* datetime

  [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

  DateTime は、[CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)と[CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)を組み合わせて、ユーザーが日付と時刻を入力できるようにします。

* dialog

  [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

  Dialog は、ボディにフォーム、フッターにボタングループを備える特殊なウィンドウです。通常はコンテンツの編集に使用されますが、情報の表示にも使用できます。

* dialogfieldset

  [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

  DialogFieldSet は、[Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) で使用される [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) です。

* directstore

  [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

  小さなヘルパークラスを使用して [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) で構成される [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) および [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) を操作する [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) サーバーサイド [プロバイダー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) より簡単に

* displayfield

  [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

  検証されることも送信されることもない、表示専用のテキストフィールド。

* editbar

  [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

  EditBar は、ユーザーがバーのボタンを使用してコンテンツを編集できるようにします。

  ここには記載されていませんが、EditBar には [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* エディター

  [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

  要求に応じて表示／非表示を処理し、いくつかの組み込みのサイズ変更およびイベント処理ロジックを持つ基本エディターフィールド。

* editorgrid

  [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

  このクラスは、 [GridPanel クラス](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) 選択したセルの編集を行うには [列](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). 編集可能な列は、 [編集者](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) 内 [列設定](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

  [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

  EditRollover を使用すると、ユーザはダブルクリックでコンテンツを編集でき、コンテキストメニューからさらに編集操作を実行できます。 編集可能な領域は、マウスがコンテンツをロールオーバーすると、フレームで示されます。

* feedimporter

  [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

  FeedImporter は、ユーザーが RSS／Atom フィードをインポートし、フィードエントリごとにページを作成できるようにします。

* field

  [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

  フォームフィールドの基底クラスであり、デフォルトのイベントの処理、サイズ設定、値の処理およびその他の機能を提供します。

* fieldset

  [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

  [フォーム](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)内のアイテムのグループ化に使用される標準コンテナ。

* fileuploaddialogbutton

  [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

  FileUploadDialogButton は、FileUploadField を使用してファイルをアップロードするための新しいダイアログを開くボタンを作成します。アップロードを別のフォームで実行する必要がある編集ダイアログ内で使用できます。

* fileuploadfield

  [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

  FileUploadField は、ユーザーがアップロードする単一のファイルを選択できるようにします。

* findreplacedialog

  [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

  FindReplaceDialog はページおよびその子ページでトークンを検索し、置換するためのダイアログです。

* flash

  [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* grid

  [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

  このクラスは、行と列の表形式でデータを表示する、コンポーネントをベースにしたグリッドコントロールのプライマリインターフェイスを表示します。

* groupingstore

  [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

  利用可能なフィールドの 1 つでレコードをグループ化できるようにする、専用のストア実装。これは通常、 [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) を使用して、グループ化された GridPanel のデータモデルを検証します。

* heavymovedialog

  [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog は、ページとその子ページを移動するためのダイアログであり、以前アクティブ化したページの再アクティブ化も考慮に入れます（名前の「heavy」はこれを表しています）。

* hidden

  [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

  フォームの送信で渡す必要があるフォーム内の非表示の値を格納するための、基本的な非表示フィールド。

* historybutton

  [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

  HistoryButton は、前後のボタンを簡単に提供する小さなヘルパークラスです。 通常、関連する 2 つのインスタンスが必要です。進むボタンインスタンスは、履歴を処理する戻るボタンインスタンスにリンクされた単純なボタンです。

* htmleditor

  [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   軽量の HTML エディターコンポーネントを提供します。一部のツールバー機能は Safari ではサポートされておらず、必要に応じて自動的に非表示になります。 これらは、必要に応じて設定オプションに記載されます。

  エディターのツールバーボタンには、[buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) プロパティで定義されたツールチップがあります。

* iframedialog

  [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   iframe のコンテンツを表示したり、iframe でフォームを許可したりするプレーンダイアログ。

* iframepanel

  [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

  iframe を含むパネル。iframe の作成、iframe 読み込みイベントの作成が容易になり、iframe のコンテンツに簡単にアクセスできます。

* inlinetextfield

  [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

  InlineField は、フォーカスされていないときにラベルとして表示されるテキストフィールドです。

* jsonstore

  [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

  作成する小さなヘルパークラス [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)を JSON データから簡単に取得できます。 JsonStore は、 [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

  [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   基本ラベルフィールド。

* languagecopydialog

  [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog は、言語ツリーをコピーするためのダイアログです。

* linkchecker

  [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

  linkchecker は、サイト内の外部リンクを確認するためのツールです。

* listview

  [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

  CQ.Ext.list.ListView は、 [グリッド](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ビューと同じ。

* livecopyproperties

  [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

  LiveCopyProperties は、ライブコピープロパティ（関係の継承、同期のトリガー、同期操作）を表示および編集できるパネルを提供します。

* lvbooleancolumn

  [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

  ブールデータフィールドをレンダリングする Column 定義クラスです。 詳しくは、 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の設定オプション [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) を参照してください。

* lvcolumn

  [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

  このクラスは、 [リスト表示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

  [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

  デフォルトのロケールまたは設定済みのロケールに従って渡された日付をレンダリングする Column 定義クラス [形式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). 詳しくは、 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の設定オプション [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) を参照してください。

* lvnumbercolumn

  [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

  数値データフィールドを [形式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 文字列。 詳しくは、 [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の設定オプション [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) を参照してください。

* mediabrowsedialog

  [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

  **非推奨：代わりに[コンテンツファインダー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)を使用して、メディアを参照してください。**

  MediaBrowseDialog は、メディアライブラリを参照するためのダイアログです。

* メニュー

  [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

  メニューオブジェクト。 これは、メニュー項目を追加できるコンテナです。 メニューは、別のコンポーネント ( [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) 例：

  メニューには、次のいずれかを含めることができます。 [メニュー項目](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)または一般 [コンポーネント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* menubaseitem

  [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

  メニューにレンダリングするすべてのアイテムの基本クラス。BaseItem は、デフォルトのレンダリング、アクティブ化された状態の管理、すべてのメニューコンポーネントで共有される基本構成オプションを提供します。

* menucheckitem

  [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   デフォルトでチェックボックス（ラジオグループの一部である可能性もあります）を含むメニューアイテムを追加します。

* menuitem

  [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

  メニュー関連の機能（サブメニューなど）を必要とし、静的表示アイテムではないすべてのメニューアイテムの基底クラス。項目は、 [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) メニュー固有のアクティベーションを追加し、「処理」をクリックします。

* menuseparator

  [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

  メニューに区切りバーを追加します。区切りバーは、メニューアイテムを論理的なグループに分けるために使用されます。通常は、add() を呼び出す際に&quot;-&quot;を使用し、直接作成するのではなく、アイテム設定に追加します。

* menutextitem

  [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

  通常は見出しやグループ区切りとして使用される静的テキスト文字列をメニューに追加します。

* メタデータ

  [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

  メタデータは、アセットエディターのページなどで使用されるメタデータフィールドに必要な情報を決定するための一連のフィールドを提供します。

  次のフィールドを提供します。

* multifield

  [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

  MultiField は、複数値のプロパティを編集するための編集可能なフォームフィールドのリストです。

* mvt

  [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

  多変量分析テストコンポーネントを使用して、代替バナーとして表示される画像のセットを定義および編集できます。 クリックスルー率の統計は、バナーごとに収集されます。

* notificationinbox

  [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

  NotificationInbox は、ユーザーが WCM アクションをサブスクライブし、通知を管理できるようにします。

* numberfield

  [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

  自動でのキーストロークのフィルター処理および数値の検証を提供する数値テキストフィールド。

* offlineimporter

  [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

  OfflineImporter は、Microsoft Word ドキュメントを AEM ページにインポートして変換するツールです。この機能により、ワード プロセッサを使用してオフラインでコンテンツを編集することができます。

* ownerdraw

  [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

  OwnerDraw には、カスタム HTML コードを含めることができます（直接入力するか、URL から取得します）。

* paging

  [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

  レコードの量が増えると、ブラウザーでレンダリングするのに必要な時間が長くなります。 ページングは、クライアントとやり取りされるデータの量を減らすために使用されます。

* panel

  [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

  パネルは、特定の機能と構造コンポーネントを備えたコンテナで、アプリケーション指向のユーザーインターフェイスに最適な構成要素です。

  パネルは、次からの継承により、 [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragraphreference

  [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

  段落の参照フィールドでは、ページを閲覧したり、段落の 1 つを選択したりできます。これは、トリガーフィールドと関連する段落参照ダイアログで構成されます。

* パスワード

  [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

  Password は [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) に似ていますが、ユーザーが機密データを入力できるように、値を非公開に保ちます。

* pathcompletion

  [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

  **非推奨：代わりに [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) を使用してください。**

* pathfield

  [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

  PathField は、パス補完とボタンを使用して、パスを開くための入力フィールドです [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) サーバリポジトリを参照するために使用します。 また、高度なリンク生成のためにページの段落を参照することもできます。

* progress

  [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

  更新可能なプログレスバーコンポーネント。 プログレスバーは、次の 2 つの異なるモードをサポートします。手動と自動。

  手動モードでは、( [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) をクリックし、必要に応じて独自のコードからプログレスバーをクリアします。 この方法は、進行状況を表示する場合に最も適しています。

* propertygrid

  [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

  開発 IDE によくあるような従来型のプロパティグリッドを模した、専用のグリッドの実装。グリッドの各列には、いくつかのオブジェクトのプロパティが表示され、このデータは [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord) に名前／値のペアのセットとして格納されます。

* propgrid

  [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid は、オブジェクトのプロパティの表示と編集に使用される汎用グリッドです。

* quicktip

  [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip は、マークアップで指定され、グローバル [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) インスタンスによって自動的に管理されるツールチップのための専用のツールチップクラスです。その他の使用方法の詳細と例については、 QuickTips クラスのヘッダーを参照してください。

* 無線

  [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   単一ラジオフィールド。「チェックボックス」と同じですが、入力タイプを自動的に設定する便利さを考慮して提供されます。 グループ内の各ラジオに同じ名前を付けると、ラジオのグループ化はブラウザーによって自動的に処理されます。

* radiogroup

  [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) コントロールのグループ化コンテナ。

* referencesdialog

  [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   ReferencesDialog は、ページでリファレンスを表示するためのダイアログです。

* restoretreedialog

  [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog は、ツリーの以前のバージョンを復元するためのダイアログです。

* restoreversiondialog

  [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog は、ページの以前のバージョンを復元するためのダイアログです。

* richtext

  [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

  RichText は、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドを提供します。

  RichText コンポーネントは現在、次の機能を提供しています。

* rolloutplan

  [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

  RolloutPlan は、ページロールアウトの進捗状況を確認するためのダイアログを表示します。RolloutPlan は [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutward

  [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

  RolloutWizard は、ページロールアウトのためのウィザードを表示します。RolloutWizard は、 [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

  [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

  SearchField は、リポジトリーの検索に使用でき、検索結果をドロップダウンリストで示す検索フィールドを表示します。

* selection

  [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

  Selection を使用すると、ユーザーが選択できる複数のオプションを設定できます。オプションは、設定の一部でも JSON 応答から読み込むこともできます。 「選択」は、ドロップダウン（選択）またはコンボボックス（選択とフリーテキストの入力）としてレンダリングできます。

* サイドキック

  [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

  Sidekick は、ページ編集でよく使うツールをユーザーに提供するフローティングヘルパーです。

* siteadmin

  [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

  SiteAdmin は、WCM 管理関数を提供するコンソールです。

* siteimporter

  [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

  SiteImporter は、ユーザーが完全な Web サイトを読み込み、最初のプロジェクトを作成できるようにします。

* sizefield

  [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

  SizeField は、ユーザーが（例えば画像に対して）幅と高さを入力できるようにします。

* slider

  [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

  垂直方向または水平方向、キーボードの調節、設定可能なスナップ、軸のクリックおよびアニメーションをサポートする Slider。任意のコンテナに項目として追加できます。 使用例：...

* slideshow

  [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

  スライドショーには、スライドショーとして表示できる一連の画像や画像タイトルを定義および編集するために使用できるコンポーネントが用意されています。

  スライドショーコンポーネントは、 [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) コンポーネント。

* smartfile

  [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

  SmartFile はインテリジェントファイルアップローダです。

  Flashプラグイン（バージョン 9 以降）がインストールされている場合、アップロードは SWFupload ライブラリを使用して実行され、アップロードを処理するのに便利です。

* smartimage

  [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

  SmartImage は、インテリジェントな画像アップローダです。 アップロードされた画像を処理するツール（例えば、画像マップを定義するツールや画像クロッパー）を提供します。

  このコンポーネントは、主に別のダイアログタブで使用するように設計されています。

* spacer

  [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

  レイアウト内にサイズの大きいスペースを提供するために使用します。

* spinner

  [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

  スピナーは、数値、日付、時間の値のトリガーフィールドです。 上下のトリガー、スクロールホイールまたはキーを使用すると、値を増減できます。

* splitbutton

  [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

  デフォルトのボタンのクリックイベントとは別に、イベントを発生させることのできる組み込みのドロップダウン矢印を提供する分割ボタン。これは通常、プライマリボタンのアクションに追加のオプションを提供するドロップダウンメニューの表示用に使用されます。ただし、カスタムハンドラーにより、矢印クリックの実装を提供できます。

* static

  [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

  Static は、任意のテキストまたは HTML を表示するために使用できます。

* statistics

  [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

  Statistics は、ページインプレッション数をグラフとして表示します。ウィジェットを使用して期間を選択でき、統計を表示する必要があります。

* store

  [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

  Store クラスは、[GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)、[ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)、[DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView) などのコンポーネントの入力データを提供する [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) オブジェクトのクライアントサイドキャッシュをカプセル化します。

* suggestfield

  [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   SuggestField は、ユーザーの入力に基づいた候補を提供します。

* switcher

  [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

  Switcher のコンソールにあるヘッダーバー用のボタングループでは、web サイト、デジタルアセット、ツール、ワークフローおよびセキュリティを切り替えることができます。

* tableedit

  [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

  **非推奨：代わりに [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) を使用してください。**

* tableedit2

  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

  TableEdit2 は、テーブルを作成するためのウィジェットを提供します。

* tabpanel

  [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

  基本のタブコンテナ。TabPanel は、レイアウトを目的として、標準の [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) と同じように使用できますが、子コンポーネントを含めるための特別なサポートもあります（[`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)）。

* タグ

  [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

  ```
  CQ.tagging.TagInputField
  ```

   は、タグを入力するためのフォームウィジェットです。既存のタグから選択できるポップアップメニューを備えており、自動入力などの機能もあります。

* textarea

  [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

  multiline（テキストフィールド）従来のテキスト領域フィールドの直接置き換えとして使用できます。また、自動サイズ調整のサポートが追加されました。

* textbutton

  [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

  TextButton は、[CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button) の機能を備えたテキストリンクを提供します。

* textfield

  [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

  基本テキストフィールド。 従来のテキスト入力の直接置き換えとして、またはより高度な入力コントロール ( [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) および [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)) をクリックします。

* thumbnail

  [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

  [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

  時刻のドロップダウンと自動時刻検証機能を備えた時刻入力フィールドを提供します。使用例：...

* チップ

  [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

  @xtype tip は、[CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) と [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) の基底クラスであり、すべてのヒントベースのクラスで必要な基本のレイアウトと配置を提供します。このクラスは、単純で静的に配置された tip に直接使用できます。

* titleseparator

  [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

  メニューに区切りバーを追加します。区切りバーは、メニューアイテムを論理的なグループに分けるために使用されます。区切り文字には、タイトルを追加で含めることができます。

* toolbar

  [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

  ツールバーの基本クラス。ツールバーの [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) は [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button) ですが、ツールバーの要素（ツールバーコンテナの子アイテム）には、ほとんどのタイプのコンポーネントを使用できます。ツールバー要素は、コンストラクタを使用して明示的に作成できます。

* tooltip

  [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

  ターゲット要素をポイントしたときに追加の情報を提供するための標準のツールチップの実装。@xtype tooltip.

* treegrid

  [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

  @xtype ツリーグリッド

* treepanel

  [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

  TreePanel は、ツリー構造の UI 表現をツリー構造で提供します。

  [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreePanel に追加されたには、アプリケーションで使用されるメタデータを [属性](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) プロパティ。

* trigger

  [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

  クリック可能なトリガーボタン（デフォルトでは、コンボボックスに似ています）を追加する TextField のための便利なラッパーを提供します。トリガーにはデフォルトのアクションがないので、上書きしてトリガーのクリックハンドラーを実装する関数を割り当てる必要があります [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). TriggerField は、コンボボックスと同じようにレンダリングされるので、直接作成できます。

* uploaddialog

  [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

  UploadDialog は、ユーザーがリポジトリにファイルをアップロードできるようにします。新しい UploadDialog を作成します。

* userinfo

  [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

  現在のユーザー名を表示するツールバーアイテムであり、ユーザーがプロパティや権限借用の編集などの操作を行えるようにします。

* viewport

  [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

  表示可能なアプリケーション領域（ブラウザーのビューポート）を表す専用のコンテナです。

  Viewport は、ドキュメントの本文に自身をレンダリングし、ブラウザのビューポートのサイズに自動的に合わせてサイズを調整し、ウィンドウのサイズ変更を管理します。 1 つのビューポートのみを作成できます。

* window

  [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

  アプリケーションウィンドウとして使用するための専用のパネル。 窓は浮いている。 [サイズ変更可能な](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)、および [ドラッグ可能な](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) デフォルトでは。 Windows は [最大化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) ビューポートを塗りつぶし、以前のサイズに復元するには、 [最小化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

  [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

  作成する小さなヘルパークラス [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)を XML データから簡単に取得できます。 XmlStore は [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

  **cqinclude** リポジトリ内の別のパスのウィジェットの定義を含む疑似 xtype。ページダイアログで最も一般的に使用されます。 この xtype に対する実際の JavaScript ウィジェットクラスはありません。 CQ.Util クラスの formatData() 関数によって処理されます。詳しくは、このナレッジベースの記事を参照してください。
