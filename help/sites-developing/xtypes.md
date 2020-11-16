---
title: xtype の使用（クラシック UI）
seo-title: xtype の使用（クラシック UI）
description: AEM で利用できるすべての xtype について説明します
seo-description: AEM で利用できるすべての xtype について説明します
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '6414'
ht-degree: 53%

---


# xtype の使用（クラシック UI）{#using-xtypes-classic-ui}

このページでは、Adobe Experience Manager（AEM）で利用できるすべての xtype について説明します。

ExtJS 言語では、xtype はクラスに付与されるシンボル名です。You can read the &quot;Component XTypes&quot; paragraph of the [Overview of ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) for a detailed explanation about what an xtype is and how it can be used.

AEM で利用できるすべてのウィジェットの完全な情報については、[ウィジェット API のドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)を参照してください。

AEM で特定の xtype が使用されるコンポーネントを探すには、CRXDE で次の Xpath クエリを使用します。その際、「checkbox」を検索する xtype に置き換えます。

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>このページでは、クラシック UI での ExtJS xtype の使用方法について説明します。
>
>Adobe recommends that you leverage the standard, modern, [touch-enabled UI](/help/sites-developing/touch-ui-concepts.md) based on [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) and [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtype {#xtypes}

Adobe Experience Manager で使用できる xtype の一覧を以下で確認してください。

* annotation

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

    Dialog は、ボディにフォーム、フッターにボタングループを備える特殊なウィンドウです。通常はコンテンツの編集に使用されますが、単に情報を表示するために使用されることもあります。

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   以前は「SimpleStore」として知られていました。

   配列データから [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) を簡単に作成できるようにする小規模なヘルパークラスです。ArrayStore には自動的に [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader) が設定されます。

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

    DAM 管理画面で使用されるアセットエディターです。

* assetreferencesearchdialog

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

    AssetReferenceSearchDialog は、ページがアセットまたはタグを参照する場合に開くダイアログです。

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

    BlueprintConfig は、ブループリントのライブコピーを表示したり、このブループリントのプロパティ（同期トリガーと同期操作）を編集したりするパネルを提供します。

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

    BlueprintStatus は、ブループリントとライブコピーの関係を表示および編集できるパネルを提供します。[CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree) を使用してブラウジングし、[CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) および [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)を使用して編集します。

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   [コンポーネント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)の基底クラスであり、幅と高さを使用して、ボックスとしてサイズを変更します。

   BoxComponent は、サイズと位置を自動的に調整するボックスモデルを提供し、コンポーネントのレンダリングモデルで正常に動作します。

* browsedialog

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

    BrowseDialog により、ユーザーはパスを選択するためにリポジトリを参照できます。通常は、[BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField) で使用されます。

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **廃止：代わりに [CQ.form.PathFieldを使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

    BulkEditor は、検索エンジンと、検索結果を編集するためのグリッドを提供します。

   BulkEditor は、HTML フォームに挿入する必要があります（インポート機能によって必須となっています）。[CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) で適切に動作します。

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

    BulkEditorForm は、HTML フォームで囲まれた [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) を提供します。[CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) のスタンドアロンバージョンであり、インポートボタンに HTML フォームが必要です。

* button

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   単純なボタンクラス

* buttongroup

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   ボタンのグループのコンテナ。

* chart

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

    CQ.Ext.chart パッケージは、Flash ベースのグラフを使用したデータの視覚化を実現します。各グラフは、CQ.Ext.data.Store に直接バインドされ、グラフの自動更新が可能になります。グラフの外観を変更するには、[chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) および [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) の設定オプションを確認します。

* チェックボックス

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   単一のチェックボックスフィールド 従来のチェックボックスフィールドにそのまま置き換えて使用できます。

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) コントロールのグループ化コンテナ。

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

    ClearableComboBox は、値を消去するトリガーを持つ、編集できないコンボボックスです。

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

    ColorField は、ユーザーが直接または [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu) を使用して色の hex 値を入力できるようにします。

* colorlist

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

    ColorList は、ユーザーが編集可能なリストから色を選択できるようにします。

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) コンポーネントを含むメニュー。

* colorpalette

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

    色を選択するためのシンプルなカラーパレットクラス。パレットはどのコンテナにもレンダリングできます。

* combo

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   オートコンプリート、リモートローディング、ページングなど、その他多くの機能をサポートするコンボボックスコントロール。

   ComboBox は、従来の HTML &lt;select>フィールドと同じように動作します。相違点として、[valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) を送信するために、非表示の入力フィールドを作成する [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) を指定する必要があります。

* component

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   すべての Ext コンポーネントの基底クラス。コンポーネントのすべてのサブクラスは、[Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) クラスによって提供される、Ext コンポーネントの自動化された作成、レンダリング、破棄のライフサイクルに参加できます。コンポーネントは、コンテナ作成時に、[items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) 設定オプションでコンテナに追加されます。

* componentextractor

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

    ComponentExtractor は、ユーザーが Web サイト／ページからコンポーネントを抽出できるようにします。

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

   その他のコンポーネントを含めることのできる [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) の基底クラス。コンテナは、アイテムの格納の基本動作（アイテムの追加、挿入、削除など）を処理します。

   最もよく使用される Container クラスは、[CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)、[CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) および [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel) です。

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder は、左に実際のコンテンツファインダー、右にコンテンツフレームを含む、2 列の専用の [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) です。

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab は、[CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) のタブパネルで使用される機能を提供する専用のパネルです。通常は、検索フォーム（クエリボックス）および検索結果を表示するデータ表示画面で使用されます。

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

    WorkflowModelCombo は、利用できるワークフローモデルの一覧を表示する、カスタマイズされた [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) です。

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

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) コンポーネントを含むメニュー。

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   ポップアップの日付選択。このクラスは、有効な日付を参照および選択できるようにするために、[DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) クラスで使用されます。

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

    DateTime は、[CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) と [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField) を組み合わせて、ユーザーが日付と時刻を入力できるようにします。

