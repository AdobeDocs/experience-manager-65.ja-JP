---
title: リッチテキストエディターを設定して、アクセス可能なWebページとサイトを作成します。
description: リッチテキストエディターを設定して、アクセス可能なWebページとサイトを作成します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 38%

---


# Configure RTE to create accessible webpages and sites {#configure-rte-for-accessibility}

Adobe Experience Managerは、様々なアクセシビリティ標準に従って、人間標準のアクセシビリティ機能をサポートしています。 また、開発者は、リッチテキストエディター(RTE)を使用するExperience Managerコンポーネントを使用して、アクセシブルなコンテンツの作成に役立つ機能をカスタマイズまたは拡張できます。

Webページをデザインし、ページにコンテンツを追加する場合、コンテンツ開発者および作成者はRTEの機能を使用してアクセシビリティ関連の情報を提供できます。 例えば、見出しや段落要素から構造情報を追加します。

これらの機能を設定およびカスタマイズするには、コンポーネントのRTEプラグイン [を](#configure-the-plugin-features) 設定します。 For example, the `paraformat` plugin lets you add additional block level semantic elements, including extending the number of heading levels supported beyond the basic `H1`, `H2`, and `H3` provided by default.

RTEは、タッチ対応ユーザーインターフェイスおよびクラシックユーザーインターフェイス用の様々なコンポーネントで利用できます。 ただし、RTEを使用する主なコンポーネントは、 **Text** コンポーネントで、両方のインターフェイスで使用できます。 次の画像は、以下を含む様々なプラグインが有効なRTEを示していま `paraformat`す。

![タッチ対応UIのフルスクリーンモードのテキストコンポーネント(RTE)。](assets/chlimage_1-206.png)

*図：タッチ対応ユーザーインターフェイスのテキストコンポーネント。*

![クラシック UI のテキストコンポーネントの編集ダイアログ（RTE）。](assets/chlimage_1-207.png)

*図：クラシックユーザーインターフェイスのテキストコンポーネント*

様々なインターフェイスで使用できるRTE機能の違いについては、「 [プラグインとその機能」を参照してください](/help/sites-administering/rich-text-editor.md#aboutplugins)。

## プラグイン機能の設定 {#configure-the-plugin-features}

For the complete instructions to configure the RTE, see [configure the Rich Text Editor](/help/sites-administering/rich-text-editor.md) page. ここでは、主な手順を含むすべての問題について説明します。

* [プラグインと機能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [プラグインのアクティベートと features プロパティの設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE のその他の機能の設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

By configuring a plugin within the appropriate `rtePlugins` sub-branch in CRXDE Lite, you can activate either all or specific features for that plugin.

![CRXDE Lite で rtePlugin の例を表示。](assets/chlimage_1-208.png)

### Example - specify paragraph formats available in RTE selection field {#example-specifying-paragraph-formats-available-in-rte-selection-field}

意味的ブロックの新しい書式を選択可能にするには、次の手順を実行します。

1. 使用している RTE によって、[設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)を特定し、移動します。
1. [プラグインをアクティベート](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)することにより、[段落選択フィールドを有効](/help/sites-administering/rich-text-editor.md)にします。
1. [段落選択フィールドで使用可能にする書式を指定](/help/sites-administering/rich-text-editor.md)します。
1. これにより、コンテンツ作成者は、指定した段落書式を RTE の選択フィールドから選択できます。アクセス方法は次のとおりです。

   * タッチ対応UIでの段落ピルクローアイコンの使用
   * Using the **Format** field (pop-up selector) in the Classic UI.

段落書式オプションを介して RTE で構造要素を使用できるので、AEM はアクセス可能なコンテンツの開発に適した基礎を提供します。コンテンツ作成者は、RTE を使用してフォントのサイズや色、その他の関連する属性を書式設定できないので、インライン書式設定は作成できません。代わりに、見出しなどの該当する構造要素を選択し、「スタイル」オプションから選択されたグローバルスタイルを使用する必要があります。これにより、独自のスタイルシートで閲覧するユーザーにとってはマークアップがクリーンになり、オプションも多くなるほか、コンテンツの構造が正確になります。

## Use of the source edit feature {#use-of-the-source-edit-feature}

コンテンツ作成者が、RTE を使用して作成された HTML ソースコードを調査および調整することが必要になる場合があります。例えば、WCAG 2.0 を確実に準拠するため、RTE 内で作成されたコンテンツの一部で追加のマークアップが必要となることがあります。これをおこなうには、RTE の[ソースの編集](/help/sites-administering/rich-text-editor.md#aboutplugins)オプションを使用します。You can specify the [ `sourceedit` feature on the `misctools` plugin](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>`sourceedit` 機能の使用には十分に注意してください。タイピングの誤りやサポート対象外の機能は、問題を大きくする可能性があります。

## その他のHTML要素追加と属性のサポート {#add-support-for-more-html-elements-and-attributes}

AEM のアクセシビリティ機能をさらに拡張するには、RTE に基づく既存のコンポーネント（**テキスト**&#x200B;コンポーネントや&#x200B;**テーブル**&#x200B;コンポーネント）を、要素や属性を追加して拡張することができます。

The following procedure illustrates how to extend the **Table** component with a **Caption** element that provides information about a data table to assistive technology users:

### Example - add the caption to the Table Properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

のコンストラクターで、キャプションの編集に使用するテキスト入力フィールドを追加 `TablePropertiesDialog`します。 コンテンツ `itemId` を自動的に処理するには、 `caption` （DOM属性の名前など）に設定する必要があります。

**表で**、DOM要素に対して属性を明示的に設定または削除します。 値は、 `config` オブジェクトのダイアログによって渡されます。 DOM属性は、ブラウザー実装での一般的な問題を回避するために、対応する `CQ.form.rte.Common` メソッド( `com` のショートカット `CQ.form.rte.Common`)を使用して設定または削除する必要があります。

>[!NOTE]
>
>この手順は、Classicユーザーインターフェイスにのみ適しています。

### 例 — テキストに強調を使用する場合に、アクセシブルなHTMLを作成する {#create-accessible-html-for-text}

RTEでは、およびの代わりに `strong` および `em` タグを使用でき `b` ま `i`す。 次追加のノードは、ダイアログ内の `uiSettings` およびノードの兄弟として `rtePlugins` 使用します。

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### 詳しい手順 {#step-by-step-instructions}

1. 開始CRXDE Lite。 For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. コピー：

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   リダイレクト先は次のとおりです。

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >中間フォルダーが存在しない場合は、作成する必要があります。

1. コピー：

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   リダイレクト先は次のとおりです。

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. 次のファイルを編集用に開きます（ダブルクリックで開く）。

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. `constructor` メソッドで、

   ```
   var dialogRef = this;
   ```

   次のコードを追加します。

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 次のファイルを開きます。

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. Save your changes using **Save All…**

>[!NOTE]
>
>プレーンテキストフィールドは、キャプション要素の値に対して許可される入力の種類ではありません。 ExtJSウィジェットを使用できます。ExtJSウィジェットは、その `getValue()` メソッドを通してキャプションの値を提供します。
>
>追加の要素および属性用に編集機能を追加するには、以下の両方を確認します。
>
>* The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
>* DOM 要素で属性が設定／削除されていること（`Table`）。


>[!MORELIKETHIS]
>
>* [WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)
>* [アクセシブルなコンテンツを作成する（WCAG 2.0準拠）](/help/sites-authoring/creating-accessible-content.md)

