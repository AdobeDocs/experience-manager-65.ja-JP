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


# アクセス可能なWebページとサイトを作成するようにRTEを設定{#configure-rte-for-accessibility}

Adobe Experience Managerは、様々なアクセシビリティ標準に従って、人間標準のアクセシビリティ機能をサポートしています。 また、開発者は、リッチテキストエディター(RTE)を使用するExperience Managerコンポーネントを使用して、アクセシブルなコンテンツの作成に役立つ機能をカスタマイズまたは拡張できます。

Webページをデザインし、ページにコンテンツを追加する場合、コンテンツ開発者および作成者はRTEの機能を使用してアクセシビリティ関連の情報を提供できます。 例えば、見出しや段落要素から構造情報を追加します。

これらの機能を設定およびカスタマイズするには、[コンポーネントのRTEプラグイン](#configure-the-plugin-features)を設定します。 例えば、`paraformat`プラグインを使用すると、デフォルトで提供される基本的な`H1`、`H2`および`H3`を超えてサポートされる見出しレベルの数を拡張するなど、ブロックレベルのセマンティック要素を追加できます。

RTEは、タッチ対応ユーザーインターフェイスおよびクラシックユーザーインターフェイス用の様々なコンポーネントで利用できます。 ただし、RTEを使用する主なコンポーネントは、両方のインターフェイスで使用できる&#x200B;**Text**&#x200B;コンポーネントです。 次の画像は、`paraformat`を含む、様々なプラグインが有効なRTEを示しています。

![タッチ対応UIのフルスクリーンモードのテキストコンポーネント(RTE)。](assets/chlimage_1-206.png)

*図：タッチ対応ユーザーインターフェイスのテキストコンポーネント。*

![クラシック UI のテキストコンポーネントの編集ダイアログ（RTE）。](assets/chlimage_1-207.png)

*図：クラシックユーザーインターフェイスのテキストコンポーネント*

様々なインターフェイスで使用できるRTE機能の違いについては、[プラグインとその機能](/help/sites-administering/rich-text-editor.md#aboutplugins)を参照してください。

## プラグイン機能の設定 {#configure-the-plugin-features}

RTEを設定する詳細な手順については、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)ページを参照してください。 ここでは、主な手順を含むすべての問題について説明します。

* [プラグインと機能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [プラグインのアクティベートと features プロパティの設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE のその他の機能の設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

CRXDE Lite内の適切な`rtePlugins`サブブランチ内にプラグインを設定すると、そのプラグインのすべての機能または特定の機能をアクティブ化できます。

![CRXDE Lite で rtePlugin の例を表示。](assets/chlimage_1-208.png)

### 例 — RTE選択フィールド{#example-specifying-paragraph-formats-available-in-rte-selection-field}で使用可能な段落書式を指定する

意味的ブロックの新しい書式を選択可能にするには、次の手順を実行します。

1. 使用している RTE によって、[設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)を特定し、移動します。
1. [プラグインをアクティベート](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)することにより、[段落選択フィールドを有効](/help/sites-administering/rich-text-editor.md)にします。
1. [段落選択フィールドで使用可能にする書式を指定](/help/sites-administering/rich-text-editor.md)します。
1. これにより、コンテンツ作成者は、指定した段落書式を RTE の選択フィールドから選択できます。アクセス方法は次のとおりです。

   * タッチ対応UIでの段落ピルクローアイコンの使用
   * クラシックUIで&#x200B;**形式**&#x200B;フィールド（ポップアップセレクター）を使用する。

段落書式オプションを介して RTE で構造要素を使用できるので、AEM はアクセス可能なコンテンツの開発に適した基礎を提供します。コンテンツ作成者は、RTE を使用してフォントのサイズや色、その他の関連する属性を書式設定できないので、インライン書式設定は作成できません。代わりに、見出しなどの該当する構造要素を選択し、「スタイル」オプションから選択されたグローバルスタイルを使用する必要があります。これにより、独自のスタイルシートで閲覧するユーザーにとってはマークアップがクリーンになり、オプションも多くなるほか、コンテンツの構造が正確になります。

## ソース編集機能{#use-of-the-source-edit-feature}の使用

コンテンツ作成者が、RTE を使用して作成された HTML ソースコードを調査および調整することが必要になる場合があります。例えば、WCAG 2.0 を確実に準拠するため、RTE 内で作成されたコンテンツの一部で追加のマークアップが必要となることがあります。これをおこなうには、RTE の[ソースの編集](/help/sites-administering/rich-text-editor.md#aboutplugins)オプションを使用します。[ `sourceedit`機能は、`misctools`プラグイン](/help/sites-administering/rich-text-editor.md#aboutplugins)で指定できます。

>[!CAUTION]
>
>`sourceedit` 機能の使用には十分に注意してください。タイピングの誤りやサポート対象外の機能は、問題を大きくする可能性があります。

## より多くのHTML要素と属性追加のサポート{#add-support-for-more-html-elements-and-attributes}

AEM のアクセシビリティ機能をさらに拡張するには、RTE に基づく既存のコンポーネント（**テキスト**&#x200B;コンポーネントや&#x200B;**テーブル**&#x200B;コンポーネント）を、要素や属性を追加して拡張することができます。

次の手順は、支援テクノロジーユーザーに対してデータテーブルに関する情報を提供する&#x200B;**テーブル**&#x200B;コンポーネントを&#x200B;**キャプション**&#x200B;要素で拡張する方法を示しています。

### 例 — テーブルプロパティダイアログにキャプションを追加する{#example-adding-the-caption-to-the-table-properties-dialog}

`TablePropertiesDialog`のコンストラクターに、キャプションの編集に使用するテキスト入力フィールドを追加します。 `itemId`は、コンテンツを自動的に処理するために`caption`（DOM属性の名前）に設定する必要があります。

**テーブル**&#x200B;で、DOM要素に対する属性を明示的に設定または削除します。 この値は、`config`オブジェクトのダイアログによって渡されます。 DOM属性は、対応する`CQ.form.rte.Common`メソッド（`com`は`CQ.form.rte.Common`のショートカット）を使用して設定または削除する必要があります。これにより、ブラウザー実装での一般的な問題を回避できます。

>[!NOTE]
>
>この手順は、Classicユーザーインターフェイスにのみ適しています。

### 例 — テキスト{#create-accessible-html-for-text}で強調を使用する場合、アクセシブルなHTMLを作成する

RTEは、`b`および`i`の代わりに`strong`タグと`em`タグを使用できます。 次追加のノードは、ダイアログ内の`uiSettings`ノードと`rtePlugins`ノードの兄弟として指定します。

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

### 詳しい説明{#step-by-step-instructions}

1. 開始CRXDE Lite。 次に例を示します。[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

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

1. 追加`transferConfigToTable`メソッドの末尾の次のコード：

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

1. **すべて保存…**&#x200B;を使用して変更を保存

>[!NOTE]
>
>プレーンテキストフィールドは、キャプション要素の値に対して許可される入力の種類ではありません。 `getValue()`メソッドを通してキャプションの値を提供するExtJSウィジェットはどれでも使用できます。
>
>追加の要素および属性用に編集機能を追加するには、以下の両方を確認します。
>
>* 対応する各フィールドの`itemId`プロパティは、適切なDOM属性の名前(`TablePropertiesDialog`)に設定されます。
>* DOM 要素で属性が設定／削除されていること（`Table`）。


>[!MORELIKETHIS]
>
>* [WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)
>* [アクセシブルなコンテンツを作成する（WCAG 2.0準拠）](/help/sites-authoring/creating-accessible-content.md)

