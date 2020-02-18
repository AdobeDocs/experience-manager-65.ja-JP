---
title: 複数のインプレースエディターの設定
seo-title: 複数のインプレースエディターの設定
description: 複数のインプレースエディターが含まれるようにコンポーネントを設定できます
seo-description: 複数のインプレースエディターが含まれるようにコンポーネントを設定できます
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 複数のインプレースエディターの設定{#configuring-multiple-in-place-editors}

タッチ操作対応 UI では、複数のインプレースエディターが含まれるようにコンポーネントを設定できます。

このような設定にすると、適切なコンテンツを選択して、適切なエディターを開くことができます。次に例を示します。

![chlimage_1-8](assets/chlimage_1-8a.png)

## 複数のエディターの設定 {#configuring-multiple-editors}

複数のインプレースエディターを有効にするには、`cq:InplaceEditingConfig` ノードタイプの構造を `cq:ChildEditorConfig` ノードタイプの定義で強化します。

次に例を示します。

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

複数のエディターの設定手順

1. On the node `cq:inplaceEditing` (of type `cq:InplaceEditingConfig`) define the property:

   * 名前:`editorType`
   * タイプ: `String`
   * 値: `hybrid`

1. このノードの下に、新しいノードを作成します。

   * 名前: `cq:ChildEditors`
   * タイプ: `nt:unstructured`

1. `cq:childEditors` ノードの下に、インプレースエディターごとに新しいノードを作成します。

   * 名前：各ノードの名前は、そのノードが（ドロップターゲットのように）表すプロパティの名前にしてください。For example, `image`, `text`.
   * タイプ：cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >定義されたドロップターゲットと子エディターの間には相関関係があります。`cq:ChildEditorConfig` ノードの名前はドロップターゲット ID と見なされ、選択された子エディターへのパラメーターとして使用されます。編集可能なサブエリアにドロップターゲット（テキストコンポーネントなど）がない場合でも、子エディターの名前は対応する編集可能エリアを識別する ID と見なされます。

1. On each of these nodes ( `cq:ChildEditorConfig`) define the properties:

   * 名前: `type`
   * Value: name of the registered in-place editor; for example, `image`, `text`

   * 名前: `title`
   * Value: the title that you want to display in the components selection list (of available editors); for example, `Image`, `Text`

### リッチテキストエディター用の追加設定 {#additional-configuration-for-rich-text-editors}

複数のリッチテキストエディター（RTE）の設定は、個々の RTE インスタンスをそれぞれ別個に設定できるので、やや異なります。

>[!NOTE]
>
>詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。

複数の RTE を含めるには、インプレース RTE ごとに次のような設定が必要です。

* 「ノー `cq:InplaceEditingConfig` ドを定義」 `config` で、

   * `config` ノードの下に、個々の RTE 設定を定義します。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>各 RTE はそれぞれ異なる設定を持つことができるので、推奨されるベストプラクティスは、`config` ノードを `cq:InplaceEditingConfig` の下に定義することです。
>
>ただし、RTE の場合、`configPath` プロパティがサポートされるのは、コンポーネント内のテキストエディター（編集可能なサブエリア）のインスタンスが 1 つだけのときです。この `configPath` のサポートは、コンポーネントの古い UI ダイアログとの下位互換性のために提供されています。

## コードサンプル {#code-samples}

**GitHub のコード**

このページのコードは GitHub にあります

* [GitHub上のaem-authoring-hybrideditorsプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)としてダウンロードします

## インプレースエディターの追加 {#adding-an-in-place-editor}

For general information about adding an in-place editor see the document [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).
