---
title: アクセシブルな web ページとサイトを作成するためのリッチテキストエディターの設定
description: アクセシブルな web ページとサイトを作成するためのリッチテキストエディターの設定
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 100%

---

# アクセシブルな web ページとサイトを作成するための RTE の設定 {#configure-rte-for-accessibility}

Adobe Experience Manager は、様々なアクセシビリティ標準に従ったユーザーフレンドリーなアクセシビリティ機能をサポートしています。また、開発者は、リッチテキストエディター（RTE）を使用する Experience Manager コンポーネントを使用して、アクセシブルなコンテンツを作成するのに役立つ機能を提供するようカスタマイズまたは拡張できます。

Web ページをデザインし、そのページにコンテンツを追加する際に、コンテンツ開発者や作成者は RTE の機能を使用してアクセシビリティ関連の情報を提供できます。例えば、見出しから段落要素に至るまでの構造情報を追加できます。

これらの機能を設定およびカスタマイズするには、コンポーネントの [RTE プラグインを設定](#configure-the-plugin-features)します。例えば、`paraformat` プラグインを使用すると、ブロックレベルのセマンティック要素を追加できます。具体的には、デフォルトで提供される基本の `H1`、`H2` および `H3` に加え、見出しレベルの数を拡張する機能がサポートされます。

RTE は、タッチ操作対応 UI とクラシック UI 用の様々なコンポーネントで使用できます。ただし、RTE を使用する主なコンポーネントは&#x200B;**テキスト**&#x200B;コンポーネントで、これは両方のインターフェイスで使用できます。次の画像は、`paraformat` をはじめ様々なプラグインが有効になっている RTE を示しています。

![タッチ操作対応 UI のフルスクリーンモードのテキストコンポーネント（RTE）](assets/chlimage_1-206.png)

*図：タッチ操作対応 UI のテキストコンポーネント*

![クラシック UI のテキストコンポーネントの編集ダイアログ（RTE）](assets/chlimage_1-207.png)

*図：クラシック UI のテキストコンポーネント*

様々なインターフェイスで利用できる RTE 機能の違いについては、[プラグインとその機能](/help/sites-administering/rich-text-editor.md#aboutplugins)を参照してください。

## プラグイン機能の設定 {#configure-the-plugin-features}

RTE の設定手順について詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)ページを参照してください。ここでは、次の主な手順を含め、すべての項目について説明します。

* [プラグインとその機能](/help/sites-administering/rich-text-editor.md#aboutplugins)
* [設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [プラグインのアクティベートと features プロパティの設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [RTE のその他の機能の設定](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

CRXDE Lite の適切な `rtePlugins` サブブランチ内でプラグインを設定することにより、そのプラグインのすべての機能または特定の機能をアクティベートできます。

![CRXDE Lite で rtePlugin の例を表示](assets/chlimage_1-208.png)

### 例 - RTE 選択フィールドで使用可能な段落形式を指定 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

意味的ブロックの新しい書式を選択可能にするには、次の手順を実行します。

1. 使用している RTE によって、[設定場所](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)を特定し、移動します。
1. [プラグインをアクティベート](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)することにより、[段落選択フィールドを有効](/help/sites-administering/rich-text-editor.md)にします。
1. [段落選択フィールドで使用可能にする書式を指定](/help/sites-administering/rich-text-editor.md)します。
1. これにより、コンテンツ作成者は、指定した段落書式を RTE の選択フィールドから選択できます。アクセス方法は次のとおりです。

   * タッチ操作対応 UI で段落記号アイコンを使用。
   * クラシック UI で「**フォーマット**」フィールド（ポップアップセレクター）を使用。

段落書式オプションを介して RTE で構造要素を使用できるので、AEM はアクセシブルなコンテンツの開発に適した基盤を提供します。コンテンツ作成者は、RTE を使用してフォントのサイズや色、その他の関連する属性を書式設定できないので、インライン書式設定は作成できません。代わりに、見出しなどの該当する構造要素を選択し、「スタイル」オプションから選択されるグローバルスタイルを使用する必要があります。これにより、独自のスタイルシートで閲覧するユーザーにとってはマークアップがクリーンになり、オプションも多くなるほか、コンテンツの構造が正確になります。

## ソース編集機能の使用 {#use-of-the-source-edit-feature}

コンテンツ作成者が、RTE を使用して作成された HTML ソースコードを調査および調整することが必要になる場合があります。例えば、WCAG 2.0 を確実に準拠するため、RTE 内で作成されたコンテンツの一部で追加のマークアップが必要となることがあります。これを行うには、RTE の[ソースの編集](/help/sites-administering/rich-text-editor.md#aboutplugins)オプションを使用します。[`sourceedit` 機能は `misctools` プラグイン](/help/sites-administering/rich-text-editor.md#aboutplugins)で指定できます。

>[!CAUTION]
>
>`sourceedit` 機能の使用には十分に注意してください。タイピングの誤りやサポート対象外の機能は、問題を大きくする可能性があります。

## その他の HTML 要素および属性のサポートを追加 {#add-support-for-more-html-elements-and-attributes}

AEM のアクセシビリティ機能をさらに拡張するには、RTE に基づく既存のコンポーネント（**テキスト**&#x200B;コンポーネントや&#x200B;**テーブル**&#x200B;コンポーネントなど）を、要素や属性を追加して拡張することができます。

以下の手順では、支援テクノロジーのユーザーにデータテーブルに関する情報を提供する&#x200B;**キャプション**&#x200B;要素で&#x200B;**テーブル**&#x200B;コンポーネントを拡張する方法について説明します。

### 例 - テーブルのプロパティダイアログへのキャプションの追加 {#example-adding-the-caption-to-the-table-properties-dialog}

`TablePropertiesDialog` のコンストラクターで、キャプションの編集に使用するテキスト入力フィールドを追加します。`itemId` は、コンテンツを自動的に処理するために、`caption`（つまり、DOM 属性の名前）に設定する必要がある点に注意してください。

**テーブル**&#x200B;で、DOM 要素に属性を明示的に設定したり削除したりします。値は、`config` オブジェクトのダイアログによって渡されます。DOM 属性は、ブラウザーの実装に伴う一般的な落とし穴を回避するために、対応する `CQ.form.rte.Common` メソッド（`com` は `CQ.form.rte.Common` のショートカット）を使用して、設定／削除する必要があります。

>[!NOTE]
>
>この手順は、クラシック UI のみに適しています。

### 例 - テキストで強調を使用する際のアクセシブルな HTML の作成 {#create-accessible-html-for-text}

RTE は `b` および `i` の代わりに `strong` および `em` タグを使用できます。次のノードを兄弟として、ダイアログの `uiSettings` および `rtePlugins` ノードに追加します。

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

1. CRXDE Lite を開始します。例：[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. コピー：

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   コピー先：

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >中間フォルダーが存在しない場合は、作成する必要があります。

1. コピー：

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   コピー先：

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 次のファイルを編集用に開きます（ダブルクリックで開く）。

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. `constructor` メソッドで、次の行を読み込む前に：

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

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`。

1. `transferConfigToTable` メソッドの最後に次のコードを追加します。

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

1. **すべて保存**&#x200B;を使用して変更を保存します。

>[!NOTE]
>
>キャプション要素の値に使用できる入力タイプは、プレーンテキストフィールドだけではありません。`getValue()` メソッドを通してキャプションの値を指定する任意の ExtJS ウィジェットを使用できます。
>
>追加の要素および属性用に編集機能を追加するには、以下の両方を確認します。
>
>* 対応する各フィールドの `itemId` プロパティが適切な DOM 属性の名前（`TablePropertiesDialog`）に設定されていること。
>* DOM 要素で属性が設定／削除されていること（`Table`）。


>[!MORELIKETHIS]
>
>* [WCAG 2.0 のクイックガイド](/help/managing/qg-wcag.md)
>* [アクセス可能なコンテンツ（WCAG 2.0 適合）の作成](/help/sites-authoring/creating-accessible-content.md)

