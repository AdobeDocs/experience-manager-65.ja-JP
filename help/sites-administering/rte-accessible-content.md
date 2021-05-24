---
title: アクセシブルなWebページおよびサイトを作成するためのリッチテキストエディターの設定
description: アクセシブルなWebページおよびサイトを作成するためのリッチテキストエディターの設定
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 38%

---

# アクセス可能なWebページとサイトを作成するようにRTEを設定します。 {#configure-rte-for-accessibility}

Adobe Experience Managerは、様々なアクセシビリティ標準に従ったman standardのアクセシビリティ機能をサポートしています。 また、開発者は、リッチテキストエディター(RTE)を使用するExperience Managerコンポーネントを使用して、アクセシブルなコンテンツを作成するのに役立つ機能をカスタマイズまたは拡張できます。

Webページをデザインし、コンテンツをページに追加する場合、コンテンツ開発者と作成者は、RTEの機能を使用してアクセシビリティ関連の情報を提供できます。 例えば、見出しや段落要素から構造情報を追加します。

これらの機能を設定およびカスタマイズするには、[コンポーネントのRTEプラグイン](#configure-the-plugin-features)を設定します。 例えば、`paraformat`プラグインを使用すると、デフォルトで提供される基本の`H1`、`H2`および`H3`を超えた見出しレベルの数の拡張をサポートするなど、ブロックレベルのセマンティック要素を追加できます。

RTEは、タッチ操作対応UIとクラシックUI用の様々なコンポーネントで使用できます。 ただし、RTEを使用する主なコンポーネントは、両方のインターフェイスで使用できる&#x200B;**Text**&#x200B;コンポーネントです。 次の画像は、`paraformat`を含む様々なプラグインが有効になっているRTEを示しています。

![タッチ操作対応UIのフルスクリーンモードのテキストコンポーネント(RTE)。](assets/chlimage_1-206.png)

*図：タッチ操作対応UIのテキストコンポーネント。*

![クラシック UI のテキストコンポーネントの編集ダイアログ（RTE）。](assets/chlimage_1-207.png)

*図：クラシックユーザーインターフェイスのテキストコンポーネント。*

様々なインターフェイスで利用できるRTE機能の違いについては、[プラグインとその機能](/help/sites-administering/rich-text-editor.md#aboutplugins)を参照してください。

## プラグイン機能の設定 {#configure-the-plugin-features}

RTEの設定手順について詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)ページを参照してください。 ここでは、主な手順を含め、すべての問題について説明します。

* [プラグインと機能](/help/sites-administering/rich-text-editor.md#aboutplugins)を参照してください。
* [設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [プラグインのアクティベートと features プロパティの設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [RTE のその他の機能の設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

CRXDE Lite内の適切な`rtePlugins`サブブランチ内にプラグインを設定することで、そのプラグインのすべての機能または特定の機能をアクティブ化できます。

![CRXDE Lite で rtePlugin の例を表示。](assets/chlimage_1-208.png)

### 例 — RTE選択フィールド{#example-specifying-paragraph-formats-available-in-rte-selection-field}で使用可能な段落形式を指定

意味的ブロックの新しい書式を選択可能にするには、次の手順を実行します。

1. 使用している RTE によって、[設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)を特定し、移動します。
1. [プラグインをアクティベート](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)することにより、[段落選択フィールドを有効](/help/sites-administering/rich-text-editor.md)にします。
1. [段落選択フィールドで使用可能にする書式を指定](/help/sites-administering/rich-text-editor.md)します。
1. これにより、コンテンツ作成者は、指定した段落書式を RTE の選択フィールドから選択できます。アクセス方法は次のとおりです。

   * タッチ操作対応UIの段落ピルクローアイコンを使用する。
   * クラシックUIでの&#x200B;**形式**&#x200B;フィールド（ポップアップセレクター）の使用。

段落書式オプションを介して RTE で構造要素を使用できるので、AEM はアクセス可能なコンテンツの開発に適した基礎を提供します。コンテンツ作成者は、RTE を使用してフォントのサイズや色、その他の関連する属性を書式設定できないので、インライン書式設定は作成できません。代わりに、見出しなどの該当する構造要素を選択し、「スタイル」オプションから選択されたグローバルスタイルを使用する必要があります。これにより、独自のスタイルシートで閲覧するユーザーにとってはマークアップがクリーンになり、オプションも多くなるほか、コンテンツの構造が正確になります。

## ソース編集機能{#use-of-the-source-edit-feature}の使用

コンテンツ作成者が、RTE を使用して作成された HTML ソースコードを調査および調整することが必要になる場合があります。例えば、WCAG 2.0 を確実に準拠するため、RTE 内で作成されたコンテンツの一部で追加のマークアップが必要となることがあります。これをおこなうには、RTE の[ソースの編集](/help/sites-administering/rich-text-editor.md#aboutplugins)オプションを使用します。[ `sourceedit`機能は`misctools`プラグイン](/help/sites-administering/rich-text-editor.md#aboutplugins)で指定できます。

>[!CAUTION]
>
>`sourceedit` 機能の使用には十分に注意してください。タイピングの誤りやサポート対象外の機能は、問題を大きくする可能性があります。

## 追加のHTML要素と属性のサポート{#add-support-for-more-html-elements-and-attributes}

AEM のアクセシビリティ機能をさらに拡張するには、RTE に基づく既存のコンポーネント（**テキスト**&#x200B;コンポーネントや&#x200B;**テーブル**&#x200B;コンポーネント）を、要素や属性を追加して拡張することができます。

次の手順は、支援テクノロジーユーザーにデータテーブルに関する情報を提供する&#x200B;**Caption**&#x200B;要素を使用して、**Table**&#x200B;コンポーネントを拡張する方法を示しています。

### 例 — テーブルのプロパティダイアログにキャプションを追加する{#example-adding-the-caption-to-the-table-properties-dialog}

`TablePropertiesDialog`のコンストラクターに、キャプションの編集に使用する追加のテキスト入力フィールドを追加します。 `itemId`は`caption`（DOM属性の名前）に設定して、コンテンツを自動的に処理する必要があります。

**Table**&#x200B;で、DOM要素に対して属性を明示的に設定または削除します。 値は、`config`オブジェクトのダイアログによって渡されます。 DOM属性は、対応する`CQ.form.rte.Common`メソッド（ `com`は`CQ.form.rte.Common`のショートカット）を使用して設定または削除し、ブラウザー実装で一般的な問題が発生しないようにする必要があります。

>[!NOTE]
>
>この手順は、クラシックユーザーインターフェイスにのみ適しています。

### 例 — テキスト{#create-accessible-html-for-text}で強調を使用する場合にアクセシブルなHTMLを作成する

RTEでは、`b`および`i`の代わりに`strong`および`em`タグを使用できます。 次のノードを、ダイアログの`uiSettings`ノードと`rtePlugins`ノードの兄弟として追加します。

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

### 手順{#step-by-step-instructions}

1. 開始CRXDE Lite。 例：[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
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

1. `transferConfigToTable`メソッドの最後に次のコードを追加します。

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

1. **「すべて保存」を使用して変更を保存します。**

>[!NOTE]
>
>キャプション要素の値に使用できる入力タイプは、プレーンテキストフィールドだけではありません。 `getValue()`メソッドを使用してキャプションの値を提供するExtJSウィジェットを使用できます。
>
>追加の要素および属性用に編集機能を追加するには、以下の両方を確認します。
>
>* 対応する各フィールドの`itemId`プロパティを適切なDOM属性の名前(`TablePropertiesDialog`)に設定します。
>* DOM 要素で属性が設定／削除されていること（`Table`）。


>[!MORELIKETHIS]
>
>* [WCAG 2.0 クイックガイド](/help/managing/qg-wcag.md)
* [アクセシブルなコンテンツ（WCAG 2.0適合）の作成](/help/sites-authoring/creating-accessible-content.md)

