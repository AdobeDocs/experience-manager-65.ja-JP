---
title: 複数のインプレースエディター用に RTE を設定します。
description: リッチテキストエディターを設定して、Adobe Experience Manager で複数のインプレースエディターを作成します。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '445'
ht-degree: 100%

---

# 複数のインプレースエディターを設定 {#configure-multiple-in-place-editors}

Adobe Experience Manager のリッチテキストエディターは、複数のインプレースエディターを持つように設定できます。このような設定にすると、適切なコンテンツを選択して、適切なエディターを開くことができます。

![特定のインプレースエディター](assets/rte-inplace-editor.png)

## 複数のエディターを設定 {#configure-multiple-editors}

複数のインプレースエディターを有効にするために、`cq:InplaceEditingConfig` ノードタイプの構造を `cq:ChildEditorConfig` ノードタイプの定義で拡張しました。

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

1. タイプ `cq:InplaceEditingConfig` のノード `cq:inplaceEditing` で、次のプロパティを定義します。

   * 名前：`editorType`
   * タイプ：`String`
   * 値：`hybrid`

1. このノードの下に、次のノードを作成します。

   * 名前：`cq:ChildEditors`
   * 型：`nt:unstructured`

1. `cq:childEditors` ノードの下に、インプレースエディターごとにノードを作成します。

   * 名前：各ノードの名前は、ドロップターゲットの場合と同様に、ノードが表すプロパティの名前です。例えば、`image` と `text` です。
   * タイプ：`cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義されたドロップターゲットと子エディターの間には相関関係があります。`cq:ChildEditorConfig` ノードの名前はドロップターゲット ID と見なされ、選択された子エディターへのパラメーターとして使用されます。編集可能なサブエリアにドロップターゲット（テキストコンポーネントなど）がない場合でも、子エディターの名前は対応する編集可能エリアを識別する ID と見なされます。

1. これらのノード（`cq:ChildEditorConfig`）のそれぞれに次のプロパティを定義します。

   * 名前：`type`
   * 値：登録されているインプレースエディターの名前（`image` や `text` など）。

   * 名前：`title`
   * 値：使用可能なエディターのコンポーネント選択リストに表示されるタイトル。例えば、`Image` と `Text` です。

### リッチテキストエディター用の追加設定 {#additional-configuration-for-rich-text-editors}

複数のリッチテキストエディター（RTE）の設定は、個々の RTE インスタンスをそれぞれ別個に設定できるので、やや異なります。詳しくは、 [リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。複数の RTE を含めるには、インプレース RTE ごとに設定を作成します。個々の RTE が異なる設定を持つことができるため、アドビは `cq:InplaceEditingConfig` の下に新しい設定ノードを作成することをお勧めします。新しいノードの下に、個々の RTE 設定を作成します。

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
>ただし、RTE の場合、`configPath` プロパティがサポートされるのは、コンポーネント内のテキストエディター（編集可能なサブエリア）のインスタンスが 1 つだけのときです。この `configPath` の使用は、コンポーネントの古いユーザーインターフェイスダイアログとの下位互換性をサポートするために提供されています。

>[!CAUTION]
>
>RTE 設定ノードの名前を `config` にしないでください。この名前にすると、RTE 設定が管理者に対してのみ使用可能になり、グループ `content-author` のユーザーに対して使用可能になりません。

## コードサンプル {#code-samples}

このページのコードは、[GitHub の aem-authoring-hybrideditors プロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)にあります。プロジェクト全体を [ZIP アーカイブ](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)としてダウンロードできます。

## インプレースエディターを追加 {#add-an-in-place-editor}

インプレースエディターの追加に関する一般的な情報については、ドキュメント「[ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)」を参照してください。

>[!MORELIKETHIS]
>
>* [Experience Manager でリッチテキストエディターを設定します](/help/sites-administering/rich-text-editor.md)。

