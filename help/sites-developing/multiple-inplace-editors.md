---
title: 複数のインプレースエディター用にRTEを設定します。
description: リッチテキストエディターを設定して、Adobe Experience Managerで複数のインプレースエディターを作成します。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 26%

---

# 複数のインプレースエディターの設定{#configure-multiple-in-place-editors}

Adobe Experience Managerでリッチテキストエディターを設定して、複数のインプレースエディターを含めることができます。 このような設定にすると、適切なコンテンツを選択して、適切なエディターを開くことができます。

![特定のインプレースエディター](assets/rte-inplace-editor.png)

## 複数のエディターの設定{#configure-multiple-editors}

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

1. （タイプ`cq:InplaceEditingConfig`の）ノード`cq:inplaceEditing`で、次のプロパティを定義します。

   * 名前:`editorType`
   * 型：`String`
   * 値：`hybrid`

1. このノードの下に、次のノードを作成します。

   * 名前：`cq:ChildEditors`
   * 型：`nt:unstructured`

1. `cq:childEditors`ノードの下に、各インプレースエディター用のノードを作成します。

   * 名前：各ノードの名前は、ドロップターゲットの場合と同様に、そのノードが表すプロパティの名前です。 例えば、`image` と `text` です。
   * 型：`cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義されたドロップターゲットと子エディターの間には相関関係があります。`cq:ChildEditorConfig`ノードの名前はドロップターゲットIDと見なされ、選択した子エディターのパラメーターとして使用されます。 編集可能なサブ領域にドロップターゲットがない場合（例えば、テキストコンポーネント内にドロップターゲットがない場合）、子エディターの名前は、対応する編集可能な領域を識別するIDと見なされます。

1. これらの各ノード(`cq:ChildEditorConfig`)で、次のプロパティを定義します。

   * 名前: `type`.
   * 値：登録済みのインプレースエディターの名前。例えば、`image`と`text`です。

   * 名前: `title`.
   * 値：使用可能なエディターのコンポーネント選択リストに表示されるタイトル。 例えば、`Image` と `Text` です。

### リッチテキストエディターの追加設定{#additional-configuration-for-rich-text-editors}

複数のリッチテキストエディター（RTE）の設定は、個々の RTE インスタンスをそれぞれ別個に設定できるので、やや異なります。詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。 複数のRTEを使用するには、各インプレースRTEの設定を作成します。 Adobeでは、`cq:InplaceEditingConfig`の下に新しい設定ノードを作成することをお勧めします。各RTEは異なる設定を持つことができます。 新しいノードの下に、個々のRTE設定を作成します。

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
>ただし、RTE の場合、`configPath` プロパティがサポートされるのは、コンポーネント内のテキストエディター（編集可能なサブエリア）のインスタンスが 1 つだけのときです。この`configPath`の使用は、コンポーネントの古いユーザーインターフェイスダイアログとの下位互換性をサポートするために提供されています。

>[!CAUTION]
>
>RTE 設定ノードの名前を `config` にしないでください。そうしないと、RTE設定は管理者のみが使用でき、グループ`content-author`のユーザーは使用できません。

## コードサンプル{#code-samples}

このページのコードは、GitHubの](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)の[aem-authoring-hybrideditorsプロジェクトにあります。 プロジェクト全体を[ZIPアーカイブ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)としてダウンロードできます。

## インプレースエディター{#add-an-in-place-editor}の追加

インプレースエディターの追加に関する一般的な情報については、[ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)を参照してください。

>[!MORELIKETHIS]
>
>* [Experience Manager](/help/sites-administering/rich-text-editor.md)でのリッチテキストエディターの設定