* ダイアログ

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

    Dialog は、ボディにフォーム、フッターにボタングループを備える特殊なウィンドウです。通常はコンテンツの編集に使用されますが、単に情報を表示するために使用されることもあります。

* dialogfieldset

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

    DialogFieldSet は、[Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) で使用される [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) です。

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) サーバー側[プロバイダー](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider)と簡単にやり取りできるように、[CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) と [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) で設定された [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) を作成するための小規模なヘルパークラス。

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

    検証されることも送信されることもない、表示専用のテキストフィールド。

* editbar

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

    EditBar は、ユーザーがバーのボタンを使用してコンテンツを編集できるようにします。

   ここには記載されていませんが、EditBar は、[CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase) のすべてのメンバーを持ちます。

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

    要求に応じて表示／非表示を処理し、いくつかの組み込みのサイズ変更およびイベント処理ロジックを持つ基本エディターフィールド。

* editorgrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   このクラスは、[GridPanel クラス](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)を拡張し、選択した[列](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column)でセルを編集できるようにします。編集可能な列は、[列の設定](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column)で[エディター](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)を提供することで指定されます。

* editrollover

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   EditRollover は、ユーザーがダブルクリックすることでコンテンツを編集できるようにし、コンテキストメニューを通じてさらに編集操作を提供します。編集可能な領域は、マウスがコンテンツにロールオーバーされたときに、フレームによって示されます。

* feedimporter

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

    FeedImporter は、ユーザーが RSS／Atom フィードをインポートし、フィードエントリごとにページを作成できるようにします。

* field

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

    フォームフィールドの基底クラスであり、デフォルトのイベントの処理、サイズ変更、値の処理およびその他の機能を提供します。

* fieldset

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

    [フォーム](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel)内のアイテムのグループ化に使用される標準コンテナ。

* fileuploaddialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

    FileUploadDialogButton は、FileUploadField を使用してファイルをアップロードするための新しいダイアログを開くボタンを作成します。アップロードを別のフォームで実行する必要がある編集ダイアログ内で使用することができます。

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

    利用可能なフィールドの 1 つでレコードをグループ化できるようにする、専用のストア実装。これは通常、グループ化された GridPanel のデータモデルを証明するために、[CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) と組み合わせて使用されます。

