---
title: 複数のインプレースエディター用にRTEを設定します。
description: リッチテキストエディターを設定して、Adobe Experience Managerで複数のインプレースエディターを作成します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 26%

---


# 複数のインプレースエディターの設定 {#configure-multiple-in-place-editors}

Adobe Experience Managerでリッチテキストエディタを設定して、複数のインプレースエディタを使用できます。 このような設定にすると、適切なコンテンツを選択して、適切なエディターを開くことができます。

![特定のインプレイスエディタ](assets/rte-inplace-editor.png)

## 複数のエディターの設定 {#configure-multiple-editors}

複数のインプレースエディターを有効にするには、`cq:InplaceEditingConfig` ノードタイプの構造を `cq:ChildEditorConfig` ノードタイプの定義で強化します。

次に例を示します。

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

複数のエディターを設定するには、次の手順に従います。

1. ノード `cq:inplaceEditing` (タイプ `cq:InplaceEditingConfig`)で次のプロパティを定義します。

   * 名前：`editorType`
   * 型：`String`
   * 値：`hybrid`

1. このノードの下で、ノードを作成します。

   * 名前：`cq:ChildEditors`
   * 型：`nt:unstructured`

1. Under `cq:childEditors` node, create a node for each in-place editor:

   * 名前：各ノードの名前は、それが表すプロパティの名前で、ドロップターゲットと同様に、 例えば、`image` と `text` です。
   * 型：`cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義されたドロップターゲットと子エディターの間には相関関係があります。The name of the `cq:ChildEditorConfig` node is considered as the drop target ID, for use as a parameter to the selected child editor. 編集可能サブ領域にドロップターゲットがない場合（例えば、テキストコンポーネント内など）、子エディターの名前は、対応する編集可能領域を識別するIDと見なされます。

1. On each of these nodes (`cq:ChildEditorConfig`) define the properties:

   * 名前: `type`.
   * Value: The name of the registered in-place editor; for example, `image` and `text`.

   * 名前: `title`.
   * 値：使用可能なエディターのコンポーネント選択リストに表示されるタイトル。 例えば、`Image` と `Text` です。

### Additional configuration for Rich Text Editors {#additional-configuration-for-rich-text-editors}

複数のリッチテキストエディター（RTE）の設定は、個々の RTE インスタンスをそれぞれ別個に設定できるので、やや異なります。詳しくは、「リッチテキストエディターの [設定](/help/sites-administering/rich-text-editor.md)」を参照してください。 複数のRTEに各インプレースRTEの設定を作成させる場合。 Adobeでは、個々のRTEごとに異なる設定を持つこ `cq:InplaceEditingConfig` とができるので、に新しい設定ノードを作成することをお勧めします。 新しいノードで、個々のRTE設定を作成します。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>ただし、RTE の場合、`configPath` プロパティがサポートされるのは、コンポーネント内のテキストエディター（編集可能なサブエリア）のインスタンスが 1 つだけのときです。This use of `configPath` is provided to support backwards compatibility with older user interface dialogs of the component.

>[!CAUTION]
>
>RTE 設定ノードの名前を `config` にしないでください。Otherwise, the RTE configurations are available for only the administrators and not for the users in the group `content-author`.

## Code samples {#code-samples}

You can find the code of this page on [aem-authoring-hybrideditors project on GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). 完全なプロジェクトはZIPアーカイブとしてダウンロ [ードできます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)。

## インプレ追加ースエディター {#add-an-in-place-editor}

For general information about adding an in-place editor see the document [customize page authoring](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [Experience Managerでリッチテキストエディターを設定します](/help/sites-administering/rich-text-editor.md)。

