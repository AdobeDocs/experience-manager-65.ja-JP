---
title: CIF 製品およびカテゴリピッカーの使用
description: 顧客コマースコンポーネントで CIF 製品およびカテゴリピッカーを使用して、作成者やマーケターがコマース製品やカタログのデータを効率的に操作できるようにサポートする方法を説明します。
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 73%

---

# AEM Content &amp; Commerce Authoring ピッカー {#cif-pickers}

AEM Content &amp; Commerce Authoring には、AEM の作成者やマーケターがコマース製品のデータやカタログを効率的に操作するのに役立つ一連のオーサリングツールが用意されています。製品ピッカーとカテゴリピッカーは CIF アドオンの一部で、CIF コアコンポーネントで使用されます。プロジェクトでは、任意のコンポーネントダイアログでこれらのピッカーを使用して、製品やカテゴリを選択できます。

## 製品ピッカー {#product-picker}

プロジェクトコンポーネントで製品ピッカーを使用するには、開発者は `commerce/gui/components/common/cifproductfield` をコンポーネントダイアログに追加します。 例えば、cq:dialog: には以下を使用します。

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

「製品」フィールドでは、ユーザーが選択したい製品に対して、様々な表示を通じてナビゲーションを実行できます。 デフォルトでは、製品フィールドは製品の ID を返しますが、`selectionId` 属性を使用して設定できます。

製品ピッカーフィールドでは、次のオプションプロパティをサポートしています。

- selectionId (id, uid, sku, slug, combinedSlug, combinedSku) — ピッカーが返す製品属性を選択できます（デフォルト= id）。 sku を使用する場合は、選択した製品の sku が返され、combinedSku を使用する場合は、base#variant のような文字列と、基本製品および選択したバリアントの sku が返されます。基本製品が選択されている場合は、単一の sku が返されます。
- filter（folderOrProduct、folderOrProductOrVariant）- 製品ツリー内を移動する際にピッカーでレンダリングするコンテンツをフィルタリングします。folderOrProduct - フォルダーと製品をレンダリングします。folderOrProductOrVariant — フォルダー、製品および製品のバリアントをレンダリングします。 製品または製品バリアントがレンダリングされると、ピッカーで選択可能になります。 （デフォルトは folderOrProduct）。
- multiple（true、false）- 1 つまたは複数の製品の選択を有効にします（デフォルトは false）。
- emptyText - ピッカーフィールドの空のテキスト値を設定します。

また、次のような標準のダイアログフィールドプロパティ `name`, `fieldLabel`または `fieldDescription`、もサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントには クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、extraClientlibs プロパティを使用します。
>[!CAUTION]
>
>CIF コアコンポーネントのバージョン 2.0.0 以降、`id` のサポートは削除され、`uid` に置き換わりました。Adobeは、 `sku` または `slug` 製品 ID として。 Adobeは引き続きサポート `id` CIF コアコンポーネントバージョン 1.x を使用するプロジェクトの場合のみ。

完全に動作する `cifproductfield` の例は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)プロジェクトにあります。AEM コアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja#customizing-dialogs)も参照してください。

## カテゴリピッカー {#category-picker}

カテゴリピッカーは、製品ピッカーと同様の方法で、コンポーネントダイアログでも使用できます。

次のスニペットを cq:dialog 設定で使用できます。

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

カテゴリピッカーフィールドでは、次のオプションプロパティをサポートしています。

- selectionId(id, uid, slug, urlPath, idAndUrlPath _（非推奨）_, uidAndUrlPath _（非推奨）_) — ピッカーが返すカテゴリ属性を選択できます（デフォルト= id）。
- multiple（true、false）- 1 つまたは複数のカテゴリの選択を有効にします（デフォルトは false）。

また、次のような標準のダイアログフィールドプロパティ `name`, `fieldLabel`または `fieldDescription` もサポートされています。

>[!CAUTION]
>
>`cifproductfield` コンポーネントと同様に、`cifcategoryfield` コンポーネントにも クライアントライブラリが必要です。`cif.shell.picker`ダイアログにクライアントライブラリを追加するには、`extraClientlibs` プロパティを使用します。AEM コアコンポーネントドキュメントの[ダイアログのカスタマイズ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=ja#customizing-dialogs)を参照してください。
>[!CAUTION]
>
>CIF コアコンポーネントのバージョン 2.0.0 以降、`id` のサポートは削除され、`uid` に置き換わりました。Adobeは、 `uid` または `urlPath` をカテゴリ識別子として使用します。 Adobeは引き続きサポート `id` &amp; `idAndUrlPath` CIF コアコンポーネントバージョン 1.x を使用するプロジェクトの場合のみ。

完全に動作する `cifcategoryfield` の例は、[CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)プロジェクトにあります。