* heavymovedialog

   [CQ.wcm.HeyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

    HeavyMoveDialog は、ページとその子ページを移動するためのダイアログであり、以前アクティブ化したページの再アクティブ化も考慮に入れます（名前の「heavy」はこれを表しています）。

* hidden

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

    フォームの送信で渡す必要があるフォーム内の非表示の値を格納するための、基本的な非表示フィールド。

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton は進むボタンと戻るボタンを簡単に提供できる小規模なヘルパークラスです。通常、2 つの関連インスタンスが必要になります。進むボタンのインスタンスは、履歴を処理する戻るボタンのインスタンスに関連付けられたシンプルなボタンです。

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   軽量のHTMLエディターコンポーネントを提供します。 ツールバーの機能の一部は、Safari ではサポートされておらず、必要に応じて自動的に非表示になります。該当する場合、設定オプションに記載されています。

     エディターのツールバーボタンには、[buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) プロパティで定義されたツールチップがあります。

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

    iframe のコンテンツを表示したり、iframe でフォームを許可したりするプレーンなダイアログ。

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   iframeを含むパネル。 iframe の簡単な作成、iframe のロードイベント、iframe のコンテンツへの簡単なアクセスを可能にします。

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

    InlineField は、フォーカスされていないときにラベルとして表示されるテキストフィールドです。

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   JSON データから簡単に [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) を作成できるようにする小規模なヘルパークラスです。JsonStore には自動的に [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) が設定されます。

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   基本ラベルフィールド

* languagecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

    LanguageCopyDialog は、言語ツリーをコピーするためのダイアログです。

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

    LinkChecker は、サイト内の外部リンクを確認するためのツールです。

* listview

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView は、[Grid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) に似たビューの高速かつ軽量の実装です。

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

    LiveCopyProperties は、ライブコピープロパティ（関係の継承、同期のトリガー、同期操作）を表示および編集できるパネルを提供します。

* lvbooleancolumn

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   ブール型のデータフィールドをレンダリングする Column 定義クラスです。詳しくは、[CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 設定オプションを参照してください。

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   このクラスは、[ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView) の初期化に使用される列設定データをカプセル化します。

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   デフォルトのロケールまたは設定された [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn) に従って渡された日付をレンダリングする Column 定義クラス。詳しくは、[CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 設定オプションを参照してください。

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) 文字列に従って数値データフィールドをレンダリングする Column 定義クラスです。詳しくは、[CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) の [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) 設定オプションを参照してください。

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **廃止：代わりに、 [コンテンツファインダーを使用して](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) 、メディアを参照します。**

   MediaBrowseDialog は、メディアライブラリを参照するためのダイアログです。

* menu

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   メニューオブジェクト。これは、メニューアイテムを追加できるコンテナです。Menu は、別のコンポーネントをベースにした特殊なメニュー（[CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) など）が必要な場合に、基底クラスとしても利用できます。

   Menu には、[menu item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item) または一般的な [Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) を含めることができます。

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

    メニューにレンダリングするすべてのアイテムの基底クラス。BaseItem は、すべてのメニューコンポーネントで共有される、デフォルトのレンダリング、アクティブ化された状態の管理、基本設定オプションを提供します。

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

    デフォルトでチェックボックス（ラジオグループの一部である可能性もあります）を含むメニューアイテムを追加します。

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

    メニュー関連の機能（サブメニューなど）を必要とし、静的表示アイテムではないすべてのメニューアイテムの基底クラス。Item は、メニュー専用のアクティブ化とクリック処理を追加することで、[CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) の基本機能を拡張します。

* menuseparator

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

    メニューに区切りバーを追加します。区切りバーは、メニューアイテムを論理的なグループに分けるために使用されます。通常、区切りバーは、直接作成するのではなく、add() の呼び出し内またはアイテムの設定内で「-」を使用して追加します。

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

    通常は見出しやグループ区切りとして使用される静的テキスト文字列をメニューに追加します。

* メタデータ

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   Metadata は、アセットエディターページなどで使用されるメタデータフィールドに必要な情報を決定するフィールドのセットを提供します。

   以下のフィールドを提供します。

* multifield

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

    MultiField は、複数値のプロパティを編集するための編集可能なフォームフィールドの一覧です。

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   多変量分析テストコンポーネントは、バナーの代わりに表示される画像のセットを定義および編集するのに使用されます。クリックスルー率の統計はバナーごとに収集されます。

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

   レコードの量が増えるにつれて、ブラウザーでレンダリングするのに要する時間も増えます。Paging は、クライアントとやり取りするデータの量を減らすために使用されます。

* panel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   Panel は特定の機能と構造型コンポーネントを含むコンテナであり、アプリケーション指向のユーザーインターフェイス用の完全な構成ブロックです。

   Panel は、[CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) からの継承に基づきます。

* paragraphreference

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

    段落の参照フィールドにより、ページを閲覧したり、段落の 1 つを選択したりできます。トリガーフィールドおよび関連する段落の参照ダイアログで構成されます。

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

    Password は [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) に似ていますが、ユーザーが機密データを入力できるように、値をプライベートな状態に保ちます。

* pathcompletion

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **廃止：代わりに [CQ.form.PathFieldを使用](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField は、サーバーリポジトリを閲覧するための [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) を開くボタンとパスの入力候補機能を備えた、パス向けの入力フィールドです。高度なリンク作成のために、ページの段落を参照することもできます。

* progress

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   更新可能な進行状況バーコンポーネント。進行状況バーは、手動と自動の 2 つの異なるモードをサポートします。

   手動モードでは、独自のコードから必要に応じて進行状況バーを表示、更新（[updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar) を使用）、削除する必要があります。この方法は操作の間中、進行状況を表示する必要がある場合に最も適しています。

* propertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

    開発 IDE によくあるような従来型のプロパティグリッドを模した、専用のグリッドの実装。グリッドの各列には、いくつかのオブジェクトのプロパティが表示され、このデータは [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord) に名前／値のペアのセットとして格納されます。

* propgrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

    PropertyGrid は、オブジェクトのプロパティの表示と編集に使用される汎用グリッドです。

* quicktip

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

    @xtype quicktip は、マークアップで指定され、グローバル [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) インスタンスによって自動的に管理されるツールチップのための専用のツールチップクラスです。その他の使用方法の詳細と例については、QuickTips クラスのヘッダーを参照してください。

* radio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   単一のラジオフィールド。 チェックボックスと同じですが、入力の種類が自動的に設定されるので便利です。グループ内の各ラジオに同じ名前を付けている場合、ラジオのグループ化は、ブラウザーによって自動的に処理されます。

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

   RichText コンポーネントは現在、以下の機能を提供します。

* rolloutplan

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

    RolloutPlan は、ページのロールアウト処理を監視するためのダイアログを提供します。RolloutPlan は、[CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard) によって開始されます。

* rolloutwizard

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

    RolloutWizard は、ページのロールアウトのためのウィザードを提供します。RolloutWizard は、[CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan) を開始します。

* searchfield

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

    SearchField は、リポジトリの検索に使用できるドロップダウンリストで結果を提供する検索フィールドを提供します。

* selection

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

    Selection は、ユーザーがいくつかのオプションから選択できるようにします。オプションは、設定の一部であることも、JSON の応答から読み込むこともできます。Selection は、ドロップダウン（選択）として表示することも、コンボボックス（選択と任意のテキストの入力）として表示することもできます。

* sidekick

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

    Sidekick は、ページの編集のための一般的なツールをユーザーに提供するフローティングヘルパーです。

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

    SiteAdmin は、WCM 管理関数を提供するコンソールです。

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

    SiteImporter は、ユーザーが完全な Web サイトをインポートし、最初のプロジェクトを作成できるようにします。

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

    SizeField は、ユーザーが（例えば画像に対して）幅と高さを入力できるようにします。

* slider

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

    垂直方向または水平方向、キーボードの調節、設定可能なスナップ、軸のクリックおよびアニメーションをサポートする Slider。任意のコンテナにアイテムとして追加できます。使用例：...

* slideshow

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   Slideshow は、スライドショーとして表示できる画像と画像タイトルのセットを定義および編集するのに使用できるコンポーネントを提供します。

   Slideshow コンポーネントは、[CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) コンポーネントをベースとします。

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile はインテリジェントファイルアップローダーです。

   Flash のプラグイン（バージョン 9 以上）がインストールされている場合、アップロードは、アップロードの便利な処理方法を提供する SWFupload ライブラリを使用して実行されます。

* smartimage

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage はインテリジェント画像アップローダーです。アップロードされた画像を処理するツールを提供します。イメージマップや画像のトリミングを定義するツールを提供します。

   このコンポーネントは主に、独立したダイアログのタブで使用するために設計されています。

* spacer

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   レイアウトでサイズ変更可能なスペースを提供するために使用されます。

* spinner

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   Spinner は、数値、日付、時刻の値のトリガーフィールドです。この値は、指定されたアップ／ダウンのトリガー、スクロールホイール、スクロールキーを使用して増減できます。

* splitbutton

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

    デフォルトのボタンのクリックイベントとは別にイベントを発生させることのできる組み込みのドロップダウン矢印を提供する分割ボタン。これは通常、プライマリボタンのアクションに追加のオプションを提供するドロップダウンメニューを表示するために使用されます。ただし、カスタムハンドラーにより、矢印クリックの実装を提供できます。

* static

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

    Static は、任意のテキストまたは HTML を表示するために使用できます。

* 統計

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

    Statistics は、ページインプレッション数をグラフとして表示します。このウィジェットでは、統計を表示する期間を選択できます。

* store

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   Store クラスは、[GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)、[ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)、[DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView) などのコンポーネントの入力データを提供する [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) オブジェクトのクライアント側キャッシュをカプセル化します。

* suggestfield

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

    SuggestField は、ユーザーの入力に基づいた候補を提供します。

* switcher

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

    Switcher は、Web サイト、デジタルアセット、ツール、ワークフローおよびセキュリティを切り替えるために、コンソールのヘッダーバー用のボタングループを提供します。

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **廃止：代わりに、 [CQ.form.TableEdit2を使用し](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) ます。**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2 は表を作成するウィジェットを提供します。

* tabpanel

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   基本のタブコンテナ。TabPanels can be used exactly like a standard [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) for layout purposes, but also have special support for containing child Components ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* タグ

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

    は、タグを入力するためのフォームウィジェットです。既存のタグから選択できるポップアップメニューを備えており、自動入力などの機能もあります。

* textarea

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   複数行テキストフィールド 従来のテキストエリアフィールドと直接置き換えて使用できます。自動サイズ変更もサポートしています。

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

    TextButton は、[CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button) の機能を備えたテキストリンクを提供します。

* textfield

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   基本テキストフィールド。従来のテキスト入力と直接置き換えて使用できます。また、より高度な入力コントロール（[CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)、[CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) など）の基底クラスとして使用できます。

* thumbnail

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

    時刻のドロップダウンと自動時刻検証機能を備えた時刻入力フィールドを提供します。使用例：...

* tip

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

    @xtype tip は、[CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) と [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) の基底クラスであり、すべての tip ベースのクラスで必要な基本のレイアウトと配置を提供します。このクラスは、シンプルで静的に配置された tip に直接使用できます。

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

    メニューに区切りバーを追加します。区切りバーは、メニューアイテムを論理的なグループに分けるために使用されます。この区切りには、タイトルを表示することもできます。

* ツールバー

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Toolbar の基本クラス。Toolbar の [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) は [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button) ですが、Toolbar の要素（Toolbar コンテナの子アイテム）には、ほとんどのタイプのコンポーネントを使用できます。Toolbar の要素は、そのコンストラクターを使用して明示的に作成できます。

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

    ターゲット要素をポイントしたときに追加の情報を提供するための標準のツールチップの実装。@xtype tooltip。

* treegrid

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* treepanel

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel は、ツリー構造のデータをツリー構造の UI として提供します。

   TreePanel に追加された [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) には、[attributes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) プロパティでアプリケーションが使用するメタデータを含めることができます。

* trigger

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

    クリック可能なトリガーボタン（デフォルトでは、コンボボックスに似ています）を追加する TextField のための便利なラッパーを提供します。トリガーにはデフォルトのアクションが設定されていないので、[onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField) を上書きすることで、トリガークリックハンドラーを実装するための関数を割り当てる必要があります。TriggerField はコンボボックスとまったく同様にレンダリングされるので、直接作成することもできます。

* uploaddialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

    UploadDialog は、ユーザーがリポジトリにファイルをアップロードできるようにします。新しい UploadDialog を作成します。

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

    現在のユーザー名を表示するツールバーアイテムであり、ユーザーがプロパティや権限借用の編集などの操作をおこなえるようにします。

* viewport

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   表示可能なアプリケーションの領域（ブラウザービューポート）を表す専用のコンテナ。

   Viewport は、ドキュメントのボディにレンダリングされ、自動的にブラウザーのビューポートのサイズに調節されます。また、ウィンドウのサイズ変更を管理します。作成できる Viewport は 1 つだけです。

* window

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   アプリケーションウィンドウとして使用するための専用のパネル。デフォルトでは、ウィンドウはフローティング表示され、[サイズ変更可能](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)かつ[ドラッグ可能](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)です。ウィンドウは、ビューポートいっぱいまで[最大化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)したり、前のサイズを復元したり、[最小化](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)したりできます。

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   XML データから簡単に [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) を作成できるようにする小規模なヘルパークラスです。XmlStore には自動的に [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader) が設定されます。

   **cqinclude** Pseudoxtype。リポジトリ内の別のパスからのウィジェット定義を含めます。 ページダイアログで最もよく使用されます。実際には、この xtype の JavaScript ウィジェットクラスは存在しません。CQ.Util クラスの formatData() 関数によって処理されます。詳しくは、このナレッジベースの記事を参照してください。
