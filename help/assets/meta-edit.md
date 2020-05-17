---
title: メタデータの編集と追加
description: Learn about asset metadata in [!DNL Adobe Experience Manager Assets] an various ways by which you can edit asset metadata.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 33%

---


# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

Because organizations need controlled and reliable metadata vocabularies, [!DNL Experience Manager Assets] does not allow for on demand adding of new metadata properties. 作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。詳しくは、アセットのメタデータプロパティの [作成を参照してください](meta-edit.md#editing-metadata-schema)。

## Edit metadata for an asset {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * インター [!DNL Assets] フェイスでアセットを選択し、ツールバーの「 **[!UICONTROL 表示プロパティ]** 」をクリックします。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * From the asset page, click **[!UICONTROL View Properties]** ![chlimage_1-168](assets/chlimage_1-168.png) from the toolbar.
   アセットページには、すべてのアセットのメタデータが表示されます。 アセットがにアップロード（取り込む）されると、メタデータが抽出され [!DNL Experience Manager]ます。

   ![表示メタデータにアセットのプロパティを選択](assets/asset-metadata.png)

   *図： アセットの[!UICONTROL プロパティ]ページのメタデータを編集または追加します。*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。メタデータ書き込みワークフローは、元のバイナリにメタデータを追加します。 Changes made to the existing properties (such as `dc:title`) are overwritten and new properties (including custom properties like `cq:tags`) are added with the schema.

XMP write-back is supported and enabled for the platforms and file formats described in [technical requirements.](/help/sites-deploying/technical-requirements.md)

## Edit metadata schema {#editing-metadata-schema}

詳しくは、「メタデータスキーマフォームの [編集](metadata-schemas.md#edit-metadata-schema-forms)」を参照してください。

## カスタム名前空間を [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

You can add your own namespaces within [!DNL Experience Manager]. Just as there are predefined namespaces such as `cq`, `jcr`, and `sling`, you can have a namespace for your repository metadata and XML processing.

1. Go to the node type administration page `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Click **[!UICONTROL Namespaces]** at the top of the page. ウィンドウに名前空間管理ページが表示されます。

1. To add a namespace, click **[!UICONTROL New]** at the bottom.
1. XML名前空間の規則でカスタム名前空間を指定します。 URIの形式でIDを指定し、IDに関連付けられたプレフィックスを指定します。 「**[!UICONTROL 保存]**」をクリックします。
