---
title: ページプロパティの一括編集のためのページの設定
seo-title: ページプロパティの一括編集のためのページの設定
description: ページプロパティの一括編集を使用すると、複数のページのプロパティを一度に編集できます
seo-description: ページプロパティの一括編集を使用すると、複数のページのプロパティを一度に編集できます
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: d14688b17f47a2b1c11833eac10413d58276f6be
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 72%

---


# ページプロパティの一括編集のためのページの設定 {#configuring-your-page-for-bulk-editing-of-page-properties}

[ページプロパティの一括編集](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages)を使用すると、複数のページのプロパティを一度に編集できます。

異なる値が存在する可能性があるため、ページプロパティはデフォルトでバルク編集に対して有効になっていません。 明示的に許可（有効）する必要があります。 バルク編集で使用できるようにページプロパティを定義する場合は、次のような特定の意味を考慮する必要があります。

* ページタイトルなど、通常は一意なフィールドがあります。1 つの値が適用される場合に、そのようなフィールドの一括編集を有効にして意味があるかどうかを決断する必要があります。
* 特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。

   例えば、「発行の準備ができた」を示すチェックボックスです。 これは、バルク編集の前に複数の値を持つ場合があります（例：準備完了、レビュー中、進行中）。

>[!CAUTION]
>
>ページプロパティの一括編集には次の特徴があります。
>
>* クラシック UI では使用できません。
>* ライブコピー内のページでは使用できません。
>* リソースタイプが同じページでのみ使用できます。
>



>[!NOTE]
>
>Bulk editing is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for full information. You can customize the fields in the Bulk Metadata editor for Assets using the [Schema editor](/help/assets/metadata-schemas.md).

## フィールドの有効化 {#enabling-a-field}

>[!NOTE]
>
>特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。このため、次のフィールドタイプのみを有効にしてください。
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>



フィールドは、（テンプレートではなく）ページコンポーネントで有効化します。**

1. CRXDE Lite（または同等のメソッド）を使用して、ページコンポーネントを開きます。

   例：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >この例では、コアコンポーネントがインスタンスにインストールされ、インスタンスが We.Retail サンプルコンテンツと共に実行されていることを想定しています。詳しくは、[コアコンポーネントのドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)を参照してください。

1. Navigate to the required field within the `cq:dialog` definition.
1. フィールドノードで次のプロパティを定義します。

   * **名前**：`allowBulkEdit`
   * **Type**: `Boolean`
   * **値**: `true`
   例えば、標準的なページの[基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)の場合：

   `/libs/foundation/components/page`

   プロパティは次の場所で定義されます。

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
   >
   >`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
   >
   >設定およびその他の変更に推奨される方法は次のとおりです。
   >
   >    1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
   >    1. `/apps` 内で変更作業をおこないます。


1. 「**すべて保存**」を選択して更新内容を保持します。

